# Activation Functions: ReLU, GELU | Build Your Own LLM Workshop #4

**Build Your Own LLM Workshop — Video #4 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 25m 50s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=G5gkYVB-P-Q |

## Description

No description available.

---

## Full Transcript

[00:00] Hello, welcome back to a build your own
[00:03] large language model workshop with me
[00:05] Justin Angel. We last left off learning
[00:08] about basic perceptrons. The basic unit
[00:10] of work for any large language model. So
[00:13] one perceptron is what we work with, but
[00:15] 100 billion of those is going to end up
[00:18] creating a JPT style chatbot. Next up,
[00:21] we're going to look at activation
[00:22] functions and it's how we introduce
[00:24] something called nonlinearity. What's
[00:26] nonlinearity? we're going to see in the
[00:28] next slide. But importantly, this
[00:30] section is only going to have Excel in
[00:33] it. It's not going to have any code. The
[00:35] next section is going to have the code
[00:36] implementation for activation functions.
[00:38] Why? Wait until the next section and
[00:40] you'll find out. And now importantly to
[00:43] mention as well is that our deliverable
[00:44] is RLU squared. What is RLU? Why is it
[00:47] squared? We're going to find out during
[00:49] this one section. No one knows. Great.
[00:52] So, our first slide is pretty ugly. If
[00:56] you're interested in knowing, there's a
[00:57] great slide here that's actually much
[00:59] better. JedjPT generated it for me. I
[01:02] think it's much more visually attractive
[01:04] and slightly more uh informative, maybe
[01:07] a little less accurate, but you're not
[01:09] going to get to see that. You're going
[01:10] to see my ugly slide instead. Uh because
[01:13] all of my slides I wrote myself and I
[01:15] couldn't figure out how to make the
[01:16] slide pretty. Great. So, why do we need
[01:19] nonlinearity? Because the world is
[01:22] nonlinear, right? We want to find edges
[01:25] and we want to make it very very easy
[01:27] for networks or perceptrons to find
[01:30] edges and perceptrons are okay with
[01:33] doing that but they're not great they're
[01:35] only good for linear things right things
[01:37] that have linear ratios not great at
[01:39] parabas or any other s sort of shape. So
[01:42] in order to find edges in the real world
[01:45] we're going to need to be able to have
[01:47] something that kind of like enhances the
[01:50] output of perceptrons. What's an example
[01:52] of nonlinearity in the real world? world
[01:54] well world. One example is detecting the
[01:56] edges of building or people or stuff
[01:58] like that. That's pretty common in
[01:59] vision um uh in vision uh in computer
[02:03] vision or in robotics. Another thing we
[02:06] might want to do is absolute values.
[02:08] Pretty common in mathematics. There's no
[02:10] way to do an absolute value if you're
[02:12] just using linear math, right? Minus 3
[02:15] does not equal three in linear math
[02:16] unless you know weight is zero, I guess.
[02:19] But other than that, we're never going
[02:20] to be able to do that. Um, another thing
[02:24] is like the store operator, which we're
[02:26] going to see by the end of this chapter.
[02:29] But I want to give you an example from
[02:30] text cuz we're here building large text
[02:32] models. Why would we care about
[02:34] nonlinearity for text? Right? Imagine
[02:38] that I said something the movie was
[02:40] great or the movie was awful. Those two
[02:43] things live on the opposite side of a
[02:45] sentiment spectrum. awful and phenomenal
[02:48] are opposites in the in the sentiment
[02:50] spectrum. But if I want to say the
[02:53] intensity of the emotion expressed with
[02:56] great or phenomenal and awful, they're
[03:00] both high intensity values. So I have to
[03:03] take the sentiment and absolute value it
[03:06] to get it how how intense it was. So
[03:10] even ver even verbally in words we have
[03:14] to find absolute values. So all of these
[03:16] kind of like little examples tell us we
[03:18] need a better edge detection mechanism
[03:21] than straight up perceptrons because
[03:22] perceptrons can't really find most
[03:24] edges. Okay great. So what's the most
[03:27] basic way for us to do that? We kind of
[03:29] hinted at that earlier. Zeros is really
[03:32] really great place for perceptron
[03:34] outputs to draw an edge. So in ru what
[03:38] ru does uh in ru was part of the 2017
[03:42] all you need is is attention paper very
[03:44] famous paper that created transformers
[03:47] what they say like ru is any x that is
[03:51] bigger than zero use that x value any
[03:54] other x negative x's return a zero
[03:58] effectively it compresses our signal and
[04:00] say any negative signal just discount it
[04:03] completely we don't need it we only need
[04:05] positive values we does introduce a
[04:07] nonlinearity. What is nonlinearity? When
[04:10] we look at the value for minus4 and
[04:12] minus1, there's no linear ratio there,
[04:15] right? There's no way to reverse
[04:17] engineer what the original signal was.
[04:20] So, we introduced a nonlinearity into
[04:22] the system. And in in formulaic sense,
[04:26] it's max 0 or x, right? Basically saying
[04:29] choose the highest of the two, either
[04:31] zero or x. If x is positive, it'll
[04:32] always be the x. If it's negative, it'll
[04:34] always be zero. Um, so now I want to
[04:37] address a little bit of a something
[04:39] here. Um, which is why a lot of the
[04:42] numbers we're going to look at today are
[04:44] going to be between minus4 and four. Um,
[04:47] those represent something called normal
[04:50] distribution standard deviation, right?
[04:52] And then if you don't know what that is
[04:54] in statistics, totally fine. We're going
[04:55] to actually cover that in a lot of
[04:57] detail in section 10. But for now, you
[05:00] should remember that a lot of these
[05:02] numbers trend between minus4 and four
[05:04] because we're dealing in standard
[05:05] deviation. Most numbers in a normal
[05:08] distribution live three dist standard
[05:11] deviation away from the norm. How much?
[05:12] Most 99.7% of numbers live within three
[05:16] standard deviation away from the norm.
[05:18] And presumably a lot of the numbers the
[05:20] perceptrons work with are going to be in
[05:21] standard deviations. Hopefully,
[05:23] presumably not always, but that's kind
[05:26] of just to explain that. And then maybe
[05:28] I should mention the word logits. Logits
[05:30] are the outputs of machine learning
[05:32] models. One perceptron is a machine
[05:34] learning model. So its output would be a
[05:37] logit and those numbers tend to be
[05:40] between minus4 and four because of
[05:41] standard deviation. So now you know the
[05:43] word logits. Now we know the word relu.
[05:45] Now you've seen the formula for relu.
[05:47] What's important to remember from this
[05:49] slide? There's a lot going on here.
[05:51] Activation functions allow machine
[05:55] models to know when things stop and
[05:57] start.
[05:59] Critical to understand when things stop
[06:02] and start, right? These big large
[06:04] language models have to model the
[06:06] entirety of the language. Things stop
[06:08] and start at a point. It gets cold at a
[06:11] temperature. People are considered tall
[06:14] at a certain height. We need ways of
[06:17] modeling those edges when things stop
[06:20] and start. if even in language even when
[06:23] there's nothing visual going on.
[06:25] Great. So let's jump into our uh pseudo
[06:29] analog perceptron. I will mention that
[06:31] earlier you saw a video of a perceptron
[06:34] and it had sections that we didn't see
[06:37] this section specifically for ru. So
[06:40] we're going to start off from this
[06:41] online demo and then we're going to go
[06:43] back to the video. So this online demo
[06:47] now I added so if you remember earlier
[06:49] we had weight and bias and input and
[06:51] then weight times input plus bias that's
[06:55] the output of a perceptron. Well now I'm
[06:57] going to take the output of the
[06:59] perceptron and put a rail function in
[07:01] between it. So input one weight one and
[07:04] a half plus two you can see the math
[07:06] down here it's uh 1.7. Okay. But if I
[07:10] drop the input, oh my god, the output is
[07:14] dropping. The output is dropping. But we
[07:16] don't want negative values now. And as
[07:19] soon as the outputs are equal to
[07:21] negative values, right? Uh let's say
[07:24] input of minus1ish.
[07:27] Uh this whole per this whole thing
[07:29] should clearly be negative the entire
[07:32] result of this formula. But relu blocked
[07:35] it. Let's bring the input back to
[07:36] positive. And now didn't block it. And
[07:39] now RLU blocked it. And now RLU blocked
[07:41] it. So changing the input on this
[07:43] perceptron, this perceptron now blocks
[07:45] negative input like the inputs that
[07:47] would cause negative uh values. It stops
[07:50] it at zero. And of course if we also
[07:52] change the bias for the perceptron. If
[07:54] we lower increase, if we lower the bias
[07:57] now, a lot more many more values are
[07:59] going to end up with the negative value.
[08:02] Right? Even if I bring down the input to
[08:05] positive, bam, rail is still going to
[08:07] have to block it because the bias is
[08:09] quite negative. Okay, great. So now we
[08:11] saw that we could change bias and weight
[08:13] and inputs and rail is going to block it
[08:14] and unblock it, block it, unblock it,
[08:16] block it, unblock it. Very cool. So we
[08:19] just saw that. Let's see that in a video
[08:21] again. I'm going to talk over that. Then
[08:23] I'm going to mute the audio.
[08:26] >> So here we go. So previously we saw the
[08:29] wx plus b we have weight of one x of a
[08:33] half and b of a bias of one that's one
[08:36] and a half
[08:38] and after we added the ru uh uh to the
[08:42] circuit and then that is going to
[08:45] transfer perceptron output to output at
[08:48] one because everything is positive rail
[08:51] doesn't have to engage at all but if I
[08:54] change the let's see what am I going to
[08:56] change the bias the negative. Can Am I
[08:59] just going to bring the Yeah, bias goes
[09:01] super negative now. Bam. Rau kicks in.
[09:04] Look at the RLU bulb. Look at it again.
[09:06] I'm going to bring it back up. And boom,
[09:08] the RU bulb went off. Let's bring it
[09:11] back down again. We can see that even
[09:13] though the perceptron value is negative,
[09:14] the output value is zero. Right? The RLU
[09:18] function is going to stop the val the
[09:20] negative values of perceptron from
[09:22] flowing into the output. And that is
[09:25] effectively what RLU does. Okay, great.
[09:28] So we learned about RLU. Now I have to
[09:30] shatter your expectations of reality. Um
[09:33] 10 2025 survey 53 open source large
[09:36] language models or maybe I think a few
[09:38] that are yeah mostly open source ones
[09:41] and then uh no one uses RLU anymore.
[09:43] That's the sad reality of that. Um RLU
[09:46] was really used in that first original
[09:48] 2017 paper attention is all you need.
[09:51] maybe was also used in 2019 when we when
[09:54] GPT2 was built, but it's really not
[09:57] commonly used anymore. You can see that
[09:58] here on the chart on the right. What is
[10:01] used where we could see a new family of
[10:04] glue kind of took over from RLU pretty
[10:07] soon after RLU was introduced and that's
[10:09] pretty common at this point. And even
[10:12] more recently in the last three years,
[10:15] the gated units or swigloos have taken
[10:19] over completely in modern architecture.
[10:22] But we're going to be working here today
[10:24] and we get to choose which one of these
[10:26] we want to model. Since we are building
[10:28] a GPT2 style transformer, we'll stick
[10:30] pretty close to RLU. Maybe kind of close
[10:33] to Galu or Galoo as I like to say it,
[10:36] but not we're not going to get all the
[10:38] way to Swiss glue today. Great. And we
[10:40] actually will look at rich glue kind of
[10:43] later in I think section 18. We'll talk
[10:45] a bit more about it. Uh Zho 2023 did a
[10:48] survey of a thousand papers. Uh this is
[10:50] that column here and it kind of found
[10:52] something similar. Basically no one uses
[10:54] rail bases that one paper and a few
[10:56] papers that followed it. It's very
[10:58] uncommon. Shazir 2020 introduced the
[11:01] swiggloo function in a 2020 paper and
[11:04] then it bas he and what they showed is
[11:07] the comparative compar performance of
[11:10] these activation functions and they
[11:12] showed that ru and ga and swish and glue
[11:15] and and a few other ones actually
[11:17] swigloo performed best. At this point
[11:19] you might be asking yourself why it
[11:21] performed best. Hold that question to
[11:23] the end of the section. We'll have some
[11:25] version of an answer to it. Great. So
[11:27] now we talked about ru and we talked
[11:29] about other activation functions. We
[11:31] only talked about three. We talked about
[11:32] ru and galu and swigloo. Really those
[11:34] are the three. There's so many other
[11:36] more activation functions though. So
[11:38] there's ru and galu and prelu and elu
[11:41] and swish and celu and soft and mish and
[11:43] sigmoid and 10h and haran and you know
[11:47] there's like a whole uh cake here of uh
[11:51] of formulas. There's 10h and sigmoid and
[11:55] leaky rau and galu. Why is there a cake
[11:57] here? Because when I wrote this slide
[11:59] initially, I'm going to delete this
[12:00] cake. I thought this slide looks really
[12:02] scary. So, I introduced a cake for you
[12:04] to be less scared of this uh slide.
[12:07] What's the point of this slide besides
[12:10] scaring you with like not cake, right?
[12:13] It's to let you know that there's many
[12:14] many activation functions. There isn't a
[12:17] correct activation function, right? You
[12:19] have to experiment where machine
[12:21] learning is an empirical field. you
[12:23] choose the activation function that
[12:25] performs best. Great. So, let's go to
[12:28] Excel. Now that I've shown you a math
[12:30] formula many times and a bunch of demos,
[12:31] I think we can maybe like do a little
[12:33] bit of like coding together. So, I'm
[12:36] going to make a copy of this and we're
[12:37] going to start out with the without
[12:39] answers sheet and we're going to start
[12:41] coding stuff together. So, we're going
[12:42] to start off with RLU. We kind of talked
[12:44] about Railu a moment ago. We know that
[12:47] RU is max zero. So relu max zero or the
[12:53] this value of the input enter and oh my
[12:57] god input of five ru of five input of
[13:00] minus5 relu of zero it introduces the
[13:03] nonlinearity okay so that was one ru can
[13:06] we intro do ru to a bunch of input
[13:09] values I'm going to take this input
[13:11] value here and I'm going to drag it all
[13:14] across here oh my goodness we just raed
[13:18] a bunch of values All the negative
[13:19] values are zero, right? All the positive
[13:23] values are passed through straight is
[13:26] from ru. Great. So now we can obviously
[13:29] take this and chart it. And what do we
[13:31] get when we do that? That's the
[13:33] illustration we saw earlier of the
[13:35] various val the shape of the chart of ru
[13:39] of a line chart with ru. So that's one
[13:42] way to kind of think about ru in a
[13:44] graphical way. I think visually this
[13:47] makes a lot of sense to me. This kind of
[13:48] made really make sense to me. Everything
[13:50] under zero not we don't really care but
[13:53] we're going to suppress that signal.
[13:54] Everything above zero where it's a
[13:56] straight pass through. Okay, great. So
[13:58] what this is a two-dimensional
[14:01] chart. I'm wondering if we can make it a
[14:03] bit more oomphy. So let's say I have all
[14:06] of these inputs here, right? All these
[14:08] inputs here and all of these inputs
[14:10] here. And then I build this big chart
[14:11] where I just basically multiply the
[14:13] input by two, right? So this chart goes
[14:15] from -9 to 9 has this interesting value
[14:19] in the middle. What happens when I
[14:21] convert it to relu. Okay, great. So max
[14:25] zero. I'm going to take this value here.
[14:29] Great. I'm going to drag and drop this
[14:31] to the whole row. I'm going to drag and
[14:33] drop this for the whole table. Okay. So
[14:37] that's still not super clear to me. We
[14:38] said we're going to do conditional
[14:40] permitting. This is the only other time
[14:42] you'll see me do conditional formatting.
[14:45] Great. And then we're going to choose
[14:47] white to green because it's ne uh zero
[14:50] to positive.
[14:53] Wow. We could really see there's like a
[14:56] flat section of this chart. What do you
[15:00] mean by just that this table is flat?
[15:02] Let's try and pull it a
[15:04] three-dimensional view. You can't do
[15:05] that in Google Sheets, but you could do
[15:07] it in Excel. So, I screenshotted that.
[15:09] If we looked at this from the side, you
[15:12] could really see that the positive
[15:14] values have this little tilt lift
[15:17] happening, right? Like these are two
[15:19] side views of just taking this data and
[15:21] rendering it in 3D. That's all I did
[15:23] here. Why is that interesting to us?
[15:26] Because we're going to see in loss
[15:28] function that a lot of what we do is
[15:30] just navigate landscape. And by when we
[15:33] navigate landscapes, activation
[15:34] functions help us do that. That sentence
[15:37] made no sense to you right now. That's
[15:38] totally fine. But important to remember
[15:41] activations functions can be rendered in
[15:44] a line in a line chart. It can be
[15:46] rendered as a 2D landscape and it can be
[15:49] rendered as a 3D landscape. Super
[15:51] interesting to note. Great. So now we've
[15:54] been talking about RLU and R this and
[15:56] RLU that this whole time. Let's use RLU
[15:58] squared. Y squared. We're going to see
[16:00] later, but this is a nice function to
[16:03] know how to do. So let's read the
[16:04] formula together. max of 0x and then you
[16:07] just square it. Okay, that's pretty
[16:09] easy. So, it's max of the input
[16:14] or zero and then I'm going to uh power
[16:18] to this. Great. I'm going to throw that
[16:21] here. Great. So, these are the values of
[16:23] rel squared. What happens when I plot it
[16:26] out? You can see relu and relu squar
[16:28] behave differently at different
[16:30] magnitude of values. Negative values
[16:34] still whatever right no pass through
[16:36] they're going to be zero but for
[16:38] positive values the higher the value the
[16:40] more intense the magnitude is really
[16:43] interesting insight on relu squared
[16:46] right it really extenduate it it really
[16:49] increases the differences in increases
[16:53] the difference of the outputs of
[16:54] perceptrons
[16:56] the higher the output is maybe that's
[16:59] super useful for something we'll see
[17:01] that in a moment
[17:03] uh in a sense that we'll learn how to
[17:05] choose activation functions. Okay, so we
[17:07] talked about relu and we talked about
[17:09] relu squared. Let's talk about leaky
[17:11] relu. I'm going to try and handcode this
[17:14] myself now. Let's see if I'm successful.
[17:17] So leak le leaky relu says for values ar
[17:20] bigger than zero we're going to want to
[17:22] use the in the input value but for
[17:25] values less than that we're going to
[17:27] multiply them by something. So if input
[17:31] is big less than zero then bigger than
[17:34] zero just use the input otherwise take
[17:38] the value but multiplied with a very
[17:41] small number this leaky alpha value.
[17:44] Great. So I wrote that if statement here
[17:47] I'm going to drag this all over the
[17:49] line. What do we get? I should have
[17:54] locked this here. Here we go. What does
[17:57] this get us? When we do that, we could
[18:00] see that there's a little itty bitty
[18:03] line underneath leaky reglu. Why is this
[18:06] itty bitty line super interesting to us,
[18:09] right? Because it doesn't suppress the
[18:11] signal, the negative signal of the
[18:13] outputs completely. It does suppress it.
[18:17] It suppresses it by a lot, 20% with a
[18:19] leaky alpha of 0.2. But it can suppress
[18:22] it a little bit, right? or a lot, but it
[18:25] will just still have some signal in it.
[18:28] That's super useful if you don't want
[18:30] neurons in big networks to get totally
[18:33] turned off and totally be ignored. So
[18:35] leaky relu super useful if you want to
[18:38] do that. Okay, so is there anything
[18:39] other than leaky rau? That one was
[18:42] pretty simple. We're just going to like
[18:43] multiply by a small value. Well, there's
[18:46] galoo. And galoo is actually a really
[18:49] complicated uh uh uh activation
[18:51] function, but it's still based on a
[18:54] single value. So glue is you take x you
[18:58] multiply you power three it you multiply
[19:00] by 044 you add x back in you multiply it
[19:04] by two / pi you square you square root
[19:07] that portion you 10 h it you you add one
[19:11] to it you multiply that by x you
[19:13] multiply that by.5 really really
[19:16] complicated you're never going to have
[19:17] to remember this formula but you could
[19:21] see here an implementation in uh Google
[19:23] sheet formulas that Claude was kind
[19:26] enough to write for me. And then we
[19:29] could see, oh my goodness, these are the
[19:31] values. Let's try and put them on a
[19:34] graph. We can see that glue has this
[19:36] little bump between like very small
[19:40] negative values and zero. Why is that
[19:42] useful? Again, we're going to not lose
[19:45] the signal completely of a tiny bit of
[19:48] linear of negative value. We're not
[19:51] going to lose the complete negative
[19:53] value. We will if you keep going neg
[19:55] very negative but for like the area
[19:58] right before zero it actually is pretty
[20:00] useful to not lose the values
[20:02] completely. Why? Because rail is kind of
[20:04] like linear linear linear linear linear
[20:06] and then it shuts off. It's really hard
[20:08] for our network to learn with that.
[20:09] Maybe giving it a little bit of a
[20:11] negative bump there and still
[20:12] maintaining a little bit of signal but
[20:14] only the beginning is really useful.
[20:16] Okay great. So we saw leaky ru and gaou
[20:20] and ru squar and ru. Are there more
[20:23] functions? Yes, there's like a whole
[20:24] smorgish board of functions. There's 10h
[20:28] which uses exponents. There's sigmoid
[20:30] which uses exponent. There's celu which
[20:32] uses exponent. I think we're starting to
[20:34] see a a thing here. And swigloo which is
[20:37] what we call a gated activation
[20:40] function. We're not going to explain a
[20:41] lot about them in this class cuz you
[20:43] don't have to have them to build your
[20:44] own large language model. But important
[20:46] to know that gated modules uh activation
[20:49] functions do exist. So, I'm going to I
[20:51] already have all of the formulas here
[20:53] written out. What happens if I plot all
[20:55] them on a graph? Wow, isn't that pretty?
[20:59] Let's take a moment and appreciate how
[21:02] pretty this looks. This like looks like
[21:04] almost like a DNA helix to me or
[21:06] something, but there's like a really
[21:08] beautiful pattern that we could start
[21:10] seeing.
[21:12] So a lot of these activation functions
[21:14] in the values between 0ero and one kind
[21:16] of perform similarly but the question is
[21:19] how do they perform in negative values
[21:21] and how do they perform in values above
[21:22] one. Do they extenduate differences? Do
[21:25] they not extenduate differences? Do they
[21:29] uh work with negative values or do they
[21:31] not? So that's the question that you
[21:33] should be asking yourself as you're
[21:34] looking at this. Where do activation
[21:36] functions agree? Where do they diverge?
[21:39] which is the most interesting quadrant
[21:41] here. To me, that's 0 to one, but you
[21:43] could find other quadrants that are
[21:44] really interesting. So, that kind of
[21:46] maybe talks a little bit about the how
[21:48] we choose activation functions. Okay, so
[21:51] now you saw a bunch of activation
[21:52] functions in Excel. Uh we are not going
[21:55] to see code right away, but let's talk
[21:57] about why I'm going to use RLU squared
[21:59] for my for me when I build my large
[22:03] language models as I ran in my
[22:04] pre-training scripts. Well, why am I
[22:08] using RU Squared? It's because Karpathy
[22:10] said so. So, if you open up this uh uh
[22:15] um uh this PR that he had for Nano Chat,
[22:19] what you could see is if you look at
[22:21] section number five and he was trying to
[22:23] build like a training for uh GPT2 at sub
[22:27] $100. He said really squared worked
[22:30] really well for him. Um amazing. So
[22:33] we're going to use that as the logic for
[22:35] why we're going to do this. Remember
[22:37] machine learning is an empirical field.
[22:39] We run application tests and if
[22:40] something's faster, we're just going to
[22:42] or better faster better better
[22:45] performance from GPUs, but then we're
[22:47] just going to use it. Realistically for
[22:49] our 124 million GPT2 style model
[22:52] training on an H100, it almost doesn't
[22:55] matter. Why? Because we're trying to
[22:57] move a banana with a truck, right? It's
[22:59] like putting a banana on a bedrock of a
[23:01] truck and then the semi-trail and moving
[23:03] it across country. There's plenty of
[23:05] room available for us, but I'm still
[23:07] going to use Rail Squared because I like
[23:09] using Rail Squared for very small
[23:11] models. Okay, so now we're going to
[23:13] finish off with this real honest to god
[23:16] code from Shazer 2020. When they
[23:18] introduced
[23:20] Swigloo, which is the currently the most
[23:22] favorite activation function, they said
[23:25] this, and I'm going to quote it
[23:26] verbatim. Very rare for me to do that.
[23:29] We offer no explanation why these
[23:31] architectures work. We attribute the
[23:33] success to divine benevolence. Listen,
[23:36] as you're looking at these Excel
[23:38] spreadsheets and you've got these charts
[23:40] and you can kind of like hypothesize
[23:42] negative values work like this, really
[23:44] positive values work like that and you
[23:46] can build up hypothesis. The field has
[23:48] advanced a bit since then. But ML is an
[23:51] empirical field. We use the things that
[23:54] work. So when I build my large language
[23:57] model, my small EDBD GPT2 style model,
[24:00] I'm not going to use Rail. I'm going to
[24:01] use Railu squared because divine
[24:03] benevolence means it works better.
[24:06] Great. Now I'm going to show you this
[24:08] last thing that I want us to see
[24:09] together, which is go
[24:11] Justinangel.ai/Elego.
[24:13] And then here, what we get to see is
[24:17] that all these choices we're making
[24:19] throughout the day, for example,
[24:20] choosing RU over RLU. I could choose
[24:23] RLU. I could choose leaky railu. I could
[24:25] choose gaou. I could choose sigmoid. I
[24:27] could choose swish or silent selu. I
[24:30] could swigloo. Right? I'm going to make
[24:32] all these choices here. There's a bunch
[24:34] of choices we're going to cover
[24:35] throughout the day. There's a lot of
[24:37] alternatives during the day. But as I
[24:39] choose something, it's going to end up
[24:41] here in this little prompt in the base
[24:44] activation function relu squared. I can
[24:47] then copy it to my to a large language
[24:50] model and say, "Hey, would you mind
[24:52] building me a Python notebook with a
[24:53] pre-training script based on these
[24:56] decisions?" So, I actually think that's
[24:57] really interesting to try and do uh for
[25:01] as an exercise. And that's kind of how
[25:03] you can write your own pre-training
[25:05] scripts even if you're not super
[25:06] comfortable writing pre-training
[25:07] scripts. Important to understand the
[25:09] decisions we may not necessarily be able
[25:11] to write every single line of code
[25:13] yourselves. We live in 2026.
[25:16] Okay, great. So now you know about the
[25:18] Lego builder. Very fun. Next up is going
[25:21] to be implementing activation functions
[25:23] in code. Why why is it not in section
[25:26] four? Cuz there's like six ways or many
[25:29] more ways to write that code. And it
[25:32] depends on how good GPU performance you
[25:34] want to have out of it. So for section
[25:37] five, we're going to think about how to
[25:38] implement activation functions in code
[25:40] at various levels of GPU coding. I hope
[25:43] to see you then. Thank you so much. See
[25:45] you in GPU performance section.
