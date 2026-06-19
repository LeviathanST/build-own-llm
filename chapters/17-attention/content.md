# Attention | Build Your Own LLM Workshop #17

**Build Your Own LLM Workshop — Video #17 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 58m 28s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=CvGf-Eu2sl0 |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to a build
[00:02] your own large language model workshop
[00:04] with me, Justin Angel. We're we've
[00:08] arrived at some really exciting stuff.
[00:10] We're finally at the attention
[00:12] mechanism, which is the core of how
[00:14] transformers work. Why is attention so
[00:16] exciting? It's the secret sauce of
[00:18] transformers. Before this we saw
[00:21] tokenizers, we saw embeddings but
[00:24] attention is how we do a lot of the
[00:27] reasoning within uh large language
[00:30] models. We've also seen MLPS which are
[00:32] the other secret secret sauce I guess.
[00:35] But now we're going to see attention.
[00:38] So when we talk about attention the
[00:41] thing to realize is that I'm not going
[00:43] to try and teach you attention without
[00:45] teaching you the formulas first. Why is
[00:47] that? without seeing the formulas first,
[00:49] it's kind of wonky to try and understand
[00:51] what attention even does. So, my goal
[00:53] here is to teach you some formulas.
[00:56] Don't worry about the specific formulas.
[00:58] We'll see them broken down step by step
[00:59] in Excel. Conceptually, I want you to
[01:02] think about what attention tries to do.
[01:04] It correlates every input token with
[01:07] every other input token using learned
[01:10] concepts. What does that mean? I don't
[01:12] know. Maybe we'll have a slide dedicated
[01:14] to that later. How do you correlate
[01:16] every token with every other token? That
[01:18] sounds kind of weird. That sounds kind
[01:20] of convoluted. That sounds kind of
[01:22] quadratic if you ask me. That's not a
[01:24] nice word in computer science, but we'll
[01:27] see that in a second.
[01:29] How does it do it? How does it learn
[01:31] like all of these various connections?
[01:34] Each attention head learns specific
[01:37] concepts in something called a key value
[01:39] query. You're going to hear those words
[01:41] a lot. key value query using back
[01:44] propagation. These get combined and
[01:46] passed to more attention in the next
[01:48] layer. What does that even mean? I don't
[01:50] know. We're going to see all of that in
[01:52] Excel. But now we're going to be for the
[01:54] very first time. We're going to try and
[01:55] review the formulas. Totally fine to not
[01:58] get them right now. You're going to get
[01:59] them when you see them in Excel. They
[02:01] look very complicated and very
[02:02] intimidating here. They're actually
[02:04] pretty straightforward and contain
[02:06] almost no secret sauce as far as I could
[02:08] tell in them. Great. So the first of the
[02:11] three formulas we're going to learn for
[02:12] attention for specifically MHA multi
[02:15] head attention
[02:17] is going to be Q K and V. How do we get
[02:21] Q K and V? Quy key and value. We're
[02:25] going to multiply our input matrix by
[02:28] some learned weights. We have query
[02:30] learned weights. We have key learned
[02:31] weights. We have value learned weight.
[02:33] We're in order to get our key our query
[02:36] key and value. What we're going to do is
[02:38] we're going to just multiply the input
[02:40] by those learned weights. That doesn't
[02:42] sound super complicated. Or maybe it
[02:44] does. I don't know. But like to me that
[02:46] sounds pretty straightforward. Great.
[02:48] Then we'll do something called mask self
[02:50] attention or causal self attention.
[02:53] Either one of those basically means the
[02:54] same thing. They take those key query
[02:58] value uh matrices and then they do fun
[03:02] math. What does the fun math do? It does
[03:04] five things sequentially. Run. We
[03:07] multiply query and key creating what is
[03:10] effectively the key query circuit.
[03:12] What's a circuit? We're not going to
[03:14] learn that in this class, but that's the
[03:15] first of two circuits that we have here.
[03:19] Then we apply a causal mask. Why causal
[03:22] mask? Why do we need this thing? Is
[03:24] because when we train transformers, we
[03:27] wanted to only learn from the words that
[03:29] came before it, not the words that came
[03:30] after it. Why? The way we pre-train
[03:33] transformers is by having it predict the
[03:36] next token. If it knows the next token,
[03:38] it can't predict it. It's not really
[03:40] predicting. It could just cheat. Okay.
[03:42] So, I didn't understand that at all,
[03:44] Justin. Don't worry. We'll see it in
[03:45] Excel. The next thing it's going to do
[03:47] is we're going to divide by the root of
[03:49] the dimensions. Okay, that's fine. That
[03:51] kind of understandable that it lets us
[03:53] normalize these numbers a bit. Then,
[03:55] we'll apply softmax. Oh my goodness.
[03:58] Remember softmax from section 14?
[04:00] Revenge of the softmax. Here we come.
[04:03] We're going to use softmax inside of
[04:05] attention. That's why we learned how to
[04:07] do softmax and 2D matrices. If you
[04:10] haven't seen section 14 on softmax, this
[04:12] is a great time to go see it. Uh after
[04:16] that, that completes our Q circuit.
[04:21] Uh we're going to matrix multiply with
[04:23] value. So we're going to take this Q
[04:26] circuit and we're going to multiply it
[04:28] with V uh with the value matrix. So
[04:31] that's going to create something called
[04:32] the OV circuit. You don't have to
[04:34] remember the word circuit. You don't
[04:36] have to remember that. Maybe the useful
[04:37] thing to remember is there's really only
[04:39] two circuits in attention. What does
[04:42] query key value do? What do these
[04:44] circuits do? A little bit outside the
[04:46] scope of our of our slide deck here, but
[04:49] we are going to look at what attention
[04:51] does in a moment. Okay. Okay, so I
[04:53] taught you a little bit about the
[04:54] formulas. The last formula we have to do
[04:56] is I mentioned there's multiple
[04:58] attention heads. We have multiple query
[05:01] key values. What we actually are going
[05:03] to have is multiple heads of attention
[05:06] operating in parallel. And at the end,
[05:07] we're just going to concatenate them
[05:09] together. What is concatenate mean in
[05:11] this context? I don't know if you
[05:13] remember we did concatenating
[05:15] um uh residuals. Very similarly to that,
[05:18] we're that was section 11. very similar
[05:20] to that. We're going to just concatenate
[05:22] things together. What does concatenating
[05:24] mean here? We're just going to smudge
[05:26] them together. That's it. We're just
[05:28] going to put them side by side. And
[05:29] that's concatenation. Cool. Now, you we
[05:32] went over the formulas. Surely you
[05:34] understand them. Actually, there's no
[05:35] way you understood it from that
[05:36] explanation. Totally fine. I'm giving
[05:38] you a feel for the formula. We're going
[05:40] to see it in Excel in a moment. Great.
[05:43] So, let's look at an Excel demo. Before
[05:46] we do, I want you to have a look at the
[05:48] diagrams on the left. So scaled product
[05:50] attention this is from the um 2017 paper
[05:55] attention is all you need and you can
[05:57] kind of see the order of operations. We
[05:58] take K and Q, we math mole them, we
[06:01] scale them, we apply a mass, we do soft
[06:04] max, we do math mole, all of that good
[06:08] stuff, right? I personally don't find
[06:10] that diagram super representative of
[06:12] things that I understand. So my version
[06:15] of that diagram is the diagram on the
[06:17] left. GP uh JPT image 20 was kind enough
[06:21] to generate this for me. Um the first
[06:24] thing we do is we multiply. You can see
[06:26] it in the bottom. We take x input, we
[06:29] multiply it by the weights of the query,
[06:31] we get query. We take x input, we
[06:34] multiply by the weights of the key. We
[06:36] transpose it, we get query, we get key
[06:39] transposed. We multiply mat both of
[06:41] those together. We get the kqt like
[06:45] transposed k circuit. We square root the
[06:48] dimensions. We do division.
[06:52] We then apply a mask with addition.
[06:54] What's a mask? We'll learn in a second.
[06:56] We run that through softmax and then we
[06:59] calculate V. We probably calculated V a
[07:02] bit earlier. X multiply by the weights
[07:04] of V. We map all those together and we
[07:06] get the output. Okay, this is the second
[07:09] time we've seen the formula in action.
[07:11] This is starting to make more sense to
[07:12] me, but I can't say this makes a lot of
[07:14] sense to me. So, let's do that in Excel.
[07:17] Great. I'm going to make a copy
[07:20] file, make a copy, and we're going to
[07:23] work at the without answer sheet. just
[07:25] as a reminder or without answer sheet.
[07:28] Uh you do have the with answer sheets in
[07:30] case you want to refers to this later.
[07:33] So again here are all of the formulas
[07:35] for uh causal self attention. Not multi
[07:38] head attention but causal self
[07:39] attention. Don't worry we'll demonstrate
[07:41] e every one of these uh in turn in a
[07:44] moment. Great. So first thing we have to
[07:47] do is we have to calculate query. Let's
[07:49] say my input was 5x5
[07:52] and our
[07:54] uh uh inputs were 5x5. I actually had to
[07:58] downscale my inputs to a certain size.
[08:00] We'll learn about that I think in a
[08:02] later section. But for now, let's
[08:04] pretend my input was 5x5. That means my
[08:07] weight matrix learnable parameters for
[08:11] query is going to be 5x5 as well. All
[08:14] I'm going to do is I'm going to matt m
[08:16] it right. So my malt
[08:19] of the weight
[08:23] times the input.
[08:27] Great. So now I've calculated my query
[08:30] matrix. Great. What's the next thing I
[08:33] have to do? I have to calculate my key.
[08:35] Key is the weight of of key multiplied
[08:39] by the input. Again, we're just
[08:40] pretending that I'm not downscaling
[08:42] here. Here there will be a place where
[08:44] you are downscaling, but we'll see that
[08:45] really towards the end. So I'm going to
[08:47] multiply my
[08:49] weight of K by my input. Nothing special
[08:53] is happening so far. Just another matrix
[08:55] multiplication of the input multiplied
[08:58] by learnable weight matrix.
[09:01] Okay. So now we're kind of becoming old
[09:03] hats in this. We multiply the input by
[09:06] the weight of the value matrix or the V
[09:08] matrix. Let's mold the learn parameter
[09:12] matrix by the input matrix. Great. We
[09:17] just finished the first half of our
[09:19] formulas of calculating Q, K, and V.
[09:22] Now, we're going to plug that into the
[09:24] self attention formula. Let's do that.
[09:26] Uh before we do that, I want to show you
[09:29] that there's like a way for us to just
[09:31] do them kind of in unison. Why in
[09:33] unison? GPUs are massively paralyzed
[09:35] machines as we mentioned. So,
[09:37] realistically, we're going to probably
[09:39] do these parallelizable. But I also just
[09:41] wanted you to see that now we can kind
[09:43] of like put them side by side. Why am I
[09:45] really putting these side by side?
[09:47] Pretty soon you're going to see all of
[09:48] the tension side by side. I'm not going
[09:50] to break these into sections. But now
[09:52] you've seen taking one input, molting it
[09:55] with the weight, the learnable
[09:57] parameters for query, the learnable
[10:00] parameters for key, and the learnable
[10:02] parameters for value. Great. So we saw
[10:05] all that side by side. Next up, we have
[10:07] to do the
[10:09] QK circuit. So we'll do just what it
[10:12] says here. Soft max of Q with the
[10:16] transposed K divided by the the the root
[10:20] of the square root of the dimensions.
[10:22] First thing we have to do is we have to
[10:24] transpose K. Remember we saw transpose.
[10:26] We're learning a little bit of linear
[10:28] algebra when we're doing MLPS in section
[10:31] six. This is really the one time you
[10:33] have the second time you have to know
[10:34] transpose. First time was unembedding
[10:37] tide metrics. Second time is here for
[10:39] the attention uh transpose. Great. So I
[10:42] just transposed that. What does
[10:44] transpose means? It means I kind of
[10:46] flipped it over. This 2 O ended up at
[10:48] this corner. This O ended up at this
[10:51] corner. I kind of just flipped rows and
[10:53] columns. Great. Now I have to multiply
[10:57] uh the transposed key with the Q. So
[11:01] let's do that. malt
[11:05] multiply this with this really cool okay
[11:10] so I did that that's the top part of
[11:12] this expression now I have to divide it
[11:14] by the root of the the square root of
[11:16] the dimensions square root of the
[11:18] dimensions I have five dimensions square
[11:21] root of that I wrote that as power uh.5
[11:25] you could also write square five
[11:27] here we go same number great so I just
[11:30] need to divide each one of these by each
[11:33] one of these. I'm going to take this
[11:36] value and divide it by this value. And
[11:39] I'm going to just lock this really,
[11:40] really well. Great. I'm going to do that
[11:43] to all of these.
[11:46] And then the question is why are we
[11:48] doing that? One, it's kind of acting to
[11:50] like not increase the magnitude too
[11:53] much. Another thing to say about this is
[11:55] each one of these operations have had
[11:57] mountains of papers written about it.
[12:00] There's people who specialize their
[12:01] entire PhD on this one division, right?
[12:04] So, I'm not going to try and explain
[12:05] every one of these and its meaning, but
[12:07] we're just going to do the formulas here
[12:09] together. Okay? So, I divided that by
[12:12] the root of the d the square root of the
[12:14] dimensions. Next up, we'll have to do
[12:16] soft mix. I'm going to do softmax in
[12:19] like one line here. I'm not going to
[12:21] break it open like we did in section 14.
[12:23] It's the exponent divided by the sum
[12:26] product of all of the exponents of every
[12:28] one of the rows. Great. I'm going to
[12:30] lock the row. I'm going to lock the
[12:33] rows. What is up with this? Let's just
[12:35] copy this from with answer so you don't
[12:37] have to watch me debug this. Here we go.
[12:41] As these different lines 104 N 104 J
[12:45] 104.
[12:48] These are different lines. I think we
[12:50] this has to be J 106
[12:53] and N 106.
[12:57] Great. And then we'll move this to 106.
[13:00] Perfect. I'm going to spread that out
[13:02] over the entire row. Going to spread
[13:04] that down here. What did we learn? Every
[13:07] one of these rows sums up to 100. How do
[13:10] I know that? Because when we did softmax
[13:12] section 14, we learned about softmax of
[13:15] a 2D matrix. That's just all we're doing
[13:17] here. What did the soft mix do? Itreed
[13:20] the differences a tiny bit between the
[13:23] most reasonable, most likely values. So
[13:25] this 9.1 went from this much of the
[13:28] distribution to this much of the
[13:30] distribution. Much much uh uh uh
[13:34] difference uh it is a pretty meaningful
[13:36] difference of how much the magnitude is
[13:39] relative to the other items. Great. So
[13:42] we did that. We did softmax. We're just
[13:45] following the formula. I don't even know
[13:46] why the formula is the way that it is.
[13:48] Right? I who read papers from all the
[13:51] way from 2017. So next up, we have to do
[13:55] mask self attention. So what is mask
[13:58] self attention? We kind of did that
[13:59] here. Uh soft max, right? We did that
[14:03] for for masked attention, we add a mask
[14:06] here inside of the softmax. Okay, that
[14:09] seems pretty reasonable to me. What's a
[14:12] mask? The mask formula is listed here.
[14:14] For every value uh below like for every
[14:19] J and I if J is smaller than I the value
[14:22] is zero we add nothing. For every value
[14:24] where J is bigger than I you add a ma an
[14:27] infinitely negative number infinitely
[14:30] negative in the context of Google SL
[14:32] Google Google Sheets translates to minus
[14:34] 999. I'm not going to put massive
[14:35] numbers here but it's close enough for
[14:37] our like little math demonstration.
[14:41] So how do we add these together? pretty
[14:44] easy to tell. I'm going to take this
[14:46] number and I'm going to add this number
[14:49] to it. Great. So, that's the same
[14:52] number. This whole column is going to be
[14:54] the same. But as I drag this out, oh my
[14:58] goodness, all of these other numbers
[15:00] went super negative. What is the
[15:02] importance of them going super negative?
[15:05] Well, remember now we're going to softex
[15:07] them. They're going to be basically
[15:09] nothing, right? because we're doing
[15:11] exponents divided by the sum of the
[15:13] exponents, it's going to be basically
[15:14] nothing. So now I did that and we could
[15:17] see all of these negative super negative
[15:19] values just got zeroed out, right? Their
[15:22] values are so infantimally small that
[15:24] I'm going to have to add so many decimal
[15:26] places until we even see a number. It
[15:28] might take forever to see that. Not
[15:31] going to really happen. Uh, and also as
[15:33] I'm rendering these, like every time I'm
[15:35] clicking a button, it's recalculate like
[15:37] it's rerandomizing the page. Great. So
[15:42] that's what we did here. We could see
[15:43] softmax was applied uh within the the
[15:48] mask was applied within the soft mask
[15:50] function. Okay. So now we have to create
[15:53] our OV circuit. We already calculated
[15:55] softmax with everything inside, right?
[15:58] We could just pretend that we did that
[16:00] with a mask. Even though the formula
[16:02] doesn't show a mask, but let's pretend
[16:03] we just already did that. Now, we're
[16:06] going to like multiply these two
[16:08] together. How do you multiply these two
[16:10] things? Right? Math malt
[16:14] of V comes second. So, it'll be first
[16:18] here. The soft max.
[16:22] And here you go. What just happened?
[16:25] Some of these were already zero. So it's
[16:27] kind of hard to create something that's
[16:29] not zero from zero. But some of these
[16:31] actually did become not zeros. They got
[16:34] some magnitude in them. Okay. So that's
[16:36] it. I just created my OV circuit. I
[16:40] completed multiplying my soft whatever
[16:42] was inside my softmax with the value uh
[16:46] matrix. So let's do a complete causal
[16:49] self attention end to end. We'll try and
[16:51] put everything in one section so you
[16:53] could see it. I have my input of X
[16:56] that's going to go into my I have my
[16:59] learned weights of Q that's going to
[17:01] create Q here. So that's these two
[17:03] method together math malt together.
[17:07] I have my input of X and my learned
[17:09] weights of Q. So okay, so I'm going to
[17:12] like mim those together. Sometimes I say
[17:15] mac, sometimes I say mimalt. I've been
[17:17] working in Google Sheets way too often.
[17:21] Uh then I'm going to multiply the
[17:23] transpose of the K divided by the
[17:27] dimensions. You know, we could just do
[17:28] that in one go. There's no reason to
[17:31] split it up into multiple examples. So
[17:33] here I'm transposing K. I'm multiplying
[17:38] that transposed K with Q. Pretty
[17:41] obvious. And then I'm dividing it by the
[17:44] root by the square root of five.
[17:47] Great. After that we'll add this mask to
[17:50] it. So we'll add the mask and we'll do
[17:53] soft max. So we combine the outputs of k
[17:59] qt / d root square root of dt. We'll
[18:04] just add that inside of this expression
[18:07] here. And then we'll look at the
[18:09] exponent of that as well. And I
[18:12] pre-coded this ahead of time so you
[18:13] don't have to see me struggle with like
[18:15] arrays and dimensions and so on. And
[18:17] this is the result. Great. Now we did
[18:20] that. We have weight of V multiplied by
[18:24] the input. Right? So we're going to
[18:25] scroll all the way up here. We can see
[18:27] it's met M metalling the input with the
[18:30] weight.
[18:32] And then for self attention we multiply
[18:35] ma matrix multiply this expression with
[18:37] this expression V with the output of the
[18:41] uh Q circuit gives us the output of self
[18:46] attention or the OV circuit. Great. So
[18:49] now we math mold those together. That
[18:52] was causal self attention end to end in
[18:57] one section. You now know all of the
[18:59] math of one attention head of causal
[19:02] self attention in MHA. Great. So now we
[19:05] also said we're multi- head attention.
[19:07] We're not just at self-causal attention.
[19:10] We're multi-selfcausal attention. Okie
[19:13] dokie. So I've got my causal masks here
[19:17] in the side just kept for later because
[19:19] I'm going to need it. And I've got my
[19:20] inputs here. So now I have multiple
[19:23] heads of causal self attention running
[19:25] in parallel. So I have weight query
[19:29] weight query one. So I'm going to
[19:31] multiply that with my input. But I also
[19:35] have
[19:39] weight query 2 here. More learnable
[19:42] parameters for a totally different
[19:43] attention head. Okay. So I'm going to
[19:46] mold weight query 2 by the input.
[19:51] Very cool. So now I have two heads
[19:54] executing in likely parallel, maybe not
[19:57] exactly parallel. Maybe we're going to
[19:59] send these to the GPU as one matrix
[20:02] where if you kind of squint and I take
[20:05] away these two rows, I'm going to delete
[20:07] them because I'm an evil person. Can I
[20:09] can I delete these rows? Oh my god, it
[20:11] kind of looks like a matrix multiplying
[20:14] this matrix with this matrix. And that's
[20:17] actually how we end up implementing this
[20:19] in the GPU. We're never going to do
[20:20] these as separate operations, but for
[20:22] our purpose, we're just trying to learn
[20:24] the math.
[20:26] So, okay, we multiplied the learnable
[20:28] weights of Q1 and got Q1. We learn
[20:30] multiplied the learnable weights of Q2,
[20:32] we got Q2. We're going to do the same
[20:34] for K2 and K1. For V1 and V2, nothing
[20:39] special here. We're just doing more
[20:41] matrix multiplication between learnable
[20:42] weights and the input. Great. So, now
[20:44] every attention had has its own Q, K,
[20:47] and V. QKV1, QKV2.
[20:51] I'm gonna do the uh KQ circuit. QK
[20:56] circuit here. I'm gonna soft max it.
[20:59] Each one of these gets its own softmax.
[21:01] Every row is softmax with itself. And
[21:03] then I get causal self attention. Why?
[21:06] Because I also added the mask up here.
[21:09] So like this is the mask up that's
[21:12] learned up here. Great.
[21:15] So we did the softmax. We multiply that
[21:18] with the V and then we get every one of
[21:20] these causal self attention heads has
[21:23] its own unique output. How do we combine
[21:26] them? I'm going to have let's say two of
[21:28] these running in parallel. Let's say 12
[21:30] of these running in parallel. Let's say
[21:31] 48 of these running in parallel. How do
[21:33] we then combine them? I'm going to use
[21:36] the multi head uh uh equation formula
[21:41] and I'm going to concatenate them
[21:43] together. So I have self causal self
[21:45] attention head one cause of self
[21:47] attention head two causes self attention
[21:49] head three. Yeah. And I actually copied
[21:52] these from up here. So that's really
[21:53] cool. And let's say I have three. Let's
[21:55] say I only have three because that's
[21:57] what's going to fit reasonably in Google
[21:58] Sheets. But realistically we'll probably
[22:00] have two.
[22:02] And the way I concatenate them is I
[22:04] literally just copy them here. Right? So
[22:06] this this uh matrix got copied here.
[22:09] This matrix got copied here. this matrix
[22:12] get copied here. What's one problem
[22:14] we're going to have if we're going to
[22:16] concatenate 48 multiple attention heads
[22:19] together? That's a massive matrix that
[22:21] we're going to have to copy and in the
[22:23] next round we're going to 48 times that
[22:25] one and the next time we're going to 48
[22:27] that one again. If we do another set of
[22:29] transformer and another one and another,
[22:31] right? That's too much. We have to bring
[22:33] down the size back down to 5x5. If I
[22:36] have 15x5, how do I bring that down to
[22:39] 5x5? Remember, we learned that in uh
[22:42] linear algebra, 15 by five. This is 5 by
[22:46] 15. If I want to get to 5x5,
[22:50] I'm going to have to combine this with
[22:52] something that's 15 by 5. If these
[22:54] dimension, the last dimension here match
[22:58] with this first dimension here, this is
[23:00] going to end up at 5x5.
[23:03] Great. So now I have another learnable
[23:06] matrix of we call this W0. That just
[23:09] helps us bring Wo. That's just going to
[23:12] help W output the weight of the output.
[23:15] That's just going to help us bring this
[23:17] number down. Weight O not zero. So how
[23:21] do we do that? We matt the output.
[23:27] We matt the sorry we map these two
[23:30] matrices together. And I already have
[23:32] these up here to pre-written. No, I
[23:35] don't. So, I'm going to mult this matrix
[23:40] by this matrix and I'm going to get 15
[23:43] by 15. Not great. Oh my god, too big
[23:47] because they ended up being the same.
[23:49] So, I'm going to likely flip these.
[23:54] Great. And now it's 5x5. The two
[23:57] dimensions kind of match. So, I could do
[23:59] 15 x 15 or 5x5. I wanted to get 5x5.
[24:02] Great. So this is the output of multi
[24:05] head attention. What do you mean by just
[24:07] this is the output of multi head
[24:08] attention? Where does all the reasoning
[24:11] live? Where does all the thinking live?
[24:14] The sheet basically is going to end
[24:16] here. This is multi head attention.
[24:18] There's nothing else but but this math.
[24:21] Okay. So I will mention that we have
[24:24] multi head attention alternatives. One
[24:26] example of these alternative is called
[24:28] group query attention or GQA and
[24:30] multi-quorey attention MQA. Really the
[24:33] difference is is that we've decided that
[24:36] we can share the QVs
[24:38] uh between multiple attention head. So
[24:41] in here every in MHA every single head
[24:44] calculates its own QV or every attention
[24:48] calculates its own QV. We could actually
[24:51] decide that these QVs end up being
[24:53] shared between some of the attention
[24:55] head. How many? We'll wait to the slide
[24:57] to explain that. But let's see an
[24:59] example of sharing QV circuits. So I
[25:02] have a shared key that's shared between
[25:04] two separate attention heads. I'm going
[25:06] to still mat
[25:08] the
[25:10] shared key weights with the input.
[25:16] Great. I'm going to repeat that for the
[25:18] value.
[25:20] I was kind of hoping I could copy paste
[25:22] that, but looks like no.
[25:27] Multiply with the input. Now, I'm going
[25:30] to run the normal Q QK circuit that
[25:33] we've always run here. Great. Finally,
[25:39] I've got the Q Q circuits here. And then
[25:43] I'm going to calculate self attention
[25:45] the way that I normally do. The
[25:46] important thing is we share a key, we
[25:48] share a value between multiple attention
[25:51] heads. Very cool. So self attention head
[25:54] number one and number two both share the
[25:57] QV value. Why is that useful? We'll
[26:00] learn about that more when we get to the
[26:02] slide. What we really found out is we
[26:04] could save a lot of memory and a lot of
[26:07] compute and not lose a lot of
[26:08] performance if we share QV some of the
[26:12] time for some of the heads. Great. So
[26:15] now I want to talk about a little bit of
[26:17] magic that I did with you and I feel
[26:19] really bad for that is that I pretended
[26:22] that everything happens in 5x5.
[26:25] Realistically, we're not going to run
[26:27] these attention heads at the full hidden
[26:30] embedding dimension size. So let's say
[26:33] we're GPT2. We have 768
[26:37] hidden dimensions. Running every one of
[26:39] these attention heads at 768 dimensions
[26:42] going to be prohibitively expensive.
[26:44] We're going to run it at a down sampling
[26:46] of that. How much are we going to down
[26:48] sample? By convention, we're going to
[26:50] downscale by the number of concurrent
[26:54] multi heads of attention that we run. So
[26:56] for GPT2, we have 768 hidden dimensions.
[27:00] Remember, we learned that it's 16
[27:02] section 16 embeddings. We have 12
[27:04] attention heads. You just learned that.
[27:06] That's like the first time I've said
[27:09] that for real. GPT2 small runs 12
[27:12] attention heads in parallel. We're going
[27:13] to see them in a moment.
[27:16] So for GPT2, we're going to run 768
[27:20] divided by 12 heads. That's 16 heads.
[27:22] This sheets runs, let's say 10 full
[27:26] embedding size cuz I don't want to like
[27:28] explode this Google sheet. And we're
[27:30] only going to run two heads. How what's
[27:32] the dimension going to be? Remember,
[27:34] we're running 5x5. Let's do 10 divided
[27:37] by two. We're going to get five
[27:39] dimensions that we're going to run by.
[27:41] Okay. So let's say my embedding dimen my
[27:44] input is 10 x5 just by convention my
[27:49] actual size for Q for learnable
[27:52] parameters is going to be 5 by 10 what
[27:56] is it going to do that when we have five
[27:59] sorry 10 x 5 and f and here we have 5 by
[28:02] 10 remember because these match if we
[28:05] multiply them in the right order 5x 10
[28:09] input
[28:10] multiplied by query of 10 x 5. This is
[28:14] just linear algebra. We get a 5x5 out of
[28:16] that. That's just how downscaling works.
[28:19] So I kind of lied to you earlier. I'm so
[28:21] sorry. With qkv, I thought this is
[28:23] something worth leaving for the end.
[28:25] Similarly,
[28:26] we have another um weight query
[28:30] attention uh sorry weight query learned
[28:34] parameters. So I could do that again.
[28:36] And I'm going to mold the input
[28:40] right 5 by 10 with the learned weights.
[28:44] And actually this is a reverse because
[28:46] if I did that I'd get 10. Actually this
[28:48] is perfect. We'll get 5 by five here.
[28:51] Perfect. So this is what we wanted to
[28:53] learn. We wanted to learn that I kind of
[28:55] lied to you up here in these KQV
[28:57] circuits. Right? Remember we were
[28:59] multiplying all of these as if they were
[29:01] all 5x5. Actually the inputs are going
[29:04] to be a bit bigger. and the uh KQV are
[29:08] going to be a bit bigger. They're going
[29:10] to downsample the inputs. So, every head
[29:12] only works in a few dimensions. How many
[29:15] dimensions? The number of total
[29:17] dimensions divided by number of heads.
[29:20] Something worth knowing. This is like a
[29:22] little fun implementation detail. Okay.
[29:24] So now we saw everything in Excel.
[29:27] There's no magic you guys. There's
[29:29] nothing here dudes and dudetss. All we
[29:33] do is we just follow this attention math
[29:37] and magic happens.
[29:39] Let's look at attention types and then I
[29:41] think we're going to jump straight into
[29:43] what attention actually does cuz I think
[29:46] you've seen a bunch of math and you
[29:47] might be wondering where does all the
[29:49] reasoning live? Where does all the
[29:52] thinking live? So I just want to cover
[29:53] attention types before we move off this.
[29:56] We have MHA. That's the think that's
[29:58] this third column here. Every attention
[30:01] head of the 12 heads has its own QV uh
[30:05] matrixes. That's quite a lot. On the
[30:09] opposite side of that spectrum, we have
[30:11] MQA or multi-quorey attention. All of
[30:14] the attention heads are going to share a
[30:16] QV matrix both for the learnable
[30:19] parameters and then for the activations.
[30:22] Great. In between those is a kind of fun
[30:26] compromise. We have GQA. This is like
[30:28] one of the big breakthroughs of Deep
[30:30] Seek back early in 2025. As soon as they
[30:34] published it, the entire stock market
[30:36] dropped like 5 10 points the same day.
[30:39] Whatever I think seven points overall.
[30:42] Why did it do that? Cuz they figured out
[30:44] how to use shared key value pairs in
[30:48] such a way that needs a lot less memory
[30:50] and doesn't sacrifice any performance.
[30:53] They figured out that you could share
[30:54] KVS in a way that actually works really
[30:58] really well without sacrificing a lot of
[31:00] performance. And that was one of the big
[31:02] insights from DeepSync early 2025. So
[31:05] there's a trade-off here. The more key
[31:08] value heads you have, the better the
[31:10] performance, but it's worse on compute
[31:13] memory. The big secret from deepseek
[31:15] early 2025, I think it's sometime in Q1
[31:19] was that they found out that the
[31:20] trade-off is absolutely minimal. They
[31:23] think they got within two absolute uh
[31:26] percentages. So two percentage
[31:29] performance difference between sharing
[31:31] some of the KV circuits uh uh sorry KV
[31:36] heads between uh many of the um overall
[31:40] attention heads. We also have MLA which
[31:44] downsamples the value key with learnable
[31:46] parameters for all the heads which
[31:49] reduces the overall computation and
[31:51] memory. The secret is there's actually
[31:54] hundreds of type of attention at this
[31:56] point. I'm showing you four. We could be
[31:58] spending a whole day workshop on
[32:00] different types of alternate attention.
[32:03] I'm not going to go open that for you. I
[32:05] just wanted for you to sample a little
[32:07] bit that there are different
[32:09] alternatives to AMHA which is very
[32:11] memory intensive, very compute
[32:13] intensive, very not compute memory
[32:16] friendly and maybe doesn't have the best
[32:19] performance.
[32:21] Uh MHA by the way still used in every
[32:25] open source model at some level. So it's
[32:27] not like you're wasting time. Some of
[32:29] the layers will always have MHA. Cool.
[32:32] So let's move to a little bit of
[32:33] mechanistic interpretability. Justin,
[32:36] you showed us a bunch of math. The math
[32:37] makes no sense to me. How does this
[32:39] thing even reason? What does it do? So
[32:42] let's use our first metaphor from Welsh
[32:44] lab. Attention compares every single
[32:48] word with every other word that came
[32:50] before it. Right? Before it is the
[32:52] important part
[32:54] and then tries to understand something
[32:57] about the connection between the two
[32:58] words. So here we have this beautiful
[33:01] beautiful beautiful
[33:03] uh let's call it table or sheet from
[33:06] Welsh labs where they copy pasted or cut
[33:09] every word in Harry Potter and compared
[33:11] it with every other word in Harry
[33:13] Potter. Right? That is what attention
[33:15] does. It just compares every word with
[33:18] every other word. That's what the math
[33:20] we just saw earlier doing. Great. One
[33:24] really key insight right now. Harry
[33:25] Potter's kind of a long book, right?
[33:29] What we learn from that is attention
[33:31] with its quadratic nature. Every word is
[33:34] O of N power two when we have to
[33:36] multiply them. That's actually kind of a
[33:38] lot. That's the why I think in in
[33:42] essence we haven't seen context sizes in
[33:45] commercial products above a million
[33:47] because that's kind of hard to do if
[33:50] you're multip if you have to give every
[33:52] other if every word has to check its
[33:54] attention with every word that came
[33:56] before it. But that's not what we're
[33:58] here for. We're here to develop an
[33:59] intuition of with attention. So we're
[34:02] comparing an attention every word with
[34:04] every word that came before it. What
[34:06] does that even mean? So we're going to
[34:08] look at bird viz and we'll do that in a
[34:11] moment.
[34:13] Bird viz visualizes every one of our
[34:16] heads. One thing we now know is we have
[34:18] 12 attention head. One thing I didn't
[34:21] teach you so far is that we have
[34:22] multiple layers of attention. We'll
[34:25] spend more time on layers of attention
[34:27] in the next section, but I kind of want
[34:29] you to look at these lines. I kind of
[34:31] want you to stare at them with me
[34:33] together. Every one of the attention
[34:36] heads has a slightly different pattern
[34:38] to every other attention head
[34:40] potentially on the same layer, right?
[34:42] So, if you look at this layer zero, head
[34:46] one, all of the lines are kind of
[34:48] straight. Whereas if you look at head
[34:51] zero and like layer zero, everyone kind
[34:54] of points to this first item. But if you
[34:57] look at learn seven, all of the lines
[34:59] are kind of zigzaggy up and down Z. What
[35:02] does that mean? Let's try and interpret
[35:04] them together in a moment. So this
[35:06] visualization comes from bird viz. You
[35:08] could also generate your own vis
[35:10] visualization, which we will do, but
[35:12] bird viz is just like the easiest tool
[35:14] to use for that. Great. So we're going
[35:17] to focus in on these three attention
[35:20] heads that are all kind of copied
[35:21] together and then we're going to try and
[35:23] interpret them in the next slide. So
[35:25] what did we learn from these? Let's look
[35:28] at layer zero and head one with the
[35:30] sentence when Mary and John went to the
[35:33] store John gave a drink to Mary. This is
[35:36] this is a very famous sentence in
[35:38] mechanistic interpability. I'm not
[35:40] necessarily going to explain why this
[35:42] has something to do with u II and so on.
[35:46] Uh great. So what did attention uh head
[35:49] layer 01 short 0 comma one learned? It
[35:54] learned to identify words that are
[35:56] repeating. No one taught the attention
[35:59] head to do that. You saw all the math
[36:01] with me. You saw the attention math. You
[36:03] saw back propagation. It learned that
[36:06] when the word Mary repeats itself, it
[36:09] should really have the word attend to
[36:11] every previous repetition of that word.
[36:14] The word to repeats itself. It has to
[36:16] look at the previous word. The uh word
[36:19] John repeats itself. It looks at the
[36:20] previous word of John. Amazing. No one
[36:25] taught the attention head to do it. It
[36:27] just learned to find previous
[36:29] occurrences of the same word. What a
[36:33] mind trip. Unbelievable that it was able
[36:36] to do that. Okay. So, what did 07 find?
[36:41] Layer seven, head no layer zero at head
[36:44] seven. What did it learn? It learn to
[36:47] find the previous word. Why is that
[36:49] important? Remember we learned about
[36:51] this in positional encoding. The
[36:53] embedding space doesn't have position in
[36:56] the beginning. We have to add positions
[36:58] on top of that. This is proof that the
[37:01] head learned previous tokens. That means
[37:05] it actually knows positions wild.
[37:10] So the word Mary points to two. Two
[37:13] points to drink. Drink points to ah. Ah
[37:15] points to gave. Gave points to John. And
[37:17] so on and so forth. What a trip. No one
[37:22] taught an attention head how to do
[37:25] previous word lookups. It just learned
[37:28] that because it needed to as part of its
[37:31] pre-training. But there's nothing in
[37:32] pre-training that says you have to learn
[37:34] previous words. There's nothing in
[37:36] pre-training that says you have to learn
[37:38] to find repeating words. Okay, so layer
[37:41] zero is where really simple patterns
[37:43] happen. Let's maybe look into p like
[37:45] layer 2. Layer 2 we said in lingua map
[37:48] and when we were doing like ensemble.
[37:50] What's ensemble? We have layers and
[37:53] heads kind of collaborating together.
[37:56] It learned how punctuation works. It
[38:00] learned how to divide sentences. So you
[38:02] could see every single word in layer 2
[38:05] head six attends to the comma that
[38:09] separates sentences or attends to the
[38:12] beginning of the sentence. It learned
[38:14] how punctuation marks separate p
[38:17] sentence fragments. Wild. No one taught
[38:20] it that. It didn't like we didn't do
[38:23] anything to try and teach it the rules
[38:26] of the English language. We just showed
[38:28] it a bunch of English, did a bunch of
[38:29] math with attention and a bunch of
[38:32] propagation, and it just learned this
[38:34] pattern. We can interpret it by looking
[38:37] at it and kind of guess what it does.
[38:39] Get that gets a lot harder the further
[38:42] you look into the network. Layer 11,
[38:44] head 8, has a lot of these words and
[38:48] like takes all these patterns from all
[38:50] of these layers and connects them into
[38:53] something that's not really super human
[38:55] understandable anymore, right? Mary
[38:58] looks at the word drink. The word John
[39:01] looks at John. That makes sense. What's
[39:04] another strong connection? When looks at
[39:06] when dot looks at dot, it learned like
[39:09] punctuation marks. Wild. There's a
[39:11] pattern here that's going to help it do
[39:13] next to token selection. This head is
[39:16] maybe one of the most relevant ones for
[39:18] this sentence. Great. So, we learned
[39:21] relevancy in such a way that only a
[39:24] highdimensional alien intelligence can
[39:26] fully understand.
[39:29] Okay. So, highdimensional alien
[39:31] intelligences. Super cool. Justin,
[39:34] thanks for teaching me about that. That
[39:36] doesn't make any sense to me. Let's look
[39:38] at Neuronedia. Neuropedia takes a bunch
[39:42] of these activations in different heads
[39:44] in different layers in different head
[39:48] number in different layer numbers and
[39:50] tries to correlate those calls them
[39:52] features tries to correlate them into
[39:56] next token selection. Why did the large
[40:00] language model when it said when we
[40:02] asked it the capital of Texas is it
[40:04] autocompleted with Austin? Why did it do
[40:07] that? It activated features for uh the
[40:13] uh city names, for Texas, for say which
[40:18] and for capital cities. It found a bunch
[40:20] of features inside the network. A bunch
[40:22] of attention heads that within them had
[40:25] a pattern that correlates to capital
[40:29] cities for Texas for say which and for
[40:36] uh uh Texas capital city say which which
[40:39] caused Austin to fire. Let's look at
[40:41] Neuropedia for a moment. This Neuropedia
[40:44] is a scope for a really small model. Uh
[40:48] it's for quen 3 1.7b. Not an oftenus
[40:51] model. It's considered a small language
[40:53] model. But here you could see each one
[40:56] of these rows is a layer. It has 26
[40:59] layers of attention. How many are we
[41:01] going to have? Less than that.
[41:04] And you could see here each of the
[41:05] different attention heads is a is a
[41:08] column. And then oh my goodness,
[41:12] every one of these is like this feature
[41:15] is capital cities. This feature is place
[41:18] names. This feature is say names. This
[41:21] city is capital cities. This one is
[41:24] Texas. Again, we also have the say
[41:27] which. Here we go. What or say which.
[41:30] When we combine all of those together,
[41:33] we get it. The probabilities for Austin
[41:36] being 36%.
[41:38] Wild. the attention, learned all of
[41:41] these features, combined them together,
[41:44] and helped generate the next token
[41:45] prediction. This is as close to
[41:47] mechanistic interpability as we're going
[41:49] to get in this one uh workshop, but I
[41:53] really think it's important to tie the
[41:55] the the full loop between fun attention
[41:59] map something with back propagation
[42:02] attention heads each learn to do a roll,
[42:05] right? Each layer has a role. These
[42:07] roles are connected to like features,
[42:10] whatever features are, and then together
[42:12] they bring us back into next token
[42:14] prediction. Wild. No one taught the
[42:18] network how to do anything with English.
[42:21] We just taught it fun like attention
[42:23] math. We put a bunch of these together
[42:26] with back propagation and showed it
[42:28] English and it learned how the English
[42:30] language functions.
[42:32] Very cool. So now let's look at a little
[42:35] bit of code. We're going to see how
[42:37] causal self attention is implemented
[42:39] with math. We'll see how to build it in
[42:41] PyTorch as a module. We'll do a little
[42:44] bit of the mechanistic interpability we
[42:46] saw here ourselves. Then we'll use
[42:48] birdfizz and then I'll give you two
[42:50] exercises.
[42:51] Great. So the first thing we're going to
[42:53] do is we're going to take our math that
[42:55] we saw earlier and we're going to use it
[42:57] here.
[43:01] Causal self attention from scratch. We
[43:04] have a bunch of uh of the four
[43:06] dimensions that we taught we were taught
[43:09] in section 16. We have the bat size, the
[43:13] sequence length, the embedding size, and
[43:15] the head dimension. And the head
[43:17] dimension here because we have just one
[43:18] head is going to be equal to the
[43:20] dimension of the model. Great. So, we
[43:23] saw this massive I'm going to just flip
[43:25] it on the screen one more time. We saw
[43:28] all of these formulas. We're just going
[43:30] to implement these in code in PyTorch.
[43:32] So first we'll have a bunch of inputs.
[43:34] I'm just going to randomize some values
[43:36] so we could run math here. Then we're
[43:39] going to project them down from the
[43:41] embedding size to the hand dimension. So
[43:43] we're going to create another set of
[43:45] like weights for Q, K, and V. So another
[43:48] set of randomly generated numbers, but
[43:51] importantly going from the embedding
[43:53] size to the head dimension size. Then
[43:55] we're going to calculate Q KV. We're
[43:58] just going to matt mole the input with
[44:00] the weight of the query with the weight
[44:02] of the key with the weight of the value.
[44:06] So that's this first set of formulas we
[44:08] saw here and we saw in Excel together.
[44:10] Next we're going to do mask self
[44:12] attention.
[44:14] Right? So I'm going to have the
[44:16] scale.products.
[44:18] Then I'm going to create a torch tree.
[44:21] That just creates that fun like triangle
[44:23] shape in a in a in a matrix. So that
[44:27] just gives me that infinitely negative
[44:30] uh causal mask. I'm going to add that to
[44:33] my scores,
[44:36] right? Then I'm going to softax. Like we
[44:38] said, we're going to soft max. And
[44:40] finally, I'm going to multiply that by
[44:42] the value matrix. So again, all we're
[44:45] doing here is following this formula.
[44:48] And if we had multiple attention heads,
[44:50] this is the point where we would
[44:51] concatenate them and then down sample
[44:53] them with the weight output. Great. So,
[44:56] here's a bunch of fun dimensions. You
[44:58] get to kind of like inspect these. I
[45:00] hate personally looking at dimensions.
[45:02] It's kind of hard for me. But maybe the
[45:04] one thing that's kind of interpretable
[45:06] is this. This is what um the masked
[45:10] causal attention looks like before we
[45:12] replace it with negatively infinite
[45:13] numbers. Great. And this is the final
[45:16] output of attention weights. Does that
[45:18] make any sense to anyone when we follow
[45:20] that? Probably not. I still like
[45:22] visualizing things like we do in Excel.
[45:24] So here's my input values. Here are my
[45:27] learn Q KV learnable parameters. Here's
[45:32] multiplying the inputs with those
[45:34] learnable parameters. So we're in
[45:35] activation space right now. Here are the
[45:38] mask scores. So we've now applied a
[45:41] causal mask to Q multiply math mode by
[45:45] the transposed K and then I added
[45:48] masking to that. And here are the final
[45:50] attention weights after soft max.
[45:53] Finally, after softmax, we're going to
[45:55] apply the math mole with the value. And
[45:58] these is what we got. What did it do
[46:02] here? My goodness, we just followed the
[46:04] math. So again, this is the same thing
[46:06] we did in Excel. I could take all that
[46:09] math and just throw it inside of an NN
[46:11] PyTorch module. Right? So again, I'm
[46:15] just having a bunch of N and linear
[46:17] embedding size to head dimension. No
[46:20] biases, by the way, inside of attention.
[46:22] We just don't use biases. It's something
[46:24] that we maybe keep in MLPS, but we
[46:27] definitely don't do in attention heads
[46:28] anymore. So I have a bunch of weight
[46:32] query key value.
[46:36] We again use torch tree to get that fun
[46:39] triangle of zeros and ones. And then
[46:41] when we do the forward pass on each of
[46:43] these, we first calculate the query, the
[46:47] key, the value. I kind of told you that
[46:49] we're going to concatenate them and send
[46:51] them off to the GPU. all at once. That's
[46:53] more of a runtime kind of like GPU
[46:55] inference optimization that I don't want
[46:58] to do right now with you.
[47:00] Uh but then we'll calculate the scores.
[47:02] We'll apply the mask. We'll do soft max.
[47:06] We'll multiply attention weights by
[47:10] the weight the value and then we'll
[47:13] return that as output. Very cool. If I
[47:16] had multi head attention multiple 12
[47:19] heads running together, I'll have n
[47:22] heads uh a dimension, then I'm going to
[47:25] mult take my embedding size and multi
[47:27] divide by how many n heads I have. So
[47:29] now my head dimension is going to be
[47:31] smaller than my total embedding size cuz
[47:33] I want each head to specialize on some
[47:36] of these.
[47:37] I'm going to have a module list, we've
[47:40] already seen these, of however many
[47:42] heads I need. So the number of heads
[47:44] with causal self attention. Causal self
[47:46] attention is this head.
[47:49] Great. And then I'm going to do a
[47:51] downward projection for the a downscale
[47:54] of with a weight output. When I do a
[47:57] forward pass, I'm going to run each one
[48:00] of these uh heads with the input. So I'm
[48:02] going to run each head with the input.
[48:04] Then I'm going to concatenate them
[48:06] again.
[48:08] Then I'm stacking these together. And
[48:10] then I'm going to multiply that by my
[48:13] weight output matrix. Nothing we haven't
[48:15] seen before. So how do I run that? I say
[48:17] I have four heads, right? My embedding
[48:20] size didn't really change. I think I set
[48:22] it to like eight or something in the
[48:24] beginning. Yeah. So eight. So every one
[48:26] of these is just going to have a
[48:27] dimension of two. Not a super
[48:29] meaningfully complex head here. Tiny
[48:32] even.
[48:34] I'm going to create a random input and
[48:37] that's my mha. So, I'm going to take the
[48:39] input, run it through the MHA, it runs
[48:41] it to each of the heads. Each of the
[48:43] head does QV, does the transpose, does
[48:46] the masking, does the softmax, does the
[48:49] multiply by V. Nothing really
[48:51] interesting happened here. You you guys
[48:54] dudes and dudetss, this is all the math
[48:57] that we have to make uh attention work.
[49:00] This is roughly it from this and back
[49:03] propagation and showing it the entirety
[49:04] of the English language. It learns all
[49:06] those patterns we saw earlier. What are
[49:08] those patterns? Well, we can write our
[49:10] own visualizer. I'm going to re run this
[49:13] visualizer on GPT2. So, I'm going to
[49:15] load in GPT2, the tokenizer, the model.
[49:18] I'm also going to tell it that I wanted
[49:20] to output attentions cuz we kind of like
[49:22] maybe want to investigate them a bit
[49:24] more. Right? I don't want just the
[49:26] result of ma. I want the results of each
[49:28] of individual attention head cuz
[49:30] otherwise it's going to be hard to
[49:31] investigate it.
[49:33] I'm going to give it the prompt when
[49:34] Mary and John went to the store, John
[49:36] gave Mary a drink. And then I'm going to
[49:39] have it like generate the tokens. This
[49:42] little fungy symbol is just a space. Uh
[49:45] visualize interesting attention head. So
[49:48] remember 01 07 26 118. That's what we
[49:51] saw in the slides. I can have you don't
[49:53] have to see the code. I can visualize
[49:55] this myself. Quite a lot of not fun code
[49:58] to write. Also not super interactive.
[50:00] Kind of not super clickable. So let's
[50:03] try and use uh a bird viz to do these.
[50:06] But another way to visualize this and
[50:07] you're going to see this a lot and I
[50:09] personally can't easily read this. This
[50:12] is a lot less reasonable readable to me
[50:14] and interpretable to me than this
[50:15] diagram. But another way of showing this
[50:17] diagram is like this. So every attent
[50:20] every word attends to every previous
[50:22] word. It almost always attends to itself
[50:25] a lot. But you could see the patterns
[50:27] here very wildly different. So one of
[50:30] these always attends to itself and
[50:32] attends to a few other words. These are
[50:34] the repeating words head. This attends
[50:38] to uh every previous word. So you could
[50:41] see it really really tries to attend to
[50:43] every previous word. Here head number 26
[50:47] attends to the piece the sentence
[50:50] fragment beginning. And this head has
[50:53] like a relevancy that's super important
[50:55] that helps determine the next token
[50:57] prediction. Cool. So at least you could
[50:59] see each one of these is a radically
[51:01] different pattern. You don't have to
[51:03] learn to read this chart. You could just
[51:05] learn to see, oh my goodness, every one
[51:07] of these charts is really different.
[51:09] Let's use bird vis to do this. So
[51:11] instead of me writing all of this
[51:13] visualization code myself, I'm going to
[51:15] use the bird vis library. I'm going to
[51:18] pull in a head view and I'm going to
[51:20] say, hey, if you don't mind, can you
[51:22] just do a model view for me? So I could
[51:24] head view a single view model view for
[51:26] the entire model
[51:29] and here you get to see the entire
[51:31] attention patterns of every head in
[51:34] every layer. Great. So if I click the 01
[51:37] layer I could see this is the head that
[51:40] learned to attend to every pre to every
[51:42] repeating word. So went looks at went
[51:45] but also drink looks at drink here. Uh
[51:48] John looks at the previous John as well.
[51:51] Very cool. Uh and head sorry that was uh
[51:54] supposed to be head 01. So head 01 looks
[51:57] at repeating words. So John looks at
[51:59] John. Mary looks at Mary. Uh store looks
[52:02] just at store. Two looks at the previous
[52:05] instance of two. It learned to find
[52:07] previous words. 07 learn to look at
[52:11] previous word. Very very noticeable that
[52:14] it's looking for previous words to me.
[52:17] Great. So that's using bird viz to do
[52:19] that visualization. Now, we learned
[52:22] about all the formulas. We learned about
[52:24] the code. I would like to give you an
[52:26] exercise, and I was really struggling
[52:28] with which exercise to give you. And I
[52:31] think it's now that you know how to
[52:32] implement MHA,
[52:34] I would love for you to try and
[52:36] implement MQA. MQA, every single
[52:40] attention head shares the same QV.
[52:43] That's it. That's all we would like to
[52:45] do. If you could just share the same QV
[52:47] across all the same attention heads, you
[52:49] can have MQA, right? I just duplicated
[52:53] this and I was like, hey, I'm just going
[52:55] to try and do that. I duplicated that
[52:57] notebook. I wrote a little bit of code
[52:59] here to have duplicated QV that just
[53:03] like ends up having the same QV across
[53:06] all of the heads. Another exercise you
[53:09] could do is once you have MQA up and
[53:12] running which shares all the QVs you
[53:14] could try and get JQA up which let's say
[53:17] shares um if you need if you have three
[53:19] if you have four heads let's say they
[53:22] share QV between a few heads but not all
[53:25] the heads how many let's say you have
[53:27] four total heads try and create QV
[53:30] shared between two heads a total of two
[53:32] shared QVs so that's another fun
[53:35] exercise you could do I think that one
[53:37] really helps make like memory and
[53:39] compute and all of that good stuff land
[53:41] for us.
[53:43] So, let's make a couple of decisions. I
[53:45] actually love this chart from Michael.
[53:47] I'm going to butcher his name. Brand
[53:50] doer.
[53:53] Um he summarized the the various sizes,
[53:58] the various hyperparameters for GPT2. By
[54:01] the way, he has a great set of books
[54:04] that you can read and kind of learn
[54:05] along with how uh every one of the large
[54:08] language model concept is built. But he
[54:11] has this great chart that shows hidden
[54:14] size. We talked about it. That's the
[54:16] size of the embedding. GPT2 small 768.
[54:20] We already made that decision. Uh we
[54:22] learned that our vocabulary size is
[54:25] 50,257.
[54:27] Actually, we're gonna like make sure
[54:28] it's a multiplication of 26 of 64. Our
[54:32] context length is,024,
[54:34] a very small paragraph. Parameters,
[54:38] overall parameters, that's just the
[54:39] multiplication of a bunch of stuff, but
[54:41] we've already kind of made that
[54:42] decision. What else did we already
[54:45] decide? Feed forward size, 768
[54:48] multiplied by four. That's our MLP
[54:51] growing, shrinking. We remember that.
[54:53] That's section six. So, we already made
[54:55] that decision.
[54:57] head dimension. Uh, so like sorry,
[55:00] number of attention heads. We just made
[55:02] the decision. We're going to have 12
[55:03] attention heads working in parallel.
[55:06] Each of them trying to specialize on
[55:07] something. One's going to learn previous
[55:09] word. One's going to learn repeating
[55:11] word. Another one's going to learn
[55:12] sentence fragments.
[55:15] Attention uh uh head dimension size.
[55:18] We're going to take the total hidden
[55:20] size divided by the number of attention
[55:23] heads. That's going to keep the math and
[55:25] compute memory requirements pretty
[55:28] small. And then we're going to have uh
[55:30] 64. So that's 768 divided by 12. So our
[55:34] head dimension size is going to be 64.
[55:36] We also made the decision we're going to
[55:38] have 12 attention heads here because
[55:39] we're just trying to recreate GPT2
[55:41] small. And finally, we need to choose
[55:44] our attention architecture for our small
[55:47] GPT2 small recreation. We're going to
[55:49] try and do multi head causal attention.
[55:51] You could also try and use GQA. You can
[55:54] also try to do um the other attention uh
[55:58] types that we've learned about. So by
[56:00] now we understand every single thing in
[56:03] this chart besides something called
[56:05] layers. What's layers? It's just the
[56:07] number of transformers repeating
[56:10] themselves. What's a transformer? Great
[56:13] question. That's going to be our next
[56:15] section. Before we move on to our next
[56:17] section of what's a transformer,
[56:20] I'd like to recommend a few guides if
[56:22] you're really really interested in
[56:23] attention uh and this really spiked your
[56:26] interest. So, one I'm going to recommend
[56:28] the three brown one uh three blue one
[56:31] brown playlist where they just show you
[56:33] the same math I just showed you over and
[56:35] over again. If seeing in an animated
[56:37] form helps you, go ahead and watch this
[56:40] video or maybe the whole playlist. I
[56:42] think it's phenomenal visualization.
[56:44] Super fun to watch. Also, if you like
[56:46] visualizations, I adore Welsh Labs. I
[56:50] specifically adore not just their
[56:52] videos, but their physical book that
[56:54] kind of teaches a lot of this visually.
[56:56] I'm going to go to the shelf now and do
[56:59] this thing where the background becomes
[57:00] real. Oh my goodness, it's a real book.
[57:04] What's on the cover? It's the lost
[57:06] landscape that we were learning about in
[57:08] section seven. Even if you go to section
[57:11] 8, you could see that it has an
[57:13] attention head in it as well. So really
[57:16] fun to learn about visualizing all of
[57:19] the stuff that we were learning about. I
[57:21] really strongly recommend this book.
[57:23] It's so visual. I love it. Great. So
[57:26] what's going to be the next thing we
[57:28] learn about? We're going to learn about
[57:29] transformers. In transformers, we're
[57:32] actually not going to learn a lot of new
[57:35] stuff almost at all because we already
[57:37] know everything that's inside of a
[57:39] transformer. So, that's actually just
[57:40] going to be a rehearsal for us. We're
[57:43] not going to really learn any new
[57:45] concepts. The secret sauce of
[57:47] transformers is that they're just the
[57:49] composition of all the 17 other things
[57:52] that we've covered thus far. We've
[57:55] basically broken apart transformers to
[57:57] all the components. We learned them
[57:58] together. Section 18 is going to just be
[58:00] composing them together. So, I hope to
[58:02] see you when we get to section 18. It's
[58:05] going to be a whirlwind tour of learning
[58:07] about the transformer architecture with
[58:09] all the tools we already have, but most
[58:12] importantly, how we can take ourselves
[58:14] out of 2019, which is where GP2 GPT2 is,
[58:18] all the way to 2025 and maybe even 2026.
[58:21] So, I hope to see you soon when we do
[58:24] that. See you soon.
