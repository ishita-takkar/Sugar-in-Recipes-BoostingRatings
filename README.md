# What Makes a Recipe Popular?

by Ishita Takkar (itakkar@ucsd.edu), Jay Manjrekar (jmanjrekar@ucsd.edu)

## Intoduction

### Dataset Overview

We explore recipe data by merging the recipe information with user interactions to analyze both health consciousness and what makes a recipe popular. By examining how nutritional content and calorie levels affects consumer ratings, we uncover key trends in recipe preferences. Through data cleaning, univariate, and bivariate analyses, we highlight patterns in health awareness while also identifying factors that contribute to recipe popularity. Using these insights, we build predictive models to forecast recipe success, offering valuable guidance for both health-conscious consumers and those seeking highly-rated dishes.

This project analyzes recipe data from two sources:

RAW_recipes.csv (contains recipe details like ingredients, steps, and nutrition)

interactions.csv (user reviews and ratings for recipes)

We merge these datasets on id and recipe_id to examine how nutritional content and contributor experience influence recipe ratings and popularity.

## Data Cleaning and Exploratory Data Analysis

### Research Question

Does sugar content in a recipe impact its popularity (ratings)?
Understanding this can help health-conscious consumers make informed choices and assist content creators in optimizing recipe recommendations.

Relevant Columns:

- recipe_id: Unique identifier for each recipe
- rating: User rating (0-5 scale)
- nutrition: List of nutritional values (calories, fat, sugar, sodium, protein, etc.)
- contributor_id: ID of the user who shared the recipe
- minutes: Total preparation time
- n_steps: Number of cooking steps
- n_ingredients: Number of ingredients

### Data Cleaning

- Merged datasets on recipe_id
- Extracted nutrition values from string format into separate columns (calories, sugar, etc.)

Created new features, including:
prop_sugar = Sugar content / Total calories

## Univariate Analysis

### Distribution of Recipe Ratings

- The distribution is right-skewed, meaning most recipes receive high ratings (4-5).
- Very few recipes receive low ratings (0-2).

### Distribution of Sugar Proportion in Recipes

- Most recipes derive a small proportion of their calories from sugar.
- Indicates that sugar is not the dominant calorie source in most recipes.

<iframe
  src="assets/plot1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/plot3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Bivariate Analysis:

### Recipe Count vs. Average Rating

We explored relationships between pairs of variables to uncover potential associations. One scatter plot between calories and ratings suggested that some high-calorie recipes are rated very highly (a rating of 5) suggesting strong satisfaction from certain users, others receive a rating of 0, reflecting significant dissatisfaction. This split in opinions can be seen as both positive and negative, as it implies that high-calorie recipes evoke strong reactions, whether favorable or unfavorable. 

<iframe
  src="assets/plot4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Relationship Between Calories and Ratings

- Polarized ratings: High-calorie recipes often receive either very high (5) or very low (0) ratings.
- Suggests some users prefer indulgent meals, while others avoid them.

<iframe
  src="assets/plot2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Interesting Aggregates

### Does Sugar Content Influence Popularity?
We categorize recipes into four groups based on their sugar proportion and analyze their average rating.

- Recipes with moderate sugar levels tend to have slightly higher ratings.
- Extremely low or high sugar content does not necessarily boost ratings.

## Assessment of Missingness

### NMAR Analysis

Missing reviews (only 57 values) suggest NMAR (Not Missing At Random).
Users might only leave reviews for recipes they strongly like or dislike.

### Permutation Test for Missingness
We conducted a permutation test to analyze if missing reviews depend on rating.
P-value: 0.066 → Suggests reviews might be Missing at Random (MAR).

## Hypothesis Testing

### Testing Recipe Healthiness via User Ratings:

To evaluate whether recipes with a healthier nutritional profile (defined as having more protein and fewer carbohydrates) are rated higher, we first computed a health score as the difference between protein and carbohydrates. Recipes with a health score above the median were labeled “healthy,” and those below were labeled “unhealthy.” We then calculated the observed difference in mean ratings between these two groups.

### Research Question

Does a high protein-to-carbohydrate ratio (healthier recipes) correlate with higher ratings?

Null Hypothesis (H₀): No difference in average ratings based on protein-to-carb ratio.
Alternative Hypothesis (H₁): Recipes with a higher protein-to-carb ratio have higher ratings.

Permutation Test Results:

Observed Mean Difference: Higher protein-to-carb recipes had better ratings.
P-value: 0.0 → Strong evidence to reject the null hypothesis.
Users prefer high-protein, lower-carb recipes.

<iframe
  src="assets/hypothesis.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis

