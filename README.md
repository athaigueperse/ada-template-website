# Selective sips: cultural and bias trends in beer preferences across countries
## _by DataPilots_

## <a id="introduction"></a> Introduction
### Goal of the analysis
Taste preferences for food and drinks often go beyond the intrinsic characteristics of the items themselves and are in reality shaped by various external influences. Cultural differences are a prime example: while highly spiced dishes are popular in many South Asian countries, milder flavors are often preferred in Western Europe. This project examines similar external factors that shape beer preferences, aiming to uncover what truly drives an individual’s taste in beers. We analyze how different beer characteristics are appreciated across selected countries and assess whether the origin of a beer biases the ratings it receives. Additionally, we investigate how seasonal variations and user experience impact the enjoyment of specific beer categories. By identifying these “external” influences, we hope to help beer enthusiasts better understand their preferences and make choices based more on intrinsic qualities, ultimately improving their sensory experience and enjoyment of beer.

### Dataset
The dataset for this analysis comprises beer reviews collected from two popular beer rating platforms, BeerAdvocate and RateBeer, covering a period from 2001 to 2017. For each website, the dataset includes metadata on reviewers, beers, and breweries, along with detailed user reviews. In total, there are records of over 500,000 unique beers produced by breweries in more than 200 countries. Among the most frequently reviewed beer styles are American IPA and India Pale Ale. The dataset also includes approximately 200,000 users from over 200 countries, though the distribution of users and breweries is heavily skewed: the vast majority are located in the United States on both platforms. Overall, the dataset contains over 8 million reviews from BeerAdvocate and 7 million from RateBeer. For the parts of our analysis that involve country comparisons, we excluded reviews from countries with fewer than 50 reviewers to ensure that the data is representative at a national level.

## <a id="analysis"></a> Analysis
Content of the analysis

### Seasonal biases
In this part, we will examine how seasonal changes may influence beer ratings. To do so, we will use the time information to determine the season during which each rating was posted. This task may be complex as some countries are in the Northern hemisphere and others are in the Southern hemisphere, and some may be located close to the Equator and may thus not even experience seasons! We will simplify things by only considering reviews from the 10 countries with the most reviews. We will determine whether they are in the Northern or Southern hemisphere and use the time information in the reviews to determine the season during which each review was posted.

We will then group the ratings by season and calculate the average final rating within each group to see if some seasons are associated with higher ratings overall. We will then refine the analysis by calculating the average final rating for each beer style within each group, and compare these averages across different seasons to identify any notable variations.


### Experience biases
The last part of our analysis consisted in assessing the influence of user experience on beer ratings. It is well known that taste develops and refines over time. A good example is wine palate evolution: many young people initially dislike wine or prefer cheaper varieties, but they progressively develop a preference for older, high-quality wines as they age. We decided to investigate whether this phenomenon of palate refinement also occurs in beer ethusiasts. 

## <a id="conclusion"></a> Conclusion
Content of the conclusion
