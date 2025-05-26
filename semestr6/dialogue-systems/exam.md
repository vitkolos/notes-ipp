# Exam

The exam will have 10 questions, mostly from this pool. In general, none of them requires you to memorize formulas, but you should know the main ideas and principles.

## Introduction

- What's the difference between task-oriented and non-task-oriented systems?
	- task-oriented
		- focused on completing certain tasks (booking restaurants/flights/hotels, finding bus schedules, smart home, …)
		- most actual dialogue systems in production
		- “backend access” vs. “agent/assistant”
	- non-task-oriented
		- chitchat – social conversation, entertainment
			- getting to know the user, specific persona
		- gaming the Turing test
- Describe the difference between closed-domain, multi-domain, and open-domain systems.
	- single/closed-domain – on a well-defined area, small set of specific tasks (e.g. banking system on a specific phone number)
	- multi-domain – joining several single-domain systems
	- open-domain – “responds to anything”, used to be mostly chitchat, now somewhat working via LLMs
- Describe the difference between user-initiative, mixed-initiative, and system-initiative systems.
	- user-initiative – user asks, machine responds
	- system-initiative – “form-filling”, system asks questions, user must reply (traditional, most robust, least natural)
	- mixed-initiative – system and user both can ask & react to queries; most natural, most complex

## Linguistics of Dialogue

- What are turn taking cues/hints in a dialogue? Name a few examples.
	- a speaker can use a turn taking cue/hint to signalize when their turn ends (they yield)
	- examples: linguistic (e.g. finished sentence), voice pitch, timing (gaps), eye gaze, gestures, …
- Explain the main idea of the speech acts theory.
	- each utterance is an act: intentional, changing the state of the world (changing the knowledge/mood of the listener, influencing their behavior)
	- speech acts consist of several levels: the words, their semantics, meaning, effect
	- types of speech acts: assertive, directive, commissive, expressive, declarative
	- explicit vs. implicit; direct vs. indirect
		- explicit: I **promise** to come by later.
		- implicit: I'll come by later.
		- direct: Please close the window.
		- indirect: Could you close the window?
		- even more indirect: I'm cold.
- What is grounding in dialogue?
	- dialogue is cooperative → need to ensure mutual understanding
	- common ground = shared knowledge, mutual assumptions of dialogue participants
		- the knowledge has to be *knowingly* shared
	- common ground is expanded/updated/refined in an informative conversation
	- validated/verified via grounding feedback/evidence
		- speaker presents utterance
		- listener accepts utterance by providing evidence of understanding
	- information added to common ground only after acceptance
