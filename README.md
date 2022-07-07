# Dog Training or Running?

Dogs can run, sometimes dog parks are called dog runs. People can run, sometimes they run with their dogs. Given the overlap in language, can we identify if a user generated post is about dog training or about running?



### Problem Statement
Reddit is a social media website where users discuss topics on message boards referred to as subreddits. Can we identify if a reddit post came from the r/running subreddit or from the r/dogtraining subreddit?


### Approach

To answer the question posed above, we followed the steps as outlined below. 
 - Gathering Data
     - The subreddits we are investigating each have over 100,000 posts. To train and develop our model, we pulled a subset of the posts using the Pushshift API. The Pushshift API allows users to scrape information about the posts including title, text-referred to as selftext and the submission time-labeled as created_utc. We created a function that makes multiple calls to the API to pull the titles, text and submission timestamp of 3,000 posts from both the r/running and r/dogtraining subreddits. This data was then saved as a csv file to be used later.
     
    - More details can be found in the 'Pull Data' notebook.


 - Data Cleaning & Exploration
     - Once the data was imported, basic EDA and data cleaning was conducted. Posts with no text in the selftext, or body of the post were dropped from the dataset. We identified the most common words used across both subreddits. Additionally, we ran a basic Logistic Regression model to establish a baseline model accuracy. The selftext was vectorized using the CountVectorizer with stopwords set to 'english'. This model generated 95.7% accuracy on the test set. To make the problem more challening the 80 most impactful words were added to a list called 'custom stop words' and excluded from all future models. We re-ran a basic logistic regression model using Count Vectorizier with stopwords set to the 'custom stop words' list to establish a new baseline. The new baseline accuracy was 94%.
 
     - More details can be found in the 'Data Cleaning & EDA' notebook.
 
 - Model Exploration
     - Multiple models were run, all using CountVecorizer with stopwords set to the custom stop words. Overall the Logistic Regression continued to perform strongly, with the voting classifier model that contained Logistic Regression, Extra Trees Classifier, and Random Forest Classifier performed slightly better with 94.2% accuracy.
 
     - More details can be found in the 'Model Exploration' notebook.
 
 - Model Tuning
    - K Nearest Neighbors, Logistic Regression, Ada Boost Classifier, Gradient Boost Classifier and the Voting Classifier were tuned by adjusting the hyperparameters through grid search. Interestingly the Logistic Regression model scored slightly lower with the best hyperparameters as identified by the grid search. This is likely an anomly due to the subsets of data evaluated by each cross validation.

    - More details can be found in the 'Model Tuning' notebook.

### Recommendations


Overall, the logistic regression model is highly effective at identifying which subreddit a given post came from based on the selftext or body of the post. It is a fast, simple model, that can easily be employed. To easily boost model performance, posts with the text removed and replaced with '[removed]' should be removed from the data set during the data cleaning phase. 

