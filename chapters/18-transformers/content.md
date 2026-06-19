# Transformers | Build Your Own LLM Workshop #18

**Build Your Own LLM Workshop — Video #18 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 53m 52s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=mKAW7cYYwQs |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to our
[00:03] section on transformers. We're here in
[00:06] our build your own LLM workshop. We've
[00:09] spent 17 sections thus far learning how
[00:13] to use large language models and they
[00:15] emit probabilities. We learn how to
[00:16] train machine learning models using
[00:18] neural nets, perceptrons, multi-layered
[00:20] perceptrons, loss functions, back
[00:23] propagations, activation functions. We
[00:26] then went ahead and learned a lot about
[00:28] deep neural networks and how to build
[00:30] large language models. We learned about
[00:32] residual connections. We learned about
[00:34] initializ random initializations. We
[00:37] learned about regularization
[00:39] normalization. Finally, we got to some
[00:42] language concepts. We learned about
[00:43] tokenizations and embeddings. And now
[00:45] we're here together in the real
[00:47] culmination of all of this. This one
[00:49] section on transformers is going to pull
[00:51] all of that together. And now we're
[00:53] going to really finish off our
[00:55] architecture for GPT2 style
[00:57] transformers. This is a very exciting
[01:00] section for us because we are going to
[01:02] be complete with architecture at the end
[01:04] of it. So as always, if you need code,
[01:06] the code we're going to be writing, it's
[01:08] availing
[01:12] some time on. Our deliverable from this
[01:15] section is going to be transformers and
[01:17] we're going to learn how to work with
[01:18] GPT2 inference. Great. Let's get
[01:22] started. So, we're going to jump
[01:23] straight into an Excel demo. If this is
[01:26] where you're joining the workshop, this
[01:27] is a real bad spot or maybe it's a great
[01:29] spot because we're not going to really
[01:31] do any work alone. We're just going to
[01:33] see how we stitch everything we've done
[01:36] so far together into a transformer
[01:38] architecture. So, I'm going to go ahead
[01:40] and open this Excel spreadsheet. And
[01:42] maybe before I do, I kind of maybe want
[01:44] to get you familiar with how
[01:45] architecture diagrams work. So if you
[01:47] look on the right, you could see JPT2
[01:50] 2019 architect architecture. Uh this is
[01:53] for small I believe and then you could
[01:56] see that there's like a flow of events
[01:58] and we'll go over that more. We start
[02:00] off at the bottom and when we get some
[02:02] sample input text and we uh get end at
[02:06] the top where we have our auto
[02:07] reggressive token generation. So let's
[02:09] maybe just numerically try and
[02:11] understand what's going on here. Let's
[02:13] do a quick lay of the land before we
[02:15] jump into Excel. So we start off first
[02:18] thing we do is we tokenize the text. We
[02:19] can see that in the bottom. So that
[02:21] we're going to need to tokenize. That's
[02:22] going to be the first thing we do. The
[02:24] next thing we're going to have to do is
[02:25] token embedding layer. Okay, great. We
[02:27] are going to have to run our embedding
[02:28] layer. After that, we'll need positional
[02:30] embedding layer. So again, we'll do
[02:32] positional embedding. After that, we'll
[02:34] do a dropout. Right? We're just
[02:35] recreating the GPT2 architecture. We
[02:38] have no strong opinions about it right
[02:39] now. After that, we're going to uh uh
[02:42] have 12 transformer blocks. What's a
[02:45] transformer block? This is the time
[02:47] where we answer that question. It's a
[02:48] thing that repeats itself how many
[02:50] times? 12 times within our network.
[02:53] Great. So, what is inside of a
[02:55] transformer block? We start off with our
[02:57] first pre-layorm. Then we move on to a
[03:00] multi head attention. Then we move on to
[03:03] a dropout. We then have a residual
[03:05] connection. You can see the residual
[03:06] connection is from prelayorm all the way
[03:08] to after dropout. Then we run our second
[03:12] layer. We have a feed for network or an
[03:16] MLP. What's are in our MLP? We have our
[03:19] first linear layer. It's going to grow
[03:21] for X. We have our activation function.
[03:23] In this case, it's RLU for us. ReLU
[03:25] squared. Then we're going to have our
[03:28] second linear layer, our second uh
[03:30] matrix, and it's going to shrink down.
[03:33] After that, we'll do dropout again.
[03:35] After that, we'll do a residual
[03:37] connection. And then we'll repeat this
[03:38] transformer block a total of 12 times.
[03:40] So that's 11 times more after we're done
[03:44] with repeating this transformer block 12
[03:46] times.
[03:47] We'll do a final layer. We'll have our
[03:50] linear output layer. So that's going to
[03:53] be an unmbedding metrics. Uh we'll
[03:56] detokenize. So we'll decode the
[04:00] tokenizers. And finally uh we'll have
[04:03] our output token in a as a string. This
[04:06] is not meant to teach you anything. This
[04:08] is just meant to give you the lay of the
[04:09] land. Great. But we've learned all of
[04:12] these concepts. That's the really most
[04:14] important thing here. Let's jump into
[04:16] the transformer uh Google sheet. So,
[04:19] first thing we see here is we have the
[04:21] exact same diagram we just saw. And our
[04:23] role and our job here during this Excel
[04:26] spreadsheet is to just follow this one
[04:29] point at a time. Again, all of these are
[04:30] things we've already seen in previous
[04:32] sections. So, the first thing we're
[04:34] going to do is we're going to start off
[04:35] with tokenized text. You can see here
[04:37] I've cropped out. This is amazing. This
[04:39] is like so intuitive. Like we've got
[04:42] like the step we're in highlighted in
[04:44] red. So the first thing we have to do is
[04:46] we're going to have to tokenize some
[04:47] text. So we have the brown fox, the
[04:50] brown dog jumped over the lazy fox. Here
[04:52] we have our entire tokenizer with its
[04:55] 52,000
[04:56] uh tokenized wards. And I'm just going
[04:59] to go ahead and translate my input to
[05:01] tokenized input. Right? So that's just
[05:03] going to take a string to an int. We saw
[05:05] that during section 15 when we were
[05:07] talking about tokenizers. We just
[05:10] happened to be so lucky that our
[05:11] sentence is in the first set of tokens.
[05:13] Why? Because I'm lazy and I didn't want
[05:15] to like randomize these numbers. Great.
[05:18] So now I've have my input sentence. I've
[05:20] tokenized it. Strings go to ints.
[05:23] After that we have our embedding metrics
[05:26] that has every single token that's
[05:27] supported in a highdimensional space.
[05:30] Right? So now we're toking embedding
[05:32] layers. How many high dimensions? 768
[05:34] for GPT2 small and a vocabulary size of
[05:38] 52,000.
[05:39] Great. So I'm going to take this
[05:42] dictionary and combine it with this
[05:44] input and then that's going to give me
[05:46] the embedding input layer. So I combine
[05:49] the embedding matrix with the with the
[05:51] tokenized input and created the
[05:52] embedding input matrix. Awesome. How big
[05:55] is this matrix? It's going to have the
[05:57] same number of columns as our hidden
[05:59] dimensions. And then it's going to be
[06:00] the con the number of rows that is the
[06:03] context size. And we'll just pad that
[06:05] with an end of string or padding uh uh
[06:08] token uh for anything that we're not
[06:10] using. Great. So now I've combined it
[06:13] input tokens with the embedding metrics
[06:15] and created my embedding input matrix.
[06:18] Next step says I have to do positional
[06:20] embedding layers. If this was truly GPT2
[06:23] style, I would have a bunch of learned
[06:25] weights here. I'm not going to do that.
[06:28] No one does that anymore. There's no
[06:29] reason to do that again. We could use uh
[06:32] some absolute. So that was absolute
[06:35] learned position encoding instead of
[06:37] that. I'm going to do sinosodal absolute
[06:41] positional encoding. How does that work?
[06:43] So let's say that this was my input uh
[06:45] embedding metrics combining the tokens
[06:48] and the embeddings. On top of that, I'm
[06:50] going to calculate the positional
[06:51] embedding. This is a separate matrix,
[06:54] right? Remember it does a thing with
[06:56] sinuses and cosine, even or odd. It
[06:58] builds these beautiful wave patterns
[07:00] with something may or may not be a 4year
[07:03] transform. I don't know, right? And then
[07:06] how do I combine these? I'm just going
[07:08] to add these together. So array formula
[07:10] just means I've got like a bunch of like
[07:12] an output outside of one cell. And I'm
[07:14] going to combine this array with this
[07:17] array by just doing peace-wise addition.
[07:19] Great. So that was positional encoding.
[07:22] Nothing we haven't seen. We actually
[07:23] spent a lot of time on this when we were
[07:25] in section 16. So we talked about
[07:27] section 15 in tokenizing se section 16's
[07:30] embedding section 16 in positional
[07:33] encodings. Great. After that what the
[07:36] chart tells us we have to do the road
[07:38] map is that we have to do a dropout.
[07:40] What's a dropout? We covered this in
[07:42] section 13. A 10% loss rate. I'm going
[07:44] to create a 10% dropout rate. I'm going
[07:47] to create this input mask. Could be
[07:49] totally randomized to another set of
[07:50] inputs. And I'm just going to take this
[07:54] uh metrics that had our positional
[07:56] encoding on top of our input embedding
[07:58] metrics and I'm I'm going to apply that
[08:01] on top. How do I do that? Actually,
[08:03] pretty simple. I'm just going to do
[08:05] pie-wise multiplication. This is not
[08:06] matrix multiplication. Meaning, every
[08:08] time it sees a one, it's going to just
[08:11] uh not change that number. Every time it
[08:13] sees a zero, it's going to zero that
[08:15] out. So, I do some amount of dropout for
[08:17] these uh inputs. Great. So now we start
[08:21] our transformers. Oh my god, big big
[08:23] title. Transformer begins. Why is that
[08:26] important to highlight where that
[08:27] boundary is? We're going to repeat this
[08:29] 12 times total, right? 11 more times
[08:31] after we do this first run. So what do
[08:33] we have to do to build our GPT2 style
[08:36] transformer? We're going to build our
[08:39] layer because it says I have to do a
[08:41] layorm. Okay, great. How do you do layer
[08:43] norm? I don't know if you remember when
[08:44] we were in section I believe that was
[08:46] section 11 or section 12 when we did
[08:49] normalization. We had like a very simple
[08:51] formula to do like a single line layer
[08:53] normalization. That's all we're seeing
[08:56] here right now. So I took this array
[08:58] that had all the drop this matrix that
[09:01] had all the dropper and then I layer
[09:03] normalize these here. What does layer
[09:05] normalization do? It scales and it
[09:07] centers. That's all we're doing here.
[09:11] Great. On top of that, now we go into
[09:13] multi head attention. That's what it
[09:15] tells me that comes after the first pre
[09:17] layer. I'm gonna uh have our inputs at 5
[09:21] by five. I do want to highlight that
[09:24] it's probably going to be much bigger
[09:25] than 5x5. How much bigger? Probably 12
[09:28] times bigger. So, it's going to be five
[09:30] * 12. So, that would be 60. Let's say 60
[09:34] rows. Uh sorry, like we said, 10,024
[09:38] rows each representing each potential
[09:41] input token. And then I'm going to have
[09:43] 768 columns representing my hidden
[09:45] dimensions. And then each of the heads
[09:47] will only have 64 columns. They'll down
[09:51] sample just because there's no room in
[09:52] the Google sheet. For demo purposes,
[09:55] we'll pretend everything is 5x5. But I
[09:57] did want to highlight that course. So
[09:59] for demo purposes, my inputs 5x5. Each
[10:02] of my QV weights are 5x5. Each attention
[10:06] had it has its own QV. We're just doing
[10:09] multi head attention. We're not creating
[10:11] shared KVs. So we're not at GQA or any
[10:15] of the other uh more more fancy
[10:17] attention mechanisms. So based on these
[10:20] learned uh parameters or weights, I'm
[10:23] going to matt the input with the weight
[10:26] with the learned query key value
[10:30] weights. So every one of these is going
[10:32] to get multiplied. Every one of these is
[10:33] going to be different even though we're
[10:35] multiplying with the same input because
[10:37] each of these learn different
[10:38] parameters. Great. Then I'm going to do
[10:41] scaling and then dotproduct.
[10:45] This is stuff that we've seen before.
[10:46] I'm going to I'm going to transpose the
[10:50] the key matrix. I'm going to multip
[10:53] multiply that matte that with the query
[10:55] matrix. And then I'm going to scale by
[10:57] the number of dimensions. Nothing we
[10:59] haven't covered in the previous section
[11:00] on attention section 17 each. And then
[11:03] I'm going to soft max. And finally I'm
[11:05] going to have the output after I
[11:06] multiply that with the value matrix.
[11:09] Okay. Okay. So each had has its own
[11:12] number of attention head has its own
[11:15] each attention has it has its own
[11:16] output. We're going to concatenate them
[11:18] together. Let's pretend that there were
[11:20] 12 of these. I just didn't want to make
[11:21] this sheet like infinitely width long.
[11:24] But so let's pretend there's like nine
[11:26] more of these here. How do I take this
[11:29] massively wide kind of number of columns
[11:32] and then downscale it to something that
[11:33] we can use? The way that I'm going to do
[11:35] that is I'm going to have a weight
[11:37] output matrix weight output and that's
[11:40] going to shrink this massive uh
[11:42] concatenated matrix back to an MHA final
[11:46] output. And that's roughly it. That's
[11:48] just doing attention like we learned in
[11:50] section 17. After that, I have to do
[11:52] dropout again. Okay, now we're at 5x5.
[11:55] So, let's just stay at 5x5. I think
[11:57] that's fine. We apply another dropout
[11:59] mask and we drop out more stuff. Great.
[12:02] Now, I was told I have to do a residual
[12:03] connection.
[12:05] So, uh here I've got my pre-layer norm
[12:09] input, right? So, I just copied this
[12:12] over. I didn't really do a lot with it.
[12:14] Uh where does that come from? If I
[12:16] scroll all the way up, all the way up,
[12:19] all the way up, we can kind of see that
[12:21] this is where it comes from. My
[12:22] prelayorm uh input. Great. So, now I
[12:26] know where that comes from. Row 128 27.
[12:29] So that's the input and I can add that
[12:32] with a residual. So I'm going to take my
[12:35] pre- residual my my residual that
[12:38] happened long before this
[12:41] and I'm going to add it to the result of
[12:43] the dropout. Great. So now I've done
[12:46] both of that and then I'm going to have
[12:49] to do another prelayorm. So I'm going to
[12:51] layerm this again as I'm supposed to and
[12:54] then and then we move on to the feed 4
[12:57] network. What's in the feed 4 network?
[12:59] There's one growing layer, an activation
[13:00] function, ru probably, and then a
[13:03] shrinking function. So, in order to do
[13:05] growing, we learned this in section six
[13:07] on MLPS. We're going to just multiply
[13:10] that by four times the number of
[13:12] dimensions. Why do we do that? It gives
[13:15] it a scratch pad. It's a place to learn
[13:16] new knowledge. It's really fun and
[13:18] great. Great. Now, after I did that,
[13:23] uh, now I have that 4x. So I have this
[13:26] 4x learned uh learnable parameters and
[13:30] I'm going to take the output of the
[13:32] layer norm and I'm going to 4x that
[13:34] here. So these are my activations and
[13:36] these are my learned weights. Finally
[13:38] I'm going to do a galoo. I apparently
[13:41] decided to use galoo here not relu.
[13:43] That's totally fine. It's a complicated
[13:45] formula. Here we go. And in order to do
[13:47] galoo I just ran this like cell by cell
[13:50] and then we ran the galoo function here.
[13:53] Awesome. After we did that, we're going
[13:55] to do shrinking. How do we shrink? We
[13:57] take this matrix that is bigger but uh
[14:01] than our input but still going to help
[14:04] us shrink down the activate the post
[14:07] activation function activation. And then
[14:09] we're going to shrink this to 4x down.
[14:12] Great. So we did that. All of that we
[14:14] learned saw in section six. After that,
[14:16] what happens then? We'll do another
[14:18] dropout. So many dropouts. We're doing
[14:20] so many dropouts. Great. Right. So we
[14:23] did another drop out, right? Because
[14:25] this we're just following the diagram.
[14:26] It just tells us what to do. Then we're
[14:28] going to uh finally have to do another
[14:30] residual. The pre layer layer norm
[14:33] input. We scroll up. That's row 250 to
[14:36] 254.
[14:37] So that is precisely after we added the
[14:40] previous residual. Why are we taking the
[14:43] the spot where we added the previous
[14:44] residual? Cuz we always want to keep the
[14:47] residual stream untainted by the things
[14:49] that are happening inside these blocks.
[14:51] We just want the additions that are
[14:52] happening there. So, we're going to do
[14:54] another residual addition. We're going
[14:56] to add that to the results of the
[14:58] dropout. How do I do that? Just normal
[15:00] addition. This is like just residual
[15:03] addition. We learned about that I think
[15:04] in section 11.
[15:06] And uh so on. So now we got to the end
[15:10] of our transformer block. The way we
[15:11] know that is it says transformer block
[15:13] and ended in big in big bold titled
[15:17] letters. But now we go to the part of
[15:20] the chart that says you have to repeat
[15:21] it a total of 12 times. So instead of
[15:23] copying this transformer block 12 times
[15:25] for you, I'm just going to go
[15:26] transformer block 1 2 3 4 5 6 7 8 9 12.
[15:30] We did we repeated the transformer block
[15:32] 12 times.
[15:34] The architecture diagram says we need to
[15:36] have final pre layer. So we're going to
[15:38] do that right here. Layer one more time.
[15:41] Then I'm going to do an unmbed matrix.
[15:44] Where's the unmbeding matrix come from?
[15:45] Remember we had our embedding metrics
[15:48] and unmbedding is just uh uh in our case
[15:52] because it's tight embeddings it's just
[15:54] flipped to our embedding metrics. It's
[15:56] just transposed to our embedding matrix.
[15:58] I'm going to take the out output of the
[16:01] final layer. I'm going to met that with
[16:04] the unmbeding matrix and then I'm going
[16:07] to get my uh output for for this part of
[16:11] the transformer for this for this part
[16:13] of the large language model. Finally,
[16:16] we're done with a transformer. We're
[16:17] done with a large language model. It's
[16:19] time to do a little bit of sampling. I'm
[16:21] going to use soft max here, right? We
[16:24] said we're going to soft max before we
[16:26] can read the logits. What are logits?
[16:28] The final activations like we just stop
[16:31] running the network at some point and
[16:32] then we call it logits. At that point,
[16:35] we apply softmax to the logits. As did
[16:38] fox dog, you r the highest probability
[16:42] probably belongs to like one of these.
[16:44] Let's try and read that again. We do
[16:46] softmax to this like last final row.
[16:49] Let's see if I can add more here. Here
[16:50] we go. Dog has the highest probability.
[16:53] I didn't really update the final uh the
[16:56] final uh section after that. But let's
[16:58] pretend that just means we chose dog
[16:59] because that's what softmix told us to
[17:01] do. And I couldn't resist by teaching
[17:04] you one more concept. I know I'm like an
[17:07] awful person. This is ARG max. So let's
[17:10] say we didn't want to do any of the
[17:12] sampling that we were talking about
[17:14] before. Temperature, top K, top top P.
[17:17] What is all of that from section one?
[17:19] Why would we repeat it so far into the
[17:21] game? So instead, I'm going to teach you
[17:22] ARG max. Argax chooses the result with
[17:26] the highest number. So here in our case,
[17:29] it's section uh it's um uh it's the
[17:32] result in token 4.5A
[17:35] token ID4. For some reason, I just
[17:37] decided to hardcode the word 'the' and
[17:39] not choose it here. Great. So, I chose
[17:41] the highest result, argues
[17:51] in this Google sheet, Justin, I I was
[17:54] told there'll be exercises for each
[17:56] section because transformers are on
[17:57] magic. We've learned all these concepts
[17:59] before. You've done uh every one of the
[18:02] sections between sections 1 and 17. The
[18:05] the payoff here is you don't have to
[18:07] learn new concepts when you learn about
[18:08] transformers. Transformers and large
[18:10] language models based on them. Just
[18:12] combine all of the concepts we've seen
[18:14] before. It's semant all the way down.
[18:17] Right? We're running a training loop
[18:19] with back propagation. So it's going to
[18:21] do like a training loop over all the
[18:23] epics or the data or whatever. And it's
[18:26] going to be matt all the way down and
[18:28] then also kind of like all the way up
[18:29] because we're running back propagation.
[18:32] You've literally seen every component of
[18:34] GPT2 at this point. You you you know
[18:37] every single section of the architecture
[18:39] of GPT2. Great. So now we saw the Excel
[18:43] demo. You know all of these sections.
[18:45] You've seen all of these things. Let's
[18:47] try and do this one more time. Try and
[18:49] have a visual demo of transformers. I
[18:52] love the transformer explained demo
[18:54] here. So you can click this link. It'll
[18:57] take you to this demo.
[18:59] And then let's try and visualize
[19:01] everything we just saw but maybe with
[19:02] like slightly realer numbers than random
[19:05] values. So the nice thing about this
[19:06] demo is it loads in real values from
[19:08] GPT2 small you know it's GPT2 small one
[19:11] because the documentation tells us that
[19:13] and two it doesn't know a lot in terms
[19:15] of knowledge. It can't even autocomplete
[19:17] the capital of Texas is it's not that
[19:19] great at that. So I give it the sentence
[19:22] building your own language model is and
[19:24] then it shows easy. I guess it feels a
[19:27] bit condescending but okay. So what's
[19:30] the first thing we do when we do an
[19:32] embedding metrics? Uh we are going to
[19:35] first convert our strings to token ids.
[19:38] So here are the token ids that we've
[19:40] been working with this whole time. This
[19:41] is GPT2 tokenizer or tick token. On top
[19:44] of that we'll add positional encoding
[19:46] because this is GPT2. These are learn
[19:48] embeddings. But again remember we
[19:51] converted our token our string to an
[19:53] int. Then we convert that to a vector of
[19:56] 768 dimensions. Why 768? That's the
[20:00] number of high dimensions that GPT2
[20:02] small thinks in. Finally, we'll add our
[20:05] learn positional embedding. If we were
[20:07] coding this ourselves, it would probably
[20:08] be cinosodal absolute position
[20:10] embeddings. Finally, uh we're going to
[20:15] uh do dropout. We're going to do layer
[20:18] normalization. So, dropout, layer
[20:20] normalization. Nothing super fancy here.
[20:22] We've talked about those. And then
[20:24] finally, we get into our attentions.
[20:27] Great. What does attention look like?
[20:30] So, we're going to calculate our QV
[20:32] weights. And here, they've kind of like
[20:34] mushed them together, which I kind of
[20:36] told you is what's going to happen in
[20:39] GPT2. There's also QKV bias. Not
[20:42] something we're necessarily going to do
[20:43] in any transformer that's built after
[20:46] GPT2, but worth knowing that. And then
[20:49] we are going to have a result of our
[20:50] KQV. Let's look at that a tiny bit more
[20:54] intensely. So we are going to have our
[20:56] input, we have our like learn parameters
[20:59] for K, Q, V, right? So we have the input
[21:02] vectors and we have the learned
[21:04] parameters. So we're going to calculate
[21:06] the key metrics, the query metrics, the
[21:09] value metrics and then we're going to
[21:11] run multi head attention. What does that
[21:13] look like if you kind of like let it
[21:14] breathe a bit more? So first we do a dot
[21:17] product between key and query. We scale,
[21:19] we mask. What the scaling and masking
[21:21] mean? Scaling means that we divide by
[21:24] the square root of the dimension. Then
[21:27] we're going to like mask. So like
[21:29] everything that every token that comes
[21:31] after a token is going to be zero. And
[21:33] finally, we're going to soft max. Right?
[21:37] After we finish that circuit, we're
[21:39] going to uh multiply that by value
[21:42] creating the OV circuit. So again, we
[21:45] calculate the value matrix. And notice
[21:47] we are the vectors of 64. Y 64. Every
[21:50] attention head runs at the hidden
[21:53] dimension 768 divided by the number of
[21:55] the attention heads. 12 attention heads.
[21:58] 768 divided by 12 64. We saw that when
[22:02] we were in section 17. Great. So now we
[22:06] said we have multiple attention heads.
[22:08] How many attention heads we have? We
[22:10] have 12 attention heads. 1 2 3 4. What's
[22:15] cool about this is we know how to read
[22:18] these charts now. We kind of understand
[22:20] what each attention head here does. So,
[22:23] if we look around, maybe we'll find
[22:25] something really cool, right? So, like
[22:27] there's not a lot of self attention here
[22:29] because there's not a lot of repeating
[22:30] words, but maybe we know this attention
[22:33] head looks at the beginning of the
[22:34] sentence. That tells us something that
[22:36] it might know a little bit about
[22:37] sentence structure. So on and so forth.
[22:40] Maybe one of these knows a little bit
[22:41] about previous words. kind of hard to
[22:43] tell, but you can kind of see each one
[22:46] of these attention heads learned a
[22:47] different pattern during back
[22:48] propagation. Course, so now there's 12
[22:50] of these. What's the last thing that
[22:52] happens?
[22:54] We're going to have our final vector.
[22:56] There's going to be another dropout.
[22:57] Maybe there'll be uh the MLP. The MLP,
[23:00] unfortunately, is not super well
[23:02] detailed here. It's growing. Activation
[23:05] function shrinking. Very cool. Maybe
[23:08] another layer in there. But most
[23:10] importantly, after we're done with like
[23:12] uh attention, there's going to be a
[23:14] residual. What's a residual? It jumps to
[23:17] before we ran the entire portion of the
[23:19] attention block, and it's going to add
[23:21] that result back in using just normal
[23:23] peace-wise addition.
[23:26] Then we're going to do that again for
[23:27] our residual for our um for our MLP. So
[23:32] on and so forth. So we have residual
[23:34] connections. Here we go. Is there even
[23:37] perfectly? It even says that the
[23:38] activation function is gaou. Very cool.
[23:41] So growing, you can kind of see that
[23:43] like the size of the vector grew from
[23:45] 768 to 3,72.
[23:48] So that's 4x growing. Then it ran gaou
[23:51] and then it shrunk back in again. What
[23:53] if happens if I click this? Here we go.
[23:55] So you could see it's got expanded
[23:57] embeddings and a compression weights and
[23:59] then compression bias. Here in the MLP,
[24:01] we might still have bias depending on
[24:03] our architecture choices. Great. So,
[24:06] we've talked about how MLPS work.
[24:07] Growing, shrinking, growing, shrinking,
[24:09] like an activation function in between.
[24:11] Then, we're going to be done with that.
[24:13] We're going to residual one more time.
[24:14] And then we're going to repeat the
[24:15] transformer block 12 more times. Going
[24:18] to click it just a few times. I'm not
[24:20] going to click it 12 times, but you can
[24:21] see each of these attention heads in
[24:23] here. Each of these has 12 attention
[24:24] heads. Learn this different pattern.
[24:27] Great. So, we three more identical
[24:29] transformer blocks. Actually, let's just
[24:31] click it all the way through. Finally,
[24:34] we have the last residual, the final
[24:36] layer norm, and we've arrived here at
[24:40] choosing which of these parameters uh
[24:42] which of these output logs happen. So,
[24:44] the output logs, I kind of lied to you.
[24:46] I told you we're trying to keep
[24:47] everything between minus4 and four we
[24:49] do. The more the smarter the model, the
[24:52] more learned parameters it has, the more
[24:54] compute, the more data, the closer they
[24:56] end up being to -4 range. Unfortunately,
[24:58] GPT2 small is just too naive for that.
[25:01] It has a lot of values at like this
[25:03] range of like it's 4% output logs and
[25:07] like 4.8 point output logs tend to exist
[25:10] in like the negative range happens.
[25:12] Nothing I could do about that. Cool. So
[25:14] now I have my output logits. We're going
[25:16] to scale those like we learned because
[25:18] we're doing a softmax, right? So softmax
[25:20] just scales based on the exponents. You
[25:22] can see we calculate the exponents for
[25:24] each and then we divide based on the sum
[25:26] of all the exponents. Uh finally
[25:30] we'll run a top k top p because I've
[25:33] said top p top top k here. Great. So
[25:35] that was our demo for uh how
[25:37] transformers work. Let's look at a
[25:39] little bit of code. So we're going to
[25:41] have a few examples. We're going to have
[25:42] gpt22 from scratch using just math. Then
[25:46] we'll have fully utilizing PyTorch. So
[25:48] the first example won't utilize
[25:49] PyTorches almost at all. Then we're
[25:51] going to load some ways for smoke text.
[25:53] And then I'm going to have give you an
[25:54] exercise uh that we'll chat about when
[25:57] we get to it.
[26:00] Great. So now we're GPT2 small from
[26:03] scratch. This we have our
[26:06] hyperparameters here. The vocabulary
[26:07] size, the context size, the hidden
[26:09] dimensions, the number of the heads, the
[26:11] number of the layers, the feed forward
[26:12] dimension. We said we're going to 4x it,
[26:14] and the dropout rate. I'm still going to
[26:16] have drop out here. Okay. So first thing
[26:18] I'm going to have is uh scratch token
[26:20] and position embedding. I called
[26:22] everything here scratch for from
[26:24] scratch. Uh so we have our token
[26:26] embedding array, our positional
[26:28] embedding array. Looks like I'm still
[26:30] doing like uh uh uh learned embeddings
[26:34] here. Uh dropout. Great. We're just
[26:37] implementing GPT2. Then I do a feed
[26:39] forward. I get the token IDs. I embed
[26:42] them inside of the input uh embeddings.
[26:45] I get their positions and I do
[26:47] positional embedding based on that. And
[26:49] I finally apply a dropout. We're just
[26:51] following the GP22 diagram. Lar
[26:53] normalization. We said we have to do
[26:55] layer normalization. We're doing
[26:56] everything with math. So we're going to
[26:58] have the layer normalization math we've
[27:01] seen before. We calculate the mean. We
[27:02] calculate the variance. We do division
[27:04] based on the square root and a small
[27:05] epsilon. All of this is stuff we've seen
[27:07] in section 12. Finally, we add a bias
[27:10] and we keep going. Glue activation. My
[27:12] god, now we're seeing glue again. Maybe
[27:15] this is the point where you realize from
[27:16] section five on GPU performance. This
[27:19] this whole sheet kind of lies to you.
[27:22] You're seeing me write Python CPU code.
[27:24] My gosh, this is going to be very not
[27:26] performant. But at least it's kind of
[27:28] readable. Okay, so we have our GLU
[27:31] activation. Now we have causal multi
[27:33] head attention. Remember causal multi
[27:35] head attention. We're going to have a
[27:37] head dimension. We're going to have
[27:39] query key value projections. This is for
[27:42] like one attention head, I believe. No,
[27:44] this is for multiple attention heads.
[27:47] And then we have our uh uh trio for like
[27:51] a little causal mask.
[27:54] Then we have feed forward. We calculate
[27:56] the queries, the keys, the values.
[27:58] Notice that maybe this is a little bit
[28:00] effective because it's combining a lot
[28:02] of these key query heads together.
[28:06] Uh finally, we have our attention
[28:08] weights, our attention scores, so on so
[28:10] forth. We're just doing the math we saw
[28:12] in section 17. Scratch feed forward.
[28:15] What did we say our MLP feed forward
[28:18] network has? It's going to expand or
[28:21] upscale or uh grow. Either one of those
[28:24] is the correct terminology. Then it's
[28:25] going to contract in the middle. It's
[28:27] going to have an activation function and
[28:29] finally a dropout. A activation function
[28:31] of galoo and contraction and then
[28:34] finally dropout. Great. Now I have a
[28:36] transformer block. How do we build a
[28:38] transformer block? First layer norm
[28:40] attention. second layer norm feed
[28:43] forward network we're going to execute
[28:45] those as is and don't forget residual
[28:47] connection plus x plus x we're not going
[28:50] to forget about doing residual
[28:51] connections finally gpt2 model we have
[28:54] embedding transformer block right so
[28:57] we're going to have 12 transformer block
[28:59] the number of the layers final layer
[29:01] norm unmbbedding and then uh we're going
[29:04] to uh take that from somewhere else feed
[29:07] forward so on so 12 transformer blocks
[29:10] final layer norm embedding. Great. Then
[29:14] we're going to try and do a feed forward
[29:15] pass. A feed forward pass on a totally
[29:17] untrained random model. It's going to be
[29:19] nothing but nonsense, but at least we
[29:21] could see the dimension. So, how many
[29:23] total parameters did we end up with? 124
[29:25] million. Perfect. That is what we were
[29:28] looking for.
[29:30] And then uh we can uh try and do a feed
[29:32] forward path. We'll bring in 16 uh 16
[29:36] tokens. and then we'll get 16 tokens as
[29:39] the output for the embeddings. Now we if
[29:42] we had time we'll run soft max and then
[29:44] we'll run top K and all of that stuff
[29:46] all of the sampling options. Okay, so
[29:48] that's not really how you implement
[29:49] anything cuz all of that was CPU code
[29:51] but it was at least very readable. So
[29:53] now we're probably going to start using
[29:54] PyTorch. So same amount of like uh
[29:57] hyperparameters.
[29:59] Then we'll create a multi head attention
[30:01] block right we're going to register our
[30:04] cause of attention. We're going to do
[30:06] another feed forward layer. We're going
[30:08] to start using all of the NN stuff that
[30:10] we should be using. So multi head
[30:12] attention is already in NN. We don't
[30:14] have to reimplement MHA from scratch.
[30:17] Feed forward. We said we're going to do
[30:19] growing shr activation function
[30:21] shrinking dropout. Great. We're just
[30:23] going to run it through this NN
[30:24] sequential network. We don't even have
[30:26] to do it one at a time. Transformer
[30:28] block again. First layer norm attention
[30:31] second layer norm feed forward. Great.
[30:34] So that's using all the attention mha
[30:36] that was already built into PyTorch.
[30:39] Finally, we'll pull all that together to
[30:40] a model to a GPT2 style model and we'll
[30:43] do another feed forward pass. You can
[30:44] see there's a lot less code here. Why?
[30:46] Cuz we're using a lot of stuff that's
[30:47] built in. We can use N and embedding. We
[30:49] can use N and L layer norm. We don't
[30:50] have to code it ourselves. We could use
[30:54] uh our MHA. So a lot less code overall.
[30:57] But now we know what's behind that code.
[30:59] This code for example will be some
[31:02] somewhat GPU performance because at
[31:04] least it's going to run on the GPU. Uh
[31:06] if I said to GPU here in this code which
[31:09] I didn't still it could run on the GPU.
[31:12] It could run at the GPU which is good.
[31:14] Finally, one thing we could do is we
[31:17] could try and load our uh pre-trained
[31:19] GPT2 weights. This is really heavily
[31:21] inspired by Sebastian Rashka's uh build
[31:25] your own LLM from scratch book because
[31:26] he just showed that you can load
[31:28] transformer TensorFlow weights into
[31:31] PyTorch. That was really cool to see in
[31:33] his book. So this code just does that.
[31:35] You don't have to learn how to load
[31:37] trans TensorFlow GPT2 weights into GPT2
[31:41] lookalike uh uh in PyTorch. So just like
[31:45] let's assume that it does that. So we
[31:47] have our from scratch GPT. We load the
[31:50] pre-trained weights. We then and we put
[31:51] it into eval mode. Eval mode just means
[31:53] we're not training it. And then we could
[31:55] try and generate some text. The meaning
[31:58] of life is not the same as the meaning
[32:00] of death. Very, very cool. We coded up
[32:04] this entire transformer architecture.
[32:07] We loaded in the weights that are
[32:09] available for GPT2. Then we were able to
[32:11] generate a prompt. Very cool. And then
[32:13] we could try and verify that against the
[32:15] existing GPT2 hugging phase and try and
[32:18] run the exact same prompt and see what
[32:20] the distance is between the logits. It's
[32:22] actually very very small. It's a very
[32:24] small number of difference that or that
[32:27] happens because transformers aren't 100%
[32:29] deterministic even if you run them in
[32:31] temperature zero. There's a lot of
[32:32] research on this topic but generally
[32:34] there'll be a small difference even if
[32:35] you run in the same network. So the
[32:37] difference is so small we know that
[32:38] everything worked as expected. Great. So
[32:41] that was our from scratch transformer
[32:43] implementation.
[32:45] Let's try and change that. So as your
[32:47] exercise, prompt your favorite AI coding
[32:50] assistant. Modify the attached notebook
[32:52] to avoid coding from scratch and compare
[32:54] syntax using some of the off-the-shelf
[32:56] components from one corpathy's nano GPT.
[33:00] So that's an implementation of GPT2 from
[33:03] scratch.
[33:04] Another option is using X transformers,
[33:08] right? That's another uh open- source
[33:10] implementation of a lot of these
[33:11] components and another options we use to
[33:14] torch tune from meta and then fourth
[33:15] option from lit GPT from lightning. All
[33:18] of these are just open source
[33:19] implementations of the components and of
[33:21] the transformer architecture that we've
[33:23] seen so far. If you want to see an
[33:25] example of that, right like that's
[33:28] available here. I didn't fully review
[33:30] this but I think it's going to be pretty
[33:31] good. So if you want to see an
[33:33] implementation from PyTorch that's still
[33:35] here but nano GPT kind of
[33:36] implementations here. If you wanted to
[33:39] see X transformers that's also available
[33:42] here. So the the code reads a bit
[33:43] different but now you can read this okay
[33:46] transformer wrapper. Very cool. You can
[33:47] notice there's not a lot here because
[33:49] all of the implementations already
[33:50] available within these libraries torch
[33:53] tune from meta. I this is highly
[33:55] performant. I love this. Why? If you
[33:58] remember very early on in our first
[34:00] first first section, I ran um I ran uh a
[34:06] GP22 training and I one took 8 hours,
[34:09] one took 20 hours. It's because it used
[34:11] torch tune. So highly optimized
[34:13] implementation cuts back on a lot of
[34:16] time. So torch tune l GPT from lightning
[34:19] AI so on again we this is a very small
[34:22] implementation. It just created the
[34:24] config put that into a GPT2. Bam, here
[34:27] we go. Everything is implemented for us.
[34:30] We don't have to write a lot of code.
[34:31] So, really fun. And then finally, we had
[34:33] some architecture diagrams here because
[34:35] I didn't want you to like leave without
[34:37] any fun architecture diagram. So, you
[34:39] could kind of see how each of these
[34:40] works. Finally, we have our uh
[34:43] pre-trained GPT two ways. We can load
[34:46] them into these models and we can verify
[34:48] against hugging face. The meaning of
[34:50] life is not the same as the meaning of
[34:51] death. Very, very cool. So, that's your
[34:54] exercise. Try and do this prompt
[34:56] yourself. Try and say, "Hey, can you use
[34:59] like another framework that's maybe not
[35:01] coding math by hand on the CPU? Maybe
[35:05] it's not just using PyTorch. Maybe try
[35:06] and use the plethora of frameworks that
[35:08] are available. Feel free to find a fifth
[35:10] one. Another option is you can hey
[35:12] actually can you go implement this in
[35:14] CUDA? Can you go implement this in
[35:17] another PL in another framework? Can you
[35:19] use PyTorch compile? Can you run uh uh
[35:22] some sort of performance test? Lots of
[35:25] options for you for LLM coding
[35:26] assistance here. Great. So now we're
[35:29] done with the transformer architecture.
[35:31] Let's try and pull us from 2019 to 2025.
[35:36] You just learned the architecture in
[35:38] this whole 18 section modules
[35:41] or for three modules of GPT2. But quen 3
[35:45] built in 2025. Let's see if we can read
[35:49] this and bring our knowledge from 2019
[35:52] to 2025. So, let's look at these two
[35:54] diagrams. This might be a good time for
[35:56] you to pause the video. What are the
[35:58] differences you see?
[36:02] What are not noticeably different things
[36:04] you see here?
[36:08] Okay, now we had a little break.
[36:10] Hopefully, you were able to spot the
[36:11] differences between GPT2 extra large
[36:14] 2019 and Quen 3
[36:18] 4 4B 2025. Let's try and go over what I
[36:22] see as is the differences in the SH.
[36:24] We'll do it one at a time. First,
[36:26] there's a bunch of numbers that are all
[36:28] different. What are those numbers?
[36:29] Hyperparameters, right? We have
[36:31] different sizes. First thing we could
[36:33] see is we moved from a vocabulary size
[36:35] of 50,000 to a vocabulary size of
[36:37] 150,000. there's no correct vocabulary
[36:40] size. All we have is like this
[36:43] vocabulary size that we've decided to
[36:45] use.
[36:46] >> Um because either way, it's always a
[36:49] compromise between the number of uh
[36:51] characters and the number of words and
[36:53] finding a good size for the embedding
[36:54] metrics relative to everything else.
[36:56] Okay. Another number that I noticed is
[36:58] different is we went from 48 transformer
[37:01] block. Those are 48 transformer blocks
[37:04] in GPT2 extra large. We were in 12 for
[37:07] GPT2 small. It went to 36 transformer
[37:10] blocks. We went from 25 heads in extra
[37:14] large. We were 12 for small to 32 heads
[37:17] in quen 3.
[37:20] The embedding uh dimensions went from
[37:22] 768 or 10 or in the case of XL600
[37:28] to 2560
[37:30] uh embedding size. a much larger
[37:32] embedding size, much more nuanced inside
[37:35] of the embedding metrics. Uh we went
[37:38] from uh a supported context length of
[37:43] 1,024 tokens to 32k tokens. Wow, much
[37:48] bigger, right? We can now support 32
[37:50] times more. uh we went from hidden layer
[37:53] dimension size inside of the inside of
[37:56] the growing shrinking MLP FFN from 6,400
[38:01] to 9,728.
[38:04] So my you could see where the all the
[38:06] extra parameters on top from 1 and 1/2 B
[38:09] to 4B came from. More transformer
[38:12] layers, more heads, more bigger MLPS,
[38:16] bigger embedding size means we just have
[38:19] more columns running through this entire
[38:21] transformer architecture.
[38:23] What's another example? We were using
[38:25] MHA multi head attention for mass
[38:29] multicausal multi head attention
[38:32] in uh GPT2 small uh and GPT2 XL as well.
[38:36] And then we move to masked group core
[38:39] attention GQA. Remember we talked about
[38:41] this. We have the option of having one
[38:43] shared KV between all of the attention
[38:45] head or we have the option of sharing
[38:47] some of them between some of the
[38:49] attention heads. So this is that's the
[38:51] decision that quen 3 did here. We kind
[38:54] of know a little bit about that. We
[38:55] didn't fully and we actually did fully
[38:57] implement this in Excel earlier and we
[38:59] even had a coding exercise with it.
[39:01] Great. We're getting very close to 2025.
[39:04] What's another example we saw? We moved
[39:06] from glue activation or rau activation,
[39:09] which is what we were taught to swigloo.
[39:12] What's swigloo? It's selu activation
[39:16] swish. We saw the formula for that early
[39:19] on in activation function section number
[39:22] four. And then we added another linear
[39:24] layer inside. Why did we add this linear
[39:26] layer? That's something called gated
[39:28] gated activation functions. We haven't
[39:30] seen these thus far. We're going to add
[39:33] another linear layer, another matrix as
[39:36] part of our activation function. And
[39:38] then that's something that's worth us
[39:39] learning about, right? We're not going
[39:40] to do it in the context of this
[39:42] workshop. But now you know what you
[39:44] don't know. You know that there's a
[39:45] thing called gated activation functions.
[39:47] You kind of have a basis of not gated
[39:49] activation functions. So now let's try
[39:51] and like learn one more thing. Great. So
[39:53] that's another thing we learned. We
[39:55] changed the activation function from
[39:56] glue to swigloo. What else did we add
[39:59] here? We can see the normalization is
[40:02] kind of different. So first we were
[40:04] using RMS norm, right? And so we used to
[40:07] use layer norm for GPT2. Now we're in
[40:10] RMS norm. Everyone just uses RMS norm
[40:12] nowadays because it doesn't have to
[40:14] calculate the variance. Finally, there's
[40:17] another thing we can tell here. there's
[40:19] uh a K QK RMS norm inside of the mass
[40:24] group attend uh query attention GQA. Why
[40:27] is that? That's a new thing that Coin
[40:29] decided to do. It's becoming the norm.
[40:31] Not super the norm yet, but for smaller
[40:34] model QK norms have proven to be
[40:36] slightly more stable. So that's another
[40:38] concept we're not going to cover in this
[40:39] workshop. But now we know what we don't
[40:41] know to get to 2025.
[40:43] Cool. What's the one last difference we
[40:46] had instead of a of an absolute
[40:49] positional embedding layer, right?
[40:51] Either learn like GPT2 did or cinosodal
[40:54] like we want to do, we're actually going
[40:56] to use rope inside of the attention
[40:59] block. So, we're not changing the
[41:00] embeddings right away. Inside of
[41:03] attention, we're going to calculate the
[41:06] relative position between pairs of
[41:08] tokens and we're going to apply that
[41:10] within attention.
[41:12] Great. So we didn't fully learn about
[41:14] rope. We didn't do the math and a whole
[41:15] sheet about it. But we can now know,
[41:17] okay, I kind of understand how this
[41:19] works. I understand why I need
[41:20] positional encodings and so on. Right?
[41:22] Rope is something you can learn on your
[41:24] own. Hey, I just want to call out we
[41:26] were only about two concepts that we
[41:29] haven't learned away from uh 2025. So we
[41:33] didn't know about Qk RMS norm. Now we
[41:35] do. It's just RMS ignoring the QK uh
[41:38] matrixes. and we didn't know about gated
[41:41] activation functions. But for everything
[41:42] else, we can kind of read the chart. We
[41:44] can kind of update it. That's something
[41:46] new that you didn't have before. You now
[41:49] have the ability to read architecture
[41:50] diagrams. Oh, and then yeah, and uh one
[41:53] last thing to mention, there's no
[41:55] dropout. No one does drop out anymore,
[41:57] right? Like why we talked about this
[42:00] when we talked about section 13
[42:02] regularization. Dropout really popular
[42:05] early on. It's something that deep
[42:06] neural networks love to do, but that's
[42:08] because they see the data over and over
[42:10] again in multiple epochs. We don't have
[42:12] that in large language models. For the
[42:14] most part, as far as I know, most large
[42:16] language models are trained with seeing
[42:18] the the text once. So, because of that,
[42:20] droplet is not really helping us prevent
[42:22] that kind of overfitting.
[42:25] So, you now know how to read
[42:26] architecture diagrams. There's so many
[42:28] more. I super recommend Sebastian
[42:31] Rashtra's uh LM architecture gallery. He
[42:35] came up with this 5 months ago.
[42:37] Brilliant, brilliant, brilliant. Also
[42:38] has a GitHub repo, by the way, if you
[42:40] want to see the data behind it. So,
[42:42] let's say I open that up here. I'm just
[42:44] going to click this link. And then this
[42:46] is the architecture diagrams. As of May
[42:48] 27, when I'm recording this, I think I'm
[42:50] recording the 29th. There's 72 models
[42:53] here. Let's look at the most recent
[42:55] model that was added. I'm going to click
[42:56] the changes button, right? Oh my
[42:59] goodness. So, Laguna XS.2 was added.
[43:03] Great. By the way, this is a great
[43:04] diagram of everything everything. It
[43:07] looks great on a wall if you have it.
[43:08] So, let's go try and compare our GPT2
[43:12] model, which was the thing we've been
[43:13] building all along here, 2019, to this
[43:16] Laguna XS2 33 billion model that uh was
[43:20] built. So, this is from like a week ago
[43:23] effectively. This is the middle of 2026.
[43:27] Can we read this diagram and understand
[43:29] what's going on and at least understand
[43:31] what we don't know? Right? So we were
[43:33] two concepts away between GPT2 and quen
[43:36] 3. We needed to learn about QK norm. We
[43:39] need to learn about gated activation
[43:40] functions. Let's look at this diagram
[43:43] from something from a week ago. What do
[43:45] we not know here? Create slightly
[43:47] different numbers. First thing that I
[43:49] can catch is there's an thing called
[43:51] layers. That's going to be not covered
[43:53] by our workshop. But once your model
[43:55] gets big enough above 10 billion
[43:57] parameters, we generally don't we don't
[44:00] activate the entire network for every
[44:01] pass. We have this thing called mixture
[44:03] of experts. So that's a concept we're
[44:06] not familiar with, not going to learn in
[44:07] this workshop, but you know what you
[44:09] don't know. And again, if you look at
[44:12] the rest of this, you kind of know
[44:14] everything. Vocabulary size 100,000.
[44:16] There's a feed forward network that's
[44:18] growing and shrinking. There's a context
[44:21] length of 131. We repeat the thing.
[44:23] What's the other concept we don't know
[44:24] about? We use GQA, still very relevant.
[44:27] And there's also SWA, sliding window
[44:30] attention. So sliding window attention
[44:32] instead of comparing to the entire
[44:35] context length compares only to things
[44:37] right before and right after it in a
[44:39] sliding context kind of way. We don't
[44:41] know what S swa is. But what's worth
[44:44] knowing is that um uh is something we
[44:48] don't know. So in order to get this from
[44:50] 2025 quen 3 model to 2026 Laguna XS.2
[44:55] model, we only had to learn two more
[44:57] concepts. MOER, which is actually a 2025
[45:00] concept. That's the thing DeepSync did
[45:01] in the early parts of 2025 that made the
[45:04] stock market crash because everyone was
[45:06] like, "Oh my god, you don't have to run
[45:07] this entire model." And they have both
[45:10] GQA and SWA sliding window attention.
[45:13] So, we're two concepts away from 2025
[45:16] entering 2026. I'll also mention that
[45:18] it's like at a 3:1 ratio. So, there's
[45:20] still global attention with GQA and now
[45:22] there's local attention with SWA. Great.
[45:26] You can now read these diagrams. You
[45:28] know what you don't know. All you are
[45:30] away from here is like four more
[45:32] concepts. Maybe we'll have some
[45:34] resources to bridge for those in a
[45:35] minute. Great. So, there's lots more
[45:37] diagrams. Everyone go read Sebastian
[45:39] Rash's LLM architecture diagram.
[45:42] Let's make some decisions because we're
[45:44] still trying to build a large language
[45:45] model oursel even though we're experts
[45:47] now. So, transformer blocks, we should
[45:50] have some, right? How many? 12 layers.
[45:53] We're just trying to build GPT2 small
[45:55] equivalent here. So we could train it
[45:57] pretty quickly on one GPU layer
[45:59] distribution by year. So how many layers
[46:02] normally people have? If you look at
[46:04] this year by year by year and by the way
[46:06] I grabbed this from uh Sebastian
[46:08] Rashtra's GitHub and I had Claude make
[46:11] it beautiful for us. But effectively you
[46:13] can see the number of layers in open
[46:15] source models is going up year by year
[46:17] by year. Right? We've just chosen to use
[46:19] 12 layers because it's really easy to
[46:21] train on. It's what GPT2 small trend on.
[46:23] So we'll try and try trend something
[46:26] similar to that. Another thing that I
[46:27] derived from Sebastian Russia's GitHub
[46:30] repo that's behind LLM uh architecture
[46:33] diagrams is the contact size. We're
[46:35] going to have our contact size be tiny
[46:37] 1k a thousand tokens. Realistically you
[46:41] could also see the contact size is
[46:43] growing year by year with a max kind of
[46:45] hovering around 1 million for the really
[46:47] really large models. So really amazing.
[46:51] We now have made the last set of
[46:53] decisions we need to uh have a complete
[46:56] transformer architecture. Let's
[46:58] recommend a couple of resources. At this
[47:00] point, you are able to read existing
[47:03] GP22 code. You can read a model end to
[47:06] end and understand what you know and
[47:08] what you don't know. So it's three three
[47:10] big chunks of resources I could
[47:11] recommend here. One is Corpathy's three
[47:14] repos. Mini GPT from five years ago,
[47:17] nano GPT from four years ago, nanohat
[47:19] from now. Nanohat really great. He's
[47:23] using his auto research solution to
[47:25] iterate on this and make it better and
[47:27] make it faster to train and improve the
[47:29] performance. To me, not readable by
[47:32] humans anymore. It's really code meant
[47:34] for machines to read. It's almost so
[47:36] like a bit harder to read.
[47:39] uh but it is running a lot of nightly
[47:41] experiments to try and get to the best
[47:42] fastest most efficient training on the
[47:44] scaling laws that he found within these
[47:47] models. Uh nano GPT I think is the most
[47:51] readable option here. So if you go to
[47:53] nano GPT you can go ahead and read the
[47:56] model pi file and this is stuff that you
[47:58] know how to read. It's got a layer. It's
[48:00] got causal self attention. Oh my god,
[48:02] how many heads? How many how it's got
[48:04] drop it here, right? Flash attention.
[48:06] What's flash attention? Maybe we'll talk
[48:08] about that a bit in a moment. We have uh
[48:11] the forward pass an MLP growing
[48:14] shrinking MLP. You could read this code
[48:16] and really understand how it's built.
[48:18] Great. So that's the first set of
[48:20] resources anything from Karpathy from
[48:22] his three reimplementations of GPT.
[48:24] Another set of resources I could really
[48:26] recommend is uh Sebastian Roger's build
[48:29] your own LLM books. So the first book is
[48:32] build a large language model. I'm going
[48:34] to do this thing where I reach out and
[48:36] the background becomes real.
[48:41] Oh my goodness. This is the build your
[48:42] own LLM book from Sebastian Rasha. Build
[48:45] a large language model from scratch.
[48:47] Very much recommended. We did cover most
[48:49] of this material in this workshop, but I
[48:52] still think it's great that you're able
[48:54] to read his GitHub repo and his book and
[48:56] like maybe get a second perspective on
[48:58] things. Additionally, he's also building
[49:00] a build your own reasoning model that
[49:04] effectively enters like the land of RL
[49:06] and a little bit of reasoning. We
[49:08] haven't covered RL yet, but we will
[49:10] later on in this workshop. More reapers
[49:12] you could read. I really love these two
[49:14] open source reapers. These are the only
[49:16] two that I will recommend personally.
[49:18] You have Tom Matthews No Magic Micro GPT
[49:21] co-authored with Claude and he admits
[49:23] that. But I still think it's really
[49:25] really amazing because he has single
[49:28] file implementations of an entire GPT
[49:31] architecture and a bunch of other things
[49:33] as well. So for example, if you read
[49:35] this micro GPT file, he's got his own
[49:38] implementation of right here. This is an
[49:42] your own implementation of PyTorch
[49:43] Autograd. He just created his own
[49:45] implementation. I learned a lot from
[49:47] reading this file. I thought it was
[49:48] great. You too can go read this file
[49:51] right now. This is how he handles
[49:52] building his own autograd. What's
[49:54] autograd? Feed forward back propagation.
[49:57] You have to keep things in memory. You
[49:58] have to do derivatives. This is his
[50:00] implementation of that. I really love
[50:02] that and I would really recommend that.
[50:04] How do you do parameter initialization?
[50:06] So on and so forth. This whole repo I'm
[50:09] just going to go to the global readme
[50:11] file has a bunch of I'm going to go to
[50:14] the global readme file has a bunch of
[50:17] implementation of all the concepts we've
[50:19] learned. So BP tokenizers, he's got uh
[50:23] optimizers if you want to learn more
[50:25] about optimizers. So on every one of
[50:27] these sections has stuff we we have
[50:29] either learned about or we learned
[50:30] about. So for example, I'm not going to
[50:32] teach you reinforce when we get to RL,
[50:34] but I strongly recommend you try and
[50:36] read about it here, right? Dropod
[50:39] concepts that we've covered, attention,
[50:42] flash attention, page attention, other
[50:44] forms of attention, KV caching,
[50:46] quantization, rope. If you want to learn
[50:48] more, this is a great place to do that.
[50:50] At another repo that I really want to
[50:52] recommend is this repo from I'm sorry
[50:54] I'm going to butcher the name Ryan Ya.
[50:59] Uh this is a very recent repo. I think
[51:01] it's from like a month ago and I just
[51:04] absolutely adore it. Why? Because he's
[51:07] trying to teach you through code a lot
[51:08] of the concepts that we were teaching
[51:10] here in this workshop. Really amazing
[51:13] resource. So for example, if you want to
[51:15] learn about tokenization, you go to this
[51:16] notebook. You want to learn about
[51:18] embeddings, you go to this notebook. He
[51:20] doesn't teach the fundamentals of ML the
[51:23] way that we did in this workshop, but I
[51:24] think you can now go read his code and
[51:26] steal ideas from him. What idea did I
[51:29] steal from him? Right? When we go into a
[51:32] full training pipeline, he has this like
[51:35] really like this this is their version
[51:37] of learning how to train a machine
[51:39] learning model. I really loved that.
[51:42] Here he's trying to explain the chain
[51:45] rule using fun analogies. I've never
[51:47] seen anyone do that before. Remember
[51:49] when we learned about chain rule in
[51:51] section 8? I basically stole this idea
[51:53] from them, right? The quality of the the
[51:56] of the muff of the baked good divided by
[51:59] sugar has to do with sweetness. Oh my
[52:01] god, that's basically our muffin example
[52:03] from earlier. So I really think there's
[52:05] a lot to learn from this and you can
[52:06] like now you can read stuff and you you
[52:09] already know about 80% of the stuff in
[52:11] this repo really great for you to read
[52:13] through this and learn a little bit more
[52:15] right overfitting how do we prevent that
[52:17] dropout weight decay have a large
[52:19] diverse data set you could do gradient
[52:21] clipping this is the stuff that we
[52:22] covered in section 13 so now you could
[52:24] go read another implementation of that
[52:26] and see what you know and what you don't
[52:28] know great so this these two repos are
[52:31] my favorite I really love that Uh the no
[52:34] magic repo has everything kind of
[52:36] standalone and then Ryan's repo has
[52:40] everything building step by step like we
[52:41] did in this workshop. Really really
[52:43] amazing resources for you to go read
[52:45] from. Next up is going to be
[52:48] pre-training. Pre-training is going to
[52:50] be mostly about where we get data from.
[52:52] How do we work with data and then end in
[52:54] the end of that we'll create a
[52:56] pre-training notebook that we can use to
[52:58] pre-train our large language model. This
[53:00] is now we've moved from se from the
[53:03] third module of this uh workshop. First
[53:06] module was let's use NLM. Second module
[53:09] was let's train a machine learning model
[53:11] any machine learning model with neural
[53:13] networks. Third module we were building
[53:15] up the architecture for transformers
[53:17] starting from deep neural networks all
[53:19] the way to language specific concepts
[53:21] like tokenizer embeddings and now the
[53:23] transformer architecture.
[53:25] The last thing we have to do before we
[53:26] train a large language model is to learn
[53:28] about pre-training. where does the data
[53:30] come from? How do we uh how do we have
[53:33] high quality data? So on and so forth.
[53:35] So that's going to be our next and final
[53:37] section before we have our pre-training
[53:39] script. After that, we'll have to do
[53:41] instruction tuning RL and then we'll
[53:43] cover a little bit about what we didn't
[53:44] cover. Strongly recommend that you stick
[53:46] around. Let's finish up this workshop.
[53:48] Thank you so much and I hope to see you
[53:50] in the next section.
