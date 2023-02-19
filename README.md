# Recipe User-Interaction Analysis
### By: Jessica Hung, Samantha Lin

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
		`'calories', 'total fat', 'sugar', 'sodium', 'protein', 'saturated fat', 'carbohydrate'`, each in the type `float`.

`print(counts[['Quarter', 'Count']].head().to_markdown(index=False))`



## Assessment of Missingness


## Hypothesis Testing