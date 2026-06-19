# Using Large Language Models | Build Your Own LLM Workshop #1

**Build Your Own LLM Workshop — Video #1 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 50m 40s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=vXiB0UdDhk8 |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome to a build your
[00:03] own large language model workshop with
[00:05] me, Justin Angel.
[00:07] As the slide says, this workshop is
[00:10] titled building large language models to
[00:13] develop intuition. You can go get a copy
[00:15] of the deck at go.justinangel.ai/deck.
[00:20] I think the first question that I'd like
[00:22] to answer is why should we build our own
[00:25] large language model? What do we get out
[00:27] of this? What do you, the viewer, the
[00:29] listener gets out of spending many hours
[00:32] of your life doing this very esoteric
[00:35] kind of thing. So, the answer is one,
[00:38] you'll get to develop taste and
[00:39] intuition for how AI and machine
[00:42] learning models are built. That to me is
[00:45] the key defining thing you take from
[00:46] this workshop. It's an understanding of
[00:49] how the models that are driving a lot of
[00:52] economic development, a lot of
[00:54] technological development are actually
[00:56] built. You'll get a sense for there's no
[00:59] magic behind any of this. This is all
[01:01] just math and back propagation.
[01:04] You'll get a sense for what are the
[01:06] limitations of these models. Very
[01:08] critical if you're building any sort of
[01:10] applications or agents on top of them.
[01:12] So, developing that taste and intuition
[01:14] is really going to be the core
[01:16] deliverable of this workshop.
[01:18] Also, this is a deeply technical
[01:21] workshop. It's meant for people who are
[01:23] comfortable with code. We're going to
[01:25] learn how to write all of the code
[01:27] that's required to build a small large
[01:29] language model. What does that mean?
[01:32] That means you're going to be able to
[01:33] write all of the machine learning code
[01:35] by the end of this. You're going to be
[01:36] able to write all of the LLM
[01:39] architecture by the end of this. You're
[01:41] going to know how to do pre-training and
[01:43] post-training and so on and so forth.
[01:45] Why is that useful to you? Also, that's
[01:48] going to let you be able to read all of
[01:50] the code from like the open-source
[01:52] models, from the various releases, so
[01:56] on. There's a bunch of open-source
[01:58] projects that have built open-source
[02:00] large language models like nano chat and
[02:03] so on. That will let you be able to read
[02:05] that code. Why is that useful? One, you
[02:08] might want to work on something like
[02:09] that. And two, that skill set is very
[02:11] transferable within working on an AI and
[02:14] machine machine learning solutions. So,
[02:17] very useful to have that skill.
[02:20] Also, the third thing you get from this
[02:22] is that you understand model releases.
[02:25] So, next time Deep Seek releases a model
[02:27] and crashes the stock market, you'll be
[02:29] able to understand what it means that
[02:31] you got sparse attention versus dense
[02:33] attention and why that matters so much.
[02:36] You don't have that context right now,
[02:38] so it'll be really useful to have that
[02:40] context. So, understanding model
[02:41] releases, their model cards, so on. You
[02:44] know, we all live in a world where
[02:46] there's new models every week or so. So,
[02:48] it'll be really useful to understand
[02:49] those as well.
[02:51] I also want to address whether or not
[02:52] this workshop will make you more
[02:54] hireable, I guess, by lab, by frontier
[02:57] labs, by neo labs. Do you get hired to
[02:59] that PhD program you really wanted,
[03:02] right?
[03:03] This alone won't do that.
[03:06] However, all of the knowledge here is
[03:08] required for all of the things that you
[03:10] will need in order to get the those
[03:13] positions. For example, you want to get
[03:15] hired by a frontier lab developing
[03:18] whatever models, right? The way to do
[03:21] that is know a lot of GPU programming,
[03:24] be an expert in AI safety. Whatever it
[03:26] is the subfield that you're interested
[03:28] in, everything in this workshop going to
[03:31] be base knowledge that you're going to
[03:32] need for those positions. Um so, really
[03:35] critical to know this stuff. So, just to
[03:38] summarize, this workshop will have you
[03:40] build your own LLM. You'll be able to
[03:42] follow any LLM training code off the
[03:44] internet. You'll be able to review
[03:45] architecture diagrams and model
[03:47] releases, technical reports, so on. And
[03:50] then maybe that improves your higher
[03:52] ability for every position in AI/ML that
[03:55] you're most interested in.
[03:57] Great. So, a little bit of the
[03:58] expectations that we have from you,
[04:01] let's start with that. In terms of
[04:03] prerequisites, this is meant for
[04:05] software engineers, people who are
[04:06] comfortable with coding, people who can
[04:08] really spend an 8-hour day reading,
[04:11] reviewing code, learning new concepts.
[04:13] If that's not you, this is the wrong
[04:15] workshop for you. If it is you, you
[04:17] should probably stick along. Uh some not
[04:19] prerequisites that we have for this
[04:21] workshop, math. I think linear algebra,
[04:25] calculus, statistics, topology, all of
[04:27] those are phenomenal and are very useful
[04:30] in the field of AI/ML, not necessarily
[04:32] something you have to come in with.
[04:33] We'll teach you all of that during the
[04:35] day. Most importantly, you'll get taught
[04:37] intuition. Intuition's going to be the
[04:39] number one thing that we focus on here,
[04:41] not necessarily creating our own uh
[04:44] proofs of whether or not these
[04:46] methodologies work. Python, if you know
[04:49] how to code in Python, awesome. I didn't
[04:51] when I started AI/ML, so super useful to
[04:54] come in with that skill, but also we're
[04:56] going to keep our Python used to like
[04:58] I wouldn't say bare minimum, but often
[05:00] we'll simplify the code to use
[05:02] cross-lingual idioms that would make
[05:05] sense across languages. So, you'll be
[05:07] able to follow along, even write a lot
[05:09] of Python code. And you know, we live in
[05:12] 2026 now. If you want to just use an AI
[05:15] to help you read and write code, that's
[05:17] eminently available to all of us.
[05:20] Machine learning, right? Often to train
[05:23] a large language model, you're going to
[05:25] need to know how to train a machine
[05:26] learning model. You're going to need to
[05:28] know what a perceptron is, a neuron. All
[05:31] of that stuff we're going to be covering
[05:32] here today. You don't have to come into
[05:34] this workshop with that. That does mean
[05:36] we'll spend a chunk of time covering
[05:38] what are machine learning basics, but
[05:41] all of that knowledge, every single
[05:42] section in this workshop is 100%
[05:46] transferable into large language models.
[05:49] So, a little bit about me, now that we
[05:51] talked a little about you, I'll
[05:52] introduce myself. I've been a software
[05:54] engineer for 23 years. I remember
[05:58] writing code in languages no one thinks
[06:00] about anymore like VBScript, ASP3, my
[06:03] goodness. Um, I've
[06:05] held many positions and many roles over
[06:08] the years. My last one was an IC8, so
[06:11] director level IC at Meta.
[06:15] Uh, I I'm just going to read you my
[06:16] Twitter bio because that summarizes me
[06:18] pretty well, at least professionally.
[06:20] Worked at Meta, Uber, Amazon, Apple, and
[06:23] Microsoft building apps, developer
[06:25] platforms, and new hardware. Um, I've
[06:27] done a lot. So, I'm a very experienced
[06:30] software engineer. If you want to follow
[06:32] me, you can follow me on Twitter or IG
[06:34] at Justin Angel. So, even though I've
[06:37] done a lot, what I've not
[06:39] done is I don't have 20 years of
[06:41] experience as a machine learning
[06:42] engineer. This is a recent conversion
[06:45] for me within the last 6 to 12 months.
[06:48] Uh, and I'll start off by maybe doing an
[06:50] unhumble thing by quoting myself and
[06:52] then explaining why I felt the need to
[06:54] make the that own shift within my
[06:56] career. And the quote is something that
[06:58] I said about uh 2 years ago, "Any
[07:01] software engineer that doesn't
[07:03] intrinsically understand AI will soon be
[07:06] unemployable. Any software engineer that
[07:09] doesn't intrinsically understand AI will
[07:11] soon be unemployable." I All of my code
[07:14] in 2023 was written by AI. All of my
[07:17] code in 2024 was written by AI. It was
[07:19] very patently clear to me that this is
[07:22] going to become the future and we have
[07:24] to understand the models that are going
[07:26] to one power all AI coding assistants,
[07:28] but also a lot of knowledge work and a
[07:30] lot of other work in the future.
[07:32] So, really worth knowing that. I do
[07:34] strongly believe that AI is going to
[07:38] fully transform software engineering and
[07:40] related fields, not in a doomerism kind
[07:42] of way, but in a this is practically
[07:44] going to happen kind of way. I went and
[07:46] picked up an AI ML masters in the last
[07:49] several months. I got my masters in comp
[07:52] sci AI ML like it says, and I wrote my
[07:55] thesis on LM psychotherapy. Worth
[07:58] mentioning again, not a software like
[08:00] not a machine learning engineer with 20
[08:02] years experience. So, if you want that
[08:05] crowd or a data scientist for example,
[08:07] if you want that crowd, you should
[08:08] probably [clears throat] be in another
[08:09] workshop.
[08:10] Um the learning methodology for today,
[08:13] how will I teach you how to build a
[08:14] large language model? Building a large
[08:16] language model is a very, very advanced
[08:18] concept I think in within the realm of
[08:20] machine learning. So, how are we going
[08:22] to do that? One, we're going to build
[08:24] concepts on top of each other until we
[08:26] get there. We're going to have about 23
[08:28] sections in this workshop over many
[08:30] hours.
[08:33] For those concepts, we'll divide every
[08:36] one of our
[08:37] sections into three different
[08:39] portions. The first portion is just
[08:42] going to be me. My responsibility will
[08:44] let you know what problem we're trying
[08:46] to solve in the section. What is the
[08:48] technology we're trying to learn? How
[08:49] does it fit into the bigger ecosystem in
[08:52] the bigger picture? Give you a lot of
[08:54] great insights about it. I'm not just
[08:55] teaching you the the sheer fundamentals.
[08:57] I'm going to teach you as much as I can
[08:59] about thinking with intuition about why
[09:01] we need this and does this really solve
[09:03] a problem? So, I'll read some slides to
[09:05] you. That's going to be a portion of
[09:06] every section. Then, we're going to jump
[09:08] straight into most likely what we call
[09:11] AI by hand. That's just Excel or in my
[09:14] case Google Sheets, where I show you the
[09:16] math when we go section by section
[09:18] trying to understand how does this kind
[09:20] of fit in together? Even if you don't
[09:23] know any of the math, that's going to
[09:24] help you build a phenomenal amount of
[09:26] intuition for it.
[09:28] Also, once we've seen Excel and we
[09:30] develop a little bit of intuition, the
[09:32] next thing we're going to do is we're
[09:34] going to look at code samples. So, every
[09:36] section comes with a Python notebook
[09:39] that we're going to review section by
[09:40] section and builds upon each upon itself
[09:43] with all of the stuff that we've learned
[09:45] in the slides and in Excel and gets
[09:47] implemented in code in Python and
[09:49] PyTorch. So, that's my responsibility to
[09:52] walk you through that. What's your
[09:53] responsibility within this methodology?
[09:57] One, every worksheet for Excel has a
[10:01] with answers and without answer sheet. I
[10:03] expect you to go into the without answer
[10:05] sheet and then fill these in yourselves.
[10:07] You should really try and do this
[10:09] alongside with me.
[10:11] Colab, we have Python notebooks. I
[10:13] expect you to go ahead and run them and
[10:15] tinker with them and read them. Also,
[10:18] they'll have each Python notebook will
[10:20] contain some exercises. I kind of
[10:22] structured it so it doesn't take you
[10:23] more than 15 minutes, 20 minutes tops to
[10:27] do the exercises between each section.
[10:29] There's not a lot of them. Most sections
[10:31] will only have one or two or three
[10:32] exercises, but super worth doing those
[10:35] and fully understanding like the
[10:37] notebook that you're in. That's going to
[10:38] be the most useful thing if you're going
[10:40] to want to learn practical skill set.
[10:42] Uh answers, again, both the Colab
[10:46] notebooks and the Google Sheets are
[10:48] going to have all of the answers. So, if
[10:50] you don't want to do any self work,
[10:52] that's fine, but at least go ahead and
[10:53] read the answers. Try and grok the that
[10:56] material.
[10:58] I do want to give props to Professor Tom
[11:00] Yey from CU Boulder. He came up with the
[11:02] AI AI by hand methodology where you kind
[11:05] of like draw out the matrixes
[11:08] multiplications by hand. You draw out
[11:10] the whole thing and you really move
[11:12] numbers around. I think that's what
[11:13] really made it land for me from a mathy
[11:16] perspective.
[11:18] Let's talk about our day. So, I
[11:20] mentioned we have 20 sections. You
[11:21] haven't seen them yet, but let's think
[11:23] about how we would divide our day of a
[11:25] workshop
[11:27] to get you to small meaningful
[11:29] deliverables as fast as we can. So, the
[11:31] first section of the day is the intro
[11:34] section. In this section, we're going to
[11:37] be grabbing an off-the-shelf GPT-2 style
[11:40] transformer,
[11:42] and we're going to try and run it. We're
[11:43] going to learn about auto-regressive
[11:44] loops and whatnot. That's just how we
[11:46] use large language models. Also, we'll
[11:49] use that section to build our entire
[11:50] road map for the day. So, when I show
[11:52] you our road map with 23 sections, you
[11:54] understand why we have those particular
[11:56] 23 sections. Next up, the next big
[12:00] deliverable that we're going to have is
[12:01] a machine learning fundamentals. We're
[12:03] going to start off with a single neuron.
[12:06] What is even a neuron? How do you train
[12:09] a la- network with it? What is a loss
[12:12] function? How do you use disk with it?
[12:15] Right, all of those questions we're
[12:16] going to answer in this one big module
[12:19] that contains multiple sections.
[12:22] So, in the deliverable from that will be
[12:24] a working deep neural network that we
[12:27] have trained. It won't be
[12:28] language-based, but it will get us very,
[12:30] very close in terms of the concepts we
[12:32] need to lar- large language models.
[12:34] Specifically, all of those concepts are
[12:36] 100% transferable to large language
[12:39] models.
[12:40] The next chunk of modules that we have
[12:43] to focus on is going to be about
[12:45] building a transformer architecture.
[12:47] What is a transformer? It's a bunch of
[12:49] architecture components strung together.
[12:52] It's a
[12:53] multi-layer perceptron, an MLP. It's a
[12:56] dropout component. It's a tokenizer.
[12:59] It's embeddings. It's an attention
[13:01] mechanism. We're going to have to learn
[13:03] every one of these components together,
[13:05] and then finally bring them together
[13:07] into one large transformer architecture.
[13:09] Finally, we have to focus on a deliv- on
[13:13] large language model. So, the
[13:15] deliverable would be writing
[13:17] post-training, pre-training scripts, and
[13:19] actually having our own large language
[13:22] model working by the end of the day. A
[13:24] real model that you can use with your
[13:26] name, the number V1, and say that you
[13:29] built it yourselves.
[13:31] So, how is our day built? Let's start
[13:33] off with like a little bit of work
[13:34] shopping links here. We mentioned we
[13:36] have the four modules. Intro it's how to
[13:38] use an LM. DNNML it's how to train a
[13:43] machine learning model. Architecture,
[13:45] all of the stuff we're going to need for
[13:46] transformer architecture. And large
[13:48] language models pre post pre-training
[13:50] and post-training. If you ever need
[13:52] links, all of the links are in this one
[13:54] slide. Maybe memorize this slide. It has
[13:56] all of the code notebooks and all of the
[13:58] Excel spreadsheets. There's also the
[14:00] mega link of go.justinangel.ai/drive.
[14:03] That mega
[14:06] link has all of these links inside of
[14:08] it. So, you don't have to necessarily
[14:09] even remember about the slide. Just
[14:10] remember that all of our
[14:13] links follow a very easy naming
[14:15] convention. You go to go.justinangel.ai.
[14:19] And then if you want to go to code
[14:20] notebook, you go to code
[14:22] - the number of the section. Or if you
[14:26] want to go to an Excel spreadsheet, you
[14:27] go to excel
[14:29] the number of the section. Really really
[14:31] easy to remember, very organized. And
[14:33] again, this deck exists at
[14:35] go.justinangel.ai/deck.
[14:40] So, if this was an in-person workshop,
[14:42] our schedule would be
[14:44] action packed.
[14:46] A
[14:46] a oppressive, some would say.
[14:49] We would spend no more than 20 minutes
[14:51] per section. And we would And that would
[14:54] include yourself work. I'm going to take
[14:56] the liberty to have all of the
[14:58] spaciousness in the world to really
[15:00] review every single point when we do the
[15:02] online version. So, this version might
[15:04] be a bit longer than the 8-9 hour action
[15:07] packed day that we normally have. But, I
[15:09] think it'll be worth it to you. You're
[15:11] also welcome to come to the next
[15:12] in-person workshops. They're all going
[15:14] to be in San Francisco, I think.
[15:17] Great. So, we mentioned that we're going
[15:19] to spend 8 hours together in this room
[15:22] talking about machine learning models
[15:24] and large language models. One problem
[15:26] that I have is I want to send you at the
[15:28] end of the day with your own working
[15:30] large language model that you've
[15:32] trained. However, it takes about eight,
[15:34] maybe 8 hours, maybe 20 hours to train a
[15:37] large language model. For that, we're
[15:40] going to need to kick off training right
[15:41] now. So, we're going to go ahead and do
[15:43] that, and we're going to go to our first
[15:44] Colab notebook. Oh my goodness, this is
[15:46] going to be so exciting, even if you
[15:48] don't know what Colab is. We're going to
[15:49] go to go to justinangel.ai/code-zero,
[15:51] cuz we're in the zero section, I guess.
[15:57] We're going to connect to an A100 GPU.
[16:00] Colab just rents out GPUs for you, so
[16:02] I'm going to click A100 GPU, I'm going
[16:04] to click run all, and it's going to
[16:06] start building the model for me over the
[16:08] next 20 hours. I'm going to need Google
[16:11] Colab Pro Plus, cuz it's going to need
[16:13] to run in the background for
[16:14] 20-something hours.
[16:16] I And in this notebook, you're going to
[16:18] see a bunch of code that you don't
[16:20] understand, but you will by the end of
[16:21] today. Most importantly, it has all of
[16:24] our architecture, all of our
[16:25] pre-training, so on and so forth. I'm
[16:27] going to scroll, scroll, scroll really
[16:29] fast past this. Why am I doing this? I
[16:31] want you to see the large language model
[16:33] emitting nonsense in the beginning. So,
[16:35] at the beginning of the day, we have our
[16:36] large language model, and we ask it,
[16:38] "Hey, would you mind auto-completing the
[16:41] the sentence in a galaxy far, far away?"
[16:44] And what it says is, "In a galaxy far,
[16:46] far away, outdoor corn today Denver
[16:49] preview examples push half emoji bracket
[16:52] unrelated natural drowning military
[16:55] malice milk." Right, it's absolutely
[16:58] nonsense. Right, the large language
[17:00] model, when you just initialize it
[17:01] randomly, doesn't speak English. And our
[17:04] whole job for the day is to teach it how
[17:06] to speak English. So, how do we do that?
[17:09] You're going to find out in the
[17:10] workshop, but I do want to just show you
[17:12] that the outcome is I'm going to run
[17:14] this training. Every thousand steps take
[17:16] about an hour. We have 20,000 steps, so
[17:19] that takes about 20 hours. Made up
[17:21] number, but still. So, we're in hour six
[17:23] right now. We're in hour seven, eight,
[17:24] nine, 10, 11, 12, 14, 15, 16, 17, 19. Oh
[17:28] my god, we got to hour 20. Great. Now,
[17:29] we have something called loss curves and
[17:31] accuracy. Neither of these are things
[17:33] you might be familiar with, so we won't
[17:35] spend time to show you do that, but I
[17:37] want to show you the post-training smoke
[17:38] test.
[17:40] Once upon a time in a small village, an
[17:42] ancient man and woman lived there. The
[17:44] best way to learn programming is by
[17:46] starting by learning a coding language.
[17:48] The theory of relativity states that the
[17:50] universe should be composed of a number
[17:52] of interfering interacting particles.
[17:54] Very cool. I didn't teach the model
[17:57] that. I didn't teach the model the
[17:59] English language. I didn't teach the
[18:01] model how to use subjects, adjectives,
[18:04] and verbs, and sentence structures, and
[18:07] you know, agreement, and all of that fun
[18:09] language stuff. The model saw a bunch of
[18:12] English, had something called
[18:14] backpropagation, had something called an
[18:16] architecture, and they learned the
[18:18] English language for us. Really cool.
[18:21] Our job for this next eight something
[18:24] hours is while this is going to run.
[18:26] Right now, the run all button is running
[18:28] for you and your computer if you want
[18:30] to.
[18:31] While it's doing that, we're going to
[18:32] learn all of the components that went
[18:34] into this training script together.
[18:37] I will mention that you have the option
[18:39] of getting Google Colab Pro Plus, that
[18:41] costs about $50 a month, cuz you need
[18:43] background execution, and that's going
[18:45] to run for 20 hours on an A100. So,
[18:47] that's an option. You could pay, I think
[18:50] I paid $82 of modal credits to run the
[18:53] same training script on modal, so that
[18:55] that only took eight hours, but I used a
[18:57] slightly different script,
[18:58] code-19-pretrain,
[19:01] and you'll be able to see it here if
[19:02] that's something you want. You also have
[19:04] the option of not doing any of that and
[19:06] not spending any of this money. You
[19:08] could just go use my pre-trained
[19:10] weights. So, if you go to
[19:10] go.justinangel.ai/hf,
[19:14] HF stands for hugging face. It's where
[19:16] we store all of our data sets and all of
[19:17] our models, we the open source people,
[19:21] and then you can just go ahead and
[19:23] download the model. And here you could
[19:24] see this workshop V1 pre-training PTH,
[19:27] that is the outcome of this massive
[19:29] training script that runs for 20 hours.
[19:31] So, you could just use mine, or if you
[19:33] want to have the good vibes of like I
[19:35] have trained my own model, then you
[19:37] could probably run it yourself. The
[19:39] script just works. You could just do
[19:40] that, go ahead and do that.
[19:43] With that, we've arrived at our first
[19:45] section, intro to LLMs. I'm going to now
[19:49] start talking about how to use LLMs.
[19:54] Our first section is going to be intro
[19:56] to large language models.
[19:58] And by intro to large language models,
[20:00] what we're really going to be doing here
[20:01] is we're going to see next word
[20:03] prediction in person for the very first
[20:05] time.
[20:06] Um, every one of our intro slides for
[20:08] one of our sections is going to have the
[20:09] name of the section and deliverables.
[20:11] Specific things we're trying to get out
[20:13] of the section that are very applicable
[20:15] to us building our large language model.
[20:17] So, what are our deliverables? Next word
[20:19] prediction and something called
[20:21] temperature and top K and top P. If you
[20:23] don't know what it is, super valid, you
[20:25] don't have to know that as we're just
[20:27] getting started. Great. And then every
[20:30] one of our uh sections has a code
[20:32] notebook that we can open and an Excel
[20:34] notebook that we can open as well. And
[20:36] we will do that at the appropriate time
[20:38] during the uh after the slides.
[20:41] So, now I want you to kind of take a
[20:43] moment with yourself, maybe pause me,
[20:46] maybe don't, and ask yourself, what do I
[20:49] know about what language language models
[20:51] are, right? Like what do I already kind
[20:54] of like intuitively understand about
[20:56] them?
[20:57] So,
[20:58] >> [sighs]
[20:59] >> kind of like if you think about going to
[21:00] chat GPT or Claude or whatever, you kind
[21:03] of know they generate text. Okay, so
[21:06] that's great. So, LLMs generate text. Uh
[21:09] and we're going to spend a the entire
[21:10] day getting our LLMs to generate text.
[21:13] Um but how do they do that? They do it
[21:15] in something we call auto regressive.
[21:16] That's just a fun way of saying one
[21:19] token or word at a time. So,
[21:22] um what's an example of that? On the
[21:24] left you could see GPT-2
[21:26] auto regressively generating the next
[21:28] word of the prompt Justin and I as
[21:31] software engineer worked for. And then
[21:33] it has Meta 53% and Microsoft 23% and
[21:38] Uber at 11% and Amazon at 8% and Apple
[21:41] at 3%, right? Super creepy that it knows
[21:44] that about me, but it does have some
[21:47] probabilistic model of how the world
[21:49] works based on everything that it's
[21:51] read. Super creepy. Love it, but it's
[21:54] also doing it one token at a time.
[21:57] Right, why is one token at a time
[21:59] important for us? We're going to spend
[22:00] this whole section on doing auto
[22:02] regressive generation of text one token
[22:05] at a time. Uh what do else do we know
[22:07] about large language models? We know
[22:09] that they're machine learning models.
[22:11] What does that mean? That means we have
[22:12] to give them some data, we have to train
[22:14] them, and then we can evaluate them on
[22:16] how well they generalize to unseen data
[22:18] that wasn't in the training set, right?
[22:21] Uh hot dog or uh
[22:23] or wiener dog, right? Um we show it a
[22:26] bunch of photos of hot dogs and wiener
[22:28] dogs, and in the end we show it a bunch
[22:30] of photos of hot dogs and wiener dogs
[22:31] it's never seen before, and that is our
[22:33] accuracy. How well it does on unseen
[22:36] data that it generalizes to.
[22:38] Um new and we're going to spend the
[22:40] first eight like eight sections building
[22:42] machine learning models and getting
[22:43] really comfortable with that concept. We
[22:45] also know that large language models are
[22:47] deep neural networks, so they have like
[22:49] this fixed architecture that has
[22:51] learnable parameters. What does that
[22:52] mean? I don't know right now, maybe you
[22:54] don't know either. By the end of the day
[22:56] we're going to learn what it means
[22:57] together. So, our second half of the day
[22:59] is really built on reviewing the deep
[23:02] neural network architecture.
[23:05] Um so why do we sample? Right, like hard
[23:08] pivot. Why do we have to sample? So we
[23:11] now know that large language models
[23:13] outputs a list of probabilities.
[23:15] Probabilities are great. I could just
[23:17] choose the top probability, right? The
[23:19] cat sat on the mat. The dog barks
[23:21] loudly. Those are the probabilities
[23:22] shown on the screen in front of us,
[23:24] right? I could just choose the highest
[23:26] probability between dog, cat, and car
[23:29] and uh just say, "Okay, I'm going to
[23:31] choose the top probability, the most
[23:33] aggressive form of
[23:36] uh
[23:37] of sampling."
[23:39] Uh why shouldn't I do that? Well, the
[23:40] dog the dog barks loudly even though the
[23:43] dog is the top probability of this round
[23:46] is that it doesn't have great
[23:47] probabilities for the next round after
[23:49] that cuz the cat sat on actually has
[23:52] much higher probabilities, right? So you
[23:54] kind of have to like look around this
[23:56] tree and find out which of the future
[23:59] possibilities beyond this token has the
[24:01] best probability.
[24:05] Why is that a problem? Let's say we're
[24:07] trying to generate a small paragraph of
[24:09] only 100 words
[24:11] and we will only check two items, right?
[24:14] In each one of these levels. So we're
[24:16] going to have a tree with 100 levels in
[24:18] or a graph with 100 levels in.
[24:20] Um that's going to require two to the
[24:22] power of 100 checks, right? We would
[24:24] have to flush out this entire tree. Uh
[24:27] that's going to take more compute than
[24:29] has humans have created since we've
[24:31] started having CPUs, right? We would
[24:35] need to effectively wait till the heat
[24:36] death of the universe to have a small
[24:38] paragraph generated we using this like
[24:41] what we now call beam search. Beam
[24:43] search means we run over every single
[24:45] beam of this tree and we find the most
[24:48] optimal sentence. Um again, the heat
[24:51] death of the universe is going to take
[24:52] quite a while to complete. So we're
[24:54] going to need a a
[24:55] that is a bit more heuristic, a bit more
[24:58] easy to come up with, something we can
[24:59] kind of intune on. And also like even
[25:02] checking one level in, let's say we only
[25:03] check two options and we check
[25:06] two levels in, right? We now have to do
[25:08] three times the compute. Like check this
[25:11] current round, the top two words and how
[25:13] they perform, then we're going to have
[25:15] to check three total rounds. That's
[25:16] three times the compute. That's quite a
[25:18] lot more compute. That's going to cost
[25:19] us money, really, really bad. In an
[25:22] ideal universe, we would always do beam
[25:24] search. We cannot always do beam search.
[25:26] It's just far too expensive.
[25:29] Great. So, we now learned that there's
[25:31] this uh tree of probabilities and we
[25:33] can't possibly sample it with beam
[25:35] search effectively. So, what do we do,
[25:38] right? Even though we know that the
[25:40] better probabilities exist somewhere
[25:41] there. Well, we'll come up with some fun
[25:44] sampling strategies of like from this
[25:46] current round, how do we choose the
[25:48] absolute best or some version of like
[25:52] guestimated best. So, the first thing we
[25:54] have in our tool belt of sampling is
[25:56] temperature and uh the formula is here
[25:59] in front of you. Because this is our
[26:01] first formula, I'll mention that every
[26:03] time you see a formula, you're going to
[26:04] have sample code to come along with it
[26:06] and it'll have an English-ish
[26:08] explanation that tries to explain the
[26:11] that concept. So, here we see
[26:13] temperature and it's
[26:15] uh does something with exponents and
[26:17] sums. Maybe it's kind of unclear to me
[26:19] what it does. It's totally fine right
[26:21] now. Let's try and build an intuition
[26:22] for what it does and then understand the
[26:24] math. So, here in the bottom left, you
[26:26] could see temperature half. You could
[26:28] see temperature the original
[26:30] temperature, temperature one. You could
[26:31] see temperature two. And you could see
[26:33] that the original temperature
[26:37] has a distribution. When we lower the
[26:39] temperature, we extenuate the
[26:42] differences, we enhance the differences
[26:44] between
[26:46] uh between the various probabilities.
[26:48] Why does that help us? Because now we're
[26:50] much more likely to choose the top
[26:52] probability. Okay, so that's temperature
[26:54] over less than one when we like lower
[26:57] the temperature. When we increase the
[26:58] temperature, what we see is the
[27:00] temperature flattening. We make all of
[27:03] the probabilities kind of equal. So we
[27:05] take away the knowledge of the model of
[27:08] the world and we say actually we're
[27:09] going to discount it a bit and we're
[27:10] going to have a slightly higher
[27:11] probability. And it's going to be a a
[27:13] little bit, let's say, more creative. I
[27:16] use more creative because I don't
[27:17] necessarily know if there's research
[27:18] that indicates higher temperature are
[27:20] more creative.
[27:21] Uh great. So how do we do that? So
[27:23] higher temperature flattens, lower
[27:25] temperature increases differences. Um
[27:28] how do we do that? Well, we just take
[27:30] the current uh probability that the
[27:32] model outputted or whatever it is that
[27:34] it outputs, maybe it outputs something
[27:36] called logits, I'm not sure yet. And we
[27:38] divide it by the temperature number,
[27:40] which is why there's like an inverse
[27:41] ratio with like numbers smaller than one
[27:43] and numbers greater than one.
[27:45] Uh and then we divide the the current
[27:48] probability by the sum of all of these
[27:50] probabilities. We also use an exponent.
[27:52] We'll learn a lot more about exponents
[27:54] in section 14. There's no reason to go
[27:56] into that right now. Cool. We're going
[27:58] to review this math in the Excel
[27:59] spreadsheet. You don't have to get
[28:00] scared right now. You can get scared
[28:02] later.
[28:04] Okay, so what are my other two sampling
[28:06] strategies that I could do here? One
[28:08] option is called top K, which is just a
[28:10] fancy way of saying we're going to limit
[28:12] our selection to the top options we've
[28:14] seen. Why do we have to limit our
[28:16] options to the top options we've seen?
[28:18] Well, large language models predict
[28:20] 50,000 potential probabilities, it's
[28:22] 150,000 potential probabilities of all
[28:25] of the words words in the English
[28:27] language, but the cat sat on the is
[28:31] almost definitely not going to be auto
[28:33] completed completed with the word
[28:35] quantum or with the word uh
[28:40] uh with the word book, right? The words
[28:42] have to be a tiny bit more sensible.
[28:45] So as a result of that, we can limit our
[28:47] selection to the top criteria. So, when
[28:49] top K two, you can see we've limited our
[28:52] selection in this sentence, whatever
[28:54] that sentence might be, to the options
[28:56] dollar and yen. And we're not going to
[28:58] use all these other options here. Okay,
[29:00] so that's a way of filtering out only
[29:02] the top probabilities. Another way is to
[29:04] use top P. And uh here we can say I only
[29:08] want the options that fit in the top uh
[29:12] 70% cumulative. So, dollar is 40%
[29:15] likely, that fits in the top 70. Yen is
[29:17] top 20, that still fits in the top 60,
[29:19] so that's good enough. Silver still fits
[29:21] in the top 50, even though it's only
[29:23] it's kind of marginal. So, we So, we we
[29:26] use those options, and then we discard
[29:28] all the other options, and we
[29:29] recalculate the options just for the top
[29:32] options. So, top K, top items, top P,
[29:35] top probabilities. Great. And we're
[29:37] going to review all of that in Excel.
[29:38] This is just to give you like the
[29:40] concept and the beginning notions of it.
[29:42] And then in code, what we're going to
[29:44] see is how to use model that generate.
[29:46] Great. So, now we've talked a lot about
[29:48] this. Let's see an Excel demo. And this
[29:50] is going to be our first Excel demo, so
[29:52] I'm going to open it up here. When I say
[29:54] Excel, I probably mean Google Sheet. I'm
[29:56] going to start by cloning my uh
[29:59] my Google Sheet. You're going to have to
[30:01] do this cuz you don't have right
[30:02] permissions on these. And the first
[30:04] thing we notice is there's two sheets.
[30:06] There's here in the bottom with answers
[30:07] and without answers. I'm going to walk
[30:09] you through without answers, and I'm
[30:11] going to try and remember all the
[30:13] formulas and fill it out correctly.
[30:15] You should probably also try to do with
[30:17] the the the sheet called without answers
[30:19] with me. But if you have questions, you
[30:21] have the with answers section. You never
[30:24] have to get stuck. You're trying to
[30:25] think about it, trying to do the work.
[30:27] If you get stuck, go directly to the
[30:28] with answers section.
[30:31] Great.
[30:32] Uh so, now we're going to do with
[30:33] answers, and we see the probabilities
[30:35] are for the currency of the United
[30:37] States is the dollar, yen, silver, gold,
[30:41] pound, paper. I put them all in a bar
[30:43] chart here, so we can kind of see what
[30:45] the probabilities look like. Okay, so
[30:48] those are some probabilities. First
[30:49] question I have, I'm just a very
[30:51] pragmatic kind of person, why can't I
[30:53] just weighted sample from those
[30:55] probabilities? Those seem pretty okay to
[30:57] me. Well, okay, so now I'm going to tell
[31:00] you that I kind of lied to you with
[31:01] those probabilities above. There's
[31:02] actually 50,000 more probabilities in
[31:05] the base, and a really long tail of
[31:07] options that are totally nonsensical
[31:10] like words in Spanish and like math
[31:13] symbol. Numbers are so close to zero to
[31:15] almost be infinitesimally zero, but are
[31:19] not it. Okay, so now I realize Justin
[31:22] lied to me and there's 50,000, maybe
[31:24] 150,000 more words. Sampling sometimes
[31:27] samples words that are nonsense, so I
[31:29] had to limit my sampling here to the top
[31:32] words. But if I start sampling from all
[31:34] these other words, right, I'm going to
[31:36] get a bunch of nonsense words like the
[31:38] currency of the United States is the
[31:40] euro. Is the Is the currency, right? Is
[31:44] the paper. So, not really, really great
[31:47] if you want to have a deterministic
[31:50] style here.
[31:51] So, that's why we don't just weighted
[31:53] sample from everything. That's why we
[31:54] have to also apply some sort of top K,
[31:57] top P sampling strategies. Okay, so now
[32:00] I mentioned top K exists, that's really
[32:02] great for us. So, here we have our top
[32:04] probability, and we're going to limit us
[32:05] after our top probability just so we can
[32:07] like really look at the sheet. Uh and
[32:10] I'm going to say I actually want to
[32:11] filter out only the top two
[32:12] probabilities. So, when I do that, the
[32:15] sheet has magic in it already, some
[32:18] formulas, and it's going to limit us
[32:20] from dollar yen being 60% total, it's
[32:22] actually going to go to 100% total,
[32:24] right? And it redistributes the
[32:26] probability between them. So, now dollar
[32:28] went from 40% to 67% and yen went from
[32:31] 20% to 33%,
[32:33] right? It redistributed the
[32:34] probabilities between the top items. I
[32:36] think this is a great time for you to
[32:37] pause and play around with what happens
[32:39] when I write five in here, what happens
[32:42] when I write one in here, what happens
[32:44] when I write three in here, right? And
[32:45] it gives you a real intuitive sense of
[32:48] how top K influences our selection and
[32:50] sampling.
[32:52] Okay, so now we have top P. Top P allows
[32:56] us to choose the top probabilities.
[32:59] And we could see here that we have the
[33:01] dollar, the yen, silver, gold. But what
[33:04] let's say I want to limit it to only the
[33:06] top 50% probability, it's going to limit
[33:10] it again to dollar and yen cuz those are
[33:12] the top cumulative probabilities.
[33:15] And then based on that, we now
[33:17] redistributed probabilities. I could
[33:18] also go to 70% and now I've limited to
[33:21] dollar, yen, and silver. So what would
[33:24] the distribution look like? Before it
[33:25] was kind of like this. It was a really
[33:27] long tail. We could pretend there's
[33:28] 50,000 more items. So it's 50, 25, 25.
[33:32] Oh my goodness. We've redistributed the
[33:34] probabilities to the top probabilities
[33:36] cumulatively.
[33:38] Amazing. And now we get the temperature
[33:40] and this is going to be one of our first
[33:42] time that we're going to write a little
[33:43] bit of code ourselves. So we have
[33:46] temperature one right here and we have
[33:48] the probability right here. We're going
[33:49] to do that math formula we looked at
[33:51] earlier that says exponent of the
[33:54] probability
[33:56] divided by the temperature and I'm going
[33:58] to lock the temperature cell cuz we're
[34:00] going to drag and drop in a sec. Here we
[34:02] go. 149%.
[34:04] Doesn't really mean a lot to me. Wow,
[34:07] here we go. And I think I may did this
[34:09] math wrong. So now comes the section
[34:11] where I copy it. Here we go. I had the
[34:12] LN it
[34:14] because these are in the the correct
[34:17] base. Here we go.
[34:19] Now this makes more sense to me. So
[34:21] temperature one
[34:24] the numbers look pretty similar. Okay,
[34:27] so we don't have to do a lot for that.
[34:29] But let's say if my temperature was less
[34:31] than 1.5, the sum all of a sudden is 26%
[34:36] as we see here from the base. So, 26 is
[34:38] not how percentages work. We have to
[34:40] like recumulative it and sum it based on
[34:43] 100%. So, the way we do that is we take
[34:46] this number, we divide it by this
[34:48] number, by the sum. We're going to lock
[34:50] in row 92 so nothing weird happens. I'm
[34:52] going to drop this down here. All of a
[34:55] sudden we redistributed the
[34:56] probabilities based on temperature.
[34:59] Okay, so if I go above
[35:02] one, let's say to two, all of a sudden
[35:04] the sum of the probabilities is like 229
[35:06] and that doesn't make sense. That's not
[35:08] how percentages work. We divide by the
[35:09] sum and we get these probabilities. So,
[35:12] what do we want to learn from that?
[35:14] These are the original distributions and
[35:16] now they're not numeric. Now they're
[35:17] just bar charts because I want you to
[35:18] visually see the difference. In 0.5 we
[35:21] have a higher percentage
[35:24] a higher difference between the top
[35:26] option and the bottom option. At top two
[35:29] we have flattened out the differences.
[35:32] Higher temperature flattens out
[35:33] differences. Lower temperature increases
[35:36] the differences.
[35:38] Great. So, we saw that. That's our sheet
[35:40] for sampling. So, we got a little bit of
[35:42] intuition for the math and we even
[35:43] implemented a formula or two. Now let's
[35:45] go to the code sample.
[35:47] So, we're going to open up Colab. This
[35:49] might be your first time opening up
[35:51] Colab for real. So, the way you open up
[35:53] you use Colab and the the thing that it
[35:56] gives us is GPUs. We want to choose
[35:58] which GPU we want to go. So, I'm going
[35:59] to click this little arrow up here on
[36:01] the right and I'm going to click connect
[36:04] change runtime type. It's going to let
[36:06] me choose which GPU I want. Okay, so
[36:08] which GPU do I want? T4s have 24
[36:11] gigabytes of RAM. A100 has 40 gigabytes
[36:14] of RAM. This specifically this A100 that
[36:16] Google Colab uses.
[36:17] >> [gasps]
[36:18] >> So, I'm going to choose a T4 for this
[36:21] demo cuz I'm going to need a pretty big
[36:23] GPU to hold
[36:25] GPT-2, but most of these demos were only
[36:28] tested on A100. Up to you to try and use
[36:30] lower GPUs that are a bit more
[36:32] cost-effective. I think it's fine to
[36:34] just use an A100 for the day. Great. So,
[36:36] I save that choice. I click the connect
[36:38] button, and then I click the run all
[36:40] button, and then I'm able to see to see
[36:42] this demo. I'm not going to do that
[36:44] right now cuz I have all the answers
[36:45] saved, and I want to be able to run
[36:47] through these and show you the answer.
[36:48] But, now you know about changing
[36:51] GPU tab. You know about connecting. You
[36:52] know about run all. So, that's your
[36:54] basic entry to Colab, those three
[36:56] things.
[36:57] Choosing a GPU tab, connecting to a
[36:59] server, and clicking the run all button.
[37:02] Great. So, now I have a setup cell here.
[37:04] It's hidden. It imports a bunch of
[37:05] stuff. Let's do our very first example.
[37:08] I'm going to I don't know if you
[37:09] remember we had that workshop V1
[37:12] pre-training model that like I
[37:14] pre-trained some
[37:15] some weights. So, remember we had the
[37:17] script that we're going to run. It's
[37:18] going to take 20 hours and teach the
[37:20] model English. The results are saved
[37:22] here in workshop V1 pre-training. What
[37:24] if I just want to load this model? So,
[37:26] I'm going to copy the name of this
[37:28] model. I'm going to go back into Colab,
[37:30] and I'm going to paste it right here
[37:32] under pre-training. And that's going to
[37:34] load that model up from Hugging Face.
[37:37] I'm going to give it a prompt that says,
[37:38] "You should eat more." And I'm going to
[37:40] see what it auto-completes that as. And
[37:42] surprise, surprise, when I run that,
[37:45] it says I should eat more fruits. Right?
[37:47] It generated one token, and that token
[37:49] is fruits. Very, very cool. And a token
[37:52] is just a way for me to say word until
[37:54] we get to the tokenizer section, which
[37:55] is I think section 15. So, for now, when
[37:57] you hear the word token, hear the word
[37:59] word.
[38:01] Great. So, how did we do that? I did
[38:03] something here with CUDA, which is just
[38:05] a way of saying GPU for this one
[38:07] statement, and I converted this to
[38:10] tokens. I don't know what that means
[38:11] right now. But, most importantly, I
[38:13] called the dot generate method with new
[38:15] tokens equal one. So, that's something
[38:17] you're going to have to remember, dot
[38:19] generate with
[38:21] a a token of one.
[38:23] Great. So, I call that generate and then
[38:25] I print it out the result and then it
[38:27] says I should eat more fruits. Wow, we
[38:30] just built the cornerstone for our auto
[38:32] regressive model. It is the generation
[38:33] of a single word. Okay, so now let's try
[38:36] and generate two words. Let's be fancy
[38:38] about it. Great, I'm going to load up
[38:41] the GPT-2 medium model from hugging
[38:43] face. Why did I choose medium and not
[38:45] small? We're going to mostly work with
[38:46] small in this
[38:48] uh in this
[38:49] uh in this uh entire workshop. But, um
[38:52] we use medium cuz it's just better at
[38:54] holding information and our little test
[38:56] is going to be a knowledge retention
[38:57] test or knowledge retrieval test. It's
[38:59] the capital of Texas is and I'd like it
[39:02] to know that the answer is Austin.
[39:04] Austin is two tokens, Aus and tin. You
[39:06] don't have to even remember the that
[39:08] it's two tokens or what a token is. But,
[39:10] so okay, I went to hugging face here. I
[39:12] loaded the model. I called generate max
[39:15] tokens new. Uh the max new tokens equals
[39:19] two and then when I run that, it says
[39:21] the answer to the capital of Texas is
[39:23] Austin. Really cool. This model that has
[39:26] just read the internet somehow learned
[39:28] that the capital of Texas is Austin.
[39:31] Very nifty. Okay, so now I've generated
[39:34] one token, I've generated two tokens.
[39:35] This is starting to get ridiculous. When
[39:36] I want to do three, what I write three
[39:38] in here? No, that doesn't make any
[39:39] sense. I'm probably going to build an
[39:41] auto regressive loop. Okay, so what's an
[39:43] auto regressive loop? I'm going to say I
[39:45] will run it for 20 time. I'm going to
[39:47] generate one token and then I'm going to
[39:50] ask the model
[39:51] to give me one token at a time and
[39:53] that's really how the dot generate
[39:54] method is implemented internally. For us
[39:56] for right now, I think it's okay to just
[39:58] call dot generate in a loop. So, I'm
[40:01] going to say run this 20 time. Here's a
[40:03] fun fact and our model says here's a
[40:05] fact first fun fact, the first time I
[40:07] saw the movie, I was in the theater with
[40:09] my parents. What a touching heartfelt
[40:13] memory from GPT-2 medium. Truly I'm
[40:16] moved and touched. Okay, so now I ran
[40:20] this thing in a loop. That's really
[40:22] great, but I still hard coded the number
[40:24] 20. Maybe I want to stop it right at
[40:29] uh when the model thinks we should end
[40:31] the generation. So, I'm going to still
[40:34] call that generate. I'm still going to
[40:35] call it with max one token, but I'm give
[40:37] going to give it uh an end token ID
[40:41] uh that is end of end of string token
[40:43] ID. The model was trained on that. And
[40:45] I'm going to say, "If you ever see that
[40:46] token, just stop." Maximum safety cap
[40:50] 200 tokens.
[40:53] >> [snorts]
[40:53] >> So, I'm calling dot generate with one
[40:55] token at a time.
[40:57] And that's great. And when I hit the
[40:59] last end of string token, end of
[41:01] sentence token, I'm going to run that
[41:04] with uh I'm going to just stop this
[41:06] loop. So, 200 becomes the maximum number
[41:08] that we're going to run this in. And
[41:10] then, "The capital of France is Paris.
[41:13] And the city's population has grown by
[41:14] more than 50% since the 1970s. The
[41:17] French are very diverse people with many
[41:18] ethnicities. French-speaking countries
[41:20] include Algeria, Morocco, etc. But, they
[41:22] have one thing in common.
[41:24] They love to eat." Wow, the model knows
[41:27] a lot of things. It knows about
[41:28] French-speaking countries. It knows that
[41:30] French people love to eat, so on and so
[41:32] forth. What's important here is we
[41:34] generate one token at a time in an auto
[41:36] regressive loop. This is our first like
[41:39] real building of intuition through code.
[41:41] This is what an auto regressive loop is
[41:42] generally going to look like. It's going
[41:44] to have a maximum number of tokens
[41:46] you're going to want to generate. And
[41:47] it's going to have the end of string uh
[41:50] stopper for the loop. Great. So, now
[41:52] we're going to visualize these
[41:53] probabilities. You don't have to know
[41:55] this code specifically.
[41:57] Uh what you will what I will say about
[41:59] this code is that by the end of this
[42:01] workshop, you will know how to read it
[42:02] almost perfectly. You'll know what
[42:04] softmax is. You'll know what logits are.
[42:06] You'll know what a tokenizer is. You'll
[42:08] know what a model invocation does. You
[42:10] know what a top K is. you kind of know
[42:11] that already. Great.
[42:14] But you don't have to know this code.
[42:16] What this code does is it generates us
[42:18] the probabilities for the currency of
[42:20] the United States is the and then it's
[42:23] going to go with the dollar, the U for
[42:25] the maybe U.S. dot, right? You maybe you
[42:29] just US and silver and gold and federal
[42:33] and green and euro and same, right? And
[42:36] we can see this list this very long tail
[42:39] of options that we don't really care
[42:41] about but we see dollar is kind of
[42:42] coming up here as the top probability.
[42:44] So this tells us a lot. The model is
[42:46] coming up with 50,000 something options.
[42:48] I'm only showing the top 20 options here
[42:50] or 150,000 depending on the model.
[42:53] So now we have these options visualized.
[42:55] We probably want to sample from them. We
[42:56] learned about temperature earlier. So
[42:58] one option of specifying a temperature
[43:00] and this is maybe the easiest option in
[43:02] the dot generate method. I'm just going
[43:04] to call temperature point eight. That's
[43:06] pretty common setting to run it on. I'm
[43:09] actually not familiar with the recent
[43:10] research of what frontier models are
[43:12] trained and
[43:14] uh are run on run on but it'll probably
[43:16] be pretty close to point eight.
[43:19] Uh so when we run the meaning the
[43:23] meaning of life is and then it goes like
[43:26] the meaning of life is a
[43:27] right? It created some nonsense here
[43:31] uh but it's important to see how
[43:32] temperature works. So temperature didn't
[43:34] really work for our in our benefit here
[43:36] but maybe it will in the future.
[43:39] Great. Uh let's do temperature with
[43:41] math. We we know the formula for
[43:44] uh for for temperature. We know that we
[43:47] take the exponent of the input
[43:50] probability or input logic, whatever
[43:52] logic might be, divided by the
[43:54] temperature and divided by the
[43:55] denominator. What is the denominator?
[43:57] It's the sum of all of the inputs
[44:00] divided by the temperature. Input
[44:02] divided by temperature exponent. That's
[44:04] what temperature does. I don't
[44:05] necessarily know what these numbers are.
[44:07] They're maybe something called logits,
[44:09] which are the outputs of machine
[44:10] learning models, but there's something
[44:11] like 2.1, 1.3, .2, -4.5. But at the end
[44:15] of running it through this temperature
[44:17] formula, we've got 66%, 24%, 6%, and 2%.
[44:21] Very close to 100%. Very, very cool.
[44:24] We've converted our whatever these
[44:26] numbers were using temperature math to
[44:29] probabilities. That's actually really
[44:32] cool to see. Okay. So, now we have
[44:35] another way of implementing
[44:37] um
[44:38] implementing temperature. That's a third
[44:40] way of implementing temperature. We
[44:41] implemented by using the generate
[44:43] method, right? Option one is just put it
[44:45] in the generate method.
[44:47] Pretty good easy way of doing it.
[44:48] Another option is writing some CPU
[44:50] Python code. We'll see later why that's
[44:52] not a good idea. And then that's I think
[44:54] in section five. And then here we have a
[44:58] really well-performing option of
[45:00] implementing it. We're not going to go
[45:02] over this code. What's really important
[45:04] is to notice that we're calling
[45:05] something torch.multinomial,
[45:08] which does uh selection of items
[45:11] randomly based on their weights
[45:13] uh at the end. So, this does a little
[45:15] bit of the work of setting up uh the
[45:18] tokens divided by temperature, and then
[45:20] we do the scaling, but most importantly,
[45:22] we do selection with torch.multinomial.
[45:25] And when we do that uh with a
[45:26] temperature of one, we can see the
[45:28] currency of the United States is the
[45:29] United States, and then it's going to
[45:31] complete United, then States, then
[45:33] dollar. Very cool. Okay, so we talked
[45:35] about top K earlier, and we actually saw
[45:37] that there is a built-in top K method,
[45:40] but if we wanted to implement it
[45:41] ourselves, again, we're not going to go
[45:43] over this code, but we could see it's
[45:44] got a top K of 50 items. Limit means
[45:47] we're doing the first 50 items. And then
[45:49] we're going to do something something
[45:51] softmax here. We're going to divide by
[45:53] things. Really, I don't know what a
[45:54] softmax is. Maybe I'll learn about it
[45:56] more in section 14. Most importantly, it
[45:58] calls torch.multinomial. It does
[46:00] selection with replacement. What does
[46:02] that mean? It means we keep choosing
[46:04] from the same items over and over again.
[46:06] Great. And then that's going to add the
[46:08] currency of the United States is the
[46:09] dollar. Really interestingly, when we
[46:11] limited our selection to the top 50
[46:13] items, we kind of got to the right
[46:14] answer here.
[46:16] Really cool. It It like it limits us to
[46:18] only the most relevant options. Maybe
[46:20] for this prompt, we could have limited
[46:22] to the top five items. But we've chosen
[46:24] top K for this example. And the last
[46:27] sampling strategy we're going to see is
[46:28] top P. Remember those are the cumulative
[46:30] top probabilities. Again, we're not
[46:32] going to explain what torch.com sum is.
[46:35] Cumulative sum. We're going to get to
[46:37] the cumulative sum of numbers. But most
[46:39] importantly, we can see that it calls
[46:41] torch.multinomial,
[46:43] which does the selection of this array
[46:46] after it was formatted. So we saw the
[46:48] math in Excel. Now we have code it
[46:50] implemented. We didn't review it
[46:52] specifically, but importantly, let's see
[46:54] how that we can implement it pretty
[46:56] easily. We saw how we implement in CPU
[46:58] code. We saw how we can implement it in
[47:01] kind of like more GPU native friendly
[47:03] code. You don't have to know this code
[47:04] right now, but importantly, it does
[47:06] torch.multinomial.
[47:08] Right. Now we get to an exercise, and I
[47:10] would like for you to complete the
[47:11] sentence, "The meaning of life is" The
[47:14] way you're going to do that is you're
[47:15] going to go all the way up to section
[47:16] three. You're going to copy this
[47:17] autoregressive loop. And then you're
[47:19] going to copy it here into this
[47:21] exercise, and you're going to change the
[47:22] prompt. Okay. So now I'll mention to you
[47:25] something really important. Every one of
[47:27] the exercises I'm going to assign to you
[47:29] has an answer. Maybe you're too busy to
[47:30] look at and write your own answers and
[47:32] think about it. So if you look at the
[47:34] answer, you could click show code and
[47:36] see the answer for this exercise. Not
[47:38] going to do that for you because the
[47:39] exercise is literally the answer to your
[47:41] autoregressive loop section three. Or uh
[47:44] topic three here in this Colab notebook.
[47:46] But when it generates the answer, it
[47:49] says the meaning of life is to be happy.
[47:51] To be happy is to be free. Right? Very
[47:54] cool life philosophy we got from GPT-2
[47:56] here. I'm going to read uh Eat, Pray,
[47:59] Love right after I'm done with this
[48:01] GPT-2 demo. Very cool to to look at
[48:04] this. You should do this exercise
[48:06] yourself. I think learning how to use
[48:07] {dot} generate is maybe the most useful
[48:09] skill you're going to get from this
[48:11] module
[48:12] or the section. Uh mostly because you're
[48:15] going to do that a lot if you work with
[48:17] LLMs. Uh implementing your own top K,
[48:19] top P, temperature probably not
[48:21] something you're ever going to do. Using
[48:23] top P, top K, temperature much more
[48:26] likely. So now you have you know how to
[48:29] do that with the {dot} generate method.
[48:31] Great. So let's go back to our uh uh
[48:34] uh
[48:35] slides. And we could see here what what
[48:38] did we learn in this section? Intro to
[48:39] LLMs. We said you were going to take
[48:42] next word prediction. We know how
[48:43] autoregressive loops work. Temperature,
[48:46] top K, and top P. So we learned about
[48:48] what LLMs are. We learned that they're
[48:49] they generate text. They are
[48:51] autoregressive. That they're machine
[48:52] learning models. What does that mean? I
[48:54] don't know. We're going to learn that in
[48:55] the next couple of sections, several
[48:57] sections. They're deep neural networks.
[48:59] We learned that we would ideally run a
[49:01] bias search to find the most ideal beam
[49:04] search to find the most ideal sentence.
[49:07] But we can't do that cuz we'll have to
[49:08] wait until the heat death of the
[49:09] universe.
[49:11] So instead we have like fun
[49:12] kind of like hacks to like use
[49:14] temperature and then like either
[49:17] flattens the differences or extend or
[49:20] enhances the differences. We learned
[49:22] that we have top K to limit selection to
[49:24] the most relevant top K items or top P
[49:28] probability which limits it to the top
[49:30] cumulative sum probabilities. And then
[49:32] we learned how to use the
[49:33] model.generate.
[49:35] Cool. So we saw an Excel demo that gives
[49:37] you an intuition for this math. And then
[49:39] we saw code that shows you how to call
[49:41] {dot} generate and how to write Python
[49:43] CPU code for these math one math
[49:45] formulas that we learned. And then we
[49:46] saw some really effective GPU code that
[49:49] we didn't really go into. We you'll
[49:50] understand how it runs by the end of
[49:52] this uh whole workshop, but for now we
[49:55] built an intuition on how to use these
[49:56] three different things. Generate with
[49:58] its parameters, how to write our own
[50:01] code, like implement the formula
[50:02] ourselves, and then how to write GPU of
[50:04] performing code. And we're going to
[50:05] spend a lot more time talking about the
[50:07] differences between CPU and GPU code.
[50:10] Okay, in the next section we're going to
[50:12] have is reverse engineer LLMs. I really
[50:14] hope you'll join me for that. This is
[50:16] going to be a kind of meaty section
[50:18] because now I'm going to ask you to sit
[50:20] through more sections. Oh my god,
[50:22] Justin, why would you ask me to do that?
[50:24] The answer is going to be in the reverse
[50:26] engineer LLM section. We're going to
[50:27] take a real large language model. We're
[50:29] going to reverse engineer it and that's
[50:31] going to give us the workshop for the
[50:32] the road map for the rest of this
[50:34] workshop.
[50:35] Great, so I'll see you next in this next
[50:37] section.
