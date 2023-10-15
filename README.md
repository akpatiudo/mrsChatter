# mrsChatter
Mrs Chatterjee Vs Norway: A Review Analysis of Twitter’s Perception Of The Movie.

Introduction
…who loves the child most, the mother or the foster parents?
Who decide whose cultural way of doing things is the best and on what moral scale? Anything you have to lie and blackmail under any guise to achieve defies the essence of morality itself. Mrs Chatterjee offence is rooted somewhat in her culture, the official list of charges against her include reasons like sleeping in the same bed, hand-feeding her kids and applying kohl on their faces to ward off evil eye. She is called mad, unstable and unfit to be a mother, but she will fight against all odds to get her kids back. 
In this blockbuster movie full with empathy, doggedness and hates, you realise it’s not just Mrs Charrerjee Vs Norway but a lot more. Her in-laws, her husband, mothers of other kids in school, misogyny and deep-rooted patriarchy. Yet, her relentless efforts fighting this legal battle will bring you close to tears. During this fight, she unveiled the scam that authorities are running in the name of child welfare and tries to expose the whole foster parents’ scheme. 
The movie started with Rani Mukerji who moved to Norway 12 years ago with husband Anirudh Chatterjee, they have two kids: son Shubh and daughter Suchi.
About the Analysis
This analysis was carried out to show Twitter’s perception of the movie. I wanted to find out the most popular hashtag, the busiest day, the busiest hour, viewers sentiment about the movie, emotions, how words are pair(bigram) and how the movie conversation generally fared on Twitter.

**Use Case**
Viewing your Business from the prism of social media can change a whole lot about how you handle your business. An analysis like this can practically tell you what people feel about your goods and services. Sentiment analysis can give a company direction on what to do, thereby saving stockholders time and money Data Analysis Process
To make sense of any available data, a set of procedures must be completed. Identifying these procedures is essential as each stage is crucial in ensuring that the data is appropriately processed in a bid to offer useful and actionable information. Here are the steps I took in this process:
1	Data Gathering
2	Data Assessment and Cleaning
3	Data Processing
4	Data Analysis
5	Sentiment Analysis
6	Bigram Analysis and Network Definition
7	Data Visualization
8	Communications and Insights 

**Data Gathering**
First, I loaded in my require R packages for the NPL analysis, I scraped 126,000 tweets from Twitter using R twitteR and R rtweet. They both provide interface to the Twitter API which allows me to interact with Twitter data, such as retrieving tweets, posting tweets, searching for tweets, and accessing user information. the tweets scraped where from 30th May 2023 to 8th June 2023
I collected the user_id, tweets, likes and retweets using keywords such as ("#MrschatterjeeVsNorwayTrailer OR MrschatterjeeVsNorwayTrailer OR #MrschatterjeeVsNorway OR MrschatterjeeVsNorway").

**Data Assessment and Cleaning**
It is no new fact that most of the time spent on an analytical process is spent on Data Cleaning. Mine was no different either.
I mined a total of 126,120k tweets and there was a total of 344,500k retweets and 1,972,531M likes from across the globe
After inspecting my dataset for missing data, irrelevant features and duplicate values, I chose five columns relevant for this analysis, I used the Summary () to see how my tibble looks like, used str () to see the datatype and dim () to view the size of my tibble, I further wrote a function to extract hashtag and created column for it, then I sorted for top ten for visualization 

