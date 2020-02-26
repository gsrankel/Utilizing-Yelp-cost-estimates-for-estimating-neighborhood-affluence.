## Authors
- Gregory Rankel: [LinkedIn](https://www.linkedin.com/in/gregory-rankel/)  - [Github](https://github.com/gsrankel)
- Varun Ganti: [LinkedIn](https://github.com/adrianavesa) - [Github](https://github.com/varunganti33)
- Adriana Vesa: [LinkedIn](https://www.linkedin.com/in/adriana-v-67aa3a165/) - [Github](https://github.com/adrianavesa)


## Problem Statement
The financial impact of natural disasters is a growing concern in the world, as we observe a seemingly increasing occurrence of massive fires, floods or hurricanes. Hurricane Sandy , the 2012 October storm, did 19 billion in damage to the New York City area alone. In compact megalopolises like New York City the high concentration of population can make any natural disaster proportionally more dangerous to larger number of people. The more important point is that - even in areas perceived as affluent, there are income disparities amongst close neighborhoods - and deciding with celerity if an area is more or less affluent can have a huge influence in how resources are deployed during disasters.
New Light Technologies Inc. (NLT) is a small business based in Washington, D.C. that provides comprehensive information technology solutions for clients in government, commercial, and non-profit sectors. The company offers a unique range of capabilities from Infrastructure Modernization and Cloud Computing to Big Data Analytics, Geospatial Information Systems, and the Development of Software and Web-based Visualization Platforms. This broad technology expertise enables their customers to leverage existing technology investments - and we have been tasked to asses if the existing data collected by Yelp about the dollar price rating of businesses, can be used to asses the affluence of an area. This information can be further used in emergency situations to gauge the level of damage after a disaster, or the areas where the neediest live snd help should be sent faster. We decided to work on the New York City area as it offers an ample data set - and it reflects well the specificity of megaregions and megalopolises that dot the United States. There are over 237 million people living in these mega regions, and we considered that analyzing New York City would give us a good prototype that can be modified and used in other hyper populated areas too. We have used the specificity of large urban areas in selecting and creating our features - as the lifestyle of the people in the area to be analyzed should inform us on the features we should explore for our models.
We obtained information collected by Yelp about the way they classify the price level (in dollar signs) of businesses in New York City. We will be by using Yelp API for that. We will also download IRS data about New York City and create a metric to measure whether or not certain areas are affluent or not.
Due to what we are predicting being binary, we will run various classification models during our testing such as Logistic Regression, KNN, CART's, and ADABoost. Our assumption, is that accuracy will be the best metric in determining affluency versus not.

## Executive Summary
We were tasked to gauge the importance of the yelp $ price in assessing the affluence of a region.
We have chosen to analyze this on New York City, as it is a large area with enough data, and at the same time, representative for densely populated areas in the United States.
We have acquired the data from the Yelp Fusion API, and we ended up with more than 8000 data points - in other words - businesses that Yelp classified in accordance to their price - $ - from one $ to four $.

We have decided to use the IRS provided data for 2017 in order to decide on the affluence of a specific zip code. Each zip code has 6 thresholds of tax payers which gives an average sum of the Adjusted Gross Income (AGI) for each threshold. We have created a metric that reflects the average amount of tax payers who filed in the threshold of an AGI of over 200,000 divided by the total average sum of all the thresholds per zip code. We have then set the rate for this metric in order to assign "affluent" or not "affluent" to be 0.5 - in other words - for zip codes in which over 50 percent of the average AGI per that zip code is being derived from people who make over 200,000, we deemed that zip code to be affluent.

We have plotted our 8025 points both separately and on the map of New York City to verify that the distribution of the data we pulled is well balanced.

We have realized early on in our process that using only the $ system might be not enough in order to assess the affluence of a neighborhood, and we have used our knowledge of New York City to engineer several new features that were specific to New York City. We have created a feature that aggregates the total number of businesses in a zip code ("count"). We have used K-means to cluster the city into 8 clusters ("clusters") - a feature that tells us if a zip code has a Trader Joe grocery store in it  ("has_tj"), and a feature that tells us of a zip code has an Equinox gym in it (has_equinox). Whenever possible - local knowledge should be employed in order to improve the features used - and our reasoning was based on knowing the city - and knowing that areas where an Equinox gym is present are more affluent. We used the same reasoning when it came to Trader Joe. At the same time, we decided to keep the city category assigned by Yelp to each specific business in out final features.

## Provided Data


 - [IRS Website](https://www.irs.gov/statistics/soi-tax-stats-individual-income-tax-statistics-2017-zip-code-data-soi)
 - [Yelp API](https://www.yelp.com/developers/documentation/v3/business_search)


##  Data Dictionary


|Feature|Type|Description|
|---|---|---|
|**State**|*object*|State|
|**City**|*object*|City|
|**Zip Codes**|*int*|Zip Code |
|**Latitude**|*float*|Latitude |
|**Longitude**|*float*|Longitude|
|**ID**|*object*|Unique ID of each Data point|
|**Name**|*object*|Store/Restaurant Name|
|**Review Count**|*int*|Number of reviews
|**Categories**|*object*|Category of each point|
|**Rating**|*float*|Average rating of each point|
|**Price**|*int*|Amount of $ signs of each point|
|**High Value**|*float*|Average Adjusted Gross Income of people who made over $200,000 per Zip Code|
|**AGI Sum**|*float*|Sum of the Total Average Income per threshold per Zip Code|
|**Aff Perc**|*float*|Rate of Affluency per Zip Code (High Value /AGI Sum)|
|**Count**|*int*|Count of Restaurants in particular Zip Code|


## Conclusion and Next Steps:
We were tasked to asses if the $ Yelp classification would indicate the affluence of an area. Our conclusion is that the yelp $ price is not a very important feature when we try to asses the affluence of an area in New York City. In our opinion, the most important feature that we have observed was the neighborhood itself - and its location in the whole New York City. That is obvious from the fact that 'clusters' - our engineered feature based on 8 locations in New York City - is the second most important, after the "New York" feature - in predicting affluency.

We notice that the presence of a good grocery store - such as Trader Joes, which we have used in our model - is also a relatively good feature in predicting of how affluent a zone is.

The number of reviews a business has is also showing higher importance than the ' $ price' - and interestingly enough - another one of our engineered features performs way better then the 'price' one at predicting affluence - namely - "count" - which is the number of businesses per zip code. It makes sense that more affluent areas have more businesses, and the also have a better exposure to customers, and therefore would have more reviews.

An interesting finding was that the zip codes of New York City with under 109 businesses tend to be the least affluent ones in the city as shown in our decision tree analysis. This is an extremely important finding - as a model such as this, adjusted for various USA cities, could indicate needier areas in cases of natural disasters. In conclusion, our model, although not preforming with the price feature as a key feature as it would have been expected, can still be used by engineering features like the ones we designed, customized to each specific city, to predict the least affluent regions and therefore be used in extreme situations to deploy help where the most needed.

As a general conclusion, location and the engineered features were better predictors than the yelp $ price - so we would recommend out client to aggregate more data in order to asses the affluence of a specific region with more accuracy. Yelp $ price alone is not enough.

A caveat to our results - we have used this model only on New York City - and this model would perform differently on other cities.

A further step would be to apply this model to other densely populated cities of United States, and to smaller ones as well, and compare the results.  It would be interesting to explore the differences needed in models used for densely populated areas, and the sparsely populated ones, and explore those differences.
