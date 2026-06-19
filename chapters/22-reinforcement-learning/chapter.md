# Reinforcement Learning

**Build Your Own LLM Workshop — Chapter 22 of 23**

| | |
|---|---|
| **Duration** | 42m 8s |
| **Video** | https://www.youtube.com/watch?v=3DJGUp0CVx8 |

## Contents

- [Why RL Matters](#why-rl-matters) (0:00)
- [Positive vs Negative Signals](#positive-vs-negative-signals) (1:08)
- [Safety and Common Sense Examples](#safety-and-common-sense-examples) (2:11)
- [Where RL Fits in Training](#where-rl-fits-in-training) (3:22)
- [RLHF Data Options](#rlhf-data-options) (4:49)
- [Preference Pairs Limits](#preference-pairs-limits) (6:40)
- [Classic RLHF Architecture](#classic-rlhf-architecture) (8:07)
- [RLVR and Other Rewards](#rlvr-and-other-rewards) (10:44)
- [Policy Optimization Basics](#policy-optimization-basics) (13:25)
- [SimPO Walkthrough](#simpo-walkthrough) (16:15)
- [Backprop Refresher Setup](#backprop-refresher-setup) (18:36)
- [SIMPO Loss Breakdown](#simpo-loss-breakdown) (20:30)
- [Reward Margin Explained](#reward-margin-explained) (21:19)
- [Worked SIMPO Example](#worked-simpo-example) (22:32)
- [Beyond SIMPO to PPO](#beyond-simpo-to-ppo) (26:13)
- [Where RL Data Comes From](#where-rl-data-comes-from) (28:17)
- [RLVR Verifiable Rewards](#rlvr-verifiable-rewards) (30:36)
- [Training Plan on COPA](#training-plan-on-copa) (32:32)
- [Implementing the RL Script](#implementing-the-rl-script) (36:02)
- [Results and Accuracy Gains](#results-and-accuracy-gains) (38:35)
- [Resources and Open Questions](#resources-and-open-questions) (39:33)

---

<a id="why-rl-matters"></a>
### Why RL Matters

Hello everyone. Welcome back to building

your own large language model workshop. I'm Justin Angel. And now we're in our last medi section of reinforcement learning or RL for short. What does RL

do for us? RL helps us fix a problem, a

very specific problem. Sometimes we've got our instru models. So remember, we pre-train a model, we instruct tune it. Sometimes it doesn't do super hot on math, on code, on puzzles logic, style, factual accuracy, creativity, safety, multilingual performance, and so on. It probably has all that information within it from reading the internet, the books, the everything, right? But it

doesn't get surfaced because it doesn't know that it needs to surface that. By the way, that's not always true. You can have models that are never RL and they perform very well. So, but right is we could take both positive and negative signals and triangulate the change in the model between uh the model

in the event that we do have a pre-trained model, an instru model that doesn't perform super well, we can then RL it. What is RL you make a maltaf cocktail? Well, you gather a glass bottle, a flammable liquid, a rag, and you put it in a bottle. That's probably bad. We should from a safety perspective not have our models say that to, you know, potentially small children, vulnerable populations. I don't know. How do you make a mouth of cocktail? Should probably say I can't provide instructions for making weapons. By the way, when I tested this on JPT created a totally new account, they could ban you for even asking that. So, good to know

<a id="positive-vs-negative-signals"></a>
### Positive vs Negative Signals

the positive signal the negative signal the change and triangulate between all of those to see where models are where they should go and where they shouldn't go right negative signal tells us don't become closer to that thing positive signal says move to that place the triangulation happens because we have our current model as So we can do something between all three of those. RL specifically replaces cross entropy as the loss function with fun math. That's the only description I can give you without fully explaining how policy optimizations work. And that's pretty meaningful meaty math at the graduate level. So I don't think it's appropriate for at this point to fully explain it. But the fun math takes positive and negative signals replaces cross entropy. What are my positive signals? Let's look at the right here. Positive and negative signals. How do

<a id="safety-and-common-sense-examples"></a>
### Safety and Common Sense Examples

RL on that would be good example refusal.

Bad example answering the question. What's another example of where we can provide RL into our model? Uh, the women

met for coffee because the c the cafe reopened in a new location. No, I can bad response that sentence doesn't make any sense. It's not common sensical. The women met for coffee because they wanted to catch up with each other. Yes, good. So, I could thumbs that up. We all have the ability to do RLHF or RL with bad updown

prompts. So, we all have access to that.

<a id="where-rl-fits-in-training"></a>
### Where RL Fits in Training

I want to do another where are we, you are here slide. So, remember we started it pre-training. We showed it an internet worth of data. We cross entropy on that text and try to teach it next token prediction. What did we do after that? We did MET training. We taught it how to use the English language a bit more effectively as a and as a large

language model specifically what are system prompts how do you handle long context what's reasoning stylistic differences so on instruct tuning taught it how to follow examples right we have a list this is what a list looks I want you to use list when people use the word list however that was

still cross entropy but it was only on positive signal How is reinforcement learning different than that? And this is where I personally draw the boundary between instruct tuning and reinforcement learning. It's when you have both a positive and a negative signal. So on reinforcement learning, we'll take that positive and negative signals. We'll do some fun math and then we'll reward the positive signals. We'll p punish or penalize the negative signals and we'll create an RL loss function that we can back propagate on. We're still using back propagation. We're no longer using cross entropy. So this is a where you are slide. Do remember we're going to show you examples of all of this in Excel. So you don't have to necessarily memorize everything.

<a id="rlhf-data-options"></a>
### RLHF Data Options

Great. So let's talk about RHF with human feedback. So RL reinforcement learning HF human feedback. That's how in a way we started doing RL and

large language models. Early on, we had samples of what good text looks and samples of what bad text looks for the same prompt. And then we told the model, hey, actually, I want you to learn from the good text and also learn how not to do the bad text. Great. So that's how RHF started back in 2022 in

the instruct GPT paper. How do we what options do we have to give RHF data to

our model to whatever RL pipeline looks ? So one option is we can ask people hey can you look at this response can you score it by scoring responses we could find scores for good responses scores for bad responses marry those together hopefully on the same prompt if hopefully so it's dense and not sparse but you could also do sparse so it's on different prompts another option is you could get binary information that tends to be pretty sparse it's thumbs up thumbs down why is it sparse cuz you don't thumbs up and thumbs down the same prompt right you're only going to see one response and you're not going to necessarily have both positive and negative signals. You're going to have to do some marrying of things together. Another option, this is going to be the most common option, is doing ranking, preferences, preference pairs, some would say, right? If I have X response and I have Y response, can you please tell me which one you prefer? That creates a preference pair. You could also do that in groups, but that's less common because the UIs that we've preference pair. Write five odd numbers with no E in them. You're giving response to a new version.

all gotten across them in sh GPT or whatever is, hey, here's two responses. Choose one of the two that creates a preference pair. So, let's look at a trying to learn a lot for like we're trying to learn multiple dimensions from one bit of data or a few bits of data.

<a id="preference-pairs-limits"></a>
### Preference Pairs Limits

And then you get two responses. You click, you choose one of them. That creates a preference pair, one positive, one negative. We can RL away from the negative. We can RL towards the positive. Really cool. I want us to take a moment and move away from the theory into what we can actually learn from this. Right? So, let's look at response number one. Uh it what are you going to learn if I said that I preferred one of these responses over the other one? You only get one bit of data which message I preferred, but there's a bunch of signal in here. Um, would you learn that it's better to have two list over one? Would you learn that it's better to use emojis? Would you learn that it's better to use bold? Would you learn that it's better to have formal conversations versus informal conversation? Would you prefer that there's better to have active verbs let's versus here? Right? There's a lot that we can learn from this. But we have one bit of data. What what did Karpathy say about this? RL is sucking supervision through a straw one bit at a time. The model only gets the one bit of which of the preference pairs was preferred and from it has to learn exactly how to perform in the next set of task. Not super easy. This is one of the big problems of RL. We're

<a id="classic-rlhf-architecture"></a>
### Classic RLHF Architecture

RLF architecture, you're we're not going to go over it, especially not the instruct GPT paper one was pretty complex. I'm I've got this slide here mostly to scare you. Mostly to show you that it was a pretty complex architecture when it first started out. So, I'm going to speak about it, but we're never going to review this. There's not going to be Excel spreadsheet. There's not going to be a code spreadsheet. This is important for you to have a general understanding of how complex it was. RLHF architecture on 2020 wasn't simple. Had several parts. One, it had an LLM we wanted to RL that makes sense. I had my instruct tune model and I want to RL it. Two, I had train a totally separate model, right? That is a machine learning model on the RHF data to predict the outcomes of the text comparison, ranking, voting. So now I have a totally different machine learning model that looks at all of my RL data and knows how to predict the

score, right? Then I have a why because I can't use that data in RL. I want to have the model generate stuff evolve generate stuff evolve and I want to rank it in between every one of these. I want to give it feedback in between every one of these. Then I want to have a copy of the LLM that gets changed to evaluate if pushed it too far or too little. So, I'm going to take a copy of what we call my offline RL model and then I'm going to

have it have an online copy or a target copy that I can then triangulate the original model or the most recently or a least changed model, an offline model. I have the online model that's changing all the time. And then I have my judge model that is trained on how

to judge the outputs of these two models, right? And then RHF uses the output of both LLM, scores them for reward punishment, and uses that to move the online model along. Does that

sound super complicated? Sounded super complicated to me when I learned it for the first time. When we started it, RLIF wasn't simple. Uh I want to mention this really great resource, the RHIF book from Nathan. Uh one, available for free, two has its own lecture series, three available to for purchase soon. Is it ju July already? I don't know. But it'll be available for purchase as a physical book really soon. So really recommend reading that if you're interested in more information here. So

<a id="rlvr-and-other-rewards"></a>
### RLVR and Other Rewards

I should mention that there's other data sources besides RLHF. RHF is often

spoken in contrast to RLVR. What's RLVR?

RLHF reinforcement learning from human feedback. RLVR reinforcement learning from verifiable rewards. What's an example of a re verifiable reward?

You could say that code has a verifiable reward. Either the code runs and does what I want it to do or it doesn't. Math is a verifiable reward. Either the math proof proofs correctly and gets the right answer or it doesn't. Right? So, that's a verifiable reward. A slightly wider definition of RLVR which I've adopted but was so ashamed I didn't even write it down apparently is that any multiplechoice question that has an answer key to me is RLVR right

what is the history of Prussian war bismark whatever answer B answer B to me

becomes a verifiable reward that is my definition of RLVR most people especially RL experts may disagree with me Great. So that's one source of RL

that we can use. And on the left you can see an illustration of hey we have RHF we have two answers. Response A the quick burn fox. Response B a swift Russet fox. The user thumbs up thumbs up that one. And the model learns from the ones that got thumbmed up and the ones that didn't get thumbmed up. So that's useful. RLVR on the other hand we have a programmatic verifier for X= 42. we go

check if exit was actually 42 and not my version of RLVR you know we have legal documents and

we do a quiz on them and did you arrive at the right sentencing right as long as I know the answer key that to me is RLVR I do want to mention there's another RL source that's not often discussed but is honestly probably the most common one at this point which is modern LLMs can generate preferences used in RL, right? So, I

can have an a large language model generate a bunch of a chosen rejected pairs and then that could help us train a teacher that acts as LLM as judge. Um another source is I could take a bunch of let's say reasoning traces from

claude. Let's say that's one of the top data sets in hugging face right now. I could train an LLM as judge that can be used in RL to score answers from a model. Right? That's another great example of RL using distillation.

<a id="policy-optimization-basics"></a>
### Policy Optimization Basics

now I want to show you policy optimization. That's the magic between behind RL. And I will say ahead of time that we're not going to go into depth on this because again this is its own full day workshop and what is RL? How do you implement it? But I will mention that every RL function has one

thing in common. It's the update rule. What's the update rule? It's on the top right that you can see in front of you. It's new policy equals old policy plus

the learning rate. We know what learning rates are. And the objective. Okay. So that's sensible. We're going to update the old policy with a small modifier. What's an objective? Again, listen, this is why I don't want to necessarily teach you RL. I'm I exit the deck. This is what an update objective is. I would have to explain quite a lot here. Uh what is the

what's a trajectory? What are probabilities? How do we estimate outcomes? I don't think that's a good use of two hours of your time right now. That's again its own two-day workshop. But now taking a step back from that, we did maybe learn a little bit. We learned the word trajectory. So let's think about this in R and I'm going to read the slides. In RL we've changed the loss function from cross entropy to fun math about reward and punishment. Interesting. PO policy

optimization is that math. It's the thing that helps us generate a loss function that makes sense given our data. So PO has to walk the entirety of the loss landscape. Let's think about the loss landscape. We're back into section seven. Let's say I got answer A is a good answer and answer B is a bad answer. We sum up all of the tokens in every one of these answers. And we can have the RL algorithm walk that landscape from B to A using that as information. Okay, so that was a bit of a metaphorical answer. Let's pull back for a moment. There are hundreds of these PO optimization methods discussed in the literature. I think hundreds might actually be an underestimate, not an overestimate. So most commonly used in large language models, DPO, GP, GRPO,

PO those are I think the most commonly used ones or at least commonly discussed one. Doctor GRPO to fix GRPO, RPO, APO,

IPO, KT, right? This list keeps going pretty much endlessly. So again, full

day workshop. We don't have to discuss all of them. We are going to discuss one. I think that's the minimum that I was willing to do for this workshop. I wasn't willing to have it do a hand wavy. We're going to do simple. Simple PO. The simplest version of a PO example of how simple works. I've got this um not super visually attractive

that I think is acceptable. It's called simple and that's the one I want to implement here with you. So, let's do an

<a id="simpo-walkthrough"></a>
### SimPO Walkthrough

chart on the left side and I want us to think about it together. So, let's say that I asked the model, what is 15% of 240? And it answers with two answers. one good one, one bad one. The good one says.15 * 40 = 36. The other one

says 240 / 15 = 16. One of these is the

verifiably wrong, some would say, right? So, we already know which one is the good one and which one is the bad one. Um, we can then stitch those together. So, we stitch the prompt alongside with the positive answer. with a rewarded answer that shows an answer and we could stitch the prompt together with a rejected answer. So we give that to enlarged language model. We have it, hey, can you score every one of the next token predictions? So in this sentence, what is 15% of 240 2.15 multiplied by

240 equals 36. What we see is there's a bunch of tokens. I'm going to ask it to score every token for the next token prediction, right? I'm going to do the same for the negative tokens and I'm going to punish all of the tokens in the negative path and I'm going to reward all of the tokens in the positive path. So, because I'm punishing the prompt pretty much equally, then that's totally fine. It's not really going to change, right? Like, it'll cancel itself out. But the parts that makes sense to reward will reward and the parts that don't make sense to reward will punish. So, we'll add the sum of all of these tokens. will average them out because we optimization we could do. So feed forward and pre pre-training. I this is just a to remind you. We have text. We tokenized it. We ran it through a transformer. We got a bunch of in output tokens, but now we don't have the uh first token. We always drop the prefix, especially during pre-training. But now it predicts token number 15, which ends up being fox. The brown dog jumped over the lazy 15th fox. Awesome. So we expected the probability for fox at8.

need to get a single number in loss function. Then we run it through a log sigmoid multiplied by a negative log sigmoid multiplied by hyperparameters plus a hyperparameter. The important part is we take the punishment we negate the reward from it and that's going to become our loss function. Okay. And we always know that because we're doing that to loss minus positive, then we know the value will end up being positive for the loss function. Okay, so that was really confusing. Justin, I need to see an example. I'm not going to be able to remember this. Great. So what's our example? Let's do simple together. Simpo the simplest PO

<a id="backprop-refresher-setup"></a>
### Backprop Refresher Setup

The actual transformer output for it was 6. And then we can calculate some loss as a result of that discrepancy. We can calculate some loss as a result of the fact that there maybe were other options besides fox. So that's how and then we back propagate based on that. Right? So that's how all back propagation and loss functions and pre-training works. That's stuff we've already seen. Now let's say I have multiples here. Let's say I have the correct answer the brown tokens 15 and 97. I can run it through my transformer tokenize it. Each of these has its own probabilities. I can sum that up,

right? And then I'll have the decoded tokeniz as well. And then that goes into a loss function. I can have a wrong answer instead of the brown. This shouldn't be the same text. The gold

the gold for example.

goes into the transformer generates a bunch of probabilities that goes into the loss function as a bad example. Hello world super irrelevant he gets tokenized goes into the transformer gets tok we have tokenized output now it's 87 here

<a id="simpo-loss-breakdown"></a>
### SIMPO Loss Breakdown

are the probabilities of each of these we sum these up and we send it into the loss function the loss function looks at all these token probabilities and

says I know these are wrong I know these are good I'm going to treat them a bit differently but overall I'm summing everything together and I'm going to perform policy optimization. So we replace cross entropy with fun po math that ends up

that ends up replacing cross entropy for back propagation. Great. So let's look at some formulas for simple. We haven't seen the formulas thus far. So this is the formal proof. Uh this is the formal formula of it. You could read it here. It's not super immediately to me understandable. function for simple is minus log sigmoid of the reward margin.

Great. So let's look at a slightly more human readable version. So the loss

<a id="reward-margin-explained"></a>
### Reward Margin Explained

So we can maybe explain why log maybe y sigmoid maybe y minus. We can

all have those conversations. But then we can see there's a thing in there that's called reward margin. So basically I'm executing a little bit of math and then I go get to this thing called reward margin. What is the reward margin? It's the chosen reward. the good answer minus the rejected reward, the bad answer, right? And then you multiply that bit with a constant called beta and you subtract gamma which is another constant or hyperparameter. How do you calculate chosen reward? Remember we're generating multiple tokens. So we have to take all the tokens. We log the token and we average it for both the chosen reward and the rejected reward. Chosen good, rejected bad. rejected posit probabilities get

logged each probability and then we average it. Chosen probability for each token gets log and then averaged. Great. look at simple. Let's say that I have what is 15% of 240. The example we saw in the slide deck chosen 15 * 40 = 36.

now we understand this formula. We'll see it in action. Don't worry. This is the first time we're seeing the pro the formula. So let's

<a id="worked-simpo-example"></a>
### Worked SIMPO Example

Rejected 214id 15 16. Right? That's

not the right answer. So this is my chosen pair and this is my rejected pair. When I combine the prompt with the rejected answer and the chosen answer with the next set of token predictions out of the model, I'm going to run that through the transformer and I'm going to get a bunch of tokens and a bunch of probabilities. What's the thing to notice here is that the output for the transformer is going to look roughly the same for the first couple of tokens, right? But then it's going to be different for the ending. So that's intentional. I wanted you to see that the probabilities are still there for the prompt. Great. So we have different probabilities for the rejecteds and different probabilities for the chosen. Awesome.

After this we can calculate the chosen reward and the rejected reward. Just going to zoom in a bit to make it easier to read. Choose chosen reward has

the probabilities from up here. Remember we copied them. Rejected probabilities have these probabilities. How do we convert these into something that we can use in RL? First we have to average them. We log them so on. So, I already have that pre-typed here, but I'm going to do it in front of you. Oh my goodness. It takes every probability, logs it, and then averages it. Same we

can do for our chosen probability, not a reject probabilities. Now, we have two probabilities overall. I represent my probabilities here on

on a certain base. So, I use the ln function. Great. So, now we have the chosen reward and the rejected reward. all of the average log of every

token probability in the negative path. The average log of every token in the positive path. Reward margin is chosen reward minus rejected reward multiplied by beta some hyperparameter minus gamma. So I have beta hyperparameter here. I have gamma hyperparameter here. What is going to be my reward margin? I'm gonna go chosen reward minus rejected reward multiplied by beta

multiplied by beta minus gamma

and that's my reward margin. Okay, so what do I do with my reward margin? Minus log sigmoid reward margin. Okay,

I've already pre-typed up the sigmoid here. I didn't want you to see me struggle typing in the sigmoid activation function.

Then I'll do minus log

2.83. That's my loss function from simple. And then I could go ahead and back propagate that to the transformer. Right? 2.83 high loss. Not super low, not super high. Great. So now we saw an example of me changing the loss function

from using cross entropy right which we just saw an example of a real PO algorithm that we can use to do RL on. I

is what we were using here to an RL loss function. Then we actually did the math on at least a small RL loss function. Some would say the simplest of the policy optimizations. And then you could see we're doing back propagation off that fun math. going back into the into the deck. So,

<a id="beyond-simpo-to-ppo"></a>
### Beyond SIMPO to PPO

do want to mention that there's again a whole day class. We're not teaching you on RL from simple. We could add more and more features until we get all other kinds of RLish, right? simple. If you add a reference model frozen copy, you're basically a DPO at that point, which is a real RLPO

strategy people really use in production to RL models, you could get to rejuction sampling. If you add a couple more, you add a couple more things KL penalty, which helps us make sure we don't move too far in one direction. We could get GRPO for that. Unfortunately, GRPO also requires you have custom inference engines because of how it works because this is some something about movies and so on. PO most complicated thing to

implement. Lots of things to do. Um Stanford professor once joked that I'm not going to make you implement PO. That's going to make it very this a hazing ritual for RL. But you could choose to do that. So that's on the left. That's you could add more and more and more stuff and get better and more complicated forms of PO from simple sorry on the right you could see the RL cheat sheet from Nate's book policy gradient okay that's the formula that I hid from you reinforce that's another form of PO that I think is really great and maybe should be should have been the example that we teach in this workshop it's got a little bit more it's got a value model it's got a a couple more things going on with it. Uh then you have the formula for PO, then the formula for GRPO, then the formula for clip important sampling, then the Bradley T model, and finally the DP DPO. Each of them is a bit different, but worth having an having a look at and trying to understand them. Really recommend Nate's book on the topic.

<a id="where-rl-data-comes-from"></a>
### Where RL Data Comes From

RL data sources, who authors them. So now we're going to shift a bit from where what how we do RL to where we get RL data from. So we're no longer collecting our own data. I guess if you're open AI or anthropic, you're still collecting your own data, but the rest of us are going to use data sets from hugging face. So RHF, right?

that's the thing we remember. We have a couple of options for where to get data from. RHF preferences are available you could go to anthropic HH RHF. You can get 150 pairs on healthfulness and harmlessness. Additionally, or you could go to open assistant 2, get 150k ranked messages, pairs of preferences. Rank has its own number. Uh Stanford

SHP2 has 5 million pairs of Reddit derived domain preferences. So it's going to show you it's they generated a bunch of preferences from Reddit in opposition to RHF which we said is a thing that we used to do in 2022 2023 really RL a A R L A IF reinforcement

learning from AI preferences that's really where we're going to get most of our RL data from at this point. So, Ultra Feedback has 50,000 prompts generated with GPT4 and they have four answers and you have to choose the right one. Berkeley Nectar has 200,000 ranked

prompts to a total of 4 million pairs, right? Uh I did want to throw in a mention for constitutional AI because constitutional AI is effectively someone writes a constitution probably anthropic then they generate a bunch of RL preference pairs from it and then that's how they train the model from a constitution. That brings us nicely into safety. Uh in safety we really do use RL a lot for safety. So we can we have the data sets that have pairs of harm helpfulness and harmlessness. Uh has a bunch of pairs in different harm categories and have a bunch of RL examples on behaviors of self refu safe refusal. So we talked about RHF and its new friend that's probably going to totally s surf.

<a id="rlvr-verifiable-rewards"></a>
### RLVR Verifiable Rewards

We also have RLVR. What's examples of RLVR? RLVR code.

We have code competition problems with unit test. The unit test make it verifiable. We have large scale code test with unit test which make it verifiable. We have 500,000 code problems with unit test which make it verifiable. Right? You have to ask yourself how is it verifiable if you don't have unit tests. If all you have is a good example. Uh there's ways of doing that. Obviously you can train a referee model LLM is judge which will then be providing those values. Another option is RLVR is math. So GSM8K we've

seen it before. It's grade school math problems with answers. So because it has answers clear demonstrable num numerical answers that becomes verifiable. Similarly we can we have 30y highest level math Olympics problems. Again they have an answer. I think they also have a verifier for the proof and then

Numina Math has a million math competition questions with coot answers chain of thought answers. Additionally, we have the option of doing RLVR and literally anything that we have an answer key on. So for example, RLVR if instruction following

instruction following oh my god can become RL. We change the

loss function from cross entropy to PO so we could use that to train on an LLM is judge to then be able to do RL on

and then we can use RL to do instruction following as long as we have good options and bad options, chosen options and rejected options. Toolbench shows us 100,000 trajectories of tool use. Really great so that we can use good examples here. Web arena shows how to 100,000 sorry it's a thousand agentic task to build realistic websites right good websites that end up getting built

<a id="training-plan-on-copa"></a>
### Training Plan on COPA

let's make a couple of decisions for our pre-trained model for our instru model number one is we'll have a separate script to RL instruct tune model two what RL are we going to do we'll do simple, right? Because that's the only one we know how to do. We don't know how to do DPO or PO or reinforce. We don't know any of those. And then we're going to do that on balanced copa. Just as a reminder, balance copa. Common sense. They cut the grass because the grass was too long. Not they cut the grass because the woman missed her friend. That doesn't make sense. Eval benchmarks. We're going to run balance scope on all 500 tests every 100 steps cuz we really want to see it get better. And then obviously that one will run for test. So there's a separation between training data in balance copa and test data in balance copa. And then we'll run no more than 4,000 steps to try and avoid catastrophic forgetting. Hyperparameter will run it for no more than four epics because there's only a,000 training examples. That'll be a total of 4,000 steps. So, a thousand steps times four, 4,000. What does that look when we build that script? The what are the result? Simple loss declines over 4,000 steps overall while copa accuracy improves. Really great. We've been able to teach the model to be more common sensical. Love it. Um, and here you could see balance copa accuracy improving after about 2,000 steps. So let's make a couple of more decisions. This slide is meant for AI coding assistant. Um number one, we'll use an optimizer of AdamW fused, right? So we need an we still need an optimizer. We haven't really changed that from back propagation.

Hyperparameter will run batch size of one. Why? This is a very simple optimization to do this is a trivial RL feature. Copa formatting will be something fu because bar. Um so we cut the grass because the grass was too long and we'll to show two options and the results we should have random pre-train instruct tuning eval every 100 parameters. We should be able to see that and then we want to include a chart for pair accuracy tracking.

how do we do that? One option is you can ask you can write this code yourself. I believe in your ability to do that. That's not a big difference from our pre-training script. We load those weights, we change a couple, we change the function, we now know the math. So, that's an option. I don't think a lot of people do that. Another option is to have an AI coding assistant take this deck, the pre-training, the pre-training script, the instruct tuning script, and say, "Hey, can you please build the RL script for me?" So, let's say that's an option. Also, we could use go Justin Angel AI/ Lego, when I do any of those options, let's look at a quick script that we can learn from. So we have our configuration. This

which we've been building all along. It knows my activation function and my GPU and my FFN and so on. And then I could say, hey, can you build the RL script for me for epox? Uh, this is the optimizer. Here's how you format Copa. Here's the benchmark so on. It's already pre-built here. You copy this into claude or JGPT or Gemini or whatever and it can generate you these scripts. So

<a id="implementing-the-rl-script"></a>
### Implementing the RL Script

is our simple config. Beta, gamma, learning rate, number of epics, eval xsteps, maximum grade norm. So gra gradient clipping. Um then we have the rest of our architecture for our GPT2 model. Again, rel square messes us up because we have to always keep declaring it in every script because it's so atypical.

And then simple. So we have the simple formula which we learned in Excel. And then we have the implicit reward length normalized log probability explanation here. So simple lost chosen input chosen target rejected input rejected target.

We calculate the logits for each one of the chosen inputs and rejected inputs. We length normalize it minus sigmoid, right? Remember we let we normalize it. Beta time multiply by chosen reward minus rejected reward minus gamma. This is the stuff that we did in Excel. F

of log negative f log sigmoid of the

reward margin. This is exactly the code that we had in Excel. And then we return that value. For evaluation, we implemented balance copa. Again, we should never really be implementing our own our own test harnesses. We should allow another framework that's already implemented to do that. It's going to be more consistent, but I wanted to have a self-contained script. We load the data for balanced for balanced copa. It's

called balanced, by the way, because there's equal amounts of A and B. we load the training data and we also load the test data. So 1,000 examples for training, 500 examples for test

and it says so right here. And then we run a training loop. What's fun about this training loop? It's got W. It's running epox. It's doing zero grad. It's doing backward. It does steps. It does clip norms. What's the really interesting thing about it? It's because it's going to do loss function, not cross entropy. Notice there's no cross entropy anymore. It's going to do cross entropy on the simple loss. So it takes

in the chosen tokens, the rejected tokens, the pre beta, gamma, all of that and then it calculates the simple loss function. So our and then we do back propagation based on it. Great. So let's run that. We ran that.

<a id="results-and-accuracy-gains"></a>
### Results and Accuracy Gains

Here we go. Step 50, step 100, so on. Let's try and look at the chart together. Let's look at what. So our random baseline for balance scopa would be 50%, it's A or B. Our pre-trained model performed at 55% so slightly above

random. That's great. Instruct tuned performed at 56% so slightly better. The instruction tuning did help a bit. But then once we do 4,000 steps now our and again we're not checking the we're training on the trained set, we're testing on the test set. The test set performance improved to 60%. Very cool

to notice that. Very cool to notice that. We could plot that all out in a graph. You can see balance copy accuracy did increase. Simple loss decreased. And the average reward margin, right? The margin between the rejected and the chosen is increasing. That's what we want. Great. So that was RL.

<a id="resources-and-open-questions"></a>
### Resources and Open Questions

And with that, I want to recommend a couple of RL resources. RL can easily be a full day workshop as I think I've apologized for five times already. One thing that you can watch if you only have an hour, I really love this intro from Professor Tom Yay. I think he only recorded this less than a month ago. Really worth watching, he goes over PO, DPO, GRPO in an Excel way I do. Another option is you could read the rlfbook.com from Nathan. You could also buy the

physical book. I think it's going to be out in July. I will mention that I found that a bit mathy for me. I'm not really a mathy guy. So worth reading it with a mathy lens. Or you could read RLVR book from Ken. I actually thought it was really lovely and it was very code forward. It's lots of code sample code by code by code. So, however you learn best, you have two resources. Now, additionally, I think it's worth mentioning that there's a bunch of open source models that there's a lot to learn from on how to do RLO 3. Almo is

Nate Nathan's open source model. Really worth noticing that it probably have went as deep on RL as anyone has gone on. Uh we have the DeepSik paper here.

They really did innovate as well. We have the Quen 3 model and GLM5. Each of these have added a lot into RL and have very interesting tidbits here. Which model didn't I mention? For example, AR R key trinity. Why didn't I mention it as a resource for RL? They have this. I can't even remember the number. I think it's a trillion parameters or something. Almost no RL few thousand runs of RL. I'm guessing on safety and that's it. Right. They've done as much RL in that model as I ran on simple for my tiny model. So why is that important? That model performs super well on many things, right? It's not state-of-the-art, but it's not super far behind. It brings into question why we even need RL. And I think that's an open discussion that we won't know the answer for in mid26. After this, we finished covering RL. We

finished covering instruction tuning. We finished covering pre-training, post-training, we've covered architecture. There's a bunch of stuff we didn't cover. So hopefully you could join me for another five minutes where we maybe cover the stuff we didn't cover. At least you know what you don't know at the end of this. Thank you so much and I hope you could join me for another few minutes at the for our last section together. Thank you so much.

