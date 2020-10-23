# Churn-Prediction-and-Analysis

Taking into consideration that the market is being saturated and revenue from new subscriptions is increasingly deteriorating, mobile carriers tend to focus on customer service and high levels of customer satisfaction, in order to retain registered customers and maintain a low churn rate. In this analysis, I try to examine if mobile wireless carriers can benefit from performing sentiment analysis through social media networks in order to enhance and improve customer service, which will lead to increased customer satisfaction, thus keeping a low churn rate.

### Data Source and Preperation

- Collected over 213,859 tweets during the time between October 9, 2019, and October 23, 2019 using Twitter's Streaming API. Looked for tweets with keywords - "VerizonSupport," "VZWSupport," "ATT," "ATTHelp," "TMobile" and "TMobileHelp".

- The corresponding dataset included a total number of 82395, 47746 and 31842 tweets respectively for AT&T, Verizon and T-Mobile, which were then categorized into a class of 2 and 3 mobile carriers such as [ ATT, T-Mobile],[ T-Mobile, Verizon],[ ATT, Verizon] and[ ATT, T-Mobile, Verizon].

- The data was then cleaned and preprocessed for analysis. The process involved tokenizing text into words, removing stop words, links, hashtags, handles mentions and words with less than three characters.

### Exploratory Data Analysis

#### 1.	Tweets counts for each carrier and each group

![Tweet Count](https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda1.png?raw=true "Optional Title")

#### 2. Most frequent words in each carrier

![Frequent Words](https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda2.png?raw=true "Optional Title")

![Frequent Words](https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda3.png?raw=true "Optional Title")

According to the BOW model, we got the top 5 common words of each carrier. For Verizon, users like to mention Disney, free service, and yearly plans in their tweets. Similarly, for TMobile and ATT, users are talking about comments, tickets, and customers.

#### 3.	Counts for each carrier mentioned daily

![Daily Count](https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda4.png?raw=true "Optional Title")

During the time between 2019-10-09 and 2019-10-23, we can observe how the number of tweets mentioning each carrier varies. Some interesting observations are:
- On 2019-10-15 Tuesday, the number of tweets for TMobile is maximum, the possible reason can be t-mobile Tuesday promotional offers.
- On 2019-10-19, a lot of ATT users were facing network issues. That can be the reason behind the sudden rise in the number of tweets.
- On 2019-10-22, Verizon tweets were the maximum. They announced a free year of Disney+. The users might be comparing it with ATT offers. 

#### 4.	Sentiment polarity distribution for each carrier

![Sentiment Polarity](https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda5.png?raw=true "Optional Title")

We can see how the sentiment varies for each tweet mentioning different carriers. It helps us to understand how many tweets were positive and negative. For example, ATT had maximum number of tweets with -0.5 polarity (negative). Most of the tweets for each carrier were positive.

#### 5.	Overall sentiment polarity of each carrier

![Sentiment Polarity](https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda6.png?raw=true "Optional Title")

![Sentiment Polarity](https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda7.png?raw=true "Optional Title")

As we can see from the overall sentiments graph, ATT gets the lowest sentiment score, and TMobile gets the highest. An interesting observation is that carrier with more tweets mentioned has less sentiment polarity score.

#### 6.	Positive vs. Negative tweets for each carrier

![Sentiment Polarity](https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/eda8.png?raw=true "Optional Title")

From the graph, we can notice that in all three carriers, as the number of tweets increases, the proportion of negative numbers also increases. Maybe users like to complain more than praise on tweets.

#### 7.	Representative words

With the help of topic modeling we found negative and positive topics for each carrier. ATT positive topics are about wifi and service, ATT negative topics are about internet, ticket and game. Verizon positive topics are about iphone and data, Verizon negative topics are about samsung, bill and outage. TMobile positive topics are about family, speed and offer, TMobile negative topics are about coverage and service.
