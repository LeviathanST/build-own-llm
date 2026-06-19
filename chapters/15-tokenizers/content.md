# Tokenizers | Build Your Own LLM Workshop #15

**Build Your Own LLM Workshop — Video #15 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 30m 47s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=TPPhTqPu_Yg |

## Description

No description available.

---

## Full Transcript

[00:00] Hello everyone. Welcome back to uh
[00:04] building your own large language model
[00:06] with me Justin Angel. Today we're going
[00:08] to be covering uh section 15 which is
[00:11] all about tokenizers. Tokenizers are
[00:14] here to solve the problem of how do we
[00:17] take text into a deep neural network
[00:20] which we now know is all just a bunch of
[00:21] numbers. Before we get started on that,
[00:24] I do want to highlight that now from
[00:26] section 15 all the way to the end of
[00:27] this workshop, section 23, everything's
[00:30] going to be about large language models.
[00:32] So, we started with like very general
[00:34] machine learning model concepts. We
[00:36] worked our way to deep neural networks
[00:38] and now we're all the way in large
[00:40] language models land. Okay, great. So,
[00:43] let's start with tokenizers.
[00:45] The first thing that we could see here
[00:47] is that we have a problems, right? Large
[00:50] language models and deep neural networks
[00:52] in general and you know anything with
[00:53] perceptrons use numbers but language
[00:57] uses strings right. So how do we send
[00:59] text to deep neural networks? How do we
[01:01] get text out of deep neural networks?
[01:04] Right? We want to take a round peg and
[01:06] put it into a square hole and
[01:08] effectively
[01:09] that little gap in the metaphor between
[01:11] the round peg and the square hole that
[01:14] is where uh tokenizes come in. I
[01:16] actually think that's a really apt
[01:18] metaphor because it leaves a lot of
[01:20] edges that we're going to have to think
[01:22] about here and we're really going to
[01:23] spend this whole section thinking about
[01:25] those edges. So tokenizers will convert
[01:28] between strings and int right
[01:29] birectionally from strings to ints and
[01:31] from ins back to strings. Uh later on in
[01:34] section 15 we're going to learn about
[01:36] embaiting matrixes. What are those?
[01:38] Those are going to help convert those
[01:40] ins to like a bigger representation that
[01:44] is going to be more understandable by
[01:46] the large language model. But for now,
[01:49] you don't have to know about embedding
[01:51] metrics. What you have to think about is
[01:53] how tokenizers work. So one thing that
[01:55] we can know about tokenizers right away
[01:58] is they could be a single character like
[02:00] the word ah, right? the singular uh
[02:04] pronoun in English. Uh or it could be an
[02:07] exclamation mark. Or it could be a whole
[02:09] world, a whole a whole word like hello
[02:13] world. Or it could be a subword like
[02:15] parts of hell and o hello hello. Right?
[02:19] So that's something we could do. In
[02:21] order to really make this make sense for
[02:23] us, I'm going to open up the tick
[02:24] tokenizer demo. Um this is the tokenizer
[02:28] that's used by GPT2. So, it's actually
[02:30] really useful for us to get used to it
[02:32] because that's going to be the tokenizer
[02:33] that we're going to be using for our
[02:35] large language model that we're going to
[02:37] pre-train. So, let's start by writing
[02:39] hello world. And you could see that as
[02:42] I'm writing that,
[02:45] we have things that are converting that
[02:47] are converted from strings to ins. So,
[02:51] as I'm typing that, one thing that it
[02:53] definitely is not going to be a full uh
[02:55] a full token is going to be my name,
[02:58] Justin. So, I'm going to write that down
[03:00] right now. Oh, no, it is a full token.
[03:03] It's so common that the Tik Tok annizer
[03:05] for GPT2 actually has that. Let's try
[03:08] and think about a word that isn't a full
[03:10] token. Let's try and think about maybe
[03:12] me misspelling the word message. And I'm
[03:16] going to write it with one a with one s.
[03:18] And you could see now, oh no, I I wrote
[03:21] the word message incorrectly. I also
[03:23] wrote massage incorrectly realistically,
[03:25] right? it had to take two subwords and
[03:27] combine them together. A lot of words
[03:30] are subword combinations, right? That's
[03:32] something that's really important to
[03:34] realize. I recommend you go use this uh
[03:37] demo right now, tik
[03:38] tokenizer.verell.app,
[03:40] and try and see if you can't um uh get a
[03:43] more intuitive feel for how we build up
[03:46] subwords into full words in the tick
[03:49] tokenizer, specifically in the fully
[03:50] trained GPT tokenizer. So going back
[03:53] here, what we just learned is that full
[03:55] words um are token could be tokens. Half
[03:59] of words, subwords could be like it
[04:02] doesn't have to be half could be any
[04:03] portion of a word. Subwords could be
[04:06] tokens.
[04:07] Single to single characters could also
[04:09] be tokens. Why is that? Well, let's
[04:12] think about how we would build our
[04:14] tokenizer from scratch. The easiest way
[04:16] to build a tokenizer is either make it
[04:18] character-based or word based. So, let's
[04:20] try and explore those options and get to
[04:22] how tick tokenizer is built. The GPT2
[04:25] tokenizer.
[04:26] Great. So, the easiest thing for me to
[04:29] do is build my tokenizer by character,
[04:31] right? I just say every every single
[04:34] character is going to be a token. That
[04:37] makes it really easy for me. How many
[04:39] tokens are there realistically? Let's
[04:40] say I'm in asculand. Let's say 140
[04:44] characters, right? We take all of the
[04:45] English uh lower case uppercase letters,
[04:48] a couple of numbers, a couple of
[04:49] punctuation marks. Bam, we're at 140
[04:51] characters. Okay? Or some number that's
[04:55] very low like that. So, that's the
[04:56] easiest thing we could do. Um, we
[04:59] examine the entire token. We still want
[05:01] to train a tokenizer, right? We look at
[05:03] the entire corpus. Corpus is just a way
[05:05] of saying our entire tech collection of
[05:07] text. And then we're going to uh, let's
[05:09] say that we're in English. We're going
[05:11] to find the English characters. Let's
[05:12] say that we're in um a sematic language
[05:15] like Arabic. We're going to find their
[05:17] characters
[05:19] and then we're going to create a unique
[05:21] dictionary or unique list of just those.
[05:23] We'll assign each of those into a
[05:25] dictionary with like an ID and that's
[05:27] effectively how we build a
[05:29] character-based tokenizer. So, we'll
[05:31] assign a character per uh we'll assign a
[05:34] an ID per character that is used here.
[05:37] Why is that a really bad idea to build
[05:39] your um to build your tokenizer pair
[05:42] character? Well, one, it's super
[05:44] inefficient, right? We are going to
[05:46] actually have the opposite of
[05:48] compression when we build our
[05:51] pair character tokenizer. How? So, I
[05:55] take the word hello, which is five
[05:57] characters, and I convert it into f uh
[06:00] into which is one word, five characters,
[06:02] and I'm going to convert it into five
[06:04] tokens. That's kind of inefficient when
[06:07] you think about it, right?
[06:10] Um, effectively what that tells us is
[06:13] that we got negative compression, right?
[06:15] So, if let's say I took the first, let's
[06:18] say I took a 100,000 words, that's what
[06:20] you're going to see here on the left in
[06:21] the statistics, and then I said, okay,
[06:23] these 100,000 words actually have
[06:25] 612,000
[06:27] characters. Uh, the vocabulary size is
[06:31] 140. That gets me to a compression ratio
[06:33] of 6.12. That is negative compression by
[06:37] six times bigger. Not great at all.
[06:39] Right? So ma and why is that bad for us?
[06:44] One, we uh we have much larger token
[06:50] token inputs that we're going to have
[06:51] into build into our network. So our
[06:54] networks can now have to handle six
[06:56] times less uh inputs, right? Cuz now the
[06:59] inputs are bigger and our contact size
[07:01] is set. You don't know what a context
[07:02] size is, but it means your context size
[07:05] can only support less words in general.
[07:08] Another reason why that's really bad,
[07:09] the first set of layers in the network
[07:11] are going to have to like recombine all
[07:13] of these single tokens into semantic
[07:16] words and then semantic and then the
[07:18] platonic meaning and then it's going to
[07:20] have to reason. But we're going to waste
[07:22] a bunch of layers about recombining
[07:24] these words and then find their
[07:26] meanings. Not super great at all. Okay,
[07:29] so that was the easiest option. that for
[07:32] me to think about another option if pair
[07:35] character doesn't work why don't we just
[07:36] build it per word right that makes it
[07:39] like the next easiest available option
[07:42] so let's say that I have my 100,000
[07:44] words that I chose from something called
[07:46] fine web edu you don't need to know
[07:48] where I got my 100,000 words from let
[07:51] then I'm going to check what my
[07:52] vocabulary unique vocabulary is I'm
[07:55] going to have about 21,000 words so
[07:57] that's almost a 5:1 compression ratio
[08:00] that's any like that is a reduction of
[08:03] almost 80% in size. That's actually a
[08:05] pretty good compression when you think
[08:07] about it. Pair word compression is
[08:09] probably going to be the best you're
[08:11] going to be able to get on text, right?
[08:13] If every word is its own uh if every
[08:16] word is its own token, that means that
[08:18] we're going to have pretty good
[08:20] compression ratio. So if you think about
[08:22] the difference between pair character
[08:24] tokenizer that got six times more needed
[08:28] six times more space whereas pair word
[08:31] uh actually needs five times less space
[08:34] in the input. Now my context size which
[08:36] is fixed can handle five times more
[08:38] things. That's almost a 30x difference
[08:40] in size. That is very meaningful
[08:43] compared to the fully knowing that our
[08:45] large language models sometimes want to
[08:47] just like books and transcripts and the
[08:49] internet. So, there's a lot in there.
[08:53] Why is pair word tokenizer not good if
[08:56] it has this great compression ratio,
[08:58] right? Amazing compression ratio. Well,
[09:00] there's a tradeoff here, right? Um,
[09:03] we're going to have to have a massive
[09:05] embedding metrics. What's an embedding
[09:06] metrics? We don't know. But an embedding
[09:09] metrics is the thing that follows a
[09:11] tokenizer that translates the ins into
[09:13] something that makes sense to the large
[09:15] language model. Why is it bad to have a
[09:17] very very big a very very big embedding
[09:20] metrics? Well, if we look at this chart
[09:22] on the bottom right, when we look at
[09:24] GPT2 small, we can see the token
[09:26] embeddings are actually 31% of all of
[09:30] the learned weights, right? Before we
[09:31] get to all of the fun metrics,
[09:33] multiplication, ru growing, shrinking,
[09:35] all of that stuff, we already lost a
[09:37] third of our learnable parameter size
[09:40] just to token embeddings. If we're going
[09:42] to make every word a tok a token, we're
[09:45] going to use massive amounts of the
[09:47] networks on just token embeddings.
[09:50] Really, even if our network is massive,
[09:51] we're going to waste so much room. Why
[09:53] is that bad? A lot of words are super
[09:55] uncommon, right? The longest word in the
[09:58] English language, I'm going to try and
[09:59] pronounce it. Hold on. Super
[10:01] fragileicious. Maybe I didn't do that
[10:04] correctly. Is a very uncommon word. Um,
[10:07] I think the actual longest word is the
[10:09] name of a disease. That one is also
[10:11] super super uncommon. Why would we give
[10:13] a super super super super uncommon word
[10:16] like super fragileicious the same
[10:18] importance as we do a word that is super
[10:21] common like hello and world and big and
[10:24] small and hot and cold. Those are words
[10:27] that going to definitely going to need a
[10:28] token. So the sensitive embedding
[10:31] metrics is already a really sizable
[10:33] portion of our learned weights and we
[10:36] don't want to waste a bunch of memory
[10:38] space. Remember, we're memory constraint
[10:40] or compute constraint, but we don't want
[10:42] to waste a bunch of compute pair word on
[10:44] words that are super uncommon. So maybe
[10:46] there's some sort of compromise that we
[10:49] can get between pair character and pair
[10:52] word tokenizers. Here we go. I call
[10:54] these compromised tokenizers. No one
[10:57] else calls them that, but in my mind,
[10:59] they're called compromised tokenizers.
[11:01] And then basically what we're going to
[11:02] do is we're going to start up a pair
[11:04] character and then we're going to build
[11:06] up to subwords or maybe whole words. We
[11:09] are not going to go back from words to
[11:11] something that makes sense. We're going
[11:12] to start off at like our characters and
[11:14] then build it up based on how much time
[11:16] we want to spend doing uh doing the
[11:19] buildup. So what's the most common
[11:22] tokenizer that we're going to use here?
[11:24] It's called BPE. We're going to
[11:26] implement it ourselves in a moment. But
[11:28] the way to think about it is we start
[11:30] off at the smallest token pairs and then
[11:32] we're going to build up our way into
[11:34] having subwords and then maybe even
[11:36] whole whole words. There are
[11:39] alternatives to BP that no one almost
[11:41] ever talks about in large language
[11:42] models. Uh one of them is sentence
[11:45] piece. That one actually handles uh
[11:48] subword components in words that uh have
[11:51] different characters combined into
[11:53] different subwords that can't be split
[11:54] apart like Japanese and Korean and
[11:56] Chinese. So, actually kind of important
[11:58] to know about that. Maybe we need to do
[12:00] something if we're going to support
[12:01] those languages.
[12:03] So, what does it mean to build up
[12:05] things? Let's go to bp-vvisualizer.com
[12:08] and I'm going to delete the stuff that
[12:10] came out here and we're going to write
[12:12] the word merge me exclamation mark. When
[12:15] we look at merge me, sorry, I want to
[12:17] use lowercase merge. uh when I write
[12:21] merge me there's almost obviously an
[12:24] easy first thing that we can merge here
[12:26] it's me
[12:28] in the beginning of merge and the
[12:30] beginning of me or like the whole word
[12:33] of me can should should be the first
[12:35] thing that we merge. So I'm going to
[12:36] zoom in a bit here so you can maybe see
[12:38] this a bit better. First thing I'm going
[12:40] to do here is I'm going to take me I'm
[12:43] going to notice that that's the most
[12:44] common co- occurrence and then I'm going
[12:46] to merge it. Bam. So now let's say that
[12:50] I wanted a BPE with only one round. That
[12:53] is one round of BPE. This is going to be
[12:55] my tokenizer. You know, it's a tokenizer
[12:57] with only uh with only a bunch of
[13:00] characters and one subword word
[13:03] component.
[13:05] Uh we could keep running this. We don't
[13:07] have any more things we can merge,
[13:09] right? Mr. is just going to get merged
[13:11] because it's the next best thing here.
[13:13] We're going to try and merge that and so
[13:14] on and so forth. Now I have a tokenizer
[13:17] with a bunch of characters. One word
[13:19] that is me and one sub word that is me,
[13:24] right? And it's going to keep going that
[13:25] way. Okay. So let's try something
[13:26] slightly more complicated. Let's see if
[13:29] I can't merge hello world. The first
[13:31] thing I'm going to merge is he. Right?
[13:33] Again, there's not a lot of repeating
[13:35] value here. It's going to merge re and
[13:38] so on. So the quick brown fox jumps over
[13:40] the lazy dog. Let's try and run that.
[13:42] And we could see that it's going to
[13:44] start finding pairs and merge those
[13:46] together. When is it going to stop? It's
[13:48] going to stop either when it runs out of
[13:50] possible merges or when it arrives at
[13:52] the maximum number of merges that we
[13:54] said that it should do and so on and so
[13:57] forth. And already you could see that
[13:59] it's doing a bunch of merges here.
[14:01] Great. So I'm going to go back into uh
[14:03] our slide deck and then we're going to
[14:06] see a bunch of code for tokenizers.
[14:10] And now we don't have a deep neural
[14:11] network anymore. We're not keeping uh
[14:13] those from section 14 all the way from
[14:15] section 10 to 14. But we do have our
[14:19] tokenizer code. So the first thing we're
[14:21] going to do is we're going to load our
[14:22] GPT2 tokenizer. Um that is from hugging
[14:27] face. We're not using Tik Tok tokenizer
[14:28] here, but pretty close. They're both
[14:30] going to perform pretty similarly. Uh so
[14:33] I have tokenizer here. First thing I'm
[14:36] going to do, I loaded it up from hugging
[14:38] face. I'm going to take the tokenizer
[14:40] vocabulary and I'm going to print out
[14:41] the entire token vocabulary into a dataf
[14:45] frame here. A data frame is just going
[14:46] to print really pretty. That's why I use
[14:48] data frames.
[14:50] So you can see the first token is
[14:51] exclamation mark. The second token is uh
[14:54] parentheses and so on and so forth. So a
[14:57] bunch of uh punctuation marks are going
[15:00] to be the first thing here. Then it's
[15:01] going to be uppercase letters then
[15:03] lowerase letter then a bunch of other
[15:05] punctuation marks then lowerase letter
[15:07] and so on. Let's see where the world
[15:09] world goes here is going to be at token
[15:13] number 995. Right. So here you could see
[15:16] portions of subboard like inter
[15:19] interdependency international that's a
[15:22] fun subword. Uh interworld interloper.
[15:26] So that's a subword. So over here you
[15:28] can see the subwords and words. Some
[15:30] subwords are words right? Like the
[15:32] important thing is that they're all
[15:33] tokens. Great. So you can see we have a
[15:35] bunch of these here.
[15:38] Um, next up we're going to try and use
[15:41] the tokenizer to tokenize a few inputs.
[15:45] So the first thing I do is I call
[15:46] tokenizer.incode. I give it a string and
[15:49] it's going to go ahead and convert these
[15:52] two token two tokens. I'm also replacing
[15:55] this character here which is used
[15:57] instead of a space just to make this a
[15:59] little bit more readable for us because
[16:00] it does embed spaces directly into
[16:03] tokens. So what do we have here? Hello
[16:05] world. I'm super fragileicious.
[16:07] Expeditulosious.
[16:09] Great. Now maybe I pronounced it
[16:11] correctly. Hello world. Each one of
[16:13] these is a word. A punctuation mark. I'm
[16:16] because it decided to crop it here. And
[16:18] then it did a bunch of subwords. Really
[16:21] interesting to note. BPE ends up being
[16:24] kind of a mixed mode between full words
[16:26] and subwords and tokens. And that's kind
[16:29] of why it's a compromised tokenizer in
[16:31] my mind. Great. So, next up, we probably
[16:35] want to have uh a pair character
[16:38] tokenizer. So, the first thing I'm going
[16:39] to do is I'm going to load up a 100,000
[16:42] token 100,000 awards. I'm going to load
[16:44] it from a thing called fine web edu. You
[16:47] don't have to know what fine web edu is.
[16:49] We're going to find out about it once we
[16:50] get to pre-training section 20. But this
[16:52] might be the first time you see me load
[16:54] up the data set that we're going to use
[16:56] for pre-training, which is fine web edu.
[16:59] So, let's try and read. So, I got
[17:00] 100,000 awards. Let's try and read the
[17:02] first couple of words. The independent
[17:04] Jane for all of love, romance and
[17:07] scandal and Jane Austin's book. What
[17:08] they really about is freedom. So on and
[17:11] so forth. So now I have that data set. I
[17:14] have 100,000 awards. Let's use it to
[17:17] train to build to create a tokenizer
[17:21] that we can use later. The first
[17:23] tokenizer we're going to build is a by
[17:25] character tokenizer. Notice that I
[17:27] organized it into like init and encode
[17:30] decode method. Since I'm not inheriting
[17:32] from any class here, I could have
[17:33] whatever function names I want. I still
[17:36] like using init, encode, and decode. I'm
[17:38] also going to like do the training,
[17:41] right? Like the building up of this
[17:43] within the initializer because I know
[17:44] it's going to be pretty quick. Great.
[17:46] So, it gets a text corpus. It's going to
[17:49] get the characters, the unique
[17:51] characters sorted in a list. It's going
[17:53] to get the vocabulary settings, which is
[17:55] how many unique characters it found.
[17:57] Then it's going to assign every
[17:58] character it found a uh int. It's going
[18:02] to assign every int a character. So now
[18:03] I have birectional dictionary that I can
[18:05] use for easy retrieval and run and
[18:07] inference time.
[18:10] Encode is just going to use character to
[18:11] int. And decode is going to use int to
[18:15] character those dictionaries we just
[18:17] built. Great. So overall what's my
[18:19] corpus length? It's uh from 100,000
[18:22] words I went to 612,000
[18:25] characters. I have 140 characters total
[18:28] and then that's how we got to a
[18:29] compression ratio earlier of 6.12.
[18:32] Uh now I could take that tokenizer
[18:34] that's fully trained and I could try and
[18:35] convert hello world. What is it going to
[18:37] do? Actually it's going to break up
[18:40] every single character to its own token
[18:42] which is kind of what we expected. Uh
[18:44] amazing great. So now we have that.
[18:46] That's a pair character tokenizer. We've
[18:49] talked about why those don't make sense.
[18:50] they don't make sense because they uh
[18:52] make the first layers of a large
[18:54] language models do all the merges for
[18:56] for word meaning. They're also um not
[19:00] super helpful when it comes to
[19:04] compression, right? So our compression
[19:06] ratio is actually pretty bad. It's
[19:08] negative. Okay, so the other thing we're
[19:10] going to try and build here is a by word
[19:12] tokenizer. Again, it takes in a whole
[19:14] text corpus. It finds the unique words.
[19:17] Earlier we found unique characters. Now
[19:19] it finds unique words. How does it do
[19:21] that? It splits on spaces. That maybe
[19:24] doesn't make sense for non-English or
[19:26] non-romantic based languages, but uh
[19:29] does make sense for most languages we're
[19:31] going to be working with in fine web edu
[19:33] or at least this English language
[19:35] corpus. Uh and again, we're going to do
[19:38] the same thing. We're going to have a
[19:39] word toint dictionary that does uh words
[19:42] to ins and then an inword dictionary
[19:44] that does uh integers to words. Great.
[19:48] Then we have an encode that uses that
[19:50] dictionary and a decode that uses the
[19:51] other dictionary. So far pretty easy to
[19:54] understand how all of this works. I'm
[19:57] going to take my B word tokenizer, feed
[19:58] it a corpus. It does the training, the
[20:01] building up of these dictionaries in the
[20:02] initializer so I don't have to train it
[20:04] specifically. And then we look at the
[20:06] compression ratio. The compression ratio
[20:08] we got for 100,000 words got compressed
[20:10] to 22,000 words. Really great
[20:13] compression ratio uh almost 1:5. great
[20:16] compression ratio.
[20:18] What's the problem with that? So, like
[20:21] let's try and take the first fragment of
[20:23] the 100,000 words, the independent June
[20:25] for all of love. And then as we do that,
[20:28] you could see that it built up all these
[20:30] words here. Why is that not great?
[20:32] Because we actually are going to get a
[20:33] pretty meaningful long tail of words
[20:36] that aren't that common. Why would we
[20:38] waste space in our embedding matrix on
[20:40] that? Okay. So like the in between
[20:43] solution is we can train a uh bite pair
[20:46] encoding a BP.
[20:48] Notice that I'm not uh building my own
[20:51] BP in scratch. In this example I'm using
[20:54] a BP tokenizer that's coming in from
[20:56] like external libraries.
[20:59] So I'm going to create a tokenizer a BP.
[21:01] I'm going to tell it the unknown token.
[21:03] Tokenizers also have to handle what
[21:05] happens if a new token comes in that
[21:06] they've never seen. So traditionally we
[21:09] have an unknown token where there's also
[21:11] a few other special tokens like an end
[21:13] of string token a beginning of string
[21:14] token an unknown token. So there's a few
[21:17] of these
[21:19] a padding token which we don't know why
[21:21] we need yet and then so I give the BP
[21:24] token and I say that actually my
[21:26] stopping condition is once my vocabulary
[21:28] is 5,000 words. So it's going to start
[21:30] off from pair character and then it's
[21:32] going to build up and then it's going to
[21:33] stop when it gets to 5,000. Uh, this is
[21:36] just me using the syntax that supports
[21:38] this BPE trainer. I'm going to take the
[21:41] corpus. I'm going to feed it to the to
[21:43] the BPE trainer and it's going to give
[21:45] me a BP tokenizer from that. And then
[21:48] I'm going to use tokenizing on our
[21:51] entire corpus from that to see how many
[21:53] tokens we get out of that. Great. So, I
[21:56] took 100,000 words as my input. It
[21:59] stopped at 50,000 subword word token
[22:02] character tokens and I got a compression
[22:04] ratio of 1.52.
[22:06] That's not great. It's still negative
[22:09] compression, right? Like when compared
[22:11] to 100,000 words, but it's actually a
[22:13] lot better than 6 something. So, we're
[22:16] about four times more effective even
[22:18] though we only did 5,000 merges on a
[22:20] 100,000word
[22:22] uh corpus. So, actually pretty effective
[22:24] if you ask me. So, negative compression,
[22:27] but still pretty good.
[22:29] So let's try and test this tokenizer.
[22:31] The independent change for all of love,
[22:33] right? We run it through the tokenizer
[22:35] with encode. And let's run it. The
[22:37] independent
[22:39] gent for all of the love,
[22:42] so pretty good. There's a few words
[22:44] here. There's a few subword components.
[22:47] There's punctuation marks. You can kind
[22:49] of see how BPE does its thing. it it's
[22:52] always going to end up with a few single
[22:54] characters that are most common in the
[22:55] language like punctuation marks or the
[22:58] singular uh pronoun in English uh it's
[23:02] we're going to end up with a few very
[23:03] common words the all for love and it's
[23:07] going to end up with a bunch of subword
[23:08] components to be able to assemble
[23:10] everything else in the corpus. Great. Uh
[23:13] so exercise let's uh build our own
[23:16] custom BP tokenizer. I'm not necessarily
[23:19] going to solve this with you. I think
[23:20] that I've created a shim for you. No, I
[23:24] did not create a shim for you. That's
[23:26] really unfortunate. So, what I would
[23:28] ideally like you to do is try and build
[23:31] your own custom BP tokenizer. You can
[23:33] build an init method, an encode method,
[23:36] and a decode method. I think that makes
[23:38] the most sense for you. Uh, and is there
[23:40] like an ex is there room here? Here we
[23:42] go. So, here in exercise number seven,
[23:44] you should build your own BP tokenizer.
[23:46] We want you to initialize the
[23:48] vocabulary, do some merges, do encode
[23:50] and decode, implement all of that, and
[23:52] you take in the number of merges, which
[23:54] is your stop condition. Great. So, I'm
[23:56] going to look at my implementation of
[23:57] that. My implementation might not be
[23:59] great. I just wrote something and maybe
[24:00] I'm not great at Python. Um, so first,
[24:03] we're going to take the vocabulary.
[24:05] We're going to create a dictionary. I'm
[24:08] going to pre-tokenize the uh the corpus
[24:12] text that we get in. What does
[24:13] pre-tokenizing mean? I'm just going to
[24:15] split it and then I'm going to make sure
[24:18] that I have special tokens in there for
[24:20] spacing. And that's it. That's all my
[24:22] pre-tokenization is going to do. You
[24:23] could do a lot more. You could do
[24:24] special charact all the special
[24:26] characters you care about. And then I'm
[24:28] going to run the tokenizer end times. So
[24:30] what is running at end times means for
[24:32] number of merges for i number of merges.
[24:36] If you can do another round of merges,
[24:38] do it. If you can't, then you could just
[24:40] stop, right? Or because there's no more
[24:41] merges left for you. uh could be that
[24:44] you have just a very small corpus, so
[24:45] you can't really keep doing merges. You
[24:47] tokenize for one round. What does
[24:48] tokenizing for one round mean? We take
[24:51] all of the pair frequencies. We find the
[24:52] most frequent pair and then we're going
[24:54] to go ahead and merge it. What does
[24:56] merging do over here? It's going to just
[24:59] take that. It's going to go over our
[25:01] entire uh set of like existing corpus or
[25:04] like the remaining pairs and it's going
[25:06] to do a merge and emit other uh pairs
[25:08] out of that. Great. So we have that and
[25:11] then we also have uh the ability to
[25:14] encode and decode hopefully. So I'm
[25:16] going to take the custom BB tokenizer.
[25:18] I'm going to give it my corpus and then
[25:20] what's the first step? It's going to
[25:21] convert uh it's going to merge E and
[25:24] space. It's going to merge S and space.
[25:27] It's going to which W stands for white
[25:29] for white word here. It's going to merge
[25:32] T and H I and N. It's going to keep
[25:35] running for 5,000 merges as it keeps
[25:37] doing merge. And one thing we notice is
[25:39] the merge pairs are going to big bigger
[25:41] and bigger and bigger, right? Them is
[25:45] happens at uh step 367, right? It's
[25:48] going to do that merge and so on and so
[25:50] forth. Great. So that's going to run for
[25:52] 5,000 rounds. Let's try and use the
[25:55] encode method here. The independent gen
[25:59] for all the love, romance, and
[26:03] scandal. Right? So you can see our BPE
[26:05] tokenizer works even though I coded it
[26:07] myself and didn't use any framework.
[26:09] Maybe it works as effectively as the one
[26:11] that we're using externally. So the
[26:13] exercise for you is now that you've seen
[26:14] a BP implementation, build a BP
[26:17] implementation, right? Start off with
[26:19] accepting a token uh at Corpus, the
[26:22] number of merges, try and initialize
[26:24] your vocabulary, doing the merges,
[26:26] encoding and decoding, so on and so
[26:28] forth. Your goal is to really get encode
[26:29] decode to work. Great. You try and run
[26:32] this now, it's going to error out. That
[26:33] kind of makes sense. So we looked at our
[26:37] uh GPT2 tokenizer. We looked at
[26:40] converting between string and ins. We
[26:42] looked at pair character tokenizers that
[26:43] are converting between string and inst
[26:45] but all of the strings are going to be
[26:46] character single characters. Looked at
[26:48] by word tokenizer. We looked at training
[26:50] a BP tokenizer off the shelf using a
[26:53] off-the-shelf BP algorithm and then we
[26:56] built our own custom BP tokenizer. the
[26:59] exercise is for you and actually I think
[27:00] there's one more exercise for you is to
[27:03] use the open AI tick tok to tokenizer
[27:06] and then again tick token uh from uh
[27:10] open AI is going to be the thing that we
[27:13] use to train our large language model
[27:14] we're not going to train our own
[27:16] tokenizer we could we now know how to
[27:18] but I think we could because we're
[27:19] building a GPT2 style tokenizer we could
[27:22] just use theirs they've already done the
[27:24] training on that but you could also just
[27:26] choose to train your own tokenizer
[27:27] there's no reason not to. So, there's
[27:29] documentation for how to use tick
[27:31] tokenizer here. This is an open source
[27:33] project. Maybe just copy something from
[27:36] here. Maybe look at some sample code.
[27:38] Try and use uh their tick tokenizer, the
[27:41] GPT2 tokenizer, or try and train your
[27:43] own. So, that's an exercise that I leave
[27:45] for you. And again, you always have the
[27:47] answer here if you need it. Great. And
[27:49] now you have two exercises. build your
[27:51] own custom BPE tokenizer or uh and or
[27:56] use OpenAI tick tokenizer. I think both
[27:58] of those are going to be super useful.
[28:00] And as you can see here, our BPE had
[28:02] 100,000 input words. I only let it run
[28:05] for 5,000 words. I can have let it run
[28:07] longer, but it also got you like a not
[28:10] terrible compression ratio of 1.5,
[28:12] right? A lot better than we got from
[28:14] pair word even though we only did like
[28:16] 5% of merges compared to the number of
[28:19] words. So you can see like that tells us
[28:20] a lot about word frequency there. Great.
[28:23] So some decisions we're going to make.
[28:25] Decision number one is we're going to
[28:27] use the open AI tick tokenizer tick
[28:31] token that shipped with GPT2. We're
[28:33] going to have a couple of special
[28:34] characters. I kind of mentioned those in
[28:36] passing but let's mention them again.
[28:39] Unknown characters beginning of string,
[28:41] end of string, and padding. Those are
[28:43] going to be our special characters.
[28:44] Beginning of string and end of string
[28:46] are kind of self-explanatory, right? End
[28:48] of string lets the model say I'm done
[28:51] speaking now. Beginning of string it
[28:53] means hey we're going to like start a a
[28:55] sentence now. Unknown is going to emit
[28:58] whenever there's a token uh character
[29:00] that it doesn't know anything about. And
[29:02] then uh finally there's the padding
[29:04] special character. Why do we need
[29:06] padding special character? I think we're
[29:08] going to find out when we do
[29:09] pre-training. Here are uh the functions
[29:13] of how to use tick token. Uh you could
[29:15] do tick token.get get encoding GPT2
[29:17] initializes the the the
[29:20] tokenizer and you could call encode with
[29:23] a string and get an int or decode with
[29:26] an int and get a string. Great. So
[29:28] hyperparameter what is going to be our
[29:31] vocabulary size that's going to be
[29:32] really important for us because we're in
[29:34] BPE. Remember we have to tell it roughly
[29:36] how many merges we want it to do or how
[29:39] many like how big we want our vocabulary
[29:41] to be. GPT2 used 50,257.
[29:45] Uh, Corpathy in a fun tweet from 2023
[29:48] says that he saw a massive increase in
[29:50] performance when he went to
[29:52] multiplications of 64. Right? That kind
[29:54] of makes sense if you think about how
[29:56] GPUs work. Maybe multiplications of 64
[29:59] have to do with the number of cores
[30:00] inside of a GPU, an Nvidia GPU. I think
[30:04] so. But because that's a 25% speed up in
[30:07] training, why would we not use a
[30:09] multiplication of 64? We'll actually use
[30:11] 50,34.
[30:14] Great. So, those are the decisions we've
[30:16] made for our tokenizers. Next up, we're
[30:19] going to look at embeddings. Embedding
[30:20] is going to be a pretty fullon section.
[30:22] There's going to be a lot of stuff we're
[30:24] going to want to talk about. It's going
[30:25] to be embedded and unmbeddings and
[30:27] context and embedding sizes. There's
[30:28] going to be a lot to talk about there,
[30:30] but those are really important. Those
[30:31] are the in-memory representation of
[30:34] those ins that we talked about. How does
[30:36] the network first translate into
[30:38] something that it knows? Great. So all
[30:40] of that is going to happen when we
[30:42] resume and go to section 16 embedding.
