# Churn-Prediction-and-Analysis

Taking into consideration that the market is being saturated and revenue from new subscriptions is increasingly deteriorating, mobile carriers tend to focus on customer service and high levels of customer satisfaction, in order to retain registered customers and maintain a low churn rate. In this analysis, I try to examine if mobile wireless carriers can benefit from performing sentiment analysis through social media networks in order to enhance and improve customer service, which will lead to increased customer satisfaction, thus keeping a low churn rate.

## Data Source and Preperation

- Collected over 213,859 tweets during the time between October 9, 2019, and October 23, 2019 using Twitter's Streaming API. Looked for tweets with keywords - "VerizonSupport," "VZWSupport," "ATT," "ATTHelp," "TMobile" and "TMobileHelp".

- The corresponding dataset included a total number of 82395, 47746 and 31842 tweets respectively for AT&T, Verizon and T-Mobile, which were then categorized into a class of 2 and 3 mobile carriers such as [ ATT, T-Mobile],[ T-Mobile, Verizon],[ ATT, Verizon] and[ ATT, T-Mobile, Verizon].

- The data was then cleaned and preprocessed for analysis. The process involved tokenizing text into words, removing stop words, links, hashtags, handles mentions and words with less than three characters.

## Exploratory Data Analysis

### 1.	Tweets counts for each carrier and each group

<img src="https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda1.png" alt="alt text" width="70%" height="70%">

### 2. Most frequent words in each carrier

<img src="https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda2.png" alt="alt text" width="70%" height="70%">

<img src="https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda3.png" alt="alt text" width="70%" height="70%">

According to the BOW model, we got the top 5 common words of each carrier. For Verizon, users like to mention Disney, free service, and yearly plans in their tweets. Similarly, for TMobile and ATT, users are talking about comments, tickets, and customers.

### 3.	Counts for each carrier mentioned daily

<img src="https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda4.png" alt="alt text" width="70%" height="70%">

During the time between 2019-10-09 and 2019-10-23, we can observe how the number of tweets mentioning each carrier varies. Some interesting observations are:
- On 2019-10-15 Tuesday, the number of tweets for TMobile is maximum, the possible reason can be t-mobile Tuesday promotional offers.
- On 2019-10-19, a lot of ATT users were facing network issues. That can be the reason behind the sudden rise in the number of tweets.
- On 2019-10-22, Verizon tweets were the maximum. They announced a free year of Disney+. The users might be comparing it with ATT offers. 

### 4.	Sentiment polarity distribution for each carrier

<img src="https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda5.png" alt="alt text" width="70%" height="70%">

We can see how the sentiment varies for each tweet mentioning different carriers. It helps us to understand how many tweets were positive and negative. For example, ATT had maximum number of tweets with -0.5 polarity (negative). Most of the tweets for each carrier were positive.

### 5.	Overall sentiment polarity of each carrier

<img src="https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda6.png" alt="alt text" width="30%" height="30%">

<img src="https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda7.png" alt="alt text" width="70%" height="70%">

As we can see from the overall sentiments graph, ATT gets the lowest sentiment score, and TMobile gets the highest. An interesting observation is that carrier with more tweets mentioned has less sentiment polarity score.

### 6.	Positive vs. Negative tweets for each carrier

<img src="https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda8.png" alt="alt text" width="50%" height="50%">

From the graph, we can notice that in all three carriers, as the number of tweets increases, the proportion of negative numbers also increases. Maybe users like to complain more than praise on tweets.

### 7.	Representative words

With the help of topic modeling we found negative and positive topics for each carrier. ATT positive topics are about wifi and service, ATT negative topics are about internet, ticket and game. Verizon positive topics are about iphone and data, Verizon negative topics are about samsung, bill and outage. TMobile positive topics are about family, speed and offer, TMobile negative topics are about coverage and service.

## Churn Detection Analysis

### 1. Manually labeling the tweets as churn/non-churn

As we need lableled data to train machine learning algorithm, we manually labelled around 4000 tweets as 'churn' or 'not-churn' by understanding the context and the words used in the tweets. However, this wasn’t enough for the large corpus that we had.

