# Exam

## Basic notions from probability and information theory

- What are the three basic properties of a probability function?
	- $p:2^\Omega\to[0,1]$
	- $p(\Omega)=1$
	- it holds $p(\bigcup_i A_i)=\sum_i p(A_i)$ for disjoint events $A_1,\dots,A_n\subseteq\Omega$
	- ($\Omega$ is a sample space / set of possible basic outcomes)
- When do we say that two events are (statistically) independent?
	- $A,B$ are independent iff $p(A\cap B)=p(A)\cdot p(B)$
	- or $p(B\mid A)=p(B)$
- Show how Bayes' Theorem can be derived.
	- $p(A\cap B)=p(B\cap A)$
		- or $p(A,B)=p(B,A)$
	- $p(A\mid B)\cdot p(B)=p(B\mid A)\cdot p(A)$
		- from the definition of conditional probability $p(A\mid B)=\frac{p(A,B)}{p(B)}$
	- theorem: $p(A\mid B)=\frac{p(B\mid A)\cdot p(A)}{p(B)}$
- Explain Chain Rule.
	- chain rule: $p(A_1,A_2,A_3,\dots,A_n)=p(A_1\mid A_2,A_3,\dots,A_n)\cdot p(A_2\mid A_3,\dots,A_n)\cdot\ldots$
		- $\cdot\,p(A_{n-1}\mid A_n)\cdot p(A_n)$
	- if follows directly from the definition of conditional probability (or from Bayes rule) as $p(A_1,(A_2,\dots,A_n))=p(A_1\mid (A_2,\dots,A_n))\cdot p(A_2,\dots,A_n)$ etc.
- Explain the notion of Entropy (formula expected too).
	- measure of uncertainty
	- higher entropy → higher uncertainty → higher "surprise"
	- $H(X)=-\sum_{X\in\Omega}p(X)\log_2 p(X)$
	- or $H(X)=\mathbb E[\log_2(\frac1{p(X)})]$
	- coding interpretation: the least (average) number of bits needed to encode a message
	- note that $H(X)\geq 0$
- Explain Kullback-Leibler distance (formula expected too).
- Explain Mutual Information (formula expected too).

## Language models, the noisy channel model

- Explain the notion of The Noisy Channel.
- Explain the notion of the n-gram language model.
- Describe how Maximum Likelihood estimate of a trigram language model is computed. (2 points)
- Why do we need smoothing (in language modelling)?
- Give at least two examples of smoothing methods. (2 points)

## Morphological analysis

- What is a morphological tag? List at least five features that are often encoded in morphological tag sets.
- List the open and closed part-of-speech classes and explain the difference between open and closed classes.
- Explain the difference between a finite-state automaton and a finite-state transducer. Describe the algorithm of using a finite-state transducer to transform a surface string to a lexical string (pseudocode or source code in your favorite programming language). (2 points)
- Give an example of a phonological or an orthographical change caused by morphological inflection (any natural language). Describe the rule that would take care of the change during analysis or generation. It is not required that you draw a transducer, although drawing a transducer is one of the possible ways of describing the rule.
- Give an example of a long-distance dependency in morphology (any natural language). How would you handle it in a morphological analyzer?

## Syntactic analysis

- Describe dependency trees, constituent trees, differences between them and phenomena that must be addressed when converting between them. (2 points)
- Give an example of a sentence (in any natural language) that has at least two plausible, semantically different syntactic analyses (readings). Draw the corresponding dependency trees and explain the difference in meaning. Are there other additional readings that are less probable but still grammatically acceptable? (2 points)
- What is coordination? Why is it difficult in dependency parsing? How would you capture coordination in a dependency structure? What are the advantages and disadvantages of your solution?
- What is ellipsis? Why is it difficult in parsing? Give examples of different kinds of ellipsis (any natural language).

## Information retrieval

- Explain the difference between information need and query.
- What is inverted index and what are the optimal data structures for it?
- What is stopword and what is it useful for?
- Explain the bag-of-word principle?
- What is the main advantage and disadvantage of boolean model.
- Explain the role of the two components in the TF-IDF weighting scheme.
- Explain length normalization in vector space model what is it useful for?

## Language data resources

- Explain what a corpus is.
- Explain what annotation is (in the context of language resources). What types of annotation do you know? (2 points)
- What are the reasons for variability of even basic types of annotation, such as the annotation of morphological categories (parts of speech etc.).
- Explain what a treebank is. Why trees are used? (2 points)
- Explain what a parallel corpus is. What kind of alignments can we distinguish? (2 points)
- What is a sentiment-annotated corpus? How can it be used?
- What is a coreference-annotated corpus?
- Explain how WordNet is structured?
- Explain the difference between derivation and inflection?

## Evaluation measures in NLP

- Give at least two examples of situations in which measuring a percentage accuracy is not adequate.
- Explain: precision, recall
- What is F-measure, what is it useful for?
- What is k-fold cross-validation ?
- Explain BLEU (the exact formula not needed, just the main principles).
- Explain the purpose of brevity penalty in BLEU.
- What is Labeled Attachment Score (in parsing)?
- What is Word Error Rate (in speech recognition)?
- What is inter-annotator agreement? How can it be measured?
- What is Cohen's kappa?

## Deep learning for NLP

- Describe the two methods for training of the Word2Vec model.
- Use formulas to describe how Word2Vec is trained with negative sampling. (2 points)
- Explain the difference between Word2Vec and FastText embeddings.
- Sketch the structure of the Transformer model. (2 points)
- Why do we use positional encodings in the Transformer model.
- What are residual connections in neural networks? Why do we use them?
- Use formulas to express the loss function for training sequence labeling tasks.
- Explain the pre-training procedure of the BERT model. (2 points)
- Explain what is the pre-train and finetune paradigm in NLP.
- Describe the task of named entitity recognition (NER). Explain the intution behind the CRF models compared to standard sequence labeling. (2 points)
- Explain how does the self-attention differ in encoder-only and decoder-only models.

## Machine translation fundamentals

- Why is MT difficult from linguistic point of view? Provide examples and explanation for at least three different phenomena. (2 points)
- Why is MT difficult from computational point of view?
- Briefly describe at least three methods of manual MT evaluation. (1-2 points)
- Describe BLEU. 1 point for the core properties explained, 1 point for the (commented) formula.
- Describe IBM Model 1 for word alignment, highlighting the EM structure of the algorithm.
- Explain using equations the relation between Noisy channel model and log-linear model for classical statistical MT. (2 points)
- Describe the loop of weight optimization for the log-linear model as used in phrase-based MT.

## Neural machine translation

- Describe the critical limitation of PBMT that NMT solves. Provide example training data and example input where PBMT is very likely to introduce an error.
- Use formulas to highlight the similarity of NMT and LMs.
- Describe, how words are fed to current NMT architectures and explain why is this beneficial over 1-hot representation.
- Sketch the structure of an encoder-decoder architecture of neural MT, remember to describe the components in the picture (2 points)
- What is the difference in RNN decoder application at training time vs. at runtime?
- What problem does attention in NMT address? Provide the key idea of the method.
- What problem/task do both RNN and self-attention resolve and what is the main benefit of self-attention over RNN?
- What are the three roles each state at a Transformer encoder layer takes in self-attention.
- What are the three uses of self-attention in the Transformer model?
- Provide an example of NMT improvement that was assumed to come from additional linguistic information but occurred also for a simpler reason.
- Summarize and compare the strategy of "classical statistical MT" vs. the strategy of neural approaches to MT.
