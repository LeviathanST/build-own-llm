# Random Initialization | Build Your Own LLM Workshop #10

**Build Your Own LLM Workshop — Video #10 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 36m 30s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=-pwr0RMhCg8 |

## Description

No description available.

---

## Full Transcript

[00:01] Hello everyone. Welcome back to another
[00:04] episode of Justin Angel in a room
[00:07] talking about large language models.
[00:09] We're building our own large language
[00:10] model together here. And in this
[00:12] section, we've moved off from machine
[00:15] learning models specifically and how to
[00:17] train them and moved more into
[00:18] transformer architecture. So the next
[00:20] several sections are going to be how we
[00:23] build deep neural networks so their
[00:25] training works. What does works mean?
[00:28] Right. We're going to find out in this
[00:29] section. As always, if you want the code
[00:32] links, it's go justinangel.ai/code-10.
[00:36] And we have Excel-10 for Excel file. Our
[00:40] deliverable for this section is going to
[00:42] be he and RU initialization. What does
[00:44] that even mean? I don't know. We're
[00:46] going to find out together. But first,
[00:48] let's try and define the problem that
[00:50] we're going to try and solve here. And
[00:51] this is going to be the same problem
[00:52] that shared between section 10, 11, 12,
[00:55] and 13. All of them are going to try to
[00:57] tackle the same problem effectively
[00:59] which is uh training can either collapse
[01:02] or or explode. What does that mean? So
[01:07] our problem is we're going to basically
[01:08] take a bunch of randomly initialized
[01:10] number and then we're going to m metrics
[01:13] multiply them together. Why is that a
[01:16] problem? Think about it. We have a bunch
[01:18] of numbers between 0 and one and all
[01:20] we're going to do is a bunch of
[01:21] additions and multiplications of those
[01:22] same number. There's really only two
[01:25] possible outcomes if it's like randomly
[01:27] initialized. And what's going to happen
[01:30] here is either the numbers are going to
[01:32] get very very small all the way down to
[01:34] zero or they're going to get very very
[01:36] big to the point where they can't be
[01:38] contained in floats. If they collapse to
[01:40] to zero, then we lost all of our signal.
[01:42] Our transformers don't work anymore.
[01:44] There's no no information in them. If
[01:46] they've gone to numbers so big that
[01:48] floats can contain them, one, we're
[01:50] wasting a bunch of computation
[01:51] bandwidth. and two, right? Like floats
[01:54] can contain them. Our training will just
[01:56] not work. So our job for the next four
[02:00] sections is going to be to stop that
[02:03] either explosion or collapse from
[02:05] happening. And we call that in technical
[02:07] name gradient explosion or vanishing
[02:09] gradients. And those are two separate
[02:11] problems but overall refer to training
[02:13] collapse. On the left we have one of my
[02:16] favorite gifts on this topic. It's not
[02:18] on transformer architecture. It's on a
[02:20] slightly different architecture. the one
[02:22] that predates Transformers, but it
[02:24] really clearly shows that if you start
[02:26] off with a bunch of numbers represented
[02:28] in white and black, eventually
[02:30] everything kind of converges on gray or
[02:33] zero, right? So over multiple turns, all
[02:36] of these neurons, all of these weights,
[02:39] all of these learnable parameters
[02:41] converge on zero or they could like
[02:44] theoretically explode as well. So that's
[02:47] our problem. If we tr if our training
[02:49] collapsed, why is that a bad thing? Why
[02:51] can't we just run again? Well, I'd like
[02:53] to remind you training takes GPU time.
[02:57] GPU time costs money. You don't want to
[02:59] be the engineer at a frontier lab or a
[03:01] neuro lab that's responsible for
[03:03] training collapsing and costing millions
[03:05] and millions or maybe even more dollars.
[03:08] That is how people get fired. So, we
[03:10] want to be very careful to not have our
[03:12] training collapsed.
[03:15] So now remember we said you don't have
[03:17] to know any statistics for this class. I
[03:20] kind of lied to you. Not really, but you
[03:22] are going to have to learn a little bit
[03:24] of statistics. And this is the moment
[03:25] where we learn it. There's really two
[03:27] types of distributions that we want to
[03:29] talk about. And we're going to talk
[03:30] about them here in the slides, but we'll
[03:32] talk about them more when you get to
[03:33] Excel. So the method by which we
[03:36] generate random numbers could help us
[03:38] prevent
[03:40] training collapse either through
[03:42] explosions or vanishing gradients. Uh
[03:46] uniform distribution right when I write
[03:48] equals rand in Excel that's a random
[03:51] distri that's a uniform distribution
[03:53] between 0 and one means all numbers have
[03:55] an equal likelihood of appearing. So
[03:58] that's uniform distribution and we'll
[04:00] see that again in a moment when we get
[04:01] to Excel. We also have normal or
[04:04] standard distribution. It follows a
[04:07] bell-like curve and it's going to be
[04:09] centered on the mean. So if I say the
[04:12] mean is zero, most numbers will be at
[04:14] zero and then in slower increments
[04:18] decreasing around zero.
[04:20] What are those increments? We call them
[04:23] standard deviations. Um 68% of numbers
[04:26] are going to be within one standard
[04:28] deviation away from the mean. Then uh
[04:31] two standard deviations going to be 95%
[04:33] away from the mean. And finally within
[04:35] three standard deviations we arrive at
[04:37] 99.7% of the mean. That should cover
[04:39] most numbers that we're going to
[04:41] encounter. That also explains why the
[04:43] numbers in our neural networks are
[04:46] learned weights. If we can keep them
[04:48] between like let's say 0 and four minus
[04:50] 4 and four what we're going to end up
[04:52] having is just a nice standard
[04:54] distribution. That explains a lot of
[04:57] that to us. Okay. So now we've seen
[04:59] these two distributions. How do they
[05:01] help us with anything? Um
[05:05] we have activation functions right
[05:08] remember we have we said we're going to
[05:09] use RLU or RLU squared in our case but
[05:12] often it's going to be RLU especially in
[05:14] these first early tutorials. So RLU
[05:17] increases uh the number of zeros we see
[05:20] in any sort of distribution. Why? It
[05:23] takes all of the negative values. So
[05:24] let's say I generate ne normal
[05:28] distribution values between minus4 and
[05:30] four. All of the numbers between minus4
[05:32] and zero are going to get zeroed out by
[05:35] ray loop. Why are zeros a problem?
[05:37] Because all we're doing in matrix
[05:39] multiplication is a bunch of
[05:40] multiplications and additions. Multiply
[05:42] by zero, you get more zeros. Add zeros
[05:45] in addition. That's not going to change
[05:47] the outcome a lot. So rau is actually
[05:50] kind of dangerous to have inside of a
[05:52] thing that just does matrix
[05:54] multiplication.
[05:56] Um which as a result we increase the
[05:58] likelihood of having vanishing gradients
[06:00] or training collapse in general because
[06:02] we're doing all those zero
[06:04] multiplications. This has been a
[06:05] well-known problem with relu. So he
[06:07] kaiming in 2015 I hope I'm pronouncing
[06:10] their name correctly proposed that we
[06:12] have a fun standard deviation that
[06:15] compensates for relu. So instead of just
[06:17] saying, hey, my standard deviation is
[06:19] going to be one and my mean zero, I'm
[06:21] going to come up with a really fun
[06:23] standard deviation and maybe that's
[06:25] going to compensate for ReLU. And the
[06:27] paper that I linked to has that proof.
[06:30] Okay. So what if we have a totally
[06:32] different activation function, Justin?
[06:35] Do we then change our initialization? Do
[06:38] we change our standard deviation? Yes,
[06:40] we do. So tan 10 h and sigmoid those are
[06:43] activation functions we didn't discuss
[06:44] in great detail but we at least saw them
[06:46] implemented in excel spreadsheet we know
[06:48] they have a formula we know that we can
[06:50] calculate them we know that the function
[06:51] of x uh they compress their values to
[06:55] the edges. So if you look here on the
[06:58] screen in the middle left what you're
[06:59] going to see is the chart for 10 and for
[07:04] sigmoid. And you can kind of see the
[07:06] values get compressed to the edges.
[07:07] There's not that many values around the
[07:10] middle range. What does that mean to us?
[07:13] It means it's it ends up performing
[07:16] totally different than RLU and it's
[07:18] going to need its own set of
[07:19] initialization to like not have values
[07:22] collapse. Um so Xavier Glor in 2010
[07:26] proposed standard deviations that
[07:28] compensates for the compression that 10H
[07:30] and sigmoid cause. Now that we've said
[07:33] why we need RLU and 10H sigmoid custom
[07:38] initializations,
[07:39] let's talk a little bit about the
[07:41] formula. Again, we're going to see the
[07:43] formula when we get to Excel in greater
[07:44] detail. But the important thing to
[07:46] remember is we take the number of inputs
[07:48] and outputs. We divide uh we divide two
[07:52] by that and we do a square root. Why do
[07:54] we do that? Well, all of that proof is
[07:57] in the papers. For now, the important
[07:59] thing to remember is actually all we're
[08:01] going to change is the standard
[08:03] deviation based on the dimensions of the
[08:05] inputs and the outputs. Okay, great. So,
[08:07] we said that. Let's just jump straight
[08:10] into Excel. See the problem, see the
[08:12] solution. I think it's going to make a
[08:14] lot more sense to us once we're in
[08:16] Excel. So, as always, first thing I'm
[08:18] going to do is I'm going to make a copy.
[08:21] And then here we go. Make a copy. And
[08:24] we're going to be working in the without
[08:26] answer sheet
[08:28] once we get started here.
[08:31] Great. So I have without answers. Maybe
[08:33] before we get to without answers, I kind
[08:36] of want to show you where uniform
[08:37] distribution came from. Um so let's
[08:40] start with random numbers. Um so if I
[08:43] want to just create random numbers in in
[08:46] Google Sheets, I say Excel, I mean
[08:48] Google Sheets, I'm just going to say
[08:49] equals rand. And this is the random that
[08:51] we've been using for the last nine
[08:53] sections, right? I'm always going to get
[08:55] a number between zero and one. Maybe we
[08:58] just create a bunch of them just so you
[08:59] could see them. Oh my goodness, all of
[09:01] these numbers are between 0 and one. If
[09:03] I wanted to create a normal
[09:04] distribution, I would use norm. I'm
[09:07] going to give it rand as the seed. Zero
[09:10] is the mean and one is standard
[09:11] deviation. I still want most of my
[09:13] numbers between minus1 and one, right?
[09:16] That that's what a standard deviation
[09:18] means. It means we're going to have 68%
[09:20] of the numbers between minus1 and 1. The
[09:22] rest of the number are going to follow a
[09:24] normal distribution roughly between
[09:26] minus4 and 4 between minus3 and three
[09:29] between minus2 and two depending on how
[09:31] many standard deviations we want to
[09:33] have. Okay, so that's the syntax in
[09:34] Excel. We're going to be using it a lot
[09:36] more. Oh my goodness, this number ended
[09:38] up between uh between two and minus2.
[09:42] These numbers tend to hover between
[09:44] minus1 and one, but a few of them are
[09:46] going to be breakaway because of how
[09:48] probability works. Okay, so let's look
[09:50] at uniform distribution.
[09:53] I'm going to go into the distribution
[09:54] sheet. And the reason why it's not on
[09:55] this sheet is because I need 10,000
[09:58] lines of these randoms, right, of these
[10:01] randoms um in order to in order to
[10:07] uh be able to see the law of large
[10:09] numbers take effect here. So here I have
[10:12] rand. I'm just multiplying it and adding
[10:14] a number here. We don't really have to
[10:16] do that. It's just a rand. And I have
[10:18] 10,000 rows of this rand. All of these
[10:20] numbers are going to end up at roughly
[10:22] the same distribution. So let's scroll
[10:24] down. And then we can see normal
[10:26] distribution puts the numbers are
[10:29] roughly a uniform distribution. Even
[10:31] with 10,000, they're not totally equal,
[10:33] but they're getting very very close to
[10:35] that. And here the counts are just how
[10:37] many numbers are this particular number
[10:39] between 0ero and one. Right? And then I
[10:42] snap these two uh columns that are about
[10:45] 0.04 across. Great. So I'm going to copy
[10:48] this chart because I says here you
[10:50] should copy this from distribution. And
[10:51] I copy this here. What's the next thing
[10:53] we're going to want to see? We're going
[10:54] to want to see normal distribution. So
[10:57] normal distribution the thing we always
[10:59] specify standard deviation. So if I say
[11:01] the standard deviation is one and my
[11:04] mean is zero, right? Mean zero, standard
[11:06] deviation one. I'm going to see standard
[11:09] deviation that goes 68% are going to be
[11:11] between minus1 and one. And then I'm
[11:14] going to have other numbers like in
[11:16] other percentages. Okay. So I have
[11:18] 10,000 of these numbers. I'm going to
[11:19] change it back to 4 standard deviation.
[11:22] And you can kind of see that at 04
[11:24] standard deviation, most of the numbers
[11:26] actually do fall between minus1 and one
[11:29] versus at one standard deviation, which
[11:31] is kind of what we've potentially been
[11:32] working with so far. You can see a lot
[11:34] of the numbers kind of fall at minus3
[11:37] 2ish. It doesn't really stop at one. So
[11:39] 04 gets us to like really be between one
[11:42] and minus one. Cool. I'm just going to
[11:44] copy this chart to the without answer
[11:46] sheet. Now we see normal distribution.
[11:48] Again, it's 10,000 numbers cuz we need
[11:50] the law of large numbers.
[11:53] I'm going to shift this a bit up. Great.
[11:55] So, now let's see the problem that we
[11:57] have, which is gradient explosion with
[12:00] uniform distribution. So, so far all
[12:03] we've seen is equals rand. So, I'm just
[12:05] going to repeat equals rand here. I'm
[12:07] going to have a 5x5 matrix. It's going
[12:09] to be kind of hard to see things in a
[12:11] 5x5 matrix. We only have 25 items. We
[12:14] need 10,000. We need 100,000. we have
[12:17] million to see the law of large number
[12:18] really take effect but we're going to
[12:20] try and do this with 25 because I think
[12:22] it's useful over here I already have
[12:24] another uh matrix ready to go so let's
[12:26] matrix multiply them mold multiply the
[12:30] second matrix with the first matrix oh
[12:33] my goodness then I'm going to do relu
[12:36] function on it because we said rel is
[12:38] part of the problem so I'm going to take
[12:40] this
[12:42] cell and then max zero it and I'm going
[12:45] to reset all all the values here.
[12:48] Great. So, I did that once and I could
[12:51] see that the average I got out of this
[12:54] is going to be something like average.
[12:56] What's going to be the average value of
[12:58] this uh matrix, right? And this matrix
[13:02] is it AVG? No, I should I say mean? How
[13:05] do I do this? Let's look at the width
[13:07] answer sheet. And I'm just going to copy
[13:08] it. Here we go. It's average. Oh, I have
[13:12] to say the full word average, right?
[13:13] It's not average. It's not me. Great. So
[13:16] we could see that the average of this
[13:18] first uh result of ma matrix
[13:21] multiplication between m1 and m2 and
[13:23] then running a ru is actually the
[13:25] average of 1.2. Great. Why is that a
[13:28] problem? Let's say that I do that 10
[13:31] more times. Another set of just randomly
[13:33] initialized numbers. Another set of me
[13:36] multiplying the result with a randomly
[13:37] multiplied number. The average went from
[13:40] 1.2 to 3.4. Then the average we do that
[13:43] again goes to 9.2. goes to 22.8, goes to
[13:46] 51.8, goes to 1119.5,
[13:50] goes to 239. We plot that out on a
[13:52] chart. This is what gradient explosion
[13:55] looks like. This is going to be a
[13:57] problem. We run this for 72 layers,
[14:00] which is the number of consecutive
[14:02] metrics multiplication in GPT too small.
[14:04] We're never going to be able to hold
[14:06] these numbers inside of a float anymore.
[14:08] Going to have some real problems. Okay,
[14:10] so we just saw uniform distribution
[14:13] explode, right? Right? You can see the
[14:15] average just keeps increasing
[14:16] increasing. We could also look at other
[14:17] distribution on statistics like
[14:19] variance, not just the the average. But
[14:21] since we don't know what variances,
[14:23] we're not going to do that right now.
[14:25] Great. So now let's talk about normal
[14:27] distribution. You're like Justin. Normal
[14:29] distribution
[14:30] is definitely going to fix all of my
[14:32] problems. I'm not going to have any more
[14:34] explosions and any more collapse. Okay,
[14:37] let's try that together. So we saw the
[14:39] sentence earlier. norm in rand zero give
[14:42] me a mean give me a standard deviation
[14:45] I'm going to lock the mean and the
[14:46] standard deviation because I'm going to
[14:47] copy this a lot and then that is how we
[14:51] get a uniform distribution value around
[14:54] standard deviation
[14:56] uh I'm going to change the stdev to one
[14:58] here just to make it easier to see
[15:00] success or failure great then I've
[15:04] already normed in all of these other
[15:06] values here I've already done the matrix
[15:08] multiplication I've already ran RLU and
[15:11] what we could see is that the variance
[15:14] just really oscillates. So let's go to 0
[15:17] 4 the way that we had this before and
[15:19] what we see from 04 there is always
[15:22] going to or always is hard to say but
[15:25] very often you're going to see the
[15:28] entire gradient collapse and with it all
[15:31] training training collapse gra vanishing
[15:34] gradients problem. So now if I'm going
[15:36] to go to two, what's going to happen
[15:38] now? We're going to almost always have
[15:42] uh exploding gradients. Again, that's
[15:46] not great for us. So we have vanishing
[15:48] gradients, we have exploding gradients,
[15:49] and we have training collapse even with
[15:51] normal distribution. Let's see what
[15:54] happens if I go down to 02. 2 again
[15:58] total gradient collapse, right? Very
[16:01] common to see gradient collapse in these
[16:03] very small numbers. Why did we have 04
[16:06] here? 04 has a slightly better odd of
[16:09] please don't collapse. Okay. Well, we
[16:11] tried and it's still collapsing. But
[16:14] often it won't collapse. Let's figure
[16:17] out why that is. So again, we have these
[16:19] 10 rounds of matrix multiplication and
[16:21] the thing we see is the variance goes
[16:23] down to zero. The amount of change
[16:25] between these is very low. Right? If we
[16:27] go to one, maybe it's like a little bit
[16:30] more stable, but eventually it still
[16:31] starts to collapse again. Cool. So nor
[16:34] uniform distribution doesn't save us.
[16:37] Normal distribution doesn't save us.
[16:38] Maybe there's a value of standard
[16:40] deviation of the normal distribution
[16:43] that will help us out with not
[16:44] collapsing. So let's look at heaing and
[16:47] again we use he he distributions uh when
[16:51] we use relu that is when it is most
[16:54] effective theoretically. We'll look more
[16:57] about we'll learn more about that when
[16:59] we get to the code samples.
[17:01] So, Hiking says we take two and we
[17:04] divide it by the dimension of the
[17:05] inputs. We we're working with a 5x5. So,
[17:08] our input is five. So, 2 / 5. We square
[17:13] root that 6.32. I put 6.32 here, right?
[17:18] Same thing we saw before. We have 10
[17:20] rounds of matrix multiplication in RLU.
[17:22] Oh my goodness. Training still
[17:24] collapsed. Hopefully, we can get it to
[17:26] uncolapse. Maybe here we go. It didn't
[17:28] collapse. I regenerated the numbers and
[17:30] it didn't collapse. It has a good shot.
[17:32] It's stay It's staying stable. Why did
[17:34] it still collapse? Because we don't have
[17:36] the law of large numbers on our side.
[17:38] We're working with a 5x5. If we were
[17:41] working with a 100 by 100, we would
[17:43] almost certainly is a hard word to say
[17:46] here because the proof doesn't prove
[17:47] certainty, but it is a lot less likely
[17:50] to see training collapse here. Great. So
[17:52] now we have uh the right standard
[17:55] deviation to not have a metric
[17:57] multiplication followed by a relu
[18:00] collapse, right? So we as long as we use
[18:02] that standard deviation when we generate
[18:04] our numbers, we're actually going to be
[18:06] in pretty good shape.
[18:09] So that was what are we going to do
[18:11] about 10H though or sigmoid? We said the
[18:15] compressed values. We the compressed
[18:17] values change the distribution make it
[18:19] really hard for us to do a similar
[18:21] solution with standard deviation uh as
[18:24] we did with Hika for relu. So Xavier
[18:27] Gllorad came up with this other formula.
[18:29] It's a 2 divided by the dimension of the
[18:31] input and dimension of the output. We're
[18:33] working with a 5x5. So not super hard.
[18:35] It's the same number for both. 2 / 5 + 5
[18:39] = 2 / 10 the square of2.477.
[18:44] Great. So, I put that number in here. If
[18:47] training, and again, we're using 10H as
[18:49] the function here. If training still
[18:52] collapsed, it's going to happen because
[18:53] we didn't get to the law of large
[18:54] numbers. But let's try to get it to not
[18:56] collapse. Here we go. It kind of looks
[18:58] like it didn't collapse me. I'm going to
[18:59] just keep regenerating and maybe if
[19:01] we're lucky, the law of large numbers
[19:03] will not be needed. Here we go. It's
[19:05] still not super collapsing. Great. So,
[19:08] we've saw how to implement Xavier Glor.
[19:10] We saw how to implement heming this
[19:13] initialization.
[19:15] and we saw why we needed them. Is there
[19:17] another demo? No. Here we go. So that
[19:19] was the those were our demos. We all
[19:22] we're doing is still using normal
[19:24] distribution. We've moved on from
[19:25] uniform distribution. We've moved into
[19:28] normal distributions. Instead of rand,
[19:30] we're going to use norm. We're going to
[19:32] choose mean as still zero. But now we
[19:34] have formulas for SD SD for standard
[19:37] deviation.
[19:39] So, so far we've been have using one hot
[19:42] encoding and I think we started using in
[19:43] section 8 but because section 8 was so
[19:45] so intense I didn't want to give you
[19:47] more material. So now we're going to
[19:49] introduce one hot encoding. It's not
[19:51] really part of initialization but we
[19:52] need to introduce it at some point. One
[19:55] hot encoding right we want to do and
[19:58] this is going to be our sample for the
[19:59] next four sections. A * b modulus c a is
[20:04] going to be between uh 0 99 so 100
[20:07] values. B is going to be between 0 and
[20:08] 99 100 values. C is going to be between
[20:11] 0 and 19. So that's 20 values. And as a
[20:15] result, the output is going to be
[20:16] between 0 and 18, right? Cuz the
[20:17] remainder of dividing by 19 will never
[20:20] be 19. So what are our options to
[20:23] represent that in a neural network? One
[20:25] option is we just have integer encoding
[20:28] that you can see that on top. We just
[20:30] have a B c input. So three inputs, the
[20:32] numbers are integers. and one output
[20:35] which is the output integer.
[20:38] If we were really trying to build a
[20:40] multiplied by b modulus c, we would
[20:43] probably build it that way. But we're
[20:45] trying to work and build skills that are
[20:47] going to be transferable to large
[20:48] language models. Why is that relevant to
[20:51] us? Cuz large language models have a
[20:53] bunch of words as an input and a bunch
[20:54] of words as an output. Each of them has
[20:56] its own probability.
[20:58] As a result of that, we're not going to
[21:01] be using integer encoding. going to use
[21:02] something called one hot encoding. What
[21:04] is one hot encoding? It means that every
[21:06] one of the potential 100 values of A and
[21:09] B and C in the output are going to be
[21:11] represented as their own said group of
[21:14] binaries that they're going to have. So
[21:17] they're going to have a 100 input nodes
[21:18] for A. Only one of them is going to be
[21:20] true. Same for B. Same for C. Same for
[21:23] the output. So what does that mean? for
[21:25] a multiplied by bod modulus c we're
[21:29] going to have 100 options for a 100
[21:30] options for bund 20 options for c I
[21:33] still have 20 220 inputs how many
[21:35] outputs are we going to have we have 19
[21:37] outputs and in the middle we're going to
[21:39] have a bunch of hidden layers so that's
[21:41] something you should think about when
[21:42] you think about the shape of our network
[21:44] why am I teaching about one hot encoding
[21:46] right now because the next slide is
[21:48] going to be a coding slide where we're
[21:50] going to be using one hot encoding for
[21:52] our new domain which is a multip
[21:55] multiplied by b modulus c. We're getting
[21:57] so close to having large language models
[21:59] and language representation. You're not
[22:01] even you're not even sure about that or
[22:03] clear about that, but we're so close.
[22:06] Great. So, let's open up our collab
[22:07] notebook again. I've already run this,
[22:10] so I don't have to run it again. So,
[22:12] let's start with the one hot encoding.
[22:14] We mentioned that if we have one hot
[22:16] encoding, we're going to just get a 100
[22:18] zeros. let's say 100 classes of zeros
[22:21] and then only the one at the end index
[22:23] or the chosen index is going to be true.
[22:26] Okay, so that's our reposition for one
[22:28] hot encoding.
[22:29] Um now we're going to have to generate
[22:33] 190,000 input pairs. Why? 190,000
[22:37] 190,000 100 in inputs for A 100 inputs
[22:40] for B 19 inputs for C. A multiplied by B
[22:44] modulus C. And as a result of that,
[22:46] we're going to have 190,000 uh D items
[22:50] in our data set. We're going to do an
[22:52] 8020 split between those. 80% are going
[22:56] to be held for our training set. 20% are
[22:59] going to be withheld for a test data
[23:01] set. And we're going to see if the
[23:02] network can generalize on that domain.
[23:05] Uh we're going to create a bunch of data
[23:07] sets and a bunch of data loaders. So
[23:09] we're going to have the data loaders for
[23:11] our training set and the data loaders
[23:13] for our test set based on a bass as
[23:16] we've said above. So overall 190,000
[23:19] examples 152,000 go into the training
[23:22] set. The test set is going to have
[23:24] 38,000
[23:25] 219 inputs 19 output. It should be 18.
[23:29] So actually it's yeah 0 to 18 is 19. And
[23:34] then label distribution. Uh yeah, so we
[23:37] have that that as well. Uh what is going
[23:41] to be the structure of our deep neural
[23:43] network? Notice that we started naming
[23:44] things deep neural networks. We're
[23:46] almost not at MLPS anymore cuz our
[23:48] networks are going to get so deep. All
[23:50] DNN's are MLPS. Not all DNN's are MLPS.
[23:54] There's a line summary that you get to
[23:56] draw. I don't personally know where it
[23:58] is. I think it's going to be pretty um
[24:01] pretty terminology driven in a sense
[24:03] that it's not necessarily real.
[24:05] So what's going to be the structure of
[24:07] our DNN for this section and we're going
[24:09] to have similar DNN's for the next four
[24:12] sections where we work through concept
[24:14] relevant to large language models. So we
[24:17] take in the input dimension we take in
[24:18] the output dimension and we get a
[24:21] boolean that says use 10h. What does use
[24:24] 10h do? Use 10h determines if you're
[24:26] going to use the 10h activation function
[24:28] or the relu activation function. That's
[24:31] just a boolean. Then we're going to have
[24:33] n sequential. I think this might be the
[24:35] very first time we've seen N and
[24:37] sequential. So we should talk about
[24:38] that. We've seen N and linear, we've
[24:40] seen ReLUS and so on. But if we have a
[24:43] sequential group of modules, we could
[24:46] just execute them in sequential. And
[24:48] then our forward method is just very
[24:49] simple. We only do one invocation for
[24:52] the whole sequential. So what's in our N
[24:54] sequential? We start with our input
[24:56] dimension of 220. We're going to grow
[24:58] that to 512 x 512. We're going to do
[25:00] another 512 x 512. That's pretty
[25:03] uncommon to have equal dimensions. But
[25:05] for now, I'm just trying to make a
[25:07] really long a very long neural network.
[25:10] After each of these, we're going to have
[25:11] our activation function. Activation
[25:13] function. Activation function.
[25:14] Activation function. So, we're going to
[25:15] go 5 input dimension to 512. 512 is
[25:18] going to stay 512. 512 is going to go to
[25:19] 256. 256 goes to 256. 256 goes to 128.
[25:23] 128 goes to output dimensions. Great.
[25:26] Each one of those has an activation
[25:28] function following it. And that's going
[25:30] to be a deep neural network. Why did I
[25:32] do that? Because we need a lot of matrix
[25:34] multiplications to even see training
[25:36] collapse or not. So this is like the
[25:39] minimal number that I was able to build
[25:40] for that. I was able to build for that.
[25:43] Maybe there's a lower number. What is
[25:45] the total number of parameters for this
[25:47] network? This is just a neural network.
[25:49] So we have 68 thou 68,000
[25:55] parameters learnable parameters,
[25:56] learnable weights and biases. What is
[25:59] the structure? It's linear 220 followed
[26:03] by RALU linear 512 512 followed by RLU
[26:06] and so on. We're pretty used to reading
[26:09] print statements by now on models.
[26:12] Great. So how does our training script
[26:15] look like? We're going to hardcode some
[26:17] learning rates, some weight decay, some
[26:19] number of maximum epics we're going to
[26:21] have. We have a bunch of history here.
[26:23] These are methods that are going to be
[26:25] coming along with us for the next four
[26:26] modules. We have this function called
[26:28] evaluate. And then that's just going to
[26:30] check the training or test set and give
[26:33] us our accuracy percentages.
[26:35] And our new new method that's going to
[26:38] help us handle
[26:40] gradient collapse or vanishing gradients
[26:43] is the net weights method. And then it
[26:46] gets a string and it says if you see the
[26:48] word uniform, use nn init uniform. If
[26:51] you see the word he use n caming normal.
[26:55] If you see Xavier, use Xavier normal.
[26:58] And if you don't see any of that, just
[27:00] use a bunch of zeros. We're not going to
[27:02] do that here. Great. So now we have a
[27:04] training uh method. We've said every
[27:07] training loop is going to always follow
[27:09] the exact same uh format. So we're going
[27:14] to have we're going to initialize our
[27:16] model. We're going to pass in the use
[27:18] 10h or not. So use rail or use 10h.
[27:21] we're going to move it to the GPU and
[27:25] we're going to apply the initialization
[27:26] method that's listed here. So based on
[27:29] the initialization method that we get
[27:31] from the method from the function, we're
[27:34] going to call initate weights and it's
[27:36] going to apply to to our model. We're
[27:37] going to use an optimizer atom w. All of
[27:40] our examples are going to be in atom w.
[27:42] We're going to use a loss function cross
[27:44] entropy. We've seen that before loss
[27:46] function. We're going to start a
[27:47] training loop running for a maximum
[27:49] number of epochs. We're going to run the
[27:51] model. We're going to calculate loss.
[27:53] We're going to zero out the gradients.
[27:55] We're going to do a forward step. And
[27:56] actually here, the zeroing out of grads
[27:58] has to be in the pre has to actually
[28:00] move up here. So that might cause a bug
[28:02] or two, but I'm not going to do that
[28:03] right now. Great. Uh then we're going to
[28:07] at the end of each epic, we're going to
[28:08] check what our training loss is, whereas
[28:10] the test loss is. If it's 100% on both,
[28:14] we're going to stop. We will only stop
[28:16] at 100% of both. Why? we're a pretty
[28:18] deterministic
[28:20] domain. And then if we didn't reach 100%
[28:23] accuracy on both training and test by
[28:25] 100 epochs, then we're going to throw an
[28:28] error and we're going to say that. Okay,
[28:30] awesome. So the first thing we're going
[28:32] to test is uniform distribution. So
[28:35] train run in uh training for uniform use
[28:40] uh 10h false. So that's going to use
[28:42] relu and it's going to do uniform plus
[28:45] effectively. Let's run that. How does
[28:47] long does just uniform plus rel uniform
[28:50] every number has equal probability to
[28:53] manifest? How many how many uh epics
[28:57] does it take to converge? You know by
[28:59] the end of a 100 epics it kind of
[29:01] converge by epoch 85. That's if you use
[29:04] uniform and relu. So 85 epics for
[29:07] something to converge on a multiplied by
[29:10] b modulus c. That's kind of slow even
[29:13] though we have a really deep neural
[29:14] network. That's kind of slow.
[29:17] Okay. So let's change let's use he
[29:21] um initialization with relu. So use 10 h
[29:25] false just means relu he plus ru. How
[29:28] what is that going to take us? Wow we
[29:30] converging 25 epics. That's more than a
[29:34] third faster. That's 3x faster. 3x
[29:36] faster means that we are able to save 3x
[29:39] on our GPU time. 3x on our compute
[29:42] budget. A lot of money was saved here.
[29:45] Great. So we now saw a real demo of
[29:47] using hea mean being a lot faster than
[29:50] having a uniform distribution um with a
[29:54] really great. So now you have your own
[29:57] exercise. It's go ahead and implement
[30:00] Xavier and 10h. You're going to want to
[30:02] use the 10H true and you're going to
[30:04] want to say that we use Xavier
[30:06] initialization. I'm not going to show
[30:08] you the code, but you can click show
[30:09] code here if you want to. What does that
[30:12] look like? Okay, so it's converging, but
[30:14] it's not converging super fast. But at
[30:17] 100 F epics, it didn't actually fully
[30:19] converge. So I do want to mention this
[30:21] is maybe the reason that even with a
[30:23] really great initial initial
[30:25] initialization function for Xavier,
[30:30] we still don't want to use 10H in deep
[30:32] neural networks. It it's just slower to
[30:34] converge. So that's the reason why I
[30:36] didn't teach you a lot about 10H and
[30:37] sigmoid earlier. It just doesn't really
[30:39] converge in deep neural networks. I'm
[30:42] doing a lot of heavy lifting but doesn't
[30:44] really but still worth highlighting
[30:46] that. Okay. So the next exercise you
[30:48] have is use Xavier plus RLU. We said we
[30:51] use heaing initialization with RLU but
[30:55] what happens if we choose to use Xavier
[30:57] glor initialization. Great. So we're
[31:00] going to not show you the code for that.
[31:02] Should be pretty straightforward. We use
[31:04] use 10h false. We say initialization
[31:07] Xavier. You've got the code here if you
[31:08] want to see it. It's one line. If we run
[31:11] that right, what's your guess? It
[31:13] actually converges at about 50 epox.
[31:15] It's still a lot faster than uniform.
[31:18] Just switching our our activation
[31:21] function from 10H to RLU meant that we
[31:24] converge at less than 100, right? We
[31:26] stopped the previous previous run at 100
[31:29] epics. We were able to converge at 50
[31:31] here. So, it's at least 2x faster, if
[31:33] not more. So, just not using 10H, we
[31:36] just learned something really valuable.
[31:38] Great. Let's print out a comparison. I
[31:40] really recommend you try and do those
[31:42] exercises. Get connected to to a GPU.
[31:45] Try and run these cells. Try and run
[31:47] write these cells. You're going to learn
[31:49] a lot from that. So, when I compare
[31:51] these, we have accuracy on the left and
[31:54] loss on the right. Let's look at just
[31:56] accuracy. Oh my goodness, that's very
[31:58] zoomed in. Let's look at just accuracy.
[32:01] The fastest to converge very clearly,
[32:04] right? test accuracy
[32:06] uh for he and relu the red line did
[32:09] super well a little bit longer is Xavier
[32:13] and Ru why is that cuz you could see
[32:15] that the it was really hard for it to
[32:17] converge all the way to 100%. They kind
[32:19] of worked at the same rate all the way
[32:21] to full convergence. But when the
[32:23] numbers get really really small, it's
[32:24] harder for it to converge. When the
[32:26] differences get really small, it got
[32:27] trapped in a local minimum here. I can
[32:29] see that's there's this big bounce here.
[32:31] It had to find its way out of it. Right?
[32:33] So Xavier and Rail still much better
[32:36] than the alternative of uniform in Rail,
[32:38] which is this yellow line. So so far up
[32:40] until section 10, we've been using
[32:42] uniform distribution for everything.
[32:44] You're never going to use uniform
[32:45] distribution for deep neural networks.
[32:47] never is doing a lot of heavy lifting in
[32:49] that sentence, but it's roughly true for
[32:51] large language models.
[32:53] And finally, the slowest of the slow,
[32:55] it's Xavier plus 10h. Even though Glor
[32:58] distribution or GLOD initialization is
[33:01] meant to be used with 10H, 10H is just
[33:03] not built for deep neural networks. On
[33:06] the right, we've got our Teslas and you
[33:08] can see our Teslas basically dropped so
[33:10] quickly for Heru that it was perfect
[33:13] within like 20 epics. Then you could see
[33:16] Tesla's and Tesla's function uh just
[33:19] dropping pretty quickly. You can see it
[33:21] didn't really work well for Xavier
[33:23] Glor's distribution with 10H because 10
[33:26] is just not built for a DNN. Great. So
[33:28] now we saw that we have our little table
[33:30] here. He Ru won Xavier and Ru kind of
[33:34] second place. Uniform and RO third
[33:36] place. Xavier and Tana just didn't
[33:38] converge it within 100 epox. Great. So
[33:41] we saw code for that. you have exercises
[33:44] that I really think you should do. Try
[33:46] and write the Xavier and 10H code
[33:47] yourself. Try and write the Xavier and
[33:49] Rail code yourself. If you want to be
[33:50] extra challenged, don't use any of my
[33:53] helper methods. Use the uh the DNN. Use
[33:56] the MLP that I created, but try and
[33:58] write your own training loop. You're
[33:59] going to learn a lot from the process of
[34:01] doing that. What's here on the left?
[34:04] Here on the left, you can see a fun
[34:06] illustration that Gemini was kind enough
[34:08] to generate for me. And it has the torch
[34:11] n innit name space within pytorch. It
[34:14] has all of the uh distributions we work
[34:17] with random distributions uniform normal
[34:19] and trunk normal. It has a bunch of
[34:21] constants we could use. We saw using
[34:23] zeros for example. And then it has the
[34:26] scale distribution of Xavier and kiming.
[34:29] Right? So now we have those as well. Uh
[34:32] and we could do kiming for normal or you
[34:34] could do kiming for uniform. There's
[34:36] also uh equations for those. I only
[34:39] showed you the standard normal
[34:40] distributions for Kiming and Xavier, but
[34:43] there are also distributions for
[34:45] uniform. Again, not going to work super
[34:48] great within deep neural networks. And
[34:50] here you have our little snippet of code
[34:52] of like this is how I would use
[34:54] initialization when I was you when I'm
[34:56] using PyTorch.
[34:59] What decisions are we going to make as a
[35:00] result of that? We're going to use
[35:02] heaing normal initialization alongside
[35:05] our RLU activation function. Again,
[35:07] we're using RU squared. Maybe that's not
[35:09] ideal for Heihiking, but it's better
[35:11] than using a uniform distribution for
[35:13] sure. And here I want to finish off with
[35:15] a quote from Corpathy. You could tell
[35:17] that I really love quoting him. Baby
[35:19] zebras don't randomly spasm their
[35:21] muscles. I think about this quote a lot
[35:24] when I think about initialization.
[35:26] I think that if we had really great
[35:28] initialization fe fun functions uh or
[35:31] distributions, we could probably
[35:33] converge a lot faster. And I'm sure this
[35:35] is something that the Frontier Lab spend
[35:37] a lot of time thinking about internally
[35:39] because shifting your distribution by a
[35:41] little bit can actually cut back on
[35:43] training time by a lot. The Carpathy
[35:45] quote says something really important.
[35:47] Baby zebras, they learn how to walk
[35:48] right right away. They have some sort of
[35:51] wisdom in their pre-initialized neurons,
[35:53] right? They don't just randomly spasm
[35:55] their their muscles. He said that in a
[35:58] context of RL reinforcement learning.
[36:00] I'm thinking about this quote in the
[36:02] context of initialization. I think it's
[36:04] a really relevant quote. Great. So, we
[36:08] talked a lot about initialization. What
[36:10] are we going to be talking about next?
[36:11] Residuals. Why are we going to be
[36:13] talking about residuals in our next
[36:15] section? Well, if we keep adding more
[36:18] and more layers, training will keep
[36:20] collapsing, right? Initialization alone
[36:22] won't fix it. And we're going to cover
[36:23] why that is when we get to our next
[36:25] section. I hope to see you then. Thank
[36:27] you and bye-bye.
