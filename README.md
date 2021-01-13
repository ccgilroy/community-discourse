# Community Discourse with Word Embeddings

Author: Connor Gilroy

This repository contains my experiments using word embeddings to analyze general English discourse about "community". 

These notebooks are prototypes I plan to develop into empirical dissertation research for my sociology PhD. You can borrow and adapt the code if it's helpful to you; please attribute.

The notebooks are rendered as a Jupyter Book [here](http://ccgilroy.github.io/community-discourse/).

## Setup

After you download this repository, follow these steps to run the notebooks. You'll need to install conda -- I use miniconda.

Create an environment `text-env` from the `environment.yml` file to install the relevant Python packages:

```
conda env create -f environment.yml
```

Activate that environment:

```
conda activate text-env
```

I believe the environment.yml file will install the pip packages, but if it doesn't then install them inside the conda environment:

```
pip install whatlies[all] jupyter-book linkify-it-py ghp-import
```

(whatlies is necessary for the running notebooks, but the other packages are only needed to render the Jupyter Book.)

Open jupyter (I use Jupyter Lab):

```
jupyter lab
```

Then you'll be able to open and run the notebooks from your web browser.

## Render Jupyter Book 

This renders the html files, then pushes them to the gh-pages branch of the GitHub repository.

```
jupyter-book build .
ghp-import -n -p -f _build/html
```

## Data

I use gensim to programmatically download pretrained GloVe vectors; this may take time the first time you do it. Historical word vectors need to be downloaded manually from https://nlp.stanford.edu/projects/histwords/, placed in a subdirectory (I used historical-embeddings/) and unzipped. 

The wikipedia Python package downloads individual wikipedia pages. It's only appropriate for downloading a handful of pages at a time -- if you need more data there are better and nicer ways to get it.

## Acknowledgements

This work wouldn't be possible without the papers and code it builds on. I've linked directly to many references in the notebooks, but I'm especially grateful to Dustin Stoltz and Marshall Taylor, Alina Arseniev-Koehler and Jacob Foster, Pedro Rodriguez and Arthur Spirling, Austin Kozlowski et al, and William Hamilton et al. Sharing research code isn't easy, but it's so helpful.

Neither would this be possible without high quality packages. gensim, by Radim Řehůřek (RaRe Technologies) and whatlies by Vincent D. Warmerdam, Thomas Kober, and Rachael Tatman (Rasa) were essential, as was the PyData stack (NumPy, Pandas, Seaborn, etc). Melanie Walsh's Intro to Cultural Analytics & Python inspired me to use Jupyter Book.

Kate Stovel, the UW Gender and Sexuality Graduate Research Cluster, and the CSDE Computational Demography Working Group all provided feedback on early versions of these ideas and experiments. Jeff Lockhart put up with my incessant Python-related questions.
