![Python application](https://github.com/4OH4/doc-similarity/workflows/Python%20application/badge.svg)

# doc-similarity
https://github.com/4OH4/doc-similarity  

Find and rank relevant content in Python using NLP, TF-IDF and GloVe.

This repository includes two methods of ranking text content by similarity:
 1. Term Frequency - inverse document frequency (TF-idf)
 2. Semantic similarity, using GloVe word embeddings

Given a search query (text string) and a document corpus, these methods calculate a similarity metric for each document vs the query. Both methods exist as standalone modules, with explanation and demonstration code inside `examples.ipynb`.

There is an associated [blog post](https://towardsdatascience.com/how-to-rank-text-content-by-semantic-similarity-4d2419a84c32?source=friends_link&sk=a23730c6fad2744440eb8d4561088aa8) that explains the contents of this repository in more detail.

## Acknowledgements

The code in this repository utilises, is derived from and extends the excellent [Scikit-Learn](https://scikit-learn.org/), [Gensim](https://radimrehurek.com/gensim/) and [NLTK](https://www.nltk.org/) packages. 

## Setup and requirements

- anaconda: https://www.anaconda.com/products/individual#Downloads
- jupyter: https://jupyter.org/install.html
- pip install nltk~=3.4  

These should be all you need to download and install Anaconda (the launcher/navigator) and JupyterNotebook (the environment itself).  
for now I would recommend looking up: 'NumPy' and 'Pandas', as these are the two main tools used (lots of important math and plotting functions). It is fairly intuitive as it's all in Python, but definitely feel free to shoot me any further questions!

## Running the example notebook

~~After installing the requirements (if necessary), open and run `examples.ipynb` using Jupyter Lab.~~

Open and run `Policy Matching Tool.ipynb`

modify the code to use your input sitemap XML
make sure the home path is correct for your env
modify the query array of strings to your input query(ies)
output CSV filename of your choice

runSearch - top N
runAllSearch - scores all the entries in the sitemap

CSV output is 3 cols:

- query
- score
- URL

### Running on Google Colab

https://colab.research.google.com/notebooks/basic_features_overview.ipynb
https://colab.research.google.com/notebooks/snippets/importing_libraries.ipynb
https://towardsdatascience.com/getting-started-with-google-colab-f2fff97f594c

NOTE: to install py packages you need:

```
!pip3 install numpy~=1.18
!pip3 install scikit-learn~=0.22
!pip3 install gensim~=3.8
!pip3 install nltk~=3.4
!pip3 install regex
!pip3 install urllib3
!pip3 install pandas
!pip3 install bs4
!pip3 install tfidf
!pip3 install pathlib
!pip3 install matplotlib
```
You do NOT need to install jupyterlab since colab already has it (and it's incompatible with Google's)

### Running the notebook without a full jupyter browser environment

NOTE: if you get an error like:

```Resource stopwords not found.```

See: https://github.com/hotshot07/whatsapp_analyser/issues/2

I was able to solve this as noted there - running: 

```python3 -m nltk.downloader stopwords```

jupyter nbconvert --to python <notebook>.ipynb
 
this will produce a python file. if you aren't using ipython you can get rid of the get_ipython()... stuff and convert to simple py 
 
then run the python, eg:

```
 python ./Policy\ Matching\ Tool.py
```

it will ask you for a file name, enter something like test.json
 
then it produces the CSV output.
 
If you see:
 
HTTPError at url: https://docs.aws.amazon.com/...

That's just a warning - ignore.
 
### FROM HERE ON - Part of the original docsim tool - keeping here just in case for reference

Python 3 (v3.7 tested) and the following packages (all available via `pip`):

    pip install scikit-learn~=0.22  
    pip install gensim~=3.8  
    pip install nltk~=3.4  

Or install via the `requirements.txt` file:

    pip install -r requirements.txt

## Using the standalone TF-idf class

This module is a wrapper around the Scikit-Learn `TfidfVectorizer`, with some additional functionality from `nltk` to handle stopwords, lemmatization and cosine similarity calculation. To run:

    from tfidf import rank_documents
    
    document_scores = rank_documents(search_terms, documents)

## Using the standalone DocSim class

There is a self-contained class - DocSim - for running sematic similarity queries. This can be imported as a module and used without additional code:

    from docsim import DocSim
    
    docsim = DocSim(verbose=True)
    
    similarities = docsim.similarity_query(query_string, documents)

By default, a GloVe word embedding model is loaded (`glove-wiki-gigaword-50`), although a custom model can also be used.

The word embedding models can be quite large and slow to load, although subsequent operations are faster. The multi-threaded version of the class loads the model in the background, to avoid locking the main thread for a significant period of time. It is used in a similar way, although will raise an exception if the model is still loading so the status of the `model_ready` property should be checked first. The only difference is the import:

    from docsim import DocSim_threaded

## Running unit tests

To install the package requirements to run the unit tests:

    pip install -r requirements_unit_test.txt

To run all test cases, from the repository root:

    pytest

## Other

Comments and feedback welcome! Please raise an issue if you find any errors or omissions. 
