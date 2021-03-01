---
title: | 
    | Geography or Gemeinschaft? 
    | Disentangling the meaning of "community" through word embeddings
subtitle: "Community Data Science Collective March 2021 C+F Session"
author: "Connor Gilroy"
date: "February 28, 2021"
output: 
    pdf_document:
        latex_engine: xelatex
fontsize: 12pt
# header-includes:
#     - \usepackage{indentfirst}
bibliography: discourse.bib
csl: american-sociological-association.csl
linkcolor: blue
---

## Preamble

This draft will become the first empirical chapter of my dissertation in sociology. I hope for it to have an intrinsic, substantive point that can stand on its own, and for it to also serve as a potential measurement tool for subsequent chapters. I've started this chapter before my prospectus, but I have at least an intuition for what I'd like the overall shape of the dissertation to be. This chapter is really focused on analyzing culture and meaning through text on its own terms, and subsequent chapters might connect the cultural measurement of "community" to network measures (probably from some virtual community) and to spatial measures (an offline case will make my work more robust and generalizable). 

For this paper, I have a theoretical idea and a method I think works for it, and I'm aiming for the simplest substantively meaningful application possible. Since this is only one part of a dissertation, if you have suggestions for ambitious next steps that might fall outside the scope of a single paper, I also have the space to do those! I've been thinking about theories of community for a couple years^[For how I've been thinking about community, see https://ccgilroy.github.io/gilroy-reading-list/], embeddings-based methods for several months^[For a prototype of these methods, see https://ccgilroy.github.io/community-discourse/], and the specific case of Usenet for only a little over a month. Because of how this project has developed, I'm most settled on the theory, I'd hesitate to totally walk away from the method, and I'm least attached to the data I'm using. I especially welcome feedback to make sure I'm doing justice to virtual communities in general, and the case of Usenet groups in particular. Of course, I'm sure the theory can be sharpened, especially in how I explain it, and how I implement the method can be flexible in response to feedback as well.

I submitted an extended abstract for this paper to an ASA session on culture and computation, and plan to send the eventual paper either a general sociology journal (e.g. Social Forces) or a cultural sociology journal (e.g. Poetics).

\newpage

\setlength\parindent{0.5cm}
\setlength{\parskip}{0em}
\linespread{1.6}\selectfont

## Abstract

"Community" is an ambiguous concept with both sociological and everyday uses. Understanding what is essential and what is incidental to the meaning of the term opens up the ability to analyze how much people engage with or invoke the underlying meaning of community in different social groups or social contexts. Experiences of community, participation, and belonging are important both intrinsically, as one facet of individual experiences in social groups, and extrinsically as one potential motivation for social action. Using a computational approach to text analysis, I offer an empirical understanding of how "community" is used in popular English-language discourse. Through algebraic transformations of word embeddings, I disentangle spatial and sociological connotations of the word. I apply that understanding and those transformation to a set of virtual communities to demonstrate how they vary along each aspect of community. 

## Introduction and background

"Community" is complicated. Has it been "lost" or "liberated" [@wellman_community_1979], can it be "virtual" [@rheingold_virtual_2000] or even "imagined" [@anderson_imagined_2016]? In one view, community is a product of moral or cultural unity combined with social or interactional density [e.g. @tavory_summoned:_2016, drawing on Durkheim]. This way of thinking about community treats *Gemeinschaft* as the core element of community, and geographic proximity as incidental. As one line of evidence in favor of this view, extensive research has shown that virtual communities are real communities, in the sense that they really do instill a feeling of *Gemeinschaft* in their members [e.g, @rheingold_virtual_2000; @driskell_are_2002]. Of course, geography still structures much of social life; propinquity may enable community without being synonymous with it [@spiro_persistence_2016]. 

Despite this theoretical distinction, the word "community" in everyday use may still entail geographic as well as sociological or psychological senses. Disentangling or disambiguating these senses is a core challenge for computational work. The payoff is that we might then be able to observe in real settings when people create, invoke, or experience a deep sense of community. To be clear, I do not think that community is actually "radically despatialized," which is an idea urban ethnographers have critiqued [@kusenbach_hierarchy_2008]. Rather, I adopt despatialization as a method.

I use word embeddings to analyze the meaning of community. Embeddings models are an ideal method for this problem, as opposed to other text-as-data techniques like descriptive frequencies of word counts or topic models, because they encode meaning relationally. I use the similarities between "community" and other words in tandem with sociological definitions of community to determine what meanings are being brought together in the vector representation of the word. Preliminarily, I rely on pretrained GloVe embeddings, originally developed from a large corpus of Wikipedia and other online data [@pennington2014glove]. 

Groups and individuals vary in the extent to which they experience a sense of community, and in the extent to which they communicate that sense of community through their language. I demonstrate this variation by adapting Concept Mover's Distance [@stoltz_concept_2019] and applying it to posts from 20 Usenet newsgroups from the 1990s. These virtual communities were a precursor to present-day online and social media communities. Different Usenet groups have different cultures, and I show that average engagement with the concept of community differs between groups based on their topical focus. My initial findings are in line with my prior expectations in some cases, and diverge in others.

These analyses inform each other. The more theoretical analysis of the general discursive meaning of community is needed in order to interpret how people in different groups invoke that underlying meaning. The more empirical application to real communities not only shows the utility of the theory and method, but can allow me to refine it in an iterative process. In particular, I use the theoretical dimensions I develop to remove the geographic aspect of community in my empirical analysis.

This work makes two contributions. Substantively, it offers a new way of studying experiences of community across different groups, with potential applications in offline as well as online contexts. Methodologically, it combines prior sociological theory and text data to bring empirical clarity to a complex abstraction, with potential relevance for studies of other sociological concepts. I contribute to a growing literature adapting embeddings for sociological ends by extending the method to a concept that is rather less concrete and clear-cut. For instance, "community" is not quite like binary concepts such as social class [@kozlowski_geometry_2019], health or morality [@arseniev-koehler_machine_2020-1], or conservative or liberal politics [@taylor_integrating_2020]. Community has no one clear antonym. While one might conceptually oppose community to the individual, one could just as easily oppose community to society writ large. Disentangling the meaning of community with word embeddings requires making these sorts of theoretically-informed analytic choices. 

"Community" is both perceptual and expressed, which is why a text-based measure of community might complement survey and interview measures. Community psychologists devise elaborate multi-part survey scales to measure sense of community [e.g. @boessen_networks_2014]. Qualitative sociologists occasionally find challenges in getting people to talk about community explicitly in interviews [@winer_solidarity_2020]; respondents invoke "imagined" community rather than their personal experiences.

Discursive analysis might also shed light on how social scientists use the term "community." Some sociologists with theoretical interests in how groups form out of networks of social relations, such as Peter Blau and Harrison White, use the term "community" in a purely geographic sense, and adopt other words to refer to a sense of groupness or belonging. White uses "corporateness," for instance, which hasn't exactly caught on. But plenty follow the original English translation of @tonnies_community_2001 and stick with "community" to invoke *Gemeinschaft.*[^2001][^german]

[^2001]: The 2001 re-translation of *Gemeinschaft und Gesellschaft* quibbles with Gesellschaft but leaves Gemeinschaft alone.

[^german]: Benedict @anderson_imagined_2016 argues that there's something secretly Germanic in the English word "community" despite its Romance roots; this might explain why Durkheim's treatment of similar collective social experiences (in French) invokes "solidarity" instead [@aldous_exchange_1972]. If I develop a related project to examine academic usage of "community," I'd like it to be cross-linguistic.

## Data

I use two kinds of data. First, pretrained embeddings as an object of analysis themselves. Second, textual posts from different virtual communities.

The pretrained GloVe embeddings [@pennington2014glove] I use were originally trained on a full English Wikipedia corpus from 2014 and a newswire corpus called Gigaword 5. A social scientist might prefer a more logically bounded population of text for the training corpus, but the more-is-better logic of training data won out. Generally, however, prior social science researchers have found pretrained embeddings to be reasonably robust, stable, and generalizable [@stoltz_cultural_2020, @rodriguez_word_2020], and I find similarly in supplemental analyses. The preliminary consensus is that these pretrained models are good enough for typical social science uses. @kozlowski_geometry_2019, who use historical embeddings, suggest thinking of the associations encoded in these embeddings as coming from a "literary public" with known and unknown biases compared to the general population. 

My applied corpus is the 20 Newsgroups Usenet data [@Lang95]. Usenet is a distributed system for sharing electronic messages which predates the contemporary Internet, organized into topical groups such as alt.atheism or rec.motorcycles. Some of these groups are reported to have had a strong sense of community, while others were known for their hostility [@baym_practice_1994; @dame-griff_herding_2019]. This expected variation makes Usenet a compelling data source for analyzing how community-oriented different groups might be.

The 20 Newsgroups data set was compiled in 1995 and consists of nearly 20,000 messages approximately evenly distributed across those 20 groups [@Lang95]. It is a purposive sample of groups collected to represent diverse topical categories, originally intended for machine learning classification research [e.g. @dai_semi-supervised_2015] and also used as a teaching tool and test data set for topic modeling [e.g. @silge_text_2017, @sia_tired_2020]. These data are both convenient to obtain (through scikit-learn) and relevant, and so I repurpose them here for a more sociologically-oriented analysis. Rather than as a classification outcome, I will use the group labels to examine between-group variation in engagement with "community."

## Methods

I break down my method into two major parts and seven individual steps.

The first part is a discursive analysis at the level of words and their representations in a set of embeddings: 

1. I select a focal word of theoretical and substantive interest, in this case "community." To use this method for other social-science concepts, I suspect there needs to be some overlap between the specialized academic use of the word and everyday uses (or at least the uses that might be expected in some training corpus).
2. I decompose the local neighborhood, measured using cosine similarity, of words similar to the focal word (N = 1000) through principal components analysis (PCA). 
3. I inspect the resulting PCA dimensions for the proportion of local variation they explain and for any potential substantive interpretation. Here, even though the embeddings in the neighborhood of "community" do not fall into discrete clusters, I cluster them with K-means to aid in interpretation.
4. I average the vectors for extreme words (N = 10) along a PCA axis of substantive interest to "debias" the focal word vector through orthogonal projection. 

The second part is an applied analysis the level of documents in a specific corpus:

5. I apply Concept Mover's Distance (CMD) to texts of interest to measure their relation to both the original and the transformed focal word vectors. Concept Mover's Distance [@stoltz_concept_2019] is a sociological adaptation of Word Mover's Distance [@kusner_word_2015], which aggregates all of the word-level embeddings in a document and compares them to another.[^five] The motivation for CMD is that people can use different exact words to express similar underlying meanings.
6. I analyze trends and variation in the result quantitatively, to see how the CMD results for each vector correlate and what metadata predict them. I use newsgroup labels to predict CMD values.
7. I inspect some subset of the texts through qualitative close reading to validate and criticize the computational results.[^seven] 

[^five]: Because I use the Python implementation of Word Mover's Distance in the gensim package, there are minor differences in the distance metric and algorithm I use compared to Stoltz and Taylor; I also do not standardize or invert the values I report. I expect my results in Part 2 to be robust to such minor variations. 

[^seven]: I believe this last step is really important, but I haven't done it yet.

The main methodological innovation is the use of orthogonal projection rather than differencing to disentangle aspects of the focal word. I borrow this idea from NLP papers aimed at "debiasing" word embeddings in terms of, for instance, binary gender [@gonen_lipstick_2019]. As far as I'm aware, this is new for social-science applications, which have mainly constructed binary dimensions through subtraction instead. The reason I do things differently is theoretical and substantive -- even if a PCA dimension shows two kinds of words being in opposition to each other, there's no reason that they have to be opposed at the level of a text, which might be close to or far from both. Projection allows them to be independent or correlated. For comparison, I also show what happens when I construct various binary dimensions by taking the differences of two vectors. (Ultimately, the results will be fairly similar, even though the conceptualization and the math for each approach is different.)

This is not a completely automated method. In particular, the third and seventh steps necessarily involve human interpretation and evaluation. As the analyst, I decide which PCA axes are substantively relevant, and which encode less sociologically-relevant linguistic features. I'm still figuring out how to assess whether the application to Usenet is a satisfying analysis, and what would tell me that I need to iterate further.

Finally, there are opportunities for refining and checking the sensitivity of the analysis at every step: varying arbitrary parameters like the neighborhood size, filtering the vocabulary, or even swapping out the pretrained embedding model. I expect results to be stable within reasonable limits, and drastic changes ought to have predictable consequences.

## Results and interpretation

### Part 1: Discursive analysis

The goal of the discursive analysis is to understand how 'community' is represented through word embeddings, which are a relational, computational model of word meanings. The key measurement is similarity, and the conventional metric is cosine similarity. The underlying GloVe model was pretrained on a combination of Wikipedia and newswire data [@pennington2014glove]. 

Figure 1 plots the thousand words most similar to "community" in two dimensions. The first PCA dimension explains 6.6% of the variation, and the second dimension explains 5.4%. Consistent with what others have found [@kozlowski_geometry_2019], the tail is long; the first 20 dimensions explain only 48% of the total variation in the vectors. (With a narrower neighborhood of words, e.g. N = 100, fewer dimensions encode more of the local variation.)[^vocabulary]

[^vocabulary]: I initially subset the 400,000-word GloVe vector vocabulary to 130,000 words by intersecting it with another set of GloVe vectors based on Twitter data, which excludes extremely rare words, proper names, misspellings, and non-English words, though not entirely. In the final analysis, I might subset to match the Usenet corpus vocabulary instead. 

The first PCA dimension is linguistic. This is the x-axis in Figure 1. It encodes a distinction between common, functional words and words that are more complex and substantive. The dimension ranges from words like "if" and "we" and "not" to works like "not-for-profit", "community-based", "lgbt," and "interfaith." While this distinction certainly matters for the overall space of meaning in the English language, it is not especially salient for this analysis, so I leave it aside here.[^stopwords]

[^stopwords]: Filtering out a standard list of English stopwords is another way I might subset the vocabulary, and I would expect this to reduce the variation explained by the first PCA dimension.

The second PCA dimension is more sociological. This is the y-axis in Figure 1. The substantive distinction it encodes is between words with spatial or geographic meanings, like "town" or "located," and words with more social or cultural senses, like "cooperation," "governance," "organizations," and "collective." Following the ideas I laid out above, I refer to the latter as *Gemeinschaft* words. The more functional words, the ones far to the left on the first axis, do not score highly in either direction on the second axis. "Geography" and "Gemeinschaft" are are not clearly separable categories, but rather a continuum. The word "community" in fact falls nearly in the middle, which is a sign that it has both geographic and Gemeinschaft-like resonances. Because this second dimension is more substantively relevant than the first, I use it as the basis for subsequent steps of the analysis.[^dim3]

[^dim3]: I briefly explored the next few PCA dimensions. The variation they encode seems to be substantive, but absent theory I do not want to overinterpret them. Dimension 3, for instance, explains 3.8% of the overall variance and ranges from words like "research" and "science" to words like "ethnic" and "christians." The geography-Gemeinschaft dimension does also appear in the GloVe embeddings trained on Twitter data, which is another line of evidence suggesting that this particular distinction is robust.

![The nearest neighbors to "community." The word vectors are clustered with K-means to make the three broad categories of words more apparent.](../img/community_pca1000_kmeans3.png)

The next step is to draw on the words at each end of the Gemeinschaft-geography PCA axis. Figure 2 shows the 10 most extreme words along either end of the dimension, alongside the word 'community' itself. Extreme Gemeinschaft words include "cooperation," "promote," and "implement;" extreme geography words include "located," "town," and "district." The figure shows that cosine similarities are high within each set of words and low between them. The word "community" is, by construction, highly similar to both sets of words. (The contrast is apparent with wider windows, like 50 or even 100 extreme words. Eventually, of course, the sharp distinction fades and becomes a gradient.)

![Extreme words along the Gemeinschaft-geography dimension. These words are similar within each group, and distinct from the other.](../img/gemeinschaft_geography_words.png)

I use these two sets of words to "debias" community, removing or at least reducing the association it has with geography or with Gemeinschaft respectively. I average the vectors for these two sets of 10 words to create overall "geography" and "Gemeinschaft" vectors. Using each of those vectors, I transform the original vector for "community" into modified vectors, as shown in Figures 3 and 4. For comparison, I illustrate two distinct algebraic options: orthogonal projection and subtraction. Projecting "community" to be orthogonal to the geography vector produces a new vector for "community" at 90 degrees from it, with a cosine similarity of zero (Figure 3). Taking the difference between them instead creates a vector that points slightly away from the geography vector, with a small negative cosine similarity. For completeness and symmetry, Figure 4 shows the same approaches applied to community and Gemeinschaft. Substantively, I focus on despatializing community, arguing that the derived vectors in Figure 3 can be thought of as community-without-geography.

![Constructing a "community" vector without geography. The axes are cosine similarities to the orthogonal projection of community and to the average of the geography words.](../img/despatializing_community.png)

![Constructing the equivalent "community" vector without Gemeinschaft.](../img/decommunalizing_community.png)

Finally, I examine the cosine similarities between each of these vectors---the original representation of "community,", the averages for geography and Gemeinschaft, and all of the derived vectors---to assess how they relate to each other and which might be most useful for applied analysis. Figure 5 shows these similarities. The orthogonal vectors (labeled "'Community' without geography" and "'Community' without Gemeinschaft" in the figure) are extremely similar to the binary axes produced through vector subtraction. But they do not have the same relation to the original "community" vector; the orthogonal vectors are much closer to it than the binary oppositions are. This is a tradeoff, because the two binary dimensions are also more distinct from each other, and from the opposing averaged vectors. Yet, for instance, community-without-geography is also slightly more similar to the averaged Gemeinschaft words than the community-geography binary is. I believe it is better to retain more of the original meaning of "community," and I prefer the orthogonal despatialized and decommunalized vectors in the second part of this analysis. 

The final row in Figure 5 is the difference between the average of the ten Gemeinschaft words and the average of the ten geography words. Gemeinschaft is the positive direction, which means that the negative similarities between this binary vector and anything geographic are expected. What is concerning, however, is the lack of similarity with 'community' itself. The Gemeinschaft-geography binary is nearly orthogonal to "community." This fact means that this binary dimension alone is probably inadequate for an analysis of how particular texts engage with community. Figure 6 emphasizes this finding, drawing all of the vectors from Figure 5 based on how similar they are to the Gemeinschaft-geography binary (x-axis) and to the original "community" vector (y-axis).

![Comparison of the vectors derived from "community" and related words.](../img/derived_vectors_similarity.png)

![Comparison of derived vectors along Gemeinschaft-geography binary dimension](../img/derived_vectors_binary_comparison.png)

So, what is community? "Community" brings together both geography and Gemeinschaft. It has the spatial connotations of a local area, as well as sociological associations with social organization and cultural unity. With vector algebra on word embeddings, we can tease those two aspects of community apart.

### Part 2: Applied analysis

I take the vectors derived above and apply them to the 20 Newsgroups corpus. To parse the documents, I rely for now on scikit-learn's built-in parser for removing headers, footers, and quotes. I lowercase tokens and remove English stopwords. As previously described, I use Word Mover's Distance or Concept Mover's Distance [@kusner_word_2015, @stoltz_concept_2019] as a way to aggregate the word embeddings for every word in a given Usenet post and compare them against a target embedding. Because this is a distance measure, smaller values are "closer" to the target vector. To interpret what it means for a text to be close to or far from "community" or one of its derived representations, I rely on the analysis from Part 1. Table 1 presents descriptive summary statistics for all 18,296 posts across the 20 Usenet groups.

\linespread{1}\selectfont

: Descriptive statistics across all posts for each CMD value (N = 18,296).

|                                  |   Mean |    SD |
|:---------------------------------|-------:|------:|
| Distance from 'community'        |  1.227 | 0.046 |
| Distance from                    |  1.271 | 0.038 |
| geography words average          |        |       |
| Distance from                    |  1.293 | 0.036 |
| 'community' without geography    |        |       |
| Distance from 'community' pole   |  1.343 | 0.029 |
| of community-geography binary    |        |       |
| Distance from                    |  1.227 | 0.051 |
| Gemeinschaft words average       |        |       |
| Distance from                    |  1.322 | 0.027 |
| 'community' without Gemeinschaft |        |       |
| Distance from 'community' pole   |  1.355 | 0.023 |
| of community-Gemeinschaft binary |        |       |
| Distance from Gemeinschaft pole  |  1.401 | 0.027 |
| of Gemeinschaft-geography binary |        |       |

\linespread{1.6}\selectfont

I find that, when measured on the Usenet data, most of these distance measures are even more highly correlated than the original vectors are similar. Figure 7 shows these correlations. Once again, the low correlation means that the Gemeinschaft-geography binary on its own is not a good measure of community. The benefit of orthogonal projection, or even of constructing a binary using the community vector, is that it allows geographic and Gemeinschaft associations to be independent or correlated at the level of a full text, rather than inherently opposed. And, in fact, community-without-geography and community-without-Gemeinschaft have a correlation of 0.62. Even vectors which have a cosine similarity of zero have positive correlations.

![Correlations of all Concept Mover's Distance measures between 20 Newsgroups posts and each of the derived vectors from Part 1.](../img/usenet_cmd_correlations.png)

As I noted during the discursive analysis, I find netting out the geographic aspect of 'community' to be the most interesting. This is especially true in the context of virtual communities, but I compare it to the corresponding community-without-Gemeinschaft measure for symmetry and completeness. Figure 8 shows the average CMD values for each newsgroup compared to these two vectors. In Figure 9, I fit simple linear models predicting undifferentiated "community" (R^2^ = 0.13), "community" without geography (R^2^ = 0.19), and "community" without Gemeinschaft (R^2^ = 0.15). 

![Average CMD values by newsgroup for community without geography and community without Gemeinschaft.](../img/cmd_by_newsgroup.png)

![Average predicted CMD values for each of the 20 Usenet groups, relative to three variations on "community."](../img/usenet_cmd_model_comparison.png)

What this means is that a substantial amount of the variation, though far from all of it, is variation between groups. I think that's pretty neat, and I hope that, when I look at the posts driving those differences, they don't turn out to be a mirage. The precise rankings of groups change across the different outcome measures, but I'm not yet confident enough to offer much interpretation. Intuitively, it makes sense to me that religion-focused groups might have a high sense of community (low CMD), and misc.forsale might lack one. The political, sports, computer, and science-related groups, which are all intermediate, are more difficult for me to interpret. 

## Discussion and loose ends

Here are a few informal observations and outstanding concerns I have.

The lack of metadata aside from group labels is tricky. Fundamentally, I don't know much about the norms of these particular Usenet groups in the early-mid 1990s. It would be lovely if each one had an insider ethnography like @baym_practice_1994 for rec.art.tv.soaps, or a historical archival analysis like @dame-griff_herding_2019 for transgender Usenet groups. Maybe I'm not looking in the right places, but it would be great to know more about the social context for the production of a corpus that's been widely published with in CS / ML / NLP papers.

Conceptually, I prefer orthogonal projection to subtraction. But the two vectors are very similar, so the applied payoff of the former isn't huge. I still think broadening the options available to social scientists working with embeddings is useful. Based on my results, a measurement tool like the Gemeinschaft-geography binary that sidesteps the word "community" itself altogether doesn't seem right to me. I think that would have been the most obvious adaptation of the antonym-based approach developed in papers like @kozlowski_geometry_2019, so I find it noteworthy that it did not work out. 

I think it would make sense to train embeddings locally on the 20 Newsgroups data, as part of the final validation and criticism of the results. I might expect "community" to have less of an inherent geographic resonance when the embedding for it comes from a virtual community. 

\newpage

## References
