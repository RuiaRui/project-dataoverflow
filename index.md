---
layout: index
title: Datastory
subtitle: Balabalabala
---
## What we are trying to do?

Quotations are often used as a literary device to represent someone's point of view. We believe that these Quotations used in the news related to China represent the attitudes of Western politicians and, to some extent, of the Western public towards China. By analyzing those Quotations, we hope to answer the question: what are the attitudes of the Western world towards China?

We use keyword filtering to get the related quotations, then apply KeyBERT, a minimal keyword extraction technique, to the quotations and their left and right contexts to create keywords and key phrases that are most similar. We also aggregate keywords into more general topics. Then, we use `Twitter-roBERTa-base` for our sentiment analysis on each quotation and get a sentiment score from -1 ~ 1 to represent the positive scale of the attitude of that quotation. 

We will present our data story in the following structure:

- ​	[How does our data look like?](#how-does-our-data-look-like-?) 

- What are people talking about when they talk about China?
- What are their attitudes?
- The difference in attitudes?
- Interesting findings?

## How does our data look like?

The [Quotebank](https://zenodo.org/record/4277311#.YbN3I32ZNO8) data-set we use contains English quotations gathered from online news articles in the period between 2008 and 2020. We filter the data to obtain quotations relating to China which were uttered by a person with a western background as defined by their nationality. 

The data filtering was done by checking whether specific keywords relating to china can be found in either the title, quotation, or local left and right context of the quotation. We checked for the following keywords: 

`['jinping xi', 'xi jing ping', 'xi jinping', 'president xi', 'china', 'chinese', 'beijing', 'peking', 'sino-']`

In order to determine whether a certain speaker is from a 'Western' background, we check whether they come from one of the countries in the political definition of [Western countries](https://sashamaps.net/docs/maps/list-of-western-countries/). As mentioned before, after filtering we are left with approximately 2 million article-quotation pairs.



#### Overview of the Filtered Data



Below we see a map of the number of quotations per country in the western world, note that the `QuotationScale` is the logarithm of the number of quotes. As we can see the vast majority of quotes are from the US, with a smaller amount of quotes coming from all other countries. Therefore, when observing the results please take into account that most of the data the investigation is based on are from the US.

{% include quotation_distribution.html %}

{% include quotation_top5_countries.html %}

## What are people talking about when they talk about China?

To understand people's attitudes, first we need to understand what they are talking about. And we can figure this out by extracting keywords from quotations. We choose the pre-trained model KeyBERT to extract the five possible bigram keywords for each quotations, and use these five keywords to represent this quotation. After extracting keywords, we can infer what events people are discussing by associating keywords with news events. 

We generate a word cloud plot for all the quotations' keyword to show the frenquence of keywords mention in whole dataset of all the years we have.

![keyword-World_Cloud.png](images/bg.jpg)

Over all year, the most frequently mentioned keywords are:

|      | Keywords           | Count  |
| ---- | ------------------ | ------ |
| 1    | north korea        | 40042  |
| 2    | china trade        | 39788  |
| 3    | trade war          | 22993  |
| 4    | hong kong          | 21174  |
| 5    | trade talks        | 15947  |
| 6    | china sea          | 15037, |
| 7    | deal china         | 11915  |
| 8    | trade dea          | 11578  |
| 9    | chinese government | 10088  |
| 10   | climate change     | 9131   |
| 11   | human rights       | 8195   |
| 12   | china tariffs      | 6394   |
| 13   | covid 19           | 5911   |
| 14   | trump trade        | 5818   |
| 15   | president xi       | 5727   |

Suprisingly,  'North Korea' is the most frenquently mentioned keyword.  This might because we use bigram word encoding, but also due to the reason that since the change of regime in North Korea in 2011, when Kim Jong-un became leader, and since North Korea has been attempting to conduct missile and nuclear bomb tests from 2013-2017, the country has attracted a lot of attention and discussion in the international world in the intervening years. At the same time, China and North Korea, two of the most talked about socialist countries in close proximity to each other, are widely perceived to be closely linked and supportive of each other, and therefore will eventually refer to China's attitude or moves when talking about North Korea. It is therefore understandable that North Korea appears most frequently as a keyword in China-related quotations. The rest of the keywords: trade war, Hong Kong, China sea,chinese government, human rights, and climate change are more reasonable. The trade war between the United States and China in 2018-early 2020 has been a prominent topic of conversation for years, with multiple meetings between leaders and deals made or not reached being covered and discussed in the press on a regular basis. China's human rights issues and Chinese governing have always been the focus of attention and attack in the Western media. And disputes over China's territorial seas and discussions about climate change have continued to develop in the 2008-2020 era. Although the coronavirus outbreak has been a topic of discussion for everyone for the last two years, the total number of mentions of this keyword in the dataset does not rank high, mainly because the dataset only contains news quotes up to the first half of 2020.

Moreover, we create a bar chart race plot to see how the keywords change in time with counting the keyword quarterly. You can see in the plot that the keywords change frequently for the most part, but in some years some topics dominate the entire ranking.During 2017,  the keyword North Korea consistently occupy the top spot on the list, with many more mentions than other topics in the same period. In 2018, keywords related to trade war are at the top of the list.

{% include topic_chase.html %}

### How do Western speakers feel about the topics presented in the Western press

When we look at the various topics we saw the general trend that a lot of news seems to focus on the negative things that are associated in China. As an example one may take the Hong Kong protests which in itself could be interpreted as a negative event related to China. However, is it also the case that the quotations about these topics carry a negative connotation towards China?
In this section we will explore the opinion of Western speakers regarding the main topics presented in the previous section.

In order to gauge the opinion of Western quotees, we calculated the sentiment index per quotation in the dataset, and aggregate them per topic. Normally, we would not be able to aggregate the quotations per topic, as keywords regarding the same topic may be very different, e.g. 'corona virus' and 'covid-19 outbreak'. The way we deal with this is to train a classifier that classifies keywords into pre-specified topics. We train this classifier by leveraging the fact that each quotation-article pair has a list of 5 keywords. What we do is segment the top 50 most frequent keywords per year into several meaningful categories, we then assume that everything that is in a list with one of the top 50 keywords is related to that keyword topic. We then label all keywords that only occur once in the dataset as outliers if they are unrelated (not in the same list) to the top 50 keywords. We then train the classifier on this labelled data, and let it predict on the keywords that were not labelled in the original 'manual' labelling. 
{% include topic_overview.html %}
Our manual labelling resulted in the main topics shown above. 
### How do different groups of people feel about China