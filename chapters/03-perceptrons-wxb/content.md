# Perceptrons: wx+b | Build Your Own LLM Workshop #3

**Build Your Own LLM Workshop — Video #3 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 15m 54s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=uaA8ChGcMwE |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to a build
[00:02] your own large language model workshop.
[00:04] I'm Justin Angel. We have just finished
[00:07] reverse engineering a GPT2 style model
[00:10] and then we know our road map for the
[00:11] day as a result of that cuz we're just
[00:13] going to rebuild that. But for now we
[00:16] have to go into the most basic unit of
[00:18] all neural networks which is a
[00:19] perceptron.
[00:22] So our deliverable from today is going
[00:24] to be a working perceptron.
[00:27] As always, if you want to see the code
[00:28] for these samples, you could go to
[00:29] gojustangel.ai/code-3
[00:32] or excel-3 for the Excel file. Okay, so
[00:35] the first question we're probably going
[00:37] to have is what's a perceptron?
[00:40] And then like let's try and think about
[00:42] it not in terms of math, but what
[00:44] problems is it trying to solve for us?
[00:47] And the problem is that as we learn the
[00:49] English language, we have to make
[00:52] decisions about which word is the right
[00:54] word to say. We have to store
[00:56] information and then based on that make
[01:00] decisions. And I really really love this
[01:02] definition from Rosen Black 1958 where
[01:05] he asks the following questions. He came
[01:07] up with this concept.
[01:09] How is information about the physical
[01:11] world sensed detected by the biological
[01:15] system? In what form is information
[01:17] stored or remembered? And how does
[01:19] information continued in storage and
[01:21] memory then influence recognition and
[01:23] behavior? How do you store and how do
[01:26] you influence behavior with that? That's
[01:29] really what a perceptron or a neuron
[01:31] basic unit of work does. So a perceptron
[01:35] is the smallest unit of a neural
[01:37] network. Um GPT is really just 100
[01:41] billion perceptrons. That is a very very
[01:44] inaccurate summary, but it's also 51%
[01:48] kind of correct. So I think it's kind of
[01:51] interesting to note this is the basic
[01:53] unit of work. Um so on the right we get
[01:55] to see a a fun formula. This is going to
[01:57] be our second formula that we've
[01:58] encountered together. But again you
[02:00] don't have to understand it right away.
[02:02] We're going to really work through it.
[02:03] So f ofx= wx +b or another way of saying
[02:08] that that given an input the we have a
[02:11] weight. We multiply that by the input
[02:13] and we add a bias to that. If we were to
[02:16] implement that in code, we see a
[02:18] perceptron math method right here. And
[02:20] it's called P uh perceptron math. Weight
[02:23] time input plus bias. If I do 1 * 2 + 3,
[02:27] that equals 5. Right? So what does the
[02:30] perceptron really do? It holds
[02:32] behavioral information. It does
[02:34] funlinear math. There is to
[02:37] differentiate it from nonlinear math.
[02:39] Math that cannot be graphed easily on a
[02:41] linear line. and it can find edge edges.
[02:45] Really interesting stuff. Okay, so I
[02:47] didn't understand any of this before I
[02:49] or at least fully understand it beyond
[02:51] the math in the code before I saw this
[02:53] Welsh lab uh example. What uh this guy
[02:56] did is he built a physical analog
[02:59] perceptron. And I thought, wow, this is
[03:01] amazing. All of these weights and bias
[03:04] numbers, they're just knobs you get to
[03:06] turn. Isn't that amazing? Uh, I just did
[03:10] uh something really similar then because
[03:12] I love that idea. I'm a bit of a crazy
[03:14] person. I just built my own physical
[03:17] perceptron. Uh, that is really fun. So,
[03:22] in order to teach us this concept of a
[03:24] working perceptron, I'm going to just
[03:27] show you a video of me playing around
[03:29] with it. I'm going to mute the audio so
[03:31] if you want to watch it later, you'll
[03:32] have audio. But for now, I'll just
[03:33] narrate it myself. So we just learned
[03:36] about having perceptrons. That's really
[03:38] great. WX plus B. X is the input. W is
[03:42] the weight. WX and then B. So we said,
[03:45] and then we have the output for the
[03:46] perceptron. So W2
[03:50] * 1 = 2 + 1 = 3. 2 * 1 + 1 = 3. Very
[03:57] cool. So if I change the input, I can up
[04:00] it. Looks like I'm going to up it. Oh my
[04:02] god, it's so high. 2 * 2 + 1 4 + 1
[04:07] equals 5. We just learned about upper
[04:10] upper work. So I could bring the input
[04:12] further down. I could bring it down to a
[04:14] negative value. I could bring it down to
[04:16] min -1 * 2. That's -2 + one. Total of
[04:20] minus1. So a perceptron could also be
[04:23] negative valued. Right? And I could also
[04:25] change the bias and the weight
[04:27] themselves if I wanted to. Uh well, what
[04:30] am I going to do here? I'm going to
[04:31] increase the input. So fun. And I'm
[04:34] going to change the bias. So 1 * 2 is 2
[04:38] plus bias + 2 equals 4. Can bring the
[04:41] weight down now. So input is one. The
[04:45] weight is two. The bias is still two. If
[04:50] I change the weight, the formula would
[04:51] update correctly. Very cool. So now am I
[04:54] going to do that? Am I going to change
[04:55] the weight? Does Oh, I'm going to just
[04:57] change the input again. Wow. So maximum
[05:00] 2 * 2 + 2 equals 6. Very cool demo. Uh
[05:06] alternatively we can also bring the bias
[05:07] down to be negative and then we can make
[05:10] the like suppress the values of the
[05:12] weight and the input. So there's this
[05:13] relationship a linear relationship some
[05:16] would say between weight input and bias.
[05:18] Very cool. Okay. So now we saw that
[05:21] example but you guys you don't have or
[05:23] y'all you don't have this uh physical
[05:25] circuit to play around with. Let's go to
[05:27] gojustangel.as. I/neuralet and I built
[05:30] this demo that we're going to be working
[05:31] through in the next six sections. And
[05:34] then here we get to see the same thing.
[05:36] We have an input, a bias, and a weight.
[05:39] If uh and the input is one, the weight
[05:41] is 1 and 1/2 and the bias is 2. The math
[05:43] is here in the bottom. 1 1/2 * 1 + 2 =
[05:48] 1.7. But if I bring the input down to a
[05:51] negative value, oh my god, the output
[05:53] also goes negative. -1ish * 1 and 1/2 +
[05:58] 2 - one and - 1.2. Very cool to see. - 1
[06:03] and a 0.25. Very, very cool. So, there's
[06:07] a lot of stuff we could do with that. We
[06:09] could play with the bias, bring that up
[06:11] or down. We could play with the weight,
[06:14] bring that up or down. And we could see
[06:16] how the values go negative or positive.
[06:19] Why did I say that perceptance can't
[06:21] find edges? is because we could just use
[06:24] that zero as a point of reference for an
[06:27] edge. That's just a decision that I just
[06:29] made. Okay, great. So, we seen input is
[06:32] changeable. Weight is changeable. Bias
[06:34] is changeable.
[06:36] WX + B weight times input plus bias.
[06:42] Very cool. Okay. So, now we're going to
[06:44] go back here and you really recommended
[06:46] to try and play around with that demo a
[06:47] bit more. Let's see these examples both
[06:49] in Excel and then in code. So, let's
[06:52] open up Excel. First thing I do is I
[06:54] make a copy.
[07:02] Uh, and we're going to go with without
[07:03] answer sheet. And let's see what is
[07:05] going to be our neuron output. So, we
[07:08] have W of 1, X of 2, B of 3. Okay, kind
[07:11] of easy to do. W * X + B. We talked
[07:16] about this formula a lot so far. Oh my
[07:19] god, the answer is five. If I up the
[07:20] weight to two, the answer is seven. If I
[07:23] up the weight to 100, it's 2003. If I
[07:25] bring it down to negative, it's like
[07:27] one. If I bring it down to really
[07:29] negative because the bias is like
[07:31] bringing us up a bit. Now, it's really
[07:33] negative. Okay, cool. So, we just saw a
[07:35] single perceptron in action. What if we
[07:37] have a bunch of single perceptrons?
[07:38] We're still not at a like a real group
[07:40] of perceptrons, but let's say we just
[07:42] have a bunch of perceptrons. Okay. So, W
[07:46] * B * X + B. So, here I've hardcoded the
[07:51] W and B values, but I'm going to change
[07:53] the inputs. So, we have one perceptron,
[07:55] and we're going to just run a bunch of
[07:57] inputs through it. Okay, great. So, one
[07:59] thing that I do have to do is I'm going
[08:00] to have to lock down the bias and weight
[08:04] column
[08:05] cells, and I'm going to run through
[08:07] these. Great. So now we saw our one
[08:11] weight bias uh perceptron run through a
[08:13] bunch of different sequential inputs. So
[08:16] we could kind of see that these are the
[08:17] outcomes. And you could kind of tell
[08:19] there's a linear ratio here. Linear in
[08:21] the sense that it kind of changes
[08:22] similarly. But if I plot that out, uh oh
[08:26] my god, it's saying now I have to create
[08:28] a graph. That's going to be fun for me.
[08:30] Let's create a graph. Insert chart.
[08:35] I'm going to not want a column chart.
[08:36] I'm going to want a line chart.
[08:38] Wow, isn't this really cool? I'm going
[08:41] to just leave that here for now. Isn't
[08:43] this I'm going to make it a bit small so
[08:45] we can see all of it.
[08:47] So, weight one by three. Three ends up
[08:51] being where we intersect with the y
[08:53] value with the y axis. Uh we we kind of
[08:57] plot out all of these on the y column,
[09:00] all of the values in the y column and
[09:01] all the x's on the x x col uh xaxis.
[09:06] But what does B actually do? Let's see
[09:09] if there's a bunch of axis find X's in
[09:10] the base. Okay, so we set B to zero.
[09:12] Let's see what happens then. We set B to
[09:15] zero, it's going to inter the our line's
[09:17] going to intersect with uh Y at the zero
[09:20] point, right? If I put it to one, it's
[09:22] going to intersect at 1 2 3. Wow, really
[09:25] cool. We get to see real live updates.
[09:28] Uh what happens with if I take weight
[09:30] negative if it's going to flip the air
[09:34] the the line that we've got here. Very
[09:36] cool. We could change the direction of
[09:38] the line. What happens if it goes to
[09:40] very very close to zero but not zero. Oh
[09:44] my god. We got a horizontal line right
[09:47] there. Almost completely horizontal line
[09:49] that still takes the input a little bit
[09:50] in because it's not perfectly zero. Um
[09:54] very cool. So we learned a lot of very
[09:56] fun things when we did that.
[09:58] Uh, now let's try and see if there's a
[10:00] landscape we could do here. So, I'm
[10:02] going to fix the weight at one, but I'm
[10:04] going to change the bias and I'm going
[10:05] to change the input. And let's see if
[10:07] there's some sort of like thing that I
[10:10] could do with that. So, we said weight
[10:13] times input plus bias. Okay, so at
[10:18] input, I'm going to have to uh fix the
[10:22] column because I'm going to drag it
[10:24] down. And then at bias, I'm going to
[10:27] have to uh fix the row because I'm going
[10:29] to drag down as well. Uh did I just say
[10:33] something true? Let's see what happens
[10:34] if I do that. That doesn't look true to
[10:37] me. I'm just going to copy my formula
[10:39] from here. It's going to make it easier
[10:40] for us to not make mistakes. Here we go.
[10:43] I'm going to drag this down here. Going
[10:45] to drag this down here. Now, we have a
[10:48] bunch of these based on the bias and
[10:51] different inputs. Fixed weight, two
[10:53] dimensions. So, but that's kind of hard
[10:55] for me to read. I don't really read a
[10:56] bunch of numbers. I'm going to do this
[10:58] one time and one time only with you.
[11:00] Conditional formatting
[11:02] color scale. You could because this goes
[11:04] down to the negative. We'll choose the
[11:06] red to green. Oh my god, we found that
[11:09] there's a little valley in the middle of
[11:12] this chart, right? There's like this
[11:14] little middle of this table. There's
[11:16] like this values around zeroish. It's
[11:19] really nice to visualize with a color
[11:21] with color schemes. Great. So if we also
[11:25] wanted to visualize with color, we only
[11:26] choose two colors, red and green, we can
[11:29] see there's a real edge, a real
[11:32] separator, a real classifier. Use
[11:35] whatever word appeals most to you right
[11:37] now at around the zero mark, right?
[11:40] Because we said all the positives and
[11:42] zero should be green and all of the red
[11:43] should be should be red. So we now have
[11:46] a little separation boundary here. Very
[11:48] cool. That is how perceptrons affect
[11:51] behavior. What? Like for example,
[11:53] positive values are going to impact
[11:55] behavior in one way. Negative values are
[11:57] going to be in another way. We're going
[11:58] to learn more about that when we get to
[12:00] activation functions. Cool. So, we saw a
[12:03] little bit of Excel. Let's jump into
[12:04] coding. So, we've already said you can
[12:07] connect to a GPU here. I actually don't
[12:10] think you're going to need a GPU. You
[12:12] can just use a CPU. And then you can
[12:13] click run all. So, how do we implement
[12:16] wx plusb? Well, one option is we just
[12:19] implement it in weight times input plus
[12:22] bias here in a function in in uh Python.
[12:26] If you've never seen Python functions
[12:27] before, here's how a Python function
[12:29] looks like. And then we can Okay, we
[12:32] know we don't write code in functions.
[12:34] That's kind of weird. We're going to put
[12:35] it maybe in a class. So, I'm going to
[12:37] have a class that takes in the weight
[12:39] and the bias because those are fixed,
[12:40] but then runs it multiple times with the
[12:44] activate function.
[12:46] Okay, great. So, you should probably
[12:48] implement uh this f(x)= wx +b somewhere
[12:53] here. Not super hard to do, but I'm
[12:55] going to leave that as an exercise for
[12:57] you. If you want to see the answer, you
[13:00] do have the answer here in the base
[13:01] under show code. I'm not going to show
[13:03] it to you right now because you already
[13:05] know it's weight times input plus bias.
[13:08] Maybe you have to add the word self once
[13:10] or twice." Okay, great. So, go you can
[13:13] go ahead and do that yourselves. Once we
[13:15] did that, you can um uh call the uh
[13:20] perceptron class 10 times in a row with
[13:23] different inputs. So this range is just
[13:24] going to generate between minus5 and
[13:26] five. And then I'm going to say here I'm
[13:29] going to call my perceptron.activate
[13:31] with this value I just change the number
[13:33] 42 to something else. If you need the
[13:35] answer, it's below. But when I run it,
[13:38] the answer that is I see for input minus
[13:41] 5, I get minus2. two for an input of
[13:43] minus4 I get an output of one right
[13:45] that's for uh the perception we
[13:47] initialize a moment ago with a values
[13:50] weight one bias three okay so we just
[13:53] did this in excel you kind of know
[13:55] what's going to come up next it's going
[13:56] to just be a line chart oh my goodness
[14:00] if bias is three it intersects the
[14:02] y-axis at three and if the weight is one
[14:05] it's going to be a perfectly linear line
[14:06] where for every point we increase it's
[14:08] going to change play around with these
[14:11] weight values is play around with these
[14:12] bias values, generate a bunch of charts.
[14:15] It's going to help you build a lava of
[14:17] intuition.
[14:19] Why? Because these charts are going to
[14:21] build something called a landscape. And
[14:22] we're going to see these landscapes
[14:24] pretty soon. That's about section seven,
[14:26] I think. Great. So, what did we see here
[14:29] in perceptron land? We saw that there's
[14:31] a math formula for a perceptron and it
[14:34] holds information and influences
[14:36] behavior. And we saw the math for that.
[14:38] We then saw a fun metaphor which is
[14:41] building a circuit. Then we saw a video
[14:44] of me building my own circuit because I
[14:46] apparently have so much free time. Uh
[14:49] and then we saw you having a demo that
[14:51] you could basically play with something
[14:53] very similar to this physical
[14:55] perceptron. I'm going to show you the
[14:56] physical perceptron one more time. Oh my
[14:58] goodness. Those two things kind of look
[15:00] pretty similar.
[15:03] Uh then we saw code Excel example of
[15:06] working with a wx plusb formula and then
[15:09] finally we saw code of working with wx
[15:11] plusb. You might be wondering surely
[15:14] there's a platform or uh framework out
[15:17] there that implements perceptrons. Yes,
[15:20] there is. We're going to see that next.
[15:21] We're not going to see that right away.
[15:23] Uh we're going to see that when we get
[15:25] to PyTorch. Great. When are we going to
[15:27] get to PyTorch? In section 4, activation
[15:30] functions. We're going to talk more a
[15:31] lot about that when we get to activation
[15:33] functions. Why do we need activation
[15:36] functions on perceptrons? Because
[15:38] they're not great at finding edges. We
[15:40] kind of had to falsify that the zero is
[15:43] an edge, but then it's very linear and
[15:45] it's not super easy to use. Maybe we'll
[15:47] see more about that when we get to
[15:48] section four, activation functions. I'll
[15:51] see you then. Thank you.