**Data Analysis**
I Used lubridate package to see the day and time each tweet was made, the volume of tweets had their peaks on Sunday through Wednesday, this makes sense, people seem to be tweeting about Mrs Chatterjee vs Norway during the week days after watching it over the weekend, the discussion gain momentum on Mondays and Tuesdays before a downward trend begins, there are indication for those that lasted throughout the week but the peaks are not high compare to those of Monday and Tuesday
 
 ![image](https://github.com/akpatiudo/ropo/assets/118566096/beb51879-f4a1-42f0-9549-897bd7dfa262)

I looked at number of tweets per hour, between 0 hours to 5 hours, there were no much tweets, people seems to be sleeping during this time, however, from 7 hours to about 16 hours there was a steady increase in tweets, people are fully active at this hour most people seems to be back from work

![image](https://github.com/akpatiudo/ropo/assets/118566096/ea803455-23be-4b82-90af-01115ef66121)

I however need to find all the text in my “tweets.rds” object and convert it into a list which I will then convert to carpus to enable me do all the cleaning, removing of stop word and set the stage for both text and sentiment analysis 
Tokenize the text tokenizing splits the corpus into words using the tokenize word function. In this case the result is a list with 126,120 items in it, each representing a specific word. Token nice text were plotted against their frequency of occurrence.

![image](https://github.com/akpatiudo/ropo/assets/118566096/d7364e7a-7639-4c4d-ab70-46afab2caeec)

**5 Sentiment Analysis**
Contained in this data frame are 13 sentiment scores from four different dictionaries: GI, HE, LM, and QDAP. Running the analyzeSentiment() command compares the text of the tweets with these various dictionaries, looking for word matches. When there are matches with positively or negatively categorized words, the tweet is given a corresponding sentiment score, which is located in the tweets. tibble1_sentiment tibble frame.
There is no theoretical reason to rely on one of these dictionaries more than the others, thus, I created a mean value for each tweet’s sentiment level, leaving us with a single sentiment value for each tweet.  I then filter in the  order below to separate the sentiment categories, then I counted my filtrates to be 2100, 1000, 5746 respectively for negative, positive and neutral.
tweets.rds2_negative <- filter(tweets.rds2, mean_sentiment < 0)
tweets.rds2_positive <- filter(tweets.rds2, mean_sentiment > 0)
tweets.rds2_neutral <- filter(tweets.rds2, mean_sentiment == 0)
5b Sentiment Analysis: A look at People' Emotion
Stemming and lemmatizing are techniques used in natural language processing (NLP) to reduce words to their base or root form. Stemming removes prefixes, suffixes, and other affixes from words to obtain the stem or base word.
Lemmatizing, on the other hand, aims to determine the lemma,dictionary form of a word, it considers the context and grammar of the word.
the first code arranges the tokens_speech data frame by the word column and display rows 316 to 325. the second code, stemmed create a new column of word, with the stemmed versions of the words in the word column. It uses the SnowballC::wordStem()
the "NRC Emotion Lexicon" developed by Saif M. Mohammad and Peter D. Turney. is One popular sentiment lexicon for political analysis It includes sentiment annotations for various emotions and is commonly used in political sentiment analysis studies. You can obtain the "NRC Emotion Lexicon" using the get_sentiments() function from the tidytext package. This was used to see the emotional aspect of the sentiment analysis
 
 ![image](https://github.com/akpatiudo/ropo/assets/118566096/e847f169-d815-481d-aedb-65493f76bb9d)

**6 Bigram Analysis and Network Definition**
Bigram counts pairwise occurrences of words which appear together in the text. it is also known as collocation analysis or phrase extraction, It seeks to explain the co-occurrence patterns of pairs of words in a text corpus. It aims to identify and analyze meaningful word combinations, known as bigrams, that occur together more frequently than would be expected by chance. it gives a better understanding how words are used in the tweets and a network of word was build

![image](https://github.com/akpatiudo/ropo/assets/118566096/cd17209b-7dc6-465c-bce5-fd43c67b3d58)
 
**Data Visualization**
For visualisation, I exported my final csv file to Power BI and I created a dashboard to better display my findings and communicate the analysis.
 
 ![image](https://github.com/akpatiudo/ropo/assets/118566096/92718343-78be-4751-afa6-ad5f6491b1b0)

 
**Communication and Insights**
The top hashtag relating to the show was #MrsChatterjeeVsNowey. This would be as a result of the fact that it is the movie’s name, it makes sense for people to made a tweet with the above hashtag and it’s only normal that people would want to continue with that for visibility case. 7.6k hashtags and This tweet is also the most liked and most retweeted this was followed by the major cast #RaniMukerji, it has 1.6k hashtag, this is natural consider how she spawned passion, anger, agony, love, persistence, emotions into her cast, tell the word the love and the pain of a mother whose kids have been taken away from her forcefully on the pretext of improper parenting.  
The sentiment analysis shows.  64.96% of Twitter had something positive to say about the movies, 23.74% were not happy with the movie, they have something negative to say and 11.3% where neutral about the movie
Based on the sentiment/emotional scores from tweets analysed I observe the following sentiments and their corresponding counts and percentages and I report from10 and above: Anticipation: 8600 occurrences, accounting for approximately 13.2% of the sentiment score. Joy: 7146 occurrences, accounting for approximately 11.0% of the sentiment score. Negative: 6800 occurrences, accounting for approximately 10.0% of the sentiment score. Positive: 13746 occurrences, accounting for approximately 21.1% of the sentiment Trust: 11200 occurrences, accounting for approximately 17.3% of the sentiment score.

![image](https://github.com/akpatiudo/ropo/assets/118566096/b1d3a7fc-26b1-4ed2-9968-ebad5d836deb)

 
Sunday through Wednesday has the highest peak of tweets, this makes sense, people seem to be tweeting about Mrs Chatterjee vs Norway during the week days after watching it over the weekend, the discussion gain momentum on Mondays and Tuesdays before a downward trend begins, there are indication for those that lasted throughout the week but the peaks are not high compare to those of Monday and Tuesday. And the 7 hours to about the hour 16 was the busiest hour, there was steady increase in tweets, people are fully active at this hour most people seems to be back from work
Bigram tells us how words in tweets were pair It seeks to explain the co-occurrence patterns of pairs of words in a text corpus. It aims to identify and analyze meaningful word combinations, known as bigrams

![image](https://github.com/akpatiudo/ropo/assets/118566096/d3f06294-ae03-400c-bace-6ae7afd24ed8)

 
The movie did well in terms of social media presence, I think the marketing team behind the scene smashed it, well done!! 
Film: Mrs Chatterjee Vs Norway
Cast: Rani Mukerji, Anirban Bhattacharya, Jim Sarbh, Balaji Gauri, Neena Gupta
Director: Ashima Chibber
