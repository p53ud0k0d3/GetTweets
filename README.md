# GetTweets
Lets you download tweets of any user from twitter

Install [tweepy](https://github.com/tweepy/tweepy) package to connect to Twitter API

**pip install tweepy**

We’ll need Twitter credentials to access the API. Create a new app on the [Twitter Application Manager](https://apps.twitter.com/).
 You can fill in any domain for the website and leave the callback URL blank. Once created, generate your credentials.
  Copy those credentials into the code file.

```
consumer_key = "YOURCONSUMERKEY"
consumer_secret = "YOURCONSUMERSECRET"
access_key = "YOURACCESSKEY"
access_secret = "YOURACCESSSECRET"
```

We have a function *get_all_tweets()* that pulls down all tweets for a given screen name. We have to do this iteratively, as the Twitter API only allows 200 tweets at a time. Also, we can only retrieve the 3,024 most recent tweets.
Once we hit that limit, our *new_tweets* array will be blank and we will stop iterating.

We have a function *clean_tweet()* to remove unwanted texts from tweets and clean them up.

```
def clean_tweet(tweet):
    tweet = re.sub("https?\:\/\/", "", tweet)   #links
    tweet = re.sub("#\S+", "", tweet)           #hashtags
    tweet = re.sub("\.?@", "", tweet)           #at mentions
    tweet = re.sub("RT.+", "", tweet)           #Retweets
    tweet = re.sub("Video\:", "", tweet)        #Videos
    tweet = re.sub("\n", "", tweet)             #new lines
    tweet = re.sub("^\.\s.", "", tweet)         #leading whitespace
    tweet = re.sub("\s+", " ", tweet)           #extra whitespace
    tweet = re.sub("&amp;", "and", tweet)       #encoded ampersands
    return tweet
```

Find this code at the bottom. Pass the screen-name of the person whose tweets you want to download, to the function *get_all_tweets()*.
Here I am passing the screen-name of Bollywood actor Shah Rukh Khan, which is *iamsrk*.

```
if __name__ == "__main__":
    tweets = get_all_tweets("iamsrk")
    write_tweets_to_csv(tweets)
```

Run the script

**python get_tweets.py**

After the script has completed running successfully, there will be a file name *tweets.csv*, which contains all the tweets you have downloaded. Enjoy :+1:
