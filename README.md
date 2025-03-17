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

<iframe
  src="assets/plot_1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Distribution of Sugar Proportion in Recipes

- Most recipes derive a small proportion of their calories from sugar.
- Indicates that sugar is not the dominant calorie source in most recipes.

<iframe
  src="assets/plot_2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Bivariate Analysis:

### Recipe Count vs. Average Rating

We explored relationships between pairs of variables to uncover potential associations. One scatter plot between calories and ratings suggested that some high-calorie recipes are rated very highly (a rating of 5) suggesting strong satisfaction from certain users, others receive a rating of 0, reflecting significant dissatisfaction. This split in opinions can be seen as both positive and negative, as it implies that high-calorie recipes evoke strong reactions, whether favorable or unfavorable. 

<iframe
  src="assets/plot_3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Relationship Between Calories and Ratings

- Polarized ratings: High-calorie recipes often receive either very high (5) or very low (0) ratings.
- Suggests some users prefer indulgent meals, while others avoid them.

<iframe
  src="assets/plot_4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Interesting Aggregates

### Does Sugar Content Influence Popularity?
We categorize recipes into four groups based on their sugar proportion and analyze their average rating.

- Recipes with moderate sugar levels tend to have slightly higher ratings.
- Extremely low or high sugar content does not necessarily boost ratings.

| sugar_split   |   Count |   Mean_Rating |
|:--------------|--------:|--------------:|
| Very Low      |   58584 |       4.35849 |
| Low           |   58586 |       4.41689 |
| Medium        |   58574 |       4.40177 |
| High          |   58582 |       4.34195 |

## Assessment of Missingness

### NMAR Analysis

Missing reviews (only 57 values) suggest NMAR (Not Missing At Random).
Users might only leave reviews for recipes they strongly like or dislike.

### Permutation Test for Missingness
We conducted a permutation test to analyze if missing reviews depend on rating.
P-value: 0.066 → Suggests reviews might be Missing at Random (MAR).

<iframe
  src="assets/plot_5.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

## Hypothesis Testing

### Testing Recipe Healthiness via User Ratings:

To evaluate whether recipes with a healthier nutritional profile (defined as having more protein and fewer carbohydrates) are rated higher, we first computed a health score as the difference between protein and carbohydrates. Recipes with a health score above the median were labeled “healthy,” and those below were labeled “unhealthy.” We then calculated the observed difference in mean ratings between these two groups.

### Research Question

Does a high protein-to-carbohydrate ratio (healthier recipes) correlate with higher ratings?

Null Hypothesis (H₀): No difference in average ratings based on protein-to-carb ratio.
Alternative Hypothesis (H₁): Recipes with a higher protein-to-carb ratio have higher ratings.

<iframe
  src="assets/plot_6.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Permutation Test Results:

Observed Mean Difference: Higher protein-to-carb recipes had better ratings.
P-value: 0.0 → Strong evidence to reject the null hypothesis.
Users prefer high-protein, lower-carb recipes.

## Framing a Prediction Problem

Our prediction problem aims to determine what factors contribute to a recipe’s popularity, measured by the number of ratings. By analyzing various recipe attributes, nutritional content, and user interaction data, we seek to identify key elements that drive user engagement. Our model incorporates both original features such as preparation time, number of steps, and ingredients, as well as engineered features like steps per ingredient and ingredient complexity to capture the complexity and efficiency of a recipe.

Additionally, we include nutritional components like calories, protein, carbohydrates, and sugar to examine how health factors influence engagement. Using a Random Forest Regressor, we will predict the number of ratings a recipe will receive, helping to uncover trends in user preferences. These insights can assist recipe developers in optimizing their content and improving recommendation algorithms to better match users with recipes they are more likely to engage with.

## Baseline 

Linear Regression Model using:

log_minutes, n_steps, n_ingredients, steps_per_ingredient
contributor_id (one-hot encoded)

Performance:
Baseline R² Score: -0.0648 (poor fit)
Baseline RMSE: 5.10

## Final Model

Improved model using Random Forest Regressor.

### Feature Engineering:
Added ingredient_complexity
Tuned hyperparameters via GridSearchCV.

### Performance Improvement:
Final Model R² Score: 0.0111
Final Model RMSE: 4.01
Model captures slightly better variance.

## Fairness Analysis

### Does the Model Predict Worse for High-Sugar Recipes?

Groups:

Group X: Recipes with high sugar proportion
Group Y: Recipes with low sugar proportion

Null Hypothesis (H₀): Model performs equally well for both groups.
Alternative Hypothesis (H₁): Model performs worse for high-sugar recipes.

<iframe
  src="assets/plot_7.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Permutation Test Results:

- Observed Difference in RMSE: -0.0035
- P-value: 0.4820 → Fail to reject the null hypothesis.
- Conclusion: Model is not biased against high-sugar recipes.