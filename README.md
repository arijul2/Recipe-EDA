# Recipe-EDA
This is a project for DSC80 at UCSD where exploratory data analysis was performed on a recipes and ratings dataset.

## INTRODUCTION

Excess sugar consumption is a debilitating epidemic among developed nations.
One way to analyze such sugar consumption is looking at recipes online and their ratings, in relation to their sugar content.
We are trying to figure out if the recipes that are the subject of positive reviews have a higher or lower sugar content than that of negative reviews.

This dataset is a combination of recipes on recipes.com (with its nutritional information) and any interactions (ratings, questions, comments)
The original recipes dataset has 83782 rows, and the original interactions dataset has 731927 rows

combined, it has 234429 rows

the columns that are relavant to our question is
1. id : provides the id for each recipe, so we can differentiate between unique recipes
2. rating : the ratings (1-5) submitted by a user
3. nutrition : column containing nutritional information about the recipe, including the amount of sugar and calories it contains

## CLEANING AND EDA

we :
* left merged on the recipe id
* replaced 0 ratings with np.nan, since ratings can only be from 1-5
* found the average rating per recipe
* added the average rating per recipe back into the merged dataframe

up to this point, the dataframe looked like this :

|    | name                                 |     id |   minutes |   contributor_id | submitted   | tags                                                                                                                                                                                                                        | nutrition                                    |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                    |   n_ingredients |          user_id |   recipe_id | date       |   rating | review                                                                                                                                                                                                                                                                                                                                           |
|---:|:-------------------------------------|-------:|----------:|-----------------:|:------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------|----------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-----------------:|------------:|:-----------|---------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  0 | 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]     |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']                                                  | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] |               9 | 386585           |      333281 | 2008-11-19 |        4 | These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.                                                                                   |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                               | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0] |        12 | ['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', 'serve hot and enjoy !'] | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                    |              11 | 424680           |      453467 | 2012-01-26 |        5 | Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, & I made the whole batch & used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe! |
|  2 | 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                              | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |  29782           |      306168 | 2008-12-31 |        5 | This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!                                                                                                                                  |
|    |                                      |        |           |                  |             |                                                                                                                                                                                                                             |                                              |           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                   |                                                                                                                                                                                |                 |                  |             |            |          | The photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.                                                                                                                                                                                                        |
|    |                                      |        |           |                  |             |                                                                                                                                                                                                                             |                                              |           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |                                                                                                                                                                                                                                                                                                                                                                                   |                                                                                                                                                                                |                 |                  |             |            |          | Thanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family's favorite Zaar cookbook :)                                                                                                                                                                                                                          |
|  3 | 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                              | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |      1.19628e+06 |      306168 | 2009-04-13 |        5 | I made this for my son's first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.                                                                                                                                                                               |
|  4 | 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]    |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                              | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 | 768828           |      306168 | 2013-08-02 |        5 | Loved this.  Be sure to completely thaw the broccoli.  I didn&#039;t and it didn&#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.                                                                                                                                                     |

* since we needed to access the number of calories and amount of sugar in each recipe, we split up the nutrition column into multiple columns of numerical values of each measurement
* also added a column : sugar to calorie ratio

### adding extra columns for analysis

added
* review word count
* a column which indicates if the review is positive (4-5 stars) or negative (1-2 stars) or neither (3 stars, which we will ignore)
* column indicating if the average rating for a recipe is positive or negative (0 means negative, 1 means positive, 99 means neither)

### univariate analysis

want to see the distribution of ratings

<iframe src="figures/rating_dist_fig.html" width=800 height=600 frameBorder=0></iframe>

majority of reviews are 4-5 stars, there are very few 1, 2, 3 star reviews

see distribution of sugar to calorie ratio among all recipes

<iframe src="figures/sug_cal_dist_fig.html" width=800 height=600 frameBorder=0></iframe>

majority of recipes have a lower sugar content, with some outliers with extremely high sugar content

