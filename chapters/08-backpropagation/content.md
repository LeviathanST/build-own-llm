# Backpropagation | Build Your Own LLM Workshop #8

**Build Your Own LLM Workshop — Video #8 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 56m 57s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=Zf6RC6KZxKg |

## Description

No description available.

---

## Full Transcript

[00:00] Hello and welcome back to build your own
[00:03] large language model workshop with me
[00:05] Justin Angel. Now in our eighth section
[00:08] we're going to be talking about back
[00:09] propagation. We just left off from loss
[00:12] function which tells us the distance
[00:14] from how far we need to go to get to
[00:17] your ideal performance specifically
[00:19] learning the English language. And now
[00:21] we're going to be talking about how we
[00:22] actually traverse that landscape um all
[00:27] the way to speaking English. Um so our
[00:30] deliverables for this section are
[00:32] training loop specifically how do you
[00:35] train machine learning models? We don't
[00:36] know because we're not machine learning
[00:38] engineers. The atom optimizer stochastic
[00:41] gradient descent bat size and learning
[00:43] rate. Lots and lots of stuff we're going
[00:45] to cover here. I literally used
[00:47] abbreviation because I didn't have room
[00:48] to write all the deliverables.
[00:52] All right, so let's go to our demo. And
[00:55] this demo is like our final and last
[00:57] demo of our neural net kind of like
[00:59] analog perceptrons. So here we have a
[01:02] single perceptron with an input, a bias
[01:04] and a weight. Inputs are like not
[01:06] learnable parameters. We change them all
[01:08] the time, but bias and weight learnable
[01:10] parameters. So we want to learn the best
[01:12] bias and the best weight for uh the
[01:16] target that we have here. So let's say
[01:18] with for input one we want to have a
[01:21] target of minus1 right that and
[01:23] currently the output of this network is
[01:26] 7. So what does that tell us?
[01:29] That tells us that we are about.3
[01:33] away from the target. Sorry 1.7 away
[01:35] from the target because it's negative.
[01:36] So 1.7 away. And the question here is
[01:39] can we use that residual error that uh
[01:44] seven
[01:47] minus -1 so 1.7 can we use that 1.7 to
[01:52] actually back propagate
[01:55] the updates we're going to need for bias
[01:57] and weight right so through the magic of
[02:00] calculus we're able to do that we'll
[02:02] talk more about calculus in this section
[02:04] a lot but for now I just want to click
[02:06] this learn like this update weight and
[02:08] bias button and I want you to see that
[02:11] currently our output is 7. We want to
[02:13] get to minus one. I click it once
[02:16] the update gets a the bias and the
[02:18] weight got updated but now our output
[02:20] is.3. We went down closer to the minus1
[02:24] value and now our loss function is
[02:27] smaller. I'm going to click it again and
[02:29] now we're going to go from bias. 03 to
[02:33] 33 weight and we're going to go down and
[02:36] then the output goes down again with the
[02:38] loss the weight and the bias update. I'm
[02:40] going to keep clicking this button and
[02:42] you can see that within about six turns
[02:44] we've arrived at roughly the output that
[02:47] we want to be in or like maybe about
[02:48] closer to 10 turns. Right? So now the
[02:52] question here is is how did we do that?
[02:55] Right? So back propagation takes the num
[02:58] the loss that we have accumulated. It
[03:02] does a bunch of calculus derivatives and
[03:05] arrives at what is the amount by which
[03:08] we need to change the bias and the
[03:10] weight um in order to get closer to
[03:14] minimizing that loss function. Why can't
[03:16] we just do that in one churn? That's a
[03:18] great question. I'm going to hit the
[03:19] reset button. Okay, so now we're back to
[03:21] the original state. I'm going to bring
[03:23] up our learn rate to a value of one. A
[03:26] value of one. And you could see here
[03:30] what this loss function actually wants
[03:32] to do with 1.7, right? Like loss
[03:35] function of 1.7. It actually wants to
[03:37] update the bias to minus 1.5 and the
[03:39] weight to minus 1.2. That seems really
[03:42] excessive to me just looking at these
[03:44] numbers because we're trying just trying
[03:45] to get to minus one. So what happens if
[03:47] I click this button now? Bam. All of a
[03:50] sudden, the loss isn't even reducing,
[03:53] right? The loss is just alternating
[03:56] between plus and minus, plus and minus,
[03:57] plus and minus. Doesn't really work
[04:00] super well here, right? We can't just
[04:02] like do everything the derivatives of
[04:04] the calculus tell us to do. We have to
[04:06] kind of discount these rates a bit. So,
[04:08] I'm going to reset again, and I'm going
[04:10] to set our learn rate to let's say
[04:12] 0.5ish.
[04:14] And now you can see, oh my god, the loss
[04:16] is actually descending pretty quickly.
[04:17] And that's actually really good. We
[04:19] wanted an output of minus1 at target of
[04:21] minus1 we arrive there within one turn.
[04:24] So it's possible when we play with learn
[04:26] rates to actually get there faster and
[04:28] slower. Okay. So let's look a bit again
[04:30] at uh really higher learn rates. Now I'm
[04:32] going to click update again. I'm going
[04:34] to show us what the weight and the bias
[04:38] values are. And every time I click it,
[04:40] the weight bars go up and down, up and
[04:42] down, up and down, up and down. we're
[04:44] wasting a lot of cycles on bringing the
[04:47] weight values up and down up and down
[04:48] where we could have just brought them
[04:50] more uh more closely in a more
[04:53] controlled way. So let's now bring the
[04:54] learn rate further down and maybe this
[04:56] will teach us what learn rate is. Learn
[04:59] rate is that's the amount by which we
[05:01] discount how much the weight and bias
[05:03] are updating. Right? So you can see here
[05:05] these are tiny updates. Many many turns
[05:08] are going to take for us to get to our
[05:10] minus one final output. Right? And it
[05:12] actually just this demo just stops at
[05:14] about 60s something sections. Great. So
[05:19] now we learn super low learn rate. When
[05:21] we discount everything to a very very
[05:23] small amount, it actually takes so long
[05:26] for things to converge. We have to spend
[05:27] so much more time. Super high learn
[05:29] rate. Learn rate. What we end up seeing
[05:32] is that there's these weird up and down,
[05:34] up and down, up and down, up and down.
[05:36] It'll never actually converge if it's
[05:38] too high. It'll always miss. But there's
[05:41] somewhere in there maybe a nice sweet
[05:43] spot that we know is going to work for
[05:44] everything right 0.1 uh we we've also
[05:48] seen that.5 works really well for this
[05:50] particular demo generally we use 0.1 to
[05:53] discount the results of stoastic
[05:55] gradient descent which is this back
[05:56] propagation process okay cool so we
[05:59] looked at this demo let's talk a bit
[06:00] about stoastic gradient descent and
[06:03] again our problem is that random updates
[06:05] won't teach the model English we have to
[06:07] use some sort of compass to know the
[06:10] direction by which we want to go to and
[06:12] then re uh and then reduce the loss over
[06:15] time to teach the model English.
[06:17] Stoastic gradient descent uses the loss
[06:19] function to optimize the learnable
[06:21] parameters specifically weight and bias
[06:23] in the direction of minimizing loss.
[06:27] Metaphorically
[06:29] it walks or climbs down a mountain in
[06:32] the direction that appears to get us to
[06:34] the bottom fastest.
[06:36] and SGD uses calculus derivatives to
[06:38] determine how each step should be uh
[06:41] updated. What do you mean by calculus
[06:43] derivatives? Okay, I'm so sorry. Now I
[06:45] have to show you some calculus. So we
[06:47] remember from
[06:49] calculus from wherever we learned it
[06:51] from that x^2
[06:54] that its derivative is actually 2x.
[06:57] Okay. So what is that derivative? What's
[06:59] the number two? That's actually the
[07:00] slope. Why are the slopes important?
[07:03] because again we're in a lost landscape
[07:05] and we're trying to like look at the
[07:07] slope of the lost landscape to determine
[07:09] how fast we want to walk down that
[07:10] landscape. So the when we change our x
[07:13] we uh like the weight that we said here
[07:16] we also change the slope if this was our
[07:18] lost landscape. Really interesting
[07:21] calculus ends up being the perfect tool
[07:23] for doing back propagation of finding
[07:25] the slopes when we walk down a lost
[07:27] landscape. Um it enables us to look at
[07:30] like the current performance of the
[07:33] system, the next step's performance of a
[07:34] system like the previous steps and then
[07:37] see the slope between those two things
[07:39] and then decide how fast we should
[07:41] navigate that landscape. The derivatives
[07:43] determines both the direction and the
[07:45] speed in which we walk down a lost
[07:47] landscape. That's really important for
[07:49] us cuz so far all we had is direction.
[07:53] Uh all we had is the direction but not
[07:56] the speed. Okay. So now I'm going to
[07:57] show you chain rule. You're not going to
[07:59] have to know any of this ever if you're
[08:00] ever going to write code for like large
[08:02] language models, but I've been given
[08:04] feedback from this workshop that people
[08:06] want to learn about the chain rule. So
[08:07] I'll do it with you. So the chain rule
[08:09] is kind of how we've uh proven that the
[08:13] various derivatives as we're back
[08:15] propagating actually make sense. What is
[08:18] the chain rule? It says that the
[08:19] derivative of zed in its relationship to
[08:22] the derivative of x is actually a
[08:23] function of the derivative of zed
[08:25] divided by the derivative of y in rel
[08:27] multiplied by the derivative of y
[08:29] divided by the derivative of x. Let's
[08:31] say that in English, not the word
[08:33] derivative over and over again. How much
[08:35] zed changes in relation to x is actually
[08:37] a function of how much z changes in
[08:40] relation to another parameter y and how
[08:42] much y changes then in relation to x.
[08:45] Okay. So, that's a really obscure way of
[08:47] saying whatever it is you're trying to
[08:48] say. Justin,
[08:51] a muffin taste in the relationship
[08:53] between a muffin's taste and the baking
[08:57] times for that muffin is actually the
[08:59] relationship between a muffin the taste
[09:02] of a muffin and how much it brown.
[09:04] Whereas browning is a function of baking
[09:07] time. So if we know both of those
[09:09] things, we can like start like filling
[09:11] in this formula and add more values
[09:13] here. Uh in machine learning, what we
[09:17] already have is the derivative of loss,
[09:20] right? We have loss and as a result we
[09:21] have the derivative of loss and we have
[09:24] the current values of X like the weight
[09:26] and the bias. So maybe we can like
[09:29] figure out how to get the correct and
[09:32] updated values of X and of like weight
[09:34] and bias in relationship to the loss.
[09:37] The chain rule derivation you see in the
[09:39] last bottom right square here actually
[09:42] shows you how we get how we derive that
[09:44] specifically for residual errors. And
[09:47] then it's really interesting. It's
[09:49] effectively just the error times the
[09:50] input. Error being the output minus the
[09:54] expected output multiplied by the input.
[09:57] So this is how you derive chain rule.
[09:59] You don't have to know any of this. This
[10:01] is totally fine. This is to let you know
[10:04] that the back propagation kind of like
[10:06] the multiple steps you have to do uh is
[10:09] backed by some amount of calculus and
[10:11] some amount of rules within calculus.
[10:13] One of them being the chain rule. Okay,
[10:15] so we kind of built that intuition
[10:18] Justin uh do I really need to know all
[10:20] of this? Well, let's try and do a little
[10:22] bit in Excel and then see if you
[10:23] actually how much of this do you
[10:24] actually need to know? And in this in
[10:27] this uh Excel spreadsheet
[10:30] uh you're not going to actually have to
[10:32] fill in any formulas. I filled out all
[10:33] of the formulas ahead of you. What we
[10:35] are going to do is we're going to play
[10:37] around with numbers and what they do. So
[10:39] we have here our network from uh demo
[10:42] number I want to say five 3
[10:47] 1. Which demo is this? This is demo
[10:51] number three. Great. So we have that
[10:54] demo. So we have our feed forward
[10:56] network it has two neurons input one and
[10:58] a half the weights of the me the network
[11:02] the bias the value and I want to say
[11:04] that instead of a value of 3.1 I expect
[11:07] a value of four okay so that creates a
[11:10] residual of 0.9
[11:13] and then back propagation literally
[11:15] walks up that tree we do some
[11:17] derivatives we're not going to talk
[11:18] about why and what how we we derive
[11:20] these and then oh my goodness it's like
[11:23] minus 1.8 A and that tells it how much
[11:25] back propagation wants to update. We
[11:27] have our learning rate which is the
[11:28] amount by which we multiply right the
[11:31] these updates and the previous values.
[11:34] And then one is going to be pretty big.
[11:36] Why? We've seen this before that
[11:38] updating using a full one learn rate
[11:42] will actually cause things to to
[11:43] escalate up and down. So, if I paste in
[11:46] these numbers here, instead of negative
[11:48] back propagation to change these
[11:50] numbers, we're going to see it wants
[11:53] positive back propagation. And here we
[11:55] go. Now, it wants the numbers to go up.
[11:57] I copy these numbers in here. It's going
[12:00] to want the numbers to go back down. Oh
[12:02] my god. It's not It's out of control.
[12:04] It's totally out of control. Right? A
[12:06] learn rate of one is like
[12:07] uncontrollable. Let's try and get to
[12:09] like 0.1, right? And then we're trying
[12:12] to get our value to go from 3.1 to
[12:15] something closer to four. So with a
[12:17] learn rate of um a learn rate of 0.1,
[12:21] I'm going to copy the new values the
[12:22] network wants us to use, background
[12:24] wants to use, we got to 3.5. That's
[12:26] actually pretty close, right? We got
[12:28] almost halfway to what we were looking
[12:31] for. So something really important to
[12:33] notice, learn important. And back
[12:35] propagation just walks up the chin using
[12:37] derivatives from calculus. So play
[12:40] around with the learning rate, copy a
[12:41] lot of these values, get an intuitive
[12:43] sense for back propagation. Next up, we
[12:45] don't have to have a simple network. We
[12:47] can have a very complex network of two
[12:49] neurons with a relu function and then
[12:52] another output and then a sigmoid
[12:55] activation function. Why sigmoid? Cuz
[12:56] that's what I wanted for the sample.
[12:59] And we could say that currently the
[13:01] network outputs 8.4 and I expect it to
[13:04] be.3. So my residual error is 0.54.
[13:08] Great. So now we could traverse all of
[13:10] that all the way up the chain with
[13:12] derivatives. The derivative of the loss
[13:13] is the derivative of yhat. The the
[13:16] derivative of of the output neuron which
[13:18] is sigmoid here. The derivative of this
[13:21] set of biases like of these of this bias
[13:24] and these set of weights. And then okay
[13:26] let's try and op and then finally we get
[13:29] the final values that we should have um
[13:32] for our neurons. Great. So I'm going to
[13:34] just copy these here to the side so I
[13:36] don't lose them. And I'm going to do
[13:37] this update in two turns. I'm going to
[13:39] copy these here. And I'm going to copy
[13:41] these here. And we went from being at,
[13:44] let's see, we were at uh84 and now we're
[13:48] at 76. We got closer to.3. Very cool.
[13:52] And you can kind of see, and this is the
[13:54] most important thing to take from this
[13:56] demo, isn't what are the specific uh
[13:58] calculus maneuvers we pulled is that
[14:01] actually every one of the weights and
[14:02] biases has to be updated individually.
[14:05] we have to work our way up the chain to
[14:07] do uh calculus back propagation. Okay,
[14:11] great. So, you should play around with
[14:13] the learning rate here and you should
[14:14] play around with pasting values over and
[14:15] over and over again. Let's get to our
[14:18] almost small large language model
[14:22] here. It's not really that. It's just
[14:24] something that uses cross entropy. And
[14:26] again, we're just trying to find the
[14:27] first digit of the input. Our input is
[14:29] nine, which tells us that our target
[14:32] class is 9 as well. So if it was 9.1 it
[14:35] would be nine. If it was 9.2 it would be
[14:37] nine. That would be our target class
[14:39] which means that in targets here we're
[14:41] going to have zero for every other
[14:43] target. That's our ideal probability for
[14:45] all of the other numbers. We're trying
[14:47] to find the first digit of nine. So the
[14:49] correct answer is we want 100% to be on
[14:52] the digit nine. Um based on that we can
[14:55] see that we have a bunch of logits
[14:58] and then these are derived from uh the
[15:02] neuron value. Oh so we have the input we
[15:05] have the way we have the bias that gives
[15:06] us the neuron value right and then we
[15:09] have a bunch of logits uh outputs for
[15:13] this network and it gives us kind of
[15:14] like this uh bar chart. Okay, so these
[15:19] are the output logits and these are the
[15:21] classes.
[15:23] As a result, it ended up predicting that
[15:26] the correct answer is number n. Number
[15:28] eight. So we predicted uh our actual
[15:32] expected is nine. Our predicted is
[15:35] eight. That's no not good for us. We
[15:37] want to find a way of pushing these
[15:39] numbers so it's closer to number nine.
[15:41] Okay. So we're going to back propagate.
[15:43] How does back propagation work? Again,
[15:45] there's a bunch of math derivatives that
[15:46] we're not going to like fully derive the
[15:48] formulas for, but what's important is it
[15:50] has is recommending some change to the
[15:53] weight and bias of this one neuron. And
[15:55] then we can like multiply that by a
[15:57] learning rate. And then I'm going to
[15:59] have a very small learning rate here of
[16:02] 0.01 and a weight of 0.92 and a bias of
[16:06] 0.02. So that's a very small update to
[16:08] make to this network. I'm going to copy
[16:10] in these values. Oh my god, we didn't
[16:13] get close enough. Let's try and update
[16:15] that to let's say 0.1. Okay, so now it's
[16:18] at 0106 and 16. I'm going to copy this
[16:21] here. Oh my god, all of a sudden our
[16:24] network predicted the right number. The
[16:27] highest probability went to the digit 9.
[16:30] Isn't that cool? So you can kind of see
[16:32] the impact of how many times you're
[16:33] going to have to do uh an update in back
[16:36] propagation based on learning rate. You
[16:38] also saw how cross entropy this learn
[16:41] this loss function we saw earlier gets
[16:43] impacted by back propagation. Again each
[16:45] loss function because it is a function
[16:47] derives a bit differently and here you
[16:49] have the full like some portion of the
[16:51] derivatives if you're interested in
[16:53] great. So we saw an excel demo uh you
[16:56] have a bunch of exercises to play around
[16:58] with these uh learning rates yourself
[17:00] and play and copy these new values to
[17:02] build an intuitive understanding of how
[17:04] back propagation works.
[17:07] You're never going to do this calculus
[17:09] by hand. This is never going to happen.
[17:12] Uh I don't like unless you're like doing
[17:14] uh some ML research that is trying to
[17:18] find a new optimizer. I guess maybe
[17:21] something else. There's like maybe a few
[17:23] times. But as you're building a large
[17:25] language model, you're always never
[17:26] going to like do this yourself. Why?
[17:29] Specifically for us, we mentioned we're
[17:30] using the PyTorch library. Uh the
[17:33] PyTorch library we mentioned gives us
[17:35] tensors which are things that live on
[17:36] the on the GPU. Gives us tens uh GPU
[17:39] operations. Really great. Gives us a
[17:41] bunch of built-in functions. Even
[17:42] better, it also gives us this thing
[17:45] called PyTorch or Autograd which stores
[17:48] in memory all of the forward passes
[17:50] because we need the forward pass in
[17:52] order to then do all the derivations of
[17:55] backward of doing backward passes. It
[17:58] also maintains the optimizer state.
[18:00] We'll talk about what about optimizer in
[18:02] a second which have like a full history
[18:04] of all of the various steps we took.
[18:06] Justin holding the entire feed forward
[18:09] in memory holding the entire grade
[18:12] current gradient derivation in memory.
[18:15] Holding the entire history of whatever
[18:17] the optimizer state used to be. That
[18:19] sounds really memory intensive. I'm
[18:21] going to get out of the slide deck. I'm
[18:23] going to make this a lot bigger. Oh my
[18:26] goodness.
[18:28] Delete.
[18:30] We can see here that the actual weights
[18:32] and biases in memory of the parameters,
[18:36] right, are actually like a small portion
[18:39] of the size of models, right? The
[18:41] gradients are also kind of important.
[18:43] The gradient is just the jump between
[18:45] this point and the previous point. But
[18:47] the optimizer state that holds a lot of
[18:48] statistics about all of the various
[18:50] steps that actually takes a lot of
[18:52] memory. Why do we care about how much
[18:54] memory things take? Aren't isn't memory
[18:56] infinite? No. We want as many things to
[18:58] fit on a single GPU and a single GPU has
[19:01] let's say a 40 GB, let's say 80 GB,
[19:04] let's say 1860 GB RAM maximum. So like
[19:08] it's really not RAM um GPU memory. So
[19:11] it's very important that we kind of
[19:13] manage that memory effectively. Okay,
[19:15] great. I'm going to turn the slideshow
[19:17] to the way it was a moment ago before I
[19:19] deleted stuff. Let's talk about autograd
[19:21] for another moment. So again, autograd
[19:23] holds all of the me all of the feed
[19:26] forward pass and then it does our
[19:28] backward pass for us. That's actually
[19:30] really great because that means we don't
[19:32] have to uh do that ourselves.
[19:37] So let's talk about train and test data
[19:39] sets. And I'm going to talk about a
[19:40] really basic data like basic example.
[19:43] Let's talk about a + b modulus 5. So 2 +
[19:49] 3 modulus 5 remainder of 5 is zero.
[19:53] Right? 1 + 2 remainder of five is three.
[19:57] Right? So let's say we built up that
[19:59] data set and we have a 10,000 rows in it
[20:02] or however many rows. I want to test
[20:05] that my machine learning model that's
[20:07] going to predict the outcome can
[20:09] generalize on unseen data. Obviously
[20:11] it's pretty easy to just do that math.
[20:12] But I want to see that if I hold back 20
[20:15] or 30% of data, it actually does that
[20:18] successfully. So here you can see an
[20:20] illustration of what the data looks
[20:22] like. And in black, you could see us
[20:24] hiding away 20 to 30% of the data. I
[20:27] think here we're hiding away 30% of the
[20:29] data. So we could see that a plus b
[20:32] modulus 5 has these beautiful diagonal
[20:34] patterns that we want the model to
[20:36] learn. That is the math that the model
[20:38] is trying to learn, those diagonal
[20:40] lines. And then if we hide away 30% of
[20:43] the data, can it still learn those
[20:44] lines? What if I show it one of those
[20:46] pieces of math that it it's never been
[20:48] trained on? Can it predicted? Can the
[20:51] model generalize? That's what we're
[20:53] really trying to test here. So we call
[20:55] that a train data set and a test data
[20:58] set. Train data set is the data that we
[21:00] trained the model on. And the test data
[21:01] set is the data we withhold to then
[21:03] later check if it generalized. Great.
[21:06] Importantly, large language models train
[21:09] on nwords with the n plus word being the
[21:12] prediction. What does that mean? This is
[21:14] the first time we've said that. The
[21:16] sentence, the cat said on the mat, the
[21:19] cat said on is going to be our data set
[21:22] and our trained is going to be our data.
[21:25] And we want to see if it could predict
[21:27] the word matt later on. If all it saw in
[21:30] completion there is like the word math.
[21:33] Great. So, we learned about training. We
[21:35] learned about uh test data set. What
[21:38] else are we going to learn about? We're
[21:39] going to learn about learn like learn
[21:40] rate. So we we always like as we always
[21:43] do we we can see a formula here. Then
[21:46] there's like the English version of that
[21:48] formula like the plain English version
[21:49] of it. New values equals old values
[21:52] minus the loss gradient. We said we
[21:54] we're going to look at the gradient like
[21:56] how much what's the difference between
[21:58] our this step and the previous step do
[22:01] multiplied by the learning rate. We know
[22:03] that a learning rate of one is way too
[22:04] much. for basically everything. But we
[22:06] know that like a learning rate that's
[22:08] too slow takes too long to converge. So
[22:10] we can see it LR.1
[22:12] 1% took us about 60 steps to converge.
[22:15] We can see LR1 it took about 16 steps to
[22:17] converge. We can and we can see that
[22:20] LR.1
[22:22] took about six steps to converge. Why
[22:25] this number of steps we had to take
[22:26] important? Well the difference between
[22:29] LR.01
[22:30] and 0.1 is about 10x difference of
[22:33] steps. That's 10 times more GPU time
[22:36] than you're going to need. That's very,
[22:38] very expensive. You really, really want
[22:41] to get the LR just right. So, like just
[22:44] crank up the learning rate, I hear you
[22:46] saying. Well, then you're going to hit
[22:48] this problem of the zigzagging weight
[22:49] and biases. That's also really bad. So,
[22:52] we should probably like and then we end
[22:54] up wasting three times more than the
[22:57] ideal learning rate. So we can see here
[23:00] that learning rate really impacts how
[23:02] much GPU time we need by multiple
[23:05] multiplications right one of these point
[23:07] is three times more one the other one is
[23:10] 10 times more two that's lots of money
[23:12] that's millions of dollars if you're
[23:14] training a large language model that's
[23:15] commercial okay so we don't want to
[23:19] undersshoot and we don't want to
[23:21] overshoot right when we oscillate
[23:24] uh so how do we like what what do we do
[23:26] about that Well, so one thing that's
[23:29] become very common in uh training large
[23:32] language models is to not have a single
[23:35] learning rate, but instead warm up the
[23:37] learning rate to a very high value very
[23:39] quickly and then slowly descend from
[23:42] that value or descend from that value.
[23:46] So over here in purple what you can see
[23:49] is the small LM3
[23:52] learning uh learning rate uh warm-up and
[23:55] you can see it increases very very
[23:57] quickly. The reason for that is earlier
[23:59] on in the earlier steps it's very easy
[24:01] to get the loss to decrease. It doesn't
[24:03] really matter what direction you walk in
[24:05] you're kind of going to like get lost to
[24:06] decrease but after that you want to
[24:08] start taking smaller and smaller steps
[24:10] and there's multiple ways of taking
[24:11] these small steps. We call that decay.
[24:14] So one option is to decay with a cosine.
[24:16] Another one is to just do a straight
[24:18] drop. Another one is to do like little
[24:21] steps and another one is to do a linear
[24:23] decay. It doesn't really matter which
[24:25] one you choose. There's like a lot of
[24:26] research on this. You there is some
[24:28] difference and you just have to choose
[24:30] one. There's ways of running ablation
[24:32] test. But generally the important thing
[24:34] to remember for our slides for our
[24:36] purpose right now we want to have
[24:38] warm-up and we want to have decay. For
[24:40] our very small model, we can use
[24:42] ablation test to figure out the right
[24:43] one. But for now, it's just important to
[24:46] know what the warm-up and then decay
[24:48] exist. Okay. So now we have this like
[24:51] chart on the bottom and the words
[24:52] choosing a stable uh learning rate. Why
[24:55] is that important? Like is there an
[24:57] ideal learning rate for our model? So
[25:01] Quen 3 ran a bunch of learning rate
[25:03] ablation tests. Each one of the lines in
[25:06] this chart rec is a amount of compute
[25:09] that they've given all of the models on
[25:10] the same line share the same amount of
[25:12] compute and what we can see here is that
[25:15] for those same models actually there is
[25:18] an ideal learning rate and if you change
[25:20] the size of the model oh my or change
[25:23] the amount of compute then oh my god
[25:25] there's another learning rate that's
[25:26] ideal and another learning rate that's
[25:28] ideal and another learning rate that's
[25:29] ideal as you keep changing the compute
[25:32] each compute amount of data data
[25:36] ends up having its own ideal learning
[25:39] rate. So finding that scaling law of
[25:42] what is your ideal learning rate
[25:44] actually really helps. I want to just
[25:46] highlight something from an earlier
[25:47] slide that was written and I didn't say
[25:49] learning rate might be the single most
[25:51] important hyperparameter is the
[25:52] consensus. Why? Because we can we can
[25:55] like shave multiplication of training
[25:58] time off it. This research tells us
[26:00] there is actually an ideal learning rate
[26:03] for our models. Super important to then
[26:06] find it not maybe for our toy model of
[26:08] 124 million not toy small language model
[26:11] of 124 million parameters but it's much
[26:13] more important when you're like playing
[26:15] around with larger models. Uh great. So
[26:19] now let's talk about optimizers.
[26:21] What what what's important for us to
[26:23] know about optimizers? This is the whole
[26:25] like univers graduate class level class
[26:28] of like how to learn about uh changing
[26:31] the weight and biases using back
[26:33] propagation. And I'm going to try and
[26:34] summarize it here in maybe two slides.
[26:37] So not going to be super in-depth. Let's
[26:39] start by looking at this chart on the
[26:42] point that says SGD the point in red
[26:44] right you can see SGD is moving kind of
[26:48] slowly. That's going to be the polite
[26:50] way of saying that. Why don't we want to
[26:51] move slowly? More update steps mean more
[26:54] GPU time means more money. We want to
[26:57] get as close as we can to our goal as
[26:59] fast as we can. So we can see there's a
[27:02] bunch of options that we haven't yet
[27:04] learned about. SGD being the option that
[27:07] we just learned about. And then there's
[27:09] a bunch of other options. to momentum.
[27:12] Um, one thing that it does is it looks
[27:15] at the previous steps and then it
[27:16] decides, hey, based on how fast we've
[27:19] moved, we can actually adapt how fast
[27:22] we're going to go down the slope. So, if
[27:24] the slope is very steep, we can have a
[27:26] very low momentum. If a slope is slope
[27:30] is not very steep, we can actually
[27:32] accelerate a bit and try and get
[27:33] ourselves out of this point. Right? So,
[27:35] that's what momentum does. 1964
[27:38] Adagrad said hey hold on a moment
[27:41] momentum you're using a global value but
[27:44] our networks now have millions hundreds
[27:46] of millions billions of weights and par
[27:48] and biases millions of learn billions of
[27:50] learnable parameters we probably don't
[27:52] want to have a global learning rate
[27:54] right we want to accumulate them per
[27:56] parameter per weight so that's what
[27:59] addrad added to the equation rms prompt
[28:02] from hinton 2012 not even a paper Jeff
[28:06] Hinton going on a podcast or something I
[28:09] think Corsera and then said actually
[28:12] instead of accumulating over thousands
[28:14] of steps super irrelevant takes lots of
[28:17] memory let's favor the most recent pair
[28:20] parameter steps saves on memory and also
[28:23] much more accurate because if you went
[28:24] to a slope and a trough and a slope and
[28:26] a mountain a slope you don't need to
[28:28] know what happened several mountains ago
[28:29] that's just not super effective when
[28:31] trying to learn like trying to optimize
[28:34] uh a large language especially if you're
[28:36] memory constrained, which we are always
[28:38] memory constrained. That's an
[28:40] oversimplification. Sometimes we're
[28:41] computed, but let's pretend we're always
[28:43] memory constrained. Okay, great. So now
[28:45] we have these two competing things.
[28:47] Adigrad said we have to move away from
[28:49] global LR um and move to pair parameter
[28:53] optimization. RMS prompt said no no you
[28:56] have to like take away you have to stay
[28:58] global um global gradient at like at a
[29:02] global LR but then you have to still
[29:05] accumulate globally okay in comes atom
[29:09] is just the f most rec the second most
[29:12] recent family of optimizers which
[29:15] combine both of those things so it said
[29:17] let's take the pair parameter updates
[29:20] let's take the updates of only the
[29:22] recent few thousand steps and let's see
[29:24] if they can uh perform better. They do.
[29:27] Atom performs better than all the
[29:29] previous things, especially for large
[29:30] language models, which is why it's
[29:32] almost the default optimizer. But Adam,
[29:35] unfortunately, in the algorithm had a
[29:37] little I think of it as a bug, maybe
[29:40] it's a feature um that any parameter or
[29:43] weight that you update really quickly
[29:45] doesn't get updated. Not not great,
[29:48] doesn't get updated fast. Unfortunately,
[29:50] those are the values that matter most.
[29:51] So we wasted a lot of time in atom not
[29:54] updating the correct values. It still
[29:56] converges but it takes a lot longer.
[29:58] AdamW fixes that. So that ends the atom
[30:01] family which is like kind of where like
[30:03] a lot of stuff converges. Let's talk
[30:04] about Muan. Most recently 2024 really
[30:08] late in 2024. Muan was introduced to uh
[30:12] replace the atom models
[30:15] and the way that it optimizes it
[30:17] actually looks at uh manifolds and
[30:20] topology and so on. I'm not super clear
[30:22] on the specifics. I've read the paper
[30:24] once or twice but didn't fully
[30:25] understand it. But what I can tell you
[30:27] is that most large language models like
[30:30] the open source ones now use muan as an
[30:33] optimizer and notw. That is the thing
[30:35] that determines how to walk down that
[30:37] slope. how to walk down and update
[30:40] weights and biases. Okay, great. So now
[30:42] we learned about Muan. And in the chart
[30:44] on the right, we can see Muan and Adam
[30:46] W. Muan is uh outperforming AdamW on
[30:50] really any amount of compute on the same
[30:53] data. So now we can kind of tell pretty
[30:55] concretely that it is outperforming uh
[30:59] outperforming AdamW and we should expect
[31:01] that by the end of 2026 almost everyone
[31:03] has moved over to Muan. There's one
[31:06] small exception to that which is
[31:07] training embeddings. We're not going to
[31:09] talk about that a lot in this class but
[31:11] worth knowing that one is supplanting in
[31:13] one in most areas but not all. Great. So
[31:16] now we've covered optimizers. What are
[31:18] batch sizes? Batch size.
[31:22] When you think about a GPU, you think
[31:24] about something that has 40 GB of RAM.
[31:26] It could be that updating a single uh
[31:29] feed forward pass only takes let's say 4
[31:32] GB of RAM. It's not going to be four,
[31:33] but let's for the purposes of this
[31:35] conversation say four. So actually
[31:37] you're going to have 90% of your GPU
[31:39] stand idle during training. Not great.
[31:42] Why? We've talked about this in the
[31:44] past. Idle GPUs mean more time, mean
[31:46] more compute money. Uh we don't want
[31:48] that. So instead, we want to show during
[31:51] training 10 items to uh 10 items to the
[31:56] optimizer and have it kind of do its
[31:58] update based on that bat size. So that's
[32:01] what that means during training. During
[32:03] inference means something totally
[32:04] different during inference when my model
[32:06] is ready and baked and ready to go. What
[32:09] it actually means is how many totally uh
[32:12] uh separate sentences we're going to
[32:14] show the model at the same time to also
[32:16] optimize the model. So it uses 100% of
[32:19] the GPU. We never want idle GPU time.
[32:22] Okay. So what batch sizes do people
[32:23] actually use? You can kind of see the
[32:26] chart on the left. It tells you
[32:27] somewhere between let's say a million, 4
[32:31] million and 60 million are really common
[32:33] in the last 2 years. So we're going to
[32:36] choose a value roughly in that range and
[32:38] I think we'll end up with closer to 0.5
[32:40] point uh.5 million because we have a
[32:42] very small model.
[32:44] Last thing we're going to have to learn
[32:46] about together in graph propagation is
[32:48] training loops and how they work. So
[32:50] every single machine learning model that
[32:52] you will ever see follows these set of
[32:55] patterns. It has a setup and then it
[32:58] loops over the data sets multiple times
[33:00] and teaches the model based on that data
[33:02] set. Remember we talked about train and
[33:05] test data sets. So what's the setup
[33:07] like? We initialize our model. We set up
[33:10] the train the training uh data loaders.
[33:14] Uh we create an optimizer. We have a
[33:17] loss function which we call criterion
[33:19] here. Then we're going to iterate
[33:21] multiple epics. What are epics? how many
[33:23] times the model sees the the train data.
[33:27] So we're going to do that and then for
[33:30] every uh for like the values that we're
[33:32] going to show here it's batch size of
[33:34] one uh sorry not bat size of one here
[33:36] we're going to iterate over the train
[33:38] loader and then first thing we do is we
[33:42] zero out the gradients from the last
[33:43] step. We have to do that every time
[33:46] we're going to run our model with an
[33:48] input. We're going to calculate the loss
[33:50] for that input. We're then going to do a
[33:53] backward propagation loss backwards
[33:55] optimizer step. So I'm going to run run
[33:57] you through this again because you're
[33:58] going to see this every time you build a
[34:00] machine learning model especially large
[34:02] language models. First thing you do is
[34:04] model. We create a new MLP or in our
[34:07] case like uh any sort of deep neural
[34:10] network. We create a data loader so we
[34:12] have access to our data. We create an
[34:14] optimizer. In our case it's Adam W. it
[34:17] gets the learning rate whereas the the
[34:19] train loader got our bat size. We have a
[34:23] uh our loss function in our case cross
[34:25] entropy loss because we have multiple
[34:26] probabilities.
[34:28] Then we iterate over the data multiple
[34:30] times in multiple epox. Then we for each
[34:33] one of those we zero out the gradients.
[34:35] We activate the model. We calculate the
[34:38] loss. We do backward propagation. We'll
[34:41] see that in action in a moment. But just
[34:43] really important to mention every single
[34:45] example from here on end will follow
[34:47] this training loop. Great. So let's look
[34:50] at a little bit of code. I used a lot of
[34:51] words to describe a little bit of code.
[34:55] So this is the notebook for back
[34:57] propagation. We're going to go over
[34:58] these concepts. To start off with, we
[35:00] need a data set. So a plus b modulus 5.
[35:03] I'm going to go over all of the a
[35:06] between 0.99. All of the b's between
[35:08] 0.99. I'm going to have the result as a
[35:11] plus b modulus 5 and I'm going to keep
[35:13] that in my data set for later. So now I
[35:15] have this data set
[35:17] 0 + 4 modulus 5 equals 4. Right? This is
[35:22] all of the data that we've already
[35:24] calculated. Let's try and visualize
[35:26] that. This oh my god that's the grid
[35:28] from earlier. Look at all of these
[35:30] diagonals. That's what the model is
[35:31] trying to learn. Right? Every one of
[35:34] these diagonal lines is something that
[35:35] tells the model here. If you follow this
[35:38] pattern, you can get to to to the
[35:39] correct answer we expect of you. So a is
[35:43] 10 plus let's say 10. We look at the
[35:47] chart and the correct answer is zero.
[35:50] That's what the this visualization tells
[35:52] us after modulus 5.
[35:55] So let's create a big PyTorch MLP. Uh in
[35:58] terms of PyTorch MLP, I'm going to just
[35:59] create it in let's say random size. It's
[36:02] not random. And there's a reason why I'm
[36:03] choosing these numbers. Let's we'll
[36:05] start off with 200 uh input neurons. Y
[36:09] 200. A is between 0 and 99. B is between
[36:12] 0 and 99. I'm doing this thing called
[36:15] one hot encoding. We'll have a slide for
[36:17] it in a sec. That says every option for
[36:19] A and every option for B gets an onoff
[36:22] neuron in the beginning. And they're all
[36:23] mutually exclusive. Great. So we have
[36:25] 200 input neurons and we have five
[36:28] output neurons,
[36:30] right? Why? Because when we modulus five
[36:32] 0 1 2 3 4 those are the only answers
[36:35] there's five answers in between I'm
[36:38] going to go between from 200 dimensions
[36:40] to 32 dimensions
[36:43] and from 13 32 I'm going to go down to
[36:46] 16. So I'm going to go from 200 input
[36:48] neurons to 32 neur hidden layer neurons
[36:51] to 16 hidden layer neurons to five
[36:53] output neurons. That's what you want to
[36:55] learn here. Why is counting those
[36:57] numbers kind of important for us?
[36:59] Because if you count that, you can kind
[37:01] of get that we're at 7,000 parameters.
[37:04] Why is 7,445 a magic number? Because
[37:07] we're going to take away 30% of the of
[37:10] the training set, which is about 10,000
[37:13] uh of the full data set, which is 10,000
[37:16] data points and we're going to take 30%
[37:18] of it and keep it later for train for
[37:20] testing.
[37:22] This 7,000 it matches the the size of
[37:25] the training data set. If the model
[37:28] wanted to, it can memorize almost
[37:30] completely the entire training set and
[37:33] get very high accuracy, but it won't get
[37:36] full accuracy unless it can actually
[37:38] generalize beyond the training set. The
[37:40] training sets again contain only the 70%
[37:43] of data that we have chosen to show it
[37:45] in a plus b modulus 5. And it can
[37:47] memorize it because it has almost enough
[37:49] room to do that. It actually doesn't. It
[37:51] needs for it has it's off by 45. That's
[37:53] intentional. We do want to give it some
[37:55] incentive to not memorize, but we never
[37:58] want to let it completely memorize the
[37:59] training set. That models will just
[38:01] choose to do that. But we're getting as
[38:03] close as we can here. Okay, cool.
[38:06] Uh, so mod 5 MLP, we printed this out as
[38:10] a linear layer goes 200 input neurons,
[38:12] 32 hidden neurons, 32 hidden neurons,
[38:16] then go to 16 hidden neurons. Those 16
[38:18] hidden neurons go to five output
[38:20] neurons. And we enabled biases here
[38:23] because why not?
[38:25] Great. So now we have our test train
[38:28] data set. We created a data set that
[38:29] just inherits from PyTorch's data set
[38:31] class. And then we implemented the get
[38:34] item method
[38:36] um and the length method. And then we
[38:38] used train test split. That's really
[38:40] common in machine learning models, not
[38:42] super common in large language models.
[38:44] We'll talk about why that is later.
[38:47] And then um we said hold back 30% of my
[38:52] data for a test uh data set. Very cool.
[38:57] And then shuffle it. We always want to
[38:58] shuffle our train data set. Uh so now I
[39:01] have my training data set and my
[39:03] validation data set or or test data set.
[39:07] 7,000 items going train. 3,000 go into
[39:10] the validation set. The test data set.
[39:12] All of these black dots now represent
[39:15] things that the model can't learn from
[39:16] the train data set. And it doesn't have
[39:18] access to this information. It's going
[39:21] to have to be able to generalize from
[39:22] the 7,000 examples we show it, which are
[39:25] not enough to even memorize the entire
[39:27] training set intentionally. Great. Let's
[39:29] do a training loop. I created a
[39:31] calculate accuracy method. All it does
[39:33] is it looks at the uh data set you give
[39:35] it and says how well the model performed
[39:37] on it. So if it gets a bunch of A's and
[39:39] B's, how well it did. If it gets the the
[39:43] test data set that or the test data
[39:45] loader, then it's going to tell you how
[39:47] well the model does in that data set.
[39:49] Important because we wanted to
[39:50] generalize to the unseen test data.
[39:53] Okay. So now we're we're finally the
[39:54] training loop. This is the thing we've
[39:56] all been waiting for.
[39:59] We first create a train loader. It get
[40:01] takes the train data set with the
[40:02] batches we chose. Bat size ends up being
[40:05] a parameter of this method train model
[40:07] that I created it. Now we have the test
[40:11] data uh loader uh also gets the batch
[40:14] size. We have our optimizer AdamW. We
[40:17] talked about why Adamw is better than
[40:19] atom. Why it's better than RMS prop was
[40:21] better than momentum especially for our
[40:23] domain. Takes in a learning rate. I kind
[40:26] of hardcoded a learning rate here. Again
[40:28] we're we could control it with this
[40:29] train model method or function. We have
[40:32] our loss function cross entropy because
[40:34] we have five probabilities in the
[40:36] output. So we can't just use residual
[40:39] error. We have to use cross entropy.
[40:41] We have our uh epic loop. So we're going
[40:44] to show this data over and over again
[40:46] until we the model learns to to 100%.
[40:50] Uh we for each set of data we zero out
[40:54] the gradient. We run the model. We check
[40:57] the loss function. We run a back
[40:59] propagation. And then we run a like a
[41:01] little mini batch here of running loss.
[41:04] Most importantly, I don't end this loop
[41:06] until the validation accuracy, the test
[41:08] accuracy is at 100%. We don't end that
[41:11] loop. Great. So now we did that. I'm
[41:14] going to run this model. I created my
[41:16] the model I created and I'm going to
[41:18] call train model. It takes the model,
[41:21] the training data set, the validation
[41:22] data set, the LR and the bath size. How
[41:25] long did it take? About six epex. So it
[41:28] had to show all of that data. 7,000 rows
[41:30] six time. So 42,000 times gen up to
[41:34] 42,000 times is how many times we've had
[41:37] to show this data and do back
[41:38] propagation.
[41:40] Let's look at that in maybe a chart. So
[41:43] we could kind of see that in the first
[41:44] epic we had 20% accuracy. Why is that
[41:47] totally expected? We only have five
[41:50] answers 0 1 2 3 4 for modulus 5. So
[41:53] random chance initialization of a of a
[41:56] network means you would hit 20%. Which
[41:58] it did. uh that's on both the training
[42:01] data set and the test data set. You
[42:04] could see that slower and slower the
[42:06] accuracy improves on the training data
[42:08] set. That's expected. What's also really
[42:10] cool is like in the second epic it only
[42:12] improved on the training data set. So
[42:14] you just try to memorize it. It's right.
[42:17] But when you get to the third epic all
[42:19] of a sudden the performance and the
[42:21] unseen data also improved. The model is
[42:24] itty bitty able to uh generalize even in
[42:27] the third epic. The fourth epic is where
[42:29] we see our big wins, right? Massive
[42:32] jump. The model is able to like both
[42:34] memorize a lot of the training set but
[42:35] also really generate on the test data
[42:39] and finally kind of converges close to
[42:41] 100% but not exactly the fifth epic and
[42:43] then fully converges the sixth epic. As
[42:46] performance and accuracy improves,
[42:48] training loss goes down. Better train
[42:50] lower training loss, better training
[42:52] loss until it eventually reaches zero.
[42:56] Okay, so now we kind of like trained our
[42:59] model. We know that it takes six epics
[43:01] to like fully get a plus b modulus 5 to
[43:04] generalize in at least the architecture
[43:06] we came up with this 200 to to 32 to 16
[43:10] to 5 architecture. What's the ideal
[43:13] learning rate? Right? So I'm going to
[43:15] create this method called epex to
[43:16] converge. It's just going to train our
[43:18] model right with parameters and tell me
[43:21] what is what is the number of epics that
[43:23] it requires to converge. and then I'll
[43:26] hold it later in like in a dictionary.
[43:29] Okie dokie. So, I've got this method.
[43:31] I've got all of the learning rates I
[43:32] want to test. I'm going to call epics to
[43:35] converge. And then I'm going to like
[43:36] print this out and have a pretty chart.
[43:38] So, I'm going to run that. It the lowest
[43:40] learning rate, right? Very, very low
[43:42] number.
[43:44] Doesn't converge in 25 epics. I just
[43:46] decided 25 is the hard failure mode. And
[43:48] let's just move on. Uh this other one
[43:51] also doesn't converge a little bit more.
[43:53] doesn't converge a little bit more. Oh,
[43:55] now we're converging at 12 epics. Really
[43:57] cool. Now we're converging at five 3
[44:03] again. It goes back up. Let's look at
[44:05] this in a chart.
[44:07] So this chart is learning rate over
[44:10] convergence speed. We've got our uh how
[44:13] many epics it took to converge. Less
[44:15] epics means less GPU compute means we
[44:18] saved a lot of money, right? And then
[44:20] this is the learning rate we chose. We
[44:22] can see that a learning rate of uh 0.01
[44:27] sorry of 0.01 converging two epics.
[44:30] That's the fastest we've been able to do
[44:31] it. We only had to do up to 12,000
[44:33] steps. That's much better than
[44:35] converging at 12 steps. That's six times
[44:36] better. That's six times less compute.
[44:39] So learning rate really important. We
[44:41] just found our optimal learning rate for
[44:43] this one example 0.01.
[44:46] Can we also now find the ideal batch
[44:49] size? So if this is the exercise for
[44:52] you, can you please uh copy the code
[44:54] from learning grade and try and run uh a
[44:57] sweep of what is the best bat size that
[45:00] we can run here? Uh the answer I'm going
[45:02] to just like jump into the uh table. The
[45:06] table tells us that the best bet size
[45:08] ends up being three, right? The least
[45:10] amount of epics converges around best
[45:12] size of three. The lower the bat size,
[45:14] the better it works here. Why is that? A
[45:17] plus B modulus 5 has deterministic
[45:19] answers which test which text doesn't
[45:21] have. When we build large learn language
[45:24] models, lower batch sizes don't really
[45:26] help us because we don't have clear
[45:28] deterministic answers in language. And
[45:30] we'll talk more about that in a sec.
[45:33] Finally, another exercise for you is uh
[45:36] let's check all the potential configs
[45:38] that we can run our architecture. I
[45:40] decided 32 and 16. You might want to
[45:43] test other ones. fourth and two eight I
[45:46] neurons in the first hidden layer, four
[45:47] in the next hidden layer. Check all of
[45:50] these and see which one makes the most
[45:52] sense to us. So again, I already wrote
[45:55] the code. You have it in answer. You
[45:56] don't have to like look like but you
[45:58] don't have to look at the answer. You
[45:59] can just like try and code it up because
[46:01] we have example code.
[46:03] But if you look at this, you can see
[46:05] actually we gets to pretty good
[46:07] performance at around uh uh uh six epics
[46:12] at 32-6. Why is that important? Uh
[46:16] because the total parameters exceeds our
[46:21] full data set at about that point. So we
[46:24] would almost never want to go above
[46:26] that. But if we did want to memorize
[46:29] increase the the training set uh the
[46:32] model size it actually converges faster
[46:35] but it converges there faster on test
[46:37] data. Why is that? We can have a bunch
[46:40] of theories like it can't memorize the
[46:43] test data set. It's never seen it. So
[46:46] that's not why why is it why is it it
[46:49] has more room to experiment. it has more
[46:52] room to try stuff and fail and
[46:54] eventually it arrives at a generalizable
[46:56] solution a lot faster if we give it more
[46:58] memory. So it could be the 128 and 64 is
[47:01] the ideal configuration for this A plus
[47:03] B modulus 5.
[47:06] Great. So now that you have all those
[47:08] numbers, you know the ideal learning
[47:10] rate, the ideal bath size and the ideal
[47:12] architecture in terms of hidden size
[47:13] dimensions, you should go and write a
[47:16] minimal training loop that uses those
[47:18] values. Go ahead and copy stuff from the
[47:20] rest of the sheet. Really try and write
[47:22] your own training loop. I think it'll be
[47:23] really useful for you. Just because I
[47:26] know some of you won't do it, I'm going
[47:27] to review the answer because I think
[47:28] it's useful. This is the best learning
[47:31] rate and the best best size and the
[47:33] number of epics we're willing to run. We
[47:35] create the training data loader, the
[47:37] test data loader. We have our optimizer
[47:40] which is atom. You have cross entropy
[47:42] loss. We go over all the
[47:47] uh data in multiple epics. We zero out
[47:51] the gradients. We run the model. We
[47:53] check the loss function for the model.
[47:55] And then we do back propagation.
[47:57] Eventually, it'll stop. It stopped in
[48:00] three epics. Isn't that really cool? We
[48:03] were able to bring our very naive
[48:06] example from six epics to three epics.
[48:09] That's a 2x improvements. That's 2x less
[48:12] GPU time that we're going to need. So
[48:14] let's think about the next question that
[48:17] we have which is what did we actually
[48:20] learn? And I'm going to bring us back to
[48:21] the slides for a moment. So what did we
[48:24] actually learn uh as a as a if we were
[48:28] the model?
[48:34] What we learned is that um what we
[48:37] actually learned is a bunch of weights
[48:39] and biases, right?
[48:40] So over here you can see row zero has a
[48:43] bunch there's 32 rows 32 for each of our
[48:46] hidden dimensions and then there's going
[48:48] to be 200 columns and you can kind of
[48:50] see that here when we look at that. If
[48:53] you can look at this and tell me what
[48:55] the network learned, you're much more of
[48:57] an intuitive thinker than I am. I had to
[48:59] go and visualize this. So I said put all
[49:02] of these weights and also there's a bias
[49:05] row in the bottom. put all of these in a
[49:08] chart and try and visualize these for me
[49:10] and see if I can't see some patterns.
[49:14] So if we look at the top the left chart,
[49:18] let's look at it together for a moment.
[49:21] There appears to be some sort of
[49:23] repeating pattern when we visualize this
[49:25] as a heat map. You can see it goes from
[49:28] red to light red to white to dark blue
[49:31] to light blue to red and then the whole
[49:33] pattern just keeps repeating and it
[49:36] happens on every row of this first
[49:38] matrix. Why does it do that? Right? It's
[49:41] a really great it's a really great
[49:43] question. Well, if we use another
[49:47] technique called PCA, it takes us from
[49:50] 32 dimensions, that's our hidden
[49:51] dimensions, to two dimensions, that's
[49:53] what we're rendering here. We can see
[49:55] that all of those uh neurons converge on
[49:59] one of five points in a circle.
[50:02] That's really cool. Modulus 5, five
[50:05] points in a circle. The way that the
[50:07] network learned to do this is by
[50:09] bouncing from this green cluster to the
[50:11] purple cluster to the orange cluster to
[50:13] the blue cluster to the red cluster and
[50:15] back to the green cluster. Somewhere in
[50:17] the network, there's a highdimensional
[50:20] structure that just goes like that in a
[50:22] spiral or a loop. Very very cool to
[50:25] notice that. Why am I teaching you about
[50:28] a plus b modulus 5? That's almost
[50:31] irrelevant to your lives. You're not
[50:33] machine learning engineers. It's because
[50:35] it's exactly how large language models
[50:38] learn any sequential concept. Our little
[50:40] toy example of a plus b modulus 5 and
[50:43] the values that it learns actually has
[50:45] applicable uh relevancy to us as large
[50:50] language model builders. So the model
[50:54] when it wants to memorize days of the
[50:55] week creates one of these
[50:57] highdimensional structures for Sunday,
[50:59] Monday all the way to Saturday, Sunday
[51:01] again, right? Months of the year,
[51:04] January all the way to December and back
[51:06] to January, it creates this like uh
[51:08] sample again. Um uh when it does colors,
[51:13] colors are also cyclical if you think
[51:15] about it, right? You move RGB in in
[51:18] cycles. Years also move in cycles. Took
[51:22] me a while to understand that. I was
[51:23] thinking years must be sequential.
[51:26] They're not cyclical, right? Numbers
[51:27] only go up. But the number of we're in
[51:30] 2026. We'll eventually have a 2029. Then
[51:34] we'll switch back to 2030. Eventually,
[51:36] we'll make it back to 2036, which kind
[51:38] of looks similar to 2026.
[51:41] Then the the century will shift. Then
[51:43] the millennium will shift. All of these
[51:46] are concentric circles within the inner
[51:48] representation of the LLM. Same goes for
[51:51] dates. Same goes for digit edition. Uh
[51:54] this is a 2025 paper showed that when
[51:58] you ask a large language model 2 plus 3
[52:00] and 2 plus 4, it didn't just memorize
[52:02] the answer necessarily. It has some sort
[52:05] of inner structure that knows how to
[52:07] walk around and like do that addition
[52:10] using sinus and cosine and so on. also
[52:12] recently validated by enthropic in a
[52:15] causal paper where they took this
[52:16] structure out and the model didn't know
[52:18] how to do math anymore basic condition
[52:21] very fun and finally anthropic had this
[52:23] paper that I call the enthropic manifold
[52:26] paper I don't know its real name a top
[52:28] of mind but whenever a model looks at
[52:30] your messages it counts the number of
[52:32] lines and the number of words in each
[52:34] line using one of these kind of
[52:37] highdimensional structures one of these
[52:39] loops so our little example of a plus b
[52:42] modulus 5 converging on five data points
[52:46] actually is very similar to how a large
[52:49] language model memorizes any sequential
[52:52] concept like dates like months like
[52:55] years like
[52:57] colors like addition like messages
[53:01] counting words and lines there's a lot
[53:03] of momentum right now in what we call
[53:05] manifold or geometry research for LLMs
[53:08] and I think by the end of 2026 you're
[53:10] just going to see an explosion of these
[53:12] structures that we understand better.
[53:15] Great. So, I've given you so much
[53:17] information in this one section. This
[53:18] might be one of the deepest and most
[53:20] nuance sections. You should probably
[53:23] learn more. So, where can you learn more
[53:25] if you want to learn about how to set
[53:27] your learning rate and your bat size and
[53:29] your optimizers? The best place to learn
[53:31] is going to be in the open source uh uh
[53:35] papers that are released by Almo and
[53:38] small and all of the other ones Trinity
[53:40] and Quinn and so on.
[53:43] So one option is we can go and we can
[53:46] pick the Almo 3 paper and then we can
[53:49] see what it says about how we should
[53:53] build our learning rates and what other
[53:55] parameters we should set. They do a lot
[53:58] of ablation studies. It's really worth
[54:00] doing that. Both Almo 3 and the small
[54:02] three papers I think are magic to read
[54:05] for this and there's a bunch of other
[54:06] ones that are really perfect for that.
[54:08] If you want to learn more about the
[54:10] implementation of backrop in PyTorch,
[54:12] Tensoronic has a few really great guides
[54:15] on that and I link to those here. I also
[54:17] want to highlight a really important
[54:18] resource that helped me understand how
[54:21] the calculus really translates into back
[54:25] propagation.
[54:30] And that's Josh Stramer uh's book and
[54:33] also YouTube playlist on calculus so on
[54:37] and so forth. Really really helpful. Uh
[54:41] it helped by taking us example by
[54:43] example doing all the the derivations of
[54:46] the formula formulas required to like
[54:48] see the why back propagation works why
[54:51] recalculating the slope while back
[54:52] propagating actually gets us to the
[54:55] correct updates. So really really
[54:57] recommend this playlist for you to
[54:58] watch. We're not going to do it here
[54:59] together. Uh one last slide that I kind
[55:02] of skipped a moment ago is our
[55:04] decisions. So what are the architecture
[55:06] decisions we're taking from this whole
[55:08] massive massive section that we just had
[55:10] on back propagation towards our GPT2
[55:13] style large language model. One is we're
[55:17] going to use uh optimizers that are
[55:19] derived from stoastic gradient descent.
[55:22] There's really no alternative for them
[55:23] in large language models. There's maybe
[55:25] like the occasional paper that claims
[55:27] there are alternatives but generally I
[55:29] haven't seen any evidence beyond that
[55:31] that is picking up momentum
[55:33] specifically we'll use the atom
[55:35] optimizer could be that one would be a
[55:39] way better choice but since I don't
[55:40] understand it I don't want to use
[55:41] something I don't fully fully fully
[55:43] understand
[55:45] um hyperparameters we're going to choose
[55:46] a bat size of half a million and a mini
[55:49] bat size of 16 so we'll show the model
[55:52] 16 words at a time to a maximum of half
[55:54] a million tokens. Uh we'll run one
[55:58] epoch. So far, our example has ran
[56:00] multiple epics, but really important to
[56:02] note because we have so much training
[56:04] data like we have the internet worth of
[56:06] text data and our model is so small, we
[56:08] can actually just show the data once and
[56:11] the model still learns English. Really
[56:13] interesting to note that. And in terms
[56:14] of learning rate, we'll ramp really
[56:17] high. We'll start at a stable rate.
[56:19] We'll do warm up over 2,000 steps. then
[56:22] we'll cosign decay slowly over time. You
[56:25] don't need to know how to implement it
[56:26] yourself, but it's important for you to
[56:28] understand we don't have a single
[56:30] learning rate. We're always we're going
[56:31] to bring the learning rate up and then
[56:33] we're going to bring it down slowly.
[56:35] Great. So those are our decisions.
[56:36] What's our next and last final section
[56:39] on machine learning models? How to save
[56:41] and load those. So now we spent a bunch
[56:43] of GPU time to train a model. Now we
[56:46] want to save it to disk and be able to
[56:47] load it. I hope you'll join me again at
[56:49] section 9 when we do that. That section
[56:51] is going to be a bit quicker than this
[56:53] section. Thank you so much.
