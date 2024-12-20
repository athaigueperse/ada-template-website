# Selective Sips: Cultural and bias trends in beer preferences across countries
## _by DataPilots_

## <a id="introduction"></a> Introduction
### Goal of the analysis
Taste preferences for food and drinks often go beyond the intrinsic characteristics of the items themselves and are in reality shaped by various external influences. Cultural differences are a prime example: while highly spiced dishes are popular in many South Asian countries, milder flavors are often preferred in Western Europe. Our project examined similar external factors that shape beer preferences, aiming to uncover what truly drives an individual’s taste in beers. We analyzed how different beer characteristics are appreciated across selected countries and assessed whether users from certain countries are more generous in their ratings compared to users from other countries. We also evaluateed whether the origin of a beer biases the ratings it receives. Additionally, we investigated how seasonal variations impact the enjoyment of specific beer categories, and how user rating tendencies evolve as they gain experience. By identifying these “external” influences, we hoped to help beer enthusiasts better understand their preferences and make choices based more on intrinsic qualities, ultimately improving their sensory experience and enjoyment of beer.

### Dataset
The dataset for our analysis comprised beer reviews collected from two popular beer rating platforms, BeerAdvocate and RateBeer, covering a period from 2001 to 2017. For each website, the dataset included metadata on reviewers, beers, and breweries, along with detailed user reviews. In total, there were records of over 500,000 unique beers produced by breweries in more than 200 countries. Among the most frequently reviewed beer styles were American IPA and India Pale Ale. The dataset also included approximately 200,000 users from over 200 countries, though the distribution of users and breweries was heavily skewed: the vast majority were located in the United States on both platforms. Overall, the dataset contained over 8 million reviews from BeerAdvocate and 7 million from RateBeer. For the parts of our analysis that involved country comparisons, we excluded reviews from countries with fewer than 50 reviewers to ensure that the data was representative at a national level.

## <a id="Cultural_influence_on_beer_preferences"></a> Cultural influence on beer preferences
We decided to start our analysis by investigating how the origin of reviewers influences their appreciation of beers. Specifically, we aimed to explore the cultural impact on beer appreciation by investigating qualitative aspects, such as beer style preferences across countries, and quantitative aspects, such as the significance of various beer attributes in influencing the final rating across different regions.

### Beer style preferences
_How do beer style preferences differ between countries, and are these regional preferences stable over time?_

In this part, we examine how different beer styles are reviewed across different countries. 

- In our analysis, we approached features in two scopes: first, we started with the number of ratings of certain beer styles as features of a given country to determine if certain countries cluster together in terms of beer style preferences. Secondly, we added average ratings of each beer style from each country as an additional feature to our previous data and then reduced this fourth dimensional dataframe to third dimensional one via merging these two features. Our initial analysis in P2 showed that we should group together the countries according to their actual regions since clustering dependent on Euclidean distances between these points. Then, we used principal component analysis to reduce 3D data into 2D mapping and via unsupervised clustering algorithm (K-means), we clustered the data. An optimal number of clusters were chosen according to Silhouette and Inertia scores(Elbow Method) to find a consistent one based on these two decision makers. After this step, regions were plotted with the PCA loadings. However, we cannot directly understand the regional beer preferences using PCA loadings; therefore, in each region,  we found the top 5 beer styles and plotted them as multiple bar plots. 

- In the second part, we used the time information in reviews to determine if regional beer style preferences, which were found in the previous part, remain stable over time — supporting the hypothesis that they are influenced by culture — or if they fluctuate, suggesting other contributing factors.

Starting from P2, we made inital analyses and showed the results below which also helped that detecting the core problems and how we could proceed to find the regional preferences.

![Wordcloud plot](plots/beer_style_preferences_plot3.png)

![plots1](plots/beer_style_preferences_plot1_2.png)

The word cloud maps and histograms show that the distribution of ratings of popular beer brands and styles across the world based on BeerAdvocate and RateBeer data. In the left chart, the most-rated beer brand, "St. Bernardus Abt 12," received over 8,000 ratings, followed closely by "Guinness Draught" and other popular brands that have between 5,000 and 8,000 ratings. This partially indicates that there is almost an uniform distribution among the well-known brands. 

