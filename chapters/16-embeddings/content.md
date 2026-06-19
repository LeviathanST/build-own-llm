# Embeddings | Build Your Own LLM Workshop #16

**Build Your Own LLM Workshop — Video #16 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 48m 42s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=jyrgYjeVHBo |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to building
[00:02] our own large language model workshop.
[00:04] I'm Justin Angel and now we're going to
[00:07] be building our embed embedding metrics
[00:09] and also our unmbed metrics and kind of
[00:12] just learning about what embeddings are.
[00:14] Previously we've looked at tokenizers.
[00:16] So tokenizers translate a string to int
[00:19] and an int to string, right? They just
[00:21] figure out how to represent string in
[00:24] numbers. What we haven't actually been
[00:26] able to do thus far is uh be able to
[00:31] represent those numbers in something
[00:33] that the network can really really work
[00:35] with. So what are embeddings? This is
[00:38] going to be the most difficult concept
[00:40] in this whole in this whole section.
[00:43] It's understanding what embeddings are.
[00:45] You're not going to necessarily
[00:46] understand it from this slide. You're
[00:47] going to understand it from the next set
[00:48] of slides. But I have to give you a
[00:50] definitional component. So embeddings
[00:53] are highdimensional space for tokens.
[00:55] Tokens are numbers that run between 1
[00:57] and 50,000 1 to 150,000 depending how
[01:00] big we want our tokenizer vocabulary to
[01:03] be. That's the vocabulary size.
[01:05] Embeddings are taking those ins and
[01:08] translating them to a highdimensional
[01:10] space. What does highdimensional even
[01:13] mean in this context? Right?
[01:16] So one dimension it's one axis the
[01:19] x-axis. Two dimensions it's x and y. So
[01:23] we have things in two dimension. They
[01:25] have the x and y coordinate. Three
[01:26] dimensions it's x, y, and z. Now we're
[01:28] adding depth, height, and width. Right?
[01:31] Four dimensions. Let's say I add time.
[01:33] How many dimensions does Chad GPT2 small
[01:36] use? The smallest of the models. It uses
[01:38] 768 dimensions. I don't think in 76 768
[01:44] dimensions. I can maybe kind of remember
[01:45] that a hyper cube is like a 3D
[01:48] representation of a four-dimensional
[01:50] entity or a four-dimensional structure.
[01:52] One would call it a manifold. I don't
[01:55] have the ability to think in 768
[01:57] dimensions. CHPT too small. The smallest
[02:00] of the models, right? The one of the
[02:02] earliest models thinks in 768
[02:05] dimensions. Every single token every
[02:08] that potentially could represent a word
[02:10] exists in 768 dimensional space. Why
[02:14] does it do that? Because it needs to
[02:16] find a way to understand what the token
[02:18] means. And the word understand is doing
[02:21] a lot of heavy lifting in the context of
[02:23] that statement. So let's try and at
[02:25] least learn one thing from the slide
[02:27] even if we don't understand what
[02:28] highdimensional means. Right? It takes
[02:31] the token ID that we could see here on
[02:33] the screen. Hello world. I'm here.
[02:35] Translates every token to a token ID. So
[02:38] that's the tokenizer. And after that, it
[02:40] translates it to 768
[02:42] columns worth of data on every one of
[02:45] those tokens. This is still not within
[02:47] the context of our sentence. This is
[02:49] just within the context of what the
[02:52] token means one to one in 768
[02:55] dimensions. Cool. So now you're kind of
[02:57] confused. That's totally fine. We'll do
[03:00] a hard break lift. What do you mean by
[03:03] understand Justin? Right? Like I don't
[03:06] understand what it means to understand
[03:07] things. So let's again go back to our
[03:10] definition. Each token maps to n
[03:12] dimensional space and for GPT2 small is
[03:15] 768. The meaning of the token world
[03:19] exist in superposition of 768
[03:23] highdimensional structure. What do I
[03:26] mean by superposition? Superposition
[03:28] means not necessarily every one of the
[03:31] 768
[03:33] dimensions is fully used. Right? When I
[03:36] if I'm a person, I definitely exist in
[03:38] all of the 3D dimensions of 3D space. A
[03:42] dog definitely exists in 3D space. I
[03:44] also use most of my some portion of my
[03:46] 4D dimensions at least exist in some
[03:49] portion of 4D dimensions, right? But I
[03:51] don't exist in all 4D dimensions. For
[03:53] example, I don't exist in minus 20,000
[03:56] AD. that just oh sorry in minus 2000 BC
[03:59] I just like my space-time worm doesn't
[04:01] go that far. So most of these wars are
[04:04] represented in all 768 dimensions don't
[04:07] exist in them. Cool. Now you're super
[04:09] confused cuz I use the word like
[04:10] superposition. Let's go back to our
[04:13] world to our word of understand
[04:16] and we're going to use something called
[04:17] analogy vectors here. This is a bit of a
[04:20] magic trick but let's at least try and
[04:22] see this magic trick. Let's say that I
[04:23] take the tokens for queen, woman, man,
[04:26] and king, right? I use a technique
[04:29] called PCA. I retrieve their 768
[04:32] highdimensional embedding and then I use
[04:35] PCA to compress it down to two
[04:37] dimensions. Two dimensions only, we're
[04:39] going to lose a lot of data in that
[04:41] compression. Right? If something exists
[04:43] in three dimensions and I compress it to
[04:44] two dimensions, right? Like that's
[04:46] called a painting or a photo. It loses a
[04:48] lot of data in that process. So we're
[04:51] going to lose a lot a lot a lot of data
[04:53] compressing to 768 or representing 768
[04:57] dimensional structure in two dimensions.
[05:00] We could still do that using PCA. We're
[05:02] not going to teach you about the PCA
[05:03] here minus the fact that it can take a
[05:05] high dimensional representation and take
[05:07] it down to two or three dimensionals
[05:08] which we could see. What do we see? Man
[05:12] and woman uh man and king exist roughly
[05:15] within the same distance and in
[05:18] direction from woman and queen. and we
[05:20] could see that on the screen in front of
[05:21] us. We're going to build that that chart
[05:24] together later on. I do want you to have
[05:26] that understanding.
[05:28] So what does that tell us? Analogy
[05:30] vectors are really great parlor trick.
[05:32] You could do them with like geography
[05:35] for example, capital cities. Paris and
[05:37] France exist in the same direction in
[05:39] space as Berlin and Germany for example.
[05:42] Very very cool. This is not necessarily
[05:46] how large language models actually do
[05:48] analogies. We have like a lot of recent
[05:50] research into that. But that is how some
[05:54] of that some of that data does exist in
[05:57] the embedding metrics. Cool. So what did
[06:00] we learn from analogy vectors? Woman and
[06:03] queen exist roughly within the same
[06:05] distance and direction from men and
[06:07] king. Berlin and Berlin and Germany
[06:10] exist roughly within the same direction
[06:11] and uh distance from Paris and France.
[06:16] What we learned, and this is key,
[06:19] these seemingly random numbers mean
[06:22] something to an alien intelligence that
[06:24] thinks in highdimensional space. You and
[06:27] I don't think in highdimensional space.
[06:30] Large language models think in
[06:32] highdimensional space. They are alien
[06:34] intelligence. We don't fully understand
[06:36] how they think. We don't fully
[06:38] understand how they work. That is an
[06:39] active field of research. We do know
[06:42] they think in highdimensional space. I'm
[06:44] going to give you a little bit of a
[06:46] spoiler to a field called mechanistic
[06:47] interpability. They use the direction
[06:50] which we've already seen. They also
[06:52] build up other structures within
[06:53] highdimensional space to think and do
[06:55] math. For example, really interesting
[06:57] field. We're not going to go into that
[06:59] as at all. Important thing to realize
[07:01] highdimensional presentation is how LLMs
[07:04] think, reason, understand, whatever word
[07:07] you want to use here to
[07:08] anthropomorphicize
[07:10] um LLMs.
[07:12] Great. So now we're going to move up
[07:14] from the philosophy of embedding spaces
[07:16] into some hyperparameters that every
[07:19] model is going to need to set. So I
[07:22] first parameter that we're going to all
[07:23] look at is the vocabulary size. We've
[07:26] actually said that one in the past.
[07:27] Remember we told BPE, I want you to do
[07:30] no more than 5,000 merges. I want you to
[07:32] have a vocabulary size of no more than
[07:34] let's say 5,000 or 10,000. GBT2 set its
[07:38] uh tokenizer at 50,000. Coin 3.6 six set
[07:42] its token size at 150,000, right?
[07:45] Depending on the model size, that's
[07:47] roughly the range we're playing in. So,
[07:49] vocabulary size, first hyperparameter
[07:51] that we're going to learn about here.
[07:52] Really important. We could see it
[07:54] represented
[07:56] here on the screen in the embedding
[07:57] metrics. That's how many rows the
[07:59] embedding metrics has. Right? All of the
[08:02] words are going to be represented once.
[08:04] All of the tokens are going to be
[08:05] represented once in the embedding
[08:07] metrics. That is our dictionary of how
[08:09] we map tokens to an highdimensional
[08:12] embedding space. Cool. That brings us
[08:14] into the second parameter that we're
[08:16] going to have to learn. The embedding
[08:18] hidden size often referred to as hidden
[08:20] dims or dim or hd dim for short. If you
[08:23] really like short I like calling it
[08:26] hidden size or hidden uh dimensions.
[08:29] um that is how many dimensions in a high
[08:33] dimensional representation are we going
[08:35] to allow each token to represent itself.
[08:38] The more dimensions the more information
[08:41] we can compress into every token right
[08:44] so the you could really think about it
[08:46] as the more the model gets to learn on
[08:49] the pair word pair subword pair token
[08:52] level. So really important. Why? Right?
[08:55] You can imagine a double hidden size
[08:58] could be super useful to learning more
[08:59] words. It will also double the size of
[09:02] our embedding metrics. We've already
[09:03] said embedding metrices are huge. They
[09:05] take up a third of GPT2 small size.
[09:08] Doubling that not really feasible. Okay.
[09:10] So now we know vocabulary size. That's
[09:12] how many words are in my tokenizer.
[09:14] Also, how many rows are going to be in
[09:16] my betting metrics? We now learned about
[09:18] embedding hidden size or hidden dims in
[09:21] embedding metrics. That's how many
[09:22] columns, how many hidden dimensions, how
[09:25] many highdimensional
[09:26] uh dimensions are we going to represent
[09:29] our tokens in? Great. So, we now we have
[09:32] two hyperparameters are under our belt.
[09:34] Third hyperparameter we're going to
[09:36] learn about right now is context size.
[09:38] Why? Large language models operate in a
[09:41] fixed context size for the most part.
[09:44] There's things we could think about
[09:45] here, ways to maybe hack our way around
[09:47] that. Maybe we'll have LLM call LLMs to
[09:50] kind of go around that. Maybe we'll have
[09:52] something else to do with like context
[09:54] size. There's a lot of fun hacks there.
[09:56] But for our purposes, context size is a
[09:59] fixed maximum number of token that our
[10:01] large language models can receive. Why
[10:04] is that important? You can think about
[10:06] uh our size of our matrixes inside of
[10:10] our model as being very conditioned on
[10:12] the context size. The content size
[10:14] determines how many rows are going to
[10:16] transfer inside of our large language
[10:19] model. It really determines how many
[10:21] maximum number of tokens our model can
[10:23] handle. At least now as we're still
[10:26] dealing with something called um causal
[10:29] self attention. Maybe in the future
[10:31] we'll learn about something else that
[10:32] kind of changes that math. But for now
[10:34] we're just going to stick to that
[10:35] definition. Contact size the maximum
[10:38] number of tokens. What why does context
[10:40] size matter?
[10:42] We can see that we have an input matrix
[10:45] and the num and each token represents uh
[10:48] a column here and the maximum number of
[10:51] columns that we can use is going to be
[10:53] our contact size. JJPT2 uses a,024
[10:56] contact size. That's laughably small.
[10:59] That's like 500 750 words. That's barely
[11:03] a few paragraphs of text. That's all
[11:06] we're going to build for now in GPT2
[11:08] small, right? If you look at like larger
[11:10] models, maybe they have a contact size
[11:12] of a million. Some people can claim that
[11:15] they've had a hundred millions nor made
[11:18] it so it's totally irrelevant. We're
[11:20] pretty soon going to see why that's a
[11:21] very hard task to do. Great. So, we
[11:24] learned about context size. Now, that's
[11:27] the number of tokens that we're going to
[11:29] accept at maximum. Uh we also have a
[11:31] thing called bat size. Bat size is
[11:34] really in this context mostly useful for
[11:38] uh inference time where I want to say
[11:40] okay my maximum content size is,024
[11:43] but I want to process two words in
[11:46] parallel not from the same sentence cuz
[11:48] the sentence has to be sequentially auto
[11:50] reggressively generated but I want to
[11:52] add two sentences at the same time to
[11:54] generate so I could use all of my GPU so
[11:56] I'm going to say my bat size is two
[11:58] which means my effective content size
[12:00] might be 512
[12:02] did I just lie to you. Probably you
[12:04] could probably use a context size of 750
[12:07] and 250 as well. There's some systems
[12:10] that do that, but for now, we'll assume
[12:12] bat size just means we divide our
[12:14] context size in whatever the bat size
[12:16] is. We're not going to really use bat
[12:18] size right now. We will set the
[12:20] hyperparameters something, but I do want
[12:23] to let you know that it exists. Cool.
[12:25] So, I just taught you about the four
[12:27] hyperparameters of embeddings. We taught
[12:29] you about vocabulary size. How many
[12:32] dimensions does that vocabulary size
[12:34] translate to? What is the context size?
[12:36] The maximum number of tokens and the bat
[12:38] size. How many how do I want to divide
[12:40] that context? Now I'm going to teach you
[12:42] about a about a third matrix. So we
[12:45] learned about the uh input matrix which
[12:48] has our input in just token space. We
[12:51] have the embedding metrics which has us
[12:53] in high hidden dimensional space or
[12:56] activation space or one of these spaces.
[12:59] That's vocabulary size time hidden size.
[13:02] Input matrix is batch size times context
[13:04] size. Now we're going to merge both of
[13:06] them together because embedding matrix
[13:08] is not specific to my sentence and h
[13:12] doesn't know what my tokens actually are
[13:14] and the uh input matrix knows what my
[13:16] tokens are but doesn't have the
[13:18] embedding space. So how do we marry both
[13:21] of those? We'll create a matrix that I
[13:24] call input embeddings matrix. You can
[13:27] call it whatever name you want to call
[13:28] it
[13:30] that takes our tokens and puts them in
[13:32] embedding space. And you could see it
[13:34] here, right? Input embeddings. So now
[13:36] it's hello, hello world, I'm here, but
[13:38] with the same values that we're going to
[13:41] have uh uh with the same values that we
[13:44] have from our embedding metrics. Great.
[13:47] Uh, and to me that means that we've
[13:50] gotten pretty pretty ahead of like being
[13:52] able to compose these together. You
[13:54] could see that the hero in the embedding
[13:57] metrics has the exact same values as it
[13:59] does in the input embeddings. Why is
[14:01] that? We're using the embedding metrics
[14:03] as a reference lookup table whatever of
[14:05] sorts to combine it into input
[14:07] embeddings. So now we learned about both
[14:10] the four hyperparameters and how they
[14:13] relate and translate into the three
[14:15] matrix types of like actually inserting
[14:17] data into our large language model. In
[14:19] effect we just learned how to put text
[14:22] into a deep neural network that just
[14:24] operates in numbers. Those numbers being
[14:27] highdimensional representation. Great.
[14:30] Four hyperparameters, three matrices.
[14:33] All of these exist in high dimensional
[14:34] space. You must be a bit confused now,
[14:36] but maybe it's starting to clear up.
[14:38] Let's look at uh an embedding matrix
[14:41] that you've already seen. Surprise. If
[14:44] you've been following this workshop end
[14:46] to end, you've already seen an embedding
[14:48] matrix. How do I know you've already
[14:50] seen an embedding matrix? One of the
[14:52] first thing we trained in section 8 a +
[14:55] b modulus 5. Remember that first
[14:57] embedding matrix? We threw it into a
[14:59] PCA. We saw that it's like just a circle
[15:02] with five points in it. Right? Cinosodal
[15:04] of sorts. One would say sinus, right?
[15:07] angle based uh the the 200 by 32
[15:11] dimensions remember we had that first
[15:13] metrics 200 inputs so 100 for a 100 for
[15:17] b 200 one hot encoding exist in 32
[15:21] dimensions those were 32 hidden
[15:24] dimensions
[15:26] and I effectively created an embedding
[15:28] matrix in there and kind of didn't tell
[15:30] you about it at all right and now we
[15:33] could see that we've actually seen one
[15:35] of these before we had a vocabulary size
[15:37] of 100. One would say, sorry, 200, maybe
[15:41] two, depending on how you want to look
[15:42] at it because we only had A and B, but
[15:44] we actually had a 32 hidden dimensions
[15:48] that each one of those uh A and B values
[15:52] got embedded into, which is why we were
[15:54] then able to do a little bit of
[15:55] interpretability work and then see that
[15:58] it's actually with PCA represented two
[16:00] dimensions in five points of a clock,
[16:02] right, of a circle. So hidden layer
[16:05] number one of A and B modulus 5 is an
[16:08] embedding matrix had 200 input neurons
[16:11] had a hidden layer of 128 neurons that
[16:14] ended uh ended up being our embedding
[16:17] metrics.
[16:18] Great. Now that we all understand how
[16:22] embedding metrics works, I'm going to
[16:23] throw a wrench in in our understanding
[16:26] of it. We have a problem. the embedding
[16:29] values that come from the embedding
[16:31] metrics into our input matrix uh into
[16:34] our input embedding metrics actually
[16:37] don't contain any positional
[16:38] information. Why? They have nothing to
[16:40] do with our sentence. So for example,
[16:43] man bites dog. That's the most common
[16:45] example here is represented exactly the
[16:48] same as dog bites man. That's actually a
[16:50] problem because man bites dog means that
[16:53] man is going through maybe a psychiatric
[16:55] evaluation. Dog bites man means man is
[16:58] going to go to the hospital, get maybe
[17:00] some sort of shot, right? Totally
[17:02] different meanings to the sentence. We
[17:04] cannot lose positional information.
[17:07] However, without positional information,
[17:10] what the LLM would get is just the words
[17:12] dog, men, and bite. It doesn't know the
[17:15] order of them. That's a real problem in
[17:17] the understanding of the sentence. So
[17:19] the solution that we're going to come up
[17:21] with is we're going to take the input
[17:24] embedding metrics that's already our
[17:25] sentence with the embedding ma
[17:27] dimensions um and we're going to add
[17:30] small values the dimen the the LLM can
[17:33] then learn hey actually
[17:36] that represents the position for so for
[17:39] example for the man position the first
[17:41] position we can add the number one to
[17:43] everything for the second position for
[17:45] bites we can add the number two to
[17:46] everything for the number for dog we can
[17:49] add the number three for everything.
[17:50] That's not at all how any of this works,
[17:53] but you can maybe start getting a taste
[17:55] to it. We'll actually see how it works.
[17:58] Don't think that everything is plus 1
[17:59] plus 2 plus 3. How does it actually
[18:02] work? Well, in the back here, you have a
[18:04] very beautiful, let's call it
[18:06] representation or visualization of how
[18:09] this actually works. We add these
[18:12] beautiful concentric sorry these
[18:14] beautiful wave circles
[18:16] to every one of our inputs. So every row
[18:19] in the input embedding is going to get
[18:21] one of these rows added on top. What do
[18:23] those rows are? How do we get to them?
[18:25] Let's try and learn that together. But
[18:27] this is really what we ended up adding.
[18:30] Remember every row is a used to be a
[18:32] token now is represented in
[18:34] highdimensional embedding space. Great.
[18:37] Why do we have positional encoding? We
[18:40] have a 3D spinning pug here in front of
[18:42] us. Why is why am I showing this to you
[18:45] before I'm teaching you formulas? I want
[18:46] you to have intuition. If you take a pug
[18:49] and you rotate in three dimensions, it's
[18:52] still a pug.
[18:54] Really critical to understand that. Take
[18:57] a pug, spin in the three dimension, the
[18:58] opposite direction, still a pug.
[19:02] We are rotating this highdimensional
[19:05] object structure representation and
[19:07] embedding space a little bit in such a
[19:10] way that it's still the same token
[19:12] embeddings that it was before but enough
[19:15] to let the model know actually that's
[19:17] the position it used to be in. So if a
[19:19] pug is rotated 10° it knows it was in
[19:22] the first position. If it's rotated 20°
[19:24] it knows it was in the second position.
[19:25] 30° it knows it's in the third position.
[19:28] the as long as we kind of rotate the
[19:31] inputs a bit, the model could learn what
[19:34] their position was. We're effectively
[19:35] overloading rotating. I'm using rotation
[19:38] in air quotes here.
[19:41] The model can then learn where their
[19:43] position was in the sentence. Very cool.
[19:46] Remember, rotating pugs in
[19:47] three-dimensional space. They're still
[19:49] pugs, but I can overload the rotational
[19:51] information with positional information.
[19:54] And that's what we're really doing here.
[19:56] Great. So, now that they gave you a fun
[19:58] metaphor about pugs in threedimensional
[20:00] space, let's give you a scary math
[20:02] formula. The formula for absolute
[20:04] position adds x and y position dependent
[20:07] values to every value in the input
[20:09] embedding metrics. What does that mean?
[20:11] It's a very complicated way of saying we
[20:13] take every single value in our input
[20:15] embedding metrics. I'm going to flash it
[20:17] on the screen again. Bottom right, input
[20:19] embedding metrics, right? And I'm going
[20:21] to take every one of those values and
[20:23] I'm going to add a small value to it.
[20:26] That's the positional embedding value.
[20:28] That is it. I'm going to take another
[20:31] matrix of the exact same dimensions and
[20:34] then put it on top and then do just
[20:37] normal pie-wise addition. That is all
[20:40] we're going to do. Okay. So in absolute
[20:43] positions and then specifically absolute
[20:46] sinosoidal positioning we alternate
[20:49] between sinus and cosine. Why? Because
[20:52] they're they repeat themselves which
[20:54] means the model can learn a lot from
[20:55] these repeating values and we'll create
[20:58] this identifiable pattern that the model
[21:00] could learn. That is an option for how
[21:03] to build absolute positioning. There are
[21:05] other options which we'll see later on.
[21:07] So the top left right formula says all
[21:11] we do to the input embedding metrics is
[21:13] we add a value to it. We add a
[21:15] positional embedding value to it. How do
[21:17] we calculate the positional embedding
[21:18] value? Well, that's actually pretty
[21:20] complicated. If the position is even,
[21:23] then we do sinus statements. If the
[21:25] position is odd, then we do cosine
[21:28] statements. We're going to see how to
[21:29] implement all of these in Excel. The
[21:33] important thing to remember is that it's
[21:35] position dependent, not token dependent.
[21:37] It doesn't know the token at all. It
[21:39] just knows the position it is in the
[21:41] sequence of tokens. And based on that,
[21:42] it's going to start generating values.
[21:45] Great. So, it's using cosine and sign
[21:47] because I told you you don't have to
[21:48] know any math. This is the cosine and s
[21:51] wave illustrated in a chart. So, now you
[21:55] can kind of have an instinctive grasp of
[21:57] cosine and sign. they alternate but they
[21:59] alternate in such a way that they don't
[22:01] overlap unless like in the few points
[22:03] where they intersect great again we add
[22:06] a value and the large language model
[22:09] learns to recognize the value that we
[22:11] had as positional information
[22:14] I will also mention that beyond absolute
[22:16] positioning of which we're going to
[22:18] learn two types sinosoidal and learned
[22:21] values where there's also relative
[22:23] positioning we call that rope in short
[22:27] why do we need rope rope. Why can't we
[22:29] just use absolute positioning to our
[22:31] heart's content? Well, if you teach the
[22:33] model absolute position, it can't extend
[22:36] beyond the context size that it saw. If
[22:38] you taught it in a,024 context size,
[22:41] then it can't really extend to 1448 or a
[22:44] million because it's only learned those
[22:46] values. It's really hard for it to
[22:48] figure out new positional embeddings.
[22:51] Also, and this is like just a judgment
[22:54] call for me to say I don't think that
[22:56] absolute positioning really solves our
[22:59] original problem of men bites dog. Let's
[23:01] let's think about why men bite dog bites
[23:05] man. We decorate the dog with a symbol
[23:07] for one. We decorate bites with a symbol
[23:10] for two. We decorate men with a symbol
[23:12] for three. The model doesn't care about
[23:14] 1 2 3. What it wants to know is the
[23:17] relative position between dog and bites
[23:20] between man and bites. It wants to know
[23:23] that man is plus one position to bites.
[23:26] It wants to know the dog is minus one
[23:28] position to bites. That's just how
[23:30] English works. That designates the bitey
[23:32] and the bite. Right? That's the
[23:35] important thing. Why is that distinction
[23:37] important? Rope doesn't include absolute
[23:40] positions. It's only about the pair the
[23:43] relative position of pairs right and
[23:46] that happens in a slightly different
[23:48] point in the sequence than everything
[23:49] else. So that is how rope or relative
[23:53] positioning works. It rotates pairs
[23:56] based on their relative distance from
[23:58] each other. And here on the top left you
[24:00] can see the dimension the when you
[24:02] increase dimensions you can see how much
[24:05] we add to every pair as uh in comparison
[24:08] to to each other.
[24:11] Great. We're not going to see the
[24:12] formula for rope. We'll see it in Excel
[24:15] for a moment. I don't think I need to
[24:17] teach you that. I think you can read
[24:18] that one on your own. There will be an
[24:20] Excel example. I think focusing on
[24:22] absolute cenosodal positioning is
[24:24] already going to strain you today and
[24:26] like make you think a lot. But I did
[24:28] want to say rope exists. It's really
[24:30] critical to know that rope exists and
[24:31] absolute positioning is just not
[24:33] something most people do anymore. Great.
[24:36] So, let's jump into Excel. We've taught
[24:38] you a bunch of concepts and a bunch of
[24:40] uh and a bunch of techniques and a bunch
[24:42] of formulas. Let's try and do that
[24:44] together. Great. So, I have my Excel
[24:46] spreadsheet pulled up here.
[24:49] Uh first thing I want to do is I want to
[24:52] take the text the brown dog jumped over
[24:55] the lazy dog and I want to move it into
[24:58] token space. I want to like embed it
[25:00] just with token numbers, right? All they
[25:02] get is an int. Luckily for me, our our
[25:06] entire tokenizer happens to have our the
[25:09] sentence, the brown dog jumped over the
[25:10] lazy dog right here in the beginning.
[25:13] Why? Because I'm lazy and I didn't want
[25:14] to put it in different positions. But
[25:16] you can imagine that they're spread over
[25:18] the entire tokenizer. It just makes it
[25:20] easier for us to see 229 and kind of
[25:23] understand that's where our tokens live.
[25:26] Great. So, first thing I want to do is I
[25:28] want to translate this text into our
[25:31] token space. So, I'm going to click
[25:33] enter. Wow, that was really easy. Why?
[25:36] Because I made it really easy on myself.
[25:37] I just put them all sequentially here.
[25:39] They don't have to be sequential. But
[25:41] now I've translated strings into ins,
[25:43] which are the tokens. Great. So, the
[25:46] next step is we need an embedding
[25:48] metrics. How big is our embedding
[25:50] metrics? It is hidden dimension columns
[25:53] and it is vocabulary size rows. Right,
[25:57] great. Now I'm going to just generate a
[25:59] bunch of random numbers and throw them
[26:01] into this chart into this table.
[26:06] Great. Now I have a bunch of random
[26:08] numbers here. My gosh, this is much
[26:10] better. So now I have an embedding
[26:13] metrics and I have a bunch of tokens. We
[26:15] could see that the tokens here correlate
[26:17] to the tokens here. It becomes really
[26:19] obvious to us that we have to move these
[26:21] tokens, our sentence into embedding
[26:24] space. Great. So let's do that. First
[26:27] thing we'll do actually before we move
[26:29] it into embedding space is we'll do an
[26:31] unembedding metrics. What's an
[26:33] unembedding metrics you ask? Embedding
[26:36] metrics bring us from
[26:39] tokens into highdimensional space.
[26:42] Right? That happens at the beginning of
[26:44] every large language model. However, we
[26:46] also want to move from highdimensional
[26:48] space back into tokens which are can be
[26:51] translated into strings cuz we have to
[26:53] generate words at the end of our like
[26:55] large language model. So we have an
[26:57] unembedding metrics. One option is we
[26:59] could learn it. So it could just be a
[27:01] bunch of other random learned values. By
[27:04] the way, I should mention all of these
[27:05] values are learned values. The model
[27:07] learns the values of the embedding
[27:09] space. So that's one option. It could
[27:10] just be a bunch of other random values.
[27:13] That's not what GPT2 did. GP22 used uh
[27:17] tied embeddings. How do you tie
[27:19] embeddings of two matrix of like flipped
[27:22] dimensions? Effectively, you could just
[27:24] transpose. So the way that we do that is
[27:27] we take this this table, this matrix,
[27:31] this two-dimensional array, and we flip
[27:33] it. This point 4 ended up here. This
[27:37] 0.5 ended up down here. We flip it 90
[27:41] degrees. That's how I think of it.
[27:43] Columns become rows. Rows become
[27:44] columns. That is our unmbeding matrix.
[27:47] It's going to happen at the end of the
[27:48] large language model. Great. So now we
[27:51] want our input matrix. I kind of
[27:53] prefilled them ahead of time because I
[27:55] didn't want to like have to deal with
[27:56] these ellipsuses. I'm so sorry, but you
[27:59] could see that the brown dog jump over
[28:01] lady lazy fox end of string end of
[28:04] string end of strings, right? Petting
[28:05] petting petting whatever it is you want
[28:07] to put here. And then I moved our tokens
[28:10] that we had here into embedding space
[28:13] here. I used this as a reference
[28:15] dictionary and I combined our tokens and
[28:17] our embedding space. Wow. What's the
[28:20] exercise? Note how the input token IDs
[28:23] were merged with the input embeddings.
[28:25] Right? So I took our tokens and I put
[28:27] them in embedding space. Amazing. Now
[28:30] they're let's say in order
[28:34] of where they were in the sentence. But
[28:36] these high dimensional embeddings from
[28:39] the embedding metrics here that's just a
[28:42] big dictionary they don't contain any
[28:44] positional information for real. But
[28:45] their order in the of the rows does
[28:48] contain that. So now the question is can
[28:50] I translate the order of the rows into
[28:53] something here in this chart that I
[28:54] could do some fun like math on? The
[28:57] answer is yes absolutely. One would say
[28:59] it's positionally absolutely. Haha,
[29:02] little pun. How do we do that? We take
[29:05] our input embeddings. This, let's
[29:07] pretend our input embeddings was this
[29:09] matrix like this um 24 context size
[29:13] matrix by 24 hidden dimensions and I'm
[29:17] going to just add to it positional
[29:19] embeddings. How do you create a
[29:21] positional embedding matrix? Well, we
[29:23] saw this di this formula earlier. This
[29:26] is absolute cinosidal positions. For
[29:29] even numbers, we'll use sinus. For odd
[29:31] numbers, we'll use cosine. We'll take
[29:34] the column. We'll take the row. We'll
[29:36] end up doing some fun math here. And
[29:38] we'll see what happens. I'm not going to
[29:41] code this in front of you. This took me
[29:43] like, you know, a couple minutes to
[29:45] write, but I could just show this to you
[29:47] for a moment. And actually, you already
[29:48] have it on screen, right? If it if it's
[29:51] uh if the position is um even then use
[29:56] sinus. If it's not even use cosine and
[29:58] just follow the formula that's listed
[30:00] above here. Great. Now that we've done
[30:02] that, I'm going to equal sign. Sure.
[30:05] Fill up the entire column. And then I'm
[30:07] going to go ahead and drag that so it
[30:11] fills up our entire hidden dimensions.
[30:13] I'm going to zoom out a bit. Going to
[30:15] make this a bit smaller. Wow, that's
[30:18] such a pretty chart. Why is it so
[30:20] pretty? Some would say
[30:23] it's because it's using the cosine and
[30:25] sinus attributes to create what
[30:27] something that kind of looks like waves.
[30:30] Okay, waves. I don't really see it,
[30:31] Justin. Don't worry about it. We'll see
[30:33] it in a moment. So now I have my input
[30:36] embeddings that exist in highdimensional
[30:38] space but doesn't have positional
[30:39] information minus the fact that every
[30:42] row is ordered based on its order in the
[30:44] context size. Now I have positional
[30:46] embeddings. They don't know anything
[30:48] about our inputs. They don't know
[30:50] anything about our tokens. They just are
[30:52] going to get added on top, bolted on top
[30:55] to our input embeddings. I'm going to
[30:57] combine both of these with a fancy fancy
[31:00] this plus this.
[31:04] And that's it. That's positional
[31:06] embeddings. Great. Now that I did that,
[31:09] sure, you can autofill a bit if that
[31:11] helps you. I'm going to delete this one
[31:13] because I disagree with it. Going to
[31:15] drag this. We're going to drag this all
[31:17] the way to the Zed column. Oh no, you
[31:20] now know I'm Canadian because I said
[31:22] zed.
[31:24] Great. What do we see here? Honestly,
[31:27] kind of hard to see where the positional
[31:29] embeddings are. Why is that hard for us
[31:32] to see? Cuz we're not meant to see it.
[31:34] We just did an alteration in
[31:36] highdimensional space. In this case, 24
[31:39] dimensions in GPT2 small, which is what
[31:41] we're building. We'll be 768. kind of
[31:44] hard to see that we added patterns to
[31:46] this. Why is it hard for us to see?
[31:48] We're not highdimensional alien
[31:50] intelligences. The large language model
[31:52] is going to learn these. Cool. I'm going
[31:54] to take a moment to like, well, Justin,
[31:57] this is a really pretty table, but it's
[31:59] not as pretty as the one you had in the
[32:00] deck. Let's see what cinosal absolute
[32:04] positioning looks like when you actually
[32:05] give it like a little bit of room to
[32:06] breathe. More than 24x4.
[32:09] Oh my goodness, Justin. That's so I'm
[32:12] going to make this smaller. That's so
[32:14] pretty, right? Goodness. You could
[32:17] really see waves being emitted from the
[32:20] center here. I think that's super cool.
[32:22] This is a super creative solution to
[32:25] input embeddings then have positional
[32:26] information. We're just going to rotate
[32:28] every one of the token embeddings in
[32:31] three in highdimensional space. Great.
[32:33] I'm going to go back to our without
[32:35] answer sheet. Going to make this bigger
[32:36] again. Awesome. Awesome. So, I did tell
[32:40] you that rope exists. I'm not going to
[32:42] break down these formulas with you here.
[32:44] I just don't think that's a good use of
[32:46] our time. That would be an extra 10 uh
[32:48] sections here in Excel. What I will tell
[32:51] you is let's say you multiplied matrix
[32:53] one and matrix 2. Let's say this happens
[32:56] somewhere inside a thing called
[32:57] attention. I don't know what attention
[32:58] is. Maybe we learn about it in the very
[33:00] next section. I have the results of the
[33:02] math mold here. Now I can apply
[33:05] positional information to every pair.
[33:08] Every pair of these is going to learn
[33:09] something a little bit about each other.
[33:11] And then that's what rope does. I'm not
[33:14] going to break open these formulas with
[33:15] you. They are, let's just say, not
[33:18] trivial, but it's really worth for you
[33:20] to learn how rope works. I think it's
[33:21] great. And I even linked to some guides
[33:24] in the rope slide that explain how this
[33:26] works.
[33:28] Great. So we went through the Excel
[33:30] demo. We looked at a tokenizer. We
[33:32] looked at the embedding metrics. We
[33:34] looked at an unembedding matrix which is
[33:35] just uh transposed embeddings. If we
[33:38] have tied embeddings, tied embeddings.
[33:42] We looked at the input matrix which is
[33:43] taking the input tokens into embedding
[33:45] space. Then we saw absolute positional
[33:48] uh cinosodal encoding which is just
[33:51] adding those on top. And then we looked
[33:53] at rope. Uh rope is just a way of like
[33:56] having actual relative position as
[33:58] opposed to absolute position in a
[33:59] sentence. Great. Love that for us. None
[34:03] of that was code adjusted. Great. Let's
[34:05] look at a little bit of code.
[34:08] So, first thing we're going to do is
[34:10] we're going to pos we're going to uh
[34:12] print our embedding metric from GPT2,
[34:15] the real GPT2 small embedding matrix.
[34:23] So, we have a tokenizer which we're
[34:25] going to just load up from GPD2.
[34:28] We have our model. We're gonna go ahead
[34:30] and load those up.
[34:32] And then we have our embedding metrics.
[34:34] How do we get the embedding metrics
[34:36] specifically for CH G for GPT2? It lives
[34:40] in U property called WTE. You don't have
[34:44] to remember that. I just happen to
[34:46] remember that in my head because I've
[34:48] done so many things with GPT2, but you
[34:50] could always just look at the GPT2
[34:53] summary or the GPT2 print and then you
[34:55] can kind of figure it out. Great. So,
[34:57] how big is that? That's 50,257
[35:01] by 768.
[35:03] 768 hidden dimensions. That's what we we
[35:06] said GPT2 small has. What's this 50,000
[35:09] whatever number? That is the token uh
[35:12] token vocabulary size. We remember in
[35:15] the previous section we heard the number
[35:18] one thing Karpathy did to speed up his
[35:20] GBD2 trainings is move this to a
[35:23] multiplication of 64. Why is that
[35:25] relevant? It makes a lot of matrix
[35:27] multiplication. Use the GPU a lot better
[35:30] depending on which GPU you're on. But
[35:32] still very very helpful specifically an
[35:33] A100. Okay. So let's take the first,024
[35:38] of these. We're not going to review
[35:39] 50,000. That seems excessive. But let's
[35:42] look at the first,024 embeddings.
[35:45] Here we go. Here we get to see that this
[35:48] is the token ID. token ID zero
[35:51] translates to the token exclamation mark
[35:53] and is represented in high dimensional
[35:55] space with 768 dimensions in such a way
[36:00] can you read that I definitely can't
[36:02] read that but maybe we could do
[36:04] something to represent that later on so
[36:07] let's go over this again I think it's
[36:09] really critical to learn tokenizer
[36:12] embeddings strings what's happening here
[36:14] so really the path we're going in when
[36:17] we enter a large language model a string
[36:20] gets translated to token which is just
[36:22] an int gets translated to embedding
[36:24] which is just a highdimensional array.
[36:26] Great. So I take the text hello world
[36:29] I'm here
[36:30] and I'm going to invoke my GPT2
[36:32] tokenizer and I'm going to say max
[36:35] length kind of maybe even let's call it
[36:36] context size is going to be like take my
[36:40] text embed and create return back a
[36:41] 10,000 sorry a 1,024 array. Uh then
[36:46] we're going to have our token ids. Those
[36:48] are the encoded ids and then we're going
[36:51] to go ahead and convert those to uh uh
[36:55] to something that we can read later on.
[36:57] I'm going to go into model WTE which we
[36:59] said is our embeddings. I'm going to
[37:01] give it my token ids and I'm going to
[37:03] get the 768 array that represents that.
[37:07] What does that look like? Hello world.
[37:09] I'm here. Hello token number 15,496.
[37:15] World token number 995
[37:18] and this is the highdimensional
[37:20] representation. How do I know that?
[37:22] Let's just remember that world had
[37:24] minus5
[37:26] as the first thing. Earlier we printed
[37:29] the first thousand things from our
[37:30] tokens. So I'm going to just scroll
[37:32] aggressively until we get to token 995.
[37:36] Token 995.
[37:38] Scroll scroll scroll scroll scroll.
[37:40] Token 995.
[37:43] world minus.15.
[37:47] We're very cool. This is just the
[37:49] general embedding space dictionary. Now
[37:52] we have an input embeddings that's
[37:53] specific to us that matches our tokens
[37:57] in that embedding space. Very cool. So
[38:00] that's our context size multiplied by
[38:03] our uh sorry the dimensions are the
[38:06] context size by the hidden dimension
[38:08] size. Great. So now we say we have a
[38:11] bunch of these numbers. What do they
[38:13] mean? Let's do a bit of analogy vector
[38:15] work. So you remember we had our like
[38:18] king, queen, man, woman, what was going
[38:20] on there. Uh we have our queen uh
[38:25] vector. So we could take our tokenizer.
[38:27] We can encode queen and we can get the
[38:29] embeddings for queen from the uh from
[38:33] the
[38:35] embedding metrics. So now I have the 768
[38:39] dimensional array that represents the
[38:41] word queen, right? I'm going to find the
[38:44] similar tokens. This uses something
[38:46] called cosine similarity. I'm not going
[38:48] to teach you about co similarity, but it
[38:51] just finds the nearest item in space in
[38:54] a highdimensional space or really any
[38:56] dimensional space because it just uses
[38:58] cosine and angles. Uh, then I'm going to
[39:01] find the top the top ones and I'm going
[39:03] to find the nearest one to queen. The
[39:05] nearest token to queen that isn't queen
[39:08] in different spellings with different
[39:10] spaces ends up being king. That's really
[39:13] cool. In embedding space, if you look
[39:15] for out of the 50,000 other tokens that
[39:18] the embedding matrix for GPT2 learn, the
[39:21] nearest token to queen is king. That's
[39:24] something really cool to think about.
[39:27] Great. So that's one thing we learned.
[39:30] What's something else we learned? Let's
[39:32] say I take the vector for queen, the
[39:34] vector for woman, and the vector for
[39:35] men. If I take vector for queen minus
[39:39] the vector for woman plus the vector for
[39:41] men, where did we end up? It kind of
[39:45] equals
[39:47] king. That's really cool. Queen minus
[39:50] women plus men equals king. That's
[39:53] something that happens just in embedding
[39:55] space. We don't have to activate our
[39:56] large language models yet. our embedding
[39:58] space can do some amount of analogies
[40:00] which is really really cool this to this
[40:03] like this is like this to this very cool
[40:07] and then when we read the vectors though
[40:09] it doesn't really tell us a lot about
[40:11] them we can't fully see that but maybe
[40:14] if we do some PCA on these four vectors
[40:17] we can so I'm going to do PCA and then
[40:20] I'm going to try and visualize it this
[40:22] is where our chart came from uh inside
[40:25] of our slideex so PCA AFGPT2 embeddings
[40:28] for woman, queen, man and king, woman
[40:32] and queen exist in highdimensional space
[40:35] roughly within the same direction and uh
[40:38] and direction and distance from man and
[40:42] king. We learned that earlier. Now we
[40:44] fully understand that. That's so cool
[40:46] that we could do that just in embedding
[40:48] space.
[40:50] Great. So now we let's move on to
[40:53] positional embeddings. I kind of lied to
[40:55] you about cenosortal embeddings. I only
[40:57] taught you cenosodal embeddings. There's
[40:59] a totally different option that GPT2 was
[41:02] actually trained on. It just had its own
[41:05] positional embeddings uh that it learned
[41:08] later on. It didn't use cinosodal
[41:10] embeddings. It just had another massive
[41:12] matrix that it had to learn. Not super
[41:16] great because now that's another matrix
[41:18] that you have to learn. You have to back
[41:19] propagate on. Takes a bunch of your
[41:21] memory. It takes a bunch of your compute
[41:24] in. So, but that is how GPT2 trained it.
[41:27] So, that was a learned absolute
[41:29] positioning. No one uses these anymore
[41:31] as far as I know, but maybe worth
[41:34] looking at the future chart where we see
[41:35] if anyone still uses these.
[41:38] Another option we have is we can apply
[41:41] absolute sinosortal embeddings. So, we
[41:43] don't have to learn a positional
[41:45] embedding matrix or positional encoding
[41:47] matrix. Uh and the way we do that is we
[41:51] implement the math that we saw earlier.
[41:53] So we're going to have our sinus and
[41:56] cosine depending on whether or not it's
[41:59] even or odd. This is kind of the numpy
[42:01] format to say even or odd out of uh the
[42:05] number two. You don't I'm not going to
[42:07] teach you this format. This is like a
[42:09] thing that Python does uh in numpy. It's
[42:12] a really great format. You should learn
[42:14] numpy independently from this one uh
[42:16] workshop. really important to just see
[42:18] at the end. We calculate a positional
[42:20] embeddings with cosine and sinus for for
[42:22] absolute and not absolute using this
[42:24] formula that we saw earlier with uh
[42:27] absolute possal positional embeddings.
[42:30] All we do with it embeddings plus
[42:32] positional embeddings that is it we're
[42:35] just adding those together pie-wise.
[42:38] Great. So let's try and visualize. Let's
[42:41] start by visualizing the and you don't
[42:43] have to know the visualization code. I
[42:44] don't think it's helpful for you. Let's
[42:46] try and visualize the GPT2 learned
[42:49] embeddings at least the first 100.
[42:52] Can you see the pattern here? Man,
[42:55] that's kind of hard. I can barely see
[42:56] the pattern. There is a pattern here.
[42:58] People have analyzed it. Kind of hard to
[43:01] see it. Not super obvious, but you can
[43:03] see maybe there's a pattern of how
[43:05] strong this line is and how strong this
[43:08] line is. And then we add that to our
[43:10] embedding metrics because this is not
[43:12] super interpretable. And also we had to
[43:14] learn all of these. That's kind of a lot
[43:17] to learn. We have to learn context size
[43:19] by embedding dimensions array. That's a
[43:21] pretty big array to learn. Maybe we
[43:23] don't have to learn it at all. We could
[43:25] just go ahead and use positional abs
[43:28] absolute positional cenosodal encoding.
[43:31] Uh there is a pattern here. You can kind
[43:33] of see it if you look at the waveform.
[43:35] If you're really really good at
[43:38] computers or really good at physics, you
[43:40] can maybe tell that it kind of learns
[43:42] something that is akin maybe a little
[43:45] bit to uh to fouryear transforms. That's
[43:48] what people tell me is here. When I look
[43:50] at that, I'm struggling to see it, but
[43:52] people have told me that that's what's
[43:54] in here or at least that's what some
[43:55] papers have claimed. Great. So now we
[43:57] can uh try and visualize the positional
[44:01] uh centural embeddings. Those are the
[44:03] ones we don't learn.
[44:05] Oh my god, look at this. This is so
[44:08] gorgeous. Is that a diagram? It looks
[44:10] like I threw a rock in a pond. My god,
[44:12] the sinuses, the cosiness, they sing to
[44:15] me. Much easier. You don't have to learn
[44:17] these. A lot less work in back prop.
[44:20] Less memory we need to load the model.
[44:21] Less compute we have to learn. Can I
[44:24] read this? And is this slightly human
[44:26] interpretable? My goodness, this is so
[44:28] much more interpretable. When we look at
[44:30] dimension 10, 50, 100, 200, the pattern
[44:33] is actually pretty clear. This is what
[44:35] the large language model is going to
[44:37] learn from. We overlay these on each
[44:39] other in let's say a 4year transform
[44:41] kind of way. My goodness, that's really
[44:44] really cool. Okay, so that was a little
[44:47] bit of mechanistic interpretability of
[44:49] what we see when we see positional
[44:51] embedding specifically cinosal and tide.
[44:54] So that was code. Okay, so let's make a
[44:56] couple of decisions. If we look at the
[44:59] top right chart, I took 10 2025 article
[45:04] that that was actually a blog post and
[45:06] then I took the 53 LLMs that they
[45:09] learned and then I kind of like just had
[45:11] Claude, hey Claude, can you just
[45:12] generate like a really nice chart that
[45:14] could use to visualize what do people
[45:16] actually use? Well, 2017 we used
[45:20] sinosal positioning or learned
[45:23] positioning. Then we moved on to uh uh
[45:26] absolute cenosal position and from so on
[45:29] we started moving closer and closer into
[45:32] rope. Very cool to see that right.
[45:36] Uh and then no like we had a couple of
[45:39] examples of learn absolute but really
[45:41] what people are using nowadays is rope.
[45:44] So we're not going to try and do
[45:46] absolute learn positioning. We're not
[45:48] going to try and do absolute uh
[45:50] sinosoidal positioning. What we are
[45:52] going to use is rope. even though you
[45:54] didn't fully understand how it works,
[45:56] but you do understand it's relative to
[45:58] how each every one of the pairs relates
[46:01] to each other. So that's what we're
[46:04] going to use. We're also going to now
[46:06] that we learned about embedding metrics,
[46:08] we've decided to have one of those. We
[46:11] don't really have a choice, but we've
[46:13] chosen to have one. And unmbeding
[46:15] metrics, we've chosen for our large
[46:17] language model that we're going to train
[46:19] here today to have tied embeddings. How
[46:21] are we going to tie them? are just going
[46:22] to transpose and flip the embeddings. Is
[46:25] that common? Not really. Not super. Not
[46:30] super easy to do. Some people still have
[46:32] non-ti embeddings. It really depends on
[46:35] what you're trying to do and how much
[46:37] compute and memory you have. There's a
[46:39] lot of disagreement on that. I'm not
[46:40] going to open that up. Great.
[46:42] Hyperparameters.
[46:44] We're going to use a context size of
[46:46] 1,024. That's a laughably small amount
[46:49] of words that we could support. Maybe
[46:51] it's like 500 750 words, but it's enough
[46:55] for us to like be able to train our
[46:57] large languard models relatively quick.
[46:59] If we double the context size, we might
[47:02] also end up doubling our training time.
[47:04] Not exactly. That's not how it works,
[47:06] but we're definitely going to need more
[47:08] parameters for our model. Finally, we
[47:11] have our hidden dimension 768.
[47:14] That's the smallest hidden dimension in
[47:16] GPT2. That's GPT2 small. And we're going
[47:18] to use that. Now, if you but if you look
[47:21] at the bottom right chart, you're going
[47:23] to see 10 2025 blog post. I also asked
[47:27] it, hey, what kind of attention are
[47:29] people using? What's attention? Not
[47:32] super clear. Maybe we're going to learn
[47:34] that in just the next section, but it's
[47:37] clear that people started using
[47:38] something called MHA and then they moved
[47:40] to GQA very very soon after. But some
[47:44] people still use MHA. So, it's totally
[47:46] fine for us to use MHA as well. What's
[47:50] the next thing we're going to learn?
[47:51] Attention. Attention is the magic that
[47:53] makes all transformers, all large
[47:55] language models today kind of work.
[47:57] Maybe it'll get deceated at some point
[48:00] in the future. Doesn't look like it's
[48:02] going to happen anytime soon. So,
[48:04] critical to learn about attention.
[48:07] Great. So, what did we learn about
[48:09] embedding metrics? We learned about
[48:10] embedding metrics, unmbedding metrics,
[48:12] contact size, vocabulary size, head and
[48:14] dimension size, bat size. We learned all
[48:17] of those hyperparameters. We learned
[48:19] about positional embeddings. We sorry,
[48:21] positional encodings. We learned about
[48:23] absolute positional encodings. We
[48:25] learned about learn positional
[48:27] encodings. We learned about relative
[48:29] positional encodings. And we've made
[48:31] some decisions about our architecture.
[48:33] Next up, we're going to move up to
[48:34] attention, the secret sauce of
[48:36] transformers. I hope you join me for the
[48:38] next section. as well.
