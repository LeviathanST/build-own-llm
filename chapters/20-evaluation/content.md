# Evaluation | Build Your Own LLM Workshop #20

**Build Your Own LLM Workshop — Video #20 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 34m 56s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=S6uLzsqOOUc |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to a build
[00:02] your own large language model workshop
[00:04] with me, Justin Angel. We we're here and
[00:08] we've just gone over how to do
[00:10] pre-training for a model. We've covered
[00:12] how to train a large language model.
[00:14] We've covered the architecture and now
[00:17] we've covered pre-training. And right
[00:19] now, we're going to be focusing on
[00:21] evaluation. What's the problem we're
[00:23] going to try and fix here together? The
[00:25] problem is we don't know if our large
[00:28] language model is any good. How do you
[00:30] know if it's good at anything? So let's
[00:33] start with a really naive set of
[00:34] answers. Maybe the model that everyone
[00:37] uses is the best model, right? Not
[00:40] necessarily our model, but maybe that's
[00:41] just an indication that it's the best
[00:43] model. So if you go to open router
[00:45] leaderboard,
[00:47] you can open it up and see which models
[00:49] people actually end up using. And you
[00:51] can see that on top of that pile right
[00:53] now is Deepseek V4 uh Flash and H and
[00:58] the Tencent High3 preview. High3 preview
[01:01] is I think free, which maybe explains
[01:03] why it's up here. Um Claude Opus pretty
[01:07] popular. Okay, great. So the leaderboard
[01:09] says DeepSc V4 is winning high three,
[01:12] right? And that's as of today in May
[01:14] 17th.
[01:16] So that's one option. But you might be
[01:19] saying actually Justin like you
[01:21] mentioned High3 is kind of free. Uh
[01:23] Deepsec V4 Flash I'm assuming is pretty
[01:25] affordable. Like there's something here
[01:28] about the fact that the cost is driving
[01:32] a lot of the usage and maybe that's not
[01:34] a great indication to what the quality
[01:37] is. So maybe the right way to do this
[01:40] math and using these leaderboards is
[01:42] going capabilities divided by price and
[01:45] that'll help us normalize for that. So,
[01:47] how do we know what's the price of any
[01:49] of these? We can go into artificial
[01:50] analysis. They have a list here per
[01:53] model. What's the price per 100 per uh
[01:57] million tokens and you can see actually
[01:59] DeepSk V4 flash. Let's try and find it
[02:03] together. Deep Seek V4
[02:08] for Flash. Uh actually pretty
[02:12] affordable. 6 cents for 100 million
[02:15] tokens on max, right? A lot more
[02:19] expensive than the new cloud us48 with
[02:22] $4 for a million tokens.
[02:25] Great. But now I have a pretty good
[02:29] understanding on price. How do I know
[02:31] whether the capabilities of these models
[02:33] if I'm trying to evaluate it now that
[02:35] I'm trying to like really like do
[02:37] something a bit more structured than who
[02:39] which model is being used the most but
[02:41] rather try and look at price and
[02:42] capabilities. So price is pretty clear.
[02:45] We have good charts for that but what is
[02:47] what is up with capabilities. So one
[02:49] option is we could look at LM Marina.
[02:52] Funny enough the top result of LM Marina
[02:55] I'm going to scroll down a bit is Opus
[02:58] 40. it thinking extended that's number
[03:02] one on all these charts even today May
[03:05] 28th
[03:07] uh if even after OPUS 48 is out even
[03:10] OPUS 47 is out 4.6 six still winning at
[03:14] this chart. So let's look back at this
[03:16] at our slide and kind of like try and
[03:18] look at this chart a bit more. So
[03:20] there's like the name of the model and
[03:23] overall and expert and hard prompts and
[03:26] coding and math and creative writing
[03:28] instruction following longer query and
[03:30] then you know a question I would have
[03:32] for you is what's behind being number
[03:34] one on hard prompts that feels super
[03:37] subjective to me right
[03:41] one thing that's worth mentioning let's
[03:44] even if you're not suspicious uh is to
[03:46] not be super suspicious right that's why
[03:49] I added the If in the bottom right,
[03:51] don't be suspicious, right? All these
[03:54] leaderboards, they're an illusion. None
[03:57] of this stuff is real. I love the paper
[03:59] leaderboard illusions. These are heavily
[04:01] game. They don't really measure reality.
[04:03] They measure very, very, very, very
[04:06] small differences. Here in this chart,
[04:07] it looks like it's 20 spots behind. It's
[04:10] actually like one and a half% behind.
[04:14] This is just because you have to stack
[04:15] rank things. So generally leaderboard is
[04:18] not great to learning about
[04:19] capabilities.
[04:21] What is another way of learning about
[04:23] capabilities? We could look at model
[04:25] cards. So every time a new model comes
[04:27] out, we say, "Hey, here's how well I'm
[04:30] doing on a bunch of ben benchmarks."
[04:33] For example, the unreleased Claude
[04:36] Mythus preview. You know, back in April
[04:39] 2026,
[04:40] uh, Anthropic announced that they're not
[04:44] releasing Mythus because it'll bring
[04:46] about Armageddon from an engineering
[04:48] security perspective. So, and they
[04:50] showed us this model card. So, let's
[04:53] look at it together. I could see a bunch
[04:55] of benchmark and I could see that like
[04:58] this model is doing really, really well
[05:00] at this. Um, one thing that's really
[05:03] clear is that Claude Mthus preview is
[05:07] winning in everything
[05:09] that's so weird how the the model whose
[05:13] card we're looking at always wins. It's
[05:15] almost like it's somehow gamified. It's
[05:18] almost like metrics that it doesn't win
[05:20] on get dropped. It's almost like the
[05:23] method by which we run evals matters. So
[05:25] that's one weird thing that we get to
[05:27] learn about eval. Another thing here is
[05:30] a lot of these numbers are hovering at
[05:33] about like 80 90%. We refer to these as
[05:36] saturated, right? If all models kind of
[05:39] perform at 90 plus%, we generally call
[05:41] them an evaluation or benchmark
[05:44] saturated cuz you can't really get a lot
[05:46] better than like a saturated baseline.
[05:51] So let's look at the specific benchmarks
[05:53] that we had here. So I'm just picking
[05:55] the previous slide and making it a bit
[05:57] more readable in terms of the a valard.
[05:59] And let's look at what actual benchmark
[06:02] uh claude mythos preview had that could
[06:06] potentially dispel Armageddon on all of
[06:08] us. So one option is bench right bench
[06:13] takes a bunch of GitHub issues
[06:16] uses the issue text uses the generate PR
[06:20] and then uses that to it's really hard
[06:23] to explain. let's say train a judge
[06:24] model to then uh improve coding for uh
[06:30] to to check if if coding is good enough
[06:33] from these models. Okay, so that's
[06:35] bench. So they're considered high
[06:37] difficulty uh so on there's non-Python
[06:40] in there. There's a bunch of visual
[06:42] assets. It's it's not a trivial test to
[06:45] succeed in but that's a coding specific
[06:47] task. Another one is terminal bench and
[06:50] OS world. They test for agentic tool
[06:53] usage i.e. can it call the right tools
[06:55] at the right time.
[06:57] Another benchmark on meth preview is
[07:00] GPQAD
[07:02] PhD level science multiplechoice
[07:05] questions. Um I have one such sample
[07:08] question here. The study of quantum
[07:10] mechanic deals with a lot of matrices.
[07:12] Consider these following matrices.
[07:14] Right? which uh uh da da da are they
[07:18] represented the same operators in
[07:21] quantum systems yes no right I don't
[07:23] even understand the question I don't
[07:24] have a PhD in quantum mechanics right so
[07:28] that's one set of questions that it's
[07:29] doing mythus preview is doing okay on
[07:33] another one is mmlu
[07:35] so mmlu and we'll look at it in a moment
[07:38] is
[07:39] general knowledge questions mmlu when
[07:43] you have three m is just multilingual.
[07:46] So this is multilingual general
[07:47] knowledge. Okay, we have USMO math
[07:51] Olympiad questions requiring formal
[07:53] proof. So okay, now we did coding a
[07:55] moment ago. Now we're doing math. Why
[07:57] are those the easy domain to write
[07:58] events for? They're verifiable. Code has
[08:01] verifiable results. You can just run the
[08:02] code. Math has verifiable results. You
[08:04] can run the proof. What do you do with
[08:06] proofs? I'm not super clear on, but it's
[08:08] very deterministic. Another test that
[08:11] they gave uh Claude, this is a new one
[08:13] that's not heavily adopted. It's
[08:16] graphics. Fun algorithm riddles is the
[08:19] way to think about it.
[08:21] Humanity's last exam. Great naming on
[08:25] this one. It's frontier level knowledge.
[08:27] So, you know how you have PhD level
[08:28] knowledge, then it's frontier level
[08:30] knowledge where it's like five people in
[08:32] a room, I guess, can answer it. In
[08:34] frontier level knowledge, it's doing re
[08:36] like pretty well. What's an example of a
[08:39] frontier level question? Below is a
[08:41] representation of a Roman inscription
[08:44] originally found in a tombstone.
[08:45] Provided translation for the polyaran
[08:48] script. A translation is provide of the
[08:50] text is provided. Transliteration,
[08:53] right? That is something that I'm
[08:54] assuming not a lot of people can do
[08:56] successfully correctly.
[08:59] And finally there's charive it charive
[09:03] which is takes a bunch of archive
[09:05] articles takes the visuals out of them
[09:07] and test for visual understanding in
[09:09] large language models. So this is more
[09:11] of a computer vision model uh test.
[09:13] Great. So these are pretty hard
[09:14] benchmarks. These are like the cutting
[09:16] edge in April 2026 I guess. U but
[09:21] there's a lot more complexity than we're
[09:22] hiding from you here. And I want to
[09:24] really talk about the complexity and how
[09:26] eval are like bad. and then I'll show
[09:28] you a bunch of eval because I want to
[09:30] show you like the problems before I show
[09:32] you the the proposed solutions. So we
[09:35] saw problem number one and two earlier
[09:38] and if you're writing a model card you
[09:40] probably won in it. A lot of problem a
[09:41] lot of evaluated.
[09:44] So problems three and five have to do
[09:45] with multiple choice questions. Uh
[09:48] sometimes the answer key is wrong. So
[09:49] let's say you have multiple choice
[09:50] questions and sometimes the answer key
[09:52] is wrong. What does that mean for how we
[09:54] train models? Do they need to learn to
[09:56] ignore wrong keys even though right? How
[09:58] do you do that? Sometimes the answers
[10:00] are part of the training. That's super
[10:03] common considering all these data sets
[10:04] are on the internet and the internet is
[10:06] what we feed the models.
[10:09] Um format choice for answers matters.
[10:11] You could a model could say three. It
[10:14] could say the third one and it could say
[10:16] blue. All of them might be answering the
[10:18] question of uh what color is the sky and
[10:20] the third option is blue. Right? All
[10:22] three. So the format matters a lot.
[10:24] Another problem is problem number six
[10:27] and we're not going to cover this too
[10:28] much in eval but if you want to evaluate
[10:32] the verifiable domains like math proofs
[10:35] or code or if you want to evaluate free
[10:37] text for like creative tasks you're
[10:40] going to have to train a judge or a
[10:43] deterministic machine learning model
[10:45] verifier. So those are LLMs judge or a
[10:48] ver an automatic verifier. Those are
[10:50] going to be the two options. Those have
[10:52] their own error bars, right? How good is
[10:54] an LLM at judging an another LLM's
[10:57] creative writing? The answer is not
[10:59] great. That's going to be a short
[11:01] version. Why? For example, uh we now
[11:04] know that large language models from the
[11:07] same family of models, so cloud to
[11:09] claude, open AAI to OpenAI, JPT to JPT,
[11:12] Llama to Llama, they tend to rate each
[11:15] other higher if they're in the same
[11:16] family. LLM is judges really fraught
[11:19] with issues. Verifiers need to be
[11:21] verified with a 100% accuracy to not
[11:24] have their own error rates. That almost
[11:26] never happens. So, there's a bunch of
[11:28] problems with that as well. Uh, another
[11:30] problem, most benchmarks have very short
[11:32] interactions, which is not how people
[11:34] use LLMs. Oh my god, here's a question.
[11:37] Multi-bullet choice question. Great.
[11:39] That was a great interaction. Thanks. No
[11:41] one uses LLMs like that unless they're
[11:42] trying to cheat on one homework
[11:44] question. I guess that so that's just
[11:46] not realistic which is also why models
[11:50] are like very clearly know when they're
[11:52] being evaluated because they know that
[11:53] no one interacts with models that way
[11:56] like they instinctively understand how
[11:58] chat works. Okay, so we have all these
[12:00] problems. There's many many many other
[12:03] problems with how eval work right
[12:05] there's a whole paper from Alaska 2024
[12:08] that is just a survey of a lot of other
[12:10] issues that I think is worth covering
[12:12] right around disability reliability uh
[12:15] how do you choose models how do you
[12:17] choose benchmarks how do you design your
[12:19] prompts how do you put in parameters and
[12:22] answers how do you parse the outputs and
[12:25] just generally what is the approach that
[12:26] you want to have when you announce hey
[12:29] I've done really Well, in a test, you
[12:31] show everyone the the the stack traces,
[12:33] the reasoning traces. No, you're not
[12:35] going to do that. They can copy your
[12:36] model. Oh my god, this is there's a lot
[12:38] of problems with this. Great. So,
[12:40] there's a lot of problems with running
[12:41] EVs. That's going to be the point of
[12:43] this slide. Why did I show you this
[12:45] slide? I want to make it clear. Evals is
[12:48] not a solved problem. Pre-training kind
[12:50] of a solved problem. We give it a bunch
[12:53] of data. We have a good architecture. We
[12:55] modify the architecture in one or two
[12:57] meaningful ways every year. kind of a
[12:59] solved problem. Not really. There's
[13:01] still lots of gains to make there. But I
[13:04] I do think that like EVAs is much more
[13:06] of a notsolved problem. Why? Anything
[13:09] that you can evaluate,
[13:11] you can then train a model to do better
[13:13] on. So writing better evals is actually
[13:15] the hardest part I think right now of
[13:17] LLMs. That's my opinion. People in the
[13:20] field can argue with me and make me
[13:22] wrong, but I still hold that opinion
[13:24] right now that I think EVAS is the most
[13:25] exciting frontier of building LLMs. Uh I
[13:29] also think the other areas are still
[13:31] very very interesting and still have a
[13:33] lot of room to grow. So let's summarize
[13:35] ways to evaluate LLM. Gemini was nice
[13:37] enough to generate this based on my
[13:39] prompt. Uh leaderboards, that was an
[13:42] option. We saw the problems of
[13:43] leaderboards, right? there's just like
[13:45] an illusion because it's like two points
[13:47] beyond but then it's 20 spots behind
[13:50] each other. You could do multiple choice
[13:52] questions which have a bunch of problems
[13:54] we covered. You could do LLM is judge
[13:56] but we said that's pretty inconsistent.
[13:57] Why would you trust the judge any more
[13:59] than you trust the model that's being
[14:01] verified? And there's automatic machine
[14:03] learning verifiers. Those almost never
[14:05] have 100% accuracy. And then there's a
[14:06] bunch of other problems. Great. So now
[14:09] that I've told you eval are really
[14:10] really hard to build. Let's talk about
[14:12] what are the types of EVAs that we have.
[14:15] This is me summarizing the paper from uh
[14:20] a benchmark of 243 uh a survey of 243
[14:23] benchmark from 2025. This is kind of my
[14:26] favorite eval paper right now. Uh not in
[14:29] terms of insights but just in terms of
[14:30] having a little bit of taxonomy. So the
[14:33] baseline of uh of benchmarks is
[14:37] linguistic right we before we had large
[14:41] language models we had the entire field
[14:42] of NLP natural language processing that
[14:45] whole field was built on can you
[14:47] understand language can you have common
[14:50] sense reasoning can you generate text
[14:52] can you have dialogue how is your
[14:53] multilingual support so on we can take
[14:56] all of those NLP tests from preet 2019
[14:59] and then just reapply them towards large
[15:01] language models which is what we've
[15:03] done.
[15:04] If you look and kind of squint, you'll
[15:07] see the word lambada bold bolded in
[15:10] blue. That's going to be the test that
[15:12] we're going to use to train our large
[15:13] language model. And we'll talk more
[15:15] about that in a bit. Um, also we can
[15:18] evaluate knowledge in large language
[15:20] models. We can see if it knows like just
[15:23] general stuff. Can it be an expert? Can
[15:25] we give it exams? Can we do stuff that's
[15:27] language based? We could check its
[15:29] reasoning on logic on common sense stuff
[15:31] on mathematics so on. We could then go
[15:34] back into like the more natural like
[15:37] into more domain specific benchmarks
[15:38] like the stems right math and physics
[15:42] and chemistry and biology. We could test
[15:44] it on knowledge there or maybe reasoning
[15:46] there. We could test it on humanities
[15:48] like law and IP and education
[15:50] psychology. We could test it on
[15:52] engineering and technology. Most
[15:54] importantly, we can also kind of
[15:56] independently from all these other
[15:58] fields, we can indep we could check its
[16:00] safety and its reliability, right? So
[16:03] like there's a bunch of work on AI
[16:05] safety right now. So worth highlighting
[16:07] there's a lot of eval
[16:09] tens of thousands of benchmarks, maybe
[16:12] even more. We're only going to run one
[16:14] for a large language model because we
[16:17] just want to see it improve in
[16:18] something. Great. So let's look at MMLU.
[16:22] And really, I should just like be really
[16:24] honest. This is my favorite benchmark.
[16:26] Why? Because I can kind of read it and
[16:28] maybe I'll get 50% if I try and do that.
[16:31] This is high school level questions and
[16:34] expert general knowledge. What's an
[16:36] example of that? There's the question
[16:38] here. Which of the following statements
[16:40] could be best described as a liberal
[16:43] perspective on future energy security?
[16:45] And there's four statements here. And
[16:46] you just have to choose one. When I read
[16:48] that, I chose the right one. I don't
[16:50] know how I did that. something in my
[16:52] brain knew that.
[16:54] But as you can see on the right side, a
[16:56] lot of these are high school level
[16:58] questions. So let's open up MMLU. This
[17:00] is what a data set looks like. I
[17:01] intentionally wanted to open up the data
[17:03] set in front of you. And then you can
[17:05] see there's a bunch of subjects. So
[17:06] let's look at all these subjects. We
[17:08] have anatomy and astronomy and college
[17:11] biology and high school computer
[17:13] science. Maybe I know a little bit about
[17:16] high school computer science. Let X
[17:18] equals 1. What is X?
[17:21] bitwise to the left in Python. I
[17:24] actually don't know bitwise operators. I
[17:26] I would fail at this, right? But I can
[17:29] kind of struggle with these questions,
[17:31] which is why it's one of my favorite
[17:33] tests to kind of look at and really
[17:35] understand what are we evaluating our
[17:37] large language models based on? Which
[17:39] foods tend to be cons to be consumed in
[17:41] lower quantities in Wales, in Scotland?
[17:44] Meat, confectionary, fruit, vegetables,
[17:46] or potatoes?
[17:48] My goodness. Right. you need to have
[17:50] some amount of knowledge to be able to
[17:52] answer these questions.
[17:55] So we now understand like what MMLU is
[17:57] that to me this is a quintessential best
[18:00] example of an eval because we as people
[18:03] who read it can then kind of empathize
[18:05] with the struggles of a model as it's
[18:06] trying to answer it. So now we want to
[18:09] talk about emerging capabilities. I I
[18:12] was kind of on the f on the fence if we
[18:15] should cover it but I think it's
[18:17] worthwhile. Why are we covering emerging
[18:20] capabilities? Cuz we have a very tiny
[18:22] model. Our model is 124 million
[18:25] parameters compared to the 1 and a half
[18:27] billion parameter
[18:30] small LLMs nowadays, right? That's like
[18:33] an order of magnitude smaller,
[18:36] let alone three orders of magnitude
[18:39] smaller than the trillion parameter
[18:41] models that are now being trained and
[18:43] run in production frontier labs. So
[18:45] we've previously seen that we have
[18:47] scaling laws like data on data and size
[18:51] and compute and size. So data how many
[18:54] tokens am I feeding my model compute how
[18:56] many flops am I going to spend on my in
[18:58] my GPUs and size how many parameters do
[19:00] I have
[19:02] some of the model capabilities to to do
[19:04] these evals only emerge they are
[19:07] emergent after a certain scale has been
[19:10] reached for example the ability to do
[19:13] MMLU will not be reached by a small 124
[19:17] million parameter model it just it
[19:19] doesn't have the capacity to learn and
[19:21] retain this kind of specialized
[19:23] knowledge. So, and that way 2022
[19:26] actually demonstrated that there's a
[19:28] minimum scale required for broad
[19:30] knowledge, multi-step math, complex
[19:32] translation, advanced linguistic
[19:34] patterns and a few other things. And
[19:36] this whole field of emerging
[19:37] capabilities is I think fascinating.
[19:39] Cool. But why is it why am I showing you
[19:41] this right now? We know that our 124
[19:46] million model is not going to be able to
[19:48] perform well in MLU. So we can't use my
[19:51] favorite eval benchmark. So instead,
[19:53] let's use Lambada. What's Lambata?
[19:56] Lambata just says, "Hey, if I give you a
[19:58] really long text, can you generate the
[20:01] next token correctly based on this
[20:03] really long text?" Uh, and we'll see
[20:05] Lambata in a moment. So I want to look
[20:08] at the left side and you can in the left
[20:10] side what you can see is charts that you
[20:13] could see the performance and evaluation
[20:15] goes from zero, right? like zero is and
[20:18] zero like absolute or zero is in zero
[20:20] randomness right because if you have
[20:22] four options in MCQ you would expect 25%
[20:25] baseline performance
[20:27] and you can see that at a certain scale
[20:30] in like this these charts are in flops
[20:32] like how much compute how much GPU time
[20:34] did they get you could see that at some
[20:37] point it goes from nothing to something
[20:39] that's an emergent capability a smaller
[20:41] model didn't have it and a slightly
[20:43] larger model now all of a sudden has it
[20:45] so that's our definition of an emerging
[20:47] capability. I think it might be worth
[20:49] seeing Lambata right now. So, I had it
[20:52] pulled up here in in a data set. What
[20:54] I'm going to click this is a very long
[20:56] text and the test is can it generate
[21:00] this? Oh my goodness, we're scrolling.
[21:02] We're scrolling. We're scrolling. Can it
[21:03] generate this very last statement here?
[21:07] Oh my goodness, this is so long. Can it
[21:10] generate the very last token? Great. So,
[21:13] that's Lambada. What lamb checks is long
[21:16] text. Can you read it com understand it
[21:19] and then generate the next token in a
[21:21] way that is deterministic and correct
[21:23] based on the long text.
[21:26] So let's do a quick code demo here.
[21:28] Let's start by loading GPT2 and our
[21:30] workship v1 models. We're done training
[21:33] workshop v1 pre-training, right?
[21:35] Remember we had a script in last time we
[21:37] ran it earlier in the day today code
[21:40] zero, right? We ended up running that
[21:42] model for 8 hours, 20 hours, however
[21:44] long we ran it. So, we're going to load
[21:46] that up. We're going to run a lambda
[21:48] manual evaluation and then we're going
[21:50] to use a pre-built LLM evaluation
[21:52] harness. Great.
[21:55] So, now we've got uh this is uh the
[22:00] collab notebook for for code 20. We've
[22:04] got two models that I'm going to load up
[22:06] here. I've got workshop v1 just in angel
[22:08] workshop v1 pre-training. I've got gpt2
[22:10] smaller gpt2.
[22:13] I've got a method that's called load
[22:14] model and tokenizer which is just going
[22:16] to load the model in the relevant
[22:18] tokenizer. We'll try and have it
[22:19] generate hello world. Today I want to
[22:22] and then see what it wants just to make
[22:24] sure that these models run.
[22:26] Our custom pre-trained model from the
[22:28] previous section says hello world. Today
[22:30] I want to share my experience with the
[22:32] students. I've been working on projects
[22:33] for a while. And then uh GPT2 small
[22:36] says, "Hello world. Today I want to talk
[22:38] about the new game, The Legend of Zelda:
[22:40] Breath of the Wild." Fascinating. Every
[22:42] model wants to do something a bit
[22:44] different. Uh after this, now that we
[22:47] have our models loaded, we want to have
[22:49] manual lamb evaluation. So we're going
[22:51] to load STEMIC Lambata. Again, that's
[22:54] just the data set we saw a moment ago. A
[22:56] moment ago.
[22:58] And we saw this data set here. There's
[23:01] the training data set, the test data
[23:02] set. We're going to use the test data
[23:04] set
[23:07] and great. So split on test. We'll load
[23:11] up the example text. We have 5,000
[23:14] examples. In my palm is clear stone
[23:16] inside small ivory statue. It's a
[23:18] guardian angel blah blah blah blah blah.
[23:20] We just want to check that the last
[23:22] token is the correct uh is the correct
[23:25] token. We'll run we'll run Lambata. So
[23:28] this is just me trying to code up a
[23:30] Lambata test in a way that makes sense
[23:31] to me. We'll only run a 100 examples
[23:34] because I don't want to waste a bunch of
[23:35] GPU time evaluating models. Uh, but you
[23:38] can definitely run it on all 5,000 if
[23:40] that brings you joy.
[23:42] And then let's see what accuracy we got
[23:44] out of our 100 examples. Workshop V1 was
[23:47] able to guess 14 correctly out of 100
[23:50] and GPT2 small was able to guess 19. So
[23:52] maybe GPT2 Small is still slightly
[23:54] better than my Workshop V1. Maybe not. I
[23:57] I should really run the full 5,000 test.
[24:00] Do you run every test once? Do you give
[24:02] it multiple attempts? Right? These are
[24:04] questions of building a test harness, an
[24:06] evaluation harness of how we evaluate
[24:09] things. This doesn't necessarily mean
[24:10] that GPT2 small is much better. It just
[24:13] means that in the 100 examples we ran
[24:14] and the way we evaluated it, it ended up
[24:16] being better.
[24:18] So why do we want to ever write this
[24:20] kind of code oursel? Because we're
[24:22] making a lot of assumptions here about
[24:24] how to show test the models, how to read
[24:27] the answers, right? There's a lot of
[24:29] assumptions baked into this. We can use
[24:32] uh Eluther's AI MMLU the LM evaluation
[24:37] harness. So for that I exclamation mark
[24:40] LM eval. I tell it which model I wanted
[24:42] to run in this case GBT2. What test do I
[24:46] want it to run? MMLU.
[24:48] How many uh temps am I going to give it?
[24:51] How many uh questions am I going to show
[24:54] it? And then please run it on the GPU.
[24:57] So, I'm only going to run MLU for 50
[24:59] tests because I don't have any reason to
[25:01] run the full 10,000 plus questions
[25:06] and it's going to run. It's checking one
[25:09] at a time. Generate, generate, generate.
[25:11] Then, it's running a bunch of tasks.
[25:13] Let's look at the final summary at the
[25:16] end. So, MLU is split between uh a bunch
[25:20] of fields like we saw MMLU humanities,
[25:23] formal logic, other business ethics. And
[25:26] we can see how we did on each one of
[25:27] these. The nice thing is it's also
[25:29] generating standard errors. So now we
[25:32] have error bars on these questions
[25:33] because it maybe runs it multiple times.
[25:36] So because it runs it multiple times, it
[25:38] can generate error bars for us. So this
[25:40] one has 6% error bar. This has 5% error
[25:43] bar. So on and so forth.
[25:46] Great. And then that gives us the
[25:48] summary
[25:50] of how we did across all of the various
[25:52] groups. So this looks a lot better to me
[25:54] than me writing my own Eval harness in
[25:57] general. Okay. So now is an exercise for
[25:59] you. Choose a benchmark and run it.
[26:02] Which benchmarks can the LM evalu
[26:06] harness run? You can open up this link
[26:09] and choose any one of these links. Let's
[26:11] try and scroll down a bit. See if
[26:12] there's something interesting that we
[26:14] can run here.
[26:16] Oh, GSM8K. I wonder what that is. I'm
[26:20] going to go in hogging face and go. Hey,
[26:22] can you GSM8K find whatever open in
[26:26] here?
[26:28] Oh, wow. This is actually a pretty hard
[26:30] data set. Remember we looked at it
[26:31] earlier. Let me open up the data set
[26:34] here.
[26:36] Great. So, this is my main data set. And
[26:39] then Natalia sold clips to 48 of her
[26:42] friends in April. And then she sold as
[26:44] many clips in May. How many clips did
[26:46] Natalia sell altogether in April and
[26:48] May? Right. And we wanted to see it
[26:50] doing math. 48 divided by two. So 24
[26:54] clips in May, right? Okay, this is the
[26:57] answer. Great. So now we know uh about a
[27:01] new data set. So we could try and run
[27:03] it. I actually think my example was for
[27:05] something a bit different. I had it run
[27:07] the Lambada test. So Lamba, let's go
[27:10] back to Lambata.
[27:15] You can see there were several
[27:16] variations. Lab evaluates the
[27:18] capabilities of computational models for
[27:19] text understanding and next word
[27:21] prediction. That's great because that's
[27:23] what training a large language model is
[27:24] supposed to do. So we run that on GPT2
[27:28] and we can see that it does pretty okay.
[27:30] It has 58% oh sorry this is for Copa. Uh
[27:33] it does pretty okay. It gets 38% on
[27:37] OpenAI version and 65% on Lambada
[27:40] standard. Okay, not bad with 30% error
[27:43] rates which is not ideal. So, as an
[27:45] exercise for you, maybe go ahead and try
[27:48] and generate uh and run these tests.
[27:50] You're going to need a GPU, a that's big
[27:52] enough to load the model, and the
[27:54] valves. Great. So, go ahead, try running
[27:57] some eval yourself.
[27:59] We should also talk about perplexity.
[28:01] Uh, one really important thing to
[28:04] mention is that there's a common eval
[28:06] that you're just going to hear over and
[28:07] over again. We talked about cross
[28:08] entropy so many times.
[28:12] cross entropy and perplexity is just two
[28:14] different ways of talking about the same
[28:16] thing. When you take the cross entropy
[28:17] loss and you uh and you square it, the
[28:22] thing uh sorry not square two to the
[28:23] power of cross entropy, what you'll end
[28:25] up getting from that is perplexity. What
[28:28] what is it? What is perplexity though? I
[28:31] really love the definition of perplexity
[28:34] values or bits of surprise, right? And
[28:36] they're human readable. So when I say
[28:38] something has a loss of three, that's
[28:40] not human readable. What it translates
[28:42] to is actually 2 ^ 3 is 8, that means
[28:47] that the model shows between eight equal
[28:49] choices when it shows its last and final
[28:51] token. That's not great, right? A cross
[28:54] entropy of 10 is actually a proplexity
[28:56] of 48,000. That's the entirety of my
[28:59] vocabulary in a 50,000 item model. That
[29:02] basically means cross entropy of 10
[29:04] means it's totally random. I have no
[29:06] control over anything. So worth
[29:08] mentioning that uh that cross entropy is
[29:12] not super human readable. Perplexity a
[29:15] lot more human readable. It refers to
[29:17] the bits of surprise. The average chose
[29:19] between so many tokens. Uh let's see
[29:23] that in Excel.
[29:25] So cross entropy from our training of
[29:28] 124 million run. So you could see loss
[29:31] here. You could on a chart based on how
[29:33] many steps we've ran. So we could see
[29:36] step the step numbers you could see the
[29:38] CE bits.
[29:40] Um let's do without answers. Great. We
[29:45] have the CE bits the number of steps.
[29:47] Then the CE bits we had at every single
[29:51] uh one of these steps. And then let's
[29:54] say we want to do perplexity. So, it's
[29:56] two to the power or you could also like
[29:59] have power to it, but I'm just going to
[30:01] write it like this. Number of bits.
[30:04] Great. Pull it all the way out here.
[30:07] Some of these are going to be kind of
[30:08] hard to read because they're going to be
[30:09] massive. But now we can translate it. At
[30:12] step 10,000
[30:14] here, right? 12. Our LLM uniformly chose
[30:19] between 12 tokens. At step 20,000
[30:23] here, RLLM chose between 20 uniformly
[30:26] chose between 28 tokens. At step 500,
[30:29] RLM uniformly chose between a,000
[30:32] tokens. So, just worth noticing how
[30:34] perplexity works. I think it's just very
[30:38] very useful to know what this number
[30:40] means cuz you're going to see it pretty
[30:41] often as an eval. It's a single
[30:43] parameter like a single number eval
[30:46] that's very common to see. Great. So,
[30:48] let's make a couple of decisions. One,
[30:51] we said our benchmark is going to be
[30:53] lambada. Why? Our 24 million model
[30:55] parameter model is just not going to be
[30:57] succeed on general knowledge test. It's
[30:59] not big or complicated enough. It
[31:01] doesn't have the mergent capabilities
[31:03] required from a large language model to
[31:05] succeed. Also, we'll probably do
[31:08] balanced copa for common sense
[31:10] reasoning. I'm going to show you
[31:11] balanced copa in a minute minute.
[31:14] Smoke testing. Let's do a smoke testing
[31:16] with a few prompts like you've already
[31:17] seen me do. And in loss we'll calculate
[31:20] cross entropy but also we can think
[31:22] about it in perplexity if it makes sense
[31:23] for us. One hyperparameter that we
[31:26] should set for our pre-training script
[31:28] is how often do we want to run the seal?
[31:30] We want to run it every 500 steps. Why?
[31:32] We have to stop everything and run
[31:34] thousands of prompts through the model.
[31:36] So we probably want to like not do it
[31:38] too often. It could be the slowest part
[31:39] of our pre-training script. If we look
[31:42] at it here,
[31:44] as loss was descending at around 2500
[31:47] um training steps, what we could see is
[31:50] the lambata accuracy went from zero
[31:53] random to all the way to 30% and it was
[31:56] just improving over time continuously.
[31:58] The more training we gave it, the better
[32:00] it got at Lambata. So super worth
[32:02] noticing that. So that's in our training
[32:04] pre-training script. We'll run eval
[32:07] every 500 steps and then we can run it
[32:08] at the end or we can run it as a
[32:10] separate script whatever we want. On the
[32:12] right we have almost three base model
[32:14] evaluations. This is what it really
[32:16] looks like when you're trying to
[32:18] evaluate a base model. Pre-trainings
[32:20] create base models. So that's the
[32:22] terminology.
[32:24] So they ran GSM 8K which we saw GSM
[32:26] symbolic math 500 human eval big
[32:30] codebench eval medq right like a bunch
[32:35] of these things they run all of it. Why
[32:37] do I love this table? Because it shows
[32:39] you the complexity. What is being
[32:41] evaluated? Is it multiple choice? Is it
[32:44] code execution? Is it financial? How do
[32:47] you know that you are correct? Is it
[32:48] passed the first attempt? Is it passed K
[32:51] attempts? uh what temperature did you
[32:53] run the model that super super matters
[32:56] when you're running evals and you want
[32:57] to be consistent what is what was the
[32:58] top P what was the pass number that you
[33:01] would check whether or not they were
[33:03] successful how many out of how many so
[33:06] all of these really matter and they
[33:07] change the results of eval again I'm
[33:09] going to recommend everyone stops and
[33:11] reads one or two of the most frontier
[33:15] open source model papers I just think
[33:16] it's good information and now I'm going
[33:18] to do this thing where I reach in and I
[33:21] make the papers physical. So this is the
[33:24] Almo 3 paper just worth noticing.
[33:28] Great.
[33:29] After we're done with Eval, which is
[33:31] roughly now I'm just going to I owe you
[33:34] uh the copa balanced eval. After that,
[33:37] we're just going to show instruction
[33:39] tuning. So let's just show you the copa
[33:42] balanced. Copa balanced.
[33:45] Here we go. What is copa balanced? I
[33:48] actually love this as a test cuz it
[33:50] shows you common sense reasoning. So
[33:52] let's say that I have the statement or
[33:55] premise of my body cast a shadow over
[33:58] the grass because option A the grass was
[34:02] cut or B the sun was rising. Clearly
[34:05] it's because the sun was rising, right?
[34:07] That is why my body cast a shadow over
[34:10] the grass. So if you could take choice
[34:12] one, choice two in the premise, kind of
[34:14] build them into a multiple choice
[34:15] question, you could show it to a model.
[34:17] There's multiple ways of doing that. You
[34:18] could show it to a model and you could
[34:20] see did it learn common sense. That's
[34:22] really useful. And we're going to try
[34:24] and train on common sense pretty soon.
[34:27] Great. Our whole goal with instruct the
[34:30] at this point is to was to evaluate our
[34:34] model to how good it how well it
[34:36] performed. And now in instruction
[34:38] tuning, we wanted to get it to follow
[34:40] our instructions. We so far with
[34:42] pre-training, we've built a fancy
[34:44] autocomplete. What we didn't build is a
[34:47] thing that can act like an AI chatbot,
[34:48] which is what we're going to build in
[34:50] the next section. I hope you'll join us
[34:52] soon. Thank you so much. Bye-bye.
