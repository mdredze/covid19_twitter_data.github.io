---
layout: page
title: Data Description
subtitle: 
---

<h1 class='#top'> Data Overview </h1>

The data contains over 10 million COVID-19 related tweets collected from 2020-02-06 to 2020-03-27.
All data entries are saved as json format.
Each tweet was annotated with two addtional extracted information, keywords and geolocation.
Within the data, tweets are grouped and saved separatively by their created dates.
Each file's name format follows *covid19_year_month_day_minimal.json*, where each line is one tweet data entry.
You can re-collect the tweets by the [Hydrator](https://github.com/DocNow/hydrator).


A data entry example:
```{"tweet_id":1227457278930014208,"user_id":860989842166923264,"date":"Wed Feb 12 04:59:55 +0000 2020","keywords":["wuhan"],"city":{"country":"United States","state":"Oregon","city":"Tigard"}}```



<h1>Data Format</h1>

The data contains five data fields: *Twitter ID*, *User ID*, *Date*, *Keywords* and *Location*.  

* Twitter ID (`tweet_id`): An integer value that represents a unique id of a tweet.
* User ID (`user_id`): An integer value that represents a unique id of the user who posts the tweet.
* Date (`created_at`): A string value that indicates the date when the tweet was created. 
* Keywords (`keywords`): A list of detected keywords that relate to Coronavirus. Default is **['UNK']**.
* Location (`location`): A dictionary of detected geolocations include country, state and city. Default is **'UNK'**.



<h1>How the Data was Processed</h1>

We generate the data by the following three steps:

1. Tweet preprocessing: We collected tweets daily from 2020-02-06 to 2020-03-27 and saved the tweets as json files. We removed the tweets that were not well formatted in json entries.

2. Keywords extraction: We annotated lowercased tweets by a list of keywords that relate to the COVID-19. Any tokens including hashtags start with the keywords will be extracted. 
    * The keyword list: coronavirus, wuhan, 2019ncov, sars, mers, 2019-ncov, wuflu, covid-19, covid19
covid, sars2, sarsscov19

3. Location extraction: We applied the [Carmen](https://github.com/mdredze/carmen-python), a geolocation annotation toolkit, to obtain the location information from tweet metadata and user profiles. Each location contains three levels of information, country, state and city. Any empty fields are assigned *UNK*.






<div align="right">
    <b><a href="#top">↥ back to top</a></b>
</div>