On the other hand, the right chart reveals that specific beer styles dominate in popularity. "American IPA" leads with over 550,000 ratings, followed by "India Pale Ale (IPA)" at around 500,000 ratings. Other styles like "Imperial Stout" and "Pale Ale" also feature prominently, with over 200,000 ratings each.


![plots3](plots/beer_style_preferences_plot4.png)

![plots5](plots/beer_style_preferences_plot5.png)

![plots6](plots/beer_style_preferences_plot6.png)

![plots7](plots/beer_style_preferences_plot7.png)

![plots8](plots/beer_style_preferences_plot8.png)

![plots9](plots/beer_style_preferences_plot9.png)

![plots10](plots/beer_style_preferences_plot10.png)

![plots11](plots/beer_style_preferences_plot11.png)



### Importance of specific beer attributes
_Does the significance of specific beer attributes in determining one’s liking of a given beer vary by country?_

TO DO

## <a id="Location_related_biases_in_ratings"></a> Location-related biases in ratings
After exploring how beer preferences differ across countries, we aimed to identify factors—beyond the intrinsic qualities of beer—that might influence user ratings. Our initial focus was on location-related biases, as these seemed the most likely to impact beer ratings.

### Cultural biases
_Are users from certain countries more generous or more critical in their ratings compared to users from other countries?_

Our first step was to investigate whether users from certain countries are more generous or more critical in their ratings compared to users from other countries. 

#### **Logistic regression**
To this aim, we started by fitting a logistic regression model on a sample (due to the significant size of the dataset) of reviews from BeerAdvocate and RateBeer,where the dependent variable was the reviewer’s country, and the independent variables were potentially relevant confounders, namely the average rating for the beer style, the brewery's average rating and the number of reviews given by the user. The model gave a propensity score to each review, which corresponded to the likelihood of a review being associated with a particular country given the confounders.
 
We used these propensity scores to match individual reviews from reviewers in one country with reviews from reviewers in another country that have similar propensity scores. This matching ensured that the paired reviews were comparable in terms of confounders, so that any differences in ratings could be attributable to the reviewer’s country rather than other factors. 

#### **Paired analysis**
To be able to determine whether users from certain countries are more generous or more critical in their ratings compared to users from other countries, we compared paired rating differences between all pairs of user location. To do so, we grouped the matched reviews by country pairs and performed a paired t-test for each group to test whether the mean difference in ratings was significantly different from zero. We only considered country pairs with at least 20 matched reviews. We then plotted the obtained p_values for each country pair to see if there were some significant differences in final beer ratings for some country pairs at a 5% significance level. The results are shown in the plot below.

![P value plot](plots/cultural_bias_plot_1.png)

As shown by the small number of data points in the plot, few country pairs had enough matches to be included in the analysis.

The colored dots below the y=0.05 line indicate that there were some country pairs for which there was a significant difference in final rating at a 5% significance level.For instance, we can see in the plot that after accounting for confounders, users from Filand tend to give ratings that are significantly lower than users from the Puerto Rico from a statistical standpoint. On the other hand, users from Russia tend to give ratings that are significantly higher than users from Wales from a statistical standpoint. These results suggested that users from certain regions tend to be more generous or more critical in their ratings compared to users from other countries.

In this way, some of the differences were statistically significant. However, statisticals significance does not imply practical significance. In order to determine if these differences were also meaningful from a practical standpoint, we decided to look at their magnitude. We plotted a boxplot to visualize the distribution of differences in final beer rating between matched reviews for the 10 country pairs for which the t-test yielded the lowest p-values. We obtained the figure below.

![rating difference boxplot](plots/cultural_bias_plot_2.png)

In the plot, few boxes contain zero (zero is not comprised between Q1 and Q3), which indicates that for most of the top 10 country pairs with the lowest p-values, ratings from one country are consistently higher or lower than those from the other country for most paired reviews in the sample. This implies that the majority of matched reviews for most of of these country pairs show a meaningful and unidirectional difference in ratings. In addition, the median for some country pairs is larger than 1 in absolute value. A difference of 1 out of 5 is large, which means that for these country pairs, the differences in ratings are not only statistically significant but also meaningful from a practical standpoint.

