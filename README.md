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

print(merged_recipe_df.head().to_markdown(index=False))

* since we needed to access the number of calories and amount of sugar in each recipe, we split up the nutrition column into multiple columns of numerical values of each measurement
* 


print(counts[['Quarter', 'Count']].head().to_markdown(index=False))


* grape
* apple

## ASSESSMENT OF MISSINGNESS
1. one
1. two
1. three
1. three

## HYPOTHESIS TESTING
