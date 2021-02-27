---
title: | 
    | Geography or Gemeinschaft? 
    | Disentangling the meaning of "community" through word embeddings
subtitle: |
    | Extended abstract for the annual meeting 
    | of the American Sociological Association
author: "Connor Gilroy"
date: "February 3, 2021"
output: 
    pdf_document:
        latex_engine: xelatex
fontsize: 12pt
header-includes:
    - \usepackage{indentfirst}
bibliography: discourse.bib
csl: american-sociological-association.csl
---

\setlength\parindent{0.5cm}
\setlength{\parskip}{0em}
\linespread{1.6}\selectfont

## Introduction

Community is an ambiguous concept with both sociological and everyday uses. Understanding what is essential and what is incidental to the meaning of the term opens up the ability to analyze how much people engage with or invoke the underlying meaning of community in different social groups or social contexts. Experiences of community, participation, and belonging are important both intrinsically, as one facet of individual experiences in social groups, and extrinsically as one potential motivation for social action. Using a computational approach to text analysis, I offer an empirical understanding of how "community" is used in popular English-language discourse. I apply that understanding to a set of virtual communities to demonstrate how they vary. 

In one view, community is a product of moral or cultural unity combined with social or interactional density [e.g. @tavory_summoned:_2016, drawing on Durkheim]. This way of thinking about community treats *Gemeinschaft* as the core element of community, and geographic proximity as incidental. As one line of evidence in favor of this view, extensive research has shown that virtual communities are real communities, in the sense that they really do instill a feeling of *Gemeinschaft* in their members [e.g, @rheingold_virtual_2000; @driskell_are_2002]. Of course, geography still structures much of social life; propinquity may enable community without being synonymous with it [@spiro_persistence_2016]. Despite this theoretical distinction, the word "community" in everyday use may still entail geographic as well as sociological or psychological senses. Disentangling or disambiguating these senses is a core challenge for computational work. The payoff is that we might then be able to observe in real settings when people create, invoke, or experience a deep sense of community.

I use word embeddings to analyze the meaning of community. Embeddings models are an ideal method for this problem, as opposed to other text-as-data techniques like descriptive frequencies of word counts or topic models, because they encode meaning relationally. I use the similarities between "community" and other words in tandem with sociological definitions of community to determine what meanings are being brought together in the vector representation of the word. Preliminarily, I rely on pretrained GloVe embeddings, originally developed from a large corpus of Wikipedia and other online data [@pennington2014glove]. 

Groups and individuals vary in the extent to which they experience a sense of community, and in the extent to which they communicate that sense of community through their language. I demonstrate this variation by adapting Concept Mover's Distance [@stoltz_concept_2019] and applying it to posts from 20 Usenet newsgroups from the 1990s. These virtual communities were a precursor to present-day online and social media communities. Different Usenet groups have different cultures, and I show that average engagement with the concept of community differs between groups based on their topical focus. My initial findings are in line with my prior expectations in some cases, and diverge in others.

These analyses inform each other. The more theoretical analysis of the general discursive meaning of community is needed in order to interpret how people in different groups invoke that underlying meaning. The more empirical application to real communities not only shows the utility of the theory and method, but can allow me to refine it in an iterative process. In particular, I plan to use the theoretical dimensions I develop to difference out the geographic aspect of community in my empirical analysis.

This work makes two contributions. Substantively, it offers a new way of studying experiences of community across different groups, with potential applications in offline as well as online contexts. Methodologically, it combines prior sociological theory and text data to bring empirical clarity to a complex abstraction, with potential relevance for studies of other sociological concepts. I contribute to a growing literature adapting embeddings for sociological ends by extending the method to a concept that is rather less concrete and clear-cut. For instance, "community" is not quite like binary concepts such as social class [@kozlowski_geometry_2019], health or morality [@arseniev-koehler_machine_2020-1], or conservative or liberal politics [@taylor_integrating_2020]. Community has no one clear antonym. While one might conceptually oppose community to the individual, one could just as easily oppose community to society writ large. Disentangling the meaning of community with word embeddings requires making these sorts of theoretically-informed analytic choices. 

## Data and methods

Word embeddings are dense vector representations of words based on their contexts. These models were developed by natural language processing (NLP) researchers [@pennington2014glove, @mikolov_efficient_2013], and have been imported into the social sciences, especially cultural sociology and political science (e.g. Kozlowski). I use pretrained GloVe embeddings, rather than training models locally on the Usenet data set. Generally, prior social science researchers have found pretrained embeddings to be reasonably robust, stable, and generalizable [@stoltz_cultural_2020, @rodriguez_word_2020], and I find similarly in supplemental analyses.

