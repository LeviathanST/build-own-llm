# What We Didn't Cover | Build Your Own LLM Workshop #23

**Build Your Own LLM Workshop — Video #23 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 16m 22s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=YdOsmHDeeLw |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to our
[00:02] final mini chapter section of building
[00:06] your own LLM. Here we're not really
[00:09] going to cover anything. You're just
[00:10] going to hear me ramble about all the
[00:12] stuff that we didn't cover. Why? Because
[00:14] I felt a sense of doom sending you out
[00:17] to the world not knowing what flash
[00:19] attention is, what KV caching is. I felt
[00:22] like we at least have to tell you that
[00:24] all this stuff exists so you can know
[00:26] what you need to do next. So the next
[00:29] few slides are going to be about
[00:30] everything that we're not talking about.
[00:32] So first then really the next three
[00:35] slides are about scaling up. We taught
[00:38] you how to build an LLM and pretending
[00:41] that we are in 2019. We don't know
[00:43] anything about scaling it up. But really
[00:45] if you want to scale it up, if you want
[00:47] to get like the billiondoll GPUs and all
[00:51] involved working together, there's a lot
[00:53] you're going to have to learn. Um, and I
[00:55] would say that's like the next big thing
[00:57] if you really want to build your own LLM
[00:59] or go work for a Neol, Frontier Lab,
[01:01] whatever.
[01:02] So there's 72 techniques of to optimize
[01:05] LM in production from daily dose DS
[01:07] here. We're def there's 72 of them.
[01:10] We're not covering any of them, but I
[01:12] want to give you a little taste of what
[01:14] they are. So first we and shared between
[01:17] training and inference for now. The next
[01:19] slide is going to be about each of
[01:20] these. Um, so TP distributes math models
[01:24] between GPUs.
[01:28] New architecture that was introduced,
[01:30] let's say December 2024. Realistically,
[01:33] no one noticed before March 2025. And
[01:36] then uh it's upgrading us from a uh a
[01:38] feed for network MLP that has all of it
[01:42] active dense to a sparse network that
[01:45] has a small portion of it active
[01:47] depending on the question. Really fun
[01:49] topic. MOE is really fun and definitely
[01:51] like the just state-of-the-art at this
[01:53] point. So, it's worth learning about it.
[01:55] EP says, "Now that I have all these
[01:57] experts, I might as well throw each
[01:59] expert on a GPU. Depending on which
[02:02] expert is active, depending on which
[02:04] sparse metrics I'm going to activate, I
[02:06] might as well go to that GPU instead of
[02:08] staying on the same GPU. So, we could do
[02:10] parallelization using that." PP is
[02:13] distributing uh different transformers
[02:16] between GPUs and machine. So, okay. So,
[02:18] I'm going to load the weights for layer
[02:20] 17 into this machine. It's going to use
[02:22] all of the GPU RAM because I'm a massive
[02:25] trillion parameter model. And this is
[02:27] it. I'm just going to have one GPU
[02:29] dedicated to layer 17. So, that's PP
[02:32] flash attention kind of shared between
[02:34] training and inference is just a way of
[02:37] having a super optimized attention
[02:39] kernel. That's the way that I think
[02:40] about it. It's like if you the way that
[02:44] we wrote all of our GPU code is not GPU
[02:46] optimized. Flash Attention very GPU
[02:49] optimized. A lot of the code samples
[02:51] that I linked to when we were talking
[02:53] about, hey, now you can read code
[02:55] samples for entire transformers did
[02:57] implement flash attention from scratch.
[02:59] I think I saw the latest implementation
[03:01] is flash attention three. Four is
[03:03] already out. Don't worry about it. Learn
[03:05] one and learn anything about flash
[03:07] attention is better than not. If you
[03:09] only learn two things on this list,
[03:10] learn about, learn about flash
[03:12] attention. Those are critical topics to
[03:15] know, I think.
[03:17] Uh, for example, I know that a few of
[03:19] the labs do ask you to just implement
[03:21] flash attention as part of their
[03:23] interview loop. So, they consider it to
[03:24] be pretty important and foundational
[03:27] training only scaling. So, now we're
[03:29] talking about how to train uh how to
[03:31] scale up training, not inference. I'm
[03:34] going to reach behind me and make the
[03:35] background real.
[03:38] We have the hugging face training book.
[03:41] The hugging face training book is
[03:43] phenomenal. This is one of my favorite
[03:45] books on the topic. And then it's going
[03:47] to explain all these topics to you, but
[03:49] I want to do a quick overview with you.
[03:52] Gradient checkpointing. So, one problem
[03:55] that we have is if we're going to do
[03:56] back propagation, we need to keep all of
[03:58] the feed forward alive. But if my
[04:01] network is massive in the hundreds of
[04:04] billions, no GPU can hold that alive,
[04:07] right? So I'm going to have to do
[04:09] something different. So the way gradient
[04:11] checkpointing works is it drops
[04:13] everything but the very last layer and
[04:15] then recomputes it as we do back
[04:17] propagation. Very fun technique to learn
[04:20] data parallelization as or parallelism
[04:23] as it goes to training only scaling,
[04:26] right? How do we shard the model's
[04:28] weights? the optimizers or states, the
[04:30] gradients or some combination of these
[04:32] across GPU. Most commonly FSDP or 0123
[04:37] 123 depends tells you if you're doing
[04:39] weights, optimizer states or gradients.
[04:41] FSDP can be easily implemented. It's
[04:44] built there's a PyTorch library for it
[04:46] or is it built into PyTorch right now,
[04:48] but you could really like bolt it on top
[04:50] of whatever training script you already
[04:52] have. uh SP sequence parallelism in
[04:56] training only is distributing everything
[04:58] that's not a math mole. So we were
[05:00] saying hey there's a form of tensor
[05:02] parallelism it distributes all the math
[05:04] moles across GPUs. SP distributes
[05:06] everything else. Softmax, norms,
[05:08] dropout, whatever you need to
[05:09] parallelize. CP context parallelism
[05:13] shards very long context between GPUs.
[05:15] Let's pretend that I want to support a
[05:17] 100 billion uh sorry 100 million context
[05:20] length. Right? If you hear Dario Amadi
[05:23] speaks about it, he says this is a
[05:25] solved problem. I'm like how? No GPU can
[05:28] hold it. The answer is context
[05:29] parallelism. We just use multiple GPUs
[05:32] for that mixed precision. I really think
[05:35] that you that I should have taught you
[05:37] this and I'm so sorry that I didn't.
[05:39] Realistically,
[05:40] we train our models in float 32. We'll
[05:43] talk about this a bit more in a moment,
[05:45] but we run a lot of our operations
[05:48] potentially in in 16 or 8 bit float.
[05:52] That saves a lot of memory that is very
[05:54] helpful to use more like use the GPU to
[05:57] hold more values, larger data, more
[06:00] values, bigger models, more
[06:01] capabilities. So I think mix precision
[06:03] if you choose one thing from this list
[06:05] go learn mixed precision. Distillation
[06:09] training a smaller model basing on the
[06:11] outputs of larger models really
[06:13] important. I think everyone does some
[06:15] amount of distillation at this scale. So
[06:17] worth knowing about distillation
[06:20] inference only scaling. I'm going to do
[06:22] this thing again where I make the
[06:23] background into a real thing.
[06:27] Philip's book really amazing. I really
[06:30] recommend it. It's slightly less
[06:33] technical in the sense that it's more
[06:34] approachable. Like it's not about the
[06:36] code and the concepts and the graphs and
[06:38] the diagrams. It's about teaching you
[06:40] how to take this massive model and put
[06:42] it in production in a way that makes
[06:44] sense. What are things we could do for
[06:46] that? First thing we could do is
[06:48] quantize. So let's say we trained our
[06:50] model in flow 32. It needs 32 bits. Can
[06:54] I run it at 16 bits, half as many bits,
[06:57] right? Can I? that gives me twice as
[07:00] many queries for that amount of bits.
[07:03] Another option is I can run it with FP8.
[07:07] I can run it with four, three, two, 1.4
[07:10] bits. So quantization runs the model at
[07:14] a lower precision with less memory
[07:16] footprint than the one we trained it in.
[07:18] KV caching, right? So like every time
[07:21] the model sees a sentence, it has to
[07:24] calculate the entire KV cache for the
[07:26] entire sentence just to see the next
[07:27] token. That kind of makes sense. But if
[07:30] all I want to do is then predict the
[07:32] next token after that, the next token
[07:33] after that, and next token after that,
[07:35] and I want to maybe do that in between
[07:37] sessions, you could just cache the KV
[07:40] section. So that's something we can do.
[07:42] And then like uh this a very common
[07:44] technique, speculative decoding. I'm
[07:47] pretty sure that's going to be just the
[07:48] wave of the future when it comes to
[07:51] optimizing inference. Uh instead of
[07:53] doing auto reggressive one token at a
[07:55] time, the models in a way can propose 4
[08:00] 8 16 options 2 4 8 16 options and then
[08:05] validate them all in one go. So if you
[08:08] win you get eight options, four options
[08:12] out of that one the cost of one
[08:14] inference. you if you lose you get
[08:17] nothing. So speculative decoding really
[08:20] interesting field that's coming along
[08:21] right now. Multi-node inference again
[08:24] when you have more than one u uh machine
[08:28] running using tensor parallelism so on
[08:31] like moving everything to different
[08:33] machine at inference time disagregation
[08:35] or prefilled decode is when you compute
[08:40] n known tokens you use high compute GPUs
[08:42] but when you're computing n +1 use high
[08:45] memory GPUs so when you're computing
[08:48] known tokens you you need high compute
[08:50] GPUs when you And plus when you compute
[08:53] new tokens the next token you have to
[08:55] use high memory GPUs. So for that you
[08:58] can actually do a prefilled decode
[09:00] disagregation. That's pretty common at
[09:02] this point. I'm pretty sure every
[09:04] inference engine has implemented that
[09:06] like and then maybe I'll throw some
[09:08] names of of inference engines like VLM
[09:10] now. Okay. So out of all of these if you
[09:13] learn something quantization Julia Tark
[09:16] has amazing amazing videos on that. The
[09:18] production quality is unbelievable. KV
[09:21] caching absolutely necessary to learn
[09:23] about and then I would say if you have
[09:25] time I would do disagregation training
[09:28] only scaling oh we did that AI safety
[09:32] for AI safety
[09:35] there's a couple of areas worth learning
[09:36] about I kind of just like this visual uh
[09:39] but it shows you the tree of all of the
[09:41] things that you're going to need to do
[09:42] to make your AI safe. This is just from
[09:45] a survey paper. So one op one thing
[09:48] you're going to need to know is
[09:49] alignment. How do you improve LLM's
[09:51] adherence to ideal behavior using
[09:53] techniques across the LLM training cycle
[09:55] premidost RL training? Right? Reduce
[09:59] inherent failures like psychophancy,
[10:01] hallucination, bias, inaccuracy,
[10:03] deceptive alignment. Honestly, reading
[10:05] writing that paragraph took me about an
[10:07] hour because there's no alignment on
[10:09] what the word alignment means. It's very
[10:12] confusing. I would say it's any
[10:14] technique you do at any point of the
[10:16] life cycle to make the model slightly
[10:18] safer for humans to use or slightly more
[10:21] helpful and slightly safer for the model
[10:24] to use. Next, you could learn about the
[10:26] field of mechanistic interpability. I
[10:28] adore this. This is the funnest stuff.
[10:31] I've actually tried putting as much of
[10:32] it I could into this workshop. It's
[10:35] looking at what's happening inside of
[10:36] LMS and trying to decipher why they do
[10:39] what they do. We are the farmers. We
[10:41] build a farm. The tomatoes do the
[10:43] growing. I also wouldn't mind being a
[10:45] molecular biologist trying to understand
[10:46] what's going on inside the cells of a
[10:48] tomato. LLM security. Honestly, very
[10:52] easy to subvert LLMs. Make get them do
[10:55] things they don't want to do. Let worth
[10:57] asking about, worth knowing a lot about.
[11:00] Red teaming, jailbreaking, defending
[11:01] against prompt injection. There's so
[11:03] much in LM security.
[11:06] Modifying LLMs after training. One of
[11:09] the big notions there is unlearning and
[11:12] it's very big in academia right now. How
[11:14] do we make an LLM model forget honestly
[11:17] we don't know how they know anything. So
[11:18] let alone how they to make them forget
[11:20] anything right now that feels not mostly
[11:23] productive is the polite way to say it.
[11:26] Editing models doing activation
[11:28] steering. Activation steering is I make
[11:30] the model less psychopentic after we're
[11:32] done training it. How do you do that?
[11:34] Activation steering and evaluations.
[11:36] There's a bunch of safety benchmarks.
[11:38] How do we know which models are safe to
[11:40] use? What does safety mean? You could
[11:42] see how AI safety really intersects
[11:44] every single thing we taught in this
[11:46] workshop.
[11:47] Great. So, there's a couple of decisions
[11:49] even though we're not teaching you
[11:50] anything new in this section that is
[11:52] worth because I needed to throw them
[11:53] somewhere in the slide deck and this is
[11:55] going to be the section where I put them
[11:56] in. Um, this is for our pre-training or
[11:59] instruct tuning in and our RL scripts.
[12:01] So decision number one is we're going to
[12:04] use TF32 to train instead of FB32
[12:08] because it's 3x faster. What does that
[12:10] mean? In front of you is the spec sheet
[12:13] for an Nvidia A100 GPU. And you could
[12:17] see that FB32 transit 19.5 teraflops
[12:23] whereas a tensor float transit
[12:26] 156 maybe 312 teraflops. massively
[12:31] faster. Let's just use that data type.
[12:34] Um, mix precision, we'll also do mix
[12:36] precision with BF-32 to get even double
[12:39] that performance. We can do double the
[12:42] teraflops. Love double flash attention.
[12:45] We'll use flash attention 2 for A100s,
[12:48] flash attention three for H100, and
[12:51] flash attention four. If you're running
[12:52] on a on a B200, you could just use flash
[12:56] attention two. We haven't explained what
[12:58] flash attention is. It's basically just
[13:00] an optimization for attention that's
[13:02] optimized to how specific kernels run.
[13:05] NMW used the fused kernel. We didn't
[13:08] explain what fused kernels are. I'm so
[13:09] sorry. Logit soft capping. It's another
[13:12] regularization technique that we didn't
[13:14] fully explain. We talked about value and
[13:16] gradient normalization. So think of
[13:18] logit soft capping as something similar
[13:20] to that. And gradient checkpointing.
[13:22] Don't do that for uh small uh GPT2 small
[13:27] training on an A100. we have enough room
[13:29] to keep the whole activation in memory.
[13:31] Okay, so I didn't teach you anything
[13:33] new, but this is just some stuff that
[13:35] the model has to know or like the RAI
[13:37] coding assistant has to know when it's
[13:38] coding up our LLM.
[13:41] We're done. This is our last slide. If
[13:43] you've stuck through it, well done. It's
[13:45] so much, right? But I want to give you a
[13:48] sense of hope and a sense of
[13:50] achievement. So let's do that. Yay. You
[13:53] as let's say a Pokemon have evolved and
[13:55] now you have new moves. What are these
[13:57] moves? Right? Number one is you can now
[14:00] build your own LLM. That's the name of
[14:02] this workshop. Build your own LLM.
[14:04] Right? You we've achieved that. You can
[14:06] go right now, look at this slide deck,
[14:09] write this code yourself, ask an AI
[14:11] coding assistant to build it for you.
[14:13] Whatever you could train on LMM, and I'm
[14:15] sure that if you listened and
[14:17] internalize these lessons, you could do
[14:19] that. Okay. What's the second thing you
[14:21] could do now? You could read every
[14:23] single LLM training code. Nano Chat,
[14:25] GPT, no magic AI, whatever
[14:29] implementation of standalone G uh um
[14:32] standalone AI chatbots you could find,
[14:34] LLMs, you can now go read it. At the
[14:37] very least, you'd know what you don't
[14:39] know. I don't know about flash
[14:40] attention. I don't know about uh KV
[14:43] caching, but you at least know 80 90% of
[14:46] the things around it, right? I don't
[14:48] know how to implement DPO myself.
[14:50] Everyone uses a library, right? But you
[14:52] can at least know what you don't know
[14:54] when you're reading it. And you're going
[14:56] to know most of it honestly because a
[14:57] lot of this stuff is repetitive. What
[14:59] else can you do that you couldn't do in
[15:01] the beginning of this workshop? You can
[15:03] review architecture diagrams for new
[15:05] models and recognize about 90% of the
[15:08] components. What does that mean? You
[15:10] could go open up Sebastian Rashka's LLM
[15:13] architecture diagram, look at any model
[15:15] that came out this year, and my
[15:17] goodness, you're going to be able to see
[15:18] what you know and what you don't know.
[15:20] and you're going to know like 80 or 90%
[15:22] of that. And finally, because I think
[15:24] some people who watch these workshops
[15:27] really want to like get hired and work
[15:29] in this. That totally makes sense. I
[15:31] would say that you are more hirable than
[15:33] you were before the workshop. But
[15:35] probably you're missing one really
[15:37] important thing. You need to know how to
[15:40] use GPUs to train and or run models and
[15:42] inference. So really worth thinking that
[15:45] if you do that you become to in my
[15:47] viewpoint hirable and in the viewpoint
[15:50] of like some very senior engineers
[15:52] who've written about this also hireable.
[15:55] So really worth thinking about it. So
[15:58] that's it. We're done. We've went
[16:00] through 23 sections, covered everything
[16:03] from ML model building to LLM
[16:06] architecture to pre-training to post-
[16:08] training to evaluations and finally all
[16:11] the stuff we didn't cover, which is GPU
[16:13] programming and safety and a few other
[16:14] things. I really hope you got a lot out
[16:17] of this. Thank you so much and enjoy
[16:19] yourself. Bye-bye.
