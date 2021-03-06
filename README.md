
# NLP Cheat Sheet - Python - Starter Kit - Nomenclature


Demo: [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/janlukasschroeder/nlp-cheat-sheet-python/master?filepath=NLP%2BCheat%2BSheet.ipynb)

Stack
- Python 3.6 (only! Run in venv if necessary)
- spacy
- lexnlp

### Installation:
spacy
```shell
pip install spacy
python -m spacy download en 
# python -m spacy download en_core_web_lg
```
LexNLP ([installation guide here](https://github.com/LexPredict/lexpredict-contraxsuite/blob/master/documentation/Installation%20and%20Configuration/Installation%20and%20Configuration%20Guide.pdf))
```shell
pip install https://github.com/LexPredict/lexpredict-lexnlp/archive/master.zip
python # to open REPL console
>>> import nltk
>>> nltk.download() # download all packages
```

#### Popular frameworks:
- [GPT-2](https://openai.com/blog/better-language-models/) - generate fake news, text summaries
- BERT
- XLnet
- [ERNIE](https://github.com/PaddlePaddle/ERNIE/)
- [Holmes](https://github.com/msg-systems/holmes-extractor#the-basic-idea): document classification, search in documents

# Datasets

- [OntoNotes 5](https://github.com/ontonotes/conll-formatted-ontonotes-5.0) - corpus comprising various genres of text (news, conversational telephone speech, weblogs, usenet newsgroups, broadcast, talk shows) in three languages (English, Chinese, and Arabic) with structural information (syntax and predicate argument structure) and shallow semantics (word sense linked to an ontology and coreference).
- [wiki_en_tfidf.mm in gensim](https://radimrehurek.com/gensim/wiki.html#latent-semantic-analysis) 3.9M documents, 100K features (distinct tokens) and 0.76G non-zero entries in the sparse TF-IDF matrix. The Wikipedia corpus contains about 2.24 billion tokens in total.
- [GPT-2 Dataset](https://github.com/openai/gpt-2-output-dataset)
- [All the news, Kaggle, 143K articles](https://www.kaggle.com/snapcrack/all-the-news)
- [Daily news for stock market prediction](https://www.kaggle.com/aaron7sun/stocknews)

## CountVectorizer 
- Convert a collection of text documents to a matrix of token counts
- [skikitLearn](https://scikit-learn.org/stable/modules/generated/sklearn.feature_extraction.text.CountVectorizer.html)

# Demos

- [Stanford CoreNLP](http://corenlp.run/)
- [Stanford NER](http://nlp.stanford.edu:8080/ner/process)

# nltk (Python lib)

- similar to spacy
- supports more models and packages than spacy
- simply GUI model download `nltk.download()`

# gensim (Python lib)

- topic modelling for humans
- loads a corpus
- calcs similarities between query and indexed documents
- SparseMatrixSimilarity
- Latent Semantic Analysis

https://radimrehurek.com/gensim/

# lexnlp (Python lib)

- Information retrieval and extraction for real, unstructured legal text
- doesn't work; seemed to be excellent for legal + financial docs
- docs aren't very good

https://github.com/LexPredict/lexpredict-lexnlp

## Word embeddings (=word vectors)

- Word embeddings are vector representation of words. 
- Sentence: Word Embeddings are Word converted into numbers.
- A word in this sentence may be “Embeddings” or “numbers ” etc.
- A dictionary may be the list of all unique words in the sentence, eg [‘Word’,’Embeddings’,’are’,’Converted’,’into’,’numbers’]
- A vector representation of a word may be a one-hot encoded vector where 1 stands for the position where the word exists and 0 everywhere else. 

### Example

- numbers = [0,0,0,0,0,1] 
- converted = [0,0,0,1,0,0]

** Either use pre-trained word vectors or train our own** 

#### Pre-trained word embeddings:
- Word2Vec (Google, 2013), uses Skip Gram and CBOW
- [On Google News trained (1.5GB)](https://drive.google.com/file/d/0B7XkCwpI5KDYNlNUTTlSS21pQmM/edit) - vocabulary of 3 million words trained on around 100 billion words from the google news dataset
- GloVe (Stanford)
- [Stanford Named Entity Recognizer (NER)](https://nlp.stanford.edu/software/CRF-NER.shtml)
- [LexPredict: pre-trained word embedding models for legal or regulatory text](https://github.com/LexPredict/lexpredict-lexnlp)
- [LexNLP legal models](https://github.com/LexPredict/lexpredict-legal-dictionary) - US GAAP, finaical common terms, US federal regulators, common law

#### Create word vectors yourself

```python
import gensim
word2vev_model = gensim.models.word2vec.Word2Vec(sentence_list)
```

https://www.analyticsvidhya.com/blog/2017/06/word-embeddings-count-word2veec/

## 1. Frequency based word embeddings

### Count Vector (= Document Term Matrix)

![img](https://s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2017/06/04164920/count-vector.png)

### TF-IDF

Term Frequency - Inverse Document Frequency

### Co-Occurrence Vector


## 2. Prediction based word embeddings

Using Neural Networks

### CBOW (Continuous Bag of words)

![cbow](https://s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2017/06/04205949/cbow1.png)

### Skip Gram

Skip – gram follows the same topology as of CBOW. It just flips CBOW’s architecture on its head. The aim of skip-gram is to predict the context given a word

## Cosine Similarity

Compute cosine similarity between samples in X and Y.


## Linear Kernel

Compute the linear kernel between X and Y.



https://scikit-learn.org/stable/modules/generated/sklearn.metrics.pairwise.linear_kernel.html#sklearn.metrics.pairwise.linear_kernel

## Bag of Words


```python
# John likes to watch movies. Mary likes movies too.
BoW1 = {"John":1,"likes":2,"to":1,"watch":1,"movies":2,"Mary":1,"too":1};
```

# spacy


```python
import spacy
```


```python
# Import dataset
nlp = spacy.load("en")
# Import large dataset. Needs to be downloaded first.
# nlp = spacy.load("en_core_web_lg")
```

# Tokenization

Segmenting text into words, punctuation etc.


```python
doc = nlp("Larry Page founded Google in early 1990.")
[token.text for token in doc]
```




    ['Larry', 'Page', 'founded', 'Google', 'in', 'early', '1990', '.']



## BILUO tagging

ToDo: get list of labels, eg I, B, O


```python
[(token, token.ent_iob_, token.ent_type_) for token in doc]
```




    [(Larry, 'B', 'PERSON'),
     (Page, 'I', 'PERSON'),
     (founded, 'O', ''),
     (Google, 'B', 'ORG'),
     (in, 'O', ''),
     (early, 'B', 'DATE'),
     (1990, 'I', 'DATE'),
     (., 'O', '')]



# Stemming

ToDo

# Lemmatization

Assigning the base forms of words, for example: 
- "was" → "be"
- "rats" → "rat"


```python
doc = nlp("Was Google founded in early 1990?")
[(x.orth_, x.lemma_) for x in [token for token in doc]]
```




    [('Was', 'be'),
     ('Google', 'Google'),
     ('founded', 'found'),
     ('in', 'in'),
     ('early', 'early'),
     ('1990', '1990'),
     ('?', '?')]



# Spans
Part of a given text. So doc[2:4] is a span starting at token 2, up to – but not including! – token 4.


```python
doc = nlp("Larry Page founded Google in early 1990.")
span = doc[2:4]
span.text
```




    'founded Google'



# Sentence Detection

Finding and segmenting individual sentences.


```python
doc = nlp("Larry Page founded Google in early 1990. Sergey Brin joined.")
[sent.text for sent in doc.sents]
```




    ['Larry Page founded Google in early 1990.', 'Sergey Brin joined.']



# Part-of-speech (POS) Tagging

Assigning word types to tokens like verb or noun.



```python
doc = nlp("We are reading a text.")
[(x.orth_, x.pos_, spacy.explain(x.pos_)) for x in [token for token in doc]]
```




    [('We', 'PRON', 'pronoun'),
     ('are', 'VERB', 'verb'),
     ('reading', 'VERB', 'verb'),
     ('a', 'DET', 'determiner'),
     ('text', 'NOUN', 'noun'),
     ('.', 'PUNCT', 'punctuation')]




```python
[(x.orth_, x.tag_, spacy.explain(x.tag_)) for x in [token for token in doc]]
```




    [('We', 'PRP', 'pronoun, personal'),
     ('are', 'VBP', 'verb, non-3rd person singular present'),
     ('reading', 'VBG', 'verb, gerund or present participle'),
     ('a', 'DT', 'determiner'),
     ('text', 'NN', 'noun, singular or mass'),
     ('.', '.', 'punctuation mark, sentence closer')]



# Dependency Parsing	

Assigning syntactic dependency labels, describing the relations between individual tokens, like subject or object.


```python
doc = nlp("We are reading a text.")
# Dependency labels
[(x.orth_, x.dep_, spacy.explain(x.dep_)) for x in [token for token in doc]]
```




    [('We', 'nsubj', 'nominal subject'),
     ('are', 'aux', 'auxiliary'),
     ('reading', 'ROOT', None),
     ('a', 'det', 'determiner'),
     ('text', 'dobj', 'direct object'),
     ('.', 'punct', 'punctuation')]




```python
# Syntactic head token (governor)
[token.head.text for token in doc]
```




    ['reading', 'reading', 'reading', 'text', 'reading', 'reading']



# Base noun phrases



```python
doc = nlp("I have a red car")
[chunk.text for chunk in doc.noun_chunks]
```




    ['I', 'a red car']



# Named Entity Recognition (NER)

Labeling "real-world" objects, like persons, companies or locations.

## Alternatives to spacy

[LexNLP](https://lexpredict-lexnlp.readthedocs.io/en/latest/modules/extract/extract.html#pattern-based-extraction-methods) entities:
- acts, e.g., “section 1 of the Advancing Hope Act, 1986”
- amounts, e.g., “ten pounds” or “5.8 megawatts”
- citations, e.g., “10 U.S. 100” or “1998 S. Ct. 1”
- companies, e.g., “Lexpredict LLC”
- conditions, e.g., “subject to …” or “unless and until …”
- constraints, e.g., “no more than” or “
- copyright, e.g., “(C) Copyright 2000 Acme”
- courts, e.g., “Supreme Court of New York”
- CUSIP, e.g., “392690QT3”
- dates, e.g., “June 1, 2017” or “2018-01-01”
- definitions, e.g., “Term shall mean …”
- distances, e.g., “fifteen miles”
- durations, e.g., “ten years” or “thirty days”
- geographic and geopolitical entities, e.g., “New York” or “Norway”
- money and currency usages, e.g., “$5” or “10 Euro”
- percents and rates, e.g., “10%” or “50 bps”
- PII, e.g., “212-212-2121” or “999-999-9999”
- ratios, e.g.,” 3:1” or “four to three”
- regulations, e.g., “32 CFR 170”
- trademarks, e.g., “MyApp (TM)”
- URLs, e.g., “http://acme.com/”

Stanford NER entities:
- Location, Person, Organization, Money, Percent, Date, Time

NLTK
- NLTK maximum entropy classifier


```python
doc = nlp("Larry Page founded Google in the US in early 1990.")
# Text and label of named entity span
[(ent.text, ent.label_) for ent in doc.ents]
```




    [('Larry Page', 'PERSON'),
     ('Google', 'ORG'),
     ('US', 'GPE'),
     ('early 1990', 'DATE')]




```python
import lexnlp.extract.en as lexnlp
import nltk
```


```python
text = "There are ten cows in the 2 acre pasture."
print(list(lexnlp.amounts.get_amounts(text)))
```

    [10, 2.0]



```python
import lexnlp.extract.en.acts
text = "test section 12 of the VERY Important Act of 1954."
lexnlp.extract.en.acts.get_act_list(text)
```




    [{'location_start': 5,
      'location_end': 49,
      'act_name': 'VERY Important Act',
      'section': '12',
      'year': '1954',
      'ambiguous': False,
      'value': 'section 12 of the VERY Important Act of 1954'}]



# Text Classification

Assigning categories or labels to a whole document, or parts of a document.

# Similarity
How similar are two documents, sentences, token or spans?


```python
doc1 = nlp("I like cats")
doc2 = nlp("I like dogs")
# Compare 2 documents
doc1.similarity(doc2)
```




    0.957709143352323




```python
# "cats" vs "dogs"
doc1[2].similarity(doc2[2])
```




    0.83117634




```python
# "I" vs "like dogs"
doc1[0].similarity(doc2[1:3])
```




    0.46475163




```python
doc = nlp("I like cats")
# L2 norm of "I like cats"
doc.vector_norm
```




    4.706799587675896




```python
# L2 norm of "cats"
doc[2].vector_norm
```




    6.933004




```python
# Vector representation of "cats"
doc[2].vector
```




    array([-0.26763  ,  0.029846 , -0.3437   , -0.54409  , -0.49919  ,
            0.15928  , -0.35278  , -0.2036   ,  0.23482  ,  1.5671   ,
           -0.36458  , -0.028713 , -0.27053  ,  0.2504   , -0.18126  ,
            0.13453  ,  0.25795  ,  0.93213  , -0.12841  , -0.18505  ,
           -0.57597  ,  0.18538  , -0.19147  , -0.38465  ,  0.21656  ,
           -0.4387   , -0.27846  , -0.41339  ,  0.37859  , -0.2199   ,
           -0.25907  , -0.019796 , -0.31885  ,  0.12921  ,  0.22168  ,
            0.32671  ,  0.46943  , -0.81922  , -0.20031  ,  0.013561 ,
           -0.14663  ,  0.14438  ,  0.0098044, -0.15439  ,  0.21146  ,
           -0.28409  , -0.4036   ,  0.45355  ,  0.12173  , -0.11516  ,
           -0.12235  , -0.096467 , -0.26991  ,  0.028776 , -0.11307  ,
            0.37219  , -0.054718 , -0.20297  , -0.23974  ,  0.86271  ,
            0.25602  , -0.3064   ,  0.014714 , -0.086497 , -0.079054 ,
           -0.33109  ,  0.54892  ,  0.20076  ,  0.28064  ,  0.037788 ,
            0.0076729, -0.0050123, -0.11619  , -0.23804  ,  0.33027  ,
            0.26034  , -0.20615  , -0.35744  ,  0.54125  , -0.3239   ,
            0.093441 ,  0.17113  , -0.41533  ,  0.13702  , -0.21765  ,
           -0.65442  ,  0.75733  ,  0.359    ,  0.62492  ,  0.019685 ,
            0.21156  ,  0.28125  ,  0.22288  ,  0.026787 , -0.1019   ,
            0.11178  ,  0.17202  , -0.20403  , -0.01767  , -0.34351  ,
            0.11926  ,  0.73156  ,  0.11094  ,  0.12576  ,  0.64825  ,
           -0.80004  ,  0.62074  , -0.38557  ,  0.015614 ,  0.2664   ,
            0.18254  ,  0.11678  ,  0.58919  , -1.0639   , -0.29969  ,
            0.14827  , -0.42925  , -0.090766 ,  0.12313  , -0.024253 ,
           -0.21265  , -0.10331  ,  0.91988  , -1.4097   , -0.0542   ,
           -0.071201 ,  0.66878  , -0.24651  , -0.46788  , -0.23991  ,
           -0.14138  , -0.038911 , -0.48678  ,  0.22975  ,  0.36074  ,
            0.13024  , -0.40091  ,  0.19673  ,  0.016017 ,  0.30575  ,
           -2.1901   , -0.55468  ,  0.26955  ,  0.63815  ,  0.42724  ,
           -0.070186 , -0.11196  ,  0.14079  , -0.022228 ,  0.070456 ,
            0.17229  ,  0.099383 , -0.12258  , -0.23416  , -0.26525  ,
           -0.088991 , -0.061554 ,  0.26582  , -0.53112  , -0.4106   ,
            0.45211  , -0.39669  , -0.43746  , -0.6632   , -0.048135 ,
            0.23171  , -0.37665  , -0.38261  , -0.29286  , -0.036613 ,
            0.25354  ,  0.49775  ,  0.3359   , -0.11285  , -0.17228  ,
            0.85991  , -0.34081  ,  0.27959  ,  0.03698  ,  0.61782  ,
            0.23739  , -0.32049  , -0.073717 ,  0.015991 , -0.37395  ,
           -0.4152   ,  0.049221 , -0.3137   ,  0.091128 , -0.38258  ,
           -0.036783 ,  0.10902  , -0.38332  , -0.74754  ,  0.016473 ,
            0.55256  , -0.29053  , -0.50617  ,  0.83599  , -0.31783  ,
           -0.77465  , -0.0049272, -0.17103  , -0.38067  ,  0.44987  ,
           -0.12497  ,  0.60263  , -0.12026  ,  0.37368  , -0.079952 ,
           -0.15785  ,  0.37684  , -0.18679  ,  0.18855  , -0.4759   ,
           -0.11708  ,  0.36999  ,  0.54134  ,  0.42752  ,  0.038618 ,
            0.043483 ,  0.31435  , -0.24491  , -0.67818  , -0.33833  ,
            0.039218 , -0.11964  ,  0.8474   ,  0.09451  ,  0.070523 ,
           -0.2806   ,  0.296    , -0.17554  , -0.41087  ,  0.70748  ,
            0.17686  ,  0.043479 , -0.31902  ,  0.64584  , -0.45268  ,
           -0.7967   ,  0.099817 , -0.1734   ,  0.11404  , -0.36809  ,
            0.12035  , -0.048582 ,  0.55945  , -0.51508  ,  0.072704 ,
            0.18106  ,  0.07802  , -0.31526  ,  0.38189  ,  0.092801 ,
           -0.044227 , -0.66154  , -0.020428 ,  0.059836 , -0.23628  ,
           -0.017592 , -0.56481  , -0.52934  , -0.16392  ,  0.077331 ,
            0.24583  , -0.32195  , -0.36811  , -0.037208 ,  0.26702  ,
           -0.57907  ,  0.46457  , -0.54636  ,  0.11855  ,  0.092475 ,
           -0.10469  ,  0.03319  ,  0.62616  , -0.33684  ,  0.045742 ,
            0.25089  ,  0.28973  ,  0.060633 , -0.4096   ,  0.39198  ,
            0.58276  ,  0.496    , -0.75881  ,  0.13655  ,  0.21704  ,
           -0.37978  , -0.54051  , -0.22813  ,  0.28393  , -0.58739  ,
            1.0472   , -0.13318  , -0.07325  ,  0.12991  , -0.44999  ],
          dtype=float32)




```python
# can also be done using sklearn's linear kernel (equivilant to cosine similarity)

```

# Unigram, bigrams, trigrams

- Unigram = one word, eg the, and, of, hotel
- Bigrams = two consecutive words, eg the hotel, in seattle, the city
- Trigrams = three consecutive words, eg easy access to, high speed internet, the heart of

Credits: https://towardsdatascience.com/building-a-content-based-recommender-system-for-hotels-in-seattle-d724f0a32070

## Get all unigrams


```python
def get_top_n_words(corpus, n=None):
    vec = CountVectorizer(stop_words='english').fit(corpus)
    bag_of_words = vec.transform(corpus)
    sum_words = bag_of_words.sum(axis=0) 
    words_freq = [(word, sum_words[0, idx]) for word, idx in vec.vocabulary_.items()]
    words_freq =sorted(words_freq, key = lambda x: x[1], reverse=True)
    return words_freq[:n]
common_words = get_top_n_words(df['desc'], 20)
df2 = pd.DataFrame(common_words, columns = ['desc' , 'count'])
df2.groupby('desc').sum()['count'].sort_values().iplot(kind='barh', yTitle='Count', linecolor='black', title='Top 20 words in hotel description after removing stop words')

```

## Get all bigrams


```python
def get_top_n_bigram(corpus, n=None):
    vec = CountVectorizer(ngram_range=(2, 2), stop_words='english').fit(corpus)
    bag_of_words = vec.transform(corpus)
    sum_words = bag_of_words.sum(axis=0) 
    words_freq = [(word, sum_words[0, idx]) for word, idx in vec.vocabulary_.items()]
    words_freq =sorted(words_freq, key = lambda x: x[1], reverse=True)
    return words_freq[:n]
common_words = get_top_n_bigram(df['desc'], 20)
df4 = pd.DataFrame(common_words, columns = ['desc' , 'count'])
df4.groupby('desc').sum()['count'].sort_values(ascending=False).iplot(kind='bar', yTitle='Count', linecolor='black', title='Top 20 bigrams in hotel description After removing stop words')

```

## Get all trigrams


```python
def get_top_n_trigram(corpus, n=None):
    vec = CountVectorizer(ngram_range=(3, 3), stop_words='english').fit(corpus)
    bag_of_words = vec.transform(corpus)
    sum_words = bag_of_words.sum(axis=0) 
    words_freq = [(word, sum_words[0, idx]) for word, idx in vec.vocabulary_.items()]
    words_freq =sorted(words_freq, key = lambda x: x[1], reverse=True)
    return words_freq[:n]
common_words = get_top_n_trigram(df['desc'], 20)
df6 = pd.DataFrame(common_words, columns = ['desc' , 'count'])
df6.groupby('desc').sum()['count'].sort_values(ascending=False).iplot(kind='bar', yTitle='Count', linecolor='black', title='Top 20 trigrams in hotel description after removing stop words')

```

# Visualization


```python
from spacy import displacy
```


```python
doc = nlp("This is a sentence")
displacy.render(doc, style="dep")
```


<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:lang="en" id="0bf72b5ccfc143b4871b353f00ec3470-0" class="displacy" width="750" height="312.0" direction="ltr" style="max-width: none; height: 312.0px; color: #000000; background: #ffffff; font-family: Arial; direction: ltr">
<text class="displacy-token" fill="currentColor" text-anchor="middle" y="222.0">
    <tspan class="displacy-word" fill="currentColor" x="50">This</tspan>
    <tspan class="displacy-tag" dy="2em" fill="currentColor" x="50">DET</tspan>
</text>

<text class="displacy-token" fill="currentColor" text-anchor="middle" y="222.0">
    <tspan class="displacy-word" fill="currentColor" x="225">is</tspan>
    <tspan class="displacy-tag" dy="2em" fill="currentColor" x="225">VERB</tspan>
</text>

<text class="displacy-token" fill="currentColor" text-anchor="middle" y="222.0">
    <tspan class="displacy-word" fill="currentColor" x="400">a</tspan>
    <tspan class="displacy-tag" dy="2em" fill="currentColor" x="400">DET</tspan>
</text>

<text class="displacy-token" fill="currentColor" text-anchor="middle" y="222.0">
    <tspan class="displacy-word" fill="currentColor" x="575">sentence</tspan>
    <tspan class="displacy-tag" dy="2em" fill="currentColor" x="575">NOUN</tspan>
</text>

<g class="displacy-arrow">
    <path class="displacy-arc" id="arrow-0bf72b5ccfc143b4871b353f00ec3470-0-0" stroke-width="2px" d="M70,177.0 C70,89.5 220.0,89.5 220.0,177.0" fill="none" stroke="currentColor"/>
    <text dy="1.25em" style="font-size: 0.8em; letter-spacing: 1px">
        <textPath xlink:href="#arrow-0bf72b5ccfc143b4871b353f00ec3470-0-0" class="displacy-label" startOffset="50%" side="left" fill="currentColor" text-anchor="middle">nsubj</textPath>
    </text>
    <path class="displacy-arrowhead" d="M70,179.0 L62,167.0 78,167.0" fill="currentColor"/>
</g>

<g class="displacy-arrow">
    <path class="displacy-arc" id="arrow-0bf72b5ccfc143b4871b353f00ec3470-0-1" stroke-width="2px" d="M420,177.0 C420,89.5 570.0,89.5 570.0,177.0" fill="none" stroke="currentColor"/>
    <text dy="1.25em" style="font-size: 0.8em; letter-spacing: 1px">
        <textPath xlink:href="#arrow-0bf72b5ccfc143b4871b353f00ec3470-0-1" class="displacy-label" startOffset="50%" side="left" fill="currentColor" text-anchor="middle">det</textPath>
    </text>
    <path class="displacy-arrowhead" d="M420,179.0 L412,167.0 428,167.0" fill="currentColor"/>
</g>

<g class="displacy-arrow">
    <path class="displacy-arc" id="arrow-0bf72b5ccfc143b4871b353f00ec3470-0-2" stroke-width="2px" d="M245,177.0 C245,2.0 575.0,2.0 575.0,177.0" fill="none" stroke="currentColor"/>
    <text dy="1.25em" style="font-size: 0.8em; letter-spacing: 1px">
        <textPath xlink:href="#arrow-0bf72b5ccfc143b4871b353f00ec3470-0-2" class="displacy-label" startOffset="50%" side="left" fill="currentColor" text-anchor="middle">attr</textPath>
    </text>
    <path class="displacy-arrowhead" d="M575.0,179.0 L583.0,167.0 567.0,167.0" fill="currentColor"/>
</g>
</svg>



```python
doc = nlp("Larry Page founded Google in the US in early 1990.")
displacy.render(doc, style="ent")
```


<div class="entities" style="line-height: 2.5; direction: ltr">
<mark class="entity" style="background: #aa9cfc; padding: 0.45em 0.6em; margin: 0 0.25em; line-height: 1; border-radius: 0.35em; box-decoration-break: clone; -webkit-box-decoration-break: clone">
    Larry Page
    <span style="font-size: 0.8em; font-weight: bold; line-height: 1; border-radius: 0.35em; text-transform: uppercase; vertical-align: middle; margin-left: 0.5rem">PERSON</span>
</mark>
 founded 
<mark class="entity" style="background: #7aecec; padding: 0.45em 0.6em; margin: 0 0.25em; line-height: 1; border-radius: 0.35em; box-decoration-break: clone; -webkit-box-decoration-break: clone">
    Google
    <span style="font-size: 0.8em; font-weight: bold; line-height: 1; border-radius: 0.35em; text-transform: uppercase; vertical-align: middle; margin-left: 0.5rem">ORG</span>
</mark>
 in the 
<mark class="entity" style="background: #feca74; padding: 0.45em 0.6em; margin: 0 0.25em; line-height: 1; border-radius: 0.35em; box-decoration-break: clone; -webkit-box-decoration-break: clone">
    US
    <span style="font-size: 0.8em; font-weight: bold; line-height: 1; border-radius: 0.35em; text-transform: uppercase; vertical-align: middle; margin-left: 0.5rem">GPE</span>
</mark>
 in 
<mark class="entity" style="background: #bfe1d9; padding: 0.45em 0.6em; margin: 0 0.25em; line-height: 1; border-radius: 0.35em; box-decoration-break: clone; -webkit-box-decoration-break: clone">
    early 1990
    <span style="font-size: 0.8em; font-weight: bold; line-height: 1; border-radius: 0.35em; text-transform: uppercase; vertical-align: middle; margin-left: 0.5rem">DATE</span>
</mark>
.</div>


Inspired by: https://www.datacamp.com/community/blog/spacy-cheatsheet
