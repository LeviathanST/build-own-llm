# What We Didn't Cover

**Build Your Own LLM Workshop — Chapter 23 of 23**

| | |
|---|---|
| **Duration** | 16m 19s |
| **Video** | https://www.youtube.com/watch?v=YdOsmHDeeLw |

## Contents

- [Final Section Intro](#final-section-intro) (0:00)
- [Scaling Up Overview](#scaling-up-overview) (0:32)
- [Parallelism and MoE](#parallelism-and-moe) (1:21)
- [Flash Attention Basics](#flash-attention-basics) (2:31)
- [Training Scale Techniques](#training-scale-techniques) (3:27)
- [Memory and Sharding Tricks](#memory-and-sharding-tricks) (4:19)
- [Mixed Precision and Distillation](#mixed-precision-and-distillation) (5:33)
- [Inference Scaling Toolbox](#inference-scaling-toolbox) (6:20)
- [KV Cache and Decoding Speedups](#kv-cache-and-decoding-speedups) (7:18)
- [AI Safety Landscape](#ai-safety-landscape) (9:30)
- [Practical Training Decisions](#practical-training-decisions) (11:47)
- [Wrap Up and Next Steps](#wrap-up-and-next-steps) (13:41)

---

<a id="final-section-intro"></a>
### Final Section Intro

Hello everyone. Welcome back to our final mini chapter section of building

your own LLM. Here we're not really going to cover anything. You're going to hear me ramble about all the stuff that we didn't cover. Why? Because I felt a sense of doom sending you out to the world not knowing what flash attention is, what KV caching is. I felt we at least have to tell you that all this stuff exists so you can know what you need to do next. So the next few slides are going to be about everything that we're not talking about.

<a id="scaling-up-overview"></a>
### Scaling Up Overview

first then really the next three slides are about scaling up. We taught you how to build an LLM and pretending that we are in 2019. We don't know anything about scaling it up. But really if you want to scale it up, if you want to get the billiondoll GPUs and all

involved working together, there's a lot you're going to have to learn. Um, and I would say that's the next big thing if you really want to build your own LLM or go work for a Neol, Frontier Lab, whatever. So there's 72 techniques of to optimize LM in production from daily dose DS here. We're def there's 72 of them. We're not covering any of them, but I want to give you a little taste of what they are. So first we and shared between training and inference for now. The next slide is going to be about each of these. Um, so TP distributes math models

<a id="parallelism-and-moe"></a>
### Parallelism and MoE

between GPUs.

New architecture that was introduced, let's say December 2024. Realistically, no one noticed before March 2025. And then it's upgrading us from a feed for network MLP that has all of it flash attention kind of shared between training and inference is just a way of having a super optimized attention kernel. That's the way that I think about it. It's like if you the way that

active dense to a sparse network that has a small portion of it active depending on the question. Really fun topic. MOE is really fun and definitely the state-of-the-art at this point. So, it's worth learning about it. EP says, "Now that I have all these experts, I might as well throw each expert on a GPU. Depending on which expert is active, depending on which sparse metrics I'm going to activate, I might as well go to that GPU instead of staying on the same GPU. So, we could do parallelization using that." PP is distributing different transformers between GPUs and machine. So, okay. So, I'm going to load the weights for layer 17 into this machine. It's going to use all of the GPU RAM because I'm a massive trillion parameter model. And this is it. I'm going to have one GPU dedicated to layer 17. So, that's PP training only scaling. So, now we're talking about how to train uh how to scale up training, not inference. I'm going to reach behind me and make the background real.

<a id="flash-attention-basics"></a>
### Flash Attention Basics

we wrote all of our GPU code is not GPU optimized. Flash Attention very GPU optimized. A lot of the code samples that I linked to when we were talking about, hey, now you can read code samples for entire transformers did implement flash attention from scratch. I think I saw the latest implementation is flash attention three. Four is already out. Don't worry about it. Learn one and learn anything about flash attention is better than not. If you only learn two things on this list, learn about, learn about flash attention. Those are critical topics to know, I think. Uh, for example, I know that a few of the labs do ask you to implement flash attention as part of their interview loop. So, they consider it to be pretty important and foundational data parallelization as or parallelism as it goes to training only scaling, right? How do we shard the model's weights? the optimizers or states, the gradients or some combination of these across GPU. Most commonly FSDP or 0123

<a id="training-scale-techniques"></a>
### Training Scale Techniques

We have the hugging face training book. The hugging face training book is phenomenal. This is one of my favorite books on the topic. And then it's going to explain all these topics to you, but I want to do a quick overview with you. Gradient checkpointing. So, one problem that we have is if we're going to do back propagation, we need to keep all of the feed forward alive. But if my network is massive in the hundreds of billions, no GPU can hold that alive, right? So I'm going to have to do something different. So the way gradient checkpointing works is it drops everything but the very last layer and then recomputes it as we do back propagation. Very fun technique to learn

<a id="memory-and-sharding-tricks"></a>
### Memory and Sharding Tricks

123 depends tells you if you're doing weights, optimizer states or gradients. FSDP can be easily implemented. It's built there's a PyTorch library for it or is it built into PyTorch right now, but you could really bolt it on top of whatever training script you already have. SP sequence parallelism in

training only is distributing everything that's not a math mole. So we were saying hey there's a form of tensor parallelism it distributes all the math moles across GPUs. SP distributes everything else. Softmax, norms, dropout, whatever you need to parallelize. CP context parallelism that you that I should have taught you this and I'm so sorry that I didn't.

shards very long context between GPUs. Let's pretend that I want to support a 100 billion sorry 100 million context length. Right? If you hear Dario Amadi speaks about it, he says this is a solved problem. I'm how? No GPU can hold it. The answer is context parallelism. We use multiple GPUs for that mixed precision. I really think

<a id="mixed-precision-and-distillation"></a>
### Mixed Precision and Distillation

Realistically, we train our models in float 32. We'll talk about this a bit more in a moment, but we run a lot of our operations potentially in 16 or 8 bit float.

That saves a lot of memory that is very helpful to use more use the GPU to hold more values, larger data, more values, bigger models, more capabilities. So I think mix precision if you choose one thing from this list go learn mixed precision. Distillation inference only scaling. I'm going to do this thing again where I make the background into a real thing.

training a smaller model basing on the outputs of larger models really important. I think everyone does some amount of distillation at this scale. So worth knowing about distillation

<a id="inference-scaling-toolbox"></a>
### Inference Scaling Toolbox

Philip's book really amazing. I really recommend it. It's slightly less technical in the sense that it's more approachable. Like it's not about the code and the concepts and the graphs and the diagrams. It's about teaching you how to take this massive model and put it in production in a way that makes sense. What are things we could do for that? First thing we could do is quantize. So let's say we trained our model in flow 32. It needs 32 bits. Can

I run it at 16 bits, half as many bits, right? Can I? that gives me twice as many queries for that amount of bits. Another option is I can run it with FP8.

I can run it with four, three, two, 1.4 bits. So quantization runs the model at

a lower precision with less memory footprint than the one we trained it in.

<a id="kv-cache-and-decoding-speedups"></a>
### KV Cache and Decoding Speedups

KV caching, right? So every time the model sees a sentence, it has to calculate the entire KV cache for the entire sentence to see the next token. That makes sense. But if all I want to do is then predict the next token after that, the next token after that, and next token after that, and I want to maybe do that in between sessions, you could cache the KV section. So that's something we can do. And then this a very common technique, speculative decoding. I'm pretty sure that's going to be the wave of the future when it comes to optimizing inference. Uh instead of doing auto reggressive one token at a time, the models in a way can propose 4

8 16 options 2 4 8 16 options and then

validate them all in one go. So if you win you get eight options, four options

out of that one the cost of one inference. you if you lose you get nothing. So speculative decoding really interesting field that's coming along right now. Multi-node inference again when you have more than one u machine

running using tensor parallelism so on moving everything to different machine at inference time disagregation or prefilled decode is when you compute

n known tokens you use high compute GPUs but when you're computing n +1 use high memory GPUs so when you're computing known tokens you need high compute GPUs when you And plus when you compute new tokens the next token you have to use high memory GPUs. So for that you can actually do a prefilled decode disagregation. That's pretty common at this point. I'm pretty sure every inference engine has implemented that and then maybe I'll throw some names of inference engines VLM now. Okay. So out of all of these if you learn something quantization Julia Tark has amazing videos on that. The production quality is unbelievable. KV caching absolutely necessary to learn about and then I would say if you have time I would do disagregation training only scaling oh we did that AI safety

<a id="ai-safety-landscape"></a>
### AI Safety Landscape

for AI safety there's a couple of areas worth learning about I this visual but it shows you the tree of all of the things that you're going to need to do to make your AI safe. This is from a survey paper. So one op one thing you're going to need to know is alignment. How do you improve LLM's adherence to ideal behavior using techniques across the LLM training cycle premidost RL training? Right? Reduce

inherent failures psychophancy, hallucination, bias, inaccuracy, deceptive alignment. Honestly, reading writing that paragraph took me about an hour because there's no alignment on what the word alignment means. It's very confusing. I would say it's any technique you do at any point of the life cycle to make the model slightly safer for humans to use or slightly more helpful and slightly safer for the model to use. Next, you could learn about the field of mechanistic interpability. I adore this. This is the funnest stuff. I've actually tried putting as much of it I could into this workshop. It's looking at what's happening inside of LMS and trying to decipher why they do what they do. We are the farmers. We build a farm. The tomatoes do the growing. I also wouldn't mind being a molecular biologist trying to understand what's going on inside the cells of a tomato. LLM security. Honestly, very

easy to subvert LLMs. Make get them do things they don't want to do. Let worth asking about, worth knowing a lot about. Red teaming, jailbreaking, defending against prompt injection. There's so much in LM security. Modifying LLMs after training. One of the big notions there is unlearning and it's very big in academia right now. How do we make an LLM model forget honestly we don't know how they know anything. So let alone how they to make them forget anything right now that feels not mostly productive is the polite way to say it. Editing models doing activation steering. Activation steering is I make the model less psychopentic after we're done training it. How do you do that? Activation steering and evaluations. There's a bunch of safety benchmarks. How do we know which models are safe to use? What does safety mean? You could see how AI safety really intersects every single thing we taught in this workshop.

<a id="practical-training-decisions"></a>
### Practical Training Decisions

Great. So, there's a couple of decisions even though we're not teaching you anything new in this section that is worth because I needed to throw them somewhere in the slide deck and this is going to be the section where I put them in. Um, this is for our pre-training or instruct tuning in and our RL scripts. So decision number one is we're going to use TF32 to train instead of FB32

because it's 3x faster. What does that mean? In front of you is the spec sheet for an Nvidia A100 GPU. And you could

see that FB32 transit 19.5 teraflops

whereas a tensor float transit 156 maybe 312 teraflops. massively

faster. Let's use that data type. Um, mix precision, we'll also do mix precision with BF-32 to get even double that performance. We can do double the teraflops. Love double flash attention. We'll use flash attention 2 for A100s, flash attention three for H100, and flash attention four. If you're running on a on a B200, you could use flash

attention two. We haven't explained what flash attention is. It's basically an optimization for attention that's optimized to how specific kernels run. NMW used the fused kernel. We didn't explain what fused kernels are. I'm so sorry. Logit soft capping. It's another regularization technique that we didn't fully explain. We talked about value and gradient normalization. So think of logit soft capping as something similar to that. And gradient checkpointing. Don't do that for small GPT2 small

training on an A100. we have enough room to keep the whole activation in memory. Okay, so I didn't teach you anything new, but this is some stuff that the model has to know or the RAI coding assistant has to know when it's coding up our LLM.

<a id="wrap-up-and-next-steps"></a>
### Wrap Up and Next Steps

We're done. This is our last slide. If you've stuck through it, well done. It's so much, right? But I want to give you a sense of hope and a sense of achievement. So let's do that. Yay. You as let's say a Pokemon have evolved and now you have new moves. What are these moves? Right? Number one is you can now build your own LLM. That's the name of this workshop. Build your own LLM. Right? You we've achieved that. You can go right now, look at this slide deck, write this code yourself, ask an AI coding assistant to build it for you. Whatever you could train on LMM, and I'm sure that if you listened and internalize these lessons, you could do that. Okay. What's the second thing you could do now? You could read every single LLM training code. Nano Chat, GPT, no magic AI, whatever

implementation of standalone G standalone AI chatbots you could find, LLMs, you can now go read it. At the very least, you'd know what you don't know. I don't know about flash attention. I don't know about KV caching, but you at least know 80 90% of the things around it, right? I don't know how to implement DPO myself. Everyone uses a library, right? But you can at least know what you don't know when you're reading it. And you're going to know most of it honestly because a lot of this stuff is repetitive. What else can you do that you couldn't do in the beginning of this workshop? You can review architecture diagrams for new models and recognize about 90% of the components. What does that mean? You could go open up Sebastian Rashka's LLM architecture diagram, look at any model that came out this year, and my goodness, you're going to be able to see what you know and what you don't know. and you're going to know 80 or 90% of that. And finally, because I think some people who watch these workshops really want to get hired and work in this. That totally makes sense. I would say that you are more hirable than you were before the workshop. But probably you're missing one really important thing. You need to know how to use GPUs to train and or run models and inference. So really worth thinking that if you do that you become to in my viewpoint hirable and in the viewpoint of some very senior engineers who've written about this also hireable. So really worth thinking about it. So that's it. We're done. We've went through 23 sections, covered everything from ML model building to LLM architecture to pre-training to post- training to evaluations and finally all the stuff we didn't cover, which is GPU programming and safety and a few other things. I really hope you got a lot out of this. Thank you so much and enjoy yourself. Bye-bye.

