## Know Your Audience: Clarity & Reach in Scientific Communication
### Rachel Z. Insler
#### General Assembly Data Science Immersive Capstone Project

#### Presentation available [*here.*](http://bit.ly/dsi_capstone) 
---

## Executive Summary

> "Clear communication should always be a goal in science. It’s important to step back and always remind yourself as a scientist:
how do I describe what I’m doing to someone who is not doing this 24/7 like I am?” 
*-Dr. Sabine Stanley, planetary scientist at Johns Hopkins University*

This quote strongly resonated with me when I came across it in a [New York Times article](https://www.nytimes.com/2021/04/09/science/science-jargon-caves.html)  on the use of scientific jargon. I've been reflecting on how, as data scientists, **our ability to transform information into actionable insights can have a profound impact on the organizations we support**. But without the ability to then clearly and effectively communicate those insights to key stakeholders, our influence will be severely limited. 

Moreover, we must keep in mind that both "clear" and "effective" are in the eye of the beholder. That is to say: **know your audience.** Put yourself in their shoes. Throughout my data-driven career, I've had the privilege of interacting with and learning from some of the brighest minds in psychology, marketing, and data science, and they have all repeatedly emphasized this same point. 

Thus, I was surprised to read about a [recent exploration](https://royalsocietypublishing.org/doi/10.1098/rspb.2020.2581) into the literature surrounding cave science that found research papers containing lots of specialized terminology were less likely to be cited by other researchers. I'd expect that discipline-specific research journals would be an appropriate forum for the use of such terminology, yet the authors  concluded that a greater proportion of scientific jargon in a paper's abstract was associated with fewer citations. 

**In this project, I set out to determine whether or not this finding holds true for the highly technical field of machine learning.** 

**Phase I**

In the [first phase](https://github.com/rzi11211/dsi-capstone/tree/main/pubmed_papers), I attempted to reproduce the findings from the original Martinez & Mammola study. I used the natural language processing (NLP) techniques in [nltk](https://www.nltk.org/) along with the statistical and modeling tools in [scikit-learn](https://scikit-learn.org/stable/), [statsmodels](https://www.statsmodels.org/), and [scipy](https://www.scipy.org/) to identify and quantify the use of jargon in a [corpus of abstracts](https://github.com/rzi11211/dsi-capstone/blob/main/01_pubmed_papers/1_pubmed_get_abstracts.ipynb) from peer-reviewed scientific journals that reference "machine learning." I then asked the question: does using a greater proportion of [machine learning jargon](https://github.com/rzi11211/dsi-capstone/blob/main/01_pubmed_papers/0_get_jargon.ipynb) lead to fewer citations?

My [analyses](https://github.com/rzi11211/dsi-capstone/blob/main/01_pubmed_papers/5a_pubmed_jargon_modeling_reg.ipynb) found that neither jargon proportion, nor jargon frequency, nor specific jargon terms were found to be predictive of the number of times that a paper was cited. 

Failing (r = .03, p = .08) to replicate the primary jargon proportion finding, I moved on to a [second phase](https://github.com/rzi11211/dsi-capstone/tree/main/towards_data_science_posts) of the project, in which I attempted to address two potential limitations in my methods: 

1. insufficient data (I only had access to 3,151 abstracts; the original study used over 20K)
2. the abstracts I used spanned many disciplines, while the original study focused on one

**Phase II**

For phase two, I [collected a new dataset](https://github.com/rzi11211/dsi-capstone/blob/main/02_towards_data_science_posts/1_tds_get_towards_data_science_posts.ipynb) of over 9,000 posts on machine learning from Medium's *Towards Data Science* blog, and ran the same set of [analyses](https://github.com/rzi11211/dsi-capstone/blob/main/02_towards_data_science_posts/5a_tds_modeling_jargon_reg.ipynb), using Medium's [*'claps'*](https://medium.com/blogging-guide/how-do-claps-work-on-medium-b2897784ce6b#:~:text=Clapping%20is%20a%20way%20readers,you%20can%20earn%20per%20story) metric as a measure of reach (in lieu of citations). Once again, I was unable to reject the null hypothesis; neither jargon proportion, nor jargon frequency, nor specific jargon terms were found to be predictive of the number of claps received by a Towards Data Science post.   

Again, I identified two possible methodological limitations: 

1. perhaps the jargon list is not appropriate
2. perhaps 'claps' are not an ideal metric

The first could be addressed with the development of a custom jargon dictionary, collected through text mining and validated by industry experts. The second could be addressed by gaining access to more granular, less subective engagement metrics such as pageviews. 

Having failed to identify a statistically significant relationship between my list of jargon terms and the reach of a piece of scientific writing, I considered alternative approaches to get at the factors that **do** contribute to a well-received article with significant reach. Word frequency models reveal little in the way of inter- or intradocument statistical structure, so perhaps I needed to address the question at a less granular level; specifically, by using topics instead of individual words or phrases. 

**Phase III**

In [phase three](https://github.com/rzi11211/dsi-capstone/tree/main/03_topic_modeling) of the project, I applied the Latent Dirichlet Allocation modeling technique to identify the topics present in my corpus, then classify each document according to the dominant topic in its text. Using the [spacy](https://spacy.io/), [pyLDAvis](https://github.com/bmabey/pyLDAvis#:~:text=pyLDAvis%20is%20designed%20to%20help,an%20interactive%20web%2Dbased%20visualization.&text=Note%3A%20LDA%20stands%20for%20latent%20Dirichlet%20allocation.), and [Gensim](https://radimrehurek.com/gensim_3.8.3/) libraries (as well as the [Gensim wrapper](https://radimrehurek.com/gensim_3.8.3/models/wrappers/ldamallet.html) for [MALLET](http://mallet.cs.umass.edu/)), I created and compared a variety of topic models, then selected the best one for each corpus using: 

1. a quantitative metric: coherence
2. qualitative evaluation of topic keywords
3. qualitative visual evaluation of topic spread/overlap 

Once a robust topic model was created and applied for each corpus, I explored the relationship between these topics and the relevant target variable. I found signficant differences in means between certain topics, but subsequent regression analyses revealed that topic accounts for almost none of the variance in my target variable. (R2 score of 0.013 for 'claps' in the TDS corpus). This means that while posts like "The Ultimate Guide to Machine Learning Prediction Models with Data & Features*” posts may get more claps, on average, than "Using Cloud Service Tools to Process & Store Your Pipeline Data*” it's not the subject matter that's driving those differences; there's something else going on there. In the future, I'd like to revisit this analysis with 

1. a better metric than 'claps'
2. controls for blocking factors such as author popularity


In conclusion, my analyses determined that neither jargon proportion, nor jargon frequency, nor specific jargon terms, nor topic were found to be predictive of the number of times that a paper was cited, or the number of claps that a post receives on the Towards Data Science blog. I have identified several areas of future investigation to address possible methodological limitations, but at the risk of revealing my experimenter bias, I confess that I was pleased by my negative results. I believe that jargon has a time and place, and that no one machine learning topic is "better" for an author to write about than any ohther. What's most important for any writer, scientist, marketer, or human is to **know your audience.**

**Inspiration**

[Distill Research Journal](https://distill.pub/journal/)
[Up Goer Five](https://xkcd.com/1133/) and associated [challenge](https://splasho.com/upgoer5/). 


*These are fabricated post titles that I generated using as many of the topic keywords as I could. 

---


## Datasets

1. [3,141 PubMed Papers abstracts](https://github.com/rzi11211/dsi-capstone/tree/main/data/raw)
2. [9,804 Towards Data Science Posts](https://github.com/rzi11211/dsi-capstone/tree/main/data/raw_pubmed) 

### Data Collection

1. PubMed Papers abstracts
   - Query machine learning PubMed IDs using [pmidcite](https://github.com/dvklopfenstein/pmidcite) library and [NCBI API](https://www.ncbi.nlm.nih.gov/home/develop/api/)
     - “machine learning” in abstract or title
     - peer-reviewed, English-language journals
     - publication date range: 2010-2020
   - Pull corresponding abstracts, titles, publication dates, and citation counts using the [requests](https://docs.python-requests.org/en/master/) library and [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/)


2. Towards Data Science blog posts
   - Query posts from Towards Data Science blog
   - Pull corresponding date, title, subtitle, section titles, paragraph text, and number of claps from each post using the requests library and Beautiful Soup
---

### File Structure

```
dsi_capstone 
|__ 01_pubmed_papers
|   |__0_get_jargon.ipynb
|   |__1_pubmed_get_abstracts.ipynb
|   |__2_pubmed_cleaning.ipynb
|   |__3_pubmed_eda.ipynb
|   |__4_pubmed_preprocessing_nlp.ipynb
|   |__5_pubmed_create_jargon_vectors.ipynb
|   |__5a_pubmed_jargon_modeling_reg.ipynb
|   |__5b_pubmed_jargon_modeling_clf.ipynb
|   |__5c_pubmed_modeling_regression_numerical.ipynb
|   |__5d_pubmed_modeling_regression_nlp.ipynb
|__ 02_towards_data_science_posts
|   |__1_tds_get_towards_data_science_posts.ipynb
|   |__2_tds_cleaning.ipynb
|   |__3_tds_eda.ipynb
|   |__4_tds_preprocessing_nlp.ipynb
|   |__5_tds_create_jargon_vectors.ipynb
|   |__5a_tds_modeling_jargon_reg.ipynb
|   |__5b_tds_modeling_jargon_clf.ipynb
|   |__5b_tds_modeling_nlp_reg.ipynb
|   |__5c_tds_modeling_nlp_clf.ipynb
|   |__5d_tds_modeling_nlp_nn.ipynb
|__ 03_topic_modeling
|   |__pubmed_papers
|   |   |__1_pubmed_modeling_topic_gensim_LDA_bigrams.ipynb
|   |   |__2_pubmed_modeling_topic_gensim_LDA_trigrams.ipynb
|   |   |__stored_models
|   |   |   |__(various topic models saved here, along with dictionary)
|   |__towards_data_science_posts
|   |   |__1_tds_modeling_topic_gensim_LDA_bigrams.ipynb
|   |   |__2_tds_modeling_topic_gensim_LDA_trigrams.ipynb
|   |   |__stored_models
|   |   |   |__(various topic models saved here, along with dictionary)
|__ data
|   |__jargon.csv
|   |__list_of_pmids.csv
|   |__pubmed_cleaned_no_outliers.csv
|   |__pubmed_cleaned.csv
|   |__pubmed_nltk_nostem_preproc_strings.csv
|   |__pubmed_nltk_stemmed_preproc.csv
|   |__pubmed_vectorized_jargon.csv
|   |__raw (these are the Towards Data Science files)
|   |__raw_pubmed
|   |__tds_cleaned_no_outliers.csv
|   |__tds_cleaned.csv
|   |__tds_nltk_nostem_preproc_strings.csv
|   |__tds_nltk_stemmed_preproc.csv
|   |__tds_vectorized_jargon.csv
|   |__ten_hundred.csv
|__ figures
|   |__ (various figures stored here)
|__ presentation.pdf
|__ README.md
```