- Give some examples of grounding signals in dialogue.
	- positive – understanding/acceptance signals
		- visual – eye gaze, facial expressions, smile
		- backchannels – particles (částice) signalling understanding (uh-uh, hmm, yeah, …)
		- explicit feedback – explicitly stating understanding (I know; yes, I understand)
		- implicit feedback – showing understanding implicitly in the next utterance
	- negative – misunderstanding
		- visual – stunned/puzzled silence
		- implicit/explicit repairs – denying (no, that's not right) / presenting alternative
		- clarification requests – demonstrating ambiguity & asking for additional information (Which John? John Smith or John Doe?)
		- repair requests – showing non-understanding & asking for correction (Oh, so you're not flying to London? Where are you going then?)
- What is deixis? Give some examples of deictic expressions.
	- “pointing” – relating between language & context/world
		- dialogue is typically set/situated in a specific context
	- deictic expressions
		- their meaning depends on the context (who is talking, when, where)
		- pronouns (I, you, him, this)
		- verbs: tense & person markers
		- adverbs (here, now, yesterday)
		- lexical meaning (come × go)
		- non-verbal (gestures, gaze)
	- typically egocentric
	- main types of deixis
		- personal – I, me, you, she
		- temporal – now, yesterday, later, on Monday
		- local – here, there
	- other types: social (politeness), discourse/textual (next chapter)
- What is coreference and how is it used in dialogue?
	- expression referring to something mentioned in context
		- anaphora = referring back
		- cataphora = referring forward
	- avoiding repetition, faster expression
	- can refer to basically anything (objects/persons/events, qualities, actions / full sentences / portions of text)
	- used frequently in dialogue, may be ambiguous
	- examples
		- anaphora: Susan dropped the plate. **It** shattered.
		- cataphora: When **he** hears that fire alarm, Sam is always cool and calm.
		- I don't like it as much as he **does**.
		- Her dress is green. **So** is mine.
		- Shall I book a room for you? – Sure, I'd like **that**.
		- ambiguity: Bill stands next to John. **He** is tall.
- What does Shannon entropy and conditional entropy measure? No need to give the formula, just the principle.
	- entropy – expected value of information conveyed (in bits)
		- $H(\mathrm{text})=-\mathbb E[\log p(\mathrm{word})]$
	- entropy plays well with the social interaction perspective
		- people tend to use all available channel capacity
		- people tend to spread information evenly (words carrying more information are emphasized)
	- conditional entropy – how hard is to guess the next word in the sentence?
		- given preceding context (n-gram)
		- related to Shannon entropy but may differ (it is typically much lower than Shannon entropy)
		- better estimate of prediction difficulty (although humans work with “unlimited” preceding context and reevaluate using following context)
		- $H_\mathrm{cond}(\mathrm{text})=-\mathbb E_p[\log\frac{p(c,w)}{q(c)}]$
- What is entrainment/adaptation/alignment in dialogue?
	- people subconsciously adapt/align/entrain to their dialogue partner over the course of the dialogue
		- wording (lexical items) – they use the same words as their dialogue partner
		- grammar (sentential constructions)
		- speech rate, prosody, loudness
		- accent/dialect – BrE speaker uses AmE words when talking to AmE speaker
	- this helps a successful dialogue (also helps social bonding, feels natural)
	- systems typically don't align, people align to dialogue systems

## Data & Evaluation

- What are the typical options for collecting dialogue data?
	- in-house collection using experts or students
		- safe, high-quality, but very expensive & time-consuming
		- free talk / scripting whole dialogues / Wizard-of-Oz
	- web crawling
		- fast & cheap, but typically not real dialogues, may not be fit for purpose
		- potentially unsafe (offensive stuff)
		- need to be careful about the licensing
	- crowdsourcing
		- compromise: employing (untrained) people over the web
		- crowd workers tend to game the system
- How does Wizard-of-Oz data collection work?
	- users believe they're talking to a system → their behavior is simpler than when talking to a human
	- system is in fact controlled by a human “wizard”, who is selecting options (free typing is too slow)
	- usage: in-house data collection, prototyping/evaluating the system before implementing it
- What is corpus annotation, what is inter-annotator agreement?
	- annotation = labels, description added to the collected data (dialogues)
		- transcriptions
		- semantic annotation (NLU: dialogue acts, …)
		- named entity labelling (NLU)
	- inter-annotator agreement (IAA)
		- measures the reliability of manual annotations
		- multiple people annotate the same thing
		- needs to account for agreement by chance
		- typical measure: Cohen's kappa
			- $\kappa=\frac{\text{agreement}-\text{chance}}{1-\text{chance}}$
- What is the difference between intrinsic and extrinsic evaluation?
	- intrinsic … checks properties of systems/components in isolation, self-contained
	- extrinsic … how the system/component works in its intended purpose
		- effect of the system on something outside itself, in the real world (i.e. user)
- What is the difference between subjective and objective evaluation?
	- subjective … asking users' opinions, e.g. questionnaires (manual)
		- not repeatable
		- we should ask many people → not so subjective
	- objective … measuring properties directly from data (automatic)
		- might or might not correlate with users' perception
- What are the main extrinsic evaluation techniques for task-oriented dialogue systems?
	- objective metrics (we record people interacting with the system, analyze the logs)
		- task success / goal completion rate – did the user get what they wanted?
			- testers can have agenda → we can check if they found what they were supposed to
			- basic check: did we provide any information at all? (any bus/restaurant)
		- duration – number of turns or time (less is better)
		- retention rate – percentage of users that return to use our dialogue system again (over a time period)
		- fallback rate – percentage of failed dialogues
		- number of total/new/active users
	- subjective evaluation
		- questionnaires for users/testers
		- example questions
			- success rate: Did you get all the information you wanted?
			- future use: Would you use the system again?
			- ASR/NLU: Do you think the system understood you well?
			- NLG: Were the system replies fluent/well-phrased?
			- TTS: Was the system's speech natural?
- What are some evaluation metrics for non-task-oriented systems (chatbots)?
	- objective metrics
		- duration (longer = better)
		- other: % returning users, checks for users swearing vs. thanking the system
	- subjective
		- likeability/engagement: Did you enjoy the conversation?
		- other similar to task-oriented
- What's the main metric for evaluating ASR systems?
	- word error rate (WER)
	- ASR output is compared to human-authored reference
	- $\mathrm{WER}=\frac{S+I+D}{N}$
		- $S$ … substitutions
		- $I$ … insertions
		- $D$ … deletions
		- $N$ … reference length
	- ~ length-normalized edit distance (Levenshtein distance)
	- sometimes insertions & deletions are weighted $0.5\times$
	- can be $\gt 1$
	- assumes one correct answer
- What's the main metric for NLU (both slots and intents)?
	- slots: precision, recall, F-measure (F1)
		- precision $P=\frac{\mathrm{correct}}{\mathrm{detected}}$
		- recall $R=\frac{\mathrm{correct}}{\mathrm{true}}$
		- F-measure $F=\frac{2PR}{P+R}$ harmonic mean
		- example
			- NLU: inform(name=Golden Dragon, food=Chinese)
			- true: inform(name=Golden Dragon, food=Czech, price=high)
			- $P=1/3,\;R=1/2,\;F=0.2$
	- accuracy (% correct) used for intent/act type
		- alternatively also exact matches on the whole semantic structure (easier, but ignores partial matches)
		- one true answer assumed
- Explain an NLG evaluation metric of your choice.
	- BLEU score
		- word-overlap with reference text(s)
		- $BLEU=BP\cdot\sqrt[4]{p_1p_2p_3p_4}$
		- $p_n$ … $n$-gram precision (how many $n$-grams of the output text exist in any reference text)
		- $BP$ … brevity penalty (short sentences achieve higher $n$-gram precisions, so we penalize them)
	- slot error rate
	- diversity – can our system produce different replies?
- Why do you need to check for statistical significance (when evaluating an NLP experiment and comparing systems)?
	- higher score is not enough to prove your model is better
		- it can happen by chance
	- we need to define the hypotheses and select a significance level $\alpha$, then compute the observed value of test statistic and reject $H_0$ or not
- Why do you need to evaluate on a separate test set?
	- we want to know how well our model works on new, unseen data (how well it generalizes)
	- memorizing training data would give us 100% accuracy (on training data)

## Natural Language Understanding

- What are some alternative semantic representations of utterances, in addition to dialogue acts?
- Describe language understanding as classification and language understanding as sequence tagging.
- How do you deal with conflicting slots or intents in classification-based NLU?
- What is delexicalization and why is it helpful in NLU?
- Describe one of the approaches to slot tagging as sequence tagging.
- What is the IOB/BIO format for slot tagging?
- What is the label bias problem?
- How can an NLU system deal with noisy ASR output? Propose an example solution.

## Neural NLU & Dialogue State Tracking

- Describe an example of a neural architecture for NLU.
- How can you use pretrained language models in NLU?
- What is the dialogue state and what does it contain?
- What is an ontology in task-oriented dialogue systems?
- Describe the task of a dialogue state tracker.
- What's a partially observable Markov decision process?
- Describe a viable architecture for a belief state tracker.
- What is the difference between dialogue state and belief state?
- What's the difference between a static and a dynamiic state tracker?
- How can you use pretrained language models or large language models for state tracking?

## Dialogue Policies

- What are the non-statistical approaches to dialogue management/action selection?
- Why is reinforcement learning preferred over supervised learning for training dialogue managers?
- Describe the main idea of reinforcement learning (agent, environment, states, rewards).
- What are deterministic and stochastic policies in dialogue management?
- What's a value function in a reinforcement learning scenario?
- What's the difference between actor and critic methods in reinforcement learning?
- What's the difference between model-based and model-free approaches in RL?
- What are the main optimization approaches in reinforcement learning (what measures can you optimize and how)?
- Why do you typically need a user simulator to train a reinforcement learning dialogue policy?

## Neural Policies & Natural Language Generation

- How do you involve neural networks in reinforcement learning (describe a Q network or a policy network)?
- What are the main steps of a traditional NLG pipeline – describe at least 2.
- Describe one approach to NLG of your choice.
- Describe how template-based NLG works.
- What are some problems you need to deal with in template-based NLG?
- Describe a possible neural networks based NLG architecture.
- How can you use pretrained language models or large language models in NLG?

## Voice assistants & Question Answering

- What is a smart speaker made of and how does it work?
- Briefly describe a viable approach to question answering.
- What is document retrieval and how is it used in question answering?
- What is dense retrieval (in the context of question answering)?
- How can you use neural models in answer extraction (for question answering)?
- How can you use retrieval-augmented generation in question answering?
- What is a knowledge graph?

## Dialogue Tooling

- What is a dialogue flow/tree?
- What are intents and entities/slots?
- How can you improve a chatbot in production?
- What is the containment rate (in the context of using dialogue systems in call centers)?
- What is retrieval-augmented generation?

## Automatic Speech Recognition

- What is a speech activity detector?
- Describe the main components of an ASR pipeline system.
- How do input features for an ASR model look like?
- What is the function of the acoustic model in a pipeline ASR system?
- What's the function of a decoder/language model in a pipeline ASR system?
- Describe an (example) architecture of an end-to-end neural ASR system.

## Text-to-speech Synthesis

- How do humans produce sounds of speech?
- What's the difference between a vowel and a consonant?
- What is F0 and what are formants?
- What is a spectrogram?
- What are main distinguishing characteristics of consonants?
- What is a phoneme?
- What are the main distinguishing characteristics of different vowel phonemes (both how they're produced and perceived)?
- What are the main approaches to grapheme-to-phoneme conversion in TTS?
- Describe the main idea of concatenative speech synthesis.
- Describe the main ideas of statistical parametric speech synthesis.
- How can you use neural networks in speech synthesis?

## Chatbots

- What are the three main approaches to building chitchat/non-task-oriented open-domain chatbots?
- How does the Turing test work? Does it have any weaknesses?
- What are some techniques rule-based chitchat chatbots use to convince their users that they're human-like?
	- signalling understanding – repeating and reformulating user's phrasing
	- good framing – it's easier to appear human as a therapist (or paranoid schizophrenic, Ukrainian boy, …)
- Describe how a retrieval-based chitchat chatbot works.
	- it first checks for similar inputs in the corpus
		- rough retrieval
	- then it retrieves and reranks corresponding outputs
	- …
- How can you use neural networks for chatbots (non-task-oriented, open-domain systems)? Does that have any problems?
- Describe a possible architecture of an ensemble non-task-oriented chatbot.
- What do you need to train a large language model?
- What are some issues you may encounter when chatting to LLMs?
