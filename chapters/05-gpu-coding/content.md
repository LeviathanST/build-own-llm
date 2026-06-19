# GPU Coding | Build Your Own LLM Workshop #5

**Build Your Own LLM Workshop — Video #5 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 21m 54s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=VVk6N1_rFD0 |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone, welcome back to a build
[00:02] your own LM workshop with me Justin
[00:04] Angel. I know what you're all wondering.
[00:06] Yes, I did put up my hair in a bun. This
[00:09] section is going to be about GPU
[00:10] performance.
[00:12] We previously implemented activation
[00:14] functions ourselves in like Excel, but
[00:17] we never saw code. Why is that? It's
[00:19] because
[00:22] we have to learn about how to write code
[00:24] in a way that's GPU performant. So, the
[00:26] first option we have is to implement
[00:29] things on the CPU in Python. So, like
[00:31] let's say the glue function that we saw
[00:33] earlier, if you don't know if you
[00:35] remember, the glue is this like really
[00:37] complicated activation function, right?
[00:39] It has this like X power 3 and multiply
[00:42] by
[00:43] by 0.04 and add back X again like lots
[00:46] of operations. So, we could just write
[00:48] it as like Python code and that would
[00:50] just work, right? Um so, what's the
[00:53] problem with writing CPU code? In a
[00:55] normal computer, let's say an i7,
[00:58] there's about four physical cores, let's
[01:00] say eight or seven hyper threaded. Um
[01:03] that's great if you want to calculate
[01:05] eight activation functions in parallel.
[01:08] You it could do super super well.
[01:11] Problem though
[01:13] is that we have our small language
[01:16] models at 124 million parameters. Let's
[01:19] say for just for like this part of the
[01:21] conversation, that means we're going to
[01:22] have to run the activation functions 124
[01:25] million times. That's going to be quite
[01:29] a lot to do on a CPU with only eight
[01:32] cores, right? So, not So, CPU is not so
[01:36] great when you only want to run things
[01:39] massive parallelization cuz there's just
[01:41] not enough physical CPU cores. Okay, so
[01:44] what's the next option? We can do
[01:46] something called PyTorch. What I we're
[01:48] not going to fully define PyTorch right
[01:50] now, but what does PyTorch give us for
[01:52] this part of the conversation? Well,
[01:54] PyTorch gives us two really important
[01:56] things in this conversation. It gives us
[01:59] the ability to have tensors, which is
[02:01] just a fun way of saying array that
[02:03] lives on the GPU.
[02:05] Tensor doesn't necessarily mean live on
[02:06] GPU, I'm just going to add that here.
[02:08] And then
[02:10] uh then it lets us run math operations
[02:12] on the GPU. Very fun. Hold data on the
[02:16] GPU and do math operations on the GPU.
[02:19] That's really useful for us. PyTorch
[02:21] also does a bunch of other things. It
[02:23] gives us a bunch of like built-in
[02:24] activation functions and other built-in
[02:27] things. It
[02:28] lets us do back propagation better. It
[02:30] does much, much more than that. We're
[02:32] not going to think about that in this
[02:34] part of the conversation. We're going to
[02:35] focus on one thing, which is how uh
[02:38] PyTorch gives us the ability to host
[02:39] data on the GPU and then perform math
[02:41] operations on the GPU.
[02:44] Here I wrote a custom PyTorch NN module.
[02:47] I just basically copied this the CPU
[02:50] code into it and then I'm going to run
[02:53] it in like something called a forward
[02:55] function. So, every NN module has a
[02:57] forward function when we run forward in
[02:59] the network, when we feed forward in the
[03:00] network. I created a tensor with like a
[03:03] few values and moved it to the GPU. You
[03:06] know it's in the GPU because it says the
[03:07] word CUDA on it. We'll cover what CUDA
[03:09] is in a moment. And then I said run all
[03:12] of this on the GPU by saying that CUDA
[03:15] and then it did. Okay, so how much
[03:17] faster can this possibly be? Well, if
[03:20] I'm running this on 32 million elements,
[03:23] right? The GPU is going to take 0.2
[03:25] milliseconds and the CPU is going to
[03:27] take 12 seconds. That's two orders of
[03:31] magnitude
[03:33] faster. 0.2
[03:35] 2 seconds
[03:37] 20 seconds, that's almost two orders of
[03:39] magnitude larger
[03:42] or faster than the CPU performs. We
[03:44] totally understand why that is. The like
[03:47] for example, an H100 GPU has 15,000
[03:50] parallel cores that could be used for
[03:52] math. And an A100 has a little less than
[03:55] that, but still has thousands of GPU
[03:57] cores. Not like the CPU and its four
[04:00] cores can't possibly compete with it.
[04:03] Can't possibly compete with it.
[04:07] Great. So, what's the problem that we
[04:09] created for ourselves by uh using NN
[04:12] modules as is? Well,
[04:15] GELU, if you remember, let's look at the
[04:17] formula again, has a lot of operation.
[04:19] Has that X power three, then addition
[04:22] with X, then it does a multiply uh does
[04:24] tanh, then it does another addition,
[04:26] then it does a multiplication, then it
[04:27] does another multiplication. So many
[04:30] things it does. The problem is that
[04:32] unoptimized, each one of those has to be
[04:35] moved from the CPU to the GPU executed
[04:39] in GPU, the results sent back to the
[04:41] CPU, then sent back to the GPU for more
[04:45] processing. This endless game of
[04:47] ping-pong between the CPU and GPU takes
[04:49] a lot longer, several orders of
[04:52] magnitudes, than just running the math
[04:54] on the GPU. The math on GPU isn't even
[04:57] the bottleneck for our performance
[04:58] anymore. It's the transferring of data
[05:01] between CPU and GPU and the various
[05:03] types of memories and buses that exist
[05:05] in between. We're not going to look at
[05:06] what those memories are. Those Those are
[05:09] very specific and they exist and we need
[05:10] to know them, but not right now. Okay,
[05:13] great. So, what does that mean that we
[05:14] had to do these eight transfers? Sorry,
[05:18] like these nine transfers. There's nine
[05:19] math operations that need transfers.
[05:23] Um so,
[05:25] that means that I'm going to have to pay
[05:26] the CPU-GPU networking penalty or like
[05:29] communication penalty nine times. It
[05:31] would be much better if I could pay it
[05:33] once, cuz the X is set. So, if I could
[05:36] just run X through that whole pipeline
[05:38] on the GPU, that would be much better.
[05:40] How do I do that? I can have this thing
[05:42] called a fused kernel. What does a fused
[05:45] kernel mean? If you ever listen to
[05:47] anyone in uh Frontier Lab, all they do
[05:49] is they write fused kernels, right?
[05:52] What's a fused kernel? It's just a way
[05:54] of saying, "I'm going to take all of the
[05:55] operations and I'm going to write them
[05:57] in one snippet of code that runs
[05:59] sequentially on the GPU." Okay, very
[06:02] very cool. That drops our needless
[06:06] GPU-CPU round trips. So, in Glu, when we
[06:09] have like nine math operations, uh
[06:12] that's really great. What's the easiest
[06:14] way for us to have a fused kernel?
[06:17] Easiest way? The easiest way? We could
[06:19] just take our custom NN module, call
[06:22] torch.compile on it. It fuses the kernel
[06:25] for us from nine kernels to one kernel,
[06:27] and now we can run it as one operation
[06:29] on the GPU. That's going to be a lot
[06:32] faster because we're saving the data
[06:33] transferring time between CPU and GPU
[06:35] and back. Okay. So, as you now have
[06:39] interpreted from my my somewhat
[06:41] pessimistic conversation style here,
[06:43] that we just generated another problems
[06:45] for ourself, right? What's the problem?
[06:48] Well, we did have to write the Glu
[06:50] function ourself. Actually, PyTorch just
[06:53] ships with a built-in Glu function. Why
[06:56] don't we just go ahead and use that? So,
[06:58] for example, there's NN ReLU and NN Glu
[07:01] and SiLU and Swish and Leaky ReLU and
[07:04] TanH and Sigmoid. All of those things
[07:06] are already built-in. Why would we code
[07:09] it ourself, right? Like
[07:11] we don't really need to.
[07:13] PyTorch ships with a fused kernel we
[07:15] could just use. They will run faster on
[07:19] most GPUs in most circumstances than
[07:21] your own home-built code unless you
[07:24] decide to write your own fused kernels
[07:26] in C++. Now, I'm foreshadowing that,
[07:31] and now I'm going to show it to you. Oh
[07:33] my goodness, this is what it looks like
[07:35] if I write my own fused kernel in C++.
[07:39] That looks a bit scary to me, right?
[07:41] It's a whole different programming
[07:42] language.
[07:43] It works with something called blocks
[07:45] and threads. Really not specific.
[07:48] There's a lot of implementation details
[07:50] that goes into CUDA C++. What is CUDA?
[07:53] CUDA is a cross NVIDIA GPU programming
[07:57] language. I'm kind of lying to you
[07:59] there, but let's let it can run on
[08:02] Yeah, doesn't necessarily run on all of
[08:04] GPUs and it doesn't necessarily run on
[08:05] all NVIDIA GPU just NVIDIA GPUs, but it
[08:10] lets us write cross GPU code. So, for
[08:12] example, if I'm writing for an A100 or
[08:13] an H100 or a B200, I can run my code on
[08:17] all of those with CUDA.
[08:19] NVIDIA has I think nine programming
[08:21] languages or nine options to code on
[08:23] their GPUs. Let's not get over fixated
[08:26] on CUDA, but CUDA is a really great
[08:28] example.
[08:29] Um if you're working in a frontier lab,
[08:31] you're probably not even using CUDA
[08:33] yourself. You're probably implementing
[08:34] one level beneath that to get like maybe
[08:37] another 5% of performance out of the
[08:39] GPU. But, you're not getting twice as
[08:41] fast. You're getting 5% extra. So, CUDA
[08:44] is a pretty good layer of abstraction
[08:45] for us to work in. Okay, really great.
[08:48] Uh maybe I should confess something. I
[08:50] don't know how to write CUDA C++ code. I
[08:53] just had Cloud write this.
[08:55] I'll confess something else. This is
[08:57] actually pretty bad CUDA code. It's not
[09:01] optimized to fully utilize uh something
[09:03] called tiling and a few other GPU
[09:06] architecture-specific concepts, which
[09:08] you have to take into account when
[09:09] you're writing your own CUDA C++ code.
[09:12] So, this is just the simplest
[09:13] translation I could have created, but
[09:15] it's definitely not production ready.
[09:17] What what can I do to maybe not use C++?
[09:21] That's a problem we just created for
[09:22] ourselves.
[09:24] We can use something called Triton. Uh
[09:26] Triton lets us keep writing Python code,
[09:29] and then we can uh and then it'll
[09:31] translate it for us to CUDA C++ code.
[09:33] This is maybe roughly kind of sort of
[09:36] equivalent to the C++ code we saw a
[09:38] moment ago. So, we don't have to learn
[09:41] C++, we don't have to learn CUDA
[09:42] directly. What we do have to learn is
[09:45] deep understanding of GPU coding. We
[09:47] have to understand how blocks works and
[09:49] tiling and so on and so forth. We'll
[09:51] learn here about these concepts in a
[09:53] moment. But I at this point, I think I
[09:55] ran you through six ways of writing
[09:57] code. I want to take a moment and maybe
[09:59] review them with you. Okay, so option
[10:01] one is we write on the CPU, not a lot of
[10:03] cores, works really great for four or
[10:05] eight
[10:06] parallel operations.
[10:08] Custom PyTorch works much better. We
[10:11] could now use the GPU with its 15,000
[10:14] parallel cores depending on our money
[10:16] budget. If we're not GPU poor,
[10:19] um
[10:20] we but then we created this problem for
[10:22] ourselves where we have a bunch of
[10:23] unfused kernels and we're doing a lot of
[10:25] round trips between the CPU and GPU. So,
[10:27] we could fuse them. Easiest option is
[10:29] PyTorch compile. Then we can we realize
[10:32] why would we write any of this code
[10:33] ourselves? Everyone uses the same
[10:35] activation functions, just use the
[10:36] built-in PyTorch ones. But if we wanted
[10:39] to know how the built-in PyTorch ones
[10:41] are implemented, we could look at CUDA
[10:42] C++. So, that's like writing much closer
[10:46] to the metal than writing in Python
[10:48] unless we write in Triton or another
[10:51] like intermediary.
[10:53] And then then if we have deep
[10:55] understanding of CPU of GPU code, then
[10:58] we can uh
[11:00] uh uh build somewhat or very performant
[11:04] Python code. Okay, so are there only six
[11:06] levels, Justin? No, there's many more.
[11:08] There's many options from each of the
[11:10] GPU TPU providers. There's uh other
[11:14] options like JAX available. I don't
[11:16] think you should really focus in on the
[11:18] specific ones, but understand there's
[11:20] different levels you could write in.
[11:22] Okay, great. So, now we know these six
[11:24] options, which one of them is faster,
[11:26] Justin? You I I'm guessing it's the C++
[11:30] code. Well, okay, so we totally removed
[11:32] CPU from this chart cuz it would be like
[11:34] a hundred times slower. Why would we
[11:36] even look at the anything on this chart?
[11:38] So, the slowest option is just writing a
[11:40] PyTorch custom module that has nine
[11:43] unfused kernels for GELU.
[11:45] Uh as soon as I torch compile and I fuse
[11:47] kernels, oh my god, this is like order
[11:50] of magnitude faster-ish.
[11:53] Uh almost
[11:58] eight times faster to run this in a
[12:01] fused kernel. That tells us a lot. By
[12:04] the way, let's explain what this chart
[12:05] is. There's like groups in the base in
[12:08] the middle here. That's how big our
[12:09] two-dimensional tensor ends up being, or
[12:12] just I think it's a one-dimensional
[12:13] two-dimensional. Uh but that's how big
[12:16] the tensors we're going to send down or
[12:18] arrays to the GPU are. So, you could see
[12:21] there's not a lot of difference between
[12:22] PyTorch custom modules at the small
[12:25] tensor array sizes, but when you get to
[12:27] the really big ones from 32K to 32
[12:30] million, there's a huge difference
[12:32] between custom PyTorch
[12:34] uh
[12:35] PyTorch
[12:36] uh
[12:36] uh custom modules and torch compile.
[12:39] Like just fusing the kernels really
[12:40] bought us a lot of performance. But, we
[12:43] can also clearly see that really neither
[12:45] of those options is going to be as fast
[12:48] as either using the built-in PyTorch
[12:51] uh activation function, CUDA C++, or
[12:54] Triton. So, PyTorch custom module is the
[12:56] slowest option, but at least it works a
[12:59] hundred times faster than the CPU code,
[13:01] then followed by torch compile, which is
[13:03] the second slowest. Why is that? Cuz
[13:05] PyTorch compile because torch compile is
[13:08] still very slow compared to really
[13:10] optimized GPU code.
[13:13] So, let's remove Py- let's make PyTorch
[13:16] compile our baseline, our 1x, and look
[13:19] at that chart again. So, that's just
[13:20] like kind of inverting the chart using
[13:22] PyTorch compile as our 1 uh x function.
[13:26] How much faster are all of the other
[13:28] options than PyTorch compile? Well, uh
[13:32] the uh you could see that the built-in
[13:35] PyTorch GELU is about 5.7 times faster
[13:38] than it at 32,000 items, but uh CUDA C++
[13:43] kind of breaks out and is a lot faster,
[13:44] but Triton is a little bit slower,
[13:47] right? And then but we we go to the
[13:49] massive metric sizes, oh my goodness,
[13:52] uh even PyTorch compile is like four
[13:54] times slower than it used to be.
[13:57] Uh but
[13:59] uh the then uh the NN module,
[14:03] uh but you could kind of see that Triton
[14:05] CUDA C++ and the built-in function are
[14:08] all kind of the same. Maybe CUDA C++ is
[14:10] a tiny bit faster, but not a lot faster.
[14:13] This brings us back and mail is an
[14:15] empirical field. We use the components
[14:17] that work fastest, bestest, most
[14:19] efficiently, right? So, now you can kind
[14:21] of guess which one we're going to use.
[14:23] We're going to use PyTorch.compile
[14:25] because I want to keep our code super
[14:26] readable. But, if you're really trying
[14:28] to save find a place to save some GPU uh
[14:31] bandwidth and with it money, it'd be
[14:33] really smart to look at these other
[14:35] options, which we're not going to do
[14:37] here today.
[14:39] This is an empty slide, and after this
[14:41] empty slide, there's the uh a slide that
[14:44] says, "Hey, do you want to learn more
[14:45] about performant code?" We're not going
[14:47] to do any more of that here today. Uh
[14:50] there's a lot of concepts you should
[14:52] learn about how GPUs work when you write
[14:54] code for them, stuff like tiling and
[14:56] loading and occupancy and the block size
[14:58] of those and how do you do memory
[14:59] alignment and so on. That's a whole day
[15:01] workshop that we're not going to get to
[15:03] here today.
[15:04] Um so, where would I start? I would
[15:06] start by like saying, "Do I want to
[15:08] learn this or not? Should I have an AI
[15:10] write this for me?" AIs still don't
[15:13] write great kernels. They're just not
[15:14] super great at that yet yet.
[15:17] Uh so, a place to start is by watching
[15:19] the Stanford lecture on the the specific
[15:21] construction of GPUs, what are the
[15:24] cores, what is the memory type of
[15:26] memories we have. That's going to get
[15:27] you pretty far into this game, but
[15:29] there's a lot more complexity. So,
[15:31] there's three books I would recommend
[15:32] here. I'm going to grab them from my
[15:34] shelf live in real time. Oh my goodness,
[15:37] what's he doing? He's grabbing inference
[15:39] engineering by Philip Key. He was so
[15:42] kindly He was so nice to send me a
[15:44] signed copy from him. Wow, Phil, you
[15:46] really signed this. Thank you so much.
[15:48] It's a great book to learn about how to
[15:50] work with GPUs in production in in
[15:53] inference time. If you want to learn how
[15:56] to work with GPUs at training time,
[16:00] I would get the ultra scale book from
[16:04] hugging face. It's phenomenal. Both of
[16:07] these, by the way, are available as free
[16:08] PDFs. You don't have to buy the physical
[16:10] books. I'm just old and like having
[16:13] physical books. A third book that you
[16:16] can read
[16:20] is this book by Chris who was wandering
[16:23] around NeurIPS last year when this book
[16:25] came out in December. This is like a few
[16:27] months ago and giving copies away. Such
[16:30] an Such a nice gesture. Okay, great. So,
[16:34] we have three books that we can read
[16:37] about how to really scale up and use
[16:39] GPUs. This is going to be maybe almost
[16:42] the last time we're going to mention
[16:43] GPUs until very far later on in the day.
[16:47] FYI, there's just a lot of optimizations
[16:49] you're going to to do for GPUs. That's a
[16:50] whole different day workshop, but it is
[16:53] the key skill if you want to work at a
[16:55] neo lab or frontier lab. Those are going
[16:58] to be really really useful for you to
[17:00] know.
[17:01] There's a lot of complexity there.
[17:02] There's a lot of concepts that are GPU
[17:04] specific concepts like flash attention
[17:07] and KV caching and so on that were are
[17:09] not covered in today's workshop, but are
[17:11] worth thinking about from a GPU lens.
[17:13] But you don't need those concepts to get
[17:15] a basic GPT-2 style transformer up and
[17:17] running, so they're not getting covered
[17:19] today. I really want to be up front
[17:20] about that.
[17:22] Great. So, let's say you did want to
[17:24] write a little bit of code here in this
[17:26] one section. I think that would be
[17:28] really useful for you. I went ahead and
[17:30] implemented the GELU
[17:33] activation function we saw, and all of
[17:35] the code is available here in Colab. So,
[17:37] you've got
[17:39] the math for GELU on a CPU, and you've
[17:42] got the custom module in uh PyTorch. And
[17:46] then you could see me call using
[17:48] torch.compile on it. And then you could
[17:51] see me using the built-in PyTorch
[17:54] activation function. And then here's the
[17:56] CUDA C++ code for it. And you could see
[17:59] that we have to wrap it in a loading
[18:01] line cuz we have to use a C++ function.
[18:03] And then you could see the Triton kernel
[18:05] code, and there's so many more things we
[18:07] could see here, right? Like we could
[18:09] have gone to JAX and a bunch of other
[18:11] stuff to work better on TPUs and so on.
[18:13] But then there's a performance
[18:14] comparison. I'm not going to You don't
[18:16] have to see this code. I'm not going to
[18:17] run you through it. But what's important
[18:19] is let's look at the outcomes. Wow,
[18:21] these are the charts that we saw in the
[18:23] slide deck. It's like I totally
[18:24] generated them here in PyTorch in Colab.
[18:29] So, this These are the differences in
[18:31] absolute time for runs. That's what we
[18:32] saw earlier. Also, I don't know if you
[18:35] remember there was a chart that showed
[18:37] us CPU versus GPU time. So, that also
[18:39] came from this Colab notebook. And
[18:41] finally, the number of kernels. Oh my
[18:45] goodness, one versus nine kernels. All
[18:47] of these came from these Colab notebook.
[18:49] Okay, great. So, what's your exercise?
[18:52] One option is you could just take this
[18:54] notebook and duplicate it and try and
[18:56] implement ReLU or ReLU squared. You're
[18:58] going to learn a lot.
[19:00] You don't have to write the C++ code if
[19:02] you don't want to cuz I didn't teach it
[19:03] to you, but you could get pretty far
[19:05] into that game. You could also ask your
[19:07] friendly AI to help you. So, one option
[19:09] is you could download this entire
[19:11] notebook. You could give it to Claude or
[19:13] whatever. You could say generate a
[19:14] collab a collab notebook demonstrating
[19:17] single input perceptrons at six levels.
[19:20] Um Python CP CPU code, PyTorch custom
[19:24] modules, PyTorch compile, the built-in
[19:27] NN modules, CUDA C++, and Triton code,
[19:30] and then compare the performance. So,
[19:31] that's another way of doing that. I did
[19:34] that. I just gave it this prompt, and I
[19:36] said, "Actually, I want you to do the
[19:38] ReLU function." I had to add that to the
[19:40] prompt.
[19:42] Um and then
[19:44] um a perceptron with ReLU, right? And
[19:47] then I said, "Generate that for ReLU."
[19:49] And this is the code that it came out
[19:50] with. Uh so, here you go. Sorry,
[19:52] actually, this is the code for sigmoid.
[19:54] So, this is the sigmoid activation
[19:56] function. We didn't actually look at it
[19:58] too intensely. It has a formula, right?
[20:00] Um but then it implementing the code on
[20:03] CPU, it's implementing it here on a
[20:06] custom module. Here, it implements it
[20:08] with torch compile. Here it is in a
[20:11] custom
[20:13] torch NN the built-in torch NN. You
[20:16] could see it's using NN sigmoid here.
[20:19] You could uh then implement it in CUDA
[20:21] C++, and then finally, you can implement
[20:23] it in a Triton kernel. And then we can
[20:26] compare performance and see which one of
[20:28] these performs better. Okay, really
[20:30] great. So, you could choose how you want
[20:31] to do this exercise. Do you want to go
[20:32] and just write code yourself, or do you
[20:35] want to go have an AI do that? Both of
[20:37] those, I think, are valid as long as you
[20:38] understand the difference of the
[20:40] different levels. CPU is slowest, and
[20:43] then there was a bunch of options that
[20:45] are faster as we bring in more and more
[20:46] and more features as we write code. When
[20:49] I write code, I have to keep those in
[20:51] mind, right? It's easier to write CPU
[20:53] code, but it's not fast. Right, what do
[20:55] I want to use here? For our
[20:58] uh for our
[21:00] uh sample script, we're going to use
[21:02] pytorch.compile cuz I think it just
[21:03] makes for really readable code, even
[21:06] though it's not the fastest option to
[21:07] run on GPUs. So, by making that
[21:09] decision, I'm in fact saying I probably
[21:11] want my GPU bill to be twice as high. I
[21:15] am physically paying twice as much money
[21:17] to run the same script. Just FYI here.
[21:20] Okay, great. Uh so, we covered
[21:22] activation functions. Next up is going
[21:25] to be MLPs and feedforward networks.
[21:28] Uh why is that the next thing we're
[21:30] building up? Cuz so far, we've only seen
[21:32] one perceptron. And we said we need 100
[21:35] billion of them to run uh
[21:38] a chatbot. So, in order to get there, we
[21:41] need to like start building up layers
[21:43] and layers of perceptrons. That's going
[21:45] to be MLP feedforward networks, whatever
[21:47] we want to call them. Okay, awesome.
[21:49] I'll see you in the next section on this
[21:51] topic.
