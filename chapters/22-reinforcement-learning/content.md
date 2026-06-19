# Reinforcement Learning | Build Your Own LLM Workshop #22

**Build Your Own LLM Workshop — Video #22 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 42m 12s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=3DJGUp0CVx8 |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to building
[00:04] your own large language model workshop.
[00:06] I'm Justin Angel. And now we're in our
[00:08] last medi section of reinforcement
[00:10] learning or RL for short. What does RL
[00:14] do for us? RL helps us fix a problem, a
[00:18] very specific problem. Sometimes we've
[00:20] got our instru models. So remember, we
[00:23] pre-train a model, we instruct tune it.
[00:26] Sometimes it doesn't do super hot on
[00:29] math, on code, on puzzles like logic,
[00:32] style, factual accuracy, creativity,
[00:35] safety, multilingual performance, and so
[00:38] on. It probably has all that information
[00:40] within it from reading the internet, the
[00:43] books, the everything, right? But it
[00:47] doesn't get surfaced because it it
[00:50] doesn't know that it needs to surface
[00:52] that. By the way, that's not always
[00:54] true. You can have models that are never
[00:56] RL and they perform very well. So, but
[01:00] in the event that we do have a
[01:01] pre-trained model, an instru model that
[01:04] doesn't perform super well, we can then
[01:07] RL it. What is RL
[01:10] right is we could take both positive and
[01:13] negative signals and triangulate the
[01:16] change in the model between uh the model
[01:20] the positive signal the negative signal
[01:22] the change and triangulate between all
[01:24] of those to see where models are where
[01:27] they should go and where they shouldn't
[01:28] go right negative signal tells us don't
[01:31] become closer to that thing positive
[01:33] signal says move to that place the
[01:35] triangulation happens because we have
[01:36] our current model as So we can kind of
[01:38] do something between all three of those.
[01:41] RL specifically replaces cross entropy
[01:44] as the loss function with fun math.
[01:47] That's the only description I can give
[01:49] you without fully explaining how policy
[01:51] optimizations work. And that's pretty
[01:54] meaningful meaty math at the graduate
[01:56] level. So I don't think it's appropriate
[01:58] for like at this point to like fully
[02:00] explain it. But the fun math takes
[02:03] positive and negative signals replaces
[02:05] cross entropy. What are my positive
[02:07] signals? Let's look at the right here.
[02:10] Positive and negative signals. How do
[02:11] you make a maltaf cocktail? Well, you
[02:13] gather a glass bottle, a flammable
[02:15] liquid, a rag, and you put it in a
[02:16] bottle. That's probably bad. We should
[02:19] from a safety perspective not have our
[02:21] models say that to, you know,
[02:24] potentially small children, vulnerable
[02:26] populations. I don't know. How do you
[02:28] make a mouth of cocktail? Should
[02:29] probably say I can't provide
[02:30] instructions for making weapons. By the
[02:32] way, when I tested this on JPT created a
[02:35] totally new account, they could ban you
[02:37] for even asking that. So, good to know
[02:40] RL
[02:42] on that would be good example refusal.
[02:46] Bad example answering the question.
[02:49] What's another example of where we can
[02:51] provide RL into our model? Uh, the women
[02:55] met for coffee because the c the cafe
[02:58] reopened in a new location. No, I can
[03:01] bad response that that sentence doesn't
[03:03] make any sense. It's not common
[03:05] sensical. The women met for coffee
[03:07] because they wanted to catch up with
[03:08] each other. Yes, good. So, I could
[03:10] thumbs that up. We all have the ability
[03:13] to do RLHF or RL with bad updown
[03:17] prompts. So, we all have access to that.
[03:22] I want to do another where are we, you
[03:24] are here kind of slide. So, remember we
[03:26] started it pre-training. We showed it an
[03:28] internet worth of data. We cross entropy
[03:31] on that text and try to teach it next
[03:33] token prediction. What did we do after
[03:35] that? We did MET training. We taught it
[03:37] how to use the English language a bit
[03:39] more effectively as a and as as a large
[03:43] language model specifically what are
[03:45] system prompts how do you handle long
[03:47] context what's reasoning stylistic
[03:49] differences so on instruct tuning taught
[03:52] it how to follow examples right we have
[03:55] like a list this is what a list looks
[03:57] like I want you to use list when people
[03:59] use the word list um however that was
[04:03] still cross entropy but it was only on
[04:06] positive signal How is reinforcement
[04:08] learning different than that? And this
[04:10] is where I personally draw the boundary
[04:12] between instruct tuning and
[04:13] reinforcement learning. It's when you
[04:15] have both a positive and a negative
[04:17] signal. So on reinforcement learning,
[04:19] we'll take that positive and negative
[04:21] signals. We'll do some fun math and then
[04:24] we'll reward the positive signals. We'll
[04:27] p punish or penalize the negative
[04:29] signals and we'll create an RL loss
[04:32] function that we can back propagate on.
[04:34] We're still using back propagation.
[04:36] We're just no longer using cross
[04:37] entropy. So this is a where you are kind
[04:40] of like slide. Do remember we're going
[04:42] to show you examples of all of this in
[04:44] Excel. So you don't have to necessarily
[04:46] memorize everything.
[04:49] Great. So let's talk about RHF with
[04:51] human feedback. So RL reinforcement
[04:54] learning HF human feedback. That's kind
[04:57] of how in a way we started doing RL and
[05:01] large language models. Early on, we had
[05:04] samples of what good text looks like and
[05:07] samples of what bad text looks like for
[05:09] the same prompt. And then we told the
[05:12] model, hey, actually, I want you to
[05:14] learn from the good text and also learn
[05:16] how not to do the bad text. Great. So
[05:18] that's how RHF started back in 2022 in
[05:22] the instruct GPT paper. How do we what
[05:25] options do we have to give RHF data to
[05:29] our model to whatever RL pipeline looks
[05:32] like? So one option is we can ask people
[05:35] hey can you look at this response can
[05:36] you score it by scoring responses we
[05:39] could find scores for good responses
[05:41] scores for bad responses marry those
[05:43] together hopefully on the same prompt if
[05:46] hopefully so it's like dense and not
[05:48] sparse but you could also do sparse so
[05:50] it's on different prompts another option
[05:52] is you could get binary information that
[05:54] tends to be pretty sparse it's thumbs up
[05:57] thumbs down why is it sparse cuz you
[05:59] don't thumbs up and thumbs down the same
[06:01] prompt right you're only going to see
[06:02] one response and you're not going to
[06:04] necessarily have both positive and
[06:05] negative signals. You're going to have
[06:06] to like do some marrying of things
[06:08] together. Another option, this is going
[06:11] to be the most common option, is doing
[06:14] ranking, preferences, preference pairs,
[06:17] some would say, right? If I have X
[06:20] response and I have Y response, can you
[06:22] please tell me which one you prefer?
[06:24] That creates a preference pair. You
[06:27] could also do that in groups, but that's
[06:28] less common because the UIs that we've
[06:32] all gotten across them in sh GPT or
[06:34] whatever is, hey, here's two responses.
[06:37] Choose one of the two that creates a
[06:39] preference pair. So, let's look at a
[06:41] preference pair. Write five odd numbers
[06:44] with no E in them. You're giving
[06:46] response to a new version.
[06:49] And then you get two responses. You
[06:50] click, you choose one of them. That
[06:52] creates a preference pair, one positive,
[06:54] one negative. We can RL away from the
[06:57] negative. We can RL towards the
[06:59] positive. Really cool. I want us to take
[07:02] a moment and move away from the theory
[07:04] into what we can actually learn from
[07:06] this. Right? So, let's look at response
[07:09] number one. Uh it like what are you
[07:11] going to learn if I said that I
[07:13] preferred one of these responses over
[07:15] the other one? You only get one bit of
[07:16] data which which message I preferred,
[07:19] but there's a bunch of signal in here.
[07:21] Um, would you learn that it's better to
[07:23] have two list over one? Would you learn
[07:26] that it's better to use emojis? Would
[07:28] you learn that it's better to use bold?
[07:31] Would you learn that it's better to have
[07:33] uh formal conversations versus informal
[07:36] conversation? Would you prefer that
[07:38] there's uh better to have active verbs
[07:41] like let's versus here? Right? There's a
[07:44] lot that we can learn from this. But we
[07:46] have one bit of data. What what did
[07:49] Karpathy say about this? RL is like
[07:51] sucking supervision through a straw one
[07:53] bit at a time. The model only gets the
[07:56] one bit of which of the preference pairs
[07:58] was preferred and from it it has to
[08:00] learn exactly like how to perform in the
[08:03] next set of task. Not super easy. This
[08:05] is one of the big problems of RL. We're
[08:08] trying to learn a lot for like we're
[08:10] trying to learn multiple dimensions from
[08:13] one bit of data or a few bits of data.
[08:17] So, RLF architecture, you're we're not
[08:20] going to go over it, especially not the
[08:22] instruct GPT paper one was pretty
[08:24] complex. I'm I've got this slide here
[08:27] mostly to scare you. Mostly to show you
[08:30] that it was a pretty complex
[08:31] architecture when it first started out.
[08:33] So, I'm going to speak about it, but
[08:36] we're never going to review this.
[08:37] There's not going to be Excel
[08:38] spreadsheet. There's not going to be a
[08:39] code spreadsheet. This is just important
[08:41] for you to like have a general
[08:42] understanding of how complex it was.
[08:44] RLHF architecture on 2020 wasn't simple.
[08:47] Had several parts. One, it had an LLM we
[08:50] wanted to RL that kind of makes sense. I
[08:52] had my instruct tune model and I want to
[08:54] RL it. Two, I had train a totally
[08:57] separate model, right? That is a machine
[09:00] learning model on the RHF data to
[09:03] predict the outcomes of the text
[09:05] comparison, ranking, voting. So now I
[09:07] have a totally different machine
[09:08] learning model that looks at all of my
[09:10] RL data and knows how to predict uh the
[09:14] score, right? Then I have a why because
[09:17] I can't use that data in RL. I want to
[09:20] have the model generate stuff evolve
[09:23] generate stuff evolve and I want to rank
[09:24] it in between every one of these. I want
[09:26] to give it feedback in between every one
[09:28] of these.
[09:29] Then I want to have a copy of the LLM
[09:31] that gets changed to evaluate if pushed
[09:34] it too far or too little. So, I'm going
[09:36] to take a copy of what we call my
[09:38] offline RL model and then I'm going to
[09:42] have it have an online copy or a target
[09:45] copy that I can then triangulate the
[09:48] original model or the most recently or
[09:50] like a least changed model, an offline
[09:53] model. I have the online model that's
[09:55] changing all the time. And then I have
[09:57] my uh judge model that is trained on how
[10:01] to judge the outputs of these two
[10:02] models, right? And then RHF uses the
[10:05] output of both LLM, scores them for
[10:07] reward punishment, and uses that to move
[10:09] the online uh model along. Does that
[10:13] sound super complicated? Sounded super
[10:15] complicated to me when I learned it for
[10:16] the first time. When we started it, RLIF
[10:19] wasn't simple. Uh I want to mention this
[10:22] really great resource, the RHIF book
[10:25] from Nathan. Uh one, available for free,
[10:28] two has its own lecture series, three
[10:31] available to for purchase soon. Is it ju
[10:34] July already? I don't know. But it'll be
[10:36] available for purchase as a physical
[10:38] book really soon. So really really
[10:40] recommend reading that if you're
[10:42] interested in more information here. So
[10:44] I should mention that there's other data
[10:46] sources besides RLHF. RHF is often
[10:50] spoken in contrast to RLVR. What's RLVR?
[10:55] RLHF reinforcement learning from human
[10:58] feedback. RLVR reinforcement learning
[11:00] from verifiable rewards. What's an
[11:03] example of a re verifiable reward?
[11:07] You could say that code has a verifiable
[11:09] reward. Either the code runs and does
[11:11] what I want it to do or it doesn't. Math
[11:14] is a verifiable reward. Either the math
[11:16] proof proofs correctly and gets the
[11:19] right answer or it doesn't. Right? So,
[11:21] that's a verifiable reward. A slightly
[11:23] wider definition of RLVR which I've
[11:26] adopted but was so ashamed I didn't even
[11:28] write it down apparently is that any
[11:31] sort of multiplechoice question that has
[11:33] an answer key to me is RLVR right uh
[11:37] what is the history of Prussian war
[11:40] bismark whatever answer B answer B to me
[11:44] becomes a verifiable reward that is my
[11:46] definition of RLVR most people
[11:48] especially RL experts may disagree with
[11:51] me Great. So that's one source of uh RL
[11:55] that we can use. And on the left you can
[11:57] kind of see an illustration of hey we
[12:00] have RHF we have two answers. Response A
[12:03] the quick burn fox. Response B a swift
[12:05] Russet fox. The user thumbs up thumbs up
[12:08] that one. And the model learns from the
[12:10] ones that got thumbmed up and the ones
[12:12] that didn't get thumbmed up. So that's
[12:13] useful. RLVR on the other hand we have a
[12:16] programmatic verifier for X= 42. we go
[12:20] check if exit was actually 42 and not my
[12:23] version of RLVR
[12:25] you know uh we have legal documents and
[12:30] we do a quiz on them and like did you
[12:32] arrive at the right sentencing right as
[12:34] long as I know the answer key that to me
[12:36] is RLVR uh I do want to mention there's
[12:39] another RL source that's not often
[12:42] discussed but is honestly probably the
[12:44] most common one at this point which is
[12:47] modern LLMs can just generate
[12:50] preferences used in RL, right? So, uh I
[12:54] can have an a large language model
[12:56] generate a bunch of a chosen rejected
[12:59] pairs and then that could help us train
[13:02] a teacher that acts as LLM as judge. Um
[13:05] another source is I could take a bunch
[13:07] of um let's say reasoning traces from
[13:11] claude. Let's say that's one of the top
[13:13] data sets in hugging face right now. I
[13:15] could train an LLM as judge that that
[13:17] can be used in RL to score answers from
[13:19] a model. Right? That's another great
[13:21] example of RL using distillation.
[13:25] So now I want to show you policy
[13:28] optimization. That's the magic between
[13:30] behind RL. And I will say ahead of time
[13:32] that we're not going to go into into
[13:34] depth on this because again this is its
[13:36] own like full day workshop and what is
[13:38] RL? How do you implement it? But I will
[13:41] mention that every RL function has one
[13:45] thing in common. It's the update rule.
[13:47] What's the update rule? It's on the top
[13:50] right that you can see in front of you.
[13:52] It's new policy equals old policy plus
[13:56] the learning rate. We know what learning
[13:57] rates are. And the objective. Okay. So
[14:00] that's kind of sensible. We're going to
[14:01] just update the old policy with a small
[14:04] modifier. What's an objective? Again,
[14:07] listen, this is why I don't want to
[14:08] necessarily teach you RL. I'm I just
[14:10] exit the deck. This is what an update
[14:13] objective is. I would have to explain
[14:15] quite a lot here. Uh what what is the uh
[14:19] what's a trajectory? What are
[14:21] probabilities? How do we estimate
[14:24] outcomes? I don't think that's like a
[14:26] good use of two hours of your time right
[14:29] now. That's again its own two-day
[14:30] workshop. But now taking a step back
[14:33] from that, we did maybe learn a little
[14:35] bit. We learned the word trajectory. So
[14:37] let's think about this in R and I'm just
[14:40] going to read the slides. In RL we've
[14:42] changed the loss function from cross
[14:44] entropy to fun math about reward and
[14:46] punishment. Interesting. PO policy
[14:50] optimization is that math. It's the
[14:53] thing that helps us generate a loss
[14:55] function that makes sense given our
[14:56] data. So PO has to walk the entirety of
[14:59] the loss landscape. Let's think about
[15:02] the loss landscape. We're back into
[15:03] section seven. Let's say I got answer A
[15:06] is a good answer and answer B is a bad
[15:08] answer. We sum up all of the tokens in
[15:11] every one of these answers. And we can
[15:14] kind of have the RL algorithm walk that
[15:17] landscape from B to A using that as
[15:19] information. Okay, so that was like a
[15:21] bit of a metaphorical answer. Let's pull
[15:24] back for a moment. There are hundreds of
[15:26] these PO optimization methods discussed
[15:29] in the literature. I think hundreds
[15:31] might actually be an underestimate, not
[15:32] an overestimate. So most commonly used
[15:35] in large language models, DPO, GP, GRPO,
[15:39] PO those are I think the most commonly
[15:42] used ones or at least commonly discussed
[15:44] one. Doctor GRPO to fix GRPO, RPO, APO,
[15:48] IPO, KT, right? This list keeps going
[15:51] pretty much endlessly. So again, full
[15:55] day workshop. We don't have to discuss
[15:57] all of them. We are going to discuss
[15:59] one. I think that's like the minimum
[16:00] that I was willing to do for this
[16:02] workshop. I wasn't willing to have it do
[16:04] a hand wavy. We're going to do simple.
[16:06] Simple PO. The simplest version of a PO
[16:10] that I think is acceptable. It's called
[16:12] simple and that's the one I want to
[16:14] implement here with you. So, let's do an
[16:16] example of how simple works. I've got
[16:18] this um not super visually attractive
[16:22] chart on the left side and I want us to
[16:24] think about it together. So, let's say
[16:25] that I asked the model, what is 15% of
[16:28] 240? And it answers with two answers.
[16:31] one one good one, one bad one. The good
[16:34] one says.15 * 40 = 36. The other one
[16:38] says 240 / 15 = 16. One of these is the
[16:42] verifiably wrong, some would say, right?
[16:45] So, we already like kind of know which
[16:47] one is the good one and which one is the
[16:48] bad one.
[16:50] Um, we can then stitch those together.
[16:53] So, we stitch the prompt alongside with
[16:56] the uh positive answer. with a rewarded
[16:59] answer that shows an answer and we could
[17:02] stitch the prompt together with a
[17:04] rejected answer. So we give that to
[17:06] enlarged language model. We have it,
[17:08] hey, can you score every one of the next
[17:11] token predictions? So in this sentence,
[17:13] what is 15% of 240 2.15 multiplied by
[17:17] 240 equals 36. What we see is there's a
[17:20] bunch of tokens. I'm going to ask it to
[17:22] score every token for the next token
[17:24] prediction, right? I'm going to do the
[17:27] same for the negative tokens and I'm
[17:29] going to punish all of the tokens in the
[17:31] negative path and I'm going to reward
[17:33] all of the tokens in the positive path.
[17:35] So, because I'm punishing the prompt
[17:37] pretty much equally, then that's totally
[17:40] fine. It's just not really going to
[17:42] change, right? Like, it'll cancel itself
[17:44] out. But the parts that makes sense to
[17:46] reward will reward and the parts that
[17:48] don't make sense to reward will punish.
[17:50] So, we'll add the sum of all of these
[17:53] tokens. will average them out because we
[17:57] need to like get a single number in loss
[17:59] function. Then we run it through a log
[18:02] sigmoid multiplied by a a negative log
[18:05] sigmoid multiplied by hyperparameters
[18:08] plus a hyperparameter. The important
[18:10] part is we take the punishment we we
[18:12] negate the reward from it and that's
[18:15] going to become our loss function. Okay.
[18:17] And we we always know that because we're
[18:19] doing that to like loss minus positive,
[18:22] then we know the value will end up being
[18:24] positive for the loss function. Okay, so
[18:26] that was really confusing. Justin, I
[18:29] need to see an example. I'm not going to
[18:31] be able to remember this. Great. So
[18:33] what's our example? Let's do simple
[18:35] together. Simpo the simplest PO
[18:37] optimization we could do. So feed
[18:40] forward and pre pre-training. I this is
[18:43] just a to remind you. We have text. We
[18:46] tokenized it. We ran it through a
[18:48] transformer. We got a bunch of in output
[18:51] tokens, but now we don't have the uh
[18:54] first token. We always drop the prefix,
[18:56] especially during pre-training. But now
[18:58] it predicts token number 15, which ends
[19:01] up being fox. The brown dog jumped over
[19:03] the lazy 15th fox. Awesome. So we
[19:06] expected the probability for fox at8.
[19:10] The actual transformer output for it was
[19:12] 6. And then we can calculate some sort
[19:15] of loss as a result of that discrepancy.
[19:17] We can calculate some sort of loss as a
[19:20] result of the fact that there maybe were
[19:21] other options besides fox. So that's how
[19:24] and then we back propagate based on
[19:25] that. Right? So that's how all back
[19:28] propagation and loss functions and
[19:30] pre-training works. That's stuff we've
[19:33] already seen. Now let's say I have
[19:35] multiples here. Let's say I have the
[19:38] correct answer the brown tokens 15 and
[19:41] 97. I can run it through my transformer
[19:44] tokenize it. Each of these has its own
[19:46] probabilities. I can uh sum that up,
[19:50] right?
[19:51] And then I'll have the decoded tokeniz
[19:54] as well. And then that goes into a loss
[19:57] function. I can have a wrong answer
[19:59] instead of the brown. This shouldn't be
[20:01] the same text. The gold
[20:07] uh the gold for example. uh
[20:12] goes into the transformer generates a
[20:14] bunch of probabilities
[20:16] that goes into the loss function as a
[20:18] bad example. Hello world super
[20:21] irrelevant he gets tokenized goes into
[20:24] the transformer gets tok we have
[20:26] tokenized output now it's like 87 here
[20:30] are the probabilities of each of these
[20:32] we sum these up and we send it into the
[20:35] loss function the loss function looks at
[20:37] all these uh token probabilities and
[20:41] says I know these are wrong I know these
[20:42] are good I'm going to treat them a bit
[20:44] differently but overall I'm summing
[20:46] everything together and I'm going to
[20:48] perform
[20:49] policy optimization. So we replace cross
[20:52] entropy with fun po math that ends up uh
[20:56] that ends up replacing cross entropy for
[20:59] back propagation.
[21:01] Great. So let's look at some formulas
[21:03] for simple. We haven't seen the formulas
[21:05] thus far. So this is the formal proof.
[21:07] Uh this is the formal formula of it. You
[21:10] could kind of read it here. It's not
[21:12] super immediately to me understandable.
[21:16] Great. So let's look at a slightly more
[21:18] human readable version. So the loss
[21:20] function for simple is minus log sigmoid
[21:23] of the reward margin.
[21:26] Okay. So we can maybe explain why log
[21:28] maybe y sigmoid maybe y minus. We can
[21:32] all have those conversations. But then
[21:33] we can see there's a thing in there
[21:34] that's called reward margin. So
[21:36] basically I'm just executing a little
[21:37] bit of math and then I go get to this
[21:39] thing called reward margin. What is the
[21:42] reward margin?
[21:44] It's the chosen reward. the good answer
[21:47] minus the rejected reward, the bad
[21:50] answer, right? And then you multiply
[21:52] that bit with a constant called beta and
[21:54] you uh subtract gamma which is another
[21:57] constant or hyperparameter.
[22:00] How do you calculate chosen reward?
[22:02] Remember we're generating multiple
[22:04] tokens. So we have to take all the
[22:06] tokens. We log the token and we average
[22:09] it for both the chosen reward and the
[22:11] rejected reward. Chosen good, rejected
[22:13] bad. rejected posit probabilities get
[22:17] logged each probability and then we
[22:19] average it. Chosen probability for each
[22:21] token gets log and then averaged. Great.
[22:25] So now we kind of understand this
[22:26] formula. We'll see it in action. Don't
[22:28] worry. This is just the first time we're
[22:30] seeing the pro the formula. So let's
[22:32] look at simple. Let's say that I have
[22:34] what is 15% of 240. The example we saw
[22:36] in the slide deck chosen 15 * 40 = 36.
[22:40] Rejected 214id 15 16. Right? That's just
[22:44] not the right answer. So this is my
[22:46] chosen pair and this is my rejected
[22:48] pair. When I combine the prompt with the
[22:50] rejected answer and the chosen answer
[22:53] with the next set of token predictions
[22:55] out of the model,
[22:57] I'm going to run that through the
[22:59] transformer and I'm going to get a bunch
[23:01] of tokens and a bunch of probabilities.
[23:03] What's the thing to notice here is that
[23:05] the output
[23:08] for uh the transformer is going to look
[23:11] roughly the same for the first couple of
[23:13] tokens, right? But then it's going to be
[23:15] different for the ending. So that's kind
[23:17] of intentional. I kind of wanted you to
[23:18] see that the probabilities are still
[23:20] there for the prompt. Great. So we have
[23:22] different probabilities for the
[23:24] rejecteds and different probabilities
[23:26] for the chosen. Awesome.
[23:30] After this uh we can calculate the
[23:33] chosen reward and the rejected reward.
[23:36] Just going to zoom in a bit to make it
[23:37] easier to read. Choose chosen reward has
[23:41] uh the probabilities from up here.
[23:43] Remember we just copied them. Rejected
[23:46] probabilities have these probabilities.
[23:48] How do we convert these into something
[23:50] that we can use in RL? First we have to
[23:53] uh average them. We log them so on. So,
[23:56] I already have that pre-typed here, but
[23:59] I'm going to do it in front of you. Oh
[24:00] my goodness. It takes every probability,
[24:03] logs it, and then averages it. Same we
[24:08] can do for our chosen probability, not
[24:09] just a reject probabilities. Now, we
[24:11] have two probabilities overall. I
[24:14] represent my probabilities here on um on
[24:18] on a certain base. So, I use the ln
[24:20] function. Great. So, now we have the
[24:22] chosen reward and the rejected reward.
[24:25] all of the the the average log of every
[24:29] token probability in the negative path.
[24:32] The average log of every token in the
[24:34] positive path. Reward margin is chosen
[24:37] reward minus rejected reward multiplied
[24:40] by beta some sort of hyperparameter
[24:42] minus gamma. So I have beta
[24:45] hyperparameter here. I have gamma
[24:47] hyperparameter here. What is going to be
[24:49] my reward margin? I'm gonna go chosen
[24:51] reward
[24:54] minus rejected reward multiplied by beta
[25:00] multiplied by beta minus gamma
[25:05] and that's my reward margin. Okay, so
[25:08] what do I do with my reward margin?
[25:10] Minus log sigmoid reward margin. Okay,
[25:14] so I've already pre-typed up the sigmoid
[25:17] here. I didn't want you to see me like
[25:18] struggle typing in the sigmoid
[25:20] activation function.
[25:24] Then I'll do minus log
[25:29] 2.83.
[25:31] That's my loss function from simple. And
[25:33] then I could go ahead and back propagate
[25:35] that to the transformer. Right? 2.83
[25:38] kind of high loss. Not super low, not
[25:40] super high. Great. So now we saw an
[25:43] example of me changing the loss function
[25:47] from uh using cross entropy right which
[25:52] is what we were using here to an RL loss
[25:55] function. Then we actually did the math
[25:57] on at least a small RL loss function.
[25:59] Some would say the simplest of the the
[26:02] the the
[26:03] policy optimizations. And then you could
[26:06] see we're doing back propagation off
[26:08] that fun math.
[26:10] going back into the into the deck. So,
[26:13] we just saw an example of a real PO
[26:16] algorithm that we can use to do RL on. I
[26:21] do want to mention that there's like
[26:22] again a whole day class. We're not
[26:24] teaching you on RL from simple. We could
[26:26] just add more and more features until we
[26:28] get all other kinds of RLish,
[26:31] right?
[26:32] simple. If you add a reference model
[26:35] frozen copy, you're basically a DPO at
[26:37] that point, which is a real RLPO
[26:41] strategy people really use in production
[26:43] to like RL models, you could get to
[26:46] rejuction sampling. If you add a couple
[26:49] more, you add a couple more things like
[26:51] KL penalty, which helps us make sure we
[26:53] don't move too far in one direction. We
[26:55] could get GRPO
[26:58] uh for that. Unfortunately, GRPO also
[27:00] requires you have custom inference
[27:01] engines because of how it works because
[27:04] this is some something about movies and
[27:05] so on. PO most complicated thing to
[27:10] implement. Lots of things to do. Um
[27:12] Stanford professor once joked that like
[27:14] I'm not going to like make you implement
[27:16] PO. That's going to make it very very
[27:19] like like this just like a hazing ritual
[27:21] for RL. But you could choose to do that.
[27:24] So that's on the left. That's you could
[27:26] just add more and more and more stuff
[27:28] and get better and more complicated
[27:30] forms of PO uh from simple
[27:33] sorry on the right you could see uh the
[27:36] RL cheat sheet from Nate's book policy
[27:39] gradient okay that's the formula that I
[27:41] kind of hid from you reinforce that's
[27:44] another form of PO that I think is
[27:46] really great and maybe should be should
[27:48] have been the example that we teach in
[27:50] this workshop it's got like a little bit
[27:52] more it's got a value model it's got a
[27:54] like a couple more things going on with
[27:56] it. Uh then you have the formula for PO,
[27:59] then the formula for GRPO, then the
[28:02] formula for clip important sampling,
[28:04] then the Bradley T model, and finally
[28:06] the DP DPO. Each of them is a bit
[28:09] different, but worth like having an like
[28:11] having a look at and trying to
[28:12] understand them. Really recommend Nate's
[28:14] book on the topic.
[28:17] RL data sources, who authors them. So
[28:19] now we're going to shift a bit from
[28:20] where what how we do RL to where we get
[28:23] RL data from. So we're no longer just
[28:26] collecting our own data. I guess if
[28:28] you're open AI or anthropic, you're
[28:31] still collecting your own data, but the
[28:33] rest of us are just going to use data
[28:34] sets from hugging face. So RHF, right?
[28:38] So that's the thing we remember. We have
[28:41] a couple of options for where to get
[28:43] data from. RHF preferences are available
[28:46] like you could go to anthropic HH RHF.
[28:48] You can get 150 pairs on healthfulness
[28:51] and harmlessness. Additionally, or you
[28:53] could go to open assistant 2, get 150k
[28:56] ranked messages, pairs of preferences.
[28:59] Rank has its own uh number. Uh Stanford
[29:04] SHP2 has 5 million pairs of Reddit
[29:07] derived domain preferences. So it's
[29:09] going to show you it's they generated a
[29:11] bunch of preferences from Reddit in
[29:14] opposition to RHF which we said is a
[29:16] thing that we used to do in 2022 2023
[29:19] really RL a A R L A IF reinforcement
[29:24] learning from AI preferences that's
[29:27] really where we're going to get most of
[29:28] our RL data from at this point. So,
[29:30] Ultra Feedback has 50,000 prompts
[29:33] generated with GPT4
[29:35] uh and they have four answers and you
[29:37] just have to choose the right one.
[29:39] Berkeley Nectar has uh 200,000 uh ranked
[29:43] prompts to a total of 4 million pairs,
[29:45] right?
[29:47] Uh I did want to throw in a mention for
[29:50] constitutional AI because constitutional
[29:53] AI is effectively someone writes a
[29:56] constitution probably anthropic then
[29:58] they generate a bunch of RL preference
[30:00] pairs from it and then that's how they
[30:03] train the model from a constitution.
[30:05] That brings us nicely into safety. Uh in
[30:08] safety we we really do use RL a lot for
[30:11] safety. So we can we have the data sets
[30:13] that have pairs of harm helpfulness and
[30:16] harmlessness. Uh has a bunch of pairs in
[30:19] different harm categories and have a
[30:22] bunch of RL examples on behaviors of
[30:25] self refu safe refusal.
[30:28] So we talked about RHF and its new
[30:30] friend that's probably going to totally
[30:32] s surf.
[30:36] We also have RLVR. What's examples of
[30:38] RLVR? RLVR code.
[30:42] We have code competition problems with
[30:45] unit test. The unit test make it
[30:47] verifiable. We have large scale code
[30:50] test with unit test which make it
[30:52] verifiable. We have 500,000 code
[30:55] problems with unit test which make it
[30:56] verifiable. Right? You have to ask
[30:58] yourself how is it verifiable if you
[31:00] don't have unit tests. If all you have
[31:02] is a good uh example. Uh there's ways of
[31:05] doing that. Obviously you can train a
[31:07] referee model LLM is judge which will
[31:09] then be providing those values. Another
[31:12] option is RLVR is math. So GSM8K we've
[31:16] seen it before. It's grade school math
[31:18] problems with answers. So because it has
[31:20] answers clear demonstrable num numerical
[31:23] answers that becomes verifiable.
[31:25] Similarly we can we have 30y highest
[31:28] level math Olympics problems. Again they
[31:31] have an answer. I think they also have a
[31:33] verifier for like the proof and then uh
[31:37] Numina Math has a million math
[31:39] competition questions with coot answers
[31:42] chain of thought answers.
[31:44] Additionally, we have the option of
[31:46] doing RLVR and literally anything that
[31:49] we have an answer key on. So for
[31:50] example, RLVR if instruction following
[31:54] instruction following oh my god can
[31:56] become RL. We change the
[32:00] loss function from cross entropy to PO
[32:05] and then we can use RL to do instruction
[32:08] following as long as we have good
[32:10] options and bad options, chosen options
[32:12] and rejected options. Toolbench shows us
[32:15] 100,000 trajectories of tool use. Really
[32:18] great so that we can use like good
[32:21] examples here. Web arena shows how to
[32:24] 100,000 sorry it's a thousand agentic
[32:27] task to build realistic websites right
[32:29] good websites that end up getting built
[32:32] so we could use that to train on an LLM
[32:35] is judge to then be able to do RL on
[32:39] let's make a couple of decisions for our
[32:42] pre-trained model for our instru model
[32:45] number one is we'll have a separate
[32:47] script to RL instruct tune model two
[32:50] what kind of RL are we going to do we'll
[32:52] do simple, right? Because that's the
[32:54] only one we know how to do. We don't
[32:55] know how to do DPO or PO or reinforce.
[32:58] We don't know any of those.
[33:00] And then we're going to do that on
[33:02] balanced copa. Just as a reminder,
[33:03] balance copa. Common sense. They cut the
[33:06] grass because the grass was too too
[33:09] long. Not they cut the grass because the
[33:12] woman missed her friend. That doesn't
[33:14] make sense. Eval benchmarks. We're going
[33:17] to run uh balance scope on uh all 500
[33:20] tests every 100 steps cuz we really want
[33:22] to see it get better. And then uh
[33:25] obviously that one will run for test. So
[33:28] there's a separation between training
[33:29] data in balance copa and test data in
[33:32] balance copa. And then we'll run no more
[33:34] than 4,000 steps to try and avoid
[33:37] catastrophic forgetting. Hyperparameter
[33:40] will run it for no more than four epics
[33:42] because there's only a,000 training
[33:44] examples. That'll be a total of 4,000
[33:46] steps. So, a thousand steps times four,
[33:49] 4,000. What does that look like when we
[33:51] build that script? The what are the
[33:53] result? Simple loss declines over 4,000
[33:56] steps overall while copa accuracy
[33:58] improves. Really great. We've been able
[34:01] to teach the model to be more common
[34:04] sensical. Love it.
[34:07] Um, and here you could see balance copa
[34:10] accuracy improving after about 2,000
[34:13] steps.
[34:14] So let's make a couple of more
[34:16] decisions. This slide is meant for AI
[34:18] coding assistant. Um number one, we'll
[34:21] use an optimizer of AdamW fused, right?
[34:24] So like we need an we still need an
[34:26] optimizer. We haven't really changed
[34:28] that from uh from back propagation.
[34:32] Hyperparameter will run batch size of
[34:34] one. Why? This is just a very simple
[34:37] optimization to do like this is a
[34:40] trivial RL feature. Copa formatting will
[34:43] be something like fu because bar. Um so
[34:46] we cut the grass because the grass was
[34:49] too long and we'll just to show two
[34:51] options and the results we should have
[34:53] random pre-train instruct tuning eval
[34:56] every 100 parameters. We should be able
[34:58] to see that and then we want to include
[34:59] a chart for pair pair accuracy tracking.
[35:03] So how do we do that? One option is you
[35:06] can ask you can write this code
[35:07] yourself. I believe in your ability to
[35:09] do that. That's not a big difference
[35:11] from our pre-training script. We load
[35:13] those weights, we change a couple, we
[35:14] change the function, we now know the
[35:16] math. So, that's an option. I don't
[35:18] think a lot of people do that. Another
[35:20] option is to have an AI coding assistant
[35:22] take this deck, the pre-training, the
[35:25] pre-training script, the instruct tuning
[35:28] script, and say, "Hey, can you please
[35:30] build the RL script for me?" So, let's
[35:32] say that that's an option. Also, we
[35:35] could use go Justin Angel AI/ Lego,
[35:39] which we've been building all along. It
[35:40] knows my activation function and my GPU
[35:43] and my FFN and so on. And then I could
[35:45] say, hey, can you build the RL script
[35:48] for me for epox? Uh, this is the
[35:50] optimizer. Here's how you format Copa.
[35:52] Here's the benchmark so on. It's already
[35:55] pre-built here. You copy this into
[35:57] claude or JGPT or Gemini or whatever and
[36:00] it can generate you these scripts. So
[36:03] when I do any of those options, let's
[36:05] look at a quick script that we can learn
[36:07] from. So we have our configuration. This
[36:12] is our simple config. Beta, gamma,
[36:15] learning rate, number of epics, eval
[36:17] xsteps, maximum grade norm. So gra
[36:20] gradient clipping.
[36:22] Um then we have the rest of our
[36:24] architecture for our GPT2 model. Again,
[36:26] rel square kind of messes us up because
[36:29] we have to always keep declaring it in
[36:30] every script because it's so atypical.
[36:34] And then simple. So we have the simple
[36:36] formula which we learned in Excel. And
[36:38] then we have the implicit reward length
[36:41] normalized log probability explanation
[36:44] here. So simple lost chosen input chosen
[36:47] target rejected input rejected target.
[36:51] We calculate the logits for each one of
[36:54] the chosen inputs and rejected inputs.
[36:57] We length normalize it minus sigmoid,
[37:00] right? Remember we let we normalize it.
[37:03] Beta time multiply by chosen reward
[37:05] minus rejected reward minus gamma. This
[37:08] is the stuff that we did in uh Excel. F
[37:12] of log negative f log sigmoid of the
[37:16] reward margin. This is exactly the code
[37:18] that we had in Excel.
[37:20] And then we return that value. For
[37:23] evaluation, we just implemented balance
[37:25] copa. Again, we should never really be
[37:26] implementing our own our own test
[37:29] harnesses. We should allow uh another
[37:32] framework that's already implemented to
[37:33] do that. It's just going to be more
[37:34] consistent, but I wanted to have a
[37:36] self-contained script. We load the data
[37:38] for balanced uh for balanced copa. It's
[37:42] called balanced, by the way, because
[37:43] there's equal amounts of A and B. uh we
[37:46] load the training data and we also load
[37:48] the test data. So 1,000 examples for
[37:51] training, 500 examples for test
[37:55] uh and it says so right here. And then
[37:57] we run a training loop. What's fun about
[37:59] this training loop? It's got W. It's
[38:01] running epox. It's doing zero grad. It's
[38:04] doing backward. It does steps. It does
[38:07] clip norms. What's the really
[38:09] interesting thing about it? It's because
[38:11] it's going to do loss function, not
[38:13] cross entropy. Notice there's no cross
[38:15] entropy anymore. It's going to do cross
[38:17] entropy on the simple loss. So it takes
[38:21] in the chosen tokens, the rejected
[38:23] tokens, the pre like beta, gamma, all of
[38:26] that and then it calculates the simple
[38:28] loss function. So our and then we do
[38:31] back propagation based on it.
[38:34] Great. So let's run that. We ran that.
[38:37] Here we go. Step 50, step 100, so on.
[38:40] Let's try and look at the chart
[38:42] together. Let's look at what. So our
[38:44] random baseline for balance scopa would
[38:46] be 50%, it's A or B. Our pre-trained
[38:49] model performed at 55% so slightly above
[38:53] random. That's great. Instruct tuned
[38:55] performed at 56% so slightly better. The
[38:58] instruction tuning did help a bit. But
[39:01] then once we do 4,000 steps now our uh
[39:04] and again we're not checking the we're
[39:06] training on the trained set, we're
[39:08] testing on the test set. The test set
[39:10] performance improved to 60%. Very cool
[39:14] to notice that. Very cool to notice
[39:16] that. We could plot that all out in a
[39:18] graph. You can see balance copy accuracy
[39:21] did increase. Simple loss decreased. And
[39:24] the average reward margin, right? The
[39:26] margin between the rejected and the
[39:29] chosen is increasing. That's what we
[39:32] want. Great. So that was RL.
[39:36] And with that, I want to like recommend
[39:38] a couple of RL resources. RL can easily
[39:41] be a full day workshop as I think I've
[39:43] apologized for like five times already.
[39:46] One thing that you can watch if you only
[39:48] have an hour, I really love this intro
[39:50] from Professor Tom Yay. I think he only
[39:52] recorded this less than a month ago.
[39:54] Really worth watching, he goes over PO,
[39:56] DPO, GRPO in kind of an Excel way like I
[39:59] do. Another option is you could read the
[40:02] rlfbook.com
[40:03] from um Nathan. You could also buy the
[40:07] physical book. I think it's going to be
[40:08] out in July. I will mention that I found
[40:11] that a bit mathy for me. I'm not really
[40:14] a mathy kind of guy. So worth reading it
[40:16] with a mathy lens. Or you could read
[40:19] RLVR book from Ken. I actually thought
[40:22] it was really lovely and it was very
[40:24] code forward. It's like lots of code
[40:26] sample code by code by code. So, however
[40:28] you learn best, you have two resources.
[40:30] Now,
[40:32] additionally, I think it's worth
[40:33] mentioning that there's a bunch of open
[40:35] source models that there's a lot to
[40:36] learn from on how to do RLO 3. Almo is
[40:40] Nate Nathan's open source model. Really
[40:42] worth noticing that it probably have
[40:45] went as deep on RL as anyone has gone
[40:47] on. Uh we have the DeepSik paper here.
[40:51] They really did innovate as well. We
[40:53] have the Quen 3 model and GLM5. Each of
[40:56] these have added a lot into RL and have
[40:59] like very interesting tidbits here.
[41:01] Which model didn't I mention? For
[41:03] example, AR R key trinity. Why didn't I
[41:06] mention it as a resource for RL? They
[41:08] have this. I can't even remember the
[41:10] number. I think it's like a trillion
[41:12] parameters or something. Almost no RL
[41:15] few thousand runs of RL. I'm guessing on
[41:18] safety and that's it. Right. They've
[41:20] done as much RL in that model as I ran
[41:23] on simple for my tiny model. So why is
[41:26] that important? That model performs
[41:28] super well on many things, right? It's
[41:30] not state-of-the-art, but it's not super
[41:32] far behind.
[41:34] It kind of brings into question why we
[41:36] even need RL. And I think that's an open
[41:38] discussion that we won't know the answer
[41:40] for in mid26.
[41:43] After this, we finished covering RL. We
[41:48] finished covering instruction tuning. We
[41:50] finished covering pre-training,
[41:51] post-training, we've covered
[41:53] architecture. There's a bunch of stuff
[41:55] we didn't cover. So hopefully you could
[41:57] join me for another five minutes where
[41:59] we kind of maybe cover the stuff we
[42:01] didn't cover. At least you know what you
[42:02] don't know at the end of this. Thank you
[42:04] so much and I hope you could join me for
[42:06] another few minutes at the for our last
[42:08] section together. Thank you so much.
