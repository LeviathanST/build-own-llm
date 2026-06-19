# SoftMax | Build Your Own LLM Workshop #14

**Build Your Own LLM Workshop — Video #14 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 20m 13s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=H2yV3jd4DKg |

## Description

No description available.

---

## Full Transcript

[00:00] Welcome back everyone. We're going to be
[00:02] chatting about softmax today where we
[00:04] left off. We were looking at all of the
[00:06] fun regularization techniques. This is
[00:09] going to be our last deep neural network
[00:11] technique that is applicable to large
[00:13] language models but not specific to
[00:15] them. So last time we looked at
[00:17] regularization, normalization so on. And
[00:20] now we're going to be looking at
[00:21] softmax. Why is it the last thing we're
[00:23] going to look at? Well, it's the last
[00:25] thing that happens within a neural
[00:27] network before we can use it to predict
[00:30] the next word. Specifically, it happens
[00:33] at the end when we convert logits to
[00:36] probabilities. So, what is a logit? What
[00:38] is probabilities? Let's try and
[00:40] remember. So, what problem is softmax
[00:42] going to solve? We have our like deep
[00:44] neural network here on the right. At the
[00:46] end of it, we get a bunch of logits.
[00:49] What are logits? logic are just
[00:51] activations that we just stop processing
[00:54] the network with. It is the output of
[00:56] the network but realistically we go math
[00:58] mall math mall
[01:01] right and at some point we stop and we
[01:03] call that logits. So that's just a fun
[01:05] way of saying uh activations at the end
[01:08] of a network. What's an important
[01:10] attribute of logits? Well, they tend to
[01:12] be between that minus4 and four range
[01:14] that we mentioned earlier. Why are they
[01:16] in that range? Well, that's because that
[01:19] hopefully if gradients didn't vanish or
[01:21] explode and training didn't collapse,
[01:24] often times they're going to be grouped
[01:25] around minus4 and four. That's not
[01:28] actually true by the way for GPT2. But
[01:30] it's a good place for us to be
[01:32] aspirationally at. Great. So, how do we
[01:35] take logits, which are just activations,
[01:38] and convert them to probabilities? And
[01:40] first, let's think about why we need
[01:42] probabilities. Remember, we we looked at
[01:44] this in section one. We looked at
[01:46] temperature and top K and top P, right?
[01:50] We need need to apply our selection on
[01:53] probabilities and not just like whatever
[01:55] random output activations we're going to
[01:57] get, not random, but like random to us
[01:59] humans. So what do we get from a
[02:02] network? Let's say that we have our deep
[02:03] neural network that does a multiplied by
[02:05] b modulus c, right? Let's say we do 10
[02:09] multiplied by 15 modulus 8. we expect it
[02:12] to say something like one or two or
[02:15] three. What we actually get is 3.5.8
[02:19] 0.05
[02:21] minus 9.8. Right? These numbers don't
[02:24] really make a lot of sense to us. I was
[02:26] just looking for an answer between 0 and
[02:28] 19. I'm not super clear how we even have
[02:30] negative numbers here. Ne numbers
[02:32] outside of that range and so on. So
[02:34] softax is going to be the thing that
[02:36] does that conversion between
[02:40] logits and probabilities.
[02:43] So the easiest way for us to take a
[02:45] bunch of numbers and convert it to
[02:47] probabilities pretty obvious in my mind.
[02:50] We're just going to sum those up and
[02:52] divide by the sum. Uh there are other
[02:54] ways to do that. For example, uh we've
[02:57] seen earlier examples where we used
[03:00] other methodologies to do that in but
[03:03] we're not going to do that now. What
[03:04] we're going to do now is we're going to
[03:06] just sum up things together. So what's
[03:09] the first problem in summing up things
[03:10] together and dividing each element in an
[03:12] array with what we just saw? We have a
[03:14] bunch of negative values in this array.
[03:17] So if we end up summing stuff up, the
[03:20] positive values and the negative values
[03:21] are going to cancel them out and we're
[03:22] going to lose a bunch of signals. Okay,
[03:25] so that's a problem. When we're doing
[03:26] linear ratios, we're going to probably
[03:27] have to baseline the minimum or
[03:29] something. Another problem is we kept
[03:32] talking about back propagation. You
[03:33] don't have to understand calculus. It's
[03:35] just a bunch of derivatives. Well, doing
[03:37] a bunch of derivatives to something that
[03:39] just sums up and divide by the sum. Not
[03:42] as clean as doing something else. What
[03:44] that something else might be? Soft max
[03:47] because it just it has better
[03:49] derivatives. Another problem that we
[03:51] have is dividing by the sum of all items
[03:54] of all the logits is going to give us a
[03:57] linear ratio which is why I call this
[03:58] linear ratio probabilities. Maybe that's
[04:00] just the name I give it. Um but that's
[04:04] going to give us linear ratio
[04:05] probabilities where all the
[04:06] probabilities are equally kind of the
[04:08] same based on their number. I don't
[04:10] necessarily know if that's what we want.
[04:12] We want to just choose one word at the
[04:14] end. It'd be great if this step could
[04:16] help make the differences bigger and uh
[04:20] reduce the and flatten out the
[04:22] differences amongst the least likely
[04:24] possibilities. Okay, so how could we do
[04:26] that? Probably using softmax. So linear
[04:29] probabilities have this these set of
[04:31] three problems. We can't sum up easily
[04:34] negative and positive numbers unless we
[04:36] do something like increase their
[04:37] magnitude to the minimum which is also
[04:40] going to like distort how we do summing.
[04:42] uh it's not great for tricky calculus
[04:45] for back propagation. And do we really
[04:47] even want a linear ratio? I'm going to
[04:49] contend that we don't. Okay, so let's
[04:51] get to the softest max.
[04:54] And here you've got this beautiful photo
[04:56] of Teddy Bear from Josh Josh from Stath
[05:00] Quest. When he introduces soft max, he
[05:03] shows you a photo of this bear and says,
[05:05] "Sh, the softest Max." Right? He also
[05:09] introduces Arg max by saying Argax uh
[05:13] and shows you a pirate flag. Really love
[05:15] his channel. You should check it out.
[05:16] You should check out the video on
[05:17] softmax if you want more information. So
[05:20] how is softmax different than just
[05:21] summing up the sum of items and then
[05:23] dividing by it? Well, the nice thing is
[05:26] it uses exponent. What's exponent? I
[05:28] told you that you don't have to know
[05:30] math for this workshop, but actually you
[05:34] do need to know about exponents. So
[05:35] let's try and introduce exponents. We
[05:37] also saw exponents earlier in functions
[05:39] like sigmoid and right but we're not
[05:41] going to necessarily we didn't really
[05:43] cover it back then so now we're going to
[05:44] cover it. An exponent behaves the way
[05:47] that you see on the bottom left of your
[05:49] screen, right? It has uh it uh a curve
[05:53] that's a negative values really really
[05:55] close to zero astoically aspiring to be
[05:59] zero and then above negative numbers it
[06:02] is some would say exponentially really
[06:05] really high. So the larger the number
[06:08] one could say it's exponentially higher.
[06:11] So by using exponents we push down
[06:13] smaller values further down and we
[06:16] increase larger numbers which is
[06:19] ultimately really better for
[06:20] probabilities. Great. So now you know
[06:23] about exponents. You know they how they
[06:25] work with small numbers, how they work
[06:27] with really large numbers. They make
[06:29] large numbers larger.
[06:31] What is softmax? It's taking the
[06:33] exponent of the logit or our input and
[06:36] then dividing it by the sum of all
[06:38] exponents and that's it. So we basically
[06:40] are linear ratio but without having to
[06:43] do minimum handling and like negative
[06:45] numbers because exponent handles
[06:47] negative numbers itself but then uh all
[06:49] we're doing is throwing it into an
[06:51] exponent first. Great. So now we have a
[06:54] theoretical understanding of the concept
[06:56] of softmax. Maybe we should jump into an
[06:58] Excel demo and then do that together.
[07:01] Great. So I'm going to make a copy of
[07:03] the sheet and we're going to work in the
[07:04] without answer sheet.
[07:07] And then without an answer sheet, the
[07:08] first thing we're going to have to do is
[07:10] create a bunch of logits. Great. So, how
[07:12] do we do that? I created a normal
[07:14] distribution with a mean of zero and a
[07:16] standard deviation of seven. Not super
[07:19] common to use that, but I think it'll
[07:20] just extenduate the differences so we
[07:22] can really see a meaty example here as
[07:24] we run through this uh sheet. So, first
[07:27] thing I'm going to do is I'm going to
[07:28] create 10 logs for me to use. Great. And
[07:31] then the next thing I'm going to do is
[07:33] we said we're going to try linear ratio
[07:34] probabilities. So when we work with
[07:37] linear ratio probabilities, we have
[07:38] negative numbers like -9 and -9 or - 7.1
[07:43] and that's going to cancel out with 6.8.
[07:44] We're just going to lose that signal if
[07:46] we sum up. So the first thing we have to
[07:48] do is find the minimum and then we're
[07:50] going to have to adjust everything based
[07:51] on the minimum. Great. So I found the
[07:53] minimum. And notice these numbers keep
[07:55] updating every time I change the sheet.
[07:57] The first thing I'm going to do is I'm
[07:58] going to take the logit. I'm going to
[08:01] take the logit and I'm going to minus
[08:03] the minimum here. which means the
[08:05] minimum value is going to be zero. Gonna
[08:08] do that for all 10 of my parameters.
[08:11] And then I did that wrong because I
[08:13] should have locked in the C column. Here
[08:17] we go. And now one number will always be
[08:20] zero. Great. So now that I've reset
[08:23] negative values, I could just sum up
[08:26] these modified baseline logits. and I
[08:30] have a sum and I could divide this
[08:33] modified logic with the sum. Again,
[08:36] we're going to lock this
[08:38] cell. We're going to drag and drop. And
[08:41] now we get probabilities out of logits.
[08:44] What's one thing that's pretty obvious
[08:45] to us? A lot of these numbers are going
[08:48] to converge at around 10 to 15% based on
[08:50] our logits. Let's Okay, let's try and do
[08:53] that again. Oh my god, they're conver
[08:55] 15%. Converging on 10 15% converging
[08:57] around 10 15%. This has a little bit to
[08:59] do with our normal distribution that we
[09:01] had above, but it's just kind of like
[09:03] things tend to converge when you do
[09:05] linear ratios.
[09:07] Great.
[09:08] So, we did that. Next up, we want to
[09:11] work on softmax. First step is we want
[09:13] to do exponents. We want to learn about
[09:15] how exponents work. So, I have a bunch
[09:16] of numbers here starting from minus2 all
[09:18] the way to 10. And I'm going to just
[09:20] like create the exponent for all of
[09:22] those. So, equals exp. What do we see
[09:26] here? By the way, you can see I kind of
[09:27] stopped the chart at number three cuz
[09:29] like these numbers are getting really
[09:31] really big and it's going to be hard to
[09:33] like see the little numbers here in the
[09:35] chart. So what do we see? We see that
[09:39] like negative values are kind of between
[09:40] minus.1
[09:42] sorry between 0.1 and one. We see that
[09:45] numbers between 0 and one or between 0
[09:48] and sorry between 1 and 2.7 and then
[09:51] numbers are starting to get
[09:52] exponentially bigger. the gaps between
[09:54] whole numbers get bigger. The larger
[09:56] numbers become even larger. The smaller
[09:58] numbers become even smaller. So that's a
[10:00] really useful attribute for us as we're
[10:03] trying to work with probabilities. And
[10:05] we'll see why in a moment. [snorts]
[10:07] So we have softmax vector here. Now
[10:10] instead of having just a single like
[10:12] exponent, we want to actually try and
[10:14] softmax a vector. So first we're going
[10:16] to create an exponent for all of these
[10:18] input logits.
[10:21] Every one of these gets represented by
[10:23] an exponent. And it's kind of hard to
[10:24] see. So I'm going to add two more digits
[10:26] here. And you can kind of see that this
[10:28] 0.07 became 0.01 like minus4.5.01.
[10:34] These numbers start making sense. Okay.
[10:35] So now we want to sum them
[10:40] and then divide each of the exponents by
[10:42] the sum of all the exponents. Great. So
[10:45] I did that and we get to see Oh, I had
[10:47] to lock the cell for the sum.
[10:52] There we go. And then we get to see,
[10:54] wow, what does this even mean? We have
[10:57] one number at 99% and another the number
[11:00] at 1%. Right? The number that was most
[11:03] likely to win has actually won. This is
[11:07] why when I talk about softmix, I say
[11:09] this is a kind of a winner takes all or
[11:10] winners take all situation. Let's see
[11:13] the same set of logits. Linear ratio
[11:15] versus soft mix ratios.
[11:18] When we look at it here, we can see that
[11:20] number nine was kind of about to win at
[11:23] linear ratio. Slightly ahead of eight,
[11:25] slightly ahead of six. But when we look
[11:27] at the softmax, it really broke out. It
[11:30] really did a lot better. It's very
[11:32] clearly the winner of this round, right?
[11:35] That's kind of what we want because
[11:36] large language models, we're just
[11:38] choosing one word per round. We don't
[11:40] need multiple winners necessarily, but
[11:42] we do have like some option to maintain
[11:46] uh other similar probabilities. So,
[11:48] let's try and refresh this. Okay, here
[11:50] we go. Now, number three and four were
[11:53] kind of identical. Not really. They had
[11:55] a little bit of a gap. They went from
[11:56] like three and uh four here. They went
[11:59] all the way up to 49% and 38%. So,
[12:03] that's that tells us something. You can
[12:05] have multiple winners, but this is a
[12:06] really winner take all kind of like math
[12:09] operation.
[12:11] One last thing we should see about
[12:13] softmax. We're kind of done with one
[12:14] with onedimensional softmax. We we're
[12:17] done learning about softmax at the end
[12:18] of our matrix. We have softmax in the mi
[12:21] for whole matrixes for 2D arrays. Why is
[12:25] that? Is that the attention the
[12:28] attention operator which we don't know
[12:30] anything about yet. And maybe we'll
[12:32] learn about it when we get to section
[12:33] 17. Uses softmix inside of attention. So
[12:37] we need to know how softmix works inside
[12:38] of attention. When we do softmix inside
[12:41] of attention, what we're going to do is
[12:43] we're going to um sum every row and
[12:45] softmax based on that. So let's say I
[12:48] have matrix one which represents my
[12:50] input, matrix 2 which represents the
[12:51] learnable weights. I matt mole both of
[12:54] those together. Now I want to soft max.
[12:57] Great. So the first thing is I have to
[12:59] do an exponent of each one of these
[13:01] cells, each one of the activations
[13:05] inside of that matrix. Then I'm going to
[13:08] sum up each row.
[13:13] As we said, when we do this for when we
[13:15] do softmax for a whole matrix, we're
[13:17] going to want it to be per row. Great.
[13:19] Now I have the pair row sum. So let's
[13:22] try and softmax each one of these each
[13:24] one of these exponents. exponent divided
[13:27] by its own row sum. I'm going to lock
[13:30] the column for row sum.
[13:34] Then I'm going to have five rows. Five
[13:36] rows, not four. Here we go. And you can
[13:38] see each row sums up at 100%. Each row
[13:42] sums up at 100%. Each row sums up at
[13:45] 100%. So let's look at the distributions
[13:47] here. Let's look at this last line. This
[13:50] last row here. You could kind of see
[13:52] that like we had point like let's look
[13:54] at the bar charts not say the numbers
[13:56] but 0.9 was really like clearly going to
[13:59] win here. It's much more useful. You
[14:01] could see that all of the other numbers
[14:03] became a lot less likely to win right
[14:05] like we we can now see that the
[14:07] distribution of them is right like we've
[14:09] been able to kind of flatten out this
[14:11] curve. So that's the function of softmax
[14:13] winners take all kind of situation.
[14:15] Great. So we did all over Excel. We
[14:18] looked at logits. We went to linear
[14:20] ratio probabilities. We did we got
[14:22] introduced to exponents. We saw how to
[14:24] do softmax for a 1D vector. We compared
[14:27] softmax with linear ratio. Softmax is
[14:29] winner takes all. And then we did
[14:31] softmax on a 2D matrix. Great. Now let's
[14:34] look at a little bit of code. This code
[14:36] is effectively the same deep neural
[14:38] network that we've been seeing all
[14:40] along. Um, we've got our data set of A
[14:44] multiplied B modulus C. We've got our
[14:46] deep neural network that now has uh the
[14:49] larorm hardcoded in and so on. Uh,
[14:52] doesn't have a drop out. It does have a
[14:55] drop. It doesn't have a dropout. We have
[14:57] hardcoded a bunch of stuff from the
[14:59] previous section. It has a training loop
[15:01] that just initializes the deep learning
[15:04] neural deep neural network. It has our
[15:07] weight DK from the previous section. has
[15:09] our initialization from section 10. So
[15:11] on this is not really special. We didn't
[15:13] really do a lot of the training loop. So
[15:15] I'm just going to call model equals
[15:16] train
[15:18] based on model equals train. I'm just
[15:20] going to try and run this model once
[15:22] it's done training. Maybe one thing
[15:23] worth noting. I didn't actually let this
[15:26] complete training. I kind of created
[15:28] some parameters that are actually pretty
[15:29] hard to finish in 100 epics. So it's 85%
[15:32] complete. Why is that useful? It means
[15:34] it's going to make mistakes at 15% of
[15:37] the data set. Um, so that's useful for
[15:40] us to know. Um, so I went ahead and I
[15:43] was like, aha, find me some interesting
[15:44] logs that fail. So I'm going to try and
[15:48] 72 multiplied by 12 modulus 10. What's
[15:52] the remainder of 10 when I do that
[15:54] operator? And this is what my network
[15:56] tell gives me as an output. I expected
[15:59] to see the number six cuz that's the
[16:01] outcome mathematically. But what I could
[16:03] see here that it's doing is that uh it's
[16:06] giving me a bunch of logs as an output.
[16:08] And my problem is I want to get
[16:10] probabilities because I'm just trying to
[16:11] choose the most likely probability. So I
[16:14] could do probability torchs softmax.
[16:17] That's the built-in softmax function.
[16:19] Why would I implement my own? All of
[16:21] these already exist as functions inside
[16:22] of PyTorch. So I'll give it the list of
[16:25] logs and then I'll just print them out.
[16:27] And as you can see that the uh the sixth
[16:30] largest has a pretty good percentage of
[16:31] 22.8
[16:33] but but number eight actually has a
[16:36] slightly higher percentage. Why is that?
[16:39] Even though it was expecting six, the
[16:40] network's not done training. Sometimes
[16:42] it's going to make mistakes but at least
[16:44] it was able to preserve and enhance the
[16:47] differences between the winning options.
[16:50] So you can see number eight, number six
[16:51] and number two are the winning options
[16:53] right now for this inprocess training
[16:55] network. But when you were looking at
[16:57] that at linear ratio, it wasn't super
[16:59] clear to even see that, right? Like when
[17:01] I kind of look and squint at this table,
[17:03] it kind of looks like 12 is kind of
[17:05] similar to six. Sorry, seven is kind of
[17:07] similar to six, right? All of a sudden
[17:10] with softmax, the small differences made
[17:13] a big difference in the final
[17:15] probability. Makes it a lot easier to
[17:17] see what the network is actually trying
[17:18] to communicate to us. Great. So that's
[17:21] softmax. So now I have an exercise for
[17:23] you. Go ahead and try and implement
[17:25] softmax yourself. You're going to need
[17:27] to use exponent. You're going to need to
[17:29] use sum and you're also going to need to
[17:31] use the max to get the logit out of the
[17:33] array. Great. So let's look at what that
[17:35] looks like. You try and implement this
[17:37] yourself, but really quickly torch max
[17:39] to get the the logit. We're going to
[17:41] exponent the log with torch.x and torch
[17:44] sum to sum up the logit. Try and write
[17:46] this up yourself and then see if you
[17:49] can't get the probabilities yourself.
[17:52] So, we finished looking at how softmax
[17:56] works. Let's think about a couple of
[17:58] decisions we're going to make. One is
[17:59] we're going to use the softmax that we
[18:01] were taught here. That one's kind of
[18:02] called log softmax. It's because it's
[18:04] soft, right? Um, and we're going to try
[18:07] and use that that in our uh output for
[18:11] our large language model. I will mention
[18:13] that there are alternatives to that,
[18:15] right? There's something called a sparse
[18:17] max which is actually much less soft
[18:21] than soft max. Some might call it
[18:23] sparse, some might call it hard max.
[18:25] Doesn't really matter the name. But you
[18:27] could see that in 3D when we visualize
[18:28] it, the soft max has this like very
[18:31] gentle slope and sparse max has this
[18:33] like very like intense slope. Why is
[18:36] that important? I don't know if you
[18:37] remember section 7, we're talking about
[18:38] loss functions. Then we got to lost
[18:40] landscapes. Oh my goodness, we're back
[18:42] at lost landscape. Our goal is to walk
[18:45] through planes. Those planes tend to be
[18:47] pretty soft themselves. We're trying to
[18:49] walk the lost landscape. So, it's really
[18:52] useful that a softmax function is also
[18:54] kind of soft itself.
[18:57] There are other softmax functions we
[18:59] could use. All of them including sparse
[19:01] max kind of predate LLMs and aren't
[19:03] commonly used in LLMs, but often you
[19:05] would see more interesting softmaxes
[19:07] used inside of attention. But for now,
[19:10] we're just going to use softmax as is.
[19:12] Great. So we have uh the decision that
[19:14] we're going to use log softmax as our
[19:16] softax. That's the name of the softmax
[19:18] that we've been studying all along. And
[19:20] then we have sampling. Remember section
[19:22] one we said we're going to uh have to
[19:25] take probabilities and then choose
[19:27] probabilities from there. Temperature
[19:29] top p top top k all of that stuff. We're
[19:32] going to bolt sampling on top of
[19:34] softmax. So softax is going to take the
[19:36] first round of sampling is going to help
[19:38] us get probabilities to make sense. and
[19:40] then top k top p temperature are going
[19:42] to take the second stab at that and with
[19:44] that we're actually completely done with
[19:46] DNN deep neural network techniques that
[19:49] are also applicable to large language
[19:51] models our next section tokenizers is
[19:54] going to be all about language the
[19:56] section after that embedding is also
[19:57] going to be all about language after
[19:59] that transformers really used for
[20:01] language so we're really going to be
[20:03] like a language only uh set of sections
[20:06] after this and I hope you would join me
[20:08] for that thank you so much and I hope to
[20:10] see you in our next section.
