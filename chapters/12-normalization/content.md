# Normalization | Build Your Own LLM Workshop #12

**Build Your Own LLM Workshop — Video #12 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 35m 2s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=ZqSbev8Y-ys |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to building
[00:02] your own large language model. I'm
[00:04] Justin Angel and in this section we're
[00:06] going to be talking about normalization.
[00:08] In the previous sections we talked about
[00:10] residuals and before that we talked
[00:12] about initialization.
[00:14] Normalization picks up from that thread
[00:16] because both of all of these things are
[00:19] meant to help us avoid uh great training
[00:23] collapse. So either through exploding
[00:25] gradients or vanishing gradients. So
[00:28] what's the problem that we're trying to
[00:29] solve here? We're still dealing with the
[00:31] fact that GPT2 style small models need
[00:34] to have 72 consecutive matrix
[00:36] multiplications and they still don't
[00:39] converge. Uh so residuals they do
[00:42] prevent vanishing gradients. That's
[00:44] great. It makes sense because we do x
[00:47] plus fx
[00:48] that's always going to be bigger than
[00:50] xish, right? There's always the
[00:52] possibility of fx being negative. X plus
[00:54] FX tends to be bigger than X in
[00:56] magnitude. Uh but they don't so but they
[01:00] don't prevent gradient uh collapse or
[01:03] vanishing gradient uh because X of X is
[01:06] bigger than X, right? Uh he
[01:08] initialization assumes that our MLP is
[01:12] like MLP ru. But that's not true for us
[01:14] in transformer land because we said
[01:16] we're going to do growing shrinking ru
[01:19] and then we're going to do another set
[01:20] of growing shrinking ru. So because our
[01:23] MLP rail in the middle MLP we're that's
[01:26] going to be a problem for us. We don't
[01:28] have the ability to just use he
[01:29] initialization glorado initialization
[01:31] whatever initialization to solve our
[01:34] GPT2 style architecture from
[01:36] experiencing training collapse. So the
[01:39] solution we we want to normalize. What
[01:41] does normalization mean here? That
[01:43] within the residual stream we maintain a
[01:47] single like coherent set of statistics.
[01:49] We don't want it to explode. We don't
[01:51] want it to collapse. We don't want the
[01:53] the things to shift. So, let's look at
[01:57] the chart on the left. The chart of the
[01:59] left, specifically the yellow line.
[02:00] Sorry, there's a bunch of other lines
[02:02] there, but the yellow line shows us what
[02:04] happens when we try and train A
[02:06] multiplied by B modulus C with 72
[02:09] layers. We can see that basically in 200
[02:11] epics, the training accuracy barely
[02:14] changes. It gets from like 23% to 30%.
[02:18] Really, really slow. One could even say
[02:20] it's really not even getting close to
[02:22] converging. So as a result of that and
[02:25] that's even with residuals, that's even
[02:27] with key initialization. So a result of
[02:29] that we need another tool in our tool
[02:31] belt. That tool is going to be
[02:32] normalization.
[02:34] What is normalization?
[02:36] Normalization. And I really love this
[02:38] GIF that I think we should all watch
[02:40] together. Shows you this shows you
[02:43] scaling, right? scaling is like let's
[02:45] say now I have a bunch of points and the
[02:48] previously my maximum point or like my
[02:52] general average of points was that
[02:54] yellow ring. So after I do another
[02:56] operation I'm going to rescale all of
[02:59] the points the points that are closer to
[03:01] the center of the graph are going to
[03:03] move further towards the yellow ring.
[03:05] The points outside the yellow ring are
[03:08] going to move closer to the yellow ring
[03:10] from the outside in. So that's what
[03:13] scaling does. Similarly, another form of
[03:16] normalization is centering. Let's say
[03:18] that the average of all of our points
[03:20] used to be zero, right? The 0 0 point.
[03:24] We can move the centering closer to that
[03:28] point.
[03:31] Um,
[03:39] great. So we were talking about
[03:40] normalization. So let's look at this GIF
[03:43] here together.
[03:45] This GIF shows us the concept of
[03:47] scaling. I really really love this GIF.
[03:49] In this GIF, you could see, hey, before
[03:51] we did an operation, we had this yellow
[03:54] ring that represents maybe like this the
[03:56] the bounds of data. But after we did an
[04:00] operation, a bunch of the points went
[04:01] outside the bounds. A bunch of points
[04:03] went went inside the bounds. What
[04:05] scaling does is it pulls the points that
[04:07] are inside the bounds closer to the
[04:08] bounds. It takes the points outside the
[04:11] bounds and pulls them closer to the
[04:12] bounds. Right? So that's scaling. Taking
[04:15] the points from the center closer to the
[04:17] bounds and taking points outside the
[04:19] bounds closer to the to the bounds.
[04:22] Another thing we could do in
[04:23] normalization is centering. What does
[04:26] centering mean here? You can't see it in
[04:28] the GIF, but centering would mean let's
[04:30] say that I had an average of zero. Let's
[04:32] say all my points were focused on the 00
[04:34] 0 point and for some reason the average
[04:36] shifted. Centering means we're going to
[04:39] take all of the points back. So the
[04:42] average is 0 0 0. Great. We can do both
[04:46] of those operations in the same uh
[04:49] normalization operation or just do
[04:51] scaling. Let's look at what kinds of
[04:53] scalings we have and then we can talk
[04:55] more about what each of them does.
[04:58] So here's a couple of formulas. the
[05:00] formulas. Let's start off with like
[05:01] naming some names. We have layerm super
[05:05] common. Larorm's sibling batch norm at
[05:09] all in large language models kind of
[05:11] common in machine learning models. Uh
[05:14] and we have RMS norm that is uh let's
[05:17] call it the newer more accepted version
[05:20] of layerm. RMS norm generally supplanted
[05:24] layer. L norm was really common in early
[05:26] large language models and RMS norm uh
[05:28] supplanted it. Why is that? So when we
[05:31] look at the formulas kind of hard to
[05:33] decipher maybe like we'll go over them
[05:35] in a moment but we could see that lonorm
[05:38] does one thing that rms norm doesn't do.
[05:41] It needs to calculate the variance. So
[05:45] variance calculations very expensive.
[05:47] You think about it like what is even
[05:49] variance? It's a statistic over the
[05:51] entirety of the arrays. So as a result
[05:54] of that, not having to calculate the
[05:56] variance is actually really useful if
[05:58] you're like a GPU compute constraint and
[06:01] you're not really losing anything by not
[06:02] calculating the variance. So let's talk
[06:05] about what each of them does. Leonorm
[06:07] and batchnorm both scale and center.
[06:10] Remember scaling means we're pulling
[06:12] things towards the bound either from the
[06:13] inside or from the outside in. And then
[06:16] centering means we're going to shift the
[06:18] average so it's back to for example
[06:19] being zero. We don't like the averaging
[06:21] changes. RMS norm doesn't center doesn't
[06:25] doesn't care about uh if you're average
[06:27] shifted. It does do scaling. It does
[06:31] want to keep everything within a bound.
[06:33] Why does scaling why is scaling the
[06:35] thing that both a layer norm and RMS
[06:37] norm do? Well, because we're trying to
[06:39] prevent gradient explosion and gradient
[06:42] collapse. So, making sure that every
[06:44] single round is consistent within the
[06:46] statistical bounds. That's actually
[06:48] super useful for us to do that. That is
[06:50] almost the classic definition of that.
[06:53] So what does lairorm do? Larorm and rms
[06:57] norm both operate on rows. So we think
[06:59] of matrixes they'll operate on rowms.
[07:01] Batchnorm operates on columns. Uh that's
[07:04] why batchorm isn't used in large
[07:05] language models. When we hear more about
[07:08] what's an embedding metrics and so on,
[07:10] it would make more sense why we wouldn't
[07:12] want to average out columns. That
[07:13] doesn't make any sense in the context of
[07:15] large language models. But in the
[07:17] context of what we're working with right
[07:18] now, deep neural networks just know what
[07:20] batch norm is. Additionally, batch norm
[07:23] and lonorm for center and then scale.
[07:26] RMS norm just scales like we just said.
[07:28] And then both when we're doing this math
[07:31] formula, we'll add a tiny value to the
[07:33] denominator to avoid division by zero.
[07:35] Right? So we're going to always add a
[07:37] tiny value to the denominator. We're
[07:40] going to call it epsilon. So now that
[07:42] we've said all of that, maybe we can
[07:44] look at the formula. Let's start with
[07:45] RMS norm because it's a bit simpler. We
[07:47] take an input, we divide it by the mean
[07:49] of the the square of all of the inputs
[07:54] and then uh add a small epsilon to that
[07:57] square root that and then we multiply by
[08:00] a fixed value. The fixed value is also a
[08:03] learned value by the way. It's becomes
[08:04] one of the parameters of the network.
[08:07] Great. So now we saw RMS norm. Not super
[08:10] clear to me why we would do this. Okay,
[08:12] let's actually think about it. That's
[08:14] scaling. While we're seeing the division
[08:16] by the mean, that's a form of scaling,
[08:18] right?
[08:20] Additionally, we can look at layerorm.
[08:22] It kind of complicates things a bit
[08:23] more. It takes an input, minuses the
[08:26] average from it. That's the thing that
[08:28] does centering and then it divides by
[08:30] the variance plus an epsilon, then
[08:32] square root, so on. What what does that
[08:34] do? That's our uh our scaling operation.
[08:38] Great. And then we have batch norm.
[08:40] Don't have to memorize these formulas.
[08:42] We're going to see them in Excel. We're
[08:43] going to build intuition for them. So
[08:45] let's do that right now. We're going to
[08:47] look at layer norm, batch norm, RMS
[08:49] norm. We're going to create some short
[08:50] versions for them for us to be able to
[08:52] do them. And then we're going to say
[08:53] them in the context of MLPS. And
[08:55] finally, we'll look at prenor and
[08:56] postnorm which is how we implement these
[08:58] in in practice.
[09:01] Great. So now uh we're in this Google
[09:04] sheet. I'm going to make a copy like we
[09:06] do. We're going to work in the without
[09:08] answers sheet. And the first thing we're
[09:11] going to look at is how lair norm is
[09:13] implemented. So let's go to without
[09:15] answers. We see the formula here. The
[09:18] first thing I can tell is I need to
[09:20] calculate the mean and the variance.
[09:22] Great. So the calculate mean we're going
[09:24] to again we said we're going to run that
[09:25] column. We're going to run that row by
[09:27] row. So let's run the mean of this row.
[09:31] And one moment I'm going to delete this.
[09:33] Great. So let's calculate the mean of
[09:35] this row. We also know that we have to
[09:38] calculate the uh sorry in order to
[09:40] calculate mean in Google Sheets we say
[09:42] average. Great. And then we have to
[09:45] calculate the variance. In order to
[09:46] calculate variance we calculate it this
[09:48] way. Variance just refers to the
[09:51] variance within the sample. Great. So we
[09:54] have that. We're going to calculate
[09:59] the mean. Now we have the mean and the
[10:01] variance for each row. We said lonorm
[10:03] works on a per row basis. Now we're
[10:06] going to center these. How do we center?
[10:08] We're going to fill out that formula we
[10:11] had here. So we have to like minus the
[10:13] mean and so on. I'm just going to copy
[10:15] this from the width answer section. So
[10:19] and that's just implementing the formula
[10:20] that we saw earlier. So what are we
[10:23] doing here? We're taking the input
[10:26] value. We're minusing the mean from it
[10:29] which we have in the side. We do a
[10:31] division by the square root of the
[10:34] variance and then we add the small
[10:37] epsilon value to it and small epsilon
[10:39] value is right here. Great. So we did
[10:42] that
[10:46] and you can see this is what it looks
[10:47] like postnormalization
[10:50] uh uh post centering but then we can
[10:54] also do a little bit more scaling. So we
[10:56] did a little bit of scaling and a little
[10:58] bit of centering where we can add uh
[11:01] scaling based on these multipliers and
[11:03] addition. So you see we have lambda and
[11:04] beta here. So we can take these multiply
[11:07] and addition and then pair cell we can
[11:10] multiply and then do an addition as
[11:13] well. And again these are learned
[11:15] values. So the network kind of learns
[11:16] how to use them in a way that makes
[11:18] sense. And I had to lock in these
[11:20] values.
[11:26] Why does this not of course J 27 ah 27
[11:32] here we go
[11:35] multiply by J28 2 J27 let's write this
[11:38] down again layer normal multiplied by
[11:41] the multiplier here we go
[11:46] we lock this one plus this one
[11:50] here we go and Now
[11:54] this is what Larorm does to a bunch of
[11:57] numbers. So you could see everything is
[11:58] now centered and scaled. Great. Now in
[12:02] batch norm we could do something
[12:03] similar. Batch norm said works on
[12:05] columns not rows. Not super useful in
[12:07] the context of large language models.
[12:08] Useful in the context of knowing it. So
[12:11] we already have the mean and variance
[12:12] calculator per column. So let's try and
[12:15] implement the formula for batch norm.
[12:17] This time I'm going to do it full on.
[12:19] Here's the input minus the mean of that
[12:23] row divided by the square root of the
[12:28] variance
[12:29] plus a small epsilon to make sure that
[12:32] we don't end up with negative values. So
[12:34] the epsilon we're going to lock in
[12:36] place. The variance we're going to lock
[12:39] in um a row. The
[12:44] mean we're going to lock in a row. And
[12:47] that's it. Great. So, let's hope that I
[12:49] did that right. Now, I'm going to run
[12:51] that over all of these columns and all
[12:53] of these rows. And then now that did
[12:56] most of the scaling in the centering.
[12:59] Did that work?
[13:03] Did I do that right? Let's try and just
[13:05] copy the batch norm from here. Feel like
[13:07] that wasn't accurate. Great. So, I'm
[13:10] going to Oh, because I didn't do
[13:12] parentheses.
[13:14] That makes sense. See, you don't really
[13:16] want to see me fuss around with
[13:17] parentheses.
[13:19] Okay, great. Here we go.
[13:23] Um, is this for batch norm? Yeah. So,
[13:27] I'm just going to copy these across.
[13:32] Perfect. These numbers look much better
[13:34] to me. Forgot about precedence and
[13:36] parenthesis.
[13:38] And then we're going to do scaling with
[13:40] beta and lambda like we saw before, a
[13:42] multiplier and an addition. And this is
[13:43] what the numbers kind of look like
[13:45] afterward. And you could see that the
[13:46] numbers seem like they're better
[13:48] distributed. Great. So b we did batch
[13:51] norm. Let's do RMS norm. RMS norm. We're
[13:54] going to take x divided by the square
[13:57] root of the mean squared and add a small
[14:01] epsilon. Instead of you watching me type
[14:04] this out, I'm just going to write equals
[14:06] here. And that didn't work. So you're
[14:08] going to see me type that out. So I've
[14:10] got x / the square root of the power 2
[14:18] of the
[14:21] x². So we're going to take x^2
[14:33] and then we're going to add a small
[14:35] epsilon to that. Let's see if I
[14:37] implemented that correctly. I'm going to
[14:40] look at the how I filled it out here.
[14:45] And actually, it wanted us to just do
[14:47] the mean of sum of squares.
[14:50] So, we had the mean of sum of squares.
[14:51] So, let's do that here.
[14:55] Great. So, that gave us the mean of sum
[14:58] of squares. That's the mean x^2 for all
[15:01] of the x's in uh in this row. So, now
[15:05] it's going to be a lot easier to
[15:06] implement it. I'm going to actually just
[15:08] copy this over.
[15:11] Great.
[15:15] Awesome. So now we have these hardcoded
[15:19] values. We still need to apply a small
[15:21] scaling. So we're going to do this
[15:23] multiplied by a small scaling.
[15:30] We have to lock the scaling function.
[15:43] Perfect.
[15:46] Here we go. And that's RMS norm. So we
[15:51] uh mean sum of squares. There's a
[15:52] function for that that we could just
[15:54] use. Sum of squares and for this whole
[15:57] row.
[15:58] And then we did the division like we
[16:01] were supposed to. And then we did
[16:02] scaling. And you can kind of see these
[16:04] values are all kind of hovering close to
[16:06] zero which is what we want. We want them
[16:08] close within the 0ero to one minus sorry
[16:12] within the -11 range within the -44
[16:15] range. So RMS norm really like brought
[16:17] these numbers and pulled them in
[16:19] compared to what they looked like
[16:21] earlier on. Great. So that's RMS norm.
[16:24] We did a lot of math for that. There's
[16:26] also shorter versions that don't have us
[16:28] like create the sum of squares in the
[16:30] side here and the mean and variance in
[16:33] the of columns and so on in the side. So
[16:36] we could just write a very long formula.
[16:38] You're not going to ever write these
[16:40] formulas yourself. They're kind of long.
[16:41] They're kind of specific. But I do want
[16:43] you to see that for this input there's a
[16:45] bunch of uh single line formulas, single
[16:48] cell formulas we could write for RMS
[16:51] norm, batch norm, and layer norm. Okay,
[16:53] awesome. So now I know that these these
[16:56] single cell solutions or single cell
[16:59] solutions.
[17:01] So let's look at MLPS growing and
[17:03] shrinking. So we said our MLPS grow and
[17:06] shrink. They have relu they have
[17:07] residuals. We're trying to build this
[17:08] one MLP for several sections. Now that's
[17:12] what's used inside of transformers for
[17:13] large language models. So we have inputs
[17:16] a 5x5. We have the M1 growing uh
[17:20] hard-coded uh sorry not hardcoded the
[17:23] learnable weights. So we have input M1
[17:26] here. We run it through a RAU function.
[17:30] We then have a shrinking uh M2 here. We
[17:34] multiply that and get the activations.
[17:36] And finally we have a residual that we
[17:38] add all the way from the beginning of
[17:40] all of that. Right? So note the
[17:43] gradients the note that gradients
[17:45] explode numbers are more red or more
[17:47] greens per residual. Right? So if you
[17:49] look all the way up here the numbers are
[17:51] like a light red and light gray and
[17:53] light green and light red. But if you
[17:55] look here they tend to be more green
[17:57] more red. Let's see a couple more
[17:58] examples of that. More green, more red,
[18:01] more green, more red. Right? So we're
[18:03] thinking about like we did do something
[18:06] here but it's not perfect, right? Like
[18:09] what do we need? we need to somehow
[18:12] apply normalization. The thing we're
[18:14] trying to prevent are these more red
[18:16] more green numbers after we run them
[18:18] through a growing shrinking RU MLP.
[18:22] So if you look at it here, we can do a
[18:24] little bit of more of a condensed form.
[18:25] I know that like these lines look great,
[18:27] but they're kind of like a mess to copy
[18:29] and like they don't make it easy to
[18:30] think about it. So same example here,
[18:33] just super short form. You can see I'm
[18:35] still doing the same set of memotes. I
[18:37] just have them like very condensed.
[18:40] Great.
[18:41] So when do we apply RMS norm? One option
[18:44] is we can apply that as pre as a
[18:48] postnorm. We can still do input multiply
[18:51] by M1 then multiply that by M2 and then
[18:54] put that and then add the input back in
[18:56] with the residual and then I could apply
[18:58] the single line RMS form here.
[19:02] So oh did we change the numbers? I'm
[19:05] sure we just changed the numbers. My
[19:08] mold C1212 let C1212
[19:12] so on that's not C12 that's going to be
[19:16] 193
[19:18] to
[19:22] E 195 here we go so I can apply my RMS
[19:27] norms again this is all single line so I
[19:30] can do that after I do all the MLP
[19:34] that's one option another option is I
[19:37] could do what's called porm porm and
[19:40] again I'm going to have to change the
[19:41] line numbers here would mean that we're
[19:43] going to RMS norm before we do all of
[19:45] our multiplications and so on so I'm
[19:49] going to change the line numbers here
[19:50] and actually they seem correct perfect
[19:52] and these work perfect so my options are
[19:56] to do a p-orm multiply it uh apply RMS
[20:00] norm before I do all my metrics
[20:02] multiplications growing shrinking relu
[20:04] and another option is to do after.
[20:08] Right. So, RMS prenorm versus postnorm.
[20:10] When do we use which? We're going to
[20:12] find out when we go back to the slide
[20:14] deck. Great. So, let's talk about
[20:16] everything we covered. We covered layer,
[20:18] batch norm, RMS norms. We saw that the
[20:20] short versions we could use cuz we ended
[20:21] up using them later on. We saw growing
[20:23] shrinking MLP that has a problem because
[20:26] it's getting more green or more red,
[20:27] which means the magnitude is increasing
[20:29] us. We're going to have vanishing or
[20:30] exploding gradients. Then, we saw the
[20:33] MLP short version. And finally we try to
[20:36] figure out when do we apply RMS norm.
[20:38] When did do we apply this porm or
[20:40] postnorm?
[20:42] Okay. So now we have the question of
[20:44] porm versus postnorm. So let's look at
[20:46] this uh illustration here from Jeang
[20:49] 2020. Uh we have layerm before we go
[20:52] into something called attention. I don't
[20:54] know what that is. And the residual. And
[20:56] then we have layer norm before we go
[20:57] into a feed forward network. That's our
[20:59] MLP. Or we could do that after. That's
[21:04] uh here in the layer norm. So after we
[21:06] do the addition residuals, which one do
[21:08] you think we started off with? Well, we
[21:10] started off with postnorm in 2017.
[21:14] That's the all you need is uh all you
[21:16] need is attention paper.
[21:19] And uh
[21:22] uh and what Shan did in 2020 is that
[21:25] they showed that it actually leads to
[21:26] unstable training. So we don't do
[21:29] postnorm anymore. Shortly after that
[21:31] paper people stopped doing postnorm all
[21:33] porm actually normalizes within the
[21:36] block creates stable gradients. That's
[21:39] awesome. Basically every modern LLM uses
[21:41] prenor. Norm uses postnorm. So when we
[21:44] think when do we want to apply rms norm
[21:47] when do we want to apply our lair norm?
[21:48] We want to apply it as a prenorm not a
[21:50] postnorm. Intuitively, that kind of
[21:53] makes sense, right? Because when we uh
[21:56] normalized residuals, if we did an
[21:59] addition and then normalized it right
[22:02] away, we just lost a portion of the
[22:04] residual. That doesn't make a lot of
[22:06] sense, right? We want to do that before
[22:09] we start our work in our small MLP. That
[22:13] makes more sense to me. Great. So, let's
[22:16] look at a little bit of code. And before
[22:17] we do, let's look at the table on the
[22:20] right. the table on the right, Gemini
[22:21] was so kind to generate it for me. These
[22:24] are the various normalizations that are
[22:26] available within PyTorch. So there's
[22:28] batch norm and lazy batch norm and more
[22:31] batch norms, there's instance norms,
[22:34] there's layer norm, there's RMS norm,
[22:35] there's group norm. Couple more of
[22:37] these, right? The important thing for us
[22:40] is we know about layer norm, we know
[22:42] about RMS norm, we know about batch
[22:43] norm. We're only going to use layer norm
[22:45] and RMS norm. Uh, and then for us, we
[22:49] just apply them later on into what's
[22:51] called the norms array. Great. Into its
[22:54] own module list. So, let's look at some
[22:56] code.
[23:02] Here we go. So, again, if you're running
[23:04] this yourself, you would connect to a
[23:05] GPU. You would run all
[23:08] this is just the setup cell. We're going
[23:11] to set up a data set like we're used to.
[23:13] 150,000 test train examples. 140,000
[23:16] test examples. We're in a * b modulus c
[23:20] where a and b is between 0 and 99 and c
[23:22] is between 0 and 19. We're going to uh
[23:26] sorry, I'm going to go keep going here.
[23:28] We have our deep neural network. In our
[23:30] deep neural network, we uh accept one
[23:33] parameter that says is this a postnorm
[23:35] or is this a pre-orm? Right? We want to
[23:37] test out which one works best.
[23:40] Uh and then we start building layers. So
[23:42] we have 219 input scales down to 128.
[23:46] And then we're going to start running
[23:47] these between uh 16 additional layers
[23:51] that are just at the same growing
[23:54] between hidden dimension and 2x running
[23:56] a relu then shrinking back down to
[23:58] hidden dimension. Normally there's not a
[23:59] lot of reason to do this. But this looks
[24:01] kind of similar to what you will see in
[24:03] an MLP. An MLP for transformers just has
[24:07] a 4x growing shrinking rate. Great. And
[24:10] then we have norms which is just a
[24:12] module list. And then we're going to
[24:14] append whatever normalization type uh is
[24:16] being sent into this deep neural
[24:19] network. So that could be a batch norm,
[24:21] that could be a layer norm, that could
[24:22] be a um an RMS norm. And then when we
[24:26] run our forward pass based on whether or
[24:28] not we're in postnorm or p-orm, if we're
[24:31] in porm, we're just going to like
[24:32] normalize x before it goes to the layer
[24:35] and before the residual. or in postnorm
[24:38] we're going to normalize after it goes
[24:40] to uh the residual and into the layer.
[24:44] Great. So pre-nome postnorm we just saw
[24:46] implementation we saw how to like hold
[24:49] norms in and we also know how to run
[24:51] things to the layers.
[24:54] Finally we're going to look at how many
[24:56] parameters we have in this model. We're
[24:58] at a 1 million parameter model. Great.
[25:02] Then we have our training loop. Our
[25:03] training loop doesn't do anything that
[25:04] the previous training loop for residuals
[25:06] didn't do. What it will do is we will
[25:09] set up the norm tag here and whether or
[25:11] not is is postnormalization or
[25:13] pre-normalization
[25:15] and then it's going to just keep
[25:16] executing the way we've always seen it
[25:18] execute. Great. So now let's create a
[25:21] baseline for us. Let's say we don't do
[25:22] any normalization. That should be pretty
[25:24] similar to the previous uh section. So
[25:28] we could see how long does that take to
[25:30] converge. That takes right. We're going
[25:32] to give it 200 epics. Uh it didn't
[25:35] converge fully at 200 layers, but you
[25:37] can see it's getting very close at 100%
[25:39] accuracy. 100% is like a rounding error,
[25:42] but getting very very close to 100%. And
[25:44] actually, it got into a pretty good
[25:46] state. Let's say 99% was achieved at 56
[25:50] epics. And then for 150 epics, it just
[25:53] couldn't fully converge without uh
[25:55] normalization. So that's something we
[25:57] just learned. Remember we have 16 layers
[25:59] of growing, shrinking, growing,
[26:00] shrinking, growing, shrinking. So total
[26:02] of 32 layers 34 if you add the input and
[26:05] the output.
[26:07] Great. So let's do porm RMS norm. We
[26:10] know porm one like that's based on the
[26:13] shong 2020 paper and then we know RMS
[26:16] norm is much more popular. So let's just
[26:18] do RMS norm. And then by setting uh by
[26:21] not setting a parameter it's going to be
[26:23] porm right now. Let's see how fast that
[26:25] converges in a solution. So it gets to
[26:27] the 99% range within 38 epics. That's
[26:31] about 20 epics faster than we did in our
[26:34] baseline. And then it fully converges by
[26:37] the time we get to
[26:39] 95 epics. So it fully converges at 95
[26:42] gets pretty close to complete solution
[26:45] by 40 epics. Not bad. Postnorm on the
[26:49] other hand, we're going to run postnorm.
[26:51] Is postnorm true?
[26:54] is postnorm true and RMS norm and like
[26:58] how long is that going to take to
[27:00] converge? Oh my goodness, right? It's
[27:03] not going to converge. It's gonna why?
[27:05] Let's look at the the accuracy. It's
[27:09] basically stuck at 33%, it's never able
[27:12] to like actually make any useful like
[27:15] the accuracy was actually better in the
[27:16] beginning and then training clearly
[27:18] collapses, right? The numbers are all
[27:20] jibber jabber. There's not this network
[27:22] doesn't do anything useful.
[27:24] Um so that's useful to know. If you take
[27:28] RMS norm from prenorm to por norm
[27:31] training just fully collapses for this
[27:33] network fully collapses pre. Okay. Can
[27:36] we do a prenor with the layerorm? Sure
[27:39] we can. Here we go. It gets to 99
[27:43] percentile within let's say that's 35 34
[27:48] uh steps. And then does it fully
[27:50] converge? Yeah, it fully converges
[27:52] within 87 epox. Great. So for this very
[27:55] simple domain, lenorm actually does
[27:57] pretty okay. Uh postnorm though for for
[28:01] lenorm
[28:02] doesn't converge at all. Training has
[28:04] fully collapsed. So postnorm again not
[28:06] stable at all. We have a batch norm. We
[28:10] can keep going with this batch norm 1d
[28:13] postnorm. Okay. So on let's look at the
[28:15] results in a graph. So let's try and
[28:17] look at all of these in graphs. So why I
[28:20] have this one massive graph with both
[28:22] pre-norm and postnorm. We're going to
[28:23] separate them out in a sec. But we can
[28:25] kind of see that the best performance
[28:27] comes from RMS norm porm from prenor RMS
[28:32] norm from porm batchnorm porm layer
[28:36] norm. Okay cool. So that's useful. You
[28:38] can see a bunch of trainings have also
[28:40] collapsed. This yellow one postnorm
[28:42] collapsed. This purple one postnormal
[28:44] layer normal totally collapsed.
[28:48] Only a few of these did really really
[28:49] well. So let's look at that at a chart.
[28:52] Only prenor layer and prenor RMS norm
[28:55] really fully converged.
[28:58] Why would we then still prefer RMS norm
[29:00] over lenorm even though lenorm might
[29:02] have converted a bit faster in this
[29:03] example? And by the way that's not given
[29:05] that's not necessarily true that lenorm
[29:08] does converge faster is because it needs
[29:09] less operations. Lenorm has more
[29:12] operations than RMS norm. Maybe it'll be
[29:14] a tiny bit more accurate, but because of
[29:16] that, it takes longer to get to these
[29:17] epics. So just counting epics isn't
[29:19] equivalent because Lonorm is getting
[29:21] like free operations that it gets to do
[29:23] within those epics. Okay, so let's uh
[29:26] let's try and visualize the activation
[29:28] values. Let's try and figure out why
[29:30] this is happening. Really really
[29:32] confusing graph. Really sorry about
[29:34] that. The most important thing to notice
[29:36] this is a logarithmic graph. the
[29:40] pre-orms like the yellow line and this
[29:43] red line porm for layer norm and preorm
[29:45] for RMS norm are kind of staying within
[29:48] like zero in one range for their
[29:50] activations for the whole run other
[29:53] systems the postnorms the activations go
[29:55] above one and then maybe have to go down
[29:57] maybe they go up and down up and down up
[29:59] and down if it's not normalized not
[30:01] great we could see the normalization
[30:03] actually work it keep kept its
[30:05] activation values within the range of
[30:08] zero and one. That's what we want to see
[30:10] from normalization. That's how we
[30:11] normalization works. It keeps the values
[30:13] within 0 and one. Everything is working
[30:15] according to expectations. Great. Let's
[30:18] go back to our uh slide deck here. I do
[30:22] have an exercise for you. If you don't
[30:24] mind, take this entire previous sheet
[30:26] and instead of doing 16 growing
[30:29] shrinking layers, do 72 layers of those
[30:32] things. Right? What are you going to
[30:34] find out when you do that? you have like
[30:36] just duplicate the whole collab
[30:38] notebook. Oh, looks like I didn't do
[30:40] this correctly. I need to change this
[30:42] from a space. Here we go.
[30:46] What do we learn from that? When we try
[30:47] and run that and look at the the sheets
[30:49] at the end, right? The activation val
[30:52] activation values the outcomes
[30:55] of activation values paranorm. Let's
[30:57] look at this one more time. A lot of the
[31:00] training collapses. So when you look at
[31:02] pre-orm and postnorm, it's 72 layers.
[31:05] the whole thing just collapses. None of
[31:07] them really converge. Either Tesla
[31:10] doesn't really shift or like you can't
[31:12] accuracy doesn't really move. Whereas
[31:14] the pre-orms all converge. That's a
[31:17] really important lesson. We could go all
[31:19] the way up to 72 layers. That's where we
[31:22] need to be for GP22 style transformers.
[31:25] And then we could get there by having
[31:27] pre-norm. We can't get there by having
[31:29] postnorm. That's why we don't use
[31:31] postnorm. Postnorm totally collapses
[31:33] training. Great. So postnorm versus
[31:36] porm, what did we learn? All pre-orm
[31:39] options converge in 72 layers. Postnorm
[31:42] training straight up collaps in 72
[31:44] layers. Uh nororm kind of oscillates
[31:47] wildly. So the training is actually kind
[31:49] of unstable. Norm is that like yellow
[31:51] line that keeps going up and down.
[31:53] Prenorm is the clear winner with RMS
[31:55] norm coming out a tiny bit ahead for 72
[31:58] layers. Didn't come out ahead at 16
[32:00] layers. came out ahead at 72 layers.
[32:04] So why did the training collapse? Right?
[32:06] We go back to the 72 layer example.
[32:08] There's a couple more charts here, but
[32:09] let's look at them here. Postnorm
[32:12] stopped deep neural networks from
[32:13] learning anything in the first 60
[32:15] layers. Right? So if you look at
[32:17] postnorm, it really doesn't learn
[32:20] anything in the first 60 layers. Right?
[32:22] It's stable, stable, stable, stable,
[32:24] stable, stable, stable, stable. And then
[32:25] the last few layers are trying to do
[32:27] something, right? Really what posorm did
[32:30] is it stopped the first set of layers
[32:32] from learning anything. The first the
[32:33] majority of layers didn't really learn
[32:35] anything. They just got normalized over
[32:36] and over again. Whereas the last few
[32:39] layers really had to kick in and do a
[32:40] little bit of work. Why did porm batch
[32:44] norm had exploding gradients? We could
[32:46] see that here from this red line. That's
[32:48] why we would don't often use batch norm
[32:50] even in just plain deep neural network.
[32:53] Porm maintain the direction but not the
[32:56] magnitude of change. So if you look at
[32:58] the U
[33:01] lines here, they go a little bit down.
[33:02] They go into the negative. They below
[33:05] zero. It's totally fine. It's still 0 to
[33:07] one for us for magnitude wise. But
[33:10] however, postnorm took on magnitude but
[33:13] not direction which collapsed training,
[33:15] right? Postnorm had not like increased
[33:19] its size over time but it maintained the
[33:22] magnitude but not the direction.
[33:24] Remember we talked about this. we have
[33:26] direction and magnitude to think about
[33:28] in terms of where we're trying to
[33:29] converge. Okay, so a little bit of
[33:31] decisions. We're going to use RMS norm
[33:34] even though it didn't exist when we were
[33:36] building GPT2. Why? It's just much
[33:38] better. There's no reason to use lairm
[33:40] anymore. The 10 2025 survey shows us
[33:44] here on the bottom right
[33:46] that we uh that most modern LLMs use RMS
[33:51] norm and a little bit use layer norm.
[33:53] when you go look at 2024 2025 almost
[33:56] everyone totally switched over to RMS
[33:58] norm. So we're going to follow uh that
[34:00] cue and we're going to use RMS norm. Uh
[34:03] porm GPT2 has 70 consecutive metrics
[34:06] multiplication and it must use porm
[34:09] otherwise it like it was going to be
[34:11] really hard for us to converge. It is
[34:12] possible to converge with postnorm right
[34:14] like we saw that in the attention papers
[34:16] that it's possible but GPT2 style would
[34:19] really need postnorm at this uh pre-norm
[34:21] at this point and not postnorm great so
[34:24] now we did all of that
[34:27] uh we did all normalization we talked
[34:29] about layer norm we talked about batch
[34:31] norm we talked about RMS norm talked
[34:33] about postnorm versus porm and we chose
[34:35] which one we're going to use lastly we
[34:38] we're going to have to look at
[34:39] regularization why even though things
[34:41] convert
[34:42] They're still a bit wonky. We really
[34:44] want to be able to solve for activation
[34:47] values within the deep neural network
[34:49] before we move on to transformers. We're
[34:52] still missing a couple of key tools and
[34:54] those key tools are going to be covered
[34:55] here under regularization uh in section
[34:58] 13. And I hope you join me for that one.
