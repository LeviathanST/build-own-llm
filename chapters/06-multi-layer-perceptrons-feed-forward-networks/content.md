# Multi-Layer Perceptrons, Feed-Forward Networks | Build Your Own LLM Workshop #6

**Build Your Own LLM Workshop — Video #6 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 40m 14s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=6BU9Gj2yoSw |

## Description

No description available.

---

## Full Transcript

[00:00] Hey everyone, welcome back. I'm Justin
[00:02] Angel. Uh let's get started. We're here
[00:06] today reviewing the multi-layered
[00:09] perceptron and feed forward networks.
[00:11] Recently where we left off, uh we were
[00:14] looking at a single perceptron and its
[00:16] activation function and how to implement
[00:18] it. Now the question is what happens
[00:20] when you have more than a one perceptron
[00:23] and our deliverable for the day is to
[00:25] have a feed forward uh network with bru
[00:28] squared working as it would in a
[00:30] transformer. This is going to be our
[00:32] first real component that we're going to
[00:34] be using in our production
[00:36] training pre-training for a large
[00:38] language model. Great. So let's think
[00:42] about perceptrons for a moment. We had a
[00:44] single perceptron. What happens if I
[00:46] have multiple perceptrons? Let's say I
[00:48] have multiple inputs into a perceptron.
[00:50] What we do with that is we sum those up.
[00:53] So previously we looked at wx +b the
[00:58] formula if you have multiple input very
[01:00] similar. It's the sum of the weight of
[01:02] the input multiplied by that particular
[01:05] input and a global bias. Let's say that
[01:08] again. Each input has its own weight. We
[01:12] sum up the input times its weight and
[01:14] then we add a global bias. global in the
[01:16] sense of like for the all inputs. Uh so
[01:19] the sum of weight and input plus bias
[01:22] what does it look like when we implement
[01:23] that? And on the right I wrote code that
[01:25] is intentionally bad but readable. Uh we
[01:28] have the weighted sum is the weight of
[01:32] that index plus the input in that index.
[01:37] All you run that through all of the
[01:38] inputs plus the bias. So if the weights
[01:42] are 3 and 0.1 and the input is one and
[01:45] 100 and then there's only one bias then
[01:48] the sum total is 18. You can run that in
[01:50] calculator. It kind of works. Okay
[01:53] great. So that's kind of confusing but
[01:55] not super clear. Maybe we should look at
[01:57] a demo and this demo is going to be
[01:59] actually pretty involved. We're going to
[02:01] run through multiple examples examples
[02:03] and we're going to try and do that here
[02:05] within the demo. So first thing we're
[02:09] doing is we can see we start off with
[02:11] one input and one bias and one weight.
[02:13] We added a relu function later on and
[02:16] then here we're going to just change
[02:18] back and go like hey actually let's not
[02:21] look at a relu function yet but let's
[02:23] look at two inputs. So input one and
[02:26] input two all leading to the same
[02:27] perceptron. So input one is at one input
[02:30] two is at.5
[02:32] input one has a weight of 1 and a half.
[02:34] Input two has a weight of minus.8. 8.
[02:38] Why is that relevant? Each input can be
[02:40] upregulated or downregulated, right?
[02:43] Based on what we later on learn. And
[02:46] remember, we're trying to learn the
[02:47] English language. So, these weights have
[02:49] a lot of meaning. So, uh we could see
[02:53] the math here. 1.5 * 1 + -.8
[03:00] * half +2 overall 1.3. Okay. So, I could
[03:04] change the input. Oh my god, this input
[03:07] is now negative. So it went really
[03:09] positive because its weight is negative.
[03:10] If it goes really positive, it's going
[03:13] to start moving us towards the uh
[03:15] towards the zero. So the higher this
[03:17] input, the more the closer to zero the
[03:20] output is going to be overall because
[03:22] it's an inverse ratio between them. This
[03:24] input though, oh my god, if I keep
[03:26] increasing it, the values go up and if I
[03:29] decrease it, the values go down. We
[03:31] learn a lot from doing that. And then we
[03:33] have one bias that we add at the end. Oh
[03:35] my goodness. A high bias means a higher
[03:38] overall output. A more negative bias
[03:41] means lower input. So we just we look at
[03:44] every input. Every input has its own
[03:46] weight for one perceptron. Every input
[03:49] has its own weight perceptron.
[03:52] And then we uh sum that up. Okay. What
[03:56] happens if you have two perceptrons and
[03:58] two inputs? Wow, this is going to get
[04:00] real complicated real fast, right? So
[04:03] what let's look at this diagram
[04:05] together. We have neuron A on top and
[04:08] neuron B on the bottom. We have input X1
[04:11] and X2 on the left side. And that would
[04:14] as a result of that the cartisian
[04:16] multiplication of all these two inputs
[04:18] two neurons will have a total of four
[04:22] weights. So the weight between neuron A
[04:26] and and uh input um and the first input
[04:30] is going to be AW1 whereas it's going to
[04:33] have a different weight associated with
[04:35] neuron BW1.
[04:38] Very cool. Total of four weights.
[04:41] Why is that important to highlight?
[04:44] Because the more inputs we have and the
[04:46] more neurons we have, the bigger the
[04:49] number of weights and biases that we're
[04:51] going to have to learn. Okay, so we have
[04:53] weights here and we have biases here and
[04:55] then I threw in RLU back in because now
[04:57] we can like kind of deal with RLU. But
[05:00] each of these neurons or perceptrons
[05:02] have their own output. So again, if I
[05:05] change the output for e for the second
[05:08] input, if I change its weight for the
[05:10] second neuron, it doesn't influence the
[05:12] first neuron at all. Really important to
[05:14] notice that each perceptron has its own
[05:17] uh relationship to each input in the
[05:19] previous layer. Why did I say input in
[05:21] the previous layer? Because now we have
[05:23] two neurons and we have two outputs for
[05:26] them. But maybe our system should only
[05:29] have one output. How do we combine them?
[05:32] We throw in another neuron at the end.
[05:34] Oh my goodness, it's getting real
[05:36] complicated in here, right?
[05:39] We have our two inputs, our two neurons,
[05:42] but those two neurons now fit into
[05:44] another neuron. we move from a single
[05:46] layered p uh network to a multi-layered
[05:50] network. Uh which I think is really
[05:52] interesting. So here we could see
[05:55] because neuron B is actually really
[05:57] negative right now it's blocked by au is
[06:00] not adding any value into this
[06:02] perceptron here into the perceptron that
[06:06] combines both of the um both of the
[06:09] hidden layer neurons together. So let's
[06:12] look at that again. We have perceptron
[06:14] A. It has two weights, two inputs
[06:17] associated with them. We have perceptron
[06:19] B, two weights, two inputs connected to
[06:21] them. Each of them with their own bias.
[06:23] If I bring these values further up
[06:25] though,
[06:27] then perceptron B starts contributing
[06:29] value into the output neuron. Why is
[06:32] that important? Sometimes we could turn
[06:34] off a neuron, sometimes we could turn it
[06:36] on. Right? Reu helps us not necessarily
[06:39] impact the the network too negatively
[06:41] when the values are negative. Okay, so
[06:45] now you must be thinking Justin, what is
[06:47] a actual an actual use case that would
[06:50] ever need to have a multi-layered
[06:52] perceptron like this? Well, there's the
[06:54] sour gate. So is a concept from comps
[06:57] sites like something you really only see
[06:59] when you're learning truth table. A
[07:01] truth table could say if the value of
[07:03] the input is zero or like you could only
[07:05] have zeros or one booleans 0 have zero.
[07:09] If it's one one have zero but only if
[07:13] one of them is positive and the other
[07:16] one is negative or the one of them is
[07:18] true and the other one is false truth
[07:20] tables then we will want to have a true
[07:23] output. There is no way to implement
[07:25] that logic with a single perceptron or
[07:28] even a single layer of perceptrons. You
[07:30] just have to like daisy chain multiple
[07:33] perceptrons together in multiple layers.
[07:36] So here if I turn on option A,
[07:41] our first neuron is contributing values
[07:43] to the output. That's great. If I turn
[07:47] on output B, then it's again ne neuron A
[07:50] that's contributing values to the output
[07:54] neuron. But if I turn both of them on,
[07:56] they're both going to contribute values.
[07:58] And there's a lot of ne there's a strong
[08:00] negative value here in the base and the
[08:02] weight uh on the second neuron that's
[08:04] going to cancel out everything and send
[08:05] it back negative. So you can see the
[08:07] interaction of multiple neurons turning
[08:09] them on and off again to get the results
[08:11] that we want to implement this very
[08:13] simple but very complicated truth table.
[08:17] Okay, so that's as far as we're going to
[08:19] go in this demo. We learned about having
[08:22] more than one input and it's each of
[08:24] them has its own weight. We learned
[08:25] about having multiple neurons each with
[08:28] its own input. So now multiple inputs
[08:29] and multiple neurons. We learned about
[08:31] having multiple layers. So multiple
[08:33] inputs with multiple neurons with
[08:35] multiple layers. We did all of that work
[08:37] all the way up. And we saw one very itty
[08:40] bitty tiny example where that circ is
[08:42] actually critical because there's no way
[08:44] for a machine learning network to
[08:46] represent this concept of either this or
[08:48] that without having a multi-ert
[08:50] perceptron. Right? And there's a lot of
[08:52] times in real life even in language we
[08:54] want to implement either but not both.
[08:59] Great. So we looked at that. That's the
[09:02] and that's the demo that we were
[09:03] building up for. So we were talking
[09:06] about doing inputs of sums. We should
[09:08] also mention there's perceptrons that
[09:10] are multi-layer. We kind of saw that a
[09:12] moment ago. And in multi-layer
[09:14] perceptrons, we just daisy chain chain
[09:16] uh daisy chain layers. How many layers?
[09:18] However many we want, however many
[09:20] architecture makes sense for. But now
[09:22] let's do a little bit of terminology
[09:24] because you're going to hear that a lot
[09:25] probably from me but also generally. Um
[09:28] the first layer of any multi-layer
[09:30] perceptron is called the input layer.
[09:32] The last layer is going to be called the
[09:34] output layer and any layer in between is
[09:36] going to be called hidden layer. Okay.
[09:39] So that's it. That's just what we wanted
[09:41] to like fully uh understand here. Why do
[09:44] we call these networks fully connected
[09:46] or FFNS? If every neuron is connected as
[09:49] an input to every output to every neuron
[09:52] in the next layer, we call it a fully
[09:54] connected network or an FFN for short.
[09:57] As you could tell, I'm using MLP and FFN
[10:00] as pretty much synonymous. They're
[10:02] pretty much synonymous in the concept of
[10:04] LLMs.
[10:06] Great. So, now we showed you a bunch of
[10:08] demos and did a bunch of terminology.
[10:10] Let's look at like a little bit of math
[10:12] and build up intuition. First thing I
[10:14] do, I make a copy. Oh, goodness. And
[10:18] then we're going to work in the without
[10:19] answer sheet.
[10:24] Here we have our single input neuron.
[10:26] neuron is misspelled. Here we go. I'll
[10:28] correct that. So, our input is one. Our
[10:30] weight is one and a half. Our bias is
[10:32] two. How do we write that? Okay. We've
[10:35] done this hundreds of times before.
[10:36] Input times weight plus bias. Hundreds
[10:39] of times for me. Maybe third or fifth
[10:41] time for you. Okay. Now, what happens if
[10:44] we have a multi-layered input? Uh, we
[10:47] should delete this. This shouldn't be
[10:48] here. Then we can do input time weight
[10:53] plus input time weight plus the bias
[10:59] 3.1. We can see we I took the same
[11:01] values you could see here in the demo on
[11:03] the right and it actually explained
[11:04] right here and like if you want to like
[11:06] see the math but you could see the
[11:08] output is correct. Okay, great. Now I'm
[11:12] going to do a little slide of hand on
[11:13] you. Uhhuh. Really fun. I'm going to use
[11:17] something called a matrix multiplication
[11:19] or a matt mole or a mimolt.
[11:27] All three of those are names for the
[11:29] same things. I'm going to use mimolt
[11:31] because that's the name of the function
[11:33] in Excel or sorry in Google sheet. I'm
[11:35] going to say multiply this array
[11:39] with this array
[11:41] and then add two to the bias. Why is
[11:44] that not going to work? Because I had
[11:47] the order wrong. The second thing you
[11:49] multiply is always going to be first in
[11:51] the order of my malt. Just a fun thing
[11:53] to notice. Oh my gosh. Oh. Oh goodness.
[11:57] One sec.
[12:00] Going to kick this array as the second
[12:02] one. Perfect. And now the output is 3.1.
[12:05] Why is my mode slightly easier to use?
[12:09] Because I don't have to do my own
[12:11] additions and multiplications. We ended
[12:14] up by just building perceptrons at a
[12:17] place where linear algebra operation
[12:20] called matrix multiplication or metal or
[12:22] mimalt ends up being really useful to us
[12:25] cuz that is all mimalt does. It just
[12:27] does these additions and
[12:28] multiplications.
[12:30] Okay, cool. We're going to review linear
[12:31] algebra a bit later. Again, don't worry
[12:33] about it.
[12:35] But let's look at a multi-layer
[12:37] perceptron. Okay, so now I'm just going
[12:38] to do math by hand again. input time
[12:41] weight plus
[12:44] uh uh input time weight plus the bias
[12:51] for this first neuron 0.95.
[12:54] This input times the weight that neuron
[12:57] gives it plus this input plus the weight
[13:01] that that second neuron gives it plus
[13:03] the bias. Okay, now we did that. So we
[13:07] have weight and biases. So now we have
[13:08] to and we ran these through RLU. So now
[13:10] I'm going to go this input times the
[13:13] weight that this one neuron gives it
[13:15] times this input times the weight that
[13:17] that neuron gives it the output neuron
[13:19] and its bias. Did we get to the right
[13:22] answer? Close enough. Actually no we
[13:26] didn't. Why did we not get the close
[13:29] enough answer? Because I didn't uh
[13:33] multiply the right value. So let's just
[13:34] stay in this chart for a moment. So we
[13:36] have this chart that shows us the
[13:39] various values
[13:42] um and how to multiply them correctly.
[13:45] Awesome. Uh so let's go back here and
[13:48] try and do that with me or matt. Uh I'm
[13:52] going to use array formula. The only
[13:54] thing that array formula adds to us
[13:56] right now is the ability to have
[13:58] multiple cells influenced by the result
[14:01] of of math. So instead of doing one molt
[14:04] or matt mole per um for each neuron, we
[14:08] could do one matt mole for multiple
[14:10] neurons. So now I'm going to just write
[14:13] that down here. You could see that it's
[14:15] multiplying this array, the input array,
[14:18] and the weight array. And then it adds
[14:20] the bias array to it. Wow, we're saving
[14:22] a lot of operations here. This is like a
[14:24] lot cleaner to work with. Um
[14:28] then we have the next output we have to
[14:30] have like combining both of these
[14:33] outputs from the RLU. So I could just
[14:35] add a space here and then
[14:38] all these inputs multiplied by these
[14:41] weights plus the bias a bit easier to
[14:44] work with. Uh, one thing that you may
[14:47] have noticed that I'm kind of kind of
[14:50] like not showing you here is that like I
[14:53] moved all of our inputs into columns and
[14:56] then there's like a bunch of like but
[14:58] they used to be rows. Why did I do that?
[15:00] Because we have to maintain metrics
[15:03] multiplication dimensions. Um, they have
[15:06] to be like it roughly like uh the second
[15:08] dimension of the first multiplied has to
[15:10] be the second dimens the first dimension
[15:12] of the second multiplied. You don't have
[15:14] to remember that. But in order to
[15:16] maintain that, I had to have a transpose
[15:18] function here. So transpose just takes a
[15:21] column and flips it to a row or takes uh
[15:23] a long matrix and flips its rows with
[15:26] its columns and its columns with its
[15:27] rows. I think of it as like just
[15:28] flipping something over. Okay. So now if
[15:31] I use transpose, I can maintain my input
[15:33] as a row and my weights is like the way
[15:36] that they were before. And then I'm
[15:37] still going to just transpose and add
[15:39] the biases. Great. And then I could do
[15:42] that here as well. So if I transpose, oh
[15:46] my goodness, like everything kind of is
[15:48] a bit more readable because since we're
[15:50] working on readability, one thing is
[15:52] that I don't like is that my biases are
[15:54] in their own weird little world and
[15:56] they're not really and then I have to
[15:57] add them out at the end to wx plus b. I
[16:00] just have to do addition. Why can't we
[16:03] just move the biases to be their own
[16:04] column in the weights? Cuz they're each
[16:07] one of these represents one neuron.
[16:08] That's another neuron. Why can't we just
[16:11] add them to to the to to the weights?
[16:14] Well, the answer is I'm going to have to
[16:16] maintain dimensions for math mall. So,
[16:18] one way of doing that is I could move
[16:20] the biases to be part of this matrix,
[16:24] but or 2D array, but I'll just add a one
[16:27] to the input. The one means that like it
[16:30] gets let's not call it canceled out, but
[16:32] doesn't necessarily influence the
[16:33] results of the math mall. When I do
[16:36] that, we can see 1.4 1.45 45 and 3,
[16:40] which is similar to when I was working
[16:42] earlier here and adding them manually.
[16:44] So, we know it kind of works. That's
[16:47] cool. Now, I want to do the same thing
[16:49] with these rail outputs and these
[16:51] weights. So, I'm just going to add a one
[16:53] here as well. And wow, we got to 1.69
[16:56] again. That's really cool for us, right?
[17:01] Okay. So, now what can we uh uh uh build
[17:05] up with that? I'm going to scroll down
[17:07] for a second. going to look at the sour
[17:08] table. So the sour table again 0 0 0 1
[17:14] right we want the output to only be one
[17:17] for when it's either but not both. So
[17:20] either 0 0 is always negative, it's
[17:22] always false, 1 one is always zero,
[17:25] right? However you want to think about
[17:27] this in true, false, or not, right? So
[17:29] these are all my inputs. I'm going to
[17:30] send all these inputs to this to to this
[17:33] neural network together. These are the
[17:36] weights of the of the matrixes. These
[17:39] are the biases that I've created. And
[17:41] these are the same numbers that we saw
[17:43] earlier. We're looking at the sorate
[17:45] here, right? Every one of these first
[17:47] inputs have a weight of one. And the
[17:49] second set of input uh have uh two and
[17:53] six minus 6. Uh so I'm going to go back
[17:56] here. Okay. So I'm going to just matt
[17:58] malt these together. We're going to have
[18:01] to do the little transpose trick we
[18:03] talked about.
[18:05] Why is this mold with a parameter of
[18:07] one? Which one did I add? Let's look at
[18:09] the width answer so you don't have to
[18:11] watch me debug this together.
[18:13] Great. So when I matt mole these
[18:15] together and then I met these eight
[18:18] parameters and with these four weights
[18:21] good and then I add the biases you could
[18:24] see that it's actually arriving at like
[18:26] an intermediary that may or may not be
[18:28] correct but then I'm going to do that
[18:30] again here in the output I'm going to
[18:32] matt mole it with the weights of the two
[18:34] and the minus 6 and the bias of zero and
[18:37] then I'm going to multiply that with the
[18:38] outputs of that relu and all of a sudden
[18:41] I got the correct output for my truth
[18:44] table, right? Only the first the two
[18:46] middle options, the one that are 1 0 1
[18:49] and 1 0 ended up creating the the
[18:52] correct outputs like the positive true
[18:55] outputs. So now I can move my biases
[18:58] into the weight. Again, we're just doing
[19:00] this little trick where we're adding the
[19:02] biases not as their own row, but as a
[19:04] column in the weights. Then I added a
[19:07] whole column of ones cuz that's how you
[19:09] maintain dimensions. We run through the
[19:12] same math, same math and we arrive at
[19:14] the same truth table at the end. 0 1 1 0
[19:17] which means that for these two inputs
[19:20] the value is true and for these two
[19:23] inputs the value is ne is false.
[19:27] Very cool. So we've now implemented our
[19:30] store example with math mole. We're
[19:34] getting very close to building like a
[19:36] full full feed forward network a full
[19:38] MLP. So now let's look back and scroll
[19:40] up a bit and look at this these MLPS. So
[19:44] one fun attributes all of these
[19:46] maintaining dimensions have is we could
[19:48] actually grow our array and then we can
[19:52] shrink our array. So let's start by
[19:54] creating a bunch of random values here.
[19:56] I'm going to just copy these over. Oh my
[19:59] god, there's a bunch of fun random
[20:00] values here. But if I multiply it with
[20:02] an array array or a matrix that's much
[20:05] bigger than it,
[20:08] I'm going to fill this out. It will
[20:10] actually grow the array.
[20:14] So mad mold
[20:17] with this
[20:19] and this. Can you imagine how many
[20:21] multiplication and additions are
[20:23] happening here? Wow. We just took this
[20:26] array the input and we grew it by a
[20:29] learned. Let's say that this was a
[20:31] hidden set of ways. So now we're like,
[20:34] okay, I've got four neurons, right? But
[20:37] like I can grow them out and then each
[20:41] of them deals with this input.
[20:44] Sorry, this is 16 neurons with four
[20:46] inputs each. That's what this
[20:48] represents. So now I'm went from four
[20:50] inputs to 16 neurons. That's really
[20:53] cool. And I have a lot more capacity to
[20:57] think about those four inputs because I
[20:59] now have 16 neurons thinking about four
[21:02] inputs. Okay. So, can I shrink that back
[21:05] down? Yes, I can. I'm going to create a
[21:08] bunch of random values. And this is
[21:11] going to be the second hidden state,
[21:12] which is going to like shrink it down.
[21:15] Here we go. So, now we have a random set
[21:18] of values. And I can map all these
[21:21] hidden values with this intermediary
[21:24] hidden layer activation.
[21:27] And now we're back to 4x4. So now I took
[21:30] my 16 neurons that I had here. And these
[21:34] were the weights. And the this is the
[21:36] activation of those weights. So input
[21:38] times the hidden weights created these
[21:41] activations. I could shrink it back down
[21:43] to four neurons. Bam. These are the
[21:46] outputs. Why would I do that? Why would
[21:49] I increase 4x and then shrink by 4x?
[21:52] That's how every MLP for every large
[21:54] language model works. You just learned
[21:56] about growing and shrinking. We could
[21:59] have theories about why that's really
[22:01] really great uh to do. And maybe I think
[22:05] I'll cover that a bit in the slide deck,
[22:06] but for now, let's just understand that
[22:09] we increased the size by 4x, we grew it,
[22:12] and then we shrunk it back down. Okay,
[22:15] awesome. So we could do a bunch of other
[22:17] fun shrinking operations. We could do
[22:19] input of five * 4. And then you could
[22:22] see that then in order to like change
[22:25] the dimensions, right? Five 5x4
[22:29] multiplied by math mode by 4.8, right?
[22:32] It's going to create a 5x8. We took the
[22:34] first dimension of the input, the last
[22:36] dimension of the hidden value, and
[22:38] that's going to change the dimensions to
[22:40] that. as long as these two dimensions
[22:42] here match. This is just a way for us to
[22:45] see that we need dimensions to match.
[22:47] Okay, cool. So, I'll create a couple of
[22:49] uh values in here.
[22:52] I create a couple of values here. And
[22:54] then I'm going to want to matt all them
[22:57] together. And what you're trying to take
[22:59] from this example is that we have to
[23:01] maintain the side the dimensions the way
[23:04] that I just mentioned. So this array by
[23:07] times this array.
[23:10] Bam. Right? The first dimension here
[23:14] move to the activation. The last
[23:16] dimension here move to the activation.
[23:18] But these two dimensions the four have
[23:21] to match up. Great. Let's do that one
[23:23] more time. So all we're doing is we're
[23:26] playing around with dimensions. I'm
[23:28] going to just create a bunch of random
[23:29] values. We're learning intuitively how
[23:33] Matt Mole works in linear algebra. And
[23:35] then how we got to math mole is through
[23:38] perceptrons. Okay. So now I have these
[23:41] two arrays. This so what's going to be
[23:43] the final size of the activation is
[23:45] going to be 5 by 16 not 8 by 16. That is
[23:48] a mistake.
[23:51] So I'm going to matt mole this this
[23:55] weight
[23:57] by matrix by these hidden activations.
[24:01] And again, because these two dimensions
[24:04] of eight match between these two
[24:06] metrics, we can make this math mole
[24:08] work. If we were trying to math mole
[24:10] dimensions that don't fit, I'm just
[24:12] going to try and say actually go only to
[24:14] row 1 9 89. Now I'm trying to multiply
[24:17] by 8 by 15. We're going to have less
[24:20] data here, right? Uh but let's say I try
[24:24] to multiply with less columns, right? So
[24:28] instead of going all the way to the R
[24:30] column, I'm going to go to the Q column.
[24:32] So now the the hidden dimension doesn't
[24:35] match. Matt Mole can't help me, right?
[24:38] That's not a math mole operation. These
[24:40] two dimensions, the eight here and the
[24:42] eight here have to match. Great. And
[24:44] then lastly, we're going to want to do
[24:46] one more row here. Actually, I'm going
[24:48] to write this from here and scroll.
[24:53] I'm going to multiply
[24:56] again. 16 matches. 16 matches. So, I can
[24:59] multiply these. I'm going to take this
[25:01] array that's only one. And this array,
[25:04] that's a five.
[25:06] And this array, that's a five. There's
[25:09] this array, that's a five. Here we go.
[25:12] Scrolling is a bit hard. Here we go. So,
[25:15] we got a five by one. And we could do
[25:17] that operation because there's the
[25:18] hidden dimension of 16 between them.
[25:20] Okay. So, let's think about what we just
[25:22] saw in this Excel spreadsheet. We start
[25:23] off with this really basic example. We
[25:26] then worked our way to doing math by
[25:28] hand. Then we used math mole which
[25:30] explained why we needed that. Then we uh
[25:33] did math for multi-layered perceptrons,
[25:36] right? We added an extra layer. Again,
[25:37] we kept doing it by hand. Then we ended
[25:41] up uh with using mimold for multiple
[25:44] layers. You can see it's a bit weird
[25:46] because like now we're using rows and
[25:47] columns in a weird way. So we introduced
[25:49] transposing for that. Right? So now we
[25:52] have transpose in our in our statements
[25:55] which just flips columns and rows to
[25:56] make it more readable. Now we learned
[25:59] the trick of like let's move the biases
[26:01] into the weights and then that just
[26:03] means I have to add a one into the the
[26:05] input columns.
[26:07] Then we learned about hey we can grow
[26:09] and shrink right and growing and
[26:12] shrinking is something every MLP in
[26:14] every large language model does. Uh so
[26:18] then we learned about why growing and
[26:20] shrinking works because we can maintain
[26:22] dimension compatibility. So 5x8
[26:26] right that's going to be the output of
[26:27] these two as long as these two
[26:28] dimensions match the the hidden the
[26:31] hidden dimensions and we did that a
[26:33] bunch of time and finally we also so
[26:35] sore which is how to implement something
[26:37] that we wanted to uh that we thought
[26:41] that we can only implement in a
[26:43] multi-layer perceptron. Perfect. So, we
[26:45] did a bunch of Excel work. Now, let's do
[26:48] even a bit more thinking about linear
[26:50] algebra, which I kind of snuck up on
[26:52] you.
[26:57] In linear algebra, if you wanted to
[26:58] represent a one-dimensional array, you
[27:01] call it a 1D tensor and then you would
[27:03] use PyTorch.tensor and you would give it
[27:05] the one-dimensional array and you would
[27:07] get back a tensor. Why would we do that?
[27:10] because tensors can live in the GPU and
[27:12] CPU and arrays can only live on the CPU.
[27:15] I think I think that statement is true.
[27:18] 2D tensor okay so we have a 2D array
[27:21] here. Let's say we want to represent it
[27:23] on as a tensor in a linear algebra
[27:26] linear algebra we would write it this
[27:28] way using PyTorch. It also follows the
[27:31] syntax of another library called NumPy.
[27:33] Just worth knowing in general if you
[27:34] ever hear the word numpy they have
[27:36] similar syntax with PyTorch. Okay. So
[27:38] then we talked about transposing 1 2 3 4
[27:41] 5 6 1 2 3 4 5 6. We flipped columns and
[27:44] rows. If you ever wanted to do that, you
[27:46] would use T. Why would you ever want to
[27:49] do that in real like in processing real
[27:52] inputs?
[27:53] It's a bit harder to answer that
[27:55] question. It's something that we have to
[27:56] do as part of attention would be the
[27:58] shortest version.
[28:00] Then we learned about matrix
[28:01] multiplication. 1 2 * 3 + 4 1 * 3 2+ 4.
[28:07] kind of looks like having multiple
[28:09] inputs to a neuron. Really, this is just
[28:11] representing one neuron with two inputs,
[28:14] right? If you wanted to do that in
[28:16] PyTorch, you would use the at
[28:17] multiplier. And then I want to kind of
[28:20] show you a math mole example that might
[28:22] confuse you and we'll talk more about
[28:23] that later about like how math mole
[28:26] works. It's let's say I have this 2x2
[28:28] matrix and this 2x2 matrix and I keep
[28:30] using the word matrix and tensor and
[28:32] array kind of interchangeably. That's
[28:34] just me. And we could see it's 0 * 4
[28:38] which is 0 + 1 * 5 which is uh
[28:47] + 6 uh which is 0 + 6 right = 6. So you
[28:53] can kind of see how you do this these
[28:55] exercises and this exercise comes from
[28:57] uh professor Tom Yay and his website
[29:00] that kind of teaches how to do math mole
[29:01] by hand.
[29:03] Okay. Okay. So then we learned about
[29:04] upscaling and down sampling. Upscaling
[29:08] down scaling. Up sampling down sampling.
[29:12] So linear algebra allows us to grow and
[29:14] shrink matrices by multiplying these
[29:16] with different dimension matrices.
[29:21] It's part of every modern LLM
[29:24] architecture.
[29:25] GAVA 2021 explained that the extra size
[29:28] allows models to experiment with
[29:30] patterns and then scrap the ones that
[29:33] didn't pan out. So, as you're thinking
[29:35] about why do I need to have growing and
[29:37] shrinking matrixes matrices in the
[29:40] middle of my uh large language model?
[29:43] Well, the answer to that ends up being
[29:45] something like it's going to think about
[29:48] a lot of stuff that you're not going to
[29:49] see. It's going to need a lot of scratch
[29:51] pad that it could write in and then
[29:53] delete later on. So that's what growing
[29:55] and shrinking does. I think that's part
[29:58] of the answer. I also think part of the
[30:00] answer here is this is where we store a
[30:02] lot of information. These very large
[30:05] matrixes of weights is where we store a
[30:07] lot of knowledge. There's a lot of roles
[30:09] that these growing shrinking MLPS play.
[30:12] But the GVA 2021 explanation really
[30:14] explains why they're useful. They're are
[30:16] basically a scratch pad within the
[30:18] activations.
[30:20] Okay. Okay, so now we did a lot of math
[30:22] and oh my god, Justin, you told me I
[30:24] don't need linear algebra, but now you
[30:25] somehow got me into math moles.
[30:28] Get me back to code. Okay, awesome. So
[30:31] now we're going to write a and we're not
[30:33] going to redo all that in code. You
[30:35] could do that later on. What we're going
[30:37] to do is we're going to build a custom
[30:38] PyTorch module
[30:40] that has linear layers. So linear layers
[30:44] is just a way of saying an array or a
[30:46] matrix, right? So that's a 2x two, two
[30:48] columns, two rows. Then it goes to a
[30:51] relu. Then it goes to linear of two by
[30:53] one. So that's just one two columns one
[30:56] row.
[30:58] We're going to run through that hidden
[31:00] value one relu value one output value.
[31:02] And then we're going to implement the
[31:04] init going to build up the structure.
[31:06] That's how we build every Pytharch
[31:08] module. And the four is going to run you
[31:10] the input through all of those
[31:12] possibilities. And in order to create
[31:14] this MLP, we'll do equals new MLP.
[31:17] uh we also want to maybe create the
[31:19] values that we saw from previous
[31:22] examples right so let's go here and I
[31:26] think these are the values that are
[31:28] embedded in
[31:30] uh this example I think it's for this
[31:33] example yeah it's for this example so
[31:35] you can see we have the value of like 1
[31:38] and8 so I just copied these values 1
[31:41] and8 into the setup function so we can
[31:44] just like see an example of this in code
[31:46] but it's the same circuit you just saw a
[31:48] moment ago. It's the same visual
[31:49] implemented in code. This is a whole
[31:52] this is a multi-layered perceptron. And
[31:54] then I'm going to run these tensors of 1
[31:56] and.5 again 1 and.5. These are the same
[31:59] inputs. And then the output is 1.69.
[32:01] We've seen this 1.69 so many times now.
[32:04] Now it's implemented in a PyTorch custom
[32:06] module. Should we write everything as a
[32:08] PyTorch custom module? Go to the
[32:10] previous section. Figure out what what
[32:13] you think about that. Right? in terms of
[32:14] GPU acceleration. Is this the right
[32:16] layer for us? Maybe we need a PyTorch
[32:17] compile to make this faster. Okay, so
[32:20] now we we have the exact same uh
[32:24] construction for MLP, the same
[32:25] architecture, but now we're going to put
[32:27] different values in it. These are the
[32:29] store values 2 and minus 6. Remember the
[32:32] minus 6 is going to just cancel out
[32:33] positive if they're both positive. We're
[32:35] going to run that with the values of 0 0
[32:38] 1 1 0 and 1 0. And it prints up the
[32:40] correct truth table. Very cool to see.
[32:44] Very cool to see that all we had to do
[32:46] is change the values and this MLP with
[32:48] two neurons and then one neuron ended up
[32:51] create being able to support as well
[32:53] with different values. So now we have a
[32:55] bunch of exercises for you and I would
[32:57] love it if you could do these.
[32:59] One is we're going to want to create a
[33:01] feed forward network or an multi-layer
[33:03] perceptron that upsamples the weights
[33:05] and down samples the weight. Upscales
[33:07] the weights, downscales the weight, then
[33:09] runs to relu squared, right? And then
[33:12] we're going to start with a dimension of
[33:13] 768
[33:14] upscale ratio of four. And then you just
[33:17] need to create the linear layers here
[33:19] that have an input dimension of this the
[33:22] input dimension and then upscales to 4x
[33:25] and then downscales back down. And then
[33:27] the forward tech the forward function is
[33:29] already implemented for you. So you
[33:31] upscale you rail you square and then you
[33:33] down sample.
[33:40] How does that what uh what does that
[33:42] look like when we implement that? You
[33:43] have the answer sheet right here. We get
[33:45] a linear layer of like input and
[33:47] dimension input and then upscale and
[33:49] then we flip those. Great. So when we
[33:52] run that, we can also print it out,
[33:55] right? And we could see this is what the
[33:57] print out looks like for a rel squared
[33:59] upscale downscale growing shrinking MLP.
[34:03] This is roughly what it the output looks
[34:05] like. So you could see, oh my god, 768
[34:07] and 372,
[34:09] 372, 768 growing, shrinking. We could
[34:13] also print out how many parameters are
[34:15] in each uh one of these. So about 2 and
[34:17] 1/2 million parameters per matrix. So a
[34:21] total of 5 million parameters that are
[34:23] trainable weights and biases
[34:26] between these. Uh I will now mention
[34:29] that I've been hoodwinking you a bit.
[34:32] We've been talking about biases these
[34:33] whole time, but really one thing that
[34:35] I'm going to start doing and did I start
[34:37] doing it here? No. But I did it here in
[34:40] this answer for this code. I said bias
[34:43] false. A lot of MLPS in like many LLMs
[34:47] just don't have biases in them. They
[34:49] just disabled that. So now we're down to
[34:51] just weights on neurons. And we can have
[34:53] a conversation about why that is, but
[34:55] that's just the reality of how MLPS
[34:57] often get implemented. So we also have
[34:59] bias force. So now you you should
[35:01] probably be able to do this exercise.
[35:02] You write every single line of code
[35:04] here. More exercise you could do is try
[35:06] and code up an end MLP, right? There's
[35:08] answers here for you. If you want to
[35:09] just copy the values, if you want to
[35:12] implement an or MLP where or right at
[35:16] least one of them has to be positive,
[35:18] you can implement it here using these
[35:21] code. And again, you have the values
[35:22] here. But you could also think about it.
[35:23] You could also code up an MLP that grows
[35:25] to 5 to 8 to 16 to 1, right? And then
[35:29] you have the answer here as well. And
[35:32] then what's the parameter count of that
[35:33] going to be? And then finally we have
[35:35] the bonus reference for this is the code
[35:38] that we saw earlier in the linear
[35:39] algebra slide. This is how you create a
[35:42] 1D tensor. This is how you create a 2D
[35:44] tensor. This is how you transpose a
[35:46] tensor with T. And this is how you
[35:48] matrix multiply math two matrixes.
[35:52] Right? So now you have all of that. Here
[35:53] is reference in code as well. Great. So
[35:56] we did so much work. Let's make a couple
[35:58] of decisions. I think this is maybe one
[36:00] of the first timers we're going to see
[36:01] this kind of slide. How do we build our
[36:03] GPT2 style large language model? We're
[36:07] going to make a couple of decisions. So,
[36:09] first we're going to have two feed
[36:12] forward networks per MLP. One is going
[36:14] to upsample, the other one's going to
[36:16] down sample. We're going to have a RAU
[36:18] squared in between them. And we're not
[36:20] going to use biases. Why? Because most
[36:22] LLMs just don't use biases anymore in
[36:24] MLPS. Hyperparameters. These are numbers
[36:27] that we can like run ablation test
[36:29] experiments and then try and like figure
[36:31] out if they're the right number. We're
[36:33] going to use 768 for the input size and
[36:35] 372 which is 4x 3072 4x on the output.
[36:40] Why are we using those values? Cuz
[36:42] that's what JPT2 did. We are building a
[36:44] JPT2 style transformer. That's all we're
[36:46] trying to do here today. Great. So let's
[36:49] learn a tiny bit more about feed forward
[36:51] networks. There's two demos you could
[36:54] play around with. This is from computer
[36:55] vision. There's multiple levels of math
[36:58] mole here. I'm going to draw the figure
[37:00] two on a board and it's going to do a
[37:03] bunch of matrix multiplication and at
[37:05] the end it's going to say that the
[37:06] output is two. It knows how to recognize
[37:09] that. If you go ahead and then you try
[37:13] and render the number three, then it's
[37:15] going to say that the output is number
[37:16] three. And the way that it's doing that
[37:18] is it's going from the input layer to
[37:19] the convolution, right? And you can see
[37:21] how each of these kind of like looks at
[37:24] the previous layer. It also uses
[37:26] something called convolution which we
[37:27] don't need to have in u large language
[37:30] models. It's something that's almost
[37:32] exclusively used in computer vision.
[37:36] And then there's the feed forward
[37:37] network playground. It's from
[37:39] TensorFlow. TensorFlow is an alternative
[37:41] to PyTorch. So far we've only been using
[37:43] PyTorch and we'll only keep using it.
[37:45] But worth knowing Google has their own
[37:47] solution. And then in this playground we
[37:50] have uh the ability to change uh how
[37:52] many neurons are in each layer. how many
[37:55] neurons are in each layer, how many
[37:57] hidden layers we have, right? And then
[38:00] we could try and train them to separate
[38:02] our data sets. So, for example, here I
[38:04] wanted to train to change the to be able
[38:07] to discern the blue dots from the orange
[38:10] dots, the inner circle. I'm going to run
[38:12] this over multiple time and you could
[38:14] see how it was able to do that. How was
[38:17] it able to use this MLP by changing its
[38:19] weight and its biases but and
[38:22] differentiate between the blue points
[38:23] and the orange points? It used something
[38:26] called loss and through loss it was able
[38:29] to do back propagation. You don't need
[38:31] to know what loss and back propagation
[38:33] is at this point. Loss is going to be
[38:35] our next section and back propagation is
[38:37] going to be the the section right after
[38:39] that. Important to mention this is how
[38:42] MLPS get used in real life. We use a
[38:45] loss function and then back propagation.
[38:48] But worth playing around with this
[38:49] playground. It has a lot of great
[38:50] features that you can like learn a lot
[38:51] from without necessarily writing code.
[38:53] Let's talk about um linear algebra. I
[38:56] kind of snuck that in on you. You do
[38:58] need to kind of have an intuitive grasp
[39:00] on it or not intuitive grasp. You could
[39:02] learn the math. So there's several
[39:04] levels I would recommend here. One is
[39:06] Professor Tom Yay has his math mole by
[39:09] handbook while that you could just do
[39:11] that. You could do like a bunch of
[39:12] matrix multiplication in a in like a
[39:14] little seduku like book. I would really
[39:17] recommend this book for that purpose. He
[39:19] al also is building an online version
[39:21] that's private and not public yet, but
[39:23] he will have something there. You could
[39:25] also sign up to his AI Academy. You
[39:28] could do a bunch of math by hand. And
[39:30] finally, there's a book by Mike Cohen
[39:32] that's to me really well known from his
[39:35] work in mechanistic interperability, but
[39:37] here he just wrote a full linear algebra
[39:39] by code example. So if you learn best by
[39:41] code and you want to learn linear
[39:43] algebra, this is a great book to read
[39:45] through.
[39:46] Great. So we covered everything we
[39:48] needed to on MLPS and feed for networks,
[39:50] you have a bunch of coding exercises.
[39:52] Next up, we're going to learn about loss
[39:54] function. Why do we need loss functions?
[39:56] Because we're trying to get the neurons
[39:58] to have good weights and biases that are
[40:00] going to contribute to the final outcome
[40:02] we're looking for them. In our case,
[40:04] learning of learning English. Awesome. I
[40:07] hope to see you in the next section on
[40:08] loss functions and the one after that on
[40:11] back propagation.
