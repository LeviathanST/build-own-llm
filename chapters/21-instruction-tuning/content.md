# Instruction Tuning | Build Your Own LLM Workshop #21

**Build Your Own LLM Workshop — Video #21 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 40m 26s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=8iwxM6XRpVQ |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to building
[00:03] our own large language model workshop.
[00:05] I'm Justin Angel. We had just wrapped up
[00:08] evaluation and pre-training. So we're
[00:10] kind of done with pre-training and now
[00:12] we're moving on to post-raining
[00:14] specifically instruct tuning and then
[00:16] our goal is to take a autocomplete
[00:20] engine that is a large language model
[00:21] and convert it to something that
[00:23] resembles an AI chatbot. Let's have a
[00:25] look at like why we have to do that. So
[00:28] let's start off with our problem. The
[00:29] pre-train models won't follow any
[00:32] instructions from users, right? Help me
[00:34] write me a poem, fix my homework.
[00:37] They're not going to do any of that
[00:38] stuff. They are fancy autocomplete on
[00:42] steroid that happen to speak English. I
[00:45] say English, by the way, whenever I want
[00:47] to say language.
[00:49] Great. So, what's an example of that?
[00:51] Let's look at our left on right side of
[00:53] our screen. Our right side of the screen
[00:55] says, explain what a neural network is
[00:57] in simple terms. And the response is,
[00:59] what is the difference between a neural
[01:01] network and a neural network? What is
[01:02] the difference between a neural network
[01:03] and a neural network? I'm just going to
[01:05] exit the slide. I'm going to improvise.
[01:07] I'm going to show you something pretty
[01:09] funny. It just keeps saying that
[01:11] forever. It's like I kind of cropped it
[01:13] out, but it just keeps saying that
[01:15] forever. It's absolutely jibber jabber
[01:18] nonsense. Um,
[01:21] here we go. So, uh, we also have the
[01:24] instruction of what is the capital of
[01:26] France? And the response is the capital
[01:28] of France is France. That's not great.
[01:30] It's not super accurate even though it
[01:32] probably knows the answer is Paris. Oh,
[01:33] how do we know it knows the answer? The
[01:35] next sentence is the capital of France
[01:36] is Paris. It doesn't even understand the
[01:38] notion of answering a question. So what
[01:41] does it look like once we've instruction
[01:44] fine-tuned the model? Uh the first thing
[01:46] that like we could see is it says
[01:48] explain what a neural network is in
[01:51] simple terms. And then it says a neural
[01:52] network is a type of computer that is
[01:54] compromised with many layers of nodes
[01:56] each with its own unique identifiers and
[01:57] architectures. These nodes are
[01:58] responsible for processing data in the
[02:00] network such as input output output.
[02:01] Right? This reads like maybe a high
[02:05] schooler wrote a Wikipedia answer.
[02:07] That's kind of how you answer questions
[02:09] when you don't know who you're talking
[02:11] to. So that makes sense. What is the
[02:13] capital of France? The capital of France
[02:14] is Paris. So at least
[02:17] it would was able to to say something
[02:19] kind of made sense. So we kind of want
[02:21] to move it towards this direction where
[02:25] it's able to follow our instructions.
[02:27] For example, answer questions. So how do
[02:29] we do that? What's the solution to our
[02:31] problem? Uh we can show models examples
[02:34] of how we'd like them to answer
[02:36] questions or relate to us in a chat
[02:38] format and then they'll generalize from
[02:41] those tasks. How much text did we show
[02:44] this model in pre-training? About 10
[02:46] billion tokens. How many instruction
[02:48] fine-tuned examples are we going to show
[02:50] it? A few thousand. It we're just going
[02:53] to show a few thousand examples and
[02:55] we'll hope that it'll they'll general
[02:57] generalize beyond that. So in instruct
[03:00] fine-tuning, we retrain an existing
[03:02] pre-trained transformer, but we use
[03:04] sample prompts and answers instead of
[03:06] any text. So remember pre-training, we
[03:09] showed it the entirety of the internet
[03:10] and says, "Hey, can you do next token
[03:12] prediction on that?" in uh instructor
[03:15] fine-tuning, we'll show it only a few
[03:17] examples, a few thousand examples, a few
[03:20] hundred thousand examples, and then
[03:22] we'll hope that we're able to back
[03:23] propagate from that to updating uh the
[03:26] network so it works well with
[03:27] instructions.
[03:29] This is a good time to do a you are here
[03:32] slide. So you are here in instruct
[03:35] fine-tuning the third phase. We've gone
[03:37] through pre-training. We've mentioned
[03:39] men training, but let's try and kind of
[03:42] fine-tune what those differences are.
[03:44] Let's try and like really understand.
[03:46] So, in pre-training, we have a the the
[03:50] model learn the English language. That's
[03:53] all we're trying to do. How do we do
[03:55] that? We show it trillions of tokens,
[03:57] billions of tokens, and then we ask,
[04:00] hey, is the result the result we were
[04:02] looking for from our one sample
[04:04] sentence? Let's say I have a sample
[04:06] sentence, the capital of France is
[04:08] Paris. I would like the answer to be
[04:11] 100% Paris when it generates the token.
[04:13] And I would like all the other answers
[04:15] like Austin, Texas to be at 0%. So if I
[04:19] got an answer of 92% Paris and an answer
[04:22] of 8% Austin Texas, I'll penalize the mo
[04:25] model at both things. One, the result
[04:28] for Paris should be higher and two, the
[04:30] result for Austin should be lower. What
[04:32] do we call that? We call that cross
[04:33] entropy. Right? So we've learned about
[04:36] loss functions. That's all section
[04:37] seven. And we've learned about how cross
[04:40] entropy works.
[04:43] What else do we have to do after
[04:44] pre-training? And we're we're not going
[04:46] to do that in this workshop. A new thing
[04:48] that emerged in 2025 ling the the
[04:51] dialogue of building large language
[04:53] models is mid-training. Specifically, we
[04:56] want to improve the style, the
[04:58] reasoning, the long context and tool use
[05:00] of the model. What does style mean? Are
[05:03] you writing professionally? Are you
[05:05] writing uh familiarly? Are you
[05:08] reasoning? How does the model try and
[05:10] address problems like math and coding?
[05:12] It just, you know, even when it just
[05:14] says, well, aha, and then just keeps
[05:17] going. That's reasoning. Long context.
[05:20] We train a model on let's say most
[05:22] average samples are 40,000 tok to tokens
[05:26] 4,000 tokens however many tokens we have
[05:28] on average but we wanted to be able to
[05:30] generate a million tokens in so we have
[05:32] to learn and develop a set of technique
[05:34] that extend its long context window
[05:37] and tool use when we want to ask JGPT or
[05:40] claude to be our version of Google it
[05:43] has to use the web search tool so it has
[05:45] to learn all of these new skills within
[05:48] the context of using the English
[05:49] language age, right? So, for that we
[05:51] would show maybe 100,000 examples. We're
[05:54] still doing cross entropy and prompts
[05:56] though. All we're doing is we're showing
[05:57] it a thread that looks like we wanted
[06:00] to, a chat that kind of looks like we
[06:02] want to, and then it learns, oh my
[06:04] goodness, this is how I should express
[06:06] myself. So instead of saying when we ask
[06:09] it uh how much is two power of whatever
[06:13] and then it just spits out a number we
[06:16] actually wanted to go since 5 * 3 is 15
[06:19] and 15 * 2 is 30. Therefore x right we
[06:24] wanted to like go step by step we show
[06:26] it an example we cross entropy on that
[06:28] example and we do back propagation. We
[06:30] haven't seen an example of mid training
[06:32] and we're not going to see it in the
[06:33] context of this workshop, but important
[06:35] to know that it exists and is really
[06:36] part of the lexicon of how we expect to
[06:39] train large language models. Not in
[06:42] mandatory phase at all if you don't
[06:44] really care about the style, the
[06:45] reasoning, the long context, the tool to
[06:48] tool use just yet.
[06:51] What do we have that we are going to
[06:52] work on? This is the URL here slide
[06:55] instruct tuning. We want to create the
[06:58] AI assistant persona. How do we do that?
[07:00] We let's say we have a 100,000 examples
[07:03] of a model that uh sees how we want the
[07:07] model to behave and then it learns that
[07:10] from from the sample. For example, list
[07:13] three benefits of physical exercise.
[07:15] Then it has a list of three benefits.
[07:16] The model learns the number three kind
[07:18] of matches that number. When it says
[07:20] when I see the verb list, I want to see
[07:22] a list. Okay, that kind of makes sense.
[07:24] Why is that different? We're still kind
[07:26] of just training on cross entropy. Why
[07:29] is that different? Because now we have a
[07:32] positive signal for it. Now all of a
[07:34] sudden we know what we want the model to
[07:37] do. So in pre-training land, we didn't
[07:40] really have a positive signal. All we
[07:42] had is like, hey, here's a mountain of
[07:44] text that is theoretically unsupervised
[07:47] learning in a sense that we don't know
[07:48] the correct answer. And then like
[07:50] there's no blessed good way of
[07:52] completing the capital of France is
[07:54] because it could be Paris, could be full
[07:56] of cheese, could be has a master strike,
[07:59] right? All of those are equally valid
[08:01] option. In instruct tuning, we have one
[08:03] valid option. We know exactly what we
[08:06] want the model to say and how we want it
[08:08] to behave. So in instruct tuning, we'll
[08:11] show it 100,000 examples of how to do
[08:13] instruction following.
[08:16] Great. I will also mention since we are
[08:18] already like a bit road mapping here to
[08:20] the next section we have reinforcement
[08:22] learning. How is reinforcement learning
[08:24] different now we'll have positive and
[08:26] negative signals and we need to learn
[08:28] how to take all of those into account
[08:29] but we're not going to do instruct
[08:31] reinforcement learning just yet. Great.
[08:33] So how do we actually what task can we
[08:36] actually teach the model in instruct
[08:38] tuning? And I'm going to give you this
[08:40] as kind of like the state of the world
[08:42] late 2023 and then we'll have the next
[08:45] slide to tell us what happened since
[08:47] then. So around 2023 we had alpaka 2023
[08:51] and self-instruct papers in 2022.
[08:54] Really the way that we built instruct
[08:56] tuning was in kind of like a verbing
[08:59] kind of way. We generate a task. We
[09:03] rewrite a sentence. We give an example.
[09:05] We describe a sentence. We provide a
[09:07] list. We identified a type. We summarize
[09:10] a text. We edit a sentence. We create
[09:12] suggest a story. Right? We It's to verb
[09:16] a noun was how we did instruct
[09:18] fine-tuning. So we developed that.
[09:20] That's how we started with instruct
[09:22] tuning. We had 50,000 examples, 100,000
[09:24] examples. We showed it to the model and
[09:26] it learned how to to follow instructions
[09:28] and become an AI chatbot. It went from a
[09:31] glorious autocomplete to an AI chatbot.
[09:34] Really cool to notice that. What's one
[09:38] important notice to mention about
[09:39] instruction fine-tuning? It's all style
[09:42] over substance. None of this is like
[09:44] teaching the model new knowledge. It's
[09:46] not really learn maybe it's learning
[09:48] like how to answer questions. That's
[09:50] knowledge, but it's not teaching it that
[09:51] the capital of France is Paris. That's
[09:53] not what we're doing here. We're
[09:55] teaching it how to respond in a
[09:57] stylistic way that matches what we
[09:59] wanted to do. So instruction tuning
[10:02] isn't about correct answers. It's about
[10:04] correctly attempting the task. It's not
[10:06] even about being successful in the task.
[10:09] Pre-trained models don't even attempt
[10:11] the task. That's why we have to do this
[10:13] step. Great. So what happened since 2023
[10:17] alpaka paper came out and what's like
[10:19] instruction tuning? Let's call it circa
[10:21] 2024 and later after 2024 we really
[10:24] changed our verbing a noun style of
[10:27] instruct tuning and we've looked at it
[10:30] as adding more capabilities to the
[10:32] model. So this becomes like manners over
[10:36] memory. We really don't like want to
[10:38] give it all of the potential options for
[10:40] task. That's an infinite amount of verbs
[10:42] people would present an AI chatbot. But
[10:44] we want to teach it manners. What's an
[10:46] example?
[10:48] So over here we have a screenshot from
[10:50] small LM2 where they really really went
[10:53] into how their instruct fine-tuning
[10:55] works and you can kind of see what are
[10:58] the type of things they gave it in
[10:59] instruct fine-tuning. They try to teach
[11:02] it conversation on instruction
[11:04] following. They try to teach it math.
[11:06] You could see that under math data. You
[11:08] they try to teach it coding. You could
[11:10] see that from star code to instruct.
[11:12] They try to teach it tool use. You could
[11:14] see that from function calling data set.
[11:17] You they try to teach it to respect
[11:19] system prompts. You know be there used
[11:21] to be a time where system prompts
[11:22] weren't really a thing. We kind of had
[11:24] to like make that up and then people
[11:26] could easily just like make the model
[11:28] forget system prompts. So we can create
[11:31] that capability using instruction
[11:33] fine-tuning. We also try to teach the
[11:36] model long context. Our data is 40,000
[11:40] tokens long on average that we fine-tune
[11:42] on that we pre-train on. We want to be
[11:45] able to work for a million. Then we have
[11:47] to show it examples of doing that
[11:48] extrapolating to longer context. And
[11:51] then we want to teach it multi-term
[11:53] conversations. No one uses the chatbot
[11:55] for one question. Maybe some people do.
[11:57] maybe if they're trying to cheat on one
[11:59] homework question, but generally we all
[12:01] having like slightly longer conversation
[12:03] than that. Great. So, we moved from
[12:06] verbing a noun to, hey, what capability
[12:08] do I want to add? And that's actually
[12:10] reflected in the data sets nowadays as
[12:12] well. You'll pull in a data set for the
[12:14] capability you care about.
[12:17] So, how does this actually work under
[12:19] the hood? We are software engineers and
[12:20] we really care about what do we end up
[12:22] showing the model. So there's a bunch of
[12:25] formats that we can use to show an
[12:27] example of attempting a task and then uh
[12:31] see how the model would respond to it.
[12:33] So the the most common model that is
[12:36] being discussed here for example is
[12:37] going to be alpaka.
[12:39] We show it an instruction with this
[12:41] three hash marks and then what is 2 plus
[12:44] 2 and its response is four. If I wanted
[12:47] it to go like what is a very complicated
[12:50] math expression and then we would show
[12:52] it doing it step by step. That would be
[12:54] another option. I just didn't have room
[12:55] on this slide to do a really complicated
[12:57] math example. Okay. Is that the only
[12:59] format that exists? No. The screen is
[13:02] littered with examples of pretty much
[13:04] identical formats that have nothing but
[13:07] cosmetic differences. Chedd says I am
[13:10] start I am end. I am start I am end for
[13:12] the assistant. Right. G the gamma format
[13:15] is start of turn, end of turn, start of
[13:17] turn, end of turn, right? All of these
[13:19] have different formats. Lama 3, Zephyr,
[13:21] Mestral, all these have different
[13:23] formats, but they're basically the same
[13:25] one, right? When you kind of squint and
[13:27] look at it, you're like, well, okay,
[13:29] this one really cared about highlighting
[13:30] an assistant persona, and this one
[13:33] really wanted to have like the uh to
[13:36] save on on tokens. Each of these kind of
[13:39] prefers slightly different things. None
[13:41] of them have the right answers. probably
[13:43] training on a mixture of these is better
[13:45] than training on all of these. But for
[13:47] us in our instruction fine-tuning
[13:49] script, we'll use alpaka and nothing
[13:51] else. Why? Because it's easy, simple,
[13:53] and it's pretty well accepted.
[13:56] Since we're talking about formats, I
[13:58] should mention we said we've moved from
[13:59] a verb a noun syntax. So now we are all
[14:04] about capabilities. So how do we teach a
[14:07] model using fine tu using instruction
[14:09] tuning? How do I have these new extra
[14:12] capabilities? So for example, system
[14:14] prompts, we would show it an example of
[14:16] an IM start system and then would
[14:19] respect the system prompt extra. This is
[14:21] from Chedml. Um you are a helpless AI
[14:24] assistant named small M3 by hugging
[14:26] ffist. You are a thoughtful inter here's
[14:28] your metadata like your knowledge cut
[14:29] off reasoning disabled. I am in right.
[14:32] So now it we it sees a bunch of examples
[14:34] of system prompts. Then it'll have a
[14:36] prompt. Then it'll show how it takes the
[14:38] system prompt into account.
[14:40] reasoning. Uh we can add reasoning here.
[14:43] Now we've added the the think tags into
[14:46] a into a math expression. So how many
[14:48] prime numbers are between 50 and 70? And
[14:50] you could see it going 50 51 52 53 54
[14:54] right it's going one at a time trying to
[14:56] go like this yes no versus just spit out
[14:58] a random answer 42 11 right it could
[15:02] just do that. Instead it's actually
[15:04] reasoning in think tags. So that's the
[15:06] invention of tra of chain of thought
[15:09] inside of a reasoning trace
[15:13] tool use. We can define a bunch of tools
[15:15] and then we can give it a bunch of
[15:17] examples on how to use those tools
[15:18] within the within the instruction tuned
[15:22] format.
[15:25] Great. So that's an example of us having
[15:27] seen a bunch of new capabilities
[15:29] introduced into the model using instruct
[15:32] instruction tuning. What are some
[15:34] sources that we can find for instruction
[15:37] tuning instructions? Uh, instruction
[15:39] tuning instructions that's repetitive
[15:41] and needless. Um, prelim NLP benchmarks.
[15:45] So, we mentioned the field of natural
[15:47] language processing existed before large
[15:49] language models did a lot of really
[15:52] brilliant things. Some of these were
[15:54] just natural language tasks. We can take
[15:57] all of these things and then we can
[15:59] convert it into instruction fine-tuning.
[16:02] uh tasks. For example, the balanced copa
[16:07] 2019 benchmark is one such data set that
[16:10] we'll actually use in our instruction
[16:11] fine-tuning.
[16:13] What is the balanced copa data set? I've
[16:16] got it open right here. I've got a
[16:18] scenario. The garden looked well
[16:21] groomed. This so balanced copa is about
[16:23] common sense. The gu the garden looked
[16:26] well groomed. Was that because a the
[16:29] grass was cut or b because the sun was
[16:31] rising?
[16:32] Clearly the garden looked well groomed
[16:34] because the grass was cut. We find a way
[16:36] of combining this into a question into a
[16:39] multiplechoice and then we reward the
[16:42] model when shift its weights closer to
[16:46] the correct answer that teaches it to
[16:49] like show common sense more. Great. So
[16:52] we could do that. Uh that was using the
[16:55] flance style, not any of the styles
[16:57] we've seen thus far, but that was one
[16:59] example of another in of another style
[17:01] that you could use for instruction
[17:03] tuning. Another source for instruction
[17:06] fine-tuning could be human written
[17:07] prompts. Right? That's kind of how we
[17:10] started the open assistant style of
[17:12] 2023. We had people sitting in Nigeria
[17:15] in the Philippines and they were like
[17:17] writing these fun prompts, right? You
[17:20] could see some problems with that
[17:22] scalability. so on and so forth. Also,
[17:25] why did models uh start using new words
[17:28] that we weren't commonly using in
[17:30] English? Because they were were being
[17:32] used in regional dialects of English
[17:34] spoken in those countries. Why do models
[17:36] delve, for example, because it's just
[17:38] more common to say that in Nigerian
[17:40] English, right? So, it's some problems
[17:42] with instruction tuning here. It didn't
[17:45] just learn instruction tuning, it
[17:47] learned the local dialect. another
[17:49] option for instruction tuning almost
[17:52] definitely the most dominant source at
[17:54] this point in time where we have great
[17:56] LLMs the LLMs that are super good the
[17:59] frontier can generate these prompts and
[18:02] then teach newer models using these
[18:04] prompts we don't have to pay people or
[18:06] we don't have to salvage tasks from pre
[18:08] 2019 we could just use LLMs great so
[18:12] those are the three general buckets
[18:14] categories of where we got get our
[18:16] instruction in tuning data sets uh and
[18:20] we covered balanced copa. Let's look at
[18:21] an example of how we convert balanced
[18:24] copa into the alpaca style. That's what
[18:26] our script is going to have to do. So
[18:28] instruction given the premise which
[18:30] alternative is more likely my body cast
[18:33] a shadow over the grass. Choice one the
[18:36] grass was cut. Choice two the sun was
[18:38] rising rising. Response choice two the
[18:41] sun was rising. Right? it needs to like
[18:44] see an example of both following the
[18:45] instruction format and then it'll
[18:47] generalize uh outside of the format but
[18:50] also see an example of how common sense
[18:52] works.
[18:54] Now, we have to talk about fine-tuning,
[18:56] which is how we show the model any of
[18:59] this stuff, right? So, we wrote a bunch
[19:01] of great instructions. So far, we've
[19:04] kind of been working on cross entropy.
[19:06] We're going to shift a little bit away
[19:08] from that in the sense that maybe our
[19:10] our model is still using cross entropy,
[19:14] but we're no longer pre-training the
[19:16] entire model. We're going to want to
[19:18] fine-tune it for specific tasks. And
[19:21] here, I have to really apologize.
[19:23] Fine-tuning is its own full day
[19:25] workshop. We're just not going to be
[19:26] able to cover all of the complexity and
[19:29] interesting notions within it and its
[19:31] history. I'm going to give it exactly
[19:33] one slide here. What's the slide? So,
[19:36] fine-tuning takes thousands of prompts
[19:38] and retrains a pre-trained LLM to match
[19:41] stylistic mannerism. Stylistic
[19:43] mannerism, it doesn't teach it anything
[19:45] new. It teaches it to speak like a
[19:47] doctor. It doesn't teach it medicine.
[19:50] Because it's a full day workshop, let's
[19:52] try and summarize to the three super
[19:55] category types that we have within
[19:57] fine-tuning. That'll give you enough
[19:59] lexicons that you can go and like one
[20:01] understand what's going on with
[20:02] fine-tuning and two you can go decide
[20:05] which kind you want to research. So
[20:07] three kinds of fine-tuning that we can
[20:09] really talk about. There's full
[20:11] fine-tuning. That's effectively what
[20:13] we've been doing in pre-training. We
[20:16] have the entire network unlocked. We've
[20:18] got cross entropy and we're going to
[20:20] update every single learnable parameter
[20:22] and weight. Why is that a problem?
[20:25] Pre-training on the entire model is like
[20:28] billions of parameters, millions of
[20:30] parameters. It's slow and expensive.
[20:34] So for full fine-tuning, we have to
[20:37] train the entire model and as a result
[20:39] of that, we'll use 100% of the memory
[20:41] required in the GPU. So we need a GPU
[20:43] that can hold the me the the model and
[20:46] at the same time also hold the entire
[20:48] batch size of all the examples of feed
[20:51] forward and back propagation kind of
[20:53] intense what's an alternative 2021 came
[20:57] up with uh the um the Laura the Laura
[21:02] finetuning approach where we keep most
[21:05] of the mo model frozen but we add an
[21:08] adapter at for some of the parameters at
[21:11] some of the layers
[21:12] And it's empirically proven to be as
[21:15] robust as fine-tuning. I had to write
[21:17] this sentence like 10 times until I
[21:20] could like make it like make sense. It's
[21:22] empirically proven to be as robust as
[21:23] full fine tuning. Is it as good as fine
[21:26] tetuning? Unclear, but we've empirically
[21:28] proven that it performs to the same
[21:29] level. And that's from Thinking Machines
[21:31] 2025.
[21:33] Why? Why is Laura better than full
[21:35] fine-tuning? One, it has equal
[21:37] performance. We've empirically proven it
[21:39] as we said, but two, because we're
[21:42] training a small adapter that we've
[21:43] bolted on in layer 7, we bolted on in
[21:46] layer 15, right? This is a very small
[21:49] adapter that we're bolting on top of our
[21:51] model because we're only fine-tuning
[21:52] this itty bitty model. We need a lot
[21:54] less space on our GPU, right? We still
[21:56] have to run the full model to do feed
[21:58] forward, but in terms of like
[22:00] maintaining gradients and optimizer
[22:02] state and all of that, we're only
[22:04] maintaining it for a very small
[22:05] percentage of a network, maybe 1 to 5%.
[22:08] So very small like the memory footprint
[22:10] is much smaller than it would otherwise
[22:12] be. So that's Laura. What's Qura? That's
[22:16] a 2023 advancement where we discovered
[22:19] that like oh my god I want to hold this
[22:21] massive 100 billion parameter model in
[22:23] memory one to two to 5% that could still
[22:27] be 5 billion parameters hey can I
[22:29] somehow instead of using the amount of
[22:32] memory that would need for five billion
[22:33] parameters can I use 1%. Can I use a
[22:36] smaller amount of memory there? So yes,
[22:40] we can instead of holding our adapter at
[22:42] full fidelity at like a float 32, we can
[22:45] hold it at something like a float 8 or
[22:47] float 16 or something like that. I'm not
[22:50] going to fully explain why what what's
[22:52] going on with data types. I had this in
[22:54] one of the formats for this deck and
[22:56] decided to just cut it out. I think it's
[22:58] like something we can learn outside of
[22:59] the context of this workshop. Why what
[23:02] is important for us to know? It's
[23:04] important for us to know that Qura
[23:06] quantitize
[23:08] lowers the fidelity uses a different
[23:10] data type. It just uses less memory.
[23:13] That's the important thing. So we take
[23:15] our our adapter that used to take 1 to
[23:18] 5% of memory and now it can take 15% of
[23:21] even that amount of memory, right? So of
[23:24] the remaining 1 to 5%.
[23:27] So let's look at the differences one
[23:29] more time. Full frame training loads the
[23:31] entire model into memory. It lets you
[23:33] edit the entire model. Has to do back
[23:35] propagation the entire model. Super
[23:37] inefficient. Laura comparable to full
[23:40] fine-tuning. Has the same result. We
[23:42] bolt an adapter on top and a few layers
[23:44] on a few parameters. And then we can
[23:47] decide to like only fine-tune those even
[23:49] though we run our feed forward on the
[23:51] whole network. We only back propagate on
[23:53] a very small percentage on the adapter.
[23:56] Qura says the adapter itself in memory
[23:59] could have lower fidelity than the rest
[24:00] of the model. Even better, we can hold
[24:03] it with less memory. We can have bigger
[24:04] bat sizes. Amazing. So full fine-tuning,
[24:09] Laura fine-tuning, quantitized Laura
[24:12] fine-tuning, Qura. Th those are the
[24:15] differences. Great. So we kind of
[24:17] covered the three big types of
[24:18] fine-tuning.
[24:20] Let's talk about the worst thing that
[24:22] can happen. One would say it's even
[24:24] catastrophic if it happens. It's
[24:26] catastrophic forgetting. So if we have
[24:29] too many specific tasks, we can
[24:32] effectively overtrain on them causing
[24:34] the capabilities that we acquired in
[24:36] pre-training to be totally forgotten or
[24:39] somewhat forgotten or somewhat
[24:40] diminished. What's an example
[24:44] on the left side? Bitterman 2024 also
[24:48] same bitter by the way that we saw a
[24:49] chart from in 20 from 2023 summarizing
[24:52] batch size and whatnot. They showed that
[24:55] longer finetuning on code causes
[24:57] catastrophic
[24:59] forgetting on for common sense. What
[25:01] does that mean? If I take a really great
[25:03] pre-trained model and then I run this on
[25:06] code for fine-tuning for like an
[25:08] infinite amount of epics. I think here
[25:10] they ended up doing uh something like 16
[25:13] epics, right? Worth of just showing the
[25:16] data over and over again 16 times. It
[25:18] lost so many it lost a substantial
[25:21] amount of its common sense abilities,
[25:24] right? Laura, however, did mitigate this
[25:27] a bit because we didn't unlock the whole
[25:29] model to be edited. So really, the model
[25:31] was able to recover and kind of protect
[25:33] itself more. What does that mean to us?
[25:37] Laura is a natural defense against
[25:39] catastrophic forgetting. Why? Because
[25:42] we're not unlocking the whole model. So
[25:44] that's actually something really
[25:45] important to know. Other ways we can
[25:47] like mitigate catastrophic forgetting.
[25:49] Don't run as many steps, as many epics.
[25:52] Right? You could see here on the x-axis,
[25:54] the more epics we run, the more we
[25:56] forget. Common sense when we train on
[25:58] code.
[26:00] Run less steps. That's a pretty easy
[26:02] answer. One answer, use Laura. Another
[26:05] one, use less steps. There's a third
[26:08] answer which is called kale divergence,
[26:10] which we're not going to get into right
[26:11] now. There's many many answers as to how
[26:13] to prevent catastrophic forgetting.
[26:16] Right? Basically, I don't want to just
[26:17] eat my cake. I want to eat my cake and
[26:20] then have a bigger cake at the end.
[26:22] Right? I don't want to just have it. I
[26:24] want to make it bigger. So, that's the
[26:26] whole game with instruction tuning. And
[26:27] honestly, to some extent with RL, can I
[26:30] get extra capabilities without giving up
[26:32] any existing capabilities?
[26:34] Um, I'm going to just read directly from
[26:36] the from the deck. LM pre-training works
[26:39] on a wide distribution. forgetting
[26:41] happens when we have a smaller
[26:42] distribution takes precedence. So
[26:44] imagine you've been trained on the
[26:46] entirety of the English language and all
[26:48] of a sudden all you see is math examples
[26:50] or code example. You're going to go like
[26:51] I don't need any of this English stuff,
[26:53] right? So one fourth solution we have to
[26:56] catastrophic forgetting. We mix in more
[26:59] examples of the stuff that we were
[27:01] trained on in pre-training. More
[27:02] examples of like just predicting text in
[27:05] a general kind of way. So mixing becomes
[27:07] really really common. Great. So we
[27:10] talked about catastrophic forgetting,
[27:12] why it's catastrophic, catastrophically
[27:14] bad some would say, and then we talked
[27:17] about the various things we could do to
[27:18] mitigate that. Specifically, train less
[27:22] and use Laura um mix in data, something
[27:26] called kale divergence, which we're not
[27:28] going to cover in this workshop. There's
[27:29] a bunch of ways of doing that. Great.
[27:33] Let's come up with a couple of
[27:34] decisions. What are my architecture
[27:36] choices? One will have a separate script
[27:38] for instructing instructoring a
[27:41] pre-trained model. Why? The pre-trained
[27:44] model script runs for hours, days,
[27:48] right? Weeks potentially. Instructor
[27:50] tuning is traditionally much much much
[27:53] faster than that. Could potentially run
[27:54] in an hour in 15 minutes. My version
[27:58] actually has so few steps it runs in 5
[28:00] minutes.
[28:02] What type of finetuning are we going to
[28:04] use? We're going to use 124 million uh
[28:07] model LLM. And because of that, it fits
[28:10] great within my GPU, right? So 124
[28:14] million parameter LLM fits really well
[28:17] within an A140 GB. I'm not going to cue
[28:20] Laura, but I will lura to help reduce
[28:23] the chances of catastrophic forgetting.
[28:26] Uh the instruction data set, I'm going
[28:27] to use Tatsu Lab Alpaka, which we'll see
[28:30] in a moment. The instruction format is
[28:33] going to be alpaka. Obviously, it's in
[28:34] the name of the data set. Benchmark is
[28:37] going to be balanced copa. So, I'm going
[28:38] to make sure to evaluate it on common
[28:41] sense. I want to see even though my
[28:43] instructions have nothing to do with
[28:45] common sense. I want to see it get
[28:46] better at common sense. That's the
[28:48] important thing for me. I want to see it
[28:50] improve. Not just when I smoke test the
[28:53] model and see it follow instructions
[28:54] better. I want to see it do something
[28:56] better. I want to see it be more
[28:58] cognizant. And totally I'll use 1,200
[29:01] steps maximum. I just don't want to see
[29:04] the model catastrophically forget. The
[29:06] chart in the bit in the bottom is going
[29:08] to show us 2,000 steps. It's going to
[29:10] show us that we didn't really gain a lot
[29:11] from that from balance copa. So let's
[29:13] look at these charts. One of them is
[29:17] training loss. What's our training loss
[29:19] on? Cross entropy. Cross entropy on
[29:22] what? We're using Laura finetuning on an
[29:24] adapter that we've bolted on top of the
[29:26] model. What's it based on? How likely is
[29:29] the model to predict the entire format
[29:31] of the alpaca format? What's the alpaca
[29:33] format? We saw it here. What is 2 plus 2
[29:36] for? We want to reward the model if it
[29:40] has the the the probabilities of
[29:43] producing every one of these tokens.
[29:45] Great. So that's what we're go we're
[29:47] going to do. So we see training loss
[29:49] dropping really quickly. In the
[29:51] beginning, it really didn't know what to
[29:53] do about the alpaca format. Then it
[29:54] picked it up almost within like a 100
[29:56] steps. then within 500 step it really
[29:58] equalized in a good spot and he's
[30:00] getting more and more and more
[30:01] instruction tuning but maybe he's
[30:03] catastrophically forgetting at the same
[30:05] time. So let's look at balanced copa or
[30:08] common sense mo uh our common sense
[30:11] evaluation not a big improvement started
[30:14] off at 55% got to 57%. Doesn't sound
[30:18] super great. I do want to highlight
[30:20] randomness is 50%. This is a very small
[30:23] model. It doesn't have common sense
[30:25] choice and emerging capability. It's
[30:26] really just starting to pick it up at
[30:28] 124 million, right? It hasn't reached
[30:31] the peak of common sense emerging
[30:33] capability, but an improvement from 55
[30:35] to 57 is actually a huge change because
[30:38] 50 is random, right? Like there's only
[30:40] two options for for balance scopa. So 50
[30:43] is random. That's actually a pretty
[30:44] meaningful improvement.
[30:46] And I did promise you we'll show you
[30:48] tatsu lab alpaka. So let me show you
[30:50] that alpaka data set tatsu.
[30:55] Great. Let's just pull one up. I just
[30:57] want to make sure that you're able to
[30:58] see that. So, let's look at the
[30:59] instruction. Give me three tips for
[31:02] staying healthy. The output is eat a
[31:04] balanced diet to make sure you include
[31:06] plenty of fruits and vegetables,
[31:07] exercise a lot, so on. What's the text
[31:10] we're going to show? Below instruction,
[31:11] describe a text. Write a response that
[31:13] appropriately completes this request.
[31:14] Right? And then so on. And then there's
[31:17] and then we now know how to stitch this
[31:19] together to an instruction response uh
[31:21] instruction. Great. So now we not need
[31:25] to write a script for this. I'm actually
[31:27] not going to write this myself. We've
[31:28] gotten so far into this that like one I
[31:30] would have to like write all of Laura
[31:32] for you and you you didn't learn Laura
[31:34] like this it own full day workshop. So
[31:38] we're going to have a slide dedicated
[31:39] for AI coding assistant which we're
[31:41] going to seek on this deck. What what is
[31:45] this deck? What is the slide going to
[31:47] have? It's going to say Laura. Here's a
[31:48] bunch of parameters for Laura.
[31:51] You don't know what uh rank means. you
[31:53] don't know what alpha means again it's a
[31:54] full day workshop to learn about
[31:56] fine-tuning data we'll have to have end
[31:59] of string tokens one important thing to
[32:01] mention is we will pad in items and
[32:04] we'll see that in a moment when we look
[32:06] at the code training we'll use atom w
[32:09] again for training we have to choose an
[32:11] optimizer this is a new training run
[32:13] that's separate from our pre-training
[32:14] run we have to choose batch sizes batch
[32:16] of 32 gradient clipping how are we going
[32:20] to what data type are we going to use
[32:22] cross entropy so on uh batching really
[32:26] important to mention that we'll batch
[32:28] right why is that my model can only
[32:31] accept let's say a thousand characters
[32:33] maybe a 100,000 tokens
[32:37] we want to show it let's say 32 examples
[32:40] at the same time that means we're going
[32:41] to have a lot of dead space in between
[32:43] these examples if you put them at fixed
[32:45] distances we'll use a padding token to
[32:47] fill that area up eval will run our
[32:50] balance copa eval every 10% of steps
[32:53] every which is about 500 test samples
[32:56] and we'll use natural language not
[32:58] alpaca for that. So we want to check
[33:00] that it still knows how to speak
[33:02] language cuz otherwise we would have
[33:03] done catastrophic forgetting. Smoke test
[33:06] will generate five instruction prompts
[33:08] before and after so we can compare and
[33:10] storage will end up storing it instead
[33:12] of dash pre-training PTH which is where
[33:15] we're going to pick up we're going to
[33:16] write dash instruct afterwards. Great.
[33:19] So this wasn't meant for us. This was
[33:20] meant for an AI coding assistant, but
[33:22] maybe like it made sense to you when I
[33:24] read it. So, how do we write this
[33:26] notebook? One option is you go learn how
[33:28] fine-tuning works. Another one is we can
[33:31] again
[33:32] uh copy this AI coding assistant prompt,
[33:37] show it this deck, show it the
[33:38] pre-training script, ask it to write it.
[33:40] Another option is we could go to go just
[33:43] in angel AI/ Lego. We just said that we
[33:47] have all of our choices here in the
[33:48] script, right? And now we know a little
[33:52] bit about find about instruction
[33:54] fine-tuning. So we could say I want my
[33:56] script to to use Laura or cure Laura and
[34:00] then this is how many steps I wanted
[34:02] maximum. What chat format should I use?
[34:04] Use chat ML use alpaka, right? What is
[34:08] the instruct data set? maybe used
[34:10] balanced cop by itself or open assistant
[34:12] or flan or small tool mix fine use tatsu
[34:16] lab alpaka and then I can copy this into
[34:20] let's say my AI coding assistant and say
[34:23] hey would you mind you're generating all
[34:25] these scripts for me and it'll also
[34:26] generate the instruction tuned uh script
[34:31] so when we do that here's an example of
[34:33] something we could get out of it one
[34:36] thing that it does and like we could
[34:37] just review the script and see what it
[34:39] does. So, first thing, I have a little
[34:41] bit of setup here. First thing, it needs
[34:43] to load up my Google Drive that has my
[34:46] pre-training model. And then also, it
[34:49] needs to be able to save my instru. So,
[34:53] this is my pre-trained model. This is my
[34:55] instru model. Great. So, hopefully it
[34:58] found that. Great. It did find that.
[34:59] That's great for me. There's a bunch of
[35:01] configurations here. Some of them
[35:03] belonging to the model. Some of them
[35:05] belonging to the Laura adapter. you
[35:07] don't know anything about Laura
[35:08] adapters. I can't explain what these
[35:10] numbers are to you. Great. So now we
[35:12] have all of our configs. Here's my model
[35:14] architecture. Again, we said this is a
[35:16] very specific model. It's using RU
[35:18] squared. It's got this many transformer
[35:20] heads. So on and so forth. We load it
[35:22] into memory. Then we apply Laura. We
[35:25] pulled in a library to do that for us
[35:28] using the config that we said earlier.
[35:31] We load the Alpaca data set. As you
[35:33] could see, we're kind of building the
[35:35] instructions ourselves. We're not using
[35:36] the instructions that came with the data
[35:38] set. We but we are using its component
[35:40] the instruction and the output text.
[35:42] Maybe an instruction and an output text
[35:44] if we have an instruction.
[35:47] After that we'll tokenize the example.
[35:49] We'll send it in the correct format to
[35:51] the model. Then we'll do batching. Why
[35:53] do we have to do batching? If I have a
[35:56] context window of 100,000 characters, I
[35:58] don't want to just do one example. I
[36:01] want to do 32 examples. I want to fill
[36:03] out the entire context window cuz that's
[36:06] going to save on the cost of doing
[36:07] Laura. What What's the problem? Let's
[36:09] say I have 100,000
[36:12] contact size tokens. Let's say I do 10
[36:15] examples. The first example would be
[36:17] zero tokens. The second example 10,000
[36:19] tokens. The third example at 20,000
[36:22] tokens. There's going to be a lot of
[36:23] padding in between them. So for that,
[36:25] I'm going to have to add the padding
[36:27] token into them.
[36:29] So important to notice that we are doing
[36:31] quite a lot of padding here. Balanced
[36:34] copa evaluation. We said we we've got
[36:36] balanced copa. We also said we will
[36:38] never ever write our own eval harness.
[36:41] We'll always use an a pre-existing eval
[36:44] harness. Here I wrote my own because I
[36:46] said I'm never going to do that. So of
[36:47] course I had to. You load the data set.
[36:50] You run it through the samples. You give
[36:52] it a choice. And then you evaluate it
[36:54] and kind of like try to figure out which
[36:55] option to choose. Great. Let's generate
[36:58] a couple of smoke tests.
[37:01] Explain what a neural network is. What
[37:04] is the capital of France? How many Rs
[37:06] are in strawberry? List three benefits
[37:08] of exercise. And we'll just generate the
[37:10] text from the model. So before before we
[37:13] ran this uh what is the capital of
[37:15] France? The capital of France is France.
[37:16] The capital of France is Paris.
[37:18] Overview. The f the capital of country
[37:20] of France. The capital of France is
[37:21] Paris. History. The capital of France is
[37:24] Paris. Right? It's just emitting
[37:25] nonsense at this point. Not great. Uh,
[37:29] write a short poem about the moon. Then
[37:31] it just repeats stuff and nausem here.
[37:34] Uses exclamation like uses dashes,
[37:38] multi- choice questions. Not not super
[37:40] great. What is a neural network? Explain
[37:43] a neural network in simple terms. It
[37:45] just keeps asking the same question over
[37:47] and over again. So, not great at
[37:48] instruction tuning. We run instruction
[37:51] tuning. We run the training set again.
[37:54] And what's the training on? It's just
[37:55] going to be cross entropy with Laura on
[37:58] our instruction data set.
[38:01] And then we could see the training loss
[38:03] over the many many steps. It's just
[38:05] going to drop over time. Balance copa is
[38:07] going to increase over time meaningfully
[38:09] to me. Uh and so on. Eventually we take
[38:13] the Laura adapter. We have to save it
[38:15] somewhere, right? And at the end of RL,
[38:17] we might merge it back into the model.
[38:19] And then we can generate some text here
[38:21] and see instruction write me a short
[38:23] poem. the response. The moon is like a
[38:24] wave. A wave is like the sky. It is a
[38:27] reminder of the moment. It's a way to
[38:28] communicate. It's a reminder of the
[38:30] past, right? And eventually it doesn't
[38:32] fully complete this in a way that makes
[38:34] sense, but it's getting close to the
[38:36] instructions that like it passes my
[38:38] sniff test of doing better. Uh explain
[38:41] what a neural network is in simple
[38:42] terms. A neural network is a type of
[38:44] computer architecture that uses
[38:45] structures and algorithms, right? Reads
[38:47] like a Wikipedia entry. Great. So that's
[38:50] our instruction fine-tuning
[38:53] after uh let's learn let's talk about
[38:56] resources where you could learn more.
[38:58] One resource is if you want to learn
[39:00] more about fine-tuning, you should read
[39:02] the Cedar paper from 2024 from the
[39:04] Ireland Center for AI. It is very
[39:07] comprehensive to everything we knew in
[39:09] 2024. And honestly, it hasn't shifted
[39:11] that much. Some new insight in 2025, but
[39:14] not that many.
[39:16] What does this paper look like? Oh my
[39:19] goodness, he's pulling it again. Once
[39:20] again, he manifested this into physical
[39:23] form. Um, and then we have all of the
[39:27] various uh fine-tuning parameters so
[39:31] explained here and how we how
[39:33] fine-tuning works and the differences
[39:35] between it and a rail. Really great
[39:37] paper. I strongly recommend it. Again,
[39:38] available for free online. Other places
[39:41] you could find information about
[39:42] fine-tuning instruct tuning models are
[39:45] the papers for the models that have done
[39:47] it. So Almo 3, small three actually
[39:50] small two is better for instruct fine
[39:52] tuning I think because they don't talk
[39:54] about it a lot in small three trinity
[39:57] ary so on so I would recommend reading
[39:59] these papers if you want to learn more
[40:01] about instruct fine-tuning
[40:04] our last full me section is going to be
[40:06] about reinforcement learning why because
[40:08] we still have things we want to do after
[40:11] we've gotten our model to answer
[40:12] instructions we want to answer them in a
[40:15] specific way we want them to answer it
[40:17] correctly potentially. So that's going
[40:19] to be all in rein in reinforcement
[40:21] learning. I hope you join us and I'll
[40:23] see you soon.
