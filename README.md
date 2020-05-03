# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs & Classification - by Elton Yeo, DSI13

by: Elton Yeo, DSI13

### Context and Problem Statement

The Ministry of Manpower (MOM) wants to build up the service industry in Singapore, in order to make it more resilient to changes in the global economy. Among various data points, they wish to understand the current state and concerns of frontline service workers within the industry. This will allow them to generate solutions to train current workers and attract future workers to the industry. In particular, they are scoping their current study to service workers in the hospitality industry and the F&B industry. 

They have commissioned our group of data scientists to help to collect and process feedback from service workers in these two sub-industries. 
- In order to do so, we will use existing posts from two subreddits. Of these two subreddits (talesfromyourserver and talesfromthefrontdesk), we will determine which subreddit a given post came from. 
- We will use two different classication models for our predictions, Naive Bayes and Logistic Regression.

Developing a suitable model which classifies new feedback into either of the sub-industries will allow us to then perform more in-depth studies into the specific feedback, and generate insights for the specific sub-industries for MOM.


### Executive Summary

In gathering our data, we used feedback and advice found on two subreddits, one for servers in the F&B industry, and one for staff at the frontdesk of the hospitality industry. 960 and 870 unique posts were gathered from each subreddit respectively. We removed URLs, non-letters, stop words, and lemmatized words, and ran them through either the CountVectorizer or TfidfVectorizer before fitting it into our models.

EDA was performed and this led to some additional stop words being added, therefore, further cleaning our data. We also had a better understanding of the most common words in both datasets.

A logistic regression model with tfidfvectorizer gave the highest accuracy of 0.96 (rounded to 2 decimal places), and the highest ROC AUC score of 0.99 (rounded to 2 decimal places) when applied to our testing data. The high scores were consistent across the training and testing data, which means that we have a model that generalises well and can be used to classfy future unseen datasets relatively well. 


### Data Analysis, Cleaning and Preprocessing

We scraped data from two subreddits. We removed moderator messages and duplications. There were some posts with text in the title, but no text in the body. We assumed that the text in the title would be important (they could be short messages with pertinent content), and did not delete such posts with no text in the body; instead, we combined the title and body of each post before further analysis/processing. There were no outliers or null values. 

We created a function to clean the text. The function helped to: 
- remove any URLs which had been included in posts
- remove non-letters and split the text into just words
- convert all letters to lower case and split into individual words
- lemmatize words (i.e. group together different inflected forms of a word so they can be analysed as a single item)
- remove stop words from a pre-determined set
- remove stop words from a set which I have customised (based on my observation/assessment of meaningless/unnecessary words)

We used word clouds and bar graphs to visualise the frequency of words in both datasets. Meaningless words found during the visualisation were removed as part of a customised list of stop words. 


### Modelling

Having cleaned the data, we used two different classication models for our predictions, Naive Bayes and Logistic Regression. 

For each model, we used CountVectorizer and TfidfVectorizer respectively to treat the data before feeding it into the model. This converted the words into numbers, which can then be processed by our models. In the case of TfidfVectorizer, it also weighted words based on how often they appeared within and across documents. 

Success was evaluated based on:
- The area under the Receiver Operating Characteristic (ROC) curve, which ranges from 0 to 1.The higher the ROC area under curve (AUC), the more separated our positive and negative populations, and the better our model in classifying the feedback

- The accuracy score, which ranges from 0 to 1. The higher the accuracy score, the more closely our predicted target variables match our true target variables.

Our baseline accuracy score was 0.525, and our baseline ROC AUC score was 0.5. The accuracy score and ROC AUC score for our final chosen model (Logistic regression with tfidfvectorizer) were 0.96 and 0.99 respectively. Our final chosen model performed better than the baseline, and the other models we trained, at classifying feedback into the sub-industries. The high scores were consistent across the training and testing data, which means that we have a model that generalises well and can be used to classfy future unseen datasets relatively well. 


### Conclusion and Recommendations

With our final chosen model, we can now classify new feedback that come from service workers in the hospitality and F&B industry with high accuracy. Thereafter, we can further analyse the feedback for each sub-industry to generate a detailed report for MOM on the current state and concerns of workers in the sub-industries, so that they may use such insights to create and refine policies.  

Proposed next steps: We can further apply the steps we have taken in this project to develop models that can help to differentiate larger collections of feedback into even more sub-industries, and this will help to extend the scope of MOM's study and allow them to understand the feedback and concerns of more sub-industries better. This would greatly benefit their study. 

In terms of the modeling, we could consider using other classification models such as K-nearest neighbours, or we could play around with more parameters in Gridsearch to achieve even better results or greater computing efficiency (which would be important if we are processing a lot of feedback data).

Given that MOM is interested in the service industry in Singapore, we could consider using posts from local forums such as HardwareZone to develop the model, so that the model will be trained on words which Singaporeans might be more likely to use. 