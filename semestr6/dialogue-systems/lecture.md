# Lecture

- credit requirements
	- final exam
	- lab exercises
- <https://web.stanford.edu/~jurafsky/slp3/>
- communication domains
	- single/closed-domain
	- multi-domain
	- open-domain
- application areas
	- phone
	- apps
	- smart speakers
	- appliances
	- cars
	- web
	- embodied (robots)
	- virtual characters
- modes of communication
	- text
	- voice
	- multimodal – video, mimics, touch, …
- dialogue initiative
	- system-initiative
	- user-initiative
	- mixed-initiative
- traditional architecture
	- main loop
		- voice → text → meaning → reaction → text → voice
	- components
		- speech recognition
		- language understading
		- dialogue management
			- has access to backend (in order to perform tasks)
		- language generation
		- speech synthesis
	- multimodal system would have additional components
- automatic speech recognition (ASR)
	- converting speech signal into text
	- typically produces several possible hypotheses with confidence scores
		- n-best list
		- lattice
		- confusion network
	- very good in ideal conditions
	- problems: noise, accents, distance, channel (phone), …
	- voice activity detection
		- is the user talking to the system?
		- wake words (OK, Google)
	- ASR is usually implemented using neural networks
- natural/spoken language understanding (NLU/SLU)
	- extracting the meaning from the user utterance
	- converting into a structured semantic representation
		- dialogue acts
			- act type/intent (inform, request, confirm)
			- slot/attribute
			- value
		- examples
			- inform(food=Chinese, price=cheap)
			- request(address)
		- can be more complex (using syntax trees, predicate logic)
	- specific steps
		- named entity recognition
		- coreference resolution
	- implementation varies
		- handcrafting often works for limited domains
			- keyword spotting, regular expressions, handcrafted grammars
		- machine learning approaches
	- can also provide n-best outputs
	- problems
		- recovering from bad ASR
		- ambiguities – next Friday (it is Tuesday now)
		- variation – there are many ways to express the same thing
- dialogue manager (DM)
	- stores dialogue history modeled by dialogue state
		- handcrafted × probabilistic
		- handcrafted … just replace the value in the slot by the last-mentioned
		- probabilistic … keep an estimate
	- system actions described by dialogue policy
		- decision on next system action, given dialogue state
		- involves backend queries
		- result represented as system dialogue act
		- handcrafted
			- if-then-else clauses
			- flowcharts
		- machine learning
			- often trained with reinforcement learning
			- POMDP (partially observable markov decision process)
			- recurrent neural networks
- natural language generation (NLG)
	- how to express things might depend on context
	- goals: fluency, naturalness, avoid repetition, …
	- traditional approach: templates
		- fill in values into predefined templates (sentence skeletons)
		- works well for limited domains
	- grammar-based approaches
		- grammar/semantic structures
		- syntactic transformation rules are applied
	- statistical approaches
		- most prominent: transformer neural networks
		- generating word-by-word
- speech synthesis
	- standard pipeline: text normalization, pronunciation analysis, intonation/stress generation, waveform synthesis
	- TTS methods
		- formant-based – phoneme-specific frequencies, rules
		- concatenative – record a single person, cut into phoneme transitions
		- hidden Markov models
		- neural networks
			- no need for phoneme conversion, can go directly from text
			- text to spectrograms → vocoder (spectrogram to audio)
- organizing the components
	- basic – pipeline
		- components oblivious of each other
	- interconnected
		- read/write changes to dialogue state
		- more reactive but more complex
	- joining the modules
		- ASR + NLU
		- NLU + state tracking
		- NLU & DM & NLG – using LLMs, may be end-to-end (without module separation)
		- audio based end-to-end (audio-to-audio)
- research areas
	- LLM-based systems
	- dialogue flows from data – finding patterns in human dialogue recordings/transcripts
	- multimodality – adding video (input/output)
	- context dependency – understand/reply in context (grounding, speaker adaptation)
	- incrementality – don't wait for the whole sentence to start processing
