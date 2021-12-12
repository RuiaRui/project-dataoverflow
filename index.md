---
layout: index
title: Datastory
subtitle: Balabalabala
---


### The data

The [Quotebank](https://zenodo.org/record/4277311#.YbN3I32ZNO8) data-set we use contains english quotations gathered from online news articles in the period between 2008 and 2020. We filter the data to obtain quotations relating to China which were uttered by a person with a western background as defined by their nationality. 

The data flitering was done by checking whether specific keywords relating to china can be found in either the title, quotation or local left and right context of the quotation. We checked for the following keywords: 

`['jinping xi', 'xi jing ping', 'xi jinping', 'president xi', 'china', 'chinese', 'beijing', 'peking', 'sino-']`

In order to determine whether a certain speaker is from a 'Western' background, we check whether they come from one of the countries in the political definition of [Western countries](https://sashamaps.net/docs/maps/list-of-western-countries/). As mentioned before, after filtering we are left with approximately 2 million article-quotation pairs. \

{% include quotation_distribution.html %}

### Which topics are associated with China by western press

{% include topic_chase.html %}

### How do Western speakers feel about the topics presented in the Western press

### How do different groups of people feel about China