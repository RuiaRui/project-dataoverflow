---
layout: index
title: Datastory
subtitle: Balabalabala
---


### The data

The [Quotebank](https://zenodo.org/record/4277311#.YbN3I32ZNO8) data-set we use contains english quotations gathered from online news articles in the period between 2008 and 2020. We filter the data to obtain quotations relating to China which were uttered by a person with a western background as defined by their nationality. 

The data flitering was done by checking whether specific keywords relating to china can be found in either the title, quotation or local left and right context of the quotation. We checked for the following keywords: 

`['jinping xi', 'xi jing ping', 'xi jinping', 'president xi', 'china', 'chinese', 'beijing', 'peking', 'sino-']`

In order to determine whether a certain speaker is from a 'Western' background, we check whether they come from one of the countries in the political definition of [Western countries](https://sashamaps.net/docs/maps/list-of-western-countries/). As mentioned before, after filtering we are left with approximately 2 million article-quotation pairs.

Below we see a map of the amount of quotations per country in the western world, note that the `QuotationScale` is the logarithm of the amount of quotes. As we can see the vast majority of quotes are from the US, with a smaller amount of quotes coming from all other countries. Therefore, when observing the results please take into account that most of the data the investigation is based on is from the US.

{% include quotation_distribution.html %}

### Which topics are associated with China by western press

{% include topic_chase.html %}

### How do Western speakers feel about the topics presented in the Western press

When we look at the various topics we saw the general trend that a lot of news seems to focus on the negative things that are associated in China. As an example one may take the Hong Kong protests which in itself could be interpreted as a negative event related to China. However, is it also the case that the quotations about these topics carry a negative connotation towards China?
In this section we will explore the opinion of Western speakers regarding the main topics presented in the previous section.

In order to gauge the opinion of Western quotees, we calculated the sentiment index per quotation in the dataset, and aggregate them per topic. Normally, we would not be able to aggregate the quotations per topic, as keywords regarding the same topic may be very different, e.g. 'corona virus' and 'covid-19 outbreak'. The way we deal with this is to train a classifier that classifies keywords into pre-specified topics. We train this classifier by leveraging the fact that each quotation-article pair has a list of 5 keywords. What we do is segment the top 50 most frequent keywords per year into several meaningful categories, we then assume that everything that is in a list with one of the top 50 keywords is related to that keyword topic. We then label all keywords that only occur once in the dataset as outliers if they are unrelated (not in the same list) to the top 50 keywords. We then train the classifier on this labelled data, and let it predict on the keywords that were not labelled in the original 'manual' labelling. 

### How do different groups of people feel about China