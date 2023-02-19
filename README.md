# Recipe User-Interaction Analysis
### By: Jessica Hung, Samantha Lin


### Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}


Who doesn't love cooking?

When people search for recipes online and skims through the pages for each one, it is natural for one to pay extra attention on the amount of time needed to complete the dish and how well this recipe has been rated by previous users. 

Our project tries to analyze the relationship between the time (in minutes) a recipe takes and its corresponding rating and answer the question:

***What is the relationship between the cooking time and average rating of recipes?***

Perhaps a longer recipe will receive lower rating because as one completes the recipe that takes a super long time, and realized the outcome is not as "wow" as expected, then the user may be more likely to leave a low rating. While at the same time, a recipe that takes less time may be less sophisticated in developing flavors and presentation, hence the rating for these recipes may be lower. Which one is more intuitive for you?


## Cleaning and EDA
### Data Cleaning
In the data cleaning process, we:
1. Left merged the `RAW_recipes.csv` with `RAW_interactions.csv` to generate a new dataframe that contains recipes and reviews from `RAW_interactions.csv` that only have a match id in the `RAW_recipes.csv`.
2. Replaced all rating `0` with `np.NaN` as a `0` rating essentially means the user did not leave a rating for the recipe they used.
3. Calculated the average rating for each recipe and assigned this new series as a new column of the dataframe.
4. Splitted the `nutrition` column into 7 new columns: 
		`'calories'`, `'total fat'`, `'sugar'`, '`sodium'`, `'protein'`, `'saturated fat'`, `'carbohydrate'`, each in the type `float`.


### Univariate Analysis Plot 1 - Distribution of `minutes`
For this plot, we intend to plot the distribution of the `minutes` column in the dataframe. As we performed the plotting directly, this is the resulting plot: 

<iframe src="assets/count-minutes-with-extremes.html" width=800 height=600 frameBorder=0></iframe>

As one can see, the distribution is extremely skewed to the right because of extreme outliers.

Due to the lack of clarity of this plot, we decided to remove the top 5 outliers using the threshold of 100000 minutes. This is the resulting plot:

<iframe src="assets/count-minutes-without-extremes.html" width=800 height=600 frameBorder=0></iframe>

This newly generated plot is still very right-skewed, hence we decided to use the interquartile quartertile range (IQR) of the data to determine the outliers defined as follows:

Recipes with 
1. `minutes` < 25th quartile - 1.5 * IQR or 
2. `minutes` > 75th quartile + 1.5 * IQR

The final distribution of `minutes` we have is:

<iframe src="assets/count-minutes-without-outliers.html" width=800 height=600 frameBorder=0></iframe>

This final plot is the clearest among all three, but we can observe spikes on `minutes` that are ending in 0s and 5s. We believe this is the result of recipe contributors' habits and convention of rounding their recipes' time to the nearest 10s or 5s. 


### Univariate Analysis Plot 1 - Distribution of `rating_original`
We decided to plot the distirbution of `rating_original` in the dataframe.

<iframe src="assets/rating-distribution.html" width=800 height=600 frameBorder=0></iframe>

We can see that the `rating_original` is left-skewed and there is no value at 0. This is because we have replaced all `0` ratings at the data cleaning process.


## Assessment of Missingness


## Hypothesis Testing