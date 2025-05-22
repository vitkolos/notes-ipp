# Exam

The exam will have 10 questions, mostly from this pool. In general, none of them requires you to memorize formulas, but you should know the main ideas and principles.

## Introduction

- What's the difference between task-oriented and non-task-oriented systems?
- Describe the difference between closed-domain, multi-domain, and open-doman systems.
- Describe the difference between user-initiative, mixed-initiative, and system-initiative systems.

## Linguistics of Dialogue

- What are turn taking cues/hints in a dialogue? Name a few examples.
- Explain the main idea of the speech acts theory.
- What is grounding in dialogue?
- Give some examples of grounding signals in dialogue.
- What is deixis? Give some examples of deictic expressions.
- What is coreference and how is it used in dialogue?
- What does Shannon entropy and conditional entropy measure? No need to give the formula, just the principle.
- What is entrainment/adaptation/alignment in dialogue?

## Data & Evaluation

- What are the typical options for collecting dialogue data?
- How does Wizard-of-Oz data collection work?
- What is corpus annotation, what is inter-annotator agreement?
- What is the difference between intrinsic and extrinsic evaluation?
- What is the difference between subjective and objective evaluation?
- What are the main extrinsic evaluation techniques for task-oriented dialogue systems?
- What are some evaluation metrics for non-task-oriented systems (chatbots)?
- What's the main metric for evaluating ASR systems?
- What's the main metric for NLU (both slots and intents)?
- Explain an NLG evaluation metric of your choice.
- Why do you need to check for statistical significance (when evaluating an NLP experiment and comparing systems)?
- Why do you need to evaluate on a separate test set?

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
