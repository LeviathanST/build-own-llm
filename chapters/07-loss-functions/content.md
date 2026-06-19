# Loss Functions | Build Your Own LLM Workshop #7

**Build Your Own LLM Workshop — Video #7 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 25m 56s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=bVz8i9EWEQw |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone, welcome back to Justin
[00:02] Angel in a room talking about machine
[00:04] learning. Specifically, we're building a
[00:07] large language model from scratch. Let's
[00:09] do that right now.
[00:11] In this section, we're going to talk
[00:13] about loss functions. So previously, we
[00:15] had talked about
[00:17] multi-layer perceptrons and we took our
[00:19] second component we're going to carry
[00:20] with us into our large language model,
[00:23] which is an MLP that grows and shrinks.
[00:25] And now, we're going to move into loss
[00:27] functions. And really, the way that I
[00:30] think about loss functions is they help
[00:32] us kind of decide how far we are off
[00:35] from the goal we're going to have. So
[00:37] our deliverable for this section is
[00:39] going to be cross-entropy.
[00:41] And then as usual, we have code and
[00:43] Excel links on top here. Okay, so let's
[00:46] think about loss functions or why we
[00:48] even need them. What's the problem that
[00:49] they're solving for us, right?
[00:51] >> [gasps]
[00:52] >> So [sighs]
[00:53] a randomly initialized LLM is actually
[00:55] pretty bad in English. And we don't
[00:58] really know how bad it might be. So you
[01:01] could go to just go to the AI code zero
[01:03] and we can look at the LLM before we
[01:06] were able to train parameters. And you
[01:08] can see here, we gave it the phrase once
[01:10] upon a time in a small village a soft
[01:13] drink Catalan captures 299 route
[01:16] Cincinnati solitaire manufacturing. Not
[01:19] super reasonable, but after training,
[01:23] uh text makes more sense. Once upon a
[01:25] time in a small village, an ancient man
[01:27] and woman lived there. Really cool
[01:30] stuff. So we just learned that during
[01:33] back propagation, we can teach a model
[01:35] English.
[01:37] But
[01:38] that initial large language model that
[01:41] was kind of bad at English, we don't
[01:43] really know how bad it was in English.
[01:45] That's really the question we're trying
[01:46] to answer with loss functions. So
[01:48] randomized
[01:50] uh a randomly initialized LLM asked the
[01:52] capital of Texas is still doesn't know
[01:54] the answer and it will probably give you
[01:56] like half an emojis and answers and
[01:57] weird HTML. So,
[02:00] loss function we quantify the distance
[02:04] from their goal. Right? So, how do you
[02:06] do that? Let's say your goal was seven,
[02:08] expected seven, and the observed value
[02:11] was six, that means my loss is one, 7.6
[02:15] 7 - 6 = 1.
[02:17] So, that's a residual error. That's like
[02:19] the first formula we're going to learn
[02:21] in loss functions. So, Y - Y hat. That's
[02:25] just how we That's just the notation and
[02:27] we say Y hat for this kind of observed
[02:29] Y. And then
[02:31] the overall goal of loss function is to
[02:35] tell us
[02:35] how far away are the machine learning
[02:38] models from their goal. They're not
[02:40] going to tell us how to get there. The
[02:41] distance, not path. Their overall goal
[02:44] is their overall purpose is to minimize
[02:47] future
[02:48] surprise. Minimize future surprise.
[02:51] Okay, so now I've given you one formula
[02:54] for residual error, like Y - Y hat. Why
[02:57] not give you a bunch of other formulas
[02:59] for a bunch of other kinds of loss
[03:01] functions? So, I'm going to open up
[03:03] Excel and we're going to just see a
[03:04] bunch of examples for loss functions.
[03:07] So, as usual, we're going to start by
[03:08] making a copy
[03:11] and then working in the without answer
[03:13] sheet.
[03:16] Great. So, now we're in the sheet. How
[03:19] do we Let's say we have this
[03:21] neural network, this MLP, and then let's
[03:24] say that the the actual value the So,
[03:26] it's outputting 3.1 based on math that
[03:28] we've seen in the previous section.
[03:30] Let's say I expected four.
[03:32] Okay, so what's my residual error? My
[03:35] actual is Y. My observed is this.
[03:42] Here we go. So, expected
[03:44] minus observed, 0.9. Okay, great. So,
[03:48] that was pretty easy. What are some
[03:50] problems we could like Let's that a
[03:52] bunch more times here. So, let's say I
[03:54] have this Y and I have this Y hat. These
[03:58] are just the values that I generated.
[03:59] You don't have to necessarily know how I
[04:01] generate them. You can look at the
[04:02] formulas. Let's say I have this Y and
[04:04] this Y hat. So, we said the error is Y
[04:09] Y hat. And then I can move all move this
[04:14] over here and do this multiple time.
[04:16] Okay, so one thing we could see is our Y
[04:18] our error tends to be negative for this
[04:20] data set.
[04:22] What else? We can kind of see that the
[04:24] error, this red line, is really the gap
[04:28] between this blue line and this purple
[04:30] line. It is the error between our
[04:32] expectation and what we've actually
[04:34] observed. Okay, so that's pretty easy.
[04:36] But what's a bunch of problems we're
[04:37] going to have? Well, one problem we're
[04:39] going to have is uh
[04:43] um one problem we're going to have is we
[04:44] have a bunch of values and we should
[04:46] probably get like a mean error of these,
[04:47] an average error, right? Cuz I want to
[04:49] get like multiple results at the same
[04:51] time and I want to like know my loss for
[04:53] multiple inputs. So, one option of doing
[04:56] that is just seeing the average value.
[04:58] So, I have a sum of 16.3 for all of
[05:01] these items. I just summed them up. And
[05:03] then I have 10 items, right? So, sum and
[05:06] count. So, what's it going to be the
[05:08] average here? It's going to be the sum
[05:10] divided by the count of items.
[05:14] Here we go. And this is the formula you
[05:15] could see here. Y - Y hat, you sum it
[05:18] all up, you divide by N. It's number of
[05:20] items. Okay, so the mean error for that
[05:22] example was -1. What does that tell us?
[05:25] Right? You can kind of see that that the
[05:27] average is like in between the minimum
[05:30] and like the maximum.
[05:33] Great. Um so, now what is the problem
[05:36] that we have with summing stuff up?
[05:38] Well, if you're summing stuff up, that
[05:40] kind of worked for us here cuz almost
[05:42] everything was negative, but because we
[05:45] have positive and negatives, we kind of
[05:47] lost their magnitude. They kind of
[05:48] canceled each other out. So, that's not
[05:51] great. We probably don't want to lose
[05:53] out on like cuz the like the mean error
[05:55] won't change a lot won't change a lot if
[05:57] the values weren't updating, but they
[05:59] wouldn't change a lot by just removing
[06:01] those two values. So, what we want to do
[06:03] is find a way of not losing those
[06:05] values. So,
[06:07] we're going to take the error and we're
[06:09] going to square it. So, we already have
[06:10] the error written up here. So, we're
[06:12] just going to square it. By squaring it,
[06:15] what we actually do
[06:17] uh is uh get all the numbers to be
[06:20] positive.
[06:22] Here we go. And then uh that kind of
[06:25] handles our problems with negative
[06:26] values.
[06:28] Uh so, we sum all of these numbers up.
[06:31] Now, we know the sum is 29.1. Let's
[06:33] validate 29.1. Yep. We have 10 items.
[06:36] The MSE, the mean squared error, is
[06:40] 2.91.
[06:41] Okay, so we're getting the to something
[06:43] better, but the problem is now that
[06:45] we've handled negative values and
[06:47] positive values that's summing,
[06:49] we increase the magnitude by a lot and
[06:51] we want to bring the magnitude back
[06:53] down. So, great. So, now we can root
[06:55] that whole expression. So, MSE root, so
[06:59] we can do that in like SQRT.
[07:02] 2.9 1.8. Oh my goodness. So, all we're
[07:06] doing is trying to handle negative
[07:08] positive values here. Okay. So, we did
[07:10] all of that. And now the question is can
[07:12] we see something called a loss
[07:13] landscape? We maybe saw something
[07:15] similar to landscapes before, but let's
[07:16] see a loss landscape. So, in a world
[07:19] where we have Y and Y hat and we said
[07:21] residual error is Y minus Y hat. I'm
[07:25] going to lock uh the row for Y and I'm
[07:28] going to lock the column for Y hat.
[07:31] Here we go.
[07:33] We don't need bold here.
[07:35] Oh.
[07:36] Oh.
[07:37] Here we go.
[07:39] Great. So, that's what our landscape
[07:40] looks like. Really interesting. We have
[07:42] this little kind of like valley in
[07:45] between of the two of these things. It's
[07:47] not really a valley, but you can kind of
[07:49] see where zero is at. Okay, so you can
[07:52] if you imagine it, there's no real value
[07:54] here. It's kind of hard to tell what
[07:55] we're supposed to do. How do we optimize
[07:57] based on that? So, if we do re mean
[08:00] residual length mean residual mean
[08:03] error,
[08:04] right? So, here I'm just creating a sum
[08:07] and you can see I have a bunch of Y's
[08:09] here and a bunch of Y hats here. In
[08:10] order to combine them, each one of these
[08:12] dots is going to grab Each one of these
[08:14] cells is going to be based on another uh
[08:19] on another set of cells. So, you can see
[08:20] here this is the Y hat we're going to
[08:22] use and the and the Y's are going to
[08:23] use. You don't really have to follow
[08:25] these tricks for Google Sheets, but just
[08:27] notice that there's different numbers
[08:28] here. Okay, so here is very positive
[08:30] numbers. Here is very negative numbers.
[08:33] It's still like kind of hard to work
[08:34] with. We said we have a problem with
[08:36] residual mean error with negatives. So,
[08:38] let's go with root mean squared error.
[08:40] That's the one that we kind of were
[08:41] building up to.
[08:43] Going to put one number here.
[08:48] Drag and drop.
[08:50] Now we see something really interesting.
[08:52] There's a bunch of positive values here
[08:54] in the edges and there's a bunch of
[08:56] let's call them not negative zeros, but
[08:59] close to zero values or like if you
[09:02] normalize them, they would be zeros
[09:04] right here in the middle. So, now we get
[09:06] like a real valley. What do I mean by
[09:08] valley? Excel, not Google Sheets, can
[09:11] like draw this chart as a 3D landscape.
[09:14] So, if you try and look at it from the
[09:16] side and you put it in a 3D landscape,
[09:18] you could really see this like it kind
[09:20] of looks like a manta ray. It's like got
[09:21] its wings up. Oh my goodness.
[09:25] And there's this little valley dip in
[09:26] the middle. That's where the loss is
[09:29] lowest. That's where performance on
[09:31] whatever a task ends up being is
[09:34] highest.
[09:35] That's really cool to see. So, this is
[09:37] our first example of going from loss in
[09:40] a single example to a 1D loss to a 2D
[09:43] loss to effectively a 3D loss landscape.
[09:47] We're going to be thinking about loss
[09:48] landscapes a lot more, but this was the
[09:50] most basic example.
[09:52] Okay, so now that we saw a loss
[09:53] landscape for the very first time and
[09:54] you can kind of understand that if we
[09:56] wanted to traverse this loss landscape,
[09:58] we'd probably walk down towards that
[10:00] little valley in the middle.
[10:02] >> [snorts]
[10:03] >> We have to ask ourselves, are we even
[10:05] using the right loss function for large
[10:08] language models? And the answer is no.
[10:10] Right, residual errors are great when
[10:12] you have one scalar value, one number
[10:15] that you're trying to reach from one
[10:16] other number. That works great.
[10:19] However,
[10:22] a large language models use probability
[10:24] multiple output probabilities. So, that
[10:26] cat sat on the mat, car, door, right?
[10:30] There's a bunch of words that could be
[10:32] generated from a large language model.
[10:34] So, as a result of that, what we would
[10:36] want to do is we would we would want to
[10:38] use the loss functions that could
[10:39] support multiple output probabilities.
[10:41] >> [snorts]
[10:41] >> So, residual errors would be used if we
[10:43] had like only one thing that we're
[10:45] trying to optimize for. Cross-entropy
[10:47] helped because we have 50,000, 150,000
[10:49] options for probabilities that we emit.
[10:53] Great. So, now we know we use residual
[10:55] errors for one thing and we use
[10:56] cross-entropy for large language models.
[10:59] Okay, that's awesome. Let's look at a
[11:01] real example. I'm going to jump us real
[11:04] quick to our
[11:06] uh example that we're going to see from
[11:08] our neural net. So, we are going to keep
[11:11] building our neural net and we have our
[11:13] first digit recognizer. What does it do?
[11:15] It takes the input
[11:17] >> [snorts]
[11:17] >> and then based on a bias and a weight,
[11:19] it tries to activate an output neuron.
[11:21] These are 10 output neurons that
[11:24] correlate to the first digit of the
[11:26] input. So, 3.2, the first digit is
[11:28] three. 9.5, the first digit is nine,
[11:31] right? That's what we would expect to
[11:33] see. But it also emits probabilities for
[11:35] every single output. That's the
[11:37] important thing to remember. So let's
[11:39] look at that demo together and then go
[11:41] back to Excel.
[11:43] So here I have an input of 2.3 and I
[11:45] could see that the highest probability
[11:47] actually does go to the cell with two,
[11:50] but there's some probability for the
[11:51] cell for the neuron with three. But
[11:53] there's no probability for the neuron
[11:55] with one. Really interesting to notice
[11:57] that. That's because we set up our
[11:58] weight and biases in such a way that
[12:00] activates that one target. Okay, so I'm
[12:03] going to change the input and it seems
[12:05] pretty successful. Let's see if at any
[12:08] point it does it has a wrong prediction.
[12:10] Oh my goodness. It just predicted the
[12:12] wrong number. 3.9 it predicted as having
[12:16] the first digit of four. Something about
[12:18] bias of zero and weight of one just does
[12:21] isn't conducive to that. So maybe I can
[12:23] bring my bias a little bit down. Oh my
[12:26] goodness, and now it's predicting
[12:28] something that resembles the correct
[12:30] value.
[12:31] Okay, so it's still predicting four. Oh
[12:33] no, it's so hard, right? So you have to
[12:35] kind of play around with these values
[12:36] until you get to the right answer. This
[12:39] isn't the right answer. It's just an
[12:40] answer that answers 3.9 is three, not
[12:43] four.
[12:44] Okay, so now we looked at that and we
[12:46] kind of understand that we have to do a
[12:47] first digit recognizer. How would we go
[12:50] about implementing that in loss
[12:51] functions? Well, we talked about cross
[12:54] entropy a moment ago.
[12:56] So let's look at this. We have not 10
[12:58] classes that we could output from our
[13:00] first digit recognizer.
[13:02] We have our Y values, right? And we know
[13:06] that we
[13:08] expect to only have
[13:12] the digit three for the for 3.2 output
[13:16] the correct 100% value. All the other
[13:18] ones we don't really care about for the
[13:20] best model will have them at 0%. Then we
[13:23] have our Y hats.
[13:26] And these are the values that we
[13:27] actually end up observing here.
[13:30] And then
[13:32] uh
[13:32] now we can like go through this formula
[13:34] of cross entropy. So okay, so log y hat,
[13:38] here we go.
[13:39] Uh log of y hat times y, log of y hat.
[13:45] And we're just writing the formula the
[13:47] way that it's written right above here.
[13:50] Log of y hat times y. Okay, so not a lot
[13:53] has shifted.
[13:55] And then we can pull all of these
[13:57] together.
[14:00] Great.
[14:02] And then we could sum up all of the log
[14:04] y of that.
[14:07] And we could see that we I made a
[14:08] mistake here, but that's totally fine.
[14:10] We can go in and fix it in a moment.
[14:12] So log times y,
[14:15] right? So I needed two
[14:19] log y hat.
[14:22] Log of y hat times y. What is it
[14:25] multiplying here?
[14:27] Yeah, that should be correct. Oh,
[14:28] actually there's no mistake here. So we
[14:31] could see that the only cell that got
[14:32] any value is this third cell because
[14:35] that's the digit we're trying to
[14:36] predict. So that's the sum. That's the
[14:38] number of samples that we've taken. So
[14:41] sum divided by number of samples
[14:43] point minus point eight eight.
[14:46] And our cross entropy is point eight
[14:48] eight. Very cool. So we're getting very
[14:50] close
[14:52] to understanding how cross entropy
[14:55] works. Intuitively, we can kind of
[14:58] calculate, "Hey, because this value
[15:02] right, was only point four,
[15:05] I had a pretty high loss function. If I
[15:07] keep bumping up this number, the loss
[15:09] function drops down, right? You and you
[15:12] should play around with these numbers.
[15:14] If I bring this number down, the loss
[15:16] goes up. High loss means I'm far away
[15:18] from where I want to be. Low loss means
[15:20] I'm close to where I want to be. So
[15:23] again, I'm going to bring that back up
[15:24] to 0.6, but if I bring this back down to
[15:27] zero, that's not going to do it because
[15:28] it's all multiplied by zero or like so
[15:31] on. Okay, great. So we did that. We saw
[15:33] an example of cross entropy live. We can
[15:36] also kind of try and explore what a loss
[15:37] landscape of cross entropy looks like.
[15:39] Really hard to do in Google Sheets, so
[15:41] we'll find another way of doing that.
[15:44] Let's look at a code example. Now we're
[15:46] going to go over all of the loss
[15:48] functions we just saw a moment ago, even
[15:50] the ones we can't fully use. Let's start
[15:52] off with a perceptron. So this is a
[15:54] basic
[15:55] PyTorch perceptron. It's an custom NN
[15:57] module and an init in the init method.
[16:00] It has a weight and a bias. In the
[16:02] forward method, it multiplies the weight
[16:05] and the input with the bias. We've seen
[16:07] this a hundred times. There's a set
[16:09] weight and set bias method function here
[16:11] that we can use later on. Okay, so I
[16:13] create perceptrons 0.5 and 0.2 * 1 =
[16:18] 0.7. Just WX + B. We've seen this many
[16:21] times now.
[16:22] Now we have we can reset the weight and
[16:24] we can check the perceptron still works.
[16:26] Okay, so the first thing we want to do
[16:27] is we want to calculate residual errors,
[16:30] right? Here we go. Y expected means - Y
[16:34] predicted equals -0.2. So let's say I
[16:38] expected 0.5, I had 0.7 0.7.
[16:43] Right? And as a result of that, my
[16:45] residual is 0.2.
[16:47] We can also try and calculate the mean
[16:49] squared error because we only have one
[16:51] item. There's no summing or division
[16:53] that I have to do. We just have to like
[16:55] power to it. So we'll
[16:57] we'll square it and then we can see this
[17:00] is what happens when we square it. We
[17:01] can also see that PyTorch has its own
[17:03] MSE loss
[17:05] built-in loss function we can use. So we
[17:07] can just go take the Y expected, the Y
[17:10] predicted, calculate the MSE loss,
[17:13] and then it's 0.4 0.04 and 0.04 like we
[17:16] like like we calculated a moment ago.
[17:23] Great. So, now
[17:25] let's think about can we visualize the
[17:27] lost landscapes?
[17:29] One option is we can hard code our input
[17:32] and we can hard hard code our expected
[17:34] value from it. And then we could scan
[17:36] through all of the weights and all of
[17:38] the biases.
[17:40] We could potentially get between minus
[17:42] two and three and minus two and two.
[17:45] >> [clears throat]
[17:45] >> So, if I do that, right? I'm going to
[17:47] just take my perceptron. I'm going to
[17:48] run, you know, nested for loop between
[17:51] all of the weights and all of the
[17:52] biases. I set that on the perceptron.
[17:54] I'm going to run the perceptron and I'm
[17:56] going to calculate the the MSE value.
[18:00] And based on that, that is what our loss
[18:02] landscape looks like. Wow, it looks like
[18:04] a manta ray. It's exactly what we saw
[18:06] earlier in Excel. What What is the
[18:08] importance of this valley loss
[18:10] landscape? It is a certain number of
[18:13] weights and a certain value that
[18:15] corresponds to a certain number of value
[18:17] of biases that will minimize the loss in
[18:19] our loss function. Minimize loss means
[18:22] we're doing better learning the task
[18:24] we're trying to achieve, for example,
[18:26] learning English. Minimizing loss means
[18:29] we learn English better.
[18:31] Okay, so now there's a bunch of exercise
[18:32] for you. One is you can try and put
[18:36] different values for inputs and Y
[18:37] expected and see if it changes what
[18:39] chart gets rendered. The answer is yes,
[18:41] it will.
[18:42] Cross entropy.
[18:45] Now we were talking about cross entropy
[18:47] earlier. And then the thing that we saw
[18:51] is that there's a bunch of math for
[18:53] cross entropy that we can run. Let's
[18:55] look at our digit MLP. So, we were
[18:58] talking about this first digit finder,
[19:01] 3.9. The correct answer is three. We
[19:03] were trying to minimize the input for
[19:05] everything else. So, how does that look
[19:08] like? Well, I just threw in a line of
[19:09] code here that says actually give me 10
[19:11] output neurons at the end.
[19:13] >> [snorts]
[19:13] >> Uh other than that, it's very similar to
[19:15] the previous um to the previous MLP that
[19:18] we had.
[19:19] So, I will set it up with one weight,
[19:22] zero bias. That's kind of how we start
[19:24] off with this demo, right? One weight,
[19:26] zero bias. I give it an input of 1.3,
[19:29] and then I kind of want to see what it
[19:31] renders. It looks like it does pretty
[19:33] well in 1.3, it renders one is the
[19:35] highest probability.
[19:37] However,
[19:39] if we keep using this, we could see that
[19:41] we can calculate the top largest, we can
[19:43] kind of understand the right value. We
[19:45] could keep scanning for different
[19:46] things. So, for example here, what we're
[19:49] scanning is
[19:52] different weights and biases with
[19:56] uh
[19:57] with different loss func with different
[19:59] uh with different loss func. So, now
[20:01] we're going to change to our loss func
[20:03] to cross entropy we're going to work on,
[20:05] and we didn't haven't generated a 3D
[20:07] landscape for it yet. And we can see
[20:09] we're going over all of the weights and
[20:10] all of the biases in a nested loop,
[20:12] what's going to be the cross entropy
[20:14] output for this digit MLP, right?
[20:18] >> [snorts]
[20:18] >> And the answer is that it's going to
[20:21] look a little bit like this. Why is it
[20:23] so flat before zero? Because in this
[20:27] section here, we're actually like
[20:29] failing to predict uh everything
[20:31] completely. So, that's something to
[20:33] notice. We look at loss landscapes, and
[20:35] we can kind of tell, "Hey, the
[20:38] type of the task we're trying to do and
[20:40] the type of the loss function influence
[20:42] the shape of the loss landscape. Our
[20:44] best performance comes here when like,
[20:46] let's say weight is one and bias is
[20:49] somewhere between uh point five my point
[20:52] minus point five and zero. That's kind
[20:55] of what we can tell from this chart.
[20:56] There's this value here that performs
[20:58] best."
[21:00] Okay. So, exercise, let's visualize the
[21:02] loss value of different uh of different
[21:04] positions.
[21:06] Um
[21:07] and this is an exercise for you. I think
[21:09] that ideally what you could do here is
[21:12] try and like put in different values for
[21:15] input and target class and see how these
[21:18] render differently.
[21:20] Great. So, that was our code for this
[21:22] section. We had We looked at MSE loss.
[21:25] We looked at a cross-entropy loss. We
[21:27] understand we're not going to use MSE
[21:29] loss because we have multiple output
[21:30] probabilities that the cross-entropy
[21:32] loss is going to take care of.
[21:35] So, now let's get to the more conceptual
[21:37] part of the lecture. We kind of did
[21:39] coding. We went through Excel. We went
[21:41] through code. Let's think about loss
[21:43] landscape for large language models. And
[21:45] for that, I think like this image is
[21:47] actually really great.
[21:49] Loss landscape can be very textured and
[21:52] very complex. They don't have to be like
[21:53] very clear valley in the middle. Here we
[21:55] go, I'm optimizing for two parameters.
[21:57] They're actually very, very complex
[22:00] because they represent the geometry of
[22:02] English, the geometry of vision, which
[22:05] are complicated topics. So, this loss
[22:08] landscape in front of you is from a 2017
[22:10] paper that is meant to be used in
[22:12] computer vision, but it shows you kind
[22:14] of the computer vision loss landscape.
[22:16] And when I look at it, I can kind of
[22:18] easily tell you could easily get trapped
[22:21] in some of these little valleys, but not
[22:24] always reach the global maximum. You
[22:25] could get trapped here and you could get
[22:27] trapped here. Your goal is to minimize
[22:29] loss to get the best performance, right?
[22:32] The best ability to speak English or the
[22:34] best ability to solve your vision task.
[22:36] Our goal is to shift towards the global
[22:39] minimum, get to the lowest point in this
[22:41] graph.
[22:43] And specifically for large language
[22:44] models, the global minimum is where next
[22:47] token prediction is ideal. I.e., it most
[22:50] matches the the data that we're going to
[22:51] show it to learn the English language.
[22:55] So, let's say that instead of we're
[22:57] looking at a vision loss landscape, I
[22:59] regenerated GPT-2 loss landscape myself.
[23:03] There's a notebook here if you want to
[23:04] see it. It's based on a 2017 paper. And
[23:07] then when you run through this and you
[23:09] try and generate your own loss
[23:10] landscape, you kind of end up with this.
[23:13] What do we see? We see a big area here
[23:15] in the middle, a big loss drop. That's
[23:19] where we want our our model to get to.
[23:21] But in order to get it, it has to move
[23:23] through this little ring around the best
[23:27] loss performance. And [snorts] sometimes
[23:30] our model can get trapped there as it's
[23:32] trying to kind of like inch its way
[23:34] forward to the best performance, the
[23:36] lowest loss.
[23:41] Okay.
[23:42] I'm going to show you a quick demo
[23:44] because I really love this one demo.
[23:47] And I never remember which button I need
[23:49] to click here.
[23:51] Uh so this is a loss landscape. I think
[23:54] it's one of the vision models from the
[23:55] 2017 paper or 2019 papers.
[23:58] So if I click here,
[24:01] if I click this button, and then click
[24:03] here, we could see if click this,
[24:07] you could see it descending. It's trying
[24:10] to reach the lowest point in the
[24:11] landscape, but it's not super successful
[24:14] in doing that because uh
[24:17] can I Let's see if I can
[24:21] It's not super successful in doing that
[24:23] because it gets stuck here in this
[24:25] little area. And it keeps doing that. So
[24:27] maybe if I give it a little bit more
[24:29] momentum and a little bit more descent
[24:33] rate,
[24:34] Oh my god, now it was able to get to
[24:36] this bottom area pretty quickly. And I
[24:38] could see that in multiple places. It's
[24:41] getting stuck and then it's getting
[24:42] released. Low momentum kind of get stuck
[24:45] in these little poles.
[24:46] Okay, very [clears throat] cool. So we
[24:48] saw this demo of how loss gets optimized
[24:51] over time.
[24:54] Let's talk about a little bit of
[24:55] decisions that we just made. Our
[24:57] decisions for this whole section, even
[24:59] though it was very complex, I think, or
[25:01] it had a lot of math, it actually are
[25:03] really simple. The decision is we're
[25:05] going to use cross entropy.
[25:07] There are lots of other cross
[25:09] There's other There's lots of other loss
[25:11] functions. However,
[25:14] cross entropy is pretty much the only
[25:16] one that gets used for the pre-training
[25:18] phase. So, really important to take note
[25:20] of that. We're going to use cross
[25:21] entropy. We just went through like 30
[25:23] minutes of loss function and loss
[25:25] landscapes and all of those things to
[25:26] get to one line of code. This is really
[25:28] exemplary of how a lot of machine
[25:30] learning works. So, we are going to use
[25:33] cross entropy as our loss function. And
[25:35] next step, we're going to talk about
[25:37] back propagation and how we get to walk
[25:40] down that slope. Well, how do we start
[25:43] from a high point in loss function and
[25:45] then end up fairly in the lowest point
[25:48] of loss that we could get to and have
[25:50] the best English performance. Hope you
[25:52] could join me for this next section. See
[25:54] you soon.
