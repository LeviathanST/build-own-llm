# Pre-training | Build Your Own LLM Workshop #19

**Build Your Own LLM Workshop — Video #19 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 1h 12m 50s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=nN335-483Pg |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to building
[00:02] our own large language model workshop.
[00:04] I'm Justin Angel and so far we've seen
[00:08] all of the architecture for large
[00:10] language models, specifically
[00:11] transformer-based ones, and how to train
[00:14] a machine learning model, how to use a
[00:16] large language model. The only thing
[00:18] that we're missing is what data are we
[00:20] training our large language model on.
[00:22] And by the end of this section, we will
[00:24] have our own pre-training script and
[00:26] then we will have all of our data up and
[00:29] running and ready to go. So great. So
[00:31] our goals for this mo for this section
[00:34] is to learn about fine web edu which is
[00:36] the data set we're going to use what's
[00:38] binning and create our pre-training
[00:40] collab notebooks. I will highlight
[00:43] there's no Excel worksheet for this
[00:46] section because there's nothing new that
[00:47] I'm teaching you here in that sense.
[00:50] So let's get started. First thing we
[00:53] want to know is what's speed training
[00:54] like we start every section. What
[00:56] problem are we trying to solve? So the
[00:58] question that I have for you is how do
[01:00] we teach large language models English?
[01:02] You know about back propagation, you
[01:04] know about the transformer architecture,
[01:06] you know we have to show it something
[01:08] have some loss and based on that back
[01:10] propagate and update weights. So what's
[01:13] the solution to how do we train large
[01:15] language models in English is we train
[01:17] them based on word distribution in a
[01:20] massive corpus. Corpus is just a way of
[01:22] saying a large collection of text. So
[01:26] that is effectively it once we combine a
[01:29] massive amount of human readable text or
[01:31] human written text with back propagation
[01:34] and the transformer architecture it
[01:36] learns English it learns previous words
[01:38] it learns uh knowledge it learns all of
[01:42] those things. So how so now our job is
[01:45] to find that data maybe clean it up a
[01:47] bit and then show it to the LLM. This
[01:50] slide is about the showing it to the LLM
[01:54] section. So LLM's pre-training loss
[01:56] function is based on being able to
[01:58] predict the next token. We all kind of
[02:00] know that because the way large language
[02:02] models work is they predict the next
[02:03] token. So it also makes sense that by
[02:05] training them, we train them on finding
[02:07] the next token.
[02:10] Uh we've talked about loss function
[02:12] adnauseum in section 7 and since then
[02:15] we're going to use cross entropy because
[02:17] we have to generate multiple
[02:18] probabilities. Great. So now I'm going
[02:20] to introduce you to the notion of
[02:22] pre-training. Pre-training is going to
[02:24] teach us basic language skill. It
[02:26] teaches the model English. I use English
[02:29] as place loader for language from a
[02:31] massive data set. How do we do that? We
[02:33] compress a bunch of language into the
[02:36] model weights and then we use those
[02:38] weights to generate text based on that.
[02:40] And we'll talk about mid training in a
[02:42] moment. I do want to show you how
[02:44] pre-training works. I know it's going to
[02:46] be a lot of code. Like we like I
[02:47] jokingly said, we spend sections and
[02:50] sections of time spending talking about
[02:52] new topics ends up being two lines of
[02:54] code. Pre-training kind of similar to
[02:57] that. It ends up being like two lines of
[02:59] codeish for this like how do we train a
[03:01] large language model. So we have our
[03:03] input tokens which go from start plus
[03:06] the to the context length. So let's say
[03:09] I have a I have a a text corpus of
[03:12] 100,000 words and my context length is
[03:15] 100 is 1,024. So I'm going to run this
[03:18] from the star wherever I'm starting in
[03:20] that corpus of a thou 100,000 words to
[03:23] the star plus the context length. So
[03:25] we'll show it a,000 words. My target
[03:28] tokens I'm going to shift everything one
[03:30] to the right and then I'm going to lose
[03:32] that first word. And then I hope that
[03:34] what the large language module generates
[03:37] uh sorry what like my target is is going
[03:39] to be the first the the last 10,023
[03:43] words plus the one word that it
[03:45] predicted. What does that look like in
[03:47] practice? The capital of Texas is
[03:49] Austin. Let's say we're trying to
[03:51] generate that sentence. My input tokens
[03:53] are going to be the capital of Texas is
[03:56] and my target is going to be capital of
[03:58] Texas is and then we add Austin. Notice
[04:00] I dropped that first the and then I
[04:02] added the target token. Based on that,
[04:06] I'm going to uh want to have uh the the
[04:09] model is going to generate a bunch of
[04:11] probabilities. We know it generates
[04:13] logits, but we know how to translate
[04:14] those to probabilities and just makes
[04:16] more sense to think about probabilities
[04:18] to me. We know that the percentage
[04:20] likelihood that it's correct is 72. We
[04:22] then do loss of minus log, which is just
[04:25] the cross entropy formula. We get a loss
[04:27] function of.33. We then back propagate
[04:30] from that loss function. Why is there
[04:32] still loss? It did predict Austin at 72%
[04:35] but also predicted it not at 100% and it
[04:38] also predicted it uh a bunch of other
[04:40] awards as well like Dallas, Houston and
[04:42] San R San Antonio potentially. Um so
[04:45] based on that like mismatch with like
[04:48] the one sentence target that I had not
[04:50] all the sentence targets just one
[04:52] sentence target there's a loss of.33.
[04:54] I'll go back and do back propagation
[04:57] based on that and update all the
[04:58] weights. So the probability is a little
[05:00] bit higher the next time I run it.
[05:02] That's it. We we now understand how all
[05:05] pre-training effectively runs. It's next
[05:08] token training based on the next token
[05:11] in the sentence based on the training
[05:12] corpus. We calculate the the loss
[05:15] function based on why isn't this 100%
[05:18] and why isn't everything else at a zero.
[05:20] We have cross entropy loss based on
[05:22] those probabilities. And then we do back
[05:25] propagation on that. That is effectively
[05:27] it. That is the magic of pre-training.
[05:29] You show a model a bunch of text data
[05:33] and that's going to and then it's going
[05:34] to like back propagate and learn all the
[05:36] weights and learn how the English
[05:37] language works through the magic of the
[05:39] transformer architecture and back
[05:40] propagation. That's why we spent two
[05:43] large modules. One teaching us about
[05:45] back propagation and the other one
[05:46] teaching us about the transformer
[05:48] architecture. We're now in the other
[05:50] module of post- training and
[05:51] pre-training.
[05:52] Okay. Okay, so I mentioned there's this
[05:54] thing called pre-training and
[05:55] post-training. Um, that's kind of an
[05:58] arbitrary line. This this thing we can
[05:59] call mid-training. What's mid-training?
[06:02] It became really common after 2019. It's
[06:05] now that the model speaks English.
[06:07] Again, I use English as a placeholder
[06:08] for language. We want to teach it and
[06:11] maybe it has a little bit of knowledge
[06:13] as well. Um, in mid training, we want to
[06:16] use the language effectively for its job
[06:18] as a large language model. What is its
[06:20] job? It answers questions. So it needs
[06:22] to think maybe we want to like expand
[06:25] the number of tokens it can reason on
[06:29] beyond the average number of token in
[06:31] our pre-training data set. So we'll work
[06:33] on lock text. There's a bunch of things
[06:35] that mid training does. We're not going
[06:36] to show mid-training examples in this
[06:38] workshop. But it's worth for you to know
[06:40] that there's this other stage that's not
[06:42] pre-training, that's not post- training.
[06:45] We call it mid training. Great. So we
[06:47] learned about pre-training and how it
[06:49] works. Now let's talk about scaling laws
[06:51] specifically from the lens of data which
[06:52] is I think the first time it becomes
[06:54] really programmatic for us to talk about
[06:56] scaling laws for real.
[06:58] Um so one thing we know about uh about
[07:02] large language models is that we can
[07:05] predict their performance based on
[07:06] combining data compute and parameters.
[07:09] What does that mean? We'll learn in this
[07:11] one section and it make it very very
[07:13] applied. So LLMs are trained on human
[07:16] written text. We've just learned that.
[07:18] But the real question we have right now
[07:20] because we still need to go write a
[07:21] pre-training script is how much data
[07:23] should we show it, right? What is the
[07:25] correct amount of data that we need to
[07:27] show our large language models? So
[07:29] luckily for us, pre-training uh follows
[07:33] a very specific loss scaling law. Uh
[07:36] that means that there's ratios between
[07:39] compute measured in flops uh model size
[07:43] measured in the number of parameters and
[07:45] data me measured in the number of tokens
[07:47] it sees and we have laws that can
[07:49] correlate between those and kind of
[07:51] predict the loss. Right? are really
[07:53] great on the on the side on the right
[07:55] here, we could see a scaling law chart
[07:59] that can predict validation loss based
[08:01] on each one of these lines is compute
[08:03] and its relationship with the size of
[08:05] the training corpus. So that's every
[08:08] line in this chart here on the middle
[08:11] left is going to be a different amount
[08:13] of compute that we've spent, different
[08:15] number of flops, how long we let the
[08:17] algorithm run, and how many GPUs.
[08:20] And it's going to show us how many
[08:22] training tokens are needed. We can see
[08:24] that too many token take training
[08:26] tokens, the loss goes back up. Not
[08:27] enough training tokens, the loss is like
[08:30] too high. So we want to have that sweet
[08:32] spot in the middle. That's that's a
[08:34] scaling out, that sweet spot in the
[08:35] middle, right? And we can see that now
[08:37] there's like a real ratio between
[08:39] compute and flops and training to and
[08:42] the amount of training tokens we want to
[08:44] have to fit that on a line to have
[08:46] optimal loss. Great. So that's from uh
[08:50] did I say where this is from? This is I
[08:52] think from Llama 3. Maybe this is
[08:55] Chinchilla. But a bunch of people have
[08:58] recreated training loss as well. So I
[09:01] think the chart in the bottom uh right
[09:03] is going to be from mini PC CPM where
[09:06] they've also been able to recreate very
[09:08] similarly training loss tokens how much
[09:11] compute we do fit it on a line you could
[09:13] predict that if you throw in more data
[09:14] more tokens more you're going to reduce
[09:16] the training loss even further. So
[09:18] that's scaling laws. It's our ability to
[09:20] predict the future based on how much
[09:22] data, how much uh how many parameters,
[09:26] how many uh how much compute and GPUs,
[09:29] right? We end up giving our training. We
[09:31] can then predict how good the model is
[09:32] going to be in terms of training loss.
[09:35] Okay. So according to Ginchilla 2022,
[09:37] which is maybe I think the first of the
[09:39] scaling laws for large language models,
[09:41] um we are going to need a 20:1 token to
[09:45] parameter ratio. So I if I have a model
[09:48] that's let's say 70 billion parameters,
[09:50] I'm going to have to show it times 20
[09:53] 1.4 trillion tokens. That's a lot of
[09:56] tokens, right? We're going to have to
[09:57] show it a lot of tokens, but that's the
[09:59] ideal ratio. You could also follow a
[10:01] similar ratio to calculate how much
[10:03] compute we're going to need, how many
[10:05] GPUs we're going to need running in
[10:06] parallel, and so on.
[10:09] But we're talking about scaling loss for
[10:10] data, not compute right now. So there
[10:13] isn't a consensus here, and it's really
[10:14] important to mention that. So chinchilla
[10:17] said 20 to1. Uh and we've seen
[10:19] chinchilla before. That's the
[10:20] irreducible complexity of language
[10:22] paper. Uh similarly llama 3 derived at a
[10:25] 39 to1 ratio like approximately 40
[10:29] tokens per 40 uh tokens of data per one
[10:33] parameter. Uh uh hundman which is 10
[10:37] cent uh predicted 96 to1 ratio. Mini CPM
[10:41] with uh predicted 192 to1. I should
[10:44] mention the other two are based on
[10:46] mixture of experts which is maybe why
[10:48] they need so much more data because not
[10:50] all the network is active at all the
[10:52] time. You don't know anything about
[10:53] mixture of experts. Totally fine. Don't
[10:56] worry about it. But there's different
[10:57] ratios here that we could see. So some
[10:59] between 20 to1 and 200 to1 is probably
[11:03] going to be the ratio that we're going
[11:04] to need. We're going to use 40 to1
[11:07] ratio. Why? It sounds good to me and I'm
[11:09] I'm happy with this ratio. Great. So
[11:12] where do we get this tremendous amount
[11:15] of tokens? Like even the small 70
[11:18] billion model which is much smaller than
[11:20] any of the frontier models needs a
[11:22] trillion tokens. That is quite a lot of
[11:24] text we're going to need. So let's talk
[11:26] about what are the potential data
[11:27] sources we're going to be able to get
[11:29] that data from. So the number one
[11:31] option, the biggest one of them all is
[11:33] we could crawl the entirety of the
[11:35] internet and we can use that data to
[11:38] train our large language model. Sounds
[11:40] simple, right? the internet full of
[11:41] text. That makes sense. We're going to
[11:43] spend this entire section explaining why
[11:45] it's not that simple. Why is that not
[11:47] that simple? It's massive, which is
[11:49] great. It's the biggest token source we
[11:50] can find, but it's messy. It's often low
[11:53] quality. It is multilingual, which is
[11:56] great, but it's full of biased data,
[11:57] right? If we train it on some
[12:00] subreddits, we're going to have some
[12:01] amount of problems.
[12:03] Great. Another data source that is the
[12:05] almost the exact opposite of internet
[12:08] data are is books. books are pretty high
[12:10] quality when you think about it. They
[12:12] have to go through editors and stuff
[12:13] like that. There's a whole thing like
[12:15] people lock it in and then uh but we
[12:19] have problems with how much data is
[12:21] available. A lot less than the entirety
[12:23] of the internet. Order of magnitude
[12:25] three orders of magnitudes less. That's
[12:27] a lot less books. And we have a bunch of
[12:30] copyright issues. If I just grab a book
[12:32] off the shelf behind me and try and feed
[12:34] it to an LLM, we're going to have
[12:35] copyright issues. And we'll see that
[12:37] when we talk more about books. Okay. So,
[12:40] another source of data that we have
[12:41] because we want high quality data that
[12:44] doesn't isn't fraud with copyright
[12:45] issues and isn't doesn't have limited
[12:48] access. We could use academic
[12:49] publishing. So, academic publishing
[12:51] could be archive for STEM fields. It
[12:54] could be PubMed for medicine. Could be
[12:56] free law for law. These tend to be
[12:58] pretty high high quality. We have like 9
[13:01] 10 pages of well-written text. goes
[13:04] through multiple cycle of peerreview.
[13:06] That's really really great. So readily
[13:08] available. We could just go download all
[13:10] of archive and it's pretty high quality.
[13:13] Another set of data sources we have are
[13:15] domain specific. Why do we need domain
[13:17] specific things? Cuz sometimes we want
[13:19] our large language models to do things
[13:20] that isn't just talk English. They need
[13:22] to solve math equations. They need to
[13:24] write code, right? They need to write
[13:27] email. I guess we'll talk more about
[13:29] that in a moment. Um, so code, math, and
[13:32] email are all data sets we can go get.
[13:35] For example, we could go download all of
[13:37] GitHub. We can then train a large
[13:38] language model on that. It can learn how
[13:40] to code. Another set of data sources
[13:43] that we have is user user generated data
[13:46] sources. So proprietary websites like
[13:49] YouTube, Twitter, Facebook, so on have a
[13:51] lot of data. If when if each of these uh
[13:54] tech companies generates a large
[13:58] language model, let's say Google has
[14:00] something called Gemini. Fair to assume
[14:02] it's trained on YouTube transcripts,
[14:04] right? So Twitter is owned by another
[14:05] company that has a large language model.
[14:07] So is and Facebook also has its own
[14:10] large language models. Safe to assume
[14:12] that they train data based on that.
[14:13] Reddit opensource like like let's say
[14:15] that it's like they don't train their
[14:17] own data set, but they do license to
[14:19] other people. There's also Q&A websites
[14:21] like Stack Overflow. Finally, let's talk
[14:24] about synthetic data. I wrote it down as
[14:26] 10 the^ of 10 tokens are available. I'm
[14:28] probably wrong at this point, but that's
[14:30] the best data source that I have uh at
[14:33] least in terms of like peer-reviewed
[14:34] anything. Why not, now that we have
[14:37] these amazing large language models, we
[14:39] don't live in 2019, why not just have
[14:41] them train uh data and create what we
[14:45] call synthetic data on data that they
[14:48] themselves generated. So we take really
[14:49] smart models, we train really stupid
[14:51] models with that. We keep going back and
[14:52] forth until we get to like really great
[14:54] models. Uh verifiably from the open-
[14:58] source data that I have access to,
[14:59] that's a relatively small corpus of
[15:02] data. It is almost guaranteed at this
[15:05] point that the Frontier and Neolabs have
[15:08] their own sources of synthetic data.
[15:10] There's whole companies dedicated to
[15:11] generating synthetic data and they have
[15:13] multi-million dollar contracts. So it's
[15:15] very likely to assume that synthetic
[15:17] data is one bigger than that right now
[15:20] and two might become the dominant source
[15:22] of data in the future right because it
[15:24] has unlimited potential whereas all of
[15:26] these other things are going to be
[15:27] limited great our architecture decision
[15:30] for this section is we'll use academic
[15:32] data why we're just training GPT too
[15:34] small we need 124 million tokens even
[15:37] multiplied by 20 multiplied by 40
[15:39] there's enough academic data for us
[15:40] that's high quality we're not going to
[15:42] pick up a lot of bias from it and it's
[15:44] readily available. We could just train
[15:46] based on that. So, we're going to use
[15:47] academic data for our large language
[15:49] model pre-training.
[15:52] Let's really deep dive into each one of
[15:54] these and at least see some more
[15:55] specifics. So, we talked about books.
[15:57] Small amount of data, not easily
[15:59] accessible, lots of copyright issues.
[16:02] So, first data set that I want to chat
[16:04] about is B book corpus from 2015. 7,000
[16:08] self-published books. They were all I
[16:11] think uh either downloaded or scraped. I
[16:13] don't remember the specific story but uh
[16:15] it was copyright taken down. Some people
[16:18] probably still use it to trade. You
[16:19] can't easily get it from hugging face.
[16:21] Okay. Then we have books 1 2 3. These
[16:24] were created sequentially based on the
[16:25] name. I think it's pretty obvious. In
[16:28] books three in 2020 had about 200,000
[16:31] books from famous authors. What is what
[16:34] do you mean by famous authors? Margaret
[16:36] Atwood, right? These are real books from
[16:38] real authors. uh it was placed on a
[16:41] bunch of websites. You can go download
[16:42] that.
[16:44] If you go read the pile, pile is just an
[16:48] amalgamation of sources. They take a
[16:50] bunch of books and a bunch of academic
[16:51] data and a bunch of coding and so on and
[16:53] they put it together. When you read
[16:55] their description of books three, all
[16:57] they say is no additional details. Every
[16:59] one of the other data sources gets a lot
[17:01] of a lot of um a lot of details. Really,
[17:05] they didn't say anything about books
[17:06] three. They don't want to get in
[17:07] trouble. So if you look at the
[17:09] composition of the pile uh you could see
[17:11] that it has a bunch of stuff from PubMed
[17:14] and free law like so all these high high
[17:17] value academic sources. It has a little
[17:19] bit of data from the internet the green
[17:22] blobs. It has a bunch of data from books
[17:26] somewhere here like you'll able to see
[17:28] it. It has some coding. So we know that
[17:30] these now get like combined together.
[17:33] Other data sources for books, Project
[17:35] Gutenberg, 75,000 public domain books
[17:38] hasn't been taken down yet. That's
[17:40] amazing. Another data source is libgen
[17:43] or Andes archive or whatever book
[17:46] pirating website is most popular today.
[17:48] Uh it has tens of let's say a 10 million
[17:51] amount of like books. Um very very
[17:54] likely based on their website that
[17:56] they've like contracted out to a bunch
[17:58] of labs to train models on. How do we
[18:01] know that? You go to Anna's archive.
[18:03] They have a page dedicated to licensing
[18:06] uh and sharing their contact for
[18:08] $250,000 with any AA lab that wants you
[18:11] drop them an email, you get 10 million
[18:13] books. If you're a lab and you start for
[18:15] for training data, really really easy to
[18:18] know to to think that you might like go
[18:20] and use that. Um readers prefer AI
[18:23] trained copyrighted books over human
[18:25] expert human writers. You know, why is
[18:28] books so so appealing even though
[18:30] they're so fraught with copyright? Even
[18:32] though there's other high quality data
[18:34] sources, once we give large language
[18:36] models books, users prefer the the
[18:39] quality of the writing over like even
[18:40] expert human writers and especially LLMs
[18:43] that look were not trained on books. So
[18:45] very very hard to train a commercial
[18:47] large language model without books.
[18:51] What's another set of data sources?
[18:52] We've talked about scientific and
[18:54] reference. We have archive for STEM,
[18:56] PubMed for medicine, free law and so on.
[18:58] So 10 million plus highquality articles
[19:01] available for us. You could just go
[19:03] ahead run a crawl or download them
[19:05] overnight over a week whatever available
[19:07] as public data sets as well. Wikipedia
[19:10] has 50 million cited articles in 300
[19:13] languages and it's in creative comments.
[19:15] Very tempting to train large language
[19:17] models based on that. P2SO has all
[19:21] semantic scholar downloaded 440 million
[19:24] articles and is available in larger uh
[19:27] composite data sets like Zida. We've got
[19:30] the distribution for Zida on the left.
[19:32] You could see that it's got uh archive
[19:35] in there and P2SO is 4% and then it's
[19:38] got U C4 which is CRM and crawl. So
[19:41] that's internet data. Uh it has star
[19:44] code which is coding and so on and so
[19:45] forth. Um, if we wanted to see the
[19:48] distribution, we could see that in the
[19:50] bottom left there's something like, hey,
[19:53] the n raw number of tokens here is about
[19:55] 2 trillion. If I do a first pass quality
[19:59] filtering, it's 1.5 trillion tokens. If
[20:02] I do a second pass to 40% quality, I'm
[20:04] at 1.3 million tokens or 1.2 trillion
[20:07] tokens. So, you could just pull that
[20:09] data set tomorrow if you need a trillion
[20:11] tokens and just train your large
[20:12] language model based on that. and that
[20:15] contains the scientific reference we
[20:16] were just talking about.
[20:19] What are other data sources? We talked
[20:20] about domain specific data sets. So you
[20:22] could go use GitHub. It has all of the
[20:24] ro code of many open source projects.
[20:27] You can query it even hourly using
[20:28] bitquery and get all of the updates and
[20:30] you could train based on that. Uh you
[20:32] could use the stack which is another one
[20:35] of these uh kind of like the pile
[20:37] combined repos and it has and star coder
[20:40] data contains a lot of cleaned up
[20:42] versions of GitHub. GitHub's full of a
[20:44] lot of stuff you probably don't want to
[20:46] train large language models on
[20:47] repetitive code so on like config files
[20:50] that don't make sense binaries that
[20:51] don't make sense so you want to clean
[20:52] that up so star quarter data does that
[20:55] uh you have proof pile for math it has
[20:57] 50 plus thousand uh math proofs so if
[21:00] you want to train a model that could do
[21:01] math proofs you could use that GSM8K
[21:05] that's actually more of an evaluation uh
[21:08] data set but if you look at it it also
[21:10] has training data why it's pretty easy
[21:13] to like take a bunch of high school uh
[21:16] sort of grade school level math, show it
[21:18] to a model. It's got the full proof in
[21:20] there. We could use it to train data as
[21:22] well, not just test on it. Uh the
[21:25] funniest of these repos, Enron emails,
[21:27] there's 50,000 emails from Enron that
[21:30] came out during discovery. If you're
[21:31] trying to train a model that helps with
[21:33] email authoring and the Enron emails
[21:36] might be a good data source for that,
[21:37] right? Because like emails are not just
[21:40] generic generic language. there like a
[21:42] specific way of writing emails. It makes
[21:44] sense.
[21:46] >> Uh next data source we're going to cover
[21:48] is user generated data that say you can
[21:50] read all of Reddit. So it has 500
[21:52] million uh messages that were available
[21:55] until 2023. Everything post 2023 Reddit
[21:58] decided to monetize and makes available
[22:00] for a price to large language model
[22:02] providers. I'm going to read you one of
[22:04] the things from the 2023 data sets from
[22:07] the subreddit lucid dreaming. So the
[22:09] other night I managed to become lucid in
[22:11] a dream. I was trying to take control of
[22:13] the dream, but I realized I was not
[22:14] dreaming too deeply. I walked over to a
[22:17] computer console looking over a thing
[22:20] and then the computer made a sound. It
[22:21] startled me like this sounds like
[22:23] gibberish to me. This sounds like AI
[22:25] generated
[22:27] GPT2
[22:29] uh uh text. It is in fact the human
[22:33] training data set from usergenerated uh
[22:36] uh Reddit. Right? So important to
[22:38] realize this is not a high quality data
[22:40] source, but it does give you a lot of
[22:41] English fluency. Other data sources,
[22:43] Stack Overflow, 50 million plus Stack
[22:46] Overflow threads also now being licensed
[22:48] to large language models. You could use
[22:50] that to train your debugging agents,
[22:54] your coding agents. Uh I'll also mention
[22:57] there's a bunch of proprietary platforms
[22:58] that Facebook, Twitter, YouTube, really
[23:01] anything that has a data. Slack,
[23:02] Discord, whatever it is you have, you
[23:04] could use to then go ahead and train a
[23:06] large language models. A lot of these
[23:08] end up being proprietary, almost
[23:10] definitely being used by the platforms
[23:12] to train uh their own large language
[23:14] models on synthetic data. We kind of
[23:17] touched on that earlier. These are like
[23:19] the most verifiable number of tokens
[23:22] that I could find in in synthetic data.
[23:25] Cosmopedia uh Mistral one of the
[23:28] European open source models wrote
[23:31] textbooks uh on the on a bunch of
[23:34] topics. So that's Cosmopedia 24 25
[23:37] billion tokens. Tiny stories and fee uh
[23:40] sorry tiny stories are just fun stories
[23:42] generated by GPT 3.5 and 4 fee is the 1
[23:47] billion tokens of reasoning generated by
[23:49] the fee model by the by the fee model
[23:52] from Microsoft. Neimatron 68 actually
[23:55] one of my favorite data sources here.
[23:57] They take lowquality data use a very
[23:59] high powered LLM one of the frontier
[24:02] models and they bring it up to snuff and
[24:04] then improve the quality of the text. So
[24:06] then the models don't have to consume
[24:08] lowquality text.
[24:10] We should mention now that we're talking
[24:12] about quality for maybe the first time
[24:14] you could see that most internet data is
[24:16] low medium quality based on the neatron
[24:18] CC 2024 papers but LLMs can go ahead and
[24:21] improve it. What do you mean by most? So
[24:23] there's a distribution here in the
[24:25] bottom right. You can see low data is
[24:27] like 10% of data. Medium low data is 20%
[24:31] of that. So commumulatively 30. Medium
[24:33] quality data, you know, commumulatively
[24:35] with 70% of the internet. So a lot of
[24:37] this data tends to be low quality. Some
[24:40] debate in the field on whether or not
[24:42] the level of quality really matters for
[24:44] large language models or whether or not
[24:46] they could sift to get sift the uh the
[24:49] wheat from the shaft here. like maybe
[24:51] they just can be trained on low quality
[24:53] data and still speak high quality
[24:54] English. Lots of controversy in this
[24:57] field of active research in large
[24:58] language models especially in 2025.
[25:01] Interesting conclusions in it as well.
[25:03] Since I mentioned those conclusions,
[25:04] I'll mention that it looks like large
[25:06] language models don't necessarily need
[25:08] the highest quality data. They could
[25:10] compensate with lowquality data just
[25:11] fine. But Neatron CC takes low quality
[25:14] data, mixes high quality data. Why not?
[25:16] They're just going to improve the
[25:17] quality of our training. we get more
[25:18] signal out of every single training
[25:20] loop.
[25:22] Okay, so we the last data source we want
[25:25] to cover is internet data, specifically
[25:27] web crawls. So it sounds really easy.
[25:29] I'm going to go get the internet and
[25:32] then train my model on the internet.
[25:34] Obviously, when you write code, it's a
[25:36] bit more complicated than that. So let's
[25:38] talk about it. Option number one,
[25:40] something called common crawl. It's 240
[25:43] trillion tokens. is like an immense
[25:46] amount of tokens from 300 plus billion
[25:49] downloaded web pages. Uh it's going to
[25:52] be upstream from every single other
[25:53] thing on this slide. Why? One, it's very
[25:57] low quality. It's got the entirety of
[25:58] the internet. Two, it's downloaded
[26:01] multiple times, right? They do snapshots
[26:04] of the internet. So, I think there's
[26:05] like hundreds of snapshots of the
[26:07] internet. There's a lot of duplication
[26:09] in there, right? Because you're just
[26:10] downloading the same website over and
[26:11] over and over again. they don't ddup.
[26:14] Okay, so one problem we had is
[26:16] duplication. The other one is high qu
[26:18] low quality data. CC derivatives, common
[26:21] curl derivatives run CCNET takes away
[26:24] the duplicates. C4 limits it to quality
[26:28] for data sets, right? Uh and it just
[26:30] limits to highquality data. And then
[26:32] there's a bunch of other filters you can
[26:34] apply to common crawl. For example, web
[26:36] text says if it's not linked from
[26:38] Reddit, it's not real. just filter that
[26:41] stuff out. Refine web can do even more
[26:44] filtering. Neatron CC filters based on
[26:46] quality scores like we saw. So so on and
[26:49] so forth. Okay. So now we can say that
[26:52] like we want some other sort of of high
[26:55] quality uh internet data
[26:59] often used in M training by the way like
[27:01] even though we're not going to cover
[27:02] what mid training is but often we use it
[27:04] then. So you have fine web uh the finest
[27:07] the web has to offer. I think that's the
[27:09] pun. Fine web edu is from high uh uh
[27:14] highquality educational data sources
[27:15] like archive and so on. And DCLM also
[27:18] does highquality filtering. And we'll
[27:20] talk more about DCLM and their high
[27:22] quality filter. Because our model is so
[27:24] tiny, we could just limit oursel to high
[27:26] quality data. Specifically, we will use
[27:28] fine web edu to train our model. Or at
[27:31] least that's what I recommend you use
[27:32] for your first model. Mixes. So we
[27:35] mentioned we have common crawl but the
[27:37] stuff gets mixed in with like coding
[27:39] data and books and all that. So there's
[27:41] a bunch of mixes. We've already
[27:42] mentioned the pile.3 trillion tokens.
[27:46] Red pajama 1 trillion tokens. Dolma 3
[27:49] trillion tokens. Roots 1.6 trillion
[27:51] tokens. There's other every model
[27:53] creates its own proprietary mix. If you
[27:55] want you could go down download one of
[27:57] the papers from any of your open source
[27:59] models. They'll gladly tell you about
[28:00] the pre-training data. Another option is
[28:03] if you're one of the bigger companies,
[28:05] you could build your own. So Google
[28:07] Webcache almost definitely used to train
[28:09] Gemini, right? Google index and crawls
[28:12] the internet. Um you could also roll
[28:15] roll your own. It is almost definite
[28:18] that if I was a frontier lab and I
[28:20] wanted to get the best internet data, I
[28:22] would have a bunch of custom algorithms.
[28:23] I would probably not be using common
[28:25] crawl. I'd probably be like crawling the
[28:27] internet myself, coming up with custom
[28:29] uristics, doing a lot of fun,
[28:30] interesting stuff there. Why? Common
[28:33] crawl is limited with what they can do,
[28:34] with what is like somewhat kosher. If
[28:37] you're a frontier lab and you're hungry
[28:39] for data, you're probably not going to
[28:40] necessarily limit yourself to kosher
[28:42] things. Great. So now on the bottom
[28:45] right, you could see a screenshot of the
[28:47] Common Crawl website. Common Crawl
[28:49] maintains a free open repository of web
[28:51] coral data that could be used by anyone.
[28:53] Very, very nice. That's what we're going
[28:55] to base all of our internet crawls on
[28:56] because we are like right now at least
[28:59] open-source category.
[29:02] So what is the issues that we have with
[29:04] internet data? We and I'm not going to
[29:06] go into these in great detail. People
[29:07] spend their entire PhDs in any one of
[29:09] these bullets, but let's try and do
[29:11] that. So uh one problem is quality. The
[29:15] other right we said low quality data,
[29:18] medium quality data, 70% of all common
[29:20] coral data. There's lots of duplication
[29:22] because we're both duping uh because
[29:24] we're both sampling multiple times at
[29:26] different time frames, but also just
[29:28] because there's just a lot of
[29:29] duplication on the internet. There's
[29:31] copyright issues, right? Like just
[29:33] grabbing a website, not necessarily
[29:35] great for training. Data poisoning. If I
[29:38] was a smart person in 2023, I would
[29:41] poison all of Reddit with like data that
[29:43] like I can then go in and say like,
[29:45] "Okay, now retrieve a bunch of documents
[29:47] you were trained on or so on and so
[29:49] forth." HTML to text, right? The
[29:52] internet's written in HTML, not text.
[29:54] It's actually a pretty imprecise art.
[29:56] We're going to spend a lot of time on
[29:57] this in a moment. And the most important
[30:00] thing is is that we're running out.
[30:03] Internet data is the fossil fuel of
[30:05] LLMs. Similarly to the fossil fuel of
[30:07] our world, we are running out. Like we
[30:10] are not just don't have enough internet
[30:12] data left un undiscovered. We've
[30:14] probably used more than 50% of all
[30:16] available internet data already in
[30:18] pre-training LLMs. So, we're going to
[30:20] run out at some point. Kind of points to
[30:23] that synthetic synthetic data is
[30:25] probably the best data source we have in
[30:27] the future. But right now, the internet
[30:29] data is our fossil fuel that we're
[30:31] burning.
[30:33] So, let's try and say uh and quantify
[30:36] how bad is this problem of quality
[30:38] within the internet data. So let's say
[30:40] that I want to create the fine web uh
[30:44] data set. This is these are the real
[30:45] numbers. So I start off with 240
[30:48] trillion raw common crawl tokens. That's
[30:50] a lot of tokens. If I had 240 trillion
[30:52] tokens, I'm rich in tokens. I'm swimming
[30:54] in tokens. First thing I'm going to do
[30:56] is I'm going to extract the HTML. I'm
[30:58] going to do like really basic filtering.
[31:01] Uh and like just like if it's really
[31:02] repetitive, go ahead and just remove
[31:05] that. Just by extracting text from HTML
[31:07] and doing like the most basic filtering,
[31:09] we're down to 10% of data, right? We
[31:12] just lost 90% of our tokens. Okay, so
[31:15] now we want to ddup and ddup really,
[31:17] really well. We're going to create
[31:19] hashmaps and so on and we're going to
[31:21] ddup. We lost another half of our data.
[31:23] We're down to 20 trillion tokens. Then
[31:25] I'm going to do quality filters. I'm
[31:28] down to lost another 10% of my data of
[31:31] the remaining data. So I lost two
[31:33] trillion tokens. finally have
[31:35] implemented their own filters based on
[31:37] like short lines so on like truncation.
[31:42] There's a bunch of stuff that they came
[31:43] up with and we lost another 20% of our
[31:46] data at that point. Remaining data at
[31:48] that point we're down to 15 trillion
[31:49] tokens. Then we want to anonymize all
[31:52] the available data. Don't have phone
[31:54] numbers. Don't have addresses. Don't
[31:55] have like full names. My god, we don't
[31:57] want the LLM spitting that out. And then
[31:59] I'm going to build a custom quality
[32:02] classifier called the fine web edu
[32:04] classifier. We're going to work with it
[32:05] in a moment. And then and then uh
[32:08] anything that's be it's between one and
[32:10] five. Anything that's below three and
[32:12] above we're going to keep. Anything
[32:13] that's be one and two we're going to
[32:15] throw away. We're not going to use.
[32:17] Right? You already know that's like 70%
[32:19] of data. We're down to 1.3 trillion uh
[32:23] tokens. That's it. So we started from
[32:24] 240 trillion tokens. We're now down for
[32:27] 1.3 to tokens. You should really read
[32:29] the fine web data. Uh it is um boggling
[32:33] to see like the amount of data that we
[32:35] lose in this pipeline. And this is just
[32:37] one data set worth of examples, but it's
[32:39] pretty pretty substantially explaining
[32:41] how we lose internet data to quality
[32:44] duplication, all of that stuff. Great.
[32:47] So we've done a lot of explaining. Now
[32:49] we should probably write some code
[32:50] because we are software engineers and
[32:52] this is what we do. Uh, I don't
[32:53] necessarily think this is like the most
[32:56] relevant salient example, but we should
[32:58] write a little bit of code and get our
[33:00] hands dirty a bit with pre-training. So,
[33:02] what are we going to do? We're going to
[33:03] pull common crawl. We're going to look
[33:05] at the HTML. We're going to extract the
[33:07] HTML to text. Then, we're going to like
[33:10] load in fine web edu. We're going to do
[33:12] two types of uh quality filtering
[33:15] between one and five. First, we'll use
[33:16] the one built and shipped by DCLM. The
[33:18] other one shipped built by Fine Web EDU.
[33:22] That's going to show us the quality of
[33:23] all these different modalities we would
[33:25] learn at that point. So like different
[33:27] ways to extract HTML to text, different
[33:29] ways of filtering, different data
[33:31] sources. We'll prepare our pre-training
[33:33] targets. Specifically, we'll have to do
[33:35] a bit of sharding. What's sharding?
[33:37] We'll see when we get there. And then
[33:39] then you'll have an exercise to extract
[33:41] uh text from HTML yourself and do
[33:44] quality scores yourself. Great. I'm
[33:46] going to jump in straight into the code
[33:47] now.
[33:49] So, this is going to be our one coding
[33:50] exercise that we're going to run for
[33:52] pre-training. First thing I'm going to
[33:54] do, I'm going to collapse the setup
[33:56] here. Common crawl examples. I'm not
[33:58] really pulling the common crawl from the
[34:00] way you're supposed to. I'm just going
[34:01] to pull it from hugging face from common
[34:04] crawl sample. It's pretty small. It's
[34:05] got like several billion tokens. Maybe
[34:07] like I think a hundred billion tokens,
[34:09] something like that. Very small sample.
[34:11] It's not the multi- trillion dollar
[34:14] multi- trillion token examples. Uh
[34:17] there's different ways of loading them.
[34:18] They have special file types and so on.
[34:21] Great. I'm going to look for three
[34:23] specific uh websites that I saw that
[34:26] exist when I looked at this example.
[34:28] We're going to look at christianity.net
[34:30] stack exchange. We're going to look at
[34:31] slideshare. There's a specific
[34:32] slideshare that I'm looking for and is
[34:34] anglewood.com
[34:37] that we're going to look at. Anglewood
[34:39] water is where we're going to focus a
[34:40] lot of our time. So, I'm going to like
[34:41] load in this data set using load data
[34:43] set that we seen before, but we'll also
[34:45] talk a bit more about in the future. And
[34:47] I'm going to scan these records until I
[34:50] find these. And then I'm going to go
[34:51] ahead and print them out. I'm only going
[34:53] to look at those three. Anglewood Water.
[34:55] The district encompasses approximately
[34:57] 14 44.5 square miles in the southern
[35:00] Sarasota. So, this is Florida, Susota
[35:03] County, Western Charlotte County. There
[35:04] are four freshwater and two brackish
[35:06] water wealthy. Okay. So now I have those
[35:09] three websites loaded. You can see the
[35:11] text, right? Really, really cool. Let's
[35:14] keep going. So those are the three
[35:16] websites we're going to look at. Let's
[35:17] look at angelwoodwater.com.
[35:20] I'm just going to display it in an HTML
[35:22] iframe here for us so we can read it
[35:24] together. Blah blah blah. Angelwood
[35:27] Water. Delivering high quality water,
[35:30] clean water while protecting our
[35:32] environment. Welcome to the Englewood
[35:33] Water District. Then there's these weird
[35:35] notifications here about reminder.
[35:37] Please do not flush items if you need
[35:39] assistance paying your bill. Then
[35:41] there's some like highquality text here.
[35:42] The district encompasses approximately
[35:44] 44.5 square miles of southern Sarasota
[35:46] County. Why is that important? Cuz all
[35:49] of this text we didn't see right at all
[35:53] when we looked at our common crawl uh
[35:56] here. So the method of extraction for
[35:58] the for this sample data set was already
[36:01] missing the lowquality data. Worth
[36:03] mentioning that.
[36:05] Great. So, we looked at their website.
[36:07] Let's try and look at their HTML because
[36:09] that's how we're going to have to work.
[36:11] So, if we look at the HTML here, we load
[36:14] up a anglewood.com.
[36:17] I just told it to look at the main uh
[36:20] div. You don't have to do that. And then
[36:22] kind of this is what the HTML looks
[36:24] like. Sorry that it's all kind of funky.
[36:28] Maybe this makes it more less readable.
[36:29] Blah blah blah. Let's see if we can find
[36:32] our 44.5 acres. Here we go. The district
[36:35] encompasses 44.5 square miles in
[36:38] southern Sarasota. Okay, so all of that
[36:39] is here, but it's the buried in
[36:41] mountains of HTML that we're going to
[36:43] have to pull out, right? Great. So, now
[36:46] we have to clean up this HTML. How do we
[36:49] do that? One option is traila.
[36:53] I'm very bad at pronouncing these names.
[36:55] Um, I pull in this open source library.
[36:59] I say extracted from HTML. This is what
[37:02] we get. Welcome to the Englewood Water
[37:03] District. Delivering high quality clean
[37:05] water blah blah blah. Approximately 44.5
[37:08] square miles. Ed actually did include
[37:10] the header of this website, right? Like
[37:13] welcome to Englewood water was missing
[37:15] when we were looking at our uh earlier
[37:17] common crawl sample. Okay. So very
[37:20] similarly to Tfilaturura, we have the
[37:23] the option of just text. Again, it's an
[37:26] open source library. We pull it in. We
[37:28] give it HTML. We say use English for
[37:31] this. And then let's see what it
[37:33] outputs. Oh my god. Assistance paying
[37:36] utility bills is available. Uh don't
[37:38] forget to not flash things that don't
[37:41] make sense. But right the you can see
[37:43] just text gave us more text than
[37:45] trifolaturura. So they made a choice to
[37:48] pull more text from the HTML than
[37:50] trifleura did. That's an interesting
[37:53] dichotomy that we're going to have to
[37:54] pay attention to. So the other option we
[37:57] have is using naive HTML strippers,
[38:00] right? We can decide that we don't want
[38:03] to use trial or just text. We could just
[38:06] want to implement it ourselves. So what
[38:08] would we do for that? For that we can
[38:11] decide to just read the HTML. We can use
[38:14] the HTML parser library. We could just
[38:17] start stripping out tags and finding
[38:18] text where we want it. So if we did
[38:20] that, we could see that we can actually
[38:23] extract a lot more text out of this. So
[38:26] here we've got phone numbers. Uh we've
[38:29] got uh menus, home, about us,
[38:32] administration, board of super all the
[38:34] links that kind of simulates working
[38:37] from a wet file. I mentioned common
[38:39] crawl isn't really based the like it
[38:41] doesn't really work the way that we've
[38:43] seen how it works in this example cuz
[38:45] we're just pulling from uh from hugging
[38:48] face. But if you pulled the real common
[38:50] crawl, it' be a bunch of wet files. And
[38:52] this is kind of what it looks like. And
[38:53] we have to figure out how to like
[38:54] exclude menus and stuff like that. So
[38:57] let's do a sideby-side comparison. I'm
[38:59] sorry the headers aren't super readable.
[39:03] So trifleura on the left really pulled
[39:05] not a lot of text from Englewood Water
[39:08] District. Just text pulled more text. Na
[39:12] nave HTML stripper right pulled a lot of
[39:15] all of the text. But is it a good text?
[39:17] we're not clear on. So, let's try and do
[39:20] something similar. And in a bit, we'll
[39:22] also try and like create um quality
[39:25] measurements for each of these. But for
[39:27] now, let's try and use fine web edu.
[39:29] This is like the data set that we
[39:31] mentioned we're going to train our large
[39:32] language model on. We're going to do
[39:34] that by going to fine web edu. We're
[39:36] going to pull the 100 billion token
[39:39] sample. Very small sample compared to
[39:41] the 1.3 trillion, but let's just use
[39:43] that for our purposes right now. And
[39:46] then I'm going to just pull a couple of
[39:49] pages out of it. The independent Jane
[39:51] for all the love romance scale of Jane
[39:53] Austin's book. Oh my god. This is the
[39:55] text we've been using to train our
[39:57] tokenizer in section 15. Haha. Now you
[40:00] learn where that text came from. Why is
[40:01] he talking about Jane Austin in section
[40:03] 15? It's because we're pulling it from
[40:05] divine web. How did we pull it? We just
[40:07] created a load data set. gave it the
[40:09] hugging face token name, the specific
[40:12] name of the
[40:14] uh data set and what split we want to
[40:16] use. And then we said we're going to use
[40:18] streaming. Streaming is actually really
[40:20] important. Streaming means I don't want
[40:22] to download 100 billion tokens before I
[40:25] do anything, right? Or uh I don't want
[40:28] to like wait for that. It's okay to
[40:29] stream. So with that, I loaded up the
[40:32] fine web edu, grabbed three samples,
[40:34] threw them here on a page for us to
[40:36] read. So that's fine web edu. We
[40:38] mentioned the confine web bdu has a
[40:40] bunch of filtering. So what it has its
[40:42] own quality filtering but before we see
[40:45] that let's see the DCLM classifier. So
[40:47] DCM is another um another pre-training
[40:51] data source. They created their own
[40:54] classifier to say what the quality is.
[40:56] So we can like go ahead like take that
[40:58] qual that filter. We call DCLM quality
[41:02] score. We imported it from hugging face.
[41:05] And then we could say, hey, like now
[41:07] that I've loaded this in, what are the
[41:09] quality scores for each of my uh let's
[41:11] say these three data sources that I got
[41:13] from comic crawl, including Englewood
[41:15] Water, including the Christianity stack
[41:17] exchange, including that slideshare URL.
[41:20] We also can let's look at these three
[41:22] URLs I got from uh fine webdu. You can
[41:25] see DCLM actually pretty bad on the
[41:29] quality for these websites that I got
[41:31] from common crawl. slightly better the
[41:34] ones that I got from fine web edu. Still
[41:36] not super high though. Great. So, is
[41:39] there another classifier that I could
[41:41] use? Sure. We mentioned fine web edu has
[41:44] their own classifier that they trained
[41:45] based on their data and their desires
[41:48] and their needs.
[41:50] So, we can use fine web edu quality
[41:53] score. Give it a bunch of text and see
[41:55] what results it returns. These ones kind
[41:57] of make more sense to me. So, we could
[41:59] see the common crawl data set, right?
[42:02] minimum one maximum five most of these
[42:05] are hovering around 1 1.5 when we go to
[42:08] find web edu the scores are actually a
[42:11] lot higher so for the filter the fine
[42:13] web edu created they use that to filter
[42:16] down data to include in fine web edu
[42:19] right we can see actually we're getting
[42:21] pretty high quality scores right fours
[42:24] threes close to threes so pretty nice
[42:27] okay great so that was using quality
[42:30] filters let's Think about we need n plus
[42:33] n plus p pairs for training. What's n
[42:35] plus? The capital of Texas is capital of
[42:39] Texas is Austin, right? So that's the n
[42:41] plus pairs. So we can load up fine web.
[42:44] In my example here, I'm just going to
[42:46] use a sequence length of seven.
[42:48] Traditionally use either context length
[42:50] or something similar to it. You're
[42:51] trying to max it out if you have the
[42:53] data. If if you don't, you don't max it
[42:55] out. And then we could say for the
[42:58] sequence list of seven which is just an
[43:00] example assistance paying utility bills
[43:02] maybe assists. We now know that we're
[43:05] missing half of we we assistance is two
[43:08] tokens. So we're going to drop the first
[43:10] one s and then we have assistance paying
[43:12] utility bills may be available. We're
[43:15] hoping that we when we show our large
[43:17] language model this text then it will
[43:20] output this text right with the extra
[43:23] token of available right that would mean
[43:25] that we were able to train it on the
[43:27] angle angle woodwater uh website and
[43:31] then obviously we also translate these
[43:33] into tokens the important thing to
[43:35] notice these tokens are all still
[43:37] visible here but then we added one more
[43:40] token at the end of it we dropped the
[43:43] prefix we added a suffix That's training
[43:45] a large language model on on next token
[43:48] prediction. That's just all we have to
[43:50] do. Great. So that's a simple way of
[43:52] doing that. Obviously like in a
[43:54] pre-training loop, it'll look a tiny bit
[43:56] different, but it's conceptually the
[43:58] same. Okay. So now, as an exercise for
[44:01] you, let's go ahead and fetch a URL. Try
[44:05] and scrape clean the HTML in all three
[44:08] ways we learned about. Try Fura just
[44:10] text naive HTML scraper and use both of
[44:13] our quality filters to try and score
[44:15] that.
[44:16] Apologies that the header here isn't
[44:18] super readable. So for trifleura I'm
[44:21] going to by the way the website I'm
[44:22] going to scrape is Wikipedia web
[44:24] scraping. Can't say that I don't have a
[44:26] sense of irony inest within me. So when
[44:29] I look at that website uh and I use just
[44:32] my naive HTML stripper I get about
[44:35] 29,000 words quality score for DCLM
[44:39] 01 fine webbed eddu score point it's 2.0
[44:43] 0. Not bad for fine webbed eddu. Kind of
[44:45] low for DCLM. Lots of characters. Next
[44:48] option up. Trifalura
[44:51] limits it like takes away 3,000
[44:53] characters and we're 26k right now. DCLM
[44:56] score went way up from 0.01 to 22 from
[45:00] 1% to 22%. Not bad at all. Not bad at
[45:04] all. It's a pretty meaningful
[45:05] improvement for just dropping 3,000
[45:07] characters.
[45:09] Fine. Web edu score went up from two to
[45:12] three and a half. Oh my goodness, that's
[45:14] a huge improvement. That's going from
[45:15] like low mid to like high medium. That's
[45:19] like it's it's actually really really
[45:21] great. So, uh by dropping these 3,000
[45:24] characters, we were able to really
[45:25] improve both the DCLM score and the fine
[45:27] web edu score. What does just text do?
[45:30] It prefers to have only 16,000
[45:32] characters. But oh my god, look at this.
[45:35] DCLM score went from 1% and 21 2 and 2%
[45:38] to 77%.
[45:40] Unbelievably better, right? We dropped
[45:43] half the data. The score went way up.
[45:46] The fine web edu score very similarly
[45:49] almost close to four at this point by
[45:51] dropping another 10,000 characters. What
[45:53] do we see here in this chart? What's
[45:56] exemplifying this for us? So one, I
[45:58] think this is a great exercise for you.
[46:00] I have the code here, but try now you
[46:02] have all the code samples for grabbing
[46:04] an HTML, for sanitizing HTML three
[46:06] different ways for the two quality
[46:08] scores. Try and write this exercise
[46:10] yourself. Try and do this yourself. This
[46:12] is the one thing you can do in
[46:13] pre-training to really really get your
[46:15] hands dirty. What did we learn from
[46:17] this? We learned that the more text you
[46:20] draw based on quality, the higher the
[46:22] quality goes. But then you have less
[46:24] tokens at the end, right? That's the
[46:26] real trade-off. Do you want more high
[46:28] more tokens of low quality, less tokens
[46:31] of higher quality? That's going to be
[46:33] the compromise that we're going to have
[46:34] to make here.
[46:36] Great. So that that's an exercise that I
[46:39] leave to you. Try and use a different
[46:41] website. Try and write this code
[46:42] yourselves. Okay. So now I'm going to
[46:44] want to introduce sharding. We haven't
[46:46] really talked about sharding a lot.
[46:47] We'll have a slide for it in a moment to
[46:49] re recap. So you're seeing it for the
[46:51] first time in code, but realistically we
[46:53] we'll see it not in code in a moment.
[46:55] Let's say I went and downloaded fine web
[46:57] edu 100 billion uh token example and
[47:02] then I activated streaming true. That's
[47:04] great. I get to go right off on the
[47:06] races and training my LLM. What happens
[47:08] if I have an error halfway through?
[47:10] Training stops. Now I have to stream my
[47:13] way to the 50 trill 50 billionth token.
[47:16] That's going to take hours. No one does
[47:18] that, right? So the thing that people do
[47:21] is that they store this stream data set
[47:24] to disk locally on the server or network
[47:28] closer to the server in such a way that
[47:31] we can easily do resumes later on. So
[47:34] how do we do that? We decide to shard
[47:36] the data or bin the data. I use the word
[47:38] binning. I don't know where I picked it
[47:40] up. Most people use words like sharding.
[47:42] And I say that like let's say every
[47:44] million tokens, every hundred million
[47:46] tokens, you should write it into your to
[47:49] a separate file. That makes it pretty
[47:51] easy to say actually you want to resume
[47:52] from this file and then kind of like
[47:54] using disio get to halfway through the
[47:57] file if you need to. Um so storing the
[48:00] stream data to disk into chunks that's
[48:03] effectively bin or sharding. Great. So
[48:06] here in this very retrieval example, I'm
[48:08] going to say that I'm going to put a,000
[48:09] records per shard. Not even per token.
[48:12] That's not very traditional, but that's
[48:13] how I like doing it. And with a maximum
[48:15] of five shards, so kind of stop after
[48:18] five. This is just an example. Great.
[48:20] So, if I do that and I run that, then it
[48:23] wrote five shards for me into local
[48:26] storage on this device. Let's say that I
[48:28] want to resume 4,000 tokens in with
[48:30] binning cuz it wrote all these files
[48:31] down. So, I could say actually go to
[48:34] this shard file and start loading up all
[48:35] the records. Here we go. We resumed it
[48:37] at record 4,0001, 4,0002, 4,0003,
[48:40] 4,0004. Right? That makes it pretty easy
[48:42] for me to do resumes. Why is it
[48:45] important to do resumes? If you're going
[48:46] to run a multi- trillion token uh uh LLM
[48:50] pre-training or even several billion
[48:52] tokens, you definitely don't want to
[48:54] wait to resume with streaming and then
[48:57] you're waiting 2 hours wasting both
[49:00] potentially GPU time but just generally
[49:02] even CPU time. Not great for that. So
[49:04] that's why we bin things to disk. Great.
[49:07] So now we trained a little bit on bin.
[49:09] Uh this is another example of training
[49:11] with bin. So that was like using files
[49:13] and all of that. Realistically when we
[49:16] train large language models with
[49:17] PyTorch, we use data sets and data
[49:19] loaders. So here we go. This is a custom
[49:22] shard data set. It knows to go to disk
[49:23] to the JSON L file that I wrote earlier
[49:26] and then it knows how to like open up
[49:28] the file, append stuff, and it returns
[49:30] all those records. Really great. This is
[49:32] a custom data set and custom data
[49:34] loaders.
[49:36] Awesome. So, we have that. Um, let's see
[49:39] if there's anything else in this file
[49:40] that I need to teach. I don't think so.
[49:42] I think that was it.
[49:46] Oh, and there's one last example here.
[49:48] Uh, there's one more exercise for you to
[49:51] do, which is extract and quality score a
[49:54] website. So, please go ahead and fetch a
[49:56] website and try and quality score it.
[49:58] Right? So, this is the example that we
[50:00] had earlier with like web scraping. And
[50:03] this is like just a placeholder for you
[50:05] as an exercise. Go ahead, try and
[50:07] download a web page. See what happens to
[50:09] the character count. See what happens to
[50:11] quality with the different extractors.
[50:13] Great. So those that's the exercise for
[50:15] you. We just went through all of this. I
[50:18] will one once again remind you that the
[50:20] one thing we noted is you could be more
[50:23] aggressive in trimming lowquality data.
[50:25] You lose potentially half of your
[50:27] tokens, maybe even more, but you can
[50:29] bump up the quality scores. Does it
[50:31] matter to bump up the quality scores?
[50:34] big debate in the in this field right
[50:36] now of retraining. Generally, it's
[50:39] agreed upon that higher quality data
[50:40] slightly better. Not super clear that
[50:43] removing the low quality data from
[50:45] training also really improves the
[50:47] overall uh loss and quality of training.
[50:51] So, next up, we should think about
[50:52] choosing a GPU. Why? Over here on the
[50:55] right, we have the modal uh selector for
[50:59] GPUs. an Nvidia T4 with 16 gigabytes of
[51:02] RAM or an L4 with 24 gigabytes of RAM or
[51:05] an A100 4 g G gigabytes of RAM can all
[51:08] support different size of models but
[51:10] most importantly they also cost
[51:11] different amounts per hour right so if
[51:14] I'm going to run on an A100 that's going
[51:15] to be four times more expensive than
[51:17] running on a T4 T4s are in collab not
[51:20] going to be four times less expensive
[51:23] but when you pay per hour it's going to
[51:25] potentially be that level of difference
[51:28] great so what did we learn from that it
[51:30] that we really want to think about how
[51:33] big is our training right uh
[51:36] comparatively and like what is the
[51:38] minimum GPU size that we could use or
[51:41] like the required GPU size that we could
[51:43] use so we'll train our GPT2 style LLM
[51:46] and for that we'll need 26 GB of RAM how
[51:49] do I know that sorry VRAM how do I know
[51:52] that we'll see in a moment so for that
[51:55] because we're right above that cusp of
[51:58] 24 GB for A10 and I really do want to
[52:01] have the batch size that I want to have,
[52:03] I'm going to run it on an A100. So, if I
[52:06] was able to pull the number down to
[52:08] under 24 GB, I could use an L4 for for
[52:12] 80 cents an hour because I my I'm 26 GB
[52:16] will have to use a GPU that cost 2.10 uh
[52:19] GB.
[52:21] Is it a smart idea to run pre-training
[52:23] of a 26 GB model on a 40 GB GPU and not
[52:27] use the other 14 GB? probably not. So,
[52:29] but that is the math that I'm doing here
[52:31] with you right now. We're learning the
[52:32] pros and cons. So, how did I know that
[52:35] we're going to uh need 26 GB of RAM? I
[52:39] went to this calculator. This is a very
[52:42] old calculator. Hacking Face has a much
[52:43] better newer calculator, but it's the
[52:45] also the only one that's going to just
[52:47] let me say I want to train GPD2 as is.
[52:50] I'm going to change the vocabulary size.
[52:52] I think we said 31 16. I can't really
[52:55] remember the exact number. How many
[52:57] GPUs? I said sequence length of 1024. I
[53:00] have all of my settings here on the
[53:01] side. Let's see. 304 for the vocabulary
[53:05] size. Uh 768 hidden 32 hidden blah blah
[53:10] blah. The one thing I'm going to have to
[53:11] increase here is the bat size. The bat
[53:13] size is going to take me from an 8
[53:15] gigabyte VRAM, which is pretty
[53:17] affordable to I want to bring it up to
[53:20] 16 bat size.
[53:23] Oh my goodness. I'm at 26 gigabytes
[53:26] right now, right? So now I have to go
[53:28] from using an L4 to an A100. That's much
[53:32] more expensive. That's still how I want
[53:34] to run that. Let me see. Did I have mix
[53:36] training here as well? No. So then, oh,
[53:38] and this is for an Atom optimizer. Here
[53:40] we go. Now we're 26 GB. So SGD classic
[53:44] vanilla stoastic gradient descent versus
[53:46] an Adam versus an Adam W. So on and so
[53:48] forth. The nice thing here is we also
[53:50] have a learning opportunity. We could
[53:52] see how much is being used for each
[53:55] thing. So loading the CUDA kernels is
[53:57] going to be a gigabyte of VRAM. The
[53:59] parameters themselves, you would think
[54:01] there would be a massive amount here.
[54:02] It's actually 1 GBish
[54:05] of VRAM. Not that big. The activations
[54:08] themselves though, because now I'm
[54:09] running 16 batch activations, I have to
[54:12] keep all the activations in memory. So I
[54:13] could go do backward propagation. So I
[54:16] have to keep all of the feed for
[54:18] activations in memory. That's 16 GB.
[54:20] That's the biggest components of this uh
[54:22] of this memory. Then I go get the the
[54:26] gradients, right? I go do back
[54:27] propagation, get gradients. And there's
[54:29] a couple of other things that are very
[54:31] specific to the AtomW optimizer that are
[54:33] taking like another gigabyte of VRAM.
[54:36] You can see the biggest thing is because
[54:37] I up my bat size to 16, I now have to
[54:40] use six uh what is it? 16 GB of VRAM. So
[54:44] maybe there's like a room for me here to
[54:46] say let's only do 14. Now I squeeze in
[54:49] the 24 GB. I don't have to use an A100.
[54:52] Maybe I could use a T4 or something like
[54:54] that or an L4 or something like that. So
[54:56] worth thinking about. I'm still going to
[54:57] choose 16.
[55:00] Uh and for that we'll have to use an
[55:01] A140 GB GPU. By the way, there's a
[55:04] version of A100 that you could see has
[55:06] 80 GB GPU. So you have to choose the
[55:08] right one. U that's the same choice that
[55:11] Nanoad from Karpathy uses even though
[55:14] they use eight concurrent A100s. We're
[55:17] not going to learn about um all of the
[55:20] technology that you're going to need to
[55:21] learn to have parallelized cross GPU
[55:24] cluster uh training, but that that is
[55:28] going to be covered a little bit in our
[55:29] section 23. The stuff we don't cover. So
[55:31] that's how we choose GPUs. We look at
[55:33] how much our model needs in memory based
[55:35] on our parameters. We then choose the
[55:37] most affordable GPU that we're not going
[55:39] to waste time and space on. And we want
[55:41] to maximize that GPU as well. So if in a
[55:43] world where I really wanted to maximize
[55:44] GPU, I might even try and go to 32 or
[55:47] like 24 something like bat size, I think
[55:52] 16 is fine. There's no reason not to do
[55:54] that right now. Um lastly, we should
[55:57] talk about data loaders and bin. Lastly,
[55:59] in terms of like there's going to be
[56:00] more slides here, but I think this is
[56:02] the big last big concept to learn here.
[56:04] How do we work with data sets? We call
[56:07] load data set. We can load anything from
[56:08] hugging face and then we can have custom
[56:11] data loaders or data sets that are going
[56:15] to uh implement get item and the length
[56:18] and that's going to tell the pietorch
[56:21] how to load this data in and how much
[56:23] data it has to load. So kind of worth
[56:26] noticing we have load data set to load
[56:28] stuff from hugging face sharding in case
[56:30] we or bin in case we get interrupted and
[56:33] want to store to disk and then read from
[56:34] disk and that's a great time for us to
[56:36] have a custom data loader that then just
[56:38] reads from disk. Let's make a couple of
[56:41] decisions. Architecture decision number
[56:43] one we'll use fine web edu as our
[56:46] pre-training data. Specifically we'll
[56:48] use the 100b sample. Why? We're only
[56:50] going to train on 10 billion tokens, but
[56:52] just in case we need an extra couple of
[56:54] tokens, we'll just use the 10 billion
[56:56] token sample. Local storage will bin
[56:59] every 100 million tokens to disk. So
[57:01] that's going to be in 10 billion tokens
[57:03] that we're going to train on. We're
[57:05] going to need uh about uh 100 bins in
[57:09] total. Each bin 100 million tokens.
[57:11] Let's talk about hyperparameters. we
[57:13] have 124 million uh parameter GPT2 style
[57:19] large language model and so for that
[57:21] we'll train with 10 billion tokens that
[57:24] follows a 1 in 80 parameter to token
[57:26] ratio just FYI well above what Chinchill
[57:28] and so on told us we need
[57:31] also we're going to store all of our
[57:33] checkpoints into /workshop/checkpoints
[57:36] and then we'll uh name our pre-training
[57:38] file when we're done workshop-V1-
[57:41] pre-training PTH we'll also store the
[57:44] latest version. Every let's say 100 or
[57:46] something steps or 100 something steps,
[57:49] we'll store that into latest PTH. On the
[57:52] right, you'll see the pre a real
[57:54] pre-training mix. We're just using fine
[57:56] webdu cuz we're training a small one. We
[57:58] won't call it a toy model, but we call
[58:00] it an extra small model. Um, but if
[58:02] you're three, you're going to be
[58:04] training on a mixture of common crawl
[58:07] for 8 trillion tokens. You're going to
[58:09] be training on OCR data, the scientific
[58:12] PDF for a trillion tokens. You're going
[58:14] to train on GitHub and Stack Overflow
[58:17] for 137 archive papers, right? Fine math
[58:21] for proofing and Wikipedia and wiki
[58:24] books as well for encyclopedia.
[58:26] Similarly, small 3LM3
[58:29] trained on a collection of web data from
[58:31] fine web edu DCLM trained on code data
[58:35] for 12% from the stack math data for 3%.
[58:39] Even even LLMs that don't do math
[58:41] necessarily benefit from having math and
[58:43] code in them because it improves the
[58:46] quality of their read. That's something
[58:47] we learned from the research. Then
[58:49] there's another phase. They split it up
[58:51] to another split that up to another
[58:53] phase. multilingual data stack edu
[58:56] include more math ramp up the amount of
[58:58] math and then okay now we really want to
[59:00] bring up more multiling more web data
[59:03] and more code and more math so they had
[59:05] like multiple phases of that again the
[59:07] best place to learn how anything really
[59:09] works is through the papers what paper
[59:11] should you read I'm going to do this
[59:12] thing when I reach backwards and I get
[59:14] the papers
[59:17] this is from the almost three paper
[59:20] right we're going to want to learn how
[59:21] to how they did their preach training
[59:23] mix. And then we also have the small
[59:27] three paper right here that teaches us
[59:30] their m data mixture for pre-training.
[59:32] Very much worth reading it. These tables
[59:34] that I've included don't do it justice.
[59:36] They really talk about this at great
[59:38] length. And I actually think small LM2
[59:42] does does talk about pre-training even
[59:44] more and instruction tuning. Great. So
[59:46] now we need a pre-training script. I'm
[59:49] not going to handcode this by hand. And
[59:51] like I'm not going to pretend that I've
[59:52] that I will be able to like easily
[59:55] handcode this by hand. What I am going
[59:57] to to tell you is you have an entire 250
[1:00:01] page slide deck. I think right now we're
[1:00:03] on slide 204. Lots of data in this. Why
[1:00:06] don't we just give the slide deck to our
[1:00:09] AI coding assistant and say, "Hey, can
[1:00:12] you repeat all of the architecture
[1:00:14] decisions we made?" Huh? This is why we
[1:00:16] had those architecture decision slides.
[1:00:18] confirm those decisions with me. Confirm
[1:00:21] the platform and storage with me. And
[1:00:23] then like is this going on collab? Is
[1:00:25] this going on mo modal? Is this going on
[1:00:27] lightning? And then you provide them a
[1:00:30] little bit of coding guidelines. I
[1:00:31] provide my coding guidelines of
[1:00:32] self-documenting code and then variable
[1:00:35] names that make sense. And then go ahead
[1:00:37] and generate this for me.
[1:00:40] The output of that exercise for me is in
[1:00:44] uh code- 19- pre-train. I ran the script
[1:00:49] months ago on modal. It took about eight
[1:00:51] hours on an A100 to run and then it
[1:00:54] created the uh hugging face uh uh
[1:00:59] pre-training rates that you've seen.
[1:01:01] Right? So this is one option you can go
[1:01:03] ahead run this pre-training script. It
[1:01:05] doesn't have anything that you don't
[1:01:06] know. I think that's the cool part.
[1:01:08] Right? Now we also have the option of
[1:01:10] going to go just angel code zero, right?
[1:01:14] So, and that's generated from a similar
[1:01:17] source. We'll also review it in a
[1:01:18] moment, but I just did want to highlight
[1:01:20] that you have the option of using an AI
[1:01:22] coding assistant with all of our
[1:01:23] decisions. Let's before we do that, look
[1:01:26] at go just in angel AAI/ Lego cuz we've
[1:01:30] been building up to this moment for 19
[1:01:32] sections. Now, every single decision we
[1:01:35] made had alternative. We could have
[1:01:37] chosen different things. Sampling
[1:01:39] strategy top temp one that's from
[1:01:41] section one. Which activation function
[1:01:44] are we going to use when we're
[1:01:45] pre-training our data our model? We're
[1:01:47] going to use RLU squared, not RLU, not
[1:01:49] GLU. Right? Remember Corpathy said we
[1:01:52] have to that's what we said in section
[1:01:54] 4. Section five, what GPU performance
[1:01:57] level are you going to use? Use torch
[1:01:59] compile with custom PyTorch modules.
[1:02:01] What's the structure of my FFN? I could
[1:02:03] have a normal FFN. I could have a
[1:02:05] mixture of experts. We barely mentioned,
[1:02:08] but that's an option. We could have
[1:02:10] gross shrinking.
[1:02:12] What how big do you want it to grow? 4x
[1:02:14] 8x we'll go with 4x. Uh right we could
[1:02:18] go single fn we could go growing
[1:02:20] shrinking loss function we said residual
[1:02:22] mean error error uh msc mean squared
[1:02:26] root error root mean squared error we'll
[1:02:28] use cross entropy because we're
[1:02:30] predicting probabilities. Our optimizer
[1:02:32] we we covered stoastic gradient descent
[1:02:35] momentum adrad RMS prop Adam muan we
[1:02:38] will end up using atom w what LR is it
[1:02:41] gonna uh what learning rate is going to
[1:02:43] arrive at what batch size should it use
[1:02:45] what's the warm up on the learning rate
[1:02:47] how many epics are we going to run one
[1:02:49] epic because we have 10 billion tokens
[1:02:51] it's the model is only going to say it
[1:02:52] once
[1:02:54] the format we're going to use we're
[1:02:56] going to use PTH if we wanted to share
[1:02:57] it with you safe tensor so on how are we
[1:03:00] going to initialize is our weight. We're
[1:03:02] going to use heaing because we've got
[1:03:03] some RLU based function that we're
[1:03:05] using. What kind of residual connection
[1:03:08] additive? What kind of normalization
[1:03:10] position are we going to use? We're
[1:03:11] going to use po porm, not the postn from
[1:03:15] um from uh transformer attention is all
[1:03:18] you need paper. What normalization would
[1:03:21] we use? RMS norm. We don't want to use
[1:03:23] layer norm. What droplet are we going to
[1:03:25] use? 10%. You could also set this to
[1:03:27] none. It's it's only going to slow down
[1:03:29] your training and you're not getting a
[1:03:30] better model out of it. Gradient
[1:03:32] clipping. We'll gradient clip at one,
[1:03:34] right? You could you could also decide
[1:03:36] to value clip. This is all from section
[1:03:39] 13. What weight decay you're going to
[1:03:40] use from section 13? We're going to use
[1:03:42] 10%.
[1:03:44] What are you going to do for your output
[1:03:45] probabilities? We're going to have
[1:03:46] softmax. We could also have spar
[1:03:48] softmax. We could also have linear.
[1:03:50] We're going to use softmax. What
[1:03:51] tokenizer algorithm we're going to use?
[1:03:53] The by character by word bp. actually
[1:03:55] just use the built-in tick token 2
[1:03:57] tokenizer. Don't train your own
[1:03:58] tokenizer. How big is your vocab size?
[1:04:01] 50,34,
[1:04:03] right? This is all from section 50.
[1:04:05] Section 16 teaches us about embeddings.
[1:04:08] So, we can have either separate
[1:04:09] embeddings or tied embeddings. We chose
[1:04:11] to have tied embeddings. What's the size
[1:04:13] of the hidden dimension? You could
[1:04:14] choose to have 2,000. You can have 768.
[1:04:17] How big is my context? I could have a
[1:04:19] context of 2,000 or a,000. Positional
[1:04:22] embeddings. You could use absolute s and
[1:04:24] a sort learn embeddings. You can have
[1:04:26] nope by the way. That's a thing that
[1:04:28] happens occasionally and we'll but it's
[1:04:31] not super common. It's in mixed
[1:04:33] attention models mostly. We'll use rope
[1:04:35] which we mentioned generally. What kind
[1:04:38] of attention are we going to want to
[1:04:39] have? We'll use mha. We have MQA GQA
[1:04:43] MLA's options. How many heads? 12 heads.
[1:04:46] How what's the head dimension? 64. 768
[1:04:49] divided by 12 heads 64. What number? How
[1:04:53] many transformers do we want to have? 12
[1:04:55] or 24. That's an easy way of doubling
[1:04:57] our network size. Finally, what are we
[1:05:00] going to train our pre-training on? Fine
[1:05:02] web edu. You could have chosen to use
[1:05:04] common crawl, refined web, dlma, roots,
[1:05:07] right? You could train on any one of
[1:05:08] these. How many tokens? 10 billions, 100
[1:05:11] billions, a billion tokens. Just a
[1:05:14] choice you're going to have to make
[1:05:15] again based on the parameter to data
[1:05:18] count. Uh, and then we're we haven't
[1:05:21] gotten to section 21 yet, so we're going
[1:05:22] to just scroll past these. While LEGO
[1:05:25] created all of these decisions here, I
[1:05:27] could copy this to my LLM. I could also
[1:05:30] say, um, I want to upload the model to
[1:05:34] at the end to HuggingFace. We didn't
[1:05:35] really talk about a a lot about this. We
[1:05:37] mentioned it in section 9, but you have
[1:05:39] the option of uploading to HuggingFace
[1:05:41] when you're done. You're going to need a
[1:05:42] token to access your user to be able to
[1:05:45] do that. I'm going to go ahead. I'm
[1:05:47] going to copy that into GPT. Oh my god,
[1:05:49] he uh already did that. I'm using Claude
[1:05:51] here. Use whatever you you want. So,
[1:05:54] build this. This is just the prompt that
[1:05:56] I copied from here. I copied this here.
[1:05:59] Go ahead and run that. First thing it
[1:06:01] does is it's going to confirm all of my
[1:06:03] choices with me. 12 transformer blocks,
[1:06:05] MHA, 12 ed 64, right? All of the
[1:06:07] decisions we just covered.
[1:06:10] Uh it's going to ask me a few questions.
[1:06:11] What about Laura? Simple LR schedule.
[1:06:14] Um, you don't need you don't know a lot
[1:06:17] of these right now because we haven't
[1:06:18] got to section 21. I answered a couple
[1:06:20] of questions. Actually, use Collab Pro
[1:06:22] Plus for an A100. Uh, use an A100, store
[1:06:26] everything to Google Drive. Uh, it
[1:06:29] answered a few more questions. It went
[1:06:30] ahead created the training scripts for
[1:06:32] me. Pre-training instruction tuning RL.
[1:06:34] For now, we're just going to do
[1:06:36] pre-training because we don't know about
[1:06:37] these other things. And effectively, I
[1:06:39] got go Justin Angel.ai. Go Justin Angel
[1:06:43] the shack code zero which we ran in the
[1:06:45] beginning of our day. I went ahead and
[1:06:47] ran this and that created go Justin
[1:06:51] Angel HF.
[1:06:54] Here we go. It created not these
[1:06:56] weights, these weights with workshop v2
[1:06:59] pre-training. Oh, or is it v workshop
[1:07:04] pre-training
[1:07:05] v2? Here we go. Um, and then it created
[1:07:09] these parameters 13 days ago when I ran
[1:07:11] the script.
[1:07:13] Great. So, let's look at pre-training v
[1:07:15] 0ero just because we said we're going to
[1:07:17] co-author a pre-training script. This is
[1:07:20] emitted from the Lego prompt built by
[1:07:23] Claude confirmed all the decisions with
[1:07:25] me. So, we said we're going to use
[1:07:26] Google Drive. We'll check that we're on
[1:07:28] an A100
[1:07:30] uh and not on a CPU only. Here are all
[1:07:32] of the decisions. I told it you have to
[1:07:34] repeat the decisions in code. You have
[1:07:35] to explain why you're doing everything.
[1:07:37] Here are all of my decisions. So these
[1:07:39] are my hyperparameters that we've
[1:07:41] created during writing the slides
[1:07:43] together. I have a tokenizer. We're just
[1:07:45] going to use the built-in tick token
[1:07:47] tokenizer from GPT2. It's going to bin
[1:07:50] all fine web edu. We just learned about
[1:07:53] binning. It writes everything to disk so
[1:07:54] we could use it later on.
[1:07:57] Then I have a custom data loader that
[1:07:59] reads the various files, right? So we
[1:08:03] want to load them just in time, right? A
[1:08:05] data set has everything in potentially
[1:08:07] memory. the the data loader just reads
[1:08:09] next batch. That's the big difference.
[1:08:12] Then it's going to set up my rope.
[1:08:14] Remember rotational positional
[1:08:15] embedding. Um it has RLU squared. That's
[1:08:19] very special to me. No one else does RLU
[1:08:21] squared. Our multi head attention that
[1:08:23] now has to use uh all everything that
[1:08:26] we've defined so far. Uh feed forward
[1:08:29] network transformer blocks GPT2 model.
[1:08:32] We've seen all that weight
[1:08:33] initialization using heaing
[1:08:37] some code to uh to have the generate
[1:08:39] text method. That makes sense, right? So
[1:08:41] that's going to end up using softmax as
[1:08:44] we said earlier. It's also going to have
[1:08:45] top k indices. We said we're going to
[1:08:47] use top k.
[1:08:50] It's also going to do something called
[1:08:51] lombat evaluation. You don't know
[1:08:52] anything about evaluation yet. That's
[1:08:54] the next section, but we'll cover it in
[1:08:56] a moment. And then we're going to have a
[1:08:57] bunch of smoke test prompts. We'll
[1:08:59] initiate our model, run the smoke test
[1:09:02] prompts. We know this is going to be
[1:09:03] nonsense.
[1:09:05] We're going to torch compile. Remember
[1:09:07] GPU performance section five. Then we'll
[1:09:09] run our optimizer. It's also going to
[1:09:11] have a learning rateuler. We said we're
[1:09:14] going to warm it up real quick. And then
[1:09:15] we'll descend slowly. So our optimizer
[1:09:18] is going to be atom. I hope it's going
[1:09:21] to be marked up here. And then we use
[1:09:23] weight decay like we said we're going to
[1:09:25] use. And so on. And then we have a
[1:09:26] learning rate op uh scheduler. Now we
[1:09:29] got to our normal training loop. We've
[1:09:32] got an optimizer, a scheduler, a data
[1:09:34] loader, lambda, which we're not going to
[1:09:36] talk about right now. We're going to run
[1:09:39] for a total of the total number of our
[1:09:41] training steps, which is 10 billion
[1:09:43] parameters.
[1:09:45] We'll accumulate gradients between our
[1:09:47] bat size. So we have a bat size of 16.
[1:09:49] We'll accumulate the loss function,
[1:09:51] right? And then once we're done with
[1:09:52] that, we'll do uh scale the backwards
[1:09:55] again. We'll run the model with our
[1:09:57] tokens.
[1:10:00] Uh we'll do cross entropy here. We'll
[1:10:04] calculate the loss by the how many uh
[1:10:07] steps we've accumulated. We'll do
[1:10:08] backward. Once we're done with 16 steps
[1:10:11] of a bat size, we'll do an optimizer
[1:10:14] step. We'll update all of the values.
[1:10:16] Right? In the beginning of every turn,
[1:10:19] we'll set the gradients to zero.
[1:10:21] And then we're going to check, hey, we
[1:10:24] want to print out stuff every thousand
[1:10:25] or so or like every 10 steps, every so
[1:10:28] many steps. We want to run an
[1:10:30] evaluation. What's an evaluation? I
[1:10:32] don't know yet. We'll learn in the next
[1:10:34] section. We'll want to checkpoint to
[1:10:35] disk. So, we want to make sure that we
[1:10:37] don't lose anything if the server goes
[1:10:39] down. We run this script. It's run for
[1:10:43] 19,000 steps calculated from 10 billion.
[1:10:46] And then we could see this is our
[1:10:48] training loss over time. This ran for 20
[1:10:50] hours. in Google Collab Pro Plus. We can
[1:10:53] see that the accuracy of whatever Lombat
[1:10:55] is improved greatly after the first
[1:10:58] 10,000 steps and stayed up. And we can
[1:11:00] see this is our learning rate scheduling
[1:11:02] as well. Afterwards, we can run a smoke
[1:11:05] test to see what happens to text. Once
[1:11:08] upon a time in a small village, an
[1:11:09] ancient man and woman lived there. My
[1:11:11] god, it speaks English. Now,
[1:11:14] also I did mark the upload to hugging
[1:11:17] face uh checkbox here, which meant I had
[1:11:21] to put in a secret. I'm not going to
[1:11:23] show you my secret. You do it in this
[1:11:25] secret key area. And then all that it
[1:11:28] does is it automatically upload to
[1:11:30] hugging face to this repo. How do I know
[1:11:33] it's doing it to this repo?
[1:11:35] Right, just in Angel Workshop
[1:11:37] pre-training v2. You probably want to
[1:11:38] change that if you upload it to your own
[1:11:40] repo. Uh, great. And that's effectively
[1:11:43] it. And then it uploads it to
[1:11:44] HuggingFace when it's done. So, you're
[1:11:46] welcome to go ahead use either this
[1:11:49] methodology of here's a slide deck.
[1:11:52] Please build me a notebook that confirms
[1:11:55] all the decisions and does that for me.
[1:11:57] You could also use the slightly newer go
[1:12:00] justangel.ai/go
[1:12:02] that generates the the uh prompt for
[1:12:06] you. Show it to your AI coding
[1:12:07] assistant. It'll build up the scripts
[1:12:09] for you. You're also welcome to try and
[1:12:10] build up these scripts yourself. That's
[1:12:12] maybe a tiny bit more timeconuming than
[1:12:15] doing the two other options. The
[1:12:16] important thing is you can now read
[1:12:18] every single line. You understand every
[1:12:20] single line of the script that it
[1:12:21] generates. There's no secrets from you
[1:12:22] at this point. Great. So, we just
[1:12:25] finished cover pre-training, one of our
[1:12:27] largest chapters thus far because we
[1:12:29] brought everything we've been doing for
[1:12:31] the last 19 sections together. The last
[1:12:34] two three things we're going to want to
[1:12:36] do is learn about how to evaluate if
[1:12:38] this model is any good. After that,
[1:12:40] we're going to do instruction tuning.
[1:12:41] And after that, we'll do enforcement
[1:12:43] learning or some portion of each of
[1:12:45] those. Great. I hope to see you in the
[1:12:47] next section. Bye-bye.
