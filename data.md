---
layout: page
title: Data
subtitle: 
---

<h1 class='#top'> Data Format </h1>

This Twitter dataset contains tens of millions tweets related to COVID-19 collected starting on February 6, 2020.

Each gzipped file contains data from a single day. Each line of the file contains a single JSON record. You should read the file one line at a time and parse that JSON line to obtain information about one tweet.

Each tweet record will have the following fields:

- `tweet_id`: An integer value. The ID of the tweet. You will use this ID to download the tweet from Twitter.
- `user_id`: An integer value. The user ID of the author of this tweet. If this is a retweet, this is the user who retweeted the tweet.
- `date`: A string value. The date the tweet was posted in the standard Twitter date format, e.g. "Wed Feb 12 04:59:55 +0000 2020"
- `keywords`: A list. Contains COVID-19 related keywords that we used to identify this tweet.
- `location`: A dictionary. The location of this tweet. If a location is known, it can include `country`, `state`, and `city`. 

An example tweet record:
```{"tweet_id":1243171774055014401,"user_id":852581594674208768,"date":"Thu Mar 26 13:43:42 +0000 2020","keywords":["covid"],"location":{"country":"United States","state":"Maryland","city":"Baltimore"}}```


To obtain the original tweets, use the [Twitter Hydrator](https://github.com/DocNow/hydrator), which takes the `tweet_id` and downloads the corresponding tweet (if it is available.)

We occasionally have missing data due to downloading issues. You can observe missing data by gaps in the dates within the file.



<h1>Data Source</h1>
We use the Twitter public keyword streaming API to download all tweets containing COVID-19 related keywords. The keywords included in this collection are:
```
coronavirus
wuhan
2019ncov
sars
mers
2019-ncov
wuflu
COVID-19
COVID19
COVID
covid-19
covid19
covid
SARS2
SARSCOV19
```

We also include tweets that contain these keywords as hashtags, e.g. #covid19.


<h1>Data Processing</h1>

We create the dataset using the following process.

1. We match (case-insensitive) every downloaded tweet against the above keywords, including if they appear as hashtags. 
2. We inferred the location of the tweet using [Carmen](https://github.com/mdredze/carmen-python), a geolocation toolkit. Carmen provides three levels of information: country, state and city. If the tweet has a `place` or `coordinates` field, Carmen returns this information. Otherwise, Carmen infers the location from the profile field.

<h1> Citation </h1>

```
@misc{huang_xiaolei_2020_3735015,
  author       = {Huang, Xiaolei and Jamison, Amelia and Broniatowski, David and Quinn, Sandra and Dredze, Mark},
  title        = {Coronavirus Twitter Data: A collection of COVID-19 tweets with automated annotations},
  month        = {Mar},
  year         = {2020},
  note         = {http://twitterdata.covid19dataresources.org/index},
  publisher    = {Zenodo},
  doi          = {10.5281/zenodo.3735015},
  url          = {https://doi.org/10.5281/zenodo.3735015}
}
```


