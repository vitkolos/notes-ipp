# Labs

- for the sake of our homework … $p(w_1,w_2,\dots,w_n)\approx \prod_i p(w_i)$ (unigram)
	- or $\approx\prod_i p(w_{i}\mid w_{i-1})$ (bigram)
- n-gram language models
- task
	- create text corpus
		- popular corpora
			- Brown, CNK, PDT
			- Common Crawl, Internet Archive, arXiv
			- RedPajama
		- what we can use
			- books (Gutenberg)
			- Wikipedia, W2C
		- we should store the data as 1 plaintext file, the size should be at least 500k tokens (words), UTF-8, at least 2 languages (one of them should be English), one file for each language
	- unigram statistics
		- guess 10 frequent words
		- compute 10 frequent words
		- show least frequent words
		- show unigram p's of efverything
	- tokenize data
		- Sacremoses
		- we may use truecase
	- bigram stats
		- guess top 10 frequent bigram
		- function for joint & conditional probability
			- for most frequent unigrams (or some words)
		- show top 10 bigrams
- homework assignment
	- estimate character 3-gram (trojice znaků) probabilities from data
	- get test data, compute its probability
	- calculate cross-entropy of the test data
	- calculate probability that test data belong to the language
	- deadline cca in 4 weeks
- corpora
	- TEITOK Universal Dependencies
	- querying in CQL
- information retrieval – assignment
	- implement simple IR system
	- we will be given a document collection and queries
	- the goal is to process the queries, generate the output, and evaluate the results
	- steps
		- inverted index
		- boolean query operators (AND, OR, AND NOT)
		- query set
		- evaluation (precision, recall)
		- submission
	- the test data should not be distributed
	- the topics are quite rich – we need only the num and the query
		- the description and the narative we used for human evaluation of the document relevance
	- there are parallel queries in both languages, we should use them for the respective documents
	- we index only the textual content of the documents
	- the files are in SGML, XML parser might not work, we can use regex
	- the minimum is to do lowercasing and punctuation removal
		- we can do also lemmatisation, stemming etc. but it is not necessary
	- details tomorrow on the website
- Levenshtein edit distance
	- basic operations: insert, delete, replace
	- Damerau-Levenshtein: transposition as a fourth possible operation
	- weighted edit distance – weights correspond to the distance on the keyboard (if we want to detect mistyping/misspelling)
- úkol: interpretovat neuronku – pokud bychom ji nezvládli vytvořit, tak nám ji pošle (blízko deadlinu)
	- můžeme přidat vlastní slovní druh pro neúplná slova
	- pro zpětnou vazbu před deadlinem mu můžeme poslat e-mail
- https://colab.research.google.com/drive/1ukk3OsonPqdVt-tL0c3CKGDOSq32OjnH?usp=sharing
- attention_mask tells the transformer what is a valid content of the sentence and what is padding
- the model has a training mode – it uses dropout technique to make the model more robust
- our (first) task
	- take a sentence
	- assign word embeddings to the words
	- average the embeddings