To measure engagement with community in at the level of individual Usenet posts, I use Concept Mover's Distance [@stoltz_concept_2019]. Concept Mover's Distance is a sociological adaptation of Word Mover's Distance [@kusner_word_2015], which aggregates all of the word-level embeddings in a document and compares them to another. Because I use the Python implementation of Word Mover's Distance in the gensim package, there are minor differences in the distance metric and algorithm; I expect the results reported below to be robust to such minor variations. I also do not standardize or invert the values I report.

Usenet is a distributed system for sharing electronic messages which predates the contemporary Internet, organized into topical groups such as alt.atheism or rec.motorcycles. Some of these groups are reported to have had a strong sense of community, while others were known for their hostility [@baym_practice_1994; @dame-griff_herding_2019]. This expected variation makes Usenet a compelling data source for analyzing how community-oriented different groups might be.

The 20 Newsgroups data set was compiled in 1995 and consists of nearly 20,000 messages approximately evenly distributed across those 20 groups [@Lang95]. It is a purposive sample of groups collected to represent diverse topical categories, originally intended for machine learning classification research [e.g. @dai_semi-supervised_2015] and also used as a teaching tool for topic modeling [e.g. @silge_text_2017]. These data are both convenient to obtain (through scikit-learn) and relevant, and so I repurpose them here for a more sociologically-oriented analysis.

## Results

I analyze what, exactly, about the meaning of community is encoded in an embedding model by examining how similar words are to each other, according to the cosine similarity of their vectors. Figure 1 shows this schematically with a small set of words I selected. The axes of the figure are "similarity to 'community'" and "similarity to 'individual.'" "Neighborhood," for instance, is far more similar to "community" than to "individual."

More systematically, an initial qualitative analysis examining the nearest neighboring words to community (Figure 2) reveals both words related to geography (e.g. "local", "area", "residents") and words related to *Gemeinschaft* (e.g. "organization", "support"). PCA of a larger set of neighboring words (N = 100) reveals similar trends, and formal clustering or dimension-creation is a logical next step.

In additional analyses, I show that the meaning of community is stable across corpora and over time. I follow Rodriguez and Stirling and confirm that the meaning of community has a moderately high correlation across embedding models pretrained on two independent data sources, Wikipedia and Twitter (Pearson correlation between cosine similarities = 0.636). I also confirm that the meaning of community is moderately stable over the course of the 20th century, using historical word embeddings pretrained with Google n-grams [@hamilton_diachronic_2016]. These results increase my confidence that these pretrained embedding models encode a core definition of community and can be fruitfully applied to the Usenet data.^[These supplementary analyses can be viewed at https://ccgilroy.github.io/community-discourse/]

Turning to those data, I apply Concept Mover's Distance (CMD) to each of the posts from the 20 Usenet groups included in the data set (N = 18,296 posts in total). For now, I simply measure the distance of each post from the undifferentiated concept "community," though I plan to difference out the geographic dimension of community in subsequent refinements of the analysis. 

The full distribution of CMD values in Figure 3 shows substantial overlap between Usenet groups, as well as substantial variation within groups. This is unsurprising, because each of these groups is a virtual community of some sort, and individual posts might be expected to vary in their tone and content substantially, just as individual experiences might vary.

At the same time, the different Usenet groups do in fact differ substantially and significantly in the average closeness of their posts to the concept of "community." Figure 4 shows the predicted mean CMD for each group (R^2^ = 0.133, F = 147.17, p = 0.0). This simple statistical test shows that a small but substantial proportion of the variation in CMD is variation between different Usenet groups, rather than variation within groups. In some cases, this variation is in line with what we might expect topically: religion groups are more community-like, the forsale group is the least. In other cases, such as politics or sports, it may be that the specific norms and tone of the communities serve to generate a sense of community, regardless of how contentious or communal the topic might be.

![2-dimensional projection of word similarities](../img/community_projection2.png){width=75%}

![Most similar words to "community", N = 20](../img/community_top20.png){width=75%}

![Full distribution of CMD values for 20 Newsgroups](../img/usenet_cmd_full.png){width=75%}

![Usenet groups differ in their average sense of community](../img/usenet_cmd_predicted.png){width=75%}

\newpage

## References

\setlength\parindent{-0.5cm}
\setlength\leftskip{0.5cm}
\noindent
