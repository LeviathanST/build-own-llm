# Regularization | Build Your Own LLM Workshop #13

**Build Your Own LLM Workshop — Video #13 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 40m 27s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=2O8v8BX1LgM |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to one more
[00:03] episode of building your own LLM
[00:05] workshop with me Justin Angel. So this
[00:09] section is dedicated to regularization
[00:11] which is how we prevent overfitting in
[00:13] large language models. Let's talk a
[00:15] little bit about overfitting and how we
[00:17] got there and why we didn't see a lot of
[00:19] it thus far. The first thing that we
[00:21] should think about is that we've been
[00:23] working with our A multiplied by B
[00:26] modulus C data set. that doesn't leave a
[00:29] lot of room for uh uh for overfitting,
[00:34] right? Because all of our training data
[00:36] is 100% accurate. There's no noise in
[00:38] our data set. So, for example, if you
[00:41] were looking at language, right, which
[00:44] we care a lot about because we're
[00:45] building large language models. U those
[00:48] are not as deterministic as our little
[00:51] math data set. Uh, for example, if I
[00:54] said the capital of France is, you can
[00:56] complete that sentence with the word
[00:58] Paris. You could say that it's full of
[01:00] cheese. You could say it has a metro
[01:03] strike. All of those are likely as
[01:05] equally logically valid as any other
[01:08] option. Right? So, language is
[01:10] nondeterministic.
[01:12] As a result of that, when our number
[01:15] data set had deterministic answers, we
[01:18] weren't seeing a lot of overfitting. But
[01:20] if we're going to add 10% noise into our
[01:23] data set, for example, we'll take 10% of
[01:25] our data and we'll just say, hey,
[01:28] actually, we're going to shift that
[01:29] answer a bit. We will see a bunch of
[01:31] overfitting happen. So, we're going to
[01:33] start doing that. This in this example,
[01:35] we're going to add 10% noise to our A
[01:38] multiplied B modulus C data set. Let's
[01:41] think more about what is like the
[01:43] minimum amount of like uh irreducible
[01:46] error the language has. So, Chinchilla
[01:48] 2022 paper actually calculated the
[01:51] irreducible error of large language
[01:54] models as 1.69. So, they ran 400 tests
[01:58] over large language models. And what
[02:00] they found is that they weren't able to
[02:02] get the loss at under 1.69.
[02:05] To me, poetically, what I hear there is
[02:08] that the entropy of language is 1.69.
[02:11] You cannot get language to be more
[02:14] consistent than that. I think there's
[02:15] something really beautiful in that. So
[02:18] on the right you can see a chart of
[02:19] Chinchilla trying to add more compute
[02:22] and overtraining last and you could see
[02:23] they're really really struggling to get
[02:25] computed under 1.69. On the bottom right
[02:29] you could see them trying to add more
[02:30] parameters or more memory for our model
[02:33] and what you could see they're not able
[02:35] to bring uh the fun the the loss of that
[02:40] of those models at under 1.69 69 even
[02:43] though they found that it does reduce
[02:45] with scaling law the more compute you
[02:47] add the more parameters you add to the
[02:49] model the more data you give to the
[02:50] model but they were never able to get
[02:52] the training loss below 1.69 69. So I
[02:55] think that's something really important
[02:56] to notice.
[02:58] Okay. So now we've added 10% noise to
[03:01] our data set. What happens if we just
[03:03] run our previous example in our from our
[03:05] previous module of uh normalization on
[03:08] that data set? We're going to see
[03:10] something really really interesting.
[03:12] We're going to see that the test
[03:13] accuracy is at 80%. 80%. Wait, I had a
[03:18] 100% accuracy and then I add a 10%
[03:21] noise. Why is my test accuracy only at
[03:24] 80%, I would have expected it to be a
[03:26] 90. And the answer there is that we've
[03:28] overfit the noise in our training data.
[03:32] Another in another indication that we
[03:35] were seeing overfitting and this is
[03:36] super classic in machine learning
[03:38] models, right? Even if you don't really
[03:40] know the noise percentages of your data,
[03:42] is we see a gap between how well our
[03:45] model does in test data and how well it
[03:48] does on training data. That gap tells us
[03:50] that the fact that it's doing better on
[03:52] data that's seen and does worse in data
[03:54] that it hasn't seen tells us that it's
[03:56] overfit to the training data. Critical.
[03:59] You're going to see a lot of charts like
[04:01] this. If you keep training machine
[04:02] learning models, you're going to see
[04:04] that when test and test and train loss
[04:07] diverge, that's almost a definite sign
[04:09] of overfitting. So, we added 10% noise
[04:12] to a data set to a data set to simulate
[04:14] language. And we saw performance go from
[04:16] 100 to 80%. That's also an indication of
[04:19] that. Uh we now know that our deep
[04:21] neural network is memorizing the
[04:24] training set and will never be able to
[04:26] perform well enough on unseen test data.
[04:29] We'll add like a little bit more noise
[04:31] here and a little bit more
[04:32] regularization to prevent that
[04:34] overfitting. Great. So what are the
[04:37] regularization solutions we have to
[04:39] prevent overfitting? Regularization by
[04:41] the way is just a fancy way of of saying
[04:43] techniques that prevent overfitting.
[04:45] Solution number one is called dropout.
[04:48] So one very easy option to say that we
[04:50] don't want to overfit on data is to say
[04:53] actually we're going to randomly turn
[04:55] off a percentage of neurons during
[04:56] runtime. What's an example of that? Here
[04:59] on the GIF there's a very simple neural
[05:01] net. There's an input layer of three
[05:04] neurons, an output layer of two neurons,
[05:06] a hidden layer of four neurons. And with
[05:09] 50% dropout at every run, we're just
[05:11] going to turn off half of the hidden
[05:13] neurons. That is it. So with 50%
[05:16] dropout, we're going to turn off half of
[05:17] the hidden layer neurons. 50% is kind of
[05:20] a lot for large language models. I think
[05:22] it's too high. We'll talk more about why
[05:26] later, but often what you see when you
[05:30] do see dropout in large language models,
[05:32] you'll see it at 10%. So we'll turn off
[05:33] about 10%. But 50% kind of works well
[05:36] for this GIF here. And I think it's like
[05:38] a really good gift to illustrate how we
[05:40] randomly turn off half of the data set.
[05:42] So that's the first solution we have
[05:45] with GPT2 2019 trained uh using 10%
[05:49] dropout. Okay. So I just introduced you
[05:52] to dropout. It's going to solve all of
[05:53] our regularization overfitting problems.
[05:56] No, it actually isn't. Modern LLMs don't
[05:59] use over don't use dropout at all. Why
[06:02] is that? Is because the kind of
[06:04] overfitting it prevents really has more
[06:06] to do with deep neural networks, not
[06:08] really with language. Why? When we train
[06:11] a deep neural network, we show it the
[06:12] data over and over and over and over
[06:14] again. In epochs, when we train large
[06:16] language models, we often have enough
[06:19] data to not have to show the same data
[06:21] twice. And the kind of the kind of
[06:24] overfitting that dropout prevents has to
[06:26] do with showing the data more than once,
[06:28] right? Like so as a result of that,
[06:30] modern LLM just don't use dropout. They
[06:33] probably saved quite a lot of uh GPU
[06:35] compute as a result of that. But for our
[06:38] GPT2 style transformer, we will use 10%
[06:42] dropout. Why? I want to teach dropout
[06:44] and I want you to learn to think about
[06:46] things uh uh both creatively but also
[06:49] constructively. And I think dropout is a
[06:50] great place to apply that intuition.
[06:53] Okay. So we talked about dropout being a
[06:55] regularization technique solves all of
[06:57] our problem minus the fact that no one
[06:58] uses it. What are other techniques we
[07:01] could use to prevent overfitting? So one
[07:03] option is gradient clipping. What does
[07:05] that mean? If I want all of my gradients
[07:08] to always be within a range of one and
[07:11] minus one, one really easy option for me
[07:14] is to do value gradient clipping, which
[07:17] just means I'm just going to clip the
[07:19] edges of once it's either over one or
[07:21] under minus one and that is it. Right?
[07:24] So, one option is I could do value
[07:26] clipping on a range that I determined
[07:28] and I could just clip that. If I was
[07:30] only training one neuron, that would
[07:33] probably be totally fine. I'm training
[07:35] multiple neurons and multiple layers and
[07:38] multiple MLPS at all of the same time,
[07:41] right? At least within the same matrix.
[07:44] So what does that mean? If I took one
[07:47] number, let's say that I took the
[07:49] numbers 15.1, 5.3, and 1.2, and I
[07:52] clipped all of those to one, they are
[07:55] all now one, which is great. But we have
[07:58] clipped them in nonequal amounts
[08:00] relatively. What does that mean? We took
[08:03] 15.1 to1, we lost 14 points. We took 5.3
[08:06] to one, we lost four points, we took 1.2
[08:08] to one, and we lost 02. That's like very
[08:12] unequal. What we did is we reduced the
[08:15] magnitude, but we also with it lost the
[08:18] direction, right? If the model wanted to
[08:21] the numbers to be 15.1 and 5.3 and 1.2,
[08:24] we would should probably try and
[08:27] maintain the direction as well because
[08:28] the directionality of that data matters
[08:30] a lot. Why is it does this matter a lot?
[08:33] We'll learn about it when we get to
[08:34] embedding section 16 when we talk more
[08:37] about highdimensional spaces. All of
[08:39] these exist in high dimensional spaces
[08:41] when we're just navigating them. For
[08:43] that we need to persist direction. So no
[08:45] one does generally value clipping. A lot
[08:48] of people just do norm clipping. So we
[08:50] could just do norm clipping. Uh great.
[08:54] And then uh we'll do that. Let's look at
[08:57] the formulas. Our formulas for value
[08:59] gradient clip is maximum minus one
[09:02] minimum one. That's assuming that's our
[09:03] range. As a result of that, we're just
[09:06] going to hard clip to those boundaries.
[09:08] Great. We just learned that we don't
[09:09] want to do that. Probably want to do a
[09:11] norm gradient clip, which we normalize
[09:14] all the values to be clipped equally.
[09:16] So we'll say actually for every J, for
[09:19] every gradient, what's a gradient? It's
[09:21] part of how optimizers work. It's the
[09:24] derivative of the thing, right? remember
[09:26] um we're going to like either choose
[09:29] minimum of one so we're not never going
[09:31] to go below that like we're never going
[09:33] to go above that or we want to divide
[09:37] the or we're going to choose a number
[09:41] that is one divided by the sum of the
[09:44] com the sum of the square the root of
[09:46] the sum of the squares of all of the
[09:48] gradients. What does that mean? Not a
[09:51] lot to us. We're not going to prove that
[09:52] this works. What's important to know is
[09:54] that it takes all of the gradients into
[09:56] account. It does some fun math with it
[09:58] and then it chooses to bring them all
[10:00] down pretty much equally. I think that's
[10:03] super useful. And this minimum term is
[10:05] going to be applied equally to all of
[10:07] the gradients. That's the important
[10:08] thing. It is a term that's applied to
[10:10] all of the gradients at once. And don't
[10:12] worry if you didn't catch the math.
[10:14] We're going to see it in Excel. Great.
[10:16] Third solution for regularization.
[10:18] Again, we're just trying to prevent
[10:20] overfitting. is it could occur because
[10:22] the model uses super large values when
[10:25] smaller values would work. What's an
[10:26] example in our domain? 1 + 2 equal
[10:30] modulus 3. Instead of saying that the
[10:33] correct answer is three, it's three.
[10:35] Let's say that we said it's five because
[10:37] we added noise, right? We added noise
[10:39] into the data set. Should the model just
[10:41] memorize 1 + 2 modulus 3 = 5 or should
[10:45] it over infer and overfitit the data to
[10:48] fit other examples? It shouldn't overf
[10:50] the the data. That was a leading
[10:52] question. It should really memorize just
[10:55] enough noise to pass the the training
[10:57] examples. So what do we do with that? We
[11:02] can penalize it every time it's using
[11:04] values that are not actually needed. How
[11:07] do we do that? We could just apply a
[11:10] weight decay every time we update
[11:12] weights. We can just say actually drop
[11:14] them by a little bit based on the
[11:16] original value. So the original value
[11:19] that has nothing to do with the update,
[11:20] take a small percentage of it and get
[11:22] rid of it. Every time we update value,
[11:25] make the network work for whatever u
[11:29] weight current weight it has. If it's
[11:30] not needed, it'll just disappear. I kind
[11:33] of imagine it as like uh in uh at the
[11:36] the beach you build a sand castle, the
[11:39] ocean comes in and it takes a little bit
[11:40] every time, right? This is just that. On
[11:44] the left, we have a really great gift
[11:45] that is very hypnotic. And I'm just
[11:47] assuming you're staring at it while I'm
[11:49] speaking. And you can see a ball that's
[11:51] going left and right and left and right
[11:53] and left and right. What? Why is that
[11:56] bad? Let's say that ball is us trying to
[11:57] optimize on a lost landscape. Clearly,
[12:00] this is a really bad state to be in.
[12:02] We're trapped in this infinite loop,
[12:04] right? Because there's no way to decay.
[12:06] If we did introduce weight decay, the
[12:08] ball would eventually end at the center.
[12:10] We wanted to lose a little bit of
[12:12] momentum. We want it to start
[12:13] distrusting its own intuition. How do we
[12:16] do that? There's a formula here. Don't
[12:18] worry about memorizing it. We're going
[12:19] to see it in Excel with weight up with
[12:22] weight decay. We take the old weight. We
[12:26] minus the learning rate times gradient.
[12:28] That's not news to us. That's just how a
[12:30] stoastic gradient descent has always
[12:32] worked. But on top of that, we take a
[12:35] set weight decay. We take the old value
[12:38] and we reduce that as well from the new
[12:41] value. That means that whatever the old
[12:44] value was, however high the old value
[12:46] was, that means we're going to chunk
[12:47] more off the new value. However high we
[12:50] said way decay, that's going to remove
[12:51] even more in each turn. And we're going
[12:53] to do that every single epoch, every
[12:55] single step. Really, really interesting.
[12:58] Don't worry if you didn't catch the
[12:59] math. The important thing, we're
[13:00] decaying the weight with every update.
[13:03] That's the important thing. We're never
[13:04] going to just let these these updates
[13:07] happen unless we take a little bit off.
[13:09] We skim a little bit off the top. Great.
[13:11] So, we now we talked about three totally
[13:13] different regularization techniques.
[13:15] Let's watch all of them in Excel and
[13:17] kind of go over these together. Great.
[13:20] First thing I do is I make a copy of
[13:22] this and then we're going to work in a
[13:24] copy and we're going to work inside the
[13:26] without answers sheet. Right? So, let's
[13:29] go to without answers. First thing is
[13:32] let's say I have this input for dropout
[13:34] and I say that 10% of these neurons
[13:37] right because each one of these
[13:38] represents a weight for a neuron each
[13:40] 10% of these weights should be dropped.
[13:43] How do I do that? I say uh random
[13:49] actually I'm just going to copy this
[13:50] because it's going to be easier on me.
[13:52] If random is bigger than this then we
[13:54] choose one otherwise choose zero. Great.
[13:57] So if random
[14:00] bigger than this cell then use one
[14:03] otherwise use zero. Don't forget we're
[14:06] going to have to lock the percentages.
[14:09] Great. And then I'm going to repeat that
[14:11] for this whole row.
[14:14] And I'm going to repeat that for all of
[14:16] these columns. Great. So 10% of of uh
[14:21] rows are going to be hidden out. I think
[14:22] I did too many. We needed to do seven
[14:25] and I did eight. So I'm going to delete
[14:27] this.
[14:29] Great. So I have seven. So this is a
[14:31] dropout mask. You can see as I update.
[14:34] Oh my goodness. I'm updating. I'm
[14:36] updating. Really great update dropout
[14:38] mask. Sometimes it's 10%. Sometimes it's
[14:41] over 10%. Sometimes it's under. And then
[14:44] I going to go and apply the mask here.
[14:46] Right. So how do you apply a mask? My
[14:48] without cheats should really not have
[14:50] this answer for you. I'm going to take
[14:53] this cell and I'm going to multiply I'm
[14:56] going to take this cell and I'm going to
[14:59] multiply it by the dropout mask.
[15:02] Multiply for Oh, I overrode this value.
[15:06] I'm going to take this cell and I'm
[15:08] going to multiply it by the dropout
[15:10] mask. Great. So now I'm going to drag
[15:13] drag and drop here all the way down
[15:16] seven cells. Great. And now that means
[15:19] every place that I've gotten less than
[15:22] 10% when I did my random, I'm going to
[15:24] apply a mask of zero. And I'm going to
[15:27] zero out that cell. And that's it. That
[15:30] means I've just turned off these weights
[15:32] in these positions that weren't turned
[15:35] off before. Right? Totally turned off
[15:38] for this one run of the training run.
[15:40] And it'll be different the next time I
[15:42] do another training step or another
[15:44] epoch. Okay, great. So now that I've
[15:47] lowered
[15:48] the total magnitude of the network, I
[15:51] have a problem because the network and
[15:53] next time it runs is going to run with a
[15:55] higher magnitude potentially, right?
[15:57] Because it's this is all random. So I
[16:00] have one of two options. One option is I
[16:02] could scale up all of the magnitude of
[16:04] all of the items here in this network. I
[16:07] could do that during training time for
[16:09] this run or I could do this during
[16:11] runtime, during inference time when we
[16:13] actually use the model. I like doing it
[16:16] here just because it makes more sense to
[16:18] me, but you could also choose to do it
[16:20] in inference time. There's no real
[16:21] difference when it comes to statistics.
[16:24] Great. So now our scale up ratio is I'm
[16:28] going to uh because 10% or of of weights
[16:32] are turned off, every weight will be
[16:34] multiplied by 1.11. So I took that I
[16:37] multiplied 1.1 with the weight of the
[16:40] cell. didn't do anything for the cells
[16:43] that got dropped out, right? They're
[16:44] still at zero. And now we've preserved
[16:46] the magnitude during training time. So
[16:49] that's one option of doing that when you
[16:51] want to rescale up the ratio uh based on
[16:54] how many cells you turned off. Okay. So
[16:56] what do we do in dropout inference time?
[16:59] If in dropout inference time we already
[17:02] uh we scaled up the magnitude during
[17:03] training time, then actually um there's
[17:06] nothing for us to do, right? So the
[17:08] dropout mask for inference times is
[17:11] always going to be one, meaning it
[17:13] doesn't do anything at inference time.
[17:15] Dropout only affects training time,
[17:18] assuming we up the magnitude during
[17:20] training times. If we didn't, if we
[17:23] chose to skip this phase of scaling up
[17:25] the ratio, then we would need to scale
[17:27] up the ratio here during inference time.
[17:29] I'm not going to show that. You can
[17:31] easily imagine what 1.11 looks like in
[17:33] these cells. But important to notice as
[17:35] long as we scaled up the magnitude of
[17:37] dropout
[17:39] during training there's dropout just
[17:41] doesn't do anything during inference
[17:44] time. Great. So that's that's dropout.
[17:47] Just a quick reminder we will build our
[17:50] large language model with dropout.
[17:52] However, no one else does that anymore.
[17:55] So it's while it's good to learn that
[17:57] this is just an example and I want you
[17:59] to think about why Dropout is so good at
[18:00] what it does. Why? because every time we
[18:03] run another step, it's going to turn off
[18:06] different weights. And it means that if
[18:08] one weight is too important to the
[18:09] network, the network has to find a way
[18:11] of compensating for that, especially
[18:13] doing back propagation. Okay, so we
[18:15] talked about we mentioned back
[18:16] propagation, our old friend. Now, we're
[18:19] going to go as close to optimizers as
[18:21] we're ever going to get to in this
[18:22] class, especially their math. So, let's
[18:24] look at back propagation. Remember, we
[18:26] had demo number three had two inputs,
[18:29] one neuron. Okay, really cool. We have a
[18:31] feed forward here, two inputs, two
[18:34] weights and a bias. The value is 3.1. We
[18:38] expected 40. We talked about expected in
[18:41] in back propagation. This is copied
[18:43] verbatim from section 8. The residual is
[18:46] minus point is minus.9.
[18:49] Then we do a derivative of baseline and
[18:51] then we find the back propagation values
[18:54] and given the back like the gradients
[18:57] and based on that we're going to update
[18:59] based on the learning rate. So we'll
[19:01] take the old values we'll minus the
[19:03] gradient multiply by the learning rate.
[19:05] All of that is stuff that we've already
[19:06] seen in back propagation. This is just
[19:08] how back propagation works. Great. When
[19:10] I say back propagation work I mean when
[19:12] your optimizer is vanilla stocastic
[19:15] gradient descent which we're not exactly
[19:17] using. We're using AdamW. But this is a
[19:19] good way of learning that. Great. So now
[19:22] we want to do uh gradient clipping uh
[19:24] back propagation. You know I kind of lie
[19:27] to you. This isn't just the back
[19:28] propagation column. This is really the
[19:30] gradient column now. Oh my gosh, she
[19:32] just changed the name. It's the same
[19:34] thing. This column means the same thing.
[19:36] Great. So now that we know that value
[19:39] gradient clip is maximum of minus one,
[19:42] minimum gradient one. How do we write
[19:45] this code? Actually, we can just write
[19:46] it the way that it says it is right
[19:48] here. Maximum and then I'm going to
[19:50] choose the range of minus one minimum
[19:53] the gradient and then I'm going to
[19:55] choose one. Right? Going to close that.
[19:58] Oh my goodness. We just wrote value uh
[20:02] uh clipped weight and biases. How do we
[20:06] do the update? We're going to take the
[20:09] old weight minus the value clipped
[20:13] multiplied by the learning rate, right?
[20:15] And we're still taking learning rate
[20:17] into account. If we dropped learning
[20:19] rate here, we could lower them further
[20:21] down. Most importantly, it's not really
[20:24] just minus one. It's minimum gradient
[20:26] which ends up being a parameter then we
[20:29] end up using at like we set it almost in
[20:32] code. Uh and then the maximum gradient
[20:35] here. Great. Here we go. And then I'll
[20:38] copy it one more time. And actually I
[20:40] think I did this one wrong cuz it was
[20:41] supposed to be minus one here. La. Okay.
[20:45] Great.
[20:49] Did I do this wrong? I feel like I did
[20:50] this wrong.
[20:52] So maximum of
[20:56] minus one. Yes. And minimum of
[21:01] ah I forgot to add G in here. Here we
[21:04] go. That was the problem.
[21:07] And then we'll add G back in here.
[21:09] Perfect.
[21:13] Here we go. So now we could start
[21:15] updating and say actually I want my
[21:17] minimum gradient to be 1 and a half.
[21:19] That's the range I want to play with.
[21:20] Okay. So now the value clipping happens
[21:22] in different directions. Great. So we've
[21:24] parameterized max gradient and minimum
[21:27] gradient with value clipping. We we know
[21:29] that learning rate is part of this. We
[21:31] just did a little bit of optimizer magic
[21:33] with value with value clipping. I love
[21:36] this. Great. So we said we're not going
[21:38] to do value clipping. Why? Because it
[21:41] clips everything to the same maximum
[21:43] which loses direction. We brought
[21:46] everything to the same magnitude but at
[21:47] the same time we lost direction. So we
[21:50] have this norm factor here. Minimum of
[21:52] one uh or one divided by the the the
[21:57] root square of the the of the sum of the
[22:01] squares. So instead of me writing this
[22:03] in front of you, I have that written
[22:06] here. It's looking at all the three
[22:08] power statements. Let's look at that. So
[22:11] power two of this and this and this. I
[22:13] made this formula as clear as possible.
[22:16] We're just reimplementing this the the
[22:19] formula as it's listed. So now I have my
[22:21] norm factor. So all I have to do is I
[22:24] take my gradient multiply by the norm
[22:27] factor. Here we go. We're going to do
[22:30] this one and this one. And then I had to
[22:32] lock norm factor which I didn't do. Here
[22:35] we go.
[22:38] Perfect. So now we've norm clipped it.
[22:41] Notice none of them are exactly one or
[22:43] minus one, but they all kind of got
[22:45] clipped equally by one/ird. That's by
[22:49] almost onethird. That's really
[22:51] interesting to notice. How much do they
[22:53] get clipped by? They all got clipped by
[22:55] 37. Everything got clipped equally. So,
[22:58] how do we add update our new value?
[23:01] We'll take the norm clip. We'll take the
[23:03] old value minus the norm clipped
[23:06] multiplied by the learning rate. And
[23:08] again, we always take the learning rate
[23:10] into account. We could decide to do 0.1
[23:12] and so on and so forth. Great. So that
[23:14] was norm clipping using a norm factor on
[23:17] all of these val gradients at the same
[23:19] time and or we could do value clipping
[23:22] on all of the gradients but then we lose
[23:23] direction.
[23:25] Finally, we talked about weight decay.
[23:28] Weight decay is really interesting here.
[23:30] We're really opening up an optimizer.
[23:32] I'm only going to show this to you for
[23:34] vanilla stocastic gradient descent
[23:36] because otherwise I'd have to show you
[23:38] how all the atom ws. It goes deep into
[23:41] its math. Doesn't really make sense for
[23:43] you to learn this in this class. If
[23:45] you're interested in optimizers, I do
[23:46] recommend watching an optimizer class.
[23:48] Great. So now we're doing weight decay.
[23:50] How do we do weight decay? Right. So we
[23:53] have our gradients here. I kind of hate
[23:55] that it says back propagation. It's just
[23:57] going to say gradients now. So how do we
[23:59] do weight decay? we have minus the
[24:02] learning rate times the weight decay
[24:05] minus the old weight. Okay, so what is
[24:07] that? So learning rate, we're going to
[24:09] lock that one in place in a bit
[24:12] multiplied by the weight decay. That's a
[24:14] fixed number for the entire run
[24:17] multiplied by the old weight. The higher
[24:20] the old weight, the higher the learning
[24:23] rate, the more we're going to wait
[24:24] decay, right? Great. So I'm going to
[24:27] lock these two cells in place. I'm going
[24:29] to lock the weight decay. Oh, sorry. I
[24:32] locked the only thing I shouldn't have.
[24:34] I'm going to lock the weight decay. I'm
[24:36] going to lock the learning rate.
[24:40] Here we go.
[24:42] Great. So, we lock that. What are we
[24:44] going to do? We're going to minus the
[24:47] old old value minus the weight decay,
[24:50] right? Sorry, minus the gradient times
[24:52] the learning rate minus the value of the
[24:55] weight decay. So now we just saw weight
[24:58] decay in action
[25:00] and let's say that like instead of
[25:03] making really big learning rate updates
[25:06] we would be doing 0.1 updates. I'm going
[25:08] just going to go ahead and delete this
[25:10] right for a moment. You could see that
[25:13] the n first weight would be 1.68 and
[25:16] really we brought it down to 1.67 or
[25:18] 1.66. Look it's doing a little bit of
[25:20] rounding here for us. Weight decay isn't
[25:24] supposed to be massive. 10% weight
[25:26] decay, 10% learning rate. You're not
[25:28] going to see massive differences, but
[25:30] it's just taking a few grains of sand
[25:32] from our sand castle, making it so the
[25:34] model has to justify every one of these
[25:36] weights. If these weight decays weren't
[25:39] appropriate, breaggation later on should
[25:41] go back and fix that in the next step,
[25:44] right? We should have worse performance.
[25:46] Okay? So, you just saw an weight decay
[25:48] in practice. You just saw how it works.
[25:50] It takes a small a small chunk of the
[25:53] old weight a small chunk of based on the
[25:56] learning rate and then decides hey from
[25:58] the gradient I'm going to take a small
[26:01] chunk out of it and not do the full
[26:03] update. Great. So we saw all of these
[26:06] concepts drop out back prop gradient
[26:10] clipping for value and norm and weight
[26:11] decay. We saw these in Excel. You should
[26:13] now have an intuitive grasp over this.
[26:15] Are you ever going to write any of this
[26:17] code yourself? No. We've got all these
[26:19] pre-implemented in PyTorch. So, let's go
[26:21] look at code. Right here in the top
[26:24] left,
[26:25] this is just like if you need a cheat
[26:27] sheet for the two lines of code each of
[26:29] these technique takes, right? We're
[26:31] going to have X plus dropout and then
[26:35] you choose to apply dropout to whatever
[26:37] layer and that's pretty much it. You use
[26:38] NN dropout for that. So, you give it the
[26:41] dropout rate. You set up a dropout and
[26:43] then you during feed forward you apply
[26:45] dropout to it. Pretty easy. Two lines of
[26:48] code to apply dropout norm clipping.
[26:51] Right? We said we're not going to do
[26:52] value clipping. We'll do norm clipping.
[26:55] You call n utils clip grad norm. We give
[26:57] it the maximum and the min and the
[26:59] parameters and it just does that. So
[27:02] that's another option. And if you want
[27:03] to apply weight decay, well the atom
[27:06] optimizer already takes weight decay as
[27:08] a parameter. You just give it the weight
[27:10] decay. Did we just learn a bunch of
[27:12] stuff in Excel that you're never going
[27:14] to have to implement yourself?
[27:15] Absolutely. Our goal here today is to
[27:18] build intuition, not necessarily write
[27:20] every line of code ourself. Great. So,
[27:22] let's write some code. We're going to go
[27:24] back to our A multiplied by B modulus C.
[27:29] I'm going to just correct this cuz I
[27:31] hate having mistakes in this deck.
[27:32] Great.
[27:35] And then we're going to go into code.
[27:37] So, what's our code example going to be?
[27:38] It's going to be what we've worked with
[27:40] so far. So, now we've got 8 multiplied
[27:43] by B modulus C. The data set hasn't
[27:46] changed at all. It's all uh 150 examples
[27:49] in train, 38,000 examples in test. Wait,
[27:53] wait, wait. I said I'm going to add some
[27:55] noise here. What's my noise rate? It's
[27:57] 10%. For 10% of noise, I'm going to add
[28:01] wrong labels, right? And I'm going to
[28:03] randomly choose some wrong labels that
[28:06] I'm going to throw into my data set. So
[28:09] 10% of data is going to be absolutely
[28:11] junk, right? And the model in order to
[28:13] succeed has to learn to train to that
[28:16] data but not apply that to the test set
[28:18] necessarily. The test set should still
[28:20] be as good as possible, right? Like not
[28:24] overfit to these to this noise. So
[28:26] that's what noise looks like. You'll
[28:28] never have to implement noise yourself.
[28:29] This is just me trying to build a data
[28:31] set before we move on to language.
[28:34] Great. So now we have our deep neural
[28:36] network. We've seen uh 16 sequential
[28:39] layers growing, shrinking. RMS norm is
[28:41] now hardcoded. Uh we we've got 219
[28:45] inputs. We've got five uh we've got uh
[28:48] 19 eight sorry 18 outputs. All of that
[28:51] stuff hasn't shifted. What is going to
[28:54] shift is we now have self dropouts and
[28:56] just another module list. Your module is
[28:58] going to be linears or dropout. Just a
[29:00] way of me making sure that we get to
[29:02] play around with it. And then if there's
[29:05] dropout and then we're going to take the
[29:07] dropout rate from the constructor from
[29:08] the initializer and then we're going to
[29:11] append a dropout here. If dropout is at
[29:13] 0% it's just not going to do anything.
[29:15] If dropout is more than 10% then for
[29:18] each layer we're going to call dropout
[29:21] after we've activated the pre-orm then
[29:24] we activate the layer then we're going
[29:26] to activate dropout and then we'll add
[29:28] the residual back in. Great. So this is
[29:31] you can see the order of operation
[29:33] pre-normalization
[29:35] activating the MLP layer the growing
[29:37] shrinking R relu MLP layer dropout and
[29:41] then residuals you could follow this
[29:43] like it's math great you now know how to
[29:45] write read this code and you understand
[29:47] what it means because you've learned all
[29:48] about it in this workshop how many
[29:51] parameters do I have I have a million
[29:54] parameters and you can kind of see the
[29:56] structure we have the input linear input
[29:59] layer we have the output layer we have
[30:02] uh s and then we have 16 of these uh
[30:06] modules that are growing shrinking
[30:08] growing shrinking and then we'll use the
[30:10] RMS norm drop out appropriately okay
[30:12] amazing so that's our DNN didn't change
[30:15] that much training run doesn't change
[30:18] that much we take drop out rate so
[30:20] there's a couple of parameters there's
[30:21] dropout there's weight decay and there's
[30:23] clip gr
[30:25] yes or no what's the dropout rate what's
[30:27] the weight decay each of these again is
[30:30] Just one or two lines of code here. When
[30:33] we initialize the drop the model, we're
[30:35] going to say dropout rate equals dropout
[30:37] rate. We're just going to be a straight
[30:38] pass through. What does that do? The
[30:40] dropout rate goes into the initializer.
[30:43] From the initializer, it goes into the
[30:45] dropout and from the and then dropout
[30:48] and then later it gets used during a
[30:50] feed forward pass. That's it. We wrote
[30:53] three lines of code to implement
[30:54] dropout. We wrote more in Excel I think
[30:57] to implement this. Great. So now we know
[30:59] how to implement dropout. How do we
[31:02] implement weight decay? Oh my goodness.
[31:04] I just let give it to the optimizer and
[31:06] it knows how to handle that. I will
[31:08] mention atomw is somewhat significantly
[31:11] more complicated than vanilla stoastic
[31:14] radiate descent which is what we've seen
[31:16] thus far, but it kind of sort of handles
[31:18] way decay similarly.
[31:21] Not really, but it's close enough for
[31:22] our purposes that we understand what it
[31:24] does. Okay. So now our final and last
[31:27] par parameter clip gradient. How how
[31:31] does that influence our uh training loop
[31:34] somewhere here? Oh my god, I'm going to
[31:36] scroll. I'm going to scroll after every
[31:38] backward pass
[31:40] right before we go and update the values
[31:43] between loss backward when we do all the
[31:46] gradient calculation. But before we do
[31:48] all of the optimizer updates, we're
[31:50] going to go ahead and clip the
[31:51] gradients. And here it's called clip
[31:53] gradient norm. Remember, we're clip
[31:55] grading norm, not clipping by value. And
[31:57] we're going to say max norm one as well,
[31:59] just in case. And it's going to do that
[32:01] for all of these parameters. Great. So
[32:03] now I have a training method that takes
[32:05] into account three new things that I
[32:06] just learned about. Dropout, weight,
[32:09] decay, and clip gradients.
[32:12] Great. So those are three regalization
[32:14] technique. What's the first one we're
[32:15] going to run? This whole notebook is
[32:17] going to be 10% noise like the title
[32:19] says, weight decay, and we'll add a
[32:21] little bit of gradient clipping at the
[32:22] end. Okay, great. So weight decay of
[32:24] zero. Let's I'm not doing any weight
[32:27] decay, right? So this is weight decay
[32:29] zero. No gradient clipping, no dropout.
[32:32] How long does that take to converge?
[32:35] Right? I'm going to just jump us up to
[32:37] to this chart. It never passes 80%.
[32:41] Right? This is the chart we saw earlier.
[32:43] 80%, why why is it not performing better
[32:46] on the test? Because it's overfitted the
[32:48] training data. And there's a huge gap
[32:50] between test and train which tells us
[32:52] this overfitting. Okay, what if I bump
[32:54] up the weight decay to a very small
[32:57] value? I'm going to go back down here
[33:00] and look at how the very very small
[33:02] value performs. Still no change. 80% uh
[33:06] on test. That tells me there's
[33:08] overfitting because I know the
[33:10] characteristics of the data set and a
[33:12] massive gap between train and test loss.
[33:15] Still very bad. Great. Let's dial weight
[33:18] decay up again. Still we're gonna see.
[33:21] Oh my god. Massive gap. Still 80%. Not
[33:25] good. 0.01. Is that going to get any
[33:28] better? I don't know. Let's see. Well,
[33:30] it's still 80% train trend. It's still
[33:33] overfitting, but the gap has gotten a
[33:35] little bit smaller. That tells me we're
[33:37] in the right direction, but we're going
[33:38] to need to do a lot more.
[33:41] Great weight of 0.1. Now we're talking.
[33:44] Now we're getting spicy. Right? You
[33:47] could kind of see it reaches 90% test
[33:50] loss, right? Which is uh sorry 90% t uh
[33:54] 90% test accuracy at about 99 actually
[33:58] it reaches it much further much earlier
[34:00] than that. It reaches it here at epic
[34:03] 77.1
[34:06] reaches uh 90% test accuracy. If we were
[34:09] fair to this algorithm and we just stop
[34:11] we would just stop executing it then cuz
[34:13] there's no way for it to get to 100%. We
[34:15] just didn't give it enough good data to
[34:17] be able to do that. We gave it a bunch
[34:18] of noise. So really success should be at
[34:20] about epic 77. But I'm not fair. So I
[34:23] just kept running it forever. And so and
[34:25] actually test does improve and does
[34:27] improve and does improve. You can maybe
[34:28] run it. Maybe it'll get to 100% at some
[34:30] point, right? Because it could
[34:31] potentially generalize at some point or
[34:33] another. Great. Because it is getting to
[34:35] better percentages on both train and
[34:37] test, but it never reached 100%. But
[34:40] it's getting there, right? It's really
[34:41] cool. It's great. It's ignoring some of
[34:43] the noise while it's scoring well on the
[34:45] train data.
[34:47] Okay, so now that I know 0.1 is actually
[34:49] work and then let's see the chart. Oh my
[34:51] goodness, this chart is really really
[34:53] important. It shows us that there isn't
[34:56] this massive gap between train and test.
[34:58] And actually both train and test pass
[35:00] 0.9. That tells me we've fixed
[35:03] overfitting. Oh my goodness, weight
[35:05] decay.1 fixed overfitting in both of our
[35:08] charts. Isn't that great? Finally, I can
[35:10] add clipping. So, clip grad equals true.
[35:14] And then see what that does. Huh. When
[35:17] are we going to reach 90% uh uh on the
[35:21] accuracy for test? That's going to be an
[35:23] epic 59. So, we've actually arrived at
[35:26] like the most reasonable interpretation
[35:29] of what a good train accuracy could be,
[35:30] test accuracy could be here. And we
[35:32] arrived at it about 25% steps epics
[35:36] earlier. That's really great. Just
[35:40] adding value nor val sorry gradient norm
[35:44] clipping we've been able to arrive much
[35:47] sooner at this uh solution of 90% test
[35:50] accuracy. Isn't that amazing? Right?
[35:53] Amazing. All I wrote is one line of
[35:55] code. We save 25% compute if this was
[35:58] our real goal. And when I keep running
[36:00] it, you can see it's actually doing
[36:02] pretty well. It's also arriving at 95%
[36:04] train accuracy. a bit higher than we got
[36:07] earlier and 93% te uh test accuracy even
[36:11] a tiny bit higher than we did earlier.
[36:14] Great. And again the charts clearly
[36:16] indicate there's not a lot of
[36:17] overfitting. I'm not a fan that test is
[36:21] now like a tiny bit overfitted but I
[36:24] think this is fine. This chart reads
[36:25] normal to me. Great. So let's put all of
[36:28] these in the same uh chart together to
[36:30] create the single most confusing chart.
[36:32] What you could see is there's a lot of
[36:34] test loss separation between test and um
[36:40] uh uh between the various runs, but the
[36:43] ones that perform best are weight decay.
[36:45] 01 sorry 0.1 and weight decay.1 plus
[36:49] clipping. Those did really well. We
[36:51] could also see the test accuracy by
[36:53] dropout rate. Really only weight
[36:55] decay.1.
[36:57] Those two runs did as well as we could
[36:59] expect.
[37:01] Finally, we could see that uh weight
[37:04] decay 0.1 10% while they didn't
[37:07] converge, they did a lot better than the
[37:09] other runs. So, that teaches us a lot
[37:12] about regularization. Why didn't I have
[37:14] an example for you for dropout? That's
[37:16] going to be your exercise. I think you
[37:19] should go ahead and try and duplicate my
[37:21] notebook code 13 and then try and do a
[37:24] sweep of all of the dropout values we
[37:27] could be supporting. So duplicate my
[37:29] notebook, try and test drop at 0% 5% 10%
[37:33] all the way to 50% and then try and add
[37:35] a little bit of weight decay to see if
[37:36] that helps. I did write this notebook
[37:38] for you ahead of time. And I'm just
[37:40] going to scroll to the results. What
[37:42] happens when we do that? We can see that
[37:45] actually dropout not super effective. It
[37:48] does help us get to like a better
[37:50] Teslas, but it's never going to be
[37:53] weight decay. Maybe that like you can
[37:55] see that in the final test accuracy.
[37:57] Maybe that's why we don't really use a
[38:00] lot of dropout. We don't see it as
[38:02] common. It just underperforms to the
[38:04] other methods. Great. So, let's make a
[38:08] couple of decisions here. You've got
[38:09] Stella Berman's amazing amazing Google
[38:12] sheet. This person went ahead and write
[38:14] like 30 papers for our benefit back in
[38:16] 2023 as part I assume as part of their
[38:19] job. And then uh they listed hey what is
[38:23] the clipping that happens? What's the
[38:24] max clip that we have got? What's the
[38:26] dropout that models have? What's the
[38:29] weight decay that everyone's using? You
[38:31] could pretty much see what the numbers
[38:33] mean, right? If you're using dropout,
[38:35] you're using it at 10% in large language
[38:37] models. If you're using clipping, you're
[38:39] going to max it at 10. Almost all of the
[38:42] all of these are going to be norm, not
[38:44] value. And in weight decay, most people
[38:47] don't use more than.1, right? That's
[38:49] generally the consensus. So, pretty easy
[38:51] for us to copy those values. Dropout
[38:54] rate 10%, weight decay at 10%, gradient
[38:56] clipping at 10. A couple of architecture
[38:59] choices we're going to make is dropout.
[39:02] We will include it in our GPT2 training
[39:04] run even though it's super ineffective
[39:06] and just going to make it run longer. I
[39:08] think it's just still valuable to see it
[39:10] run. Gradient norm clipping is going to
[39:12] be enabled. And then we set what our
[39:14] maximum is going to be. And then
[39:15] obviously we're using weight decay.
[39:18] Great. So now we finished all of our
[39:20] regularization, normalization,
[39:23] initialization
[39:25] kind of techniques to work with deep
[39:26] neural networks. We are almost
[39:28] completely done with anything that has
[39:30] that isn't all about large language
[39:32] models that that is deep neural networks
[39:35] that is reapplied to large language
[39:37] models. Now we're going to approach the
[39:39] stuff that's actually needed to just
[39:41] learn large language models. But before
[39:43] we do that, one last topic we'll cover.
[39:46] I don't expect it to take more than 10
[39:47] 15 minutes is we'll talk about softmax.
[39:50] What does softmax do? It converts logits
[39:53] random numbers that are activations at
[39:55] the end of a network to probabilities.
[39:58] Why is that important? Large language
[40:00] models communicate nothing but
[40:02] probabilities. Right? We 5% the dog set
[40:05] on the mat, the car, the chair, right?
[40:08] All of these need their own
[40:09] probabilities. Softmax is the thing that
[40:11] does that. So we'll cover that. It's one
[40:13] really quick formula and then we're off
[40:15] to getting into tokens and embeddings
[40:17] and all of the stuff that's language
[40:18] specific. We'll eventually reach
[40:20] pre-training and so on and so forth.
[40:22] Great. I hope to see you in the next
[40:24] section. Bye-bye.
