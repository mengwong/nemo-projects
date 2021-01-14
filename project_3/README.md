# Scraping and Classifying Subreddit Posts, by Yap Jun Hong (Nemo)

## Summary of the project

Classifying text is a staple tool in Natural Language Processing (NLP). This project aims to explore text classification of sub-reddits by classifying posts within 2 subreddits. As this data is unstructured and only available on the web, this project also uses web scraping tools such as BeautifulSoup to first obtain the data.

This project is a good foundation for further applications, such as setting up a notification whenever a new post is entered into a subreddit. This notification will alert businesses about relevant posts that they may wish to reply to.

## Section 1: Problem Statement

This project aims to build several models and find the best one that will classify text posts into one of two subreddits. This is therefore a binary classification task. 

The two subreddits chosen are [r/solotravel](https://www.reddit.com/r/solotravel/) and [r/JapanTravel](https://www.reddit.com/r/JapanTravel/). An explanation of reddit is given in section 1.1 below.

### 1.1: What is reddit and why does classifying posts in them matter?

Reddit is a collection of forums, called subreddits, where people gather and discuss relevant topics, ask questions, and post memes. Taking posts from 2 subreddits and classifying them into either forum matters as part of a larger goal of business intelligence. 

Businesses might keep track of posts in subreddits to keep track of customer sentiment or customer complaints. Good examples of this can be found in 'gaming subreddits', where a subreddit is formed for a game like [r/Cyberpunkgame](https://www.reddit.com/r/cyberpunkgame/). There, people post videos of bugs they've found, complaints they have, show appreciation, and so on.

However, keeping track of a subreddit daily is a potential timewaster. Trawling through subreddits daily to keep track of customer sentiment is time that could be better used for other work tasks. This can be achieved if an alarm could be set up to alert businesses to new, relevant posts that they would like to explore.

A classification model is a first step to this end goal. Businesses can build on this classification model by programming it to also classify new posts into either subreddit. They can then set up a notification to alert them to posts that they would like to see.

### 1.2: Business context

In this project, I am a marketer who's sick of wasting time keeping track of subreddits, inevitably finding myself wasting time as I trawl through more than I have to. Luckily for me, I am also a data scientist trained in web scraping and text classification and have decided to take the first steps to freeing my time for other work.

### 1.3: Models used

2 models are used in this classification task. The first is a Naive Bayes model, while the second is a Logistic Regression model that has been regularised with ElasticNet. Various tweaks were tried, such as removing stop words and comparing CountVectorizer and TfidfVectorizer. See Section 4 for more details on the final production model.

### 1.4: Measuring success

Success will be measured using Accuracy, Recall, Precision, and a Receiver of Characteristic (ROC) curve.

## Section 2: Notebooks in this Project

1. [Scraping from JapanTravel and solotravel subreddits](code/01_web_scraping.ipynb)
2. [Exploratory Data Analysis](code/02_exploratory_data_analysis.ipynb)
3. [Classification and Modelling](code/03_classifying_and_modelling.ipynb)
4. [Saved Production Model](code/04_production_model_loader.ipynb)

## Section 3: Data Dictionary

There is one dataframe called 'combined_df' which is a concatenation of both the solotravel and JapanTravel dataframes. The below data dictionary is for that combined dataframe, with a note on an extra column that was scraped ("Author") being dropped afterwards.

**Index**|**Feature**|**Data Type**|**Description**|
|---|---|---|---|
|1|Title|Object (Text)|The titles of the posts|
|2|Selftext|Object (Text)|The main body of the posts. Posts that do not contain a body are filled with "no_text"|
|3|Subreddit (Target Variable)|Categorical|The subreddit the post belongs to. JapanTravel = 1. solotravel=0|

There was a 4th column called "Author", a text variable, that was collected along with the above features. However, this was swiftly dropped during data exploration and does not play any part in modelling.

## Section 4: Production Model and Analysis

The final model used is a Logistic Regression model using Elasticnet with the following features:

- **Vectorizer**: Tf-idf Vectorizer was used
- **Columns**: 'Title' and 'Selftext' were combined and processed together
- **Stop words**: Stop words were left inside
- **Lemmatization**: Lemmatization was done
- **Max Features**: A maximum of 500 features (words) were used

### Why did I leave stop words inside?

Removing stop words reduced performance of both classifiers significantly; both bias and variance increased, particularly the variance. As you will see in the data exploration, Question 2 ("How do the shortest strings look like?"), there are a significant number of stop words used in JapanTravel. Its top most frequent word, 'the', is mentioned over 15,000 times, compared to solotravel's use of 'the', which is 3rd most frequent at only 5,000 or so usages. Since these stop words are mentioned around 2-3 times more often in JapanTravel, the presence of stop words gives the models useful information in the form of number of times they are used in a post.

This is further augmented by our analysis in Question 3 ("How do the shortest strings look like?"), Question 5 ("How many unique and non-unique tokens are there?") and Question 6 ("What is the average length of tokens?"), which finds that both subreddits have an average token length of around 3-4, with JapanTravel having 3 times as many tokens. Removing stop words removed a large number of these tokens, giving the models less information to work with.

### How did we manage to get the production model?

#### Adding 'title' to 'selftext' gave the model more information to work with

I think the biggest factor was adding the post titles to the main text, giving both subreddits more information to work with. This is significant because some posts in selftext were empty, which I had replaced with "no_text". There were more posts in solotravel that had no_text compared to JapanTravel, which could explain why there were more False Negatives before title information was added in. Since a title was mandatory, and, as we explored in question 7 ("What are the most common unigrams, bigrams, and trigrams?"), different topics were discussed, the words in the titles would be different from one another.

#### Lemmatizing words increased token frequency

The second factor was lemmatizing words. This reduced different forms of words to its lemma, the 'head word' used in a dictionary. This means there were fewer different versions of words, which increased token frequency. This difference in number is reflected in the different number of words in both subreddits.

#### Tf-idf vectorizer better than Count vectorizer

I initially used CountVectorizer to vectorize the posts. However, I used Tf-idf vectorizer in the final production model. CountVectorizer simply counts the frequency of a word, which means that rare words will be penalised. Tf-idf vectorzier considers the overall weight of words in comparison to each document (post in our case). It weighs words in comparison to how often they appear in documents, so rare words that appear in several documents a few times will still get a good weight.

I also used a max_feature argument of 500, so only the top 500 words were considered. This prevents overfitting. 

#### Using ElasticNet prevented overfitting.

Remember that we didn't use vanilla Logistic Regression, we used the ElasticNet version of it. This means that it uses a combination of Ridge and Lasso regression, giving weights to the 500 features and sometimes zero-ing them out.

## Section 5: References

Luvsandorj, Z. (2020, August 31). _Exploratory text analysis in Python_. Retrieved from [https://towardsdatascience.com/exploratory-text-analysis-in-python-8cf42b758d9e](https://towardsdatascience.com/exploratory-text-analysis-in-python-8cf42b758d9e).
