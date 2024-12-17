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

![P value plot](plots/cultural_biases_plot1.png)


**Beer origin bias**
TO DO

### Other biases

### Seasonal biases
In this part, we examined how seasonal changes may influence beer ratings. To do so, we used the time information to determine the season during which each rating was posted.  To analyze whether the season in which a beer is reviewed has a significant impact on its rating, we first performed linear regression to adjust for confounding factors. Secondly, we examined seasonal coefficients to determine statistical significance. Thirdly, we created visualizations to analyze predicted ratings for each beer style across seasons.

#### **Regression Analysis**

For the Linear Regression Model, we used the variables below: 

- **Dependent Variable**: Final Beer Rating  
- **Independent Variables**:  
   - Season (Spring, Summer, Winter)  
   - Beer Style (categorical interaction with season)  
   - ABV (Alcohol By Volume)  
   - User's Average Rating  
   - Brewery's Average Rating  
   - Style's Average Rating  

From the regression, we got the following coefficients for each variable: 

|**Feature**         | **Coefficient**|
|----------------------|-------------|
| abv                  | 0.074121     |
| user_avg_rating      | 0.137794     |
| brewery_avg_rating   | 0.275858     |
| style_avg_rating     | 0.123048     |
| season_Spring        | 0.001250     |
| season_Summer        | -0.003523    |
| season_Winter        | -0.000628    |


From the results, we found that the main predictors of beer ratings were the **Brewery Average Rating**, which had the strongest influence, followed by **User Average Rating** and **Style Average Rating**, which also had significant but smaller effects. The **ABV (Alcohol By Volume)** had a small but positive effect. On the other hand, the seasonal coefficients for **Spring (+0.0013)**, **Summer (-0.0035)**, and **Winter (-0.0006)** were very close to zero, showing that seasonal effects, while statistically significant, were minimal. Overall, we concluded that user and brewery averages were the biggest factors in beer ratings, while seasonal variations had almost no practical impact.


#### **Predicted ratings across seasons**

Using the regression coefficients, we calculated predicted ratings for each beer style in Spring, Summer, and Winter. The average predicted ratings were as follows:

| **Season** | **Average Predicted Rating** |
|------------|-----------------------------|
| Spring     | 4.058                       |
| Summer     | 4.054                       |
| Winter     | 4.057                       |


We concluded from the data that the average ratings remain consistent across seasons.
Seasonal changes have a negligible effect on the predicted ratings. The bar chart below illustrates the minimal difference in average ratings across Spring, Summer, and Winter.

![Seasonal bias plots](plots/seasonal5.png)

#### **Seasonal Trends by Beer Style**

To see the seasonal trends by beer style we plotted a heatmap for beer styles across seasons. 

In the heatmap below, we observe that most beer styles show little color variations across seasons. We understand that the predicted ratings for the beer styles are the same regardless of the season. The season has a small effect on the predicted ratings. We conclude that the seasonal changes have a small but statistically significant effect on predicted ratings.

![Seasonal bias plots](plots/seasonal2.png)


##### *Top 10 Beer Styles*

The line plot for the top-rated beer styles shows subtle fluctuations across seasons. Predicted ratings for styles like American Double/Imperial Stout and Quadruple (Quad) remain consistently high with minimal variation.

For example, we got ratings for American Double/Imperial Stout: 4.85 → 4.84 → 4.85 and for Gueuze: 4.78 → 4.78 → 4.78. Therefore, we conclude that for the highest-rated beer styles, ratings are consistent regardless of the season.

![Seasonal bias plots](plots/seasonal3.png)

##### *Bottom 10 Beer Styles*

The line plot for the lowest-rated beers (e.g., Light Lager, Pale Lager, and Malt Liquor) similarly shows minimal seasonal impact.

For example, we got ratings for beer style Light Lager: 3.29 → 3.28 → 3.29. 
We also confirm that seasonal bias is negligible across both highly rated and poorly rated beer styles.

![Seasonal bias plots](plots/seasonal4.png)

#### **Distribution of Seasonal Variation**

To understand the range of seasonal variations, we calculated the maximum-minimum difference for predicted ratings across seasons. We observed that most beer styles have a rating range of 0.004-0.005 which indicates very little variation across seasons. The histogram below shows a concentrated distribution, and we can see the negligible seasonal impact of season on beer preferences. Below there exists the histogram of distribution of seasonal variations. 

![Seasonal bias plots](plots/seasonal6.png)

In conclusion, we found that seasonal bias in beer ratings, while statistically significant, was practically negligible. The main factors that influenced beer ratings were user average ratings, brewery averages, and style averages, which had the biggest impact. Both top-rated and bottom-rated beer styles showed very little variation across seasons. Overall, we concluded that seasonality had no meaningful effect on beer ratings, as user behavior and brewery related factors played a much larger role in determining the beer ratings.

### Experience biases
The last part of our analysis consisted in assessing the influence of user experience on beer ratings. It is well known that taste develops and refines over time. A good example is wine palate evolution: many young people initially dislike wine or prefer cheaper varieties, but they progressively develop a preference for older, high-quality wines as they age. We decided to investigate whether this phenomenon of palate refinement also occurs in beer ethusiasts. 

## <a id="conclusion"></a> Conclusion
Content of the conclusion