### **Conclusion cultural bias**
These results suggested that, after accounting for potential confounders, users from certain countries appear more generous in their ratings compared to users from other countries. There seemed to be clear trends in rating differences for certain country pairs, and the differences in ratings appeared significant from both a statistical and practical standpoint for these pairs. These findings align with the hypothesis that a "cultural bias" might influence beer reviewers, potentially impacting beer ratings.

However, the matching process did not yield sufficient matches for all countries, which restricted our ability to make meaningful comparisons across a broader range of country pairs. In addition, a significant bias was only observed for some specific country pairs, meaning the results did not support the conclusion that this bias is a general or universal phenomenon. These observations highlighted the need for further investigation to clarify the role of cultural biases in beer ratings.


### Beer origin bias
_Do users show a bias by rating domestic beers higher than foreign ones?_
In countries with strong beer traditions, local beers often carry national pride. This phenomenon led us to think that the origin of a beer may bias beer ratings, with users rate domestic beers more favourably than foreign ones. This consideration motivated us to investigate whether users rate domestic beers higher than foreign ones.

#### **Matched analysis**
To achieve this, we began by labeling each review as either domestic (reviewing a beer produced in the reviewer’s country) or foreign. Next, we matched domestic and foreign beer reviews written by the same user. To control for the influence of beer style on ratings, we ensured that matched reviews were for the same beer style.

We subsequently performed a paired t-test to determine whether the mean difference in ratings between matched reviews was significantly different from zero. The test yielded an extremely small p-value, suggesting that the mean difference in final rating between matched domestic and foreign reviews was significantly different from zero. Moreover, the test statistic was negative. This result contradicted our initial hypothesis, as it implied that on average, domestic reviews were associated with _lower_ ratings than matched foreign reviews. 

Before drawing any conclusions, we plotted a histogram of rating differences between matched reviews to examine their distribution and magnitude, allowing us to evaluate their practical significance. The obtained figure is shown below.

![domestic foreign diff histogram](plots/beer_origin_bias_plot1.png)

As shown in the plot, the distribution of rating differences between matched domestic and foreign reviews was approximately symmetrical and centered around zero. The distribution was bell-shaped, with fewer data points with a rating difference farther from zero, and nearly no data points with a rating difference larger than 2. This implied that there was no clear trend in rating differences between matched domestic and foreign reviews. Additionaly, the mean rating difference between matched reviews was very small (-0.03). In this way, the difference between ratings of matched domestic and foreign reviews did not appear to be significant from a practical standpoint. We reasoned that the statistical significance identified by the t-test might be attributed to the large number of matched reviews, which can make even minor differences appear statistically significant.

We then decided to examine the distribution of rating differences between matched reviews for different countries separately to determine if certain countries exhibited a bias that was not apparent when analyzing all countries combined. We looked at the 10 countries with the highest mean difference between matched reviews among the countries with matched reviews from at least 100 different reviewers to ensure results were representative. We obtained the following boxplots:

![top 10 countries boxplot](plots/beer_origin_bias_plot2.png)

As shown in the plot, even for the 10 countries with the highest mean rating difference between matched reviews, the distribution of rating differences was centered around zero. For each of these 10 countries, the whiskers and outliers (circles) showed a roughly balanced number of positive and negative extreme values, suggesting that there was no strong skew in the rating differences. These results showed that even when looking at individual countries, there did not seem to be a particular rating bias related to whether the reviewed beer was from the same country or a different country than the reviewer.

We then decided to focus only on matched reviews from beer enthusiasts, which correspond to users who wrote a significant number of reviews. Intuitively, we expecteded beer enthusiasts to be less sensitive to factors that are not related to the instrinsic qualities of a beer. Hence, we did not expect differences between pairs of matched reviews to be significant, especially since we had observed that these differences were not practically significant when looking at all reviewers together. In our analysis, we considered that a beer enthusiast was a reviewer who had written at least 50 reviews. 