### bivariate analysis

looking at relationship between rating and sugar content

<iframe src="figures/rating_sugcal_scatter_fig.html" width=800 height=600 frameBorder=0></iframe>

the data is already more sparse (less reviews) for lower rated recipes (since no one wants to make unpopular, low rated recipes), so we cannot determine a correlation

check distribution of sugar content for low rated vs high rated recipes

<iframe src="figures/low_high_sug_fig.html" width=800 height=600 frameBorder=0></iframe>

the distribution in sugar content between low rated and high rated recipes seem very similar

### grouping EDA, aggregates

do highly rated recipes take shorter or longer than low rated?

| positive or negative   |   minutes |
|:-----------------------|----------:|
| Negative               |   98.9261 |
| Neither                |  133.161  |
| Positive               |  104.159  |

higher rated recipes seems to take longer

do highly rated recipes have more calories than low rated?

| positive or negative   |   calories |
|:-----------------------|-----------:|
| Negative               |    468.513 |
| Neither                |    465.276 |
| Positive               |    413.381 |

higher rated recipes seem to have less calories

is there more sugar in highly rated recipes?

| positive or negative   |   sugar to calorie ratio |
|:-----------------------|-------------------------:|
| Negative               |                 0.181071 |
| Neither                |                 0.1693   |
| Positive               |                 0.166069 |

there seems to be more sugar in recipes in ratings that are more positive

looking at sugar content by rating

|   rating |   sugar to calorie ratio |
|---------:|-------------------------:|
|        1 |                 0.188003 |
|        2 |                 0.172675 |
|        3 |                 0.162239 |
|        4 |                 0.155207 |
|        5 |                 0.168458 |


## ASSESSMENT OF MISSINGNESS
name, date, and rating are primarily the columns with missing values
we will focus on rating because name and date is not used for our analysis

#### Is the missngness mechanism of ratings MD?
Missingness of ratings is not MD, since there is no way to tell whether or not the rating will be missing looking at another column

#### Is the missngness mechanism of ratings NMAR?
in the original interactions dataframe, there are a lot of comments or questions that are not attatched to a rating there are 51832 such non-rating interactions, thus the missing ratings (nans) in the merged dataframe come from the data generating process. users are not required to rate when leaving a comment or question. the missingness does not depend on the rating itself
missingness of ratings is not NMAR

#### Does missingness depend on other columns? (MAR)

we performed permutation testing on every other column to see if the missingness is random
the columns it would make sense to test are : minutes, n_steps, n_ingredients, calories, total fat, sugar, sodium, protein, saturated fat, carbohydrates, sugar to calorie ratio, review word count

the test statistic we used for permutation testing is absolute difference in means (of each relavant numerical column when rating is missing vs not missing)

for minutes, the observed test statistic is 51.45237039852127

for calories, it was 69.00722806375853

the p-value for the permutation test on minutes is consistently above 0.05, thus the missingness of ratings does not depend on number of minutes the recipe takes

the p-value for the permutation test on calories is close to zero, so the missingness of ratings does seem to depend on calories statistically, although it is most likely not the cause of missingness, and therefore probabilistic imputation based on calories will not be accurate

distribution of calories when rating is missing vs not missing

<iframe src="figures/cal_missing_fig.html" width=800 height=600 frameBorder=0></iframe>

there does not seem to be a difference in the distribution of calories, based on the figure

## HYPOTHESIS TESTING

null hypothesis : any observed differences betweeen the distribution of sugar content between highly rated and low rated recipes is due to random chance
alternative : sugar content is higher in lower rated recipes

result : p value = 0

of our simulated tests, there is almost NO CASES where the difference betweeen the means was the same as or exceeded our observed statistic : 0.015002162907546163

thus, we fail to reject the null hypothesis
the difference is not statistically negligible

#### Conclusion
Recipes that are the subject of negative reviews have a higher sugar content than that of positive reviews