### 2. Train machine learning model

We used the above manually labelled tweets as an input to a machine learning model to predict the labels for a set of unseen tweets. We followed the following steps:
- Split the manually labeled input dataset of 4000 to train and test sets of 80% and 20% respectively.
- Use the train data set to train the model and test it on the test dataset. Tune the model hyperparameters and repeat. Test it on unseen data outside of the test set previously provided.
- Validate the results manually, refine the input and predict the next 500 labels with the help of the model. Now add this new labeled set to the training dataset and predict another set of 500 tweets with the updated training dataset.
- In this way we were able to label another 2000 tweets and validate them manually.

We used two models,namely Naive Bayes and XGBoost, however, XGBoost proved to outperform the others with an accuracy of 73%.  Now, we had 6000 labelled tweets. However, it still wasn’t enough. Hence, we decided to develop a rule based algorithm on top of this approach to identify the churn labels, churn reason and provide suggestions in a heuristic way.	

## Rule Based Algorithm

We developed a rule-based algorithm to determine the following:
- If the user was likely to churn 
- Reason for churn
- User wants to churn from which old carrier and to new carrier

### Detecting users churn direction

<img src="https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/algo1.png" alt="alt text" width="70%" height="70%">

Consider the simple example above - ‘ATT is good and TMobile is bad. Because ATT has better service’. The reader can easily figure out that this user might want to churn from TMobile to ATT. The reason is that ATT has better service. Then, how does the machine do the semantic analysis and come to this conclusion? Our rule-based algorithm follows the following approach to help machine with it:

1. Identify three subjects, ‘ATT’, ‘TMobile’ and ‘Verizon’ in each tweet. 
2. Disassemble the original text and find out a match between words or sentences and the subject. In the above example, we need to make the machine understand ‘good’ is describing ‘ATT’ and ‘bad’ is describing ‘TMobile’. In reality, people's language has many expressions, and this simple and neat language format is rarely encountered on Twitter. Therefore, we have summarized some semantic rules by reading a lot of tweets. 
3. Used these rules to segment the text and add some scores to each subject. We assume that users always want to churn from a low-scoring subject to a high-scoring subject.

Here are some of our rules: 

- “switch from… to…”, which is a typical sentence that clearly states where the user wants to churn from which carrier. So the carrier in “from” group will decrease score, and the score of the carrier in “to” group will increase. Synonyms of switch, such as transfer, try to, free from and so on, all follow the same rule. 
- The carrier appearing after “like” or “hate” will also increase or decrease the score, since it implies that the user has a potential intention to churn. 
- Similarly, people might use a lot of positive vocabulary to describe the new carrier they want to go, or use many negative vocabulary to describe the current carrier to imply the  intention of churn. Therefore, we will eventually add the sentiment polarity value to the score for each subject. 
- The conjunction words, such as “and” and “but ”, are very crucial signs that help us segment the text and find the words that describes the certain subject.
	
  The challenge of this algorithm is to identify more semantic rules and define the weights of score of each rule. Our current approach is to artificially collect and add rules, then adjust weights manually.

### Detecting churn reason

For the churning reason, there are some indicators that users often mention. Then we try to figure out and collect these indicators, such as “service”, “coverage”, “data”, “wifi”, “price”, “family” and so on. If one of these words appear in a sentence, we will roughly attribute it to the reason. And comparative adjectives, such as ‘smaller’, ‘cheaper’ and so on, also imply the comparative relationship between the two carriers. These comparative adjectives are also the indicators of the churning reason detection. The challenge of this algorithm is to find out a method that makes machine to find indicators automatically and improve the scalability. 

## Insights

### Summarizing churn reason

<img src="https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/insight1.png" alt="alt text" width="70%" height="70%">

When we identify the carrier that the user is unsatisfied with and extract the reasons for dissatisfaction by rule-based algorithm for each tweet, we build out three corpuses of unsatisfied reasons for each carrier. Through the analysis we can summarize the problem areas of each carrier.