We performed the same analysis, starting with a t-test to compare ratings between matched domestic and foreign reviews from beer enthusiasts. Once again, we obtained a very small p-value and a counter-intuitive negative test statistic, prompting us to plot a histogram of rating differences between matched reviews to better understand their distribution and magnitude. We obtained a very similar histogram to the one obtained when looking at all users:

![domestic foreign diff histogram enthusiasts](plots/beer_origin_bias_plot3.png)

The distribution was again bell-shaped, approximately symmetrical and centered around zero, with a very small mean value. This implied that there was no evident pattern in the rating differences between matched domestic and foreign reviews from beer enthusiasts. The data thus appeared consistent with our hypothesis that beer enthusiasts are not influenced by the origin of beers in their ratings.

We also visualized the distribution of rating differences between matched reviews from beer enthusiasts for different countries separately, adopting the same approach as for the analysis on all reviewers. As shown below, we obtained a very similar plot, suggesting that even when analyzing individual countries, there did not seem to be clear evidence of a rating bias among beer enthusiasts based on whether the beer being reviewed is domestic or foreign.

![top 10 countries boxplot enthusiasts](plots/beer_origin_bias_plot4.png)


#### **Conclusion beer origin bias**
These results indicate that a beer's status as domestic or foreign to the user does not appear to influence their ratings. This was expected for beer enthusiasts, but our findings suggested that this holds true when considering all users together.


## <a id="Other_biases"></a> Other biases
After examining cultural and origin-based biases in beer ratings, we turned our attention to other external factors unrelated to location. Using the time data available in reviews, we analyzed two such factors: the season during which the beer was reviewed and the user’s experience level.

### Seasonal biases
_Do seasonal changes affect how different beer styles are rated?_

We first decided to investigate how seasonal changes influence beer ratings, as we thought preferences for certain beer styles or flavors may vary with seasonal trends, such as lighter beers being favored in summer and darker, richer beers in winter. We started by using the time information contained in ratings to identify the season during which each rating was posted, taking into account the location of the user (Northern hemisphere, Southern hemisphere or equatorial area) to accurately determine the season. For simplicity, we only performed the analysis on users from the 10 countries with the highest number of reviews. 

We first performed a linear regression analysis with the final rating as the dependent variable and key predictors, namely season, average rating for the beer style, average rating for the brewery, user’s average rating, ABV, an attribute ratings as the independent variables. We examined the regression coefficients for the season variable to see whether ratings were significantly higher or lower in certain seasons after accounting for confounders. Using these coefficients, we then calculated predicted ratings for each beer style in each season and visualized the results with line charts, showing seasonal trends for different beer styles. This approach allowed us to compare ratings between seasons while accounting for potential confounders (included as independent variables).

#### **Regression analysis**
For the Linear regression model, we used the variables below: 

- **Dependent variable**: Final Beer Rating  
- **Independent variables**:  
   - Season (Spring, Summer, Winter)  
   - ABV (Alcohol By Volume)  
   - User's Average Rating  
   - Brewery's Average Rating  
   - Style's Average Rating
   - Appearance
   - Aroma
   - Palate
   - Taste

We trained our linear regression model and had a R2 of 0.9704, showing that the model explained most of the variability in the data. The MSE was low (0.01442), indicating that the model's predictions were very close to the true values. We concluded that our model seemed good enough to work with predictions later in the analysis.

Below are the obtained regression coefficients (note that we performed one-hot encoding of the season variable and dropped one of the columns to avoid introduing colinearity; this explains the fact that there were only 3 season coefficients):

| **Feature**          | **Coefficient** | **p-value**  |
|----------------------|-------------|------------------|
| abv            | 0.002226    | 0.000000e+00     |
| user_avg_rating| -0.000319   | 1.289318e-07     |
| brewery_avg_rating | 0.015163 | 0.000000e+00    |
| style_avg_rating| -0.001109  | 5.017367e-42     |
| appearance    | 0.076178    | 0.000000e+00     |
| aroma          | 0.209587    | 0.000000e+00     |
| palate        | 0.115837    | 0.000000e+00     |
| taste         | 0.348882    | 0.000000e+00     |
| season_Spring  | -0.000281   | 9.979510e-07     |
| season_Summer | -0.000373   | 6.309549e-11     |
| season_Winter | -0.000328   | 1.052942e-08     |

As shown in the above table, p-values of all coefficients were extremely small, indicating that all the independent variables included in the model were useful in explaining variations in ratings at a 5% significance level. The standardization of features performed before the regression enabled us to compare coefficients. This allowed us to infer that attribute ratings appeared to have the strongest influence on the final rating given that they were associated with the largest coefficients. On the other hand, the 3 season coefficients were much smaller than the other coefficients. This suggested that though season appeared to have a statistically significant impact on beer ratings, it did not seem to be the dominant factor driving rating behavior. Other factors, such as attribute ratings and the brewery average rating, appeared to play a much larger role.

#### **Average predicted ratings across seasons**
Using the regression coefficients, we calculated predicted ratings for each beer style in spring, summer and winter. The average predicted ratings across beer styles are shown in the plot below.

![Seasonal bias plots](plots/seasonal5.png)

The bars all have approximately the same height and confidence intervals overlap, indicating that average predicted ratings do not vary significantly across seasons for all beer styles combined. These results were expected from the small values of the season coefficients in the linear regression model.

#### **Seasonal variations in ratings for different beer styles**
To visualize the variations of predicted average rating across seasons for different beer styles, we plotted a heatmap, which is shown below.

![Seasonal bias plots](plots/seasonal2.png)

Most beer styles showed no visible color variations accross seasons, suggesting that the average predicted rating for most beer styles did not vary significantly across seasons. Again, this was expected from the very small regression coefficients for the season variable.

For a more fine-grained analysis, we decided to look at the seasonal variations of several subsets of beer styles. First, we considered the 10 beer styles with the highest and the lowest average predicted rating by the model.

![Seasonal bias plots](plots/seasonal3.png)

![Seasonal bias plots](plots/seasonal4.png)

The flat lines in the two plots above indicated that there was no noticeable variation across seasons for both top-rated and poorly-rated beer styles. These results suggested again that seasons did not seem to be an important factor in determining final beer ratings.
 

#### **Conclusion seasonal biases**
Our analysis suggested that seasonal variations do not appear to have a practically significant impact on beer ratings. Other factors, such as attribute ratings and user and brewery average ratings seem to play a much larger role in determining beer ratings.


### Experience bias
_Do users become more critical with experience?_

The last part of our analysis consisted in assessing the influence of user experience on beer ratings. It is well known that taste develops and refines over time. A good example is wine palate evolution: many young people initially dislike wine or prefer cheaper varieties, but they progressively develop a preference for older, high-quality wines as they age. We decided to investigate whether this phenomenon of palate refinement also occurs in beer ethusiasts. 

For this analysis, we decided to focus on users who posted a substantial number of reviews, based on a chosen threshold, and worked on the BeerAdvocate and RateBeer datasets separately. We started by sorting the reviews from each selected user chronologically and assigning an "experience level" to each review based on the number of reviews the user had posted up to that point. These levels were predefined and consistent across all users: new reviewer (first n reviews), amateur (from the n+1th to the oth review), and expert (from the o+1th review onward). 

#### **Linear regression**
To compare rating tendencies across all users, we fitted a linear regression model on ratings to quantify the effect of experience levels on ratings while adjusting for potential confounders. The dependent variable was the final rating of the beer, and the key independent variable was the experience level of the user when they wrote the review. We also included additional independent variables corresponding to potential confounders, namely the average rating for the corresponding beer style, the average rating for the corresponding brewery and the average rating for the corresponding user. We then analyzed the regression coefficients, which are shown in the plots below.

![regression coefs BA](plots/experience_bias_plot1.png)

![regression coefs RB](plots/experience_bias_plot2.png)

In both plots, each bar corresponds to a regression coefficient:
- x1: average rating for the beer style
- x2: average rating given by the user
- x3: average rating for beers of the brewery
- x4: expert experience level
- x5: new reviewer experience level.

