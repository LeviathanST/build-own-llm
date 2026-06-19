# Reverse Engineering Large Language Model | Build Your Own LLM Workshop #2

**Build Your Own LLM Workshop — Video #2 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 15m 32s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=E0rkgxwhz5g |

## Description

No description available.

---

## Full Transcript

[00:01] Hello everyone, welcome back to our
[00:03] build your own large language model
[00:05] workshop. We're going to be in our
[00:07] second section right now called reverse
[00:09] engineering LLMs. And our goal for this
[00:12] section is to get a road map for how to
[00:14] build large language models. We just
[00:17] don't know. So in our previous module,
[00:20] what we saw is running GPT-2 inside of a
[00:24] collab notebook. And maybe the key
[00:26] insight here is that we could probably
[00:30] uh figure out from that in-memory model
[00:34] how to structure our workshop today. So
[00:36] maybe we could do something to like
[00:38] reverse engineer that model and get a
[00:40] lot of the runtime components at least,
[00:42] the inference time components
[00:44] from that model.
[00:46] So how would we do that? Here on the
[00:47] left, we've got an example.
[00:49] It says print model. So all we're going
[00:52] to do is call the print method on the
[00:54] model. And then there's a bunch of words
[00:55] that happen here. I think we should
[00:57] review those words very carefully and
[00:59] see maybe they give us a hand as to what
[01:01] we need for our workshop. So again, all
[01:03] we're doing here is reverse engineering
[01:05] the GPT-2 model to figure out what
[01:07] inference time components we need in
[01:09] order to build a GPT-2 style
[01:11] transformer, which seems pretty
[01:12] straightforward. Great. So let's just
[01:14] jump straight into code. And again, like
[01:17] we've seen collab notebooks in the past.
[01:19] So I'm not going to necessarily run you
[01:21] through these again. We click connect,
[01:22] we click run all. Oh my gosh. Great.
[01:24] I've already done that, so you don't
[01:26] have to wait with me. So the first thing
[01:28] we're going to do is we're going to load
[01:30] GPT-2 right here. And then I'm going to
[01:33] say
[01:34] that we just have the model here. So
[01:37] like the whole thing is loaded. And then
[01:39] first thing I'm going to do is I'm going
[01:40] to try and print out the total number of
[01:41] parameters. What's a parameter? I don't
[01:43] even know right now. Maybe when we learn
[01:45] about perceptrons, we learn about
[01:47] parameters. But for now, let's think of
[01:49] it as a unit of size for a model. And
[01:52] GPT-2 small came out at about 124
[01:55] million.
[01:57] Is 124 million a lot? It's more than a
[02:00] few million and it's a lot less than a
[02:02] few billions. That's kind of the order
[02:03] of magnitude that we want to think
[02:04] about. But yes, it's very small based on
[02:07] modern standards. It's roughly the size
[02:10] of a small test. Great. So now we have
[02:13] the model in memory. Can I just call
[02:15] print model on it? Yes, I can. And then
[02:18] we see a bunch of words here. I am not
[02:20] going to explain what the words mean,
[02:21] but I'm going to highlight the words
[02:23] that we saw. And then we're going to
[02:25] explain them later on in future
[02:26] sections. So what are some words we're
[02:28] seeing here? We're seeing the word
[02:29] transformer. That's a real interesting
[02:31] word for those of us who know a little
[02:32] bit about large language models. Words
[02:34] like embedding. We see words like
[02:36] dropout and layer norm and linear here
[02:39] in the base. And we see a word here
[02:42] that's
[02:43] dropout again and new glue activation. I
[02:46] said glue cuz I think it's funny. You
[02:48] think you're supposed to pronounce it
[02:49] galoo or gayloo? Something like that. I
[02:52] say glue cuz I think it's funny. Uh we
[02:54] have dropout here. So on. Okay, so we
[02:57] saw a bunch of words. I don't know what
[02:58] those words mean. Maybe we'll see them
[03:00] again in a moment. Let's try and use
[03:02] something called torch info and call the
[03:04] summary method. Very similar to just
[03:06] calling print, just like a little bit
[03:08] nicer. So what's obvious from this? We
[03:11] have very similar blocks to before, but
[03:13] now we see GPT-2 block repeat itself 12
[03:16] times. That's really interesting. We
[03:19] learned that there's 12 layers or 12 GPT
[03:22] blocks within a transformer. We just
[03:24] learned something really interesting.
[03:27] Um great. And that kind of gives us the
[03:29] math of how we got to the number of
[03:31] parameters we have we had earlier. And
[03:33] the difference between 124 million and
[03:35] 163 million is whether or not you count
[03:36] the embeddings, which we do. In this one
[03:39] example, we will count the embeddings.
[03:41] Okay, great. So now I know stuff. I've
[03:44] printed out some words. I've called
[03:47] print. I've called summary. Let's try
[03:49] and reverse engineer the modules we just
[03:51] saw. We're just going to print them out
[03:52] in pretty print here to make it easier
[03:54] to read. These are the words we saw
[03:56] earlier. It's conv1d and drop and
[03:58] embedding and attention. Oh, attention.
[04:00] And layer norm and linears and gelu
[04:03] activation. Wow, it's all that stuff we
[04:05] saw a moment ago. Just a nicer list.
[04:07] Let's throw that into a graph. This is
[04:09] just me trying to render the graph in a
[04:11] way that makes sense to me. The
[04:12] hierarchy starts kind of making sense to
[04:15] me now. So, there's this thing called
[04:16] the model and it's got a transformer
[04:18] inside of it and inside of it there's
[04:19] embeddings and dropouts and module list
[04:22] layers. And this these layers repeat
[04:24] themselves 12 times and inside of them
[04:26] there's something called an attention.
[04:27] Inside of them there's something called
[04:28] an MLP. What's an attention? What's an
[04:30] MLP? We don't know yet. Great. Inside of
[04:34] those there's dropout, conv1d, gelu
[04:36] activation, layer norm, so on and so
[04:38] forth.
[04:39] Great. So, let's try and us take those
[04:41] words we just saw a moment ago and try
[04:43] and attribute them to something that
[04:45] looks like a road map for us to reverse
[04:47] engineer and like learn concepts. So,
[04:50] okay, we learned the word transformer.
[04:52] So, that's going to be section 18. We
[04:53] have to really build up to get there. We
[04:55] saw the word embedding, that's section
[04:57] 16. We saw dropout, that's a part of
[04:59] section 13. These are all sections we're
[05:01] going to be working on in our workshop.
[05:03] We saw layer norm, that's going to
[05:05] become part of normalization. We
[05:08] kind of intuitive on something called
[05:09] residuals. We need those as well. We saw
[05:12] normalization. We heard the word MLP.
[05:15] Huh, that's a fun word. We're going to
[05:17] spend a lot of of our second module
[05:20] learning the basics of machine learning
[05:21] building up to learning about MLPs and
[05:24] feedforward networks. We saw gelu
[05:26] activation, that's going to be almost
[05:27] our next section. Not the next section,
[05:30] but the next next section. So, we're
[05:32] going to talk about a lot of activation
[05:33] functions. Okay, so is there something
[05:35] beyond this little tree that is now a
[05:37] lot more visual and it's got more
[05:38] colors. There's also something called
[05:40] functions. So, those are invisible in
[05:42] the module tree. We don't need to know
[05:44] why or what the difference is. So,
[05:46] there's a lot of functions being called
[05:47] as part of our model, but when we pretty
[05:50] print them, what we get to is there's
[05:51] activation functions, initialization,
[05:54] really interesting. We also have
[05:56] normalization, and then we see something
[05:58] called softmax. So, that's section 14.
[06:01] Okay, so really cool. We learned about
[06:03] We have a lot more sections that we're
[06:05] going to have to cover than we would
[06:06] normally have to cover, right? Like cuz
[06:08] now we have softmax and embeddings and
[06:11] all of that stuff.
[06:13] Let's try to throw that into a tree just
[06:15] so we can understand what the function
[06:17] tree looks like. Oh my god, an
[06:19] In-Context Transformer is just a bunch
[06:21] of functions being called over and over
[06:24] and over again. Transformer, MLP
[06:25] Transformer,
[06:27] attention MLP, attention MLP, attention
[06:29] MLP, attention MLP, attention MLP. Oh my
[06:31] god, we're calling these
[06:33] 12 times. We're going to scroll to the
[06:34] bottom, and then we get to the end of
[06:36] this. Okay, so what did we just learn?
[06:39] A large language model is a bunch of
[06:40] functions. Really cool.
[06:42] Uh so, let's bring out the architecture.
[06:44] This is an exercise for you. Go to
[06:46] Hugging Face.
[06:49] Go to Hugging Face and choose a text
[06:52] generation model, and then maybe a small
[06:54] one so we could load into a GPU. But,
[06:56] let's say 6 billion, maybe 12 billion
[06:58] model, maybe no more than 32 billion.
[07:00] We're going to have to start with some
[07:01] problems to load them. So, let's say I
[07:03] go here and I try and choose one of
[07:05] these models. One second, and I'm going
[07:07] to scroll back down. And then ideally
[07:09] for us, we probably want to run these in
[07:10] PyTorch as well. And there's a couple of
[07:12] models here. Let's say I want to load up
[07:14] Tiny LLaMA.
[07:16] Uh that's just the name of like of a uh
[07:19] smaller LLaMA-style model. One 1.1
[07:22] billion parameters, so about five times
[07:24] bigger than the Sorry, 10 times bigger
[07:26] than the model we're working with on
[07:27] right now. GPT-2 small. And then I'm
[07:30] going to just give it the name, and I'm
[07:31] going to just load it like we saw a
[07:33] second ago. I'm going to go print, and
[07:35] I'm going to click summary. And then now
[07:38] we get to see a totally different model
[07:40] than GPT-2. This is LLaMA model. Wow,
[07:43] what does it have? It has attention
[07:45] layers like we saw a moment ago and it
[07:47] has embedding layers and we have linear
[07:49] layers and it still has an MLP and it
[07:52] still has an attention layer. Really
[07:54] cool. Has a
[07:55] RMS norm. What's an RMS norm? I don't
[07:58] know. A rotary embedding positional
[08:01] embedding. That's going to be real
[08:02] important when we get to section
[08:04] 14, I think, 15.
[08:08] Great. So, now you can go and choose any
[08:10] model from here and try and copy the
[08:12] name into your code block and then see
[08:14] if you can't print that model. I think
[08:17] that's going to be a real fun exercise
[08:18] for you to feel empowered. Great. So, we
[08:21] did that. That's the code for this and
[08:23] then we reverse engineered our roadmap
[08:25] for the day. So, we have activation
[08:27] functions and transformers and dropout,
[08:30] which is regularization, and residuals
[08:32] and attention and normalization. And now
[08:34] we get kind of getting very close to
[08:36] having a roadmap for the day. But, a lot
[08:38] of these are
[08:39] uh part of the architecture of large
[08:41] language models, but they're not the
[08:43] foundational buildings to how to train a
[08:45] large language model. So, for that we
[08:46] need a couple more things.
[08:48] And before we get to that, I actually
[08:49] want to talk a little bit about ablation
[08:51] tests. Uh here you got to see a GIF from
[08:56] uh the Voyager TV show from Star Trek
[08:58] and you could see the ablative armor on
[09:01] the Voyager. Why is that cool? Cuz I
[09:03] thought so. But, ablative ablation armor
[09:06] gives the starship
[09:09] protection and in a similar way ablation
[09:12] tests give machine learning engineers
[09:14] protection? Not clear. What does the
[09:17] word ablation mean? It means to take
[09:18] away.
[09:20] And that kind of gets into uh
[09:22] why do we use any of these components?
[09:24] You just saw a bunch of components and
[09:26] you're like, is that the only way to
[09:28] build a model? Why do we use those
[09:29] models? And the answer is, and I love
[09:32] this quote from CS 336,
[09:34] machine learning is an empirical field.
[09:37] That means we use the components that
[09:39] work. The components we use are the
[09:42] components we use because they
[09:44] outperform the components we chose to
[09:45] not use. So, the reverse engineering
[09:48] that we just did for GPT-2 is actually
[09:50] super meaningful cuz it told us these
[09:52] are the components that worked back when
[09:54] 2019 was happening when they wrote that
[09:57] paper. So, really cool. We just learned
[09:59] about ablation test and ablation test is
[10:01] just means taking something away,
[10:03] comparing how it how the system works.
[10:05] If it works better with it than without
[10:08] it, it won the ablation test. Great. So,
[10:10] a couple more quotes while I'm quoting
[10:12] people here and I love quoting people.
[10:14] Chris Ola in 2020 said LLMs are grown,
[10:17] not built. LLMs are grown, not built. We
[10:21] are going to build up the architecture,
[10:23] but the large language model learns the
[10:25] language itself. We don't have like
[10:27] language-specific things for the most
[10:30] part happening here. We're not going to
[10:32] teach about subjects and verbs and
[10:35] all of the fun linguistic concepts.
[10:37] We're just going to show it the English
[10:39] language and it's going to pick up all
[10:40] of that by itself.
[10:42] So, Karpathy has this really other great
[10:44] quote
[10:45] that he says the words large language
[10:47] models is kind of like summoning ghosts.
[10:50] We show it the entire English language
[10:52] and it's
[10:53] foggy recollection of it is what it
[10:56] learns. So, I really also love that
[10:58] metaphor and I think it's important to
[10:59] keep those two metaphors in mind where
[11:02] in my third metaphor that I'm going to
[11:03] include myself in this very august set
[11:05] of quotes. I'm probably shouldn't is
[11:08] something like
[11:10] farmers build the farm, but the tomatoes
[11:12] do the growing, right? You could set up
[11:14] trestles, but the tomatoes actually
[11:17] climb on top of the trestles and make
[11:19] the tomatoes grow. Really important.
[11:21] We're not doing the growing. We're
[11:22] letting the LLMs do the growing like
[11:24] Chris Ola says. Okay, great. So, now we
[11:27] talked about ablation test. So, now
[11:28] here's our full roadmap. We mentioned
[11:31] here are all the components under the
[11:32] architecture that we mentioned earlier.
[11:34] We also have MLP and feedforward
[11:37] networks. We have activation functions,
[11:40] and we have a bunch of concepts that
[11:41] we're going to need to learn to just
[11:43] train a model. So, this is roughly our
[11:45] road map that we reverse engineer
[11:47] partially
[11:48] from GPT-2. And the stuff we didn't
[11:50] reverse engineer is stuff we just need
[11:52] in order to build a machine learning
[11:54] model or a large language model. Okay,
[11:56] so now we have this full road map.
[11:57] There's a lot of words you don't know
[11:59] here. We're in section two right now, by
[12:00] the way, reverse engineering LLMs.
[12:03] Uh I want to show you this cuz I think
[12:05] it is going to help make a lot of things
[12:07] land.
[12:08] Every single section really has roughly
[12:10] eight lines of code, a few lines of
[12:13] code, a
[12:14] paragraph of code worth of deliverables.
[12:17] And that is roughly it, right? So, in
[12:19] section one, we saw model.generate, and
[12:22] we now know how to call how to use an
[12:24] autoregressive loop on a model. We know
[12:27] that we can reverse engineer large
[12:29] language models by calling print and
[12:30] summary on them. All that stuff, super
[12:33] cool.
[12:35] Every one of the next sections can
[12:36] really be summarized in like a line of
[12:38] code. We're going to spend like 20
[12:40] minutes per section or more. I don't
[12:42] know how long this recorded version of
[12:43] the in-person version is going to be,
[12:45] but it's about 20 to 30 minutes per
[12:47] section. Every one of those can be
[12:48] summarized in one line of code. If you
[12:50] just want the lines of code, here you
[12:52] go. They're in front of you. You have
[12:53] the scripts from code-0.
[12:56] Go just to angelai.com/code0.
[12:59] Uh
[13:00] You could just have these lines of code.
[13:02] Our goal for the day is to learn what
[13:04] this line what these lines of codes
[13:06] mean. So, we have an intuitive grasp on
[13:09] them as we're building large language
[13:11] models.
[13:13] Uh
[13:14] A lot of our
[13:16] a lot of our sections are going to have
[13:18] external demos in them. For example, in
[13:20] our learn more about section, this is
[13:22] one of my favorite ones. I forget his
[13:25] name. I think it's Shawn. I'm so sorry.
[13:26] I forgot his name, but it has this 3D
[13:29] really great model here that has all of
[13:32] the mod- the components we saw, but in
[13:34] von linear algebra form. Why linear
[13:37] algebra? I You know, you don't know the
[13:39] answer that yet. You're going to find
[13:40] out in section six. Hint. But for now,
[13:44] you could just see all of these
[13:45] embeddings and the layer norm and the
[13:47] proj- and the MLPs and the softmax.
[13:50] What's a softmax? I don't know. And you
[13:52] can actually just run these, uh which I
[13:55] think is really, really cool. I think
[13:56] there's a skip button that I could click
[13:58] and then it runs. It's really fun. You
[14:00] could see attention going through all of
[14:02] the
[14:03] various layers. We can even take a
[14:05] sample from our tiny sample model here,
[14:07] nanoGPT 80,000 parameters, to GPT-2
[14:11] small, 124 million parameters we saw
[14:13] earlier, and we can deep dive into each
[14:15] of them. Oh my goodness, I could really
[14:17] deep dive into this and see this MLP
[14:19] block. How cool is that? Okay, great. So
[14:22] now we have this demo, and I really
[14:24] recommend you spend some time here, but
[14:25] you could also use it to run through and
[14:28] see all the calculations happen in real
[14:29] time, which I really think is
[14:32] uh
[14:33] uh a useful thing to do. There's also
[14:35] all of the list of models here. There's
[14:37] nanoGPT, GPT-2, GPT-2 extra large. You
[14:41] can see it's much larger, and GPT-3. You
[14:43] could try and call print summary and
[14:45] print and summary on those. That'll be a
[14:47] fun exercise for you as well once you've
[14:49] looked at the demos.
[14:51] Great. So our next section is going to
[14:53] be about perceptrons. What are
[14:55] perceptrons? Perceptrons are the basic
[14:57] unit of work within a deep neural
[15:00] network or any neural network, really.
[15:02] Uh so I hope to see you back. We're
[15:04] going to build up from perceptrons to
[15:06] activation functions to GPU performance
[15:09] back to MLPs, which we saw as a real
[15:12] component we need to uh build uh
[15:15] large language models. Then we're going
[15:17] to go into loss functions and back
[15:19] propagations, which is how we train
[15:21] machine learning models. That's going to
[15:23] be a big section that we're a big module
[15:25] that we're going to be working on today.
[15:27] Thank you so much. I hope to see you in
[15:29] the next uh section.
