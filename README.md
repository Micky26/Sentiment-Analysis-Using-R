# Sentiment-Analysis-Using-R
Sentiment Analysis of tweets for any Twitter Handles
consumer_key <- 'xxxxx'
consumer_secret <- 'xxxxxx'
access_token <- 'xxxxxx'
access_secret <- 'AbwRUOwDk3LrNGknP844oVKg9qqpHGFqWe40ygIvPl01h'
setup_twitter_oauth(consumer_key, consumer_secret, access_token, access_secret)
options(httr_oauth_cache = T)
tweets <- userTimeline("@MBuhari", n = 3000)
ntweets <- length(tweets)
tweets.df <- twListToDF(tweets)
head(tweets.df$text)
tweets_df2 <- gsub("https.*","",tweets.df$text)
tweets_df2 <- gsub("https.*","",tweets_df2)
tweets_df2 <- gsub("#.*","",tweets_df2)
tweets_df2 <- gsub("@.*","",tweets_df2)
head(tweets_df2)
word_df <- as.vector(tweets_df2)
emotion_df <- get_nrc_sentiment(word_df)
emotion_df2 <- cbind(tweets_df2,emotion_df)
head(emotion_df2)
sent_value <- get_sentiment(word_df)
most_positive <- word_df[sent_value == max(sent_value)]
most_negative <- word_df[sent_value <= min(sent_value)]
positive_tweets <- word_df[sent_value > 0]
negative_tweets <- word_df[sent_value < 0]
neutral_tweets <- word_df[sent_value == 0]
category_sent <- ifelse(sent_value < 0, "Negative", ifelse(sent_value > 0, "Positive", "Neutral") )
table(category_sent)