In both cases (BeerAdvocate and RateBeer), the p-values of all coefficients, including those corresponding to user experience levels (x4 and x5) were extremely small, implying that the chosen features were useful in explaining variations in the final rating. As shown in the plots, the coefficients corresponding to user experience levels were much smaller than the other coefficients, meaning that though they were useful in explaining variations in the final rating, they had a much smaller effect on the final rating than the average rating of the beer style, the average rating of the brewery and average rating given by the user. In both cases, the coefficient corresponding to the expert experience level (x4) was negative, implying that being an expert reviewer is associated with lower final ratings. On the other hand, in both cases, the coefficient corresponding to the new reviewer experience level (x5) was positive, implying that being a new reviewer is associated with higher final ratings.

In this way, the linear regression analysis on both datasets suggested that user experience levels significantly influence the final rating, as indicated by their small p-values. However, their effect size appeared to be smaller compared to factors like beer style, brewery average rating, and user average rating. The results seemed to indicate that new reviewers are more generous, while expert reviewers are more critical, leading to lower ratings, but that the overall influence of experience level on the final rating was relatively subtle.

#### **Paired analysis**
We then decided to examine how ratings change within *individual* users  as they gain experience. To achieve this, we performed a paired analysis by matching reviews labeled as “new reviewer” and “expert” within each user. Comparing reviews from the same user allowed us to control for confounding factors related to user-specific characteristics. To further isolate the effect of experience on ratings, we also matched reviews based on beer style and brewery, as we thought they might be confounders. We then performed a one-tailed paired t-test to determine if ratings given by a user when they are a new reviewer are higher than those they give when they are an expert, as suggested by the previous results.

The one-tailed paired t-tests performed on both datasets yielded a positive test statistic and a very small p-value. This indicated that on average, the final rating given by a specific user to beers from the same brewery and with the same style is higher when the user is a new reviewer than when they have become an expert reviewer. These findings aligned with the results of the linear regression, which suggested that new reviewers are more generous, while expert reviewers are more critical.

The t-tests allowed us to evaluate the statistical significance of the mean difference in ratings between matched reviews. However, as explained in the part examining cultural biases in ratings, statisticals significance does not imply practical significance. In order to determine if the differences in ratings between matched reviews were also meaningful from a practical standpoint, we decided to plot a boxplot to get a better idea of their magnitude and distribution. We obtained the figure below. Differences within pairs of reviews were calculated as the rating of the review corresponding to an "expert" experience level minus the rating of the review corresponding to a "new reviewer" experience level.

![experience levels boxplot](plots/experience_bias_plot3.png)

As shown in the plot, for both datasets, the mean difference was negative but very small and close to zero. In addition, there were many paired reviews where the expert review was associated with a much lower final rating than the paired new reviewer review, as shown by the numerous data points with a large negative value for the difference. However, there were also some cases where the expert review had a much higher rating than the paired new reviewer review, leading to high positive values.

The t-tests that we had performed had detected a statistically significant difference, showing that new reviewers tend to give slightly higher ratings than expert reviewers on average. The boxplots showed that the mean difference in final rating between matched reviews was actually close to zero in practical terms, with many extreme positive and negative differences balancing each other out. They revealed the high variability and the presence of outliers in rating differences between matched reviews, which are aspects that were not captured by the t-tests. 

These results illustrated the difference between statistical and practical significance: while the t-tests demonstrated a statistically significant difference (probably because of the large sample size, which could make even small differences statistically significant), the actual effect size (difference in final ratings between matched reviews) was small and not practically meaningful. New reviewers appear to be slightly more generous than experts on average, but the difference is minimal and likely negligible in practical terms.

#### **Conclusion experience bias**
Both the linear regression and the paired analysis found that user experience level influences ratings, with more experienced users being slightly more critical. However, the effect appeared statistically significant but numerically small, suggesting that experience level has a minor impact on ratings compared to other factors like beer style, brewery reputation, and user generosity.


## <a id="conclusion"></a> Conclusion
Content of the conclusion
