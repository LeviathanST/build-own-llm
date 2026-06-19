# Residuals | Build Your Own LLM Workshop #11

**Build Your Own LLM Workshop — Video #11 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 27m 32s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=e5V7QaHq5lQ |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to another
[00:02] fun episode section of Justin Angel in a
[00:05] room talking about large language models
[00:07] as we build our own large language
[00:09] model. In this section, we're going to
[00:12] cover residuals. Our key deliverable
[00:15] deliverable is going to be an addition
[00:16] residual. And as always, you have the
[00:18] links right on top of the screen for
[00:20] code in Excel. So why do we need
[00:23] residuals? That's going to be the first
[00:24] question you might be asking the
[00:27] residual stream. Right? The problem that
[00:29] we have is the further the deeper the
[00:32] network becomes, the more layers we add,
[00:35] we're still going to see training
[00:37] collapse either through gradient
[00:38] explosion or vanishing gradients
[00:40] problem. So for example, our A
[00:44] multiplied by B modulus C earlier in the
[00:47] previous example had about seven layers,
[00:49] right? We went from like 512 from input
[00:52] to 512 to 256 to 108. We ended up at 18
[00:57] 19 outputs, right? So we had seven total
[00:59] layers. Unfortunately, GPT2 style small
[01:04] networks have 72 consecutive matrix
[01:07] multiplications. That's the minimum
[01:09] amount that it has. So as a result of
[01:13] that, we need our data, our signal, our
[01:16] weights, our activations to be able to
[01:19] carry forward to 72 layers. That really
[01:23] wouldn't work with any of the techniques
[01:25] we've learned so far. So far, the
[01:27] techniques that we've learned allow us
[01:29] to survive maybe, let's say, 10 20
[01:31] layers in 2015. The residual net paper
[01:36] that's linked here solved for really
[01:38] deep neural networks. And the way that
[01:40] they did that is they introduced
[01:41] something they call the residual stream.
[01:44] Residuals are very, very complicated.
[01:46] You could see the formula right in front
[01:47] of you. No, I'm just kidding. It's
[01:48] actually pretty straightforward. the
[01:50] residual
[01:52] is x plus whatever the fun the output of
[01:55] function x uh the function that takes x
[01:58] as input. So for example here on the
[02:00] right you can see the original ResNet
[02:02] 2015 paper it has two layers and then it
[02:06] just adds the results of the input of
[02:09] the be before we can before we process
[02:12] these two layers we just add those to
[02:14] the output and we do that again and
[02:16] again and again and again and again and
[02:17] again. That's a an addition residual. So
[02:21] why does that work? We're going to cover
[02:22] that in a moment but let's just stop and
[02:25] think about the technique. The technique
[02:27] just means we're going to be executing
[02:30] an addition of the input of the two
[02:33] layers before before it went into those
[02:36] two layers and we're going to add that
[02:37] to the output. Great. The way that I
[02:40] think about that is residuals are
[02:42] shortcuts, right? There are ways for
[02:44] data to not get lost in the network. The
[02:46] network doesn't have to work really
[02:47] really hard to maintain data. It can
[02:50] just like keep sending it through uh
[02:53] through the network. So, are there
[02:56] multiple types of residuals? Yes, you're
[02:58] not going to necessarily use most of
[03:00] these, but we should at least cover
[03:02] them. So, one option is the 2015 edition
[03:05] residuals. Those are the ones that are
[03:07] most common both in papers and in open
[03:09] source models.
[03:11] Another one is something called a
[03:12] highway residual. I call it scaled resid
[03:15] I call it a sorry, I'm talking about the
[03:17] scaled residuals now. So, scaled
[03:19] residuals introduced in 2015. What they
[03:22] do is they add things with a small
[03:24] multiplication. Why is that important
[03:27] for us to use a small multiplication?
[03:29] Because if we add X and FX together and
[03:32] they're both the same magnitude, you
[03:34] could see how the magnitude is going to
[03:36] increase over time, right? X plus FX
[03:39] both in the same magnitude. Now we
[03:40] double the magnitude. So scaled is can
[03:43] be used. Not super common in large
[03:46] language models. Another option is uh
[03:50] highway or gated where we have a bunch
[03:53] of learned weights that we're going to
[03:55] multiply our residual by. So instead of
[03:58] just a single scalar integer we're going
[04:00] to multiply it by a gate of some sort.
[04:04] Um great. And then finally about 2 3
[04:08] months ago um the KI team introduced the
[04:13] attention residuals. So residuals really
[04:16] only add stuff from the previous layer
[04:19] into this current layer. Really only add
[04:22] the activations from the previous layer
[04:23] to this layer. [snorts]
[04:25] Attention residuals can look at the
[04:27] entire network have learned parameters
[04:29] to learn when and where to get stuff
[04:32] from a lot of previous layer. The deeper
[04:34] your network, the more it can have back
[04:36] access to get stuff from previous
[04:38] layers. Why is that important? Well,
[04:40] we're going to learn about what
[04:41] different layers do and then we're going
[04:43] to figure out why we would want to go
[04:44] further back in time than the previous
[04:46] layer. I'm pretty sure that manifold
[04:49] constrained attention and all of that
[04:52] comes with it, the their custom
[04:55] residuals, they're going to probably be
[04:56] the wave of the future. It's currently
[04:58] not what everyone's using, but as far as
[05:00] I could tell, by the end of 2026, early
[05:03] 202 and 7, a lot of open source models
[05:05] are going to be using this. Great. But
[05:07] right now, most people still use
[05:08] additive residuals.
[05:11] So, let's go into an Excel demo and
[05:13] maybe see what residuals look like in
[05:14] person. We could see here in front of
[05:17] us, we have uh and I'm going to just
[05:19] going to make a copy.
[05:21] We could see that what we have is uh
[05:26] metrics addition using math. So, let's
[05:28] do that math ourselves. We're going to
[05:30] do it without answer sheet. Uh metrics
[05:34] addition is actually pretty simple.
[05:35] We're going to add the same position in
[05:38] both matrixes of equal size. So here we
[05:41] go. That's just doing addition, right?
[05:44] Uh another option is we could use the
[05:46] matrix addition uh itself. So we're
[05:49] going to say array formula. Oh, array
[05:52] formula.
[05:53] We're going to take this entire array.
[05:56] We're going to add it to this array.
[06:00] Here we go. And we just did roughly the
[06:02] same operation, right? It's equivalent
[06:04] to doing just additions on the same
[06:06] position. So now you know how to do
[06:07] additions cell by cell and you know how
[06:09] to do that for the entire matrix by just
[06:12] using array formula. We use array
[06:14] formula because we're the output of the
[06:17] cell is is going to spread to multiple
[06:19] cells. This is just a Google sheet
[06:21] thing. Great. So now let's look at a
[06:23] residual at the residual addition now
[06:25] that we know how to do addition in
[06:26] Google Sheets. So we have matrix one and
[06:30] we're going to m multiply it by an
[06:32] input. So I'm going to mimalt the matrix
[06:36] one learnable parameters with an input.
[06:42] Here we go. Great. We can see that these
[06:44] numbers are pretty high. And then we're
[06:47] going to add the residual to the results
[06:49] of the multiplication. So we're going to
[06:51] do addition on both of these. And again,
[06:54] like we said, we have to do array
[06:56] formula because we have multiple cells.
[06:59] They're going to be the output here.
[07:01] Array formula. Here we go. That's it.
[07:04] That is the simplest version of a
[07:06] residual addition. The rest of this
[07:08] Excel spreadsheet and the rest of this
[07:10] section. Really simple. We're going to
[07:12] give you a lot of context. We're going
[07:14] to complicate this a lot more, but
[07:16] realistically, this is it. You now know
[07:18] everything you need to about residual
[07:19] addition. It's a residual addition, a
[07:23] matrix addition after a m matrix
[07:26] multiplication.
[07:27] Great. So, is that really what we do
[07:30] with residuals? No. We often do two
[07:32] rounds of matrix multiplication, right?
[07:36] Often it's going to be uh we're going to
[07:38] do some attention or we're going to do
[07:40] MLPS. Our MLPS are going to have like we
[07:43] said growing shrinking. We're going to
[07:44] see two sets of matrix multiplication.
[07:47] Great. So, how is that going to look
[07:48] like? We're this looks much closer to a
[07:51] real MLP that we're going to have in our
[07:53] transformer. We're going to have an
[07:55] input. We're going to have two matrixes
[07:57] with learned weights, matrix one and
[07:58] matrix 2. We're going to mat this first
[08:02] one to input with matrix one. Then we're
[08:05] going to mat the activations for input
[08:09] mat matrix one with a matrix mall of
[08:12] matrix 2. So we did two two of these.
[08:16] Finally, we're going to ru how does it
[08:18] really work? Max zero. And at the end,
[08:21] we're not going to stop here and then
[08:22] just do another round of matrix
[08:24] multiplication and ru matrix
[08:25] multiplication ru. What we're going to
[08:27] do is we're going to add the outputs of
[08:28] the ru array formula
[08:31] ru
[08:33] plus the inputs to the to this section
[08:37] or layer of the neural network. And here
[08:39] we go. We just did an array an addition
[08:42] residual for a fairly complex MLP that
[08:45] has two rounds of math mall and array
[08:48] loop.
[08:49] Not a lot of difference from just doing
[08:51] it for one, but worth seeing that the
[08:53] structure can just be more complicated.
[08:55] Great. Another type of uh residual that
[08:59] we haven't seen thus far is
[09:00] concatenation that is used as part of
[09:03] the attention mechanism. So I just want
[09:05] to teach you this right now. We'll see
[09:07] it in action when we get to attention.
[09:09] That's like section 17. It's so far from
[09:10] us. Why even teach this now? But so we
[09:13] have matrix one learnable weights. We
[09:16] have an input. We math mold them. What
[09:18] does a concatenation look like? We're
[09:20] going to take the outputs here
[09:25] as is. We're going to take the input of
[09:28] the matmo
[09:31] and put them here. And all I did was
[09:33] just concatenate these two together.
[09:35] Right? Does is that going to cause a
[09:37] problem later on? because we're going to
[09:38] have to shrink it. Yes, but we'll see
[09:40] all of that when we get to transformers.
[09:42] But that's just another type of
[09:43] residual. This is a concatenation
[09:45] residual. So you could see that the
[09:47] signal has been maintained to 100%,
[09:49] right? Actually pretty cool residual
[09:52] when you think about it.
[09:54] And then we have scaled residuals. So
[09:56] scaled residuals, we said they're going
[09:58] to have a multiplier after the input is
[10:02] multiplied by a learnable parameters by
[10:05] learnable weights. This is just m matrix
[10:08] multiplication. So first we're going to
[10:10] multiply the output of the matrix with a
[10:15] multiplier. If I just do this, it's
[10:17] going to error out because it's going to
[10:18] say I'm going to have multiple cells
[10:20] here. So we're going to need array
[10:22] formula.
[10:24] Here we go. So now I multiplied it by
[10:26] half. And then after I multiplied by
[10:28] half, I can add the input. I can add
[10:32] array formula. I can add this output
[10:35] from the multiplication with the inputs.
[10:41] [snorts] Great. Why would I do a
[10:43] multiplier of half? Think about it.
[10:46] We're adding x to fx. We're going to
[10:48] keep increasing the magnitude unless we
[10:50] do something like scaling, which is why
[10:52] scaling actually works pretty well in
[10:55] some deep neural networks. Okay, so that
[10:58] was all of the residuals we're going to
[10:59] see. We saw concat, we saw scaled
[11:02] residuals, we saw concatenation
[11:04] residuals, we saw addition residuals,
[11:06] and more importantly, we saw an addition
[11:09] residual in something that looks very,
[11:11] very, very close to the type of MLP that
[11:14] we're going to have inside of our
[11:16] transformers, inside of our large
[11:18] language models. Why is that kind of
[11:20] different still? Earlier, we saw growing
[11:22] shrinking MLPS. We saw that in section
[11:25] six. So, we're going to keep that in
[11:27] there as well.
[11:29] But other than and the dimensions are
[11:30] going to be different. But other than
[11:32] those two differences, this is
[11:33] effectively the MLP layer that we're
[11:36] going to have inside of our large
[11:37] language model. So worth knowing that.
[11:40] Let's look at a little bit of code. And
[11:42] again, we're going to just keep going
[11:43] with our previous example of a
[11:46] multiplied by b modulus c. We're not
[11:49] going to shift from that example for the
[11:50] next three sections.
[11:53] So our data set, we're going to build
[11:55] the data set the way we've always built
[11:56] a data set. A + B A multiplied B modulus
[12:00] C is going to have 150,000 examples in
[12:04] training, 38,000 examples in test. No
[12:07] difference than what we did previously.
[12:10] Our deep neural network I'm going to
[12:11] make kind of really deep. So I'm going
[12:14] to say that we're going to get the layer
[12:16] depth here. We're going to use 19
[12:19] layers. So a total of 20 layers in sorry
[12:21] 21 layers input and output as well. So
[12:24] we have layers as a module list. This is
[12:26] going to be the first time we've seen a
[12:28] module list. And we're going to say to
[12:30] the module list just append n linear to
[12:33] the number of of layer depth. That's one
[12:36] way of writing it. There would be other
[12:37] more native ways in Python to write it.
[12:39] I just showed what is clearest to me.
[12:41] And then we're going to just run them
[12:43] between the same set of hidden
[12:44] dimensions. You know, right now we're
[12:47] just trying to learn about how deep
[12:48] neural networks work. Normally they
[12:50] would shrink. Normally they would grow.
[12:51] Normally they would do something
[12:52] interesting. We normally would not have
[12:55] uh matrixes of the same input and output
[12:57] dimensions repeat themselves many many
[12:59] times but for the sake of our demo it's
[13:01] good enough.
[13:03] And then when we forward between these
[13:05] there's a parameter here that's called
[13:06] has residuals. has residuals is going to
[13:09] tell us um if we're going to just run
[13:13] the output of our layers through RLU at
[13:17] the after every layer or if we're going
[13:19] to skip that and add the input to the
[13:24] outputs of the layer in the RLU. Right?
[13:27] So this is what residuals look like when
[13:29] we write code. We're just doing a simple
[13:31] addition of the input to the output.
[13:35] Great. So we just did that. So that's
[13:37] our deep neural network. Total number of
[13:39] parameters, 2 million parameters. You
[13:41] can see us inching up in parameters. We
[13:43] started off from 187 parameters, went up
[13:45] to half a million parameters. Now we're
[13:47] at 2 million parameters. The more
[13:50] examples advanced, the closer we're
[13:51] going to get to our final count of
[13:53] parameters of 124 million. But right
[13:55] now, we're just at 2 million parameters.
[13:57] And this is the structure of the layers.
[13:59] Right? We have layer 1 2 3 all the way
[14:01] down to 31 layers.
[14:04] Uh and actually we're going to run this
[14:06] on 20 layers. Uh great. So training uh
[14:10] we've seen the evaluate function.
[14:12] Nothing new here. Uh the training
[14:14] function now has a new parameter. How
[14:17] many layer depths do we want to have?
[14:19] And it are we going to use residuals?
[14:21] Yes. No. Obviously different training
[14:23] runs. Going to use different layer
[14:24] depths. Going to use different residuals
[14:28] uh settings. So we're going to
[14:29] initialize our model. We're going to
[14:31] call torch compile like we're used to.
[14:33] We're going to do now we know about
[14:34] heating initializations. We're going to
[14:37] create an optimizer a loss function hold
[14:40] some history. Uh we're going to set the
[14:44] we're going to activate the model. We're
[14:45] going to call the loss function. We're
[14:47] going to zero the gradient. Do a
[14:48] backward step, a forward step, so on and
[14:50] so forth. Great.
[14:54] So now we're going to have 32 layers.
[14:56] Actually we are going to run 32 layers.
[14:59] We're going to run 32 layers with no
[15:01] residuals. Let's see what that does.
[15:04] Right, you could see it's converging
[15:06] really, really slowly. Our maximum
[15:08] number of well, our maximum number of
[15:10] layers is going to be closer to
[15:13] uh I think we said 50 maximum epics
[15:16] here. So, it's going to just stop after
[15:18] 50 epics. It kind it's getting better.
[15:20] It started off at 33% 40% accuracy. It
[15:24] got to 55% AC or 57% accuracy after 50
[15:28] epics. Not a big improvement, but a
[15:30] noticeable improvement. Not super fast,
[15:32] but still noticeable. Now, let's kick in
[15:35] residuals. Has residuals true layer deck
[15:37] 32. Is it going to it's going to start
[15:40] off at a lower value. Really important
[15:42] to notice that it's g the initial
[15:44] accuracy is not as high, but it's
[15:46] actually making up for lost time really
[15:48] quickly and it's going to get to like
[15:50] 100% almost within uh it's so close. You
[15:55] can see it's only got like one or two
[15:56] mistakes really like within let's see
[15:59] which epic you get very close to 100%
[16:02] done. Let's say within epic 80, but then
[16:04] it takes like another couple of minutes
[16:06] and like another 100 epics to get to
[16:08] full run. So that took 193 epics.
[16:13] Wait. So let's visualize that. You can
[16:15] see with residuals test accuracy goes up
[16:18] up up up up really fast and it kind of
[16:21] plateaus at 100. Takes like a 100 turns
[16:23] more to finish that. And then uh test
[16:26] accuracy
[16:28] no residuals kind of play like it goes
[16:31] up and down. One thing that you'll
[16:33] notice it has these two big negative
[16:35] spikes. We'll talk more about them in a
[16:36] moment but worth noticing. And then loss
[16:39] again drops pretty fast with residuals,
[16:42] stays pretty constant, and as it kind of
[16:44] improves slowly slowly without
[16:46] residuals. Uh let's just smoke test
[16:49] these helpers because again I just want
[16:51] to remind us all we're in a multiplied
[16:53] by b modulus c 20 multiplied by 5
[16:58] modulus 1 is zero. Right? The modulus of
[17:01] one is always going to be zero. 92
[17:03] multiplied by 92 modulus 9 is going to
[17:07] be four, right? That's the domain we're
[17:09] working on. All of these are green
[17:11] because the model always gets the right
[17:13] answer in a deterministic domain like a
[17:16] multiplied by b modulo c. We can wait
[17:19] until we get to 100% accuracy which
[17:21] that's what 100% accuracy represent.
[17:24] Okay, so one last thing let's do a
[17:26] little bit of mechanistic interpability
[17:27] here together. Why did the model with
[17:31] residuals converge faster than the model
[17:34] without residuals? That's the question
[17:36] that we want to try and answer here.
[17:38] There's a lot of answers to that. The
[17:40] one that I like the most talks about the
[17:42] activation magnitudes.
[17:45] So, inside of this really deep network,
[17:47] what you could see is that each layer
[17:50] learn to only up the activation by a
[17:52] little bit as it's getting close between
[17:54] zero and one. This first line is one.
[17:57] The y-axis logarithmic. However, without
[18:00] residuals, in order for this network to
[18:02] function, you can see there's almost an
[18:04] complete explosion of inner activation
[18:06] values, the 10 to the^ of 8, right?
[18:08] Close to a billion or so numbers. Like
[18:11] that's the value of the floats. And then
[18:13] it has to bring it all the way down to
[18:15] even get close to resembling an answer
[18:17] at the end. Values totally exploded
[18:20] inside of this network even though it
[18:21] works. So really important to notice
[18:24] gradient explosion really did occur
[18:26] here.
[18:28] Exercise for you. Try and run this
[18:30] notebook. Do 72 layers no residual. Oh,
[18:33] I'm going to Okay, 72 layers without a
[18:36] residual. What does that do? 72 layers
[18:39] without a residual never even improves a
[18:41] tiny bit. We can run this for 200 epics.
[18:44] The test accuracy never improves.
[18:46] Training is totally bonked out. Nothing
[18:48] works. It can't learn anything. Why?
[18:51] because there's a gradient explosion
[18:52] inside of the network. And then you
[18:54] could try 16 layers of two feed forward
[18:57] networks or MLPS growing and shrinking
[18:59] an array. I also want you to try and
[19:01] build that DNN because it's going to be
[19:03] so close to the code that you're going
[19:05] to need for uh building a large language
[19:08] model. Great. So those are your two
[19:10] exercises. You have the answers here if
[19:12] you need them, but don't need them. Try
[19:14] and write this up yourself. Try and
[19:16] really code this up. These are two very
[19:18] straightforward exercises.
[19:21] So, why do residuals work, right? Why do
[19:24] they work? Lead 2918 demonstrated
[19:28] something that blew my mind.
[19:31] A loss landscape. This is a vision loss
[19:33] landscape because we we're still in
[19:34] prelimm times here. No residuals, really
[19:38] spiky landscape, really hard to
[19:40] navigate, lots of local minimums and
[19:42] maximums we can get trapped in. Not a
[19:45] fun time as we're trying to traverse
[19:46] this network with residuals. the network
[19:50] loss landscape smoothed out. A lot
[19:53] harder to get stuck at local minimums. A
[19:56] lot easier to fall into the global
[19:58] minimum. Global minimum has the best
[20:00] performance the network is going to
[20:02] have. Right? This is a vision model that
[20:04] also holds true for large language
[20:06] models. So I really want you to think
[20:07] about this. This is why we introduce
[20:09] loss landscape in section 7. This is why
[20:11] I was making you read about loss
[20:13] landscape. Well, it's never going to be
[20:14] useful. No, this is why residuals work.
[20:18] Residuals work because they smooth out
[20:21] the loss landscape and makes it easier
[20:23] for the network to converge. There's
[20:25] fewer local minimas and maximas. Backrop
[20:28] ends up being more accurate. We spend
[20:30] less GPU time. Residuals are really,
[20:32] really great. They're one of the small
[20:34] hidden tricks of building a deep neural
[20:36] network that is just absolutely vital
[20:37] for large language models.
[20:40] [sighs] How do we know that there's more
[20:42] local minimas and maximums? We can
[20:44] actually just look at our own training
[20:46] loss, right? We we trained a deep neural
[20:49] network without residuals. You could see
[20:51] these two spikes. We call these loss
[20:53] spikes. They're not good. Anytime you
[20:56] look at your loss curves and you see a
[20:58] loss spike, something went wrong. It's
[21:01] always worth investigating what went
[21:03] wrong there. You're going to find data
[21:05] that didn't make sense. You're going to
[21:07] find a network that didn't make sense.
[21:09] You're going to find something that went
[21:10] wrong that you could fix in your
[21:12] architecture. So, we go back to our
[21:14] metaphor. We are farmers. the tomatoes
[21:17] do the growing here. This is a great
[21:19] time for the farmer to get really
[21:21] involved in an infestation in a collapse
[21:24] in watering. I don't know what the
[21:26] metaphor is going to bring us to, but
[21:27] this is a great moment for the farmer to
[21:29] go in. We never want to see loss spikes.
[21:32] If there are loss spikes, it's almost
[21:34] always something that we can
[21:35] investigate.
[21:36] Uh so smoother lens I'm going to just
[21:39] read the the slides here. smoother
[21:42] landscape with residuals predict
[21:43] smoother loss curves which is exactly
[21:46] what we see when we run our small DNN.
[21:49] Uh the loss spikes in no residuals are
[21:52] the model leaving a local minimum and in
[21:55] the lost landscape. Why does loss go up
[21:57] when you leave a local minimum? Because
[21:58] you have to like traverse back up in the
[22:01] lost landscape. Better to just not have
[22:03] those local minimums if avoidable, which
[22:05] is what residuals do. Great. Another
[22:09] explanation that I also adore of why
[22:12] lost landscapes work and this is an this
[22:15] is a a thing that we knew since 2016 but
[22:18] really feels like we're proving a lot
[22:20] since 2024 2026 in mechanistic
[22:23] interpability became a real thing. So in
[22:26] 2016 Viet uh uh hypothesized that the
[22:30] residuals make these network into what
[22:33] we call ensembles. You don't have to
[22:35] know the word ensembles. What you have
[22:37] to know is the intuition of what they
[22:39] mean because we have residuals. What we
[22:42] in fact have, let's say we have 64
[22:45] layers with residuals every two items.
[22:47] We now have 32 residuals. What residuals
[22:50] do is they break up the big 64 layered
[22:53] network into 32 smaller uh networks that
[22:58] all collaborate with each other. They
[23:00] work together, right? That's that was
[23:03] their theory. they were able to somewhat
[23:05] prove it using math and experiments back
[23:07] in 2016. But if that's true, we'd expect
[23:10] in our large language models that we
[23:12] said have 72 layers, right? 326
[23:15] residuals,
[23:17] we'd expect that each of them would then
[23:20] have a slightly uh specialized role
[23:23] within the network. And boy, did we
[23:25] prove that in the last two years.
[23:27] There's so many papers on the topic of
[23:29] what each layer does. I actually really
[23:32] love this lingua map paper from 2016.
[23:35] They trained a model half on English,
[23:37] half on Chinese characters. So really
[23:40] multilingual large language model, very
[23:42] different than our normal large language
[23:44] models that are predominantly 70%
[23:45] English, 25% Chinese. So they went for
[23:48] 50/50, which I think was brilliant. And
[23:50] then what they found is that the earlier
[23:53] layers had a super different role than
[23:54] the middle layers had a super different
[23:56] role than the end layers uh than the
[23:59] late layers. So the early early uh
[24:02] layers in a large language model uh
[24:05] really dealt with the vagrancies of
[24:07] language. They dealt with like I want to
[24:09] combine these two halves of the word ch
[24:12] and to chair. They were combined uh
[24:15] understanding of chair for like is sofa
[24:18] a chair is a bench a chair. They really
[24:20] dealt with those kind of like fine
[24:22] linguistic issues and then they ended up
[24:24] at the platonic ideal representation of
[24:27] chair as it relates to a bunch of other
[24:29] concepts. The middle layers did a lot of
[24:31] thinking. They did a lot of reasoning
[24:34] and the late layers ended up being able
[24:37] to like form that into an output
[24:39] language again back to Chinese or
[24:41] English. Early layers built semantic
[24:44] representations of of words within a
[24:47] language. Middle layers had conceptual
[24:49] representation. Late middle layers did a
[24:52] lot of reasoning. Late late layers just
[24:55] did converted back to the final
[24:57] language. That proves that the 2016
[25:00] hypothesis that residuals break up the
[25:02] network into smaller networks that then
[25:03] collaborate is true. That is what we
[25:06] see. Residuals break up the network,
[25:08] especially in large language models. We
[25:10] now know that that's part of the story
[25:11] of how the tomato grows itself. It
[25:14] assigns responsibilities to layers based
[25:16] on their location. Very fun to find out.
[25:19] Why did we talk about all of that?
[25:21] Right? Because we had a lot of free time
[25:23] in residuals. It's not a lot of work.
[25:25] All we're doing is we're doing simple
[25:27] addition on two two dimensional arrays.
[25:30] I gave you the full gamut of why
[25:32] residuals work and what our hypotheses
[25:34] are around it. We also learned that
[25:35] there's new forms of residuals,
[25:37] specifically attention residuals and
[25:39] manifest manifest manifold constrained
[25:42] hyperconnections, which is just a way of
[25:44] saying attention residuals. Right? So
[25:46] now we know that all of that stuff
[25:47] exists. What it's so fun to nerd out
[25:49] with you. Okay, architecture decisions.
[25:52] We spent all this time talking about
[25:53] residuals. We should have some, right?
[25:55] That's our first decision. Our second
[25:57] decision is we're going to use editive
[25:59] connections. We're just going to use the
[26:01] plain old connections that we've been
[26:02] using since 2017, since 2015. If you if
[26:06] I had recorded this in 2025, I would
[26:09] have still said it's state-of-the-art.
[26:10] You're doing really well. Really, I'm
[26:12] pretty sure manifold hyperconnection,
[26:14] manifold constraint hyperconnections are
[26:16] going to be the wave of the future. And
[26:17] by the mid 2026, most open source models
[26:20] will be using them. Looking at their
[26:22] results, it's almost very clear that
[26:24] that's going to happen, unless there's a
[26:25] great reason not to that I can't see
[26:26] right now. Um, I did copy some source
[26:30] code from Torchtune. Torchtune is the
[26:32] meta library that has a bunch of like
[26:35] we're using PyTorch, so that adds a
[26:37] bunch of components that we could build
[26:39] on top of PyTorch. This is how they
[26:41] implemented something called a
[26:43] transformer. I don't know what a
[26:44] transformer is yet. Maybe I'll learn
[26:46] about it in section 18, but for now you
[26:49] can see this is how a production grade
[26:51] implementation of residuals look like.
[26:54] It is just addition. We also learned
[26:56] that we want why we want to use
[26:58] residuals cuz things converge faster.
[27:00] There's no gradient explosion. Great.
[27:03] That's it. We're done with residuals.
[27:05] Next up, we're going to talk about
[27:06] normalization. Why do we need to
[27:09] normalize? We're adding a bunch of
[27:10] numbers together and even like with
[27:13] residuals we're preventing collapse but
[27:17] we might be still getting close to
[27:19] gradient explosion with residuals
[27:21] especially the deeper the network goes.
[27:23] So we have to think about what
[27:24] normalization is and that's going to be
[27:26] the solution to that. Great. I hope to
[27:28] see you in this next section on
[27:30] residuals.
