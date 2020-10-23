# Churn-Prediction-and-Analysis

Taking into consideration that the market is being saturated and revenue from new subscriptions is increasingly deteriorating, mobile carriers tend to focus on customer service and high levels of customer satisfaction, in order to retain registered customers and maintain a low churn rate. In this analysis, I try to examine if mobile wireless carriers can benefit from performing sentiment analysis through social media networks in order to enhance and improve customer service, which will lead to increased customer satisfaction, thus keeping a low churn rate.

### Data Source and Preperation

- Collected over 213,859 tweets during the time between October 9, 2019, and October 23, 2019 using Twitter's Streaming API. Looked for tweets with keywords - "VerizonSupport," "VZWSupport," "ATT," "ATTHelp," "TMobile" and "TMobileHelp".

- The corresponding dataset included a total number of 82395, 47746 and 31842 tweets respectively for AT&T, Verizon and T-Mobile, which were then categorized into a class of 2 and 3 mobile carriers such as [ ATT, T-Mobile],[ T-Mobile, Verizon],[ ATT, Verizon] and[ ATT, T-Mobile, Verizon].

- The data was then cleaned and preprocessed for analysis. The process involved tokenizing text into words, removing stop words, links, hashtags, handles mentions and words with less than three characters.

### Workflow

![Worklflow](https://github.com/netisheth/Churn-Prediction-and-Analysis/blob/master/Images/workflow.png?raw=true "Optional Title")



