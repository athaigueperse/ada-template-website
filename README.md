# Selective sips: cultural and bias trends in beer preferences across countries
## _by DataPilots_

## <a id="introduction"></a> Introduction
### Goal of the analysis
Taste preferences for food and drinks often go beyond the intrinsic characteristics of the items themselves and are in reality shaped by various external influences. Cultural differences are a prime example: while highly spiced dishes are popular in many South Asian countries, milder flavors are often preferred in Western Europe. Our project examined similar external factors that shape beer preferences, aiming to uncover what truly drives an individual’s taste in beers. We analyzed how different beer characteristics are appreciated across selected countries and assessed whether users from certain countries are more generous in their ratings compared to users from other countries. We also evaluateed whether the origin of a beer biases the ratings it receives. Additionally, we investigated how seasonal variations impact the enjoyment of specific beer categories, and how user rating tendencies evolve as they gain experience. By identifying these “external” influences, we hoped to help beer enthusiasts better understand their preferences and make choices based more on intrinsic qualities, ultimately improving their sensory experience and enjoyment of beer.

### Dataset
The dataset for our analysis comprised beer reviews collected from two popular beer rating platforms, BeerAdvocate and RateBeer, covering a period from 2001 to 2017. For each website, the dataset included metadata on reviewers, beers, and breweries, along with detailed user reviews. In total, there were records of over 500,000 unique beers produced by breweries in more than 200 countries. Among the most frequently reviewed beer styles were American IPA and India Pale Ale. The dataset also included approximately 200,000 users from over 200 countries, though the distribution of users and breweries was heavily skewed: the vast majority were located in the United States on both platforms. Overall, the dataset contained over 8 million reviews from BeerAdvocate and 7 million from RateBeer. For the parts of our analysis that involved country comparisons, we excluded reviews from countries with fewer than 50 reviewers to ensure that the data was representative at a national level.

## <a id="analysis"></a> Analysis
### Cultural influence on beer preferences
**Beer style preferences**
TO DO

**Importance of specific beer attributes**
TO DO

### Location-related biases in ratings
After exploring how beer preferences differ across countries, we aimed to identify factors—beyond the intrinsic qualities of beer—that might influence user ratings. Our initial focus was on location-related biases, as these seemed the most likely to impact beer ratings.

**Cultural biases**
Our first step was to investigate whether users from certain countries are more generous or more critical in their ratings compared to users from other countries. 

To this aim, we started by fitting a logistic regression model on reviews from BeerAdvocate and RateBeer (combined in a single dataset),where the dependent variable was the reviewer’s country, and the independent variables were potentially relevant confounders, namely the average rating for the beer style, the brewery's average rating and the number of reviews given by the user. The model gave a propensity score to each review, which corresponded to the likelihood of a review being associated with a particular country given the confounders.
 
We used these propensity scores to match individual reviews from reviewers in one country with reviews from reviewers in another country that have similar propensity scores. This matching ensured that the paired reviews were comparable in terms of confounders, so that any differences in ratings could be attributable to the reviewer’s country rather than other factors. 

To be able to determine whether users from certain countries are more generous or more critical in their ratings compared to users from other countries, we compared paired rating differences between all pairs of user location. To do so, we grouped the matched reviews by country pairs and performed a paired t-test for each group to test whether the mean difference in ratings was significantly different from zero. We only considered country pairs with at least 10 matched reviews. We then plotted the obtained p_values for each country pair to see if there were some significant differences in final beer ratings for some country pairs at a 5% significance level. The results are shown in the plot below.

![P value plot](images/cultural_biases_plot1.png)




**Beer origin bias**
TO DO

### Other biases
**Seasonal biases**
In this part, we will examine how seasonal changes may influence beer ratings. To do so, we will use the time information to determine the season during which each rating was posted. This task may be complex as some countries are in the Northern hemisphere and others are in the Southern hemisphere, and some may be located close to the Equator and may thus not even experience seasons! We will simplify things by only considering reviews from the 10 countries with the most reviews. We will determine whether they are in the Northern or Southern hemisphere and use the time information in the reviews to determine the season during which each review was posted.

We will then group the ratings by season and calculate the average final rating within each group to see if some seasons are associated with higher ratings overall. We will then refine the analysis by calculating the average final rating for each beer style within each group, and compare these averages across different seasons to identify any notable variations.

**Experience biais**
The last part of our analysis consisted in assessing the influence of user experience on beer ratings. It is well known that taste develops and refines over time. A good example is wine palate evolution: many young people initially dislike wine or prefer cheaper varieties, but they progressively develop a preference for older, high-quality wines as they age. We decided to investigate whether this phenomenon of palate refinement also occurs in beer ethusiasts. 

## <a id="conclusion"></a> Conclusion
Content of the conclusion