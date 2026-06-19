# Saving & Loading Models | Build Your Own LLM Workshop #9

**Build Your Own LLM Workshop — Video #9 of 23**

| | |
|---|---|
| **Channel** | Justin Angel |
| **Duration** | 11m 40s |
| **Views** | 0 |
| **URL** | https://www.youtube.com/watch?v=riCiHjVEqXc |

## Description

No description available.

---

## Full Transcript

[00:01] Hello and welcome back to building your
[00:04] own large language model with me, Justin
[00:07] Angel. We're going to be finishing off
[00:09] our tour of how to build machine
[00:11] learning models that are
[00:14] based on neural networks. And we're
[00:17] going to finish off by talking about
[00:18] saving and loading data set our models.
[00:22] So so far we just trained an A plus B
[00:24] modulus 5 using backpropagation. It's
[00:27] pretty big model has about 5 million
[00:29] parameters. And then our question is
[00:32] well running that takes a couple of
[00:35] minutes, maybe an hour. How can we just
[00:38] save it to disk and then load it back
[00:40] up? So the answer is yes, absolutely and
[00:42] we should do that. So we do that by
[00:44] calling torch.save with our state
[00:47] dictionary, maybe the optimizer states
[00:49] as well. We give it a file name and then
[00:51] we save it to a PTH file. We can then go
[00:54] ahead and load it back from a PTH file.
[00:57] We then can invoke our MLP which just
[01:00] does A plus B modulus 5. So 5 plus 4
[01:03] divided by 5, the remainder is 4. Very
[01:06] cool.
[01:07] And then we can save that to G Drive, to
[01:10] Google Drive. We can save it to local
[01:12] file systems, for example model volumes
[01:15] or we can download them from the
[01:16] internet. Why is that important for us?
[01:19] Again, we're trying to just save and
[01:21] load at the end of or as a checkpoint
[01:24] during training of models.
[01:27] Um and then important to mention PTH
[01:30] which is the default storage format for
[01:32] PyTorch.
[01:34] There are other ones though. We are
[01:36] going to use PTH for our little training
[01:39] of a large language model of 124 million
[01:41] parameters or however many we choose,
[01:44] but we should mention that PTH has
[01:46] security risks. Specifically, the entire
[01:50] file is loaded using a virtual machine
[01:53] with a bunch of custom instructions and
[01:55] can easily take over your machine. So
[01:57] you can probably imagine you're only
[01:59] going to use PTH if you save the file to
[02:02] yourself and then you're going to load
[02:03] it yourself.
[02:05] You probably don't want to take a PTH
[02:07] from the internet and run it on your
[02:08] machine, almost definitely. So, highly
[02:11] insecure for web downloads. What is more
[02:13] secure? It's safe tensors. So, the
[02:15] format that has pretty much taken over
[02:17] hugging face
[02:19] and it uses JSON and then it supports a
[02:21] bunch of other features like lazy
[02:23] loading and quantization. You don't have
[02:26] to know what those are, but the security
[02:28] feature and those extra little bit of
[02:29] features really helped it become the
[02:31] most widely used format. And I do want
[02:34] to highlight like I have my hugging face
[02:36] repo for our large language models that
[02:39] we're training in this in this workshop
[02:41] and it is a PTH file.
[02:44] Great. Uh so, now we're we talked about
[02:47] PTH and we talked about the safer option
[02:49] of safe tensors. Let's talk about ONNX.
[02:52] Uh so, that one run you exported once
[02:56] and then it can run on inference
[02:57] engines.
[02:59] Um
[02:59] really the nice things about it is it's
[03:01] very compatible with both PyTorch and
[03:03] TensorFlow. PTH only works for PyTorch
[03:06] generally.
[03:08] TensorFlow has its own format that only
[03:09] works in TensorFlow. You can kind of
[03:11] load one into the other one if you do a
[03:13] bunch of work. Why would you? Safe
[03:16] tensors makes it more safe. ONNX is
[03:18] meant for cross-platform portability,
[03:20] especially as you're trying to play
[03:21] around and figure out your training
[03:23] configuration. Um GGML, I don't know how
[03:27] to pronounce this one correctly. I
[03:28] actually pronounce it Google. Is pretty
[03:30] much the de facto standard for
[03:33] inference. Why? Because it's very very
[03:35] heavily optimized for inference time
[03:38] performance and it has a bunch of really
[03:40] great optimizations in it that I'm not
[03:42] going to expand on. But if you're trying
[03:44] to take your model from training to
[03:46] production to inference time, then I
[03:49] think you're probably using a GGML and
[03:51] there's a bunch of reasons why you would
[03:52] do that. Also, I should mention edge
[03:55] computing. iOS and Android are real, and
[03:59] they can run ML models natively. They
[04:02] don't necessarily need support though
[04:04] any of the formats we mentioned thus
[04:05] far. They you could use Core ML for
[04:07] example for iOS, and Android also has
[04:10] its own format. So, worth mentioning
[04:12] that. So, those are five options for
[04:14] format, and we can um
[04:17] we're going to end up using PTH. Really
[04:20] important to mention because we don't
[04:22] really have a slide for that. At the
[04:24] end, we're going to want to save that
[04:25] file somewhere that people can reach.
[04:27] Most common is to do that the hugging
[04:30] face. Hugging face is where we store our
[04:32] data sets and our models as if we were
[04:34] doing open source work. So, really easy
[04:37] to just go and upload those files there.
[04:40] Safe tensors is the most common, or PTH
[04:42] if you're doing work for yourself.
[04:44] Great. So, let's look at a little bit of
[04:46] code of saving
[04:48] um
[04:49] of saving and loading our model. So,
[04:51] once again, we're going to initialize
[04:53] our model that does
[04:55] uh A plus B modulus C, right? So, 100
[04:59] 100 divided by five.
[05:02] Sorry, this is modulus five.
[05:05] Uh
[05:06] great. So, we have that. We have our
[05:08] architecture for our multi-layer
[05:10] perceptron. 200 inputs. Why? Because
[05:13] we're doing one hot encoding for the 100
[05:15] and 100, so 200.
[05:17] We have our hidden layer of 32, uh our
[05:20] hidden layer of 16,
[05:22] and we have an output layer of five.
[05:25] Great. Now, we have our data set that's
[05:27] based on with those 10,000 rows we
[05:29] printed out earlier. We created our
[05:31] training data set, our test data sets.
[05:34] This is all stuff that we saw in the
[05:36] previous section. Nothing new so far.
[05:38] Now, we have our data loaders ready to
[05:41] go our data sets ready to go. We have
[05:43] this function here that calculates
[05:44] accuracy on either one of those.
[05:47] And then we have our training loop. Our
[05:48] training loop runs a train training data
[05:52] set loader, takes in the bad size, the
[05:55] validation loader or the test loader. We
[05:58] have our optimizer. We have our loss
[06:01] function, cross entropy loss. We run for
[06:04] a maximum number of epochs. In those
[06:06] epochs, we zero out the gradients, we
[06:09] activate the model, we call the loss
[06:11] function, we
[06:13] uh do back propagation, and we keep a
[06:16] running loss. And eventually, if it's
[06:17] good enough, we then just stop.
[06:20] Great. So, we did that. It took about
[06:21] six epochs.
[06:23] We didn't incorporate the best
[06:24] parameters from section eight, but we
[06:26] still finished in six epochs. So, now we
[06:28] probably want to save that to disk. And
[06:30] now I have this method that's called
[06:32] invoke model with A and B just to make
[06:34] it easier for us later on to just use
[06:36] the model after we've loaded it. Okay,
[06:38] so to save the model, I'm just going to
[06:39] call torch.save. I'm going to give it
[06:41] the state dictionary. Why do you have to
[06:44] do that? Because you could also save
[06:46] keep the optimizer states. You would
[06:48] save just the weights and the biases, so
[06:51] the learnable parameters, if you're done
[06:53] training. But if you're not done
[06:54] training, you also want to keep the
[06:55] optimizer states, all of the previous
[06:57] steps that you've taken.
[06:59] So, here we're saving just the weight.
[07:01] We're going to save it into this
[07:02] temporary
[07:03] location that exists in Colab, DNNV1
[07:06] path,
[07:08] p t h. And then we can create a new
[07:10] model. We can try and load this file. We
[07:12] can invoke it with A and B.
[07:15] 5 + 4 modulus 5 = 4. Okay, so that
[07:18] worked. That's really great. We can now
[07:20] have a slightly more complicated saving
[07:22] script. This is more resembling of a
[07:24] real script you're going to have. First,
[07:26] you're going to try and store to Google
[07:28] Drive. Google Drive is persistent. It
[07:29] lives beyond the session. Colab storage
[07:32] does not live beyond the session. If
[07:34] not, if you can store to Google Drive,
[07:37] that's great. Do that. If not, try and
[07:39] save to this folder mnt workshop if it
[07:42] exists.
[07:43] That tells me that I'm running on a
[07:45] modal volume. So, modal just rents out
[07:48] GPU space. A volume is persistent
[07:49] storage, their version of persistent
[07:51] storage. So, I could we're just going to
[07:53] store to that folder knowing that it's
[07:55] persistent. I created the workshop uh
[07:58] persistent storage volume.
[08:00] If none of that works, I'm just going to
[08:02] try and store it locally here to MNT
[08:05] just to or maybe I'll print an error.
[08:07] Great. So, in loading, I'm going to
[08:09] follow the same order. I'm going to try
[08:11] and load it from Google Drive first.
[08:13] Then I'm going to try and load it from
[08:14] the persistent volume that I created on
[08:16] modal. And finally, if that doesn't
[08:18] work, I could go to this URL. I'm going
[08:21] to just compose it here real quick. And
[08:23] then I uploaded the PTH file to the to a
[08:27] website. Here we go. And it's going to
[08:30] download this up. Close enough. Well, it
[08:32] should download this PTH and I'll
[08:34] investigate later why it didn't.
[08:36] But, we can then go ahead and download
[08:38] it from the internet. Uh what happens if
[08:41] I click this link?
[08:42] I'll look into it later and see why it
[08:43] didn't do that.
[08:44] Great. So, it could download that PTH
[08:46] from the internet assuming I ever fix
[08:48] that link.
[08:49] Uh another option, another thing that we
[08:52] want to look at is we can load our GPT-2
[08:56] style model that we're training in this
[08:59] uh in this workshop, we can load it
[09:00] directly from the internet. So, I'm on
[09:02] Justin Angel workshop V1 pre-training.
[09:05] And then this is how Hugging Face lets
[09:07] you load in those PTH files and those
[09:09] models. I'm going to give it Justin
[09:11] Angel workshop V1 pre-training.
[09:14] And then I'm going to have my dot
[09:16] generate method called "Hey, generate me
[09:18] 100 tokens. Uh temperature 0.8, top K
[09:21] 50." Great. The meaning of life is and
[09:24] if everything worked, it should actually
[09:26] say something that sounds semi-coherent.
[09:28] The meaning of life is to live as a
[09:30] human being. The goal of life is to
[09:32] achieve the highest level of of
[09:34] happiness.
[09:36] Sounds cohesive and cognizant to me.
[09:38] Great. So now we were able also able to
[09:41] use the loading mechanism we described
[09:43] earlier and this is those file types we
[09:44] used PTH to load in data from hugging
[09:47] face and then actually see how loading
[09:50] and saving relates to large language
[09:52] models. Really important to know how to
[09:54] do this. This is critical. A couple of
[09:56] other things worth mentioning that we're
[09:58] going to do. So one, we're going to use
[10:00] a PTH file. We've already said that.
[10:02] We're going to have an /workshop folder
[10:04] on Google Drive. That's where I store a
[10:06] lot of my trainings, especially when I
[10:08] run on Colab and I want persistent
[10:09] storage. I also have mnt_workshop if you
[10:12] want to store stuff for later on another
[10:14] platform like Model.
[10:17] File names, I'm going to name workshop
[10:19] v1 and then the stage. We're going to
[10:21] have three stages, one for pre-training
[10:23] and two for post-training, instruct
[10:25] tuning and RL. You don't need to know
[10:27] what those are, but you do need to know
[10:28] that they have different checkpoints
[10:30] that it'll support.
[10:33] And checkpointing will save the latest
[10:35] PTH every 100 pre-training steps. So
[10:37] every 100 steps, in case there's
[10:39] something happens to the server and say
[10:40] training gets corrupted, we have the
[10:42] latest PTH. I only store latest PTH. I
[10:45] don't store the older files and keep
[10:48] them around for later cuz then you could
[10:50] see 1.4 GB you're going to have massive
[10:52] persistent storage pretty soon and
[10:54] you're going to have to pay for that. So
[10:56] worth thinking about that. Great. And
[10:58] now that we're done with saving and
[11:00] loading, we are officially complete with
[11:02] building basic machine learning models.
[11:05] The thing that happens after this is
[11:06] we've moved on to building the
[11:08] transformer architecture. Specifically,
[11:11] we're going to move into portions that
[11:13] are kind of related to deep neural
[11:15] networks, of which large language models
[11:17] are some of. Right? So like large
[11:19] language models are deep neural networks
[11:21] and as a result they are afflicted by a
[11:23] bunch of things that afflict deep neural
[11:25] networks. So that's going to be the next
[11:27] set of things we're going to learn
[11:28] about, how to keep training stable in a
[11:30] very deep neural network. And the next
[11:32] four sections is just built on that and
[11:35] giving us that skill set. And I hope you
[11:37] can join us for that as well.
