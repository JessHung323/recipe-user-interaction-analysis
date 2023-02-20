# Welcome to Recipe User-Interaction Analysis
## Let's explore more about recipes and their ratings!
{:.no_toc}

#### By: Jessica Hung, Samantha Lin
{:.no_toc}


---
### Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}
---

## **Introduction**
Who doesn't love cooking? 😆

When people search for recipes online and skim through the webpage for each one, it is natural for one to pay extra attention on the amount of time needed to complete the dish and how well this recipe has been rated by previous users because afterall, you want to make something that tastes good and is not a waste of your time. 

Our project tries to analyze the relationship between the time (in minutes) a recipe takes and its corresponding rating, and answer the question:

***What is the relationship between the cooking time and average rating of recipes?***

Perhaps a longer recipe will receive lower rating because as one completes the recipe that takes a super long time, and realizes the outcome is not as "wow" as expected, then the user may be more likely to leave a low rating. While at the same time, a recipe that takes less time may be less sophisticated in developing flavors and presentation, hence the rating for these recipes may also be lower. Which one is more intuitive for you?


## **Cleaning and EDA**
### **Data Cleaning**
In the data cleaning process, we:
1. Left merged the `RAW_recipes.csv` with `RAW_interactions.csv` to generate a new dataframe that contains recipes and reviews from `RAW_interactions.csv` that only have a match id in the `RAW_recipes.csv`.
2. Replaced all rating `0` with `np.NaN` as a `0` rating essentially means the user did not leave a rating for the recipe they used.
3. Calculated the average rating for each recipe and assigned this new series as a new column of the dataframe.
4. Splitted the `nutrition` column into 7 new columns: 
		`'calories'`, `'total fat'`, `'sugar'`, '`sodium'`, `'protein'`, `'saturated fat'`, `'carbohydrate'`, each in the type `float`.

<table border="1" class="dataframe">\n  <thead>\n    <tr style="text-align: right;">\n      <th>name</th>\n      <th>id</th>\n      <th>minutes</th>\n      <th>contributor_id</th>\n      <th>submitted</th>\n      <th>tags</th>\n      <th>nutrition</th>\n      <th>n_steps</th>\n      <th>steps</th>\n      <th>description</th>\n      <th>ingredients</th>\n      <th>n_ingredients</th>\n      <th>user_id</th>\n      <th>recipe_id</th>\n      <th>date</th>\n      <th>rating_original</th>\n      <th>review</th>\n      <th>rating_average</th>\n      <th>calories</th>\n      <th>total fat</th>\n      <th>sugar</th>\n      <th>sodium</th>\n      <th>protein</th>\n      <th>saturated fat</th>\n      <th>carbohydrate</th>\n    </tr>\n  </thead>\n  <tbody>\n    <tr>\n      <td>1 brownies in the world    best ever</td>\n      <td>333281</td>\n      <td>40.0</td>\n      <td>985201</td>\n      <td>2008-10-27</td>\n      <td>[\'60-minutes-or-less\', \'time-to-make\', \'course\', \'main-ingredient\', \'preparation\', \'for-large-groups\', \'desserts\', \'lunch\', \'snacks\', \'cookies-and-brownies\', \'chocolate\', \'bar-cookies\', \'brownies\', \'number-of-servings\']</td>\n      <td>138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0</td>\n      <td>10</td>\n      <td>[\'heat the oven to 350f and arrange the rack in the middle\', \'line an 8-by-8-inch glass baking dish with aluminum foil\', \'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted\', \'remove from heat and let cool to room temperature\', \'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated\', \'add cooled chocolate and mix until uniform in color\', \'add flour and stir until just incorporated\', \'transfer batter to the prepared baking dish\', \'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes\', \'remove from the oven and cool completely before cutting\']</td>\n      <td>these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you\'ll ever make.....sereiously! there\'s no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they\'re pure heaven!</td>\n      <td>[\'bittersweet chocolate\', \'unsalted butter\', \'eggs\', \'granulated sugar\', \'unsweetened cocoa powder\', \'vanilla extract\', \'brewed espresso\', \'kosher salt\', \'all-purpose flour\']</td>\n      <td>9</td>\n      <td>386585.0</td>\n      <td>333281.0</td>\n      <td>2008-11-19</td>\n      <td>4.0</td>\n      <td>These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.</td>\n      <td>4.0</td>\n      <td>138.4</td>\n      <td>10.0</td>\n      <td>50.0</td>\n      <td>3.0</td>\n      <td>3.0</td>\n      <td>19.0</td>\n      <td>6.0</td>\n    </tr>\n    <tr>\n      <td>1 in canada chocolate chip cookies</td>\n      <td>453467</td>\n      <td>45.0</td>\n      <td>1848091</td>\n      <td>2011-04-11</td>\n      <td>[\'60-minutes-or-less\', \'time-to-make\', \'cuisine\', \'preparation\', \'north-american\', \'for-large-groups\', \'canadian\', \'british-columbian\', \'number-of-servings\']</td>\n      <td>595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0</td>\n      <td>12</td>\n      <td>[\'pre-heat oven the 350 degrees f\', \'in a mixing bowl , sift together the flours and baking powder\', \'set aside\', \'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy\', \'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined\', \'add in the flour mixture to the wet ingredients and blend until combined\', \'scrape down the sides of the bowl and add the chocolate chips\', \'mix until combined\', \'scrape down the sides to the bowl again\', \'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking\', \'bake for 10 - 15 minutes or until golden brown on the outside and soft &amp; chewy in the center\', \'serve hot and enjoy !\']</td>\n      <td>this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don\'t have margarine or don\'t like it, then just use butter (softened) instead.</td>\n      <td>[\'white sugar\', \'brown sugar\', \'salt\', \'margarine\', \'eggs\', \'vanilla\', \'water\', \'all-purpose flour\', \'whole wheat flour\', \'baking soda\', \'chocolate chips\']</td>\n      <td>11</td>\n      <td>424680.0</td>\n      <td>453467.0</td>\n      <td>2012-01-26</td>\n      <td>5.0</td>\n      <td>Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, &amp; I made the whole batch &amp; used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe!</td>\n      <td>5.0</td>\n      <td>595.1</td>\n      <td>46.0</td>\n      <td>211.0</td>\n      <td>22.0</td>\n      <td>13.0</td>\n      <td>51.0</td>\n      <td>26.0</td>\n    </tr>\n    <tr>\n      <td>412 broccoli casserole</td>\n      <td>306168</td>\n      <td>40.0</td>\n      <td>50969</td>\n      <td>2008-05-30</td>\n      <td>[\'60-minutes-or-less\', \'time-to-make\', \'course\', \'main-ingredient\', \'preparation\', \'side-dishes\', \'vegetables\', \'easy\', \'beginner-cook\', \'broccoli\']</td>\n      <td>194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0</td>\n      <td>6</td>\n      <td>[\'preheat oven to 350 degrees\', \'spray a 2 quart baking dish with cooking spray , set aside\', \'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce\', \'pour into baking dish , sprinkle remaining cheese over top\', \'bake for 25 minutes or until cheese is lightly browned\', \'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes\']</td>\n      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don\'t think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell\'s soup. but i think mine is better since i don\'t like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>\n      <td>[\'frozen broccoli cuts\', \'cream of chicken soup\', \'sharp cheddar cheese\', \'garlic powder\', \'ground black pepper\', \'salt\', \'milk\', \'soy sauce\', \'french-fried onions\']</td>\n      <td>9</td>\n      <td>29782.0</td>\n      <td>306168.0</td>\n      <td>2008-12-31</td>\n      <td>5.0</td>\n      <td>This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!  \\nThe photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.  \\nThanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family\'s favorite Zaar cookbook :)</td>\n      <td>5.0</td>\n      <td>194.8</td>\n      <td>20.0</td>\n      <td>6.0</td>\n      <td>32.0</td>\n      <td>22.0</td>\n      <td>36.0</td>\n      <td>3.0</td>\n    </tr>\n    <tr>\n      <td>412 broccoli casserole</td>\n      <td>306168</td>\n      <td>40.0</td>\n      <td>50969</td>\n      <td>2008-05-30</td>\n      <td>[\'60-minutes-or-less\', \'time-to-make\', \'course\', \'main-ingredient\', \'preparation\', \'side-dishes\', \'vegetables\', \'easy\', \'beginner-cook\', \'broccoli\']</td>\n      <td>194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0</td>\n      <td>6</td>\n      <td>[\'preheat oven to 350 degrees\', \'spray a 2 quart baking dish with cooking spray , set aside\', \'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce\', \'pour into baking dish , sprinkle remaining cheese over top\', \'bake for 25 minutes or until cheese is lightly browned\', \'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes\']</td>\n      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don\'t think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell\'s soup. but i think mine is better since i don\'t like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>\n      <td>[\'frozen broccoli cuts\', \'cream of chicken soup\', \'sharp cheddar cheese\', \'garlic powder\', \'ground black pepper\', \'salt\', \'milk\', \'soy sauce\', \'french-fried onions\']</td>\n      <td>9</td>\n      <td>1196280.0</td>\n      <td>306168.0</td>\n      <td>2009-04-13</td>\n      <td>5.0</td>\n      <td>I made this for my son\'s first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.</td>\n      <td>5.0</td>\n      <td>194.8</td>\n      <td>20.0</td>\n      <td>6.0</td>\n      <td>32.0</td>\n      <td>22.0</td>\n      <td>36.0</td>\n      <td>3.0</td>\n    </tr>\n    <tr>\n      <td>412 broccoli casserole</td>\n      <td>306168</td>\n      <td>40.0</td>\n      <td>50969</td>\n      <td>2008-05-30</td>\n      <td>[\'60-minutes-or-less\', \'time-to-make\', \'course\', \'main-ingredient\', \'preparation\', \'side-dishes\', \'vegetables\', \'easy\', \'beginner-cook\', \'broccoli\']</td>\n      <td>194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0</td>\n      <td>6</td>\n      <td>[\'preheat oven to 350 degrees\', \'spray a 2 quart baking dish with cooking spray , set aside\', \'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce\', \'pour into baking dish , sprinkle remaining cheese over top\', \'bake for 25 minutes or until cheese is lightly browned\', \'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes\']</td>\n      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don\'t think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell\'s soup. but i think mine is better since i don\'t like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>\n      <td>[\'frozen broccoli cuts\', \'cream of chicken soup\', \'sharp cheddar cheese\', \'garlic powder\', \'ground black pepper\', \'salt\', \'milk\', \'soy sauce\', \'french-fried onions\']</td>\n      <td>9</td>\n      <td>768828.0</td>\n      <td>306168.0</td>\n      <td>2013-08-02</td>\n      <td>5.0</td>\n      <td>Loved this.  Be sure to completely thaw the broccoli.  I didn&amp;#039;t and it didn&amp;#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.</td>\n      <td>5.0</td>\n      <td>194.8</td>\n      <td>20.0</td>\n      <td>6.0</td>\n      <td>32.0</td>\n      <td>22.0</td>\n      <td>36.0</td>\n      <td>3.0</td>\n    </tr>\n  </tbody>\n</table>


### ***Univariate Analysis***
#### **Plot 1 - Distribution of `minutes`**
For this plot, we intend to plot the distribution of the `minutes` column in the dataframe. As we performed the plotting directly, this is the resulting plot: 
<iframe src="assets/count-minutes-with-extremes.html" width=800 height=600 frameBorder=0></iframe>
As one can see, the distribution is extremely skewed to the right because of extreme outliers.

Due to the lack of clarity of this plot, we decided to remove the top 5 outliers using the threshold of 100000 minutes. This is the resulting plot:
<iframe src="assets/count-minutes-without-extremes.html" width=800 height=600 frameBorder=0></iframe>
This newly generated plot is still very right-skewed, hence we decided to use the interquartile quartertile range (IQR) of the data to determine the outliers defined as follows:

Recipes with 
1. `minutes` < 25th quartile - 1.5 * IQR or 
2. `minutes` > 75th quartile + 1.5 * IQR

are considered as outliers.

The final distribution of `minutes` we have is:
<iframe src="assets/count-minutes-without-outliers.html" width=800 height=600 frameBorder=0></iframe>

This final plot is the clearest among all three, but we can observe spikes on `minutes` that are ending in 0s and 5s. We believe this is the result of recipe contributors' habits and convention of rounding their recipes' time to the nearest 10s or 5s. 


#### **Plot 2 - Distribution of `rating_original`**
We decided to plot the distirbution of `rating_original` in the dataframe.
<iframe src="assets/rating-distribution.html" width=800 height=600 frameBorder=0></iframe>

We can see that the `rating_original` is left-skewed and there is no value at 0. This is because we have replaced all `0` ratings at the data cleaning process.


### ***Bivariate Analysis***
#### **Plot 1 - Scatterplot with `minutes` and `n_steps`**
Before plotting the relationship between `minutes` and `n_steps`, we have decided to first group the dataframe by `recipe_id`. This is because one recipe may have multiple users, hence representing just one recipe would be enough.

This scatterplot shows the relationship between `minutes` and `n_steps`.
<iframe src="assets/scatter-minutes-nsteps.html" width=800 height=600 frameBorder=0></iframe>

Intuitively, one may think that the longer the time a recipe takes, the more steps are involved. However, the linear regression line shows that the relationship is very weak. This is due to the extreme outliers on the right, while the values of `n_steps` are relatively reasonable in comparison.

#### **Plot 2 - Scatterplot with `minutes` and `rating`**
Using the same grouped dataframe as above, this scatterplot shows the relationship between `minutes` and `rating_average`:
<iframe src="assets/scatter-minutes-rating.html" width=800 height=600 frameBorder=0></iframe>

We observe a very weak relationship between these two variables. We believe this is due to the extreme outliers in `minutes`, while `rating_average` is capped at 5.


## **Assessment of Missingness**

### **NMAR Analysis**
We believe that the `review` column in the interactions dataframe can be NMAR because perhaps the user never really completed the recipe they started on, hence the review would be missing in this case. That being said, if we are able to obtain an additional column indicating whether the user truly finished the recipe, we may be able to determine that the missingness of `review` is MAR for the reason stated above.

### **Missingness Dependency**
#### **Plot 1 - Missingness of `minutes` on `rating_original`**
<iframe src="assets/missing-minute-orig-rating.html" width=800 height=600 frameBorder=0></iframe>

We fail to reject the null, hence we conclude that the missingness in the `minutes` column is not dependent on the `rating_original`.

#### **Plot 2 - Missingness of `minutes` on `n_steps`**
<iframe src="assets/missing-minute-name.html" width=800 height=600 frameBorder=0></iframe>

In this case, we reject the null, hence we conclude that the missingness in the `minutes` column is dependent on the`n_steps` column. We can further conclude that there is a relationship between minute and number of steps it takes for a recipe to be completed.


## **Permutation Testing**

*Null Hypothesis*: In the population, the average rating of recipes with `minutes` under the median `minutes` of the dataset has the same average rating of recipes with `minutes` above the median `minutes` -- the ratings of the two samples come from the same population distribution.

*Alternative Hypothesis*: In the population, the average rating of recipes with `minutes` under the median `minutes` of the dataset is higher than the average rating of recipes with `minutes` above the median `minutes`.

*Test Statistic*: The difference in means of the average ratings of the two samples of the dataset.

*Significance Level*: 0.05

*p-value*: 0.0

*Conclusion*: We reject the null hypothesis that the two samples are from the same distribution.

We believe, intuitively, that the average ratings of recipes that require fewer minutes will receive higher rating. However, we need to select a threshold to determine how to separate the two samples. Median is the more natural choice because it is more robust against outliers (as we have shown in previous sections, there exists some extreme outliers in the dataset). Using the median, we are able to separate the samples and retrieve the mean of of average ratings of each sample. Since we are trying to prove that average rating of the first sample (sample with lower minutes) is higher than the second, we use signed difference in mean, instead of absolute difference in mean.


