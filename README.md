# Sugar-in-Recipes-BoostingRatings

by Ishita Takkar (itakkar@ucsd.edu), Jay Manjrekar (jmanjrekar@ucsd.edu)

## Intoduction

Food plays a crucial role in our lives, but with rising health concerns like diabetes and obesity, dietary choices are under greater inspections. This project explores whether sugar and calorie content in recipes impact their ratings, reflecting consumer health awareness. By analyzing datasets containing recipe details and user interactions, we investigate whether people rate sugary, high-calorie recipes differently from healthier options. Understanding these preferences can provide insights for recipe creations and health-conscious individuals in balancing taste and nutrition.

## Data Cleaning and Exploratory Data Analysis

We began by merging our interactions and recipes datasets on the recipe ID and ID to align user behavior with recipe details, ensuring that every rating was paired with complete and descriptive information. Next, we cleaned the data by converting columns like rating and nutritional values to numeric types Finally, we derived additional features like computing the sugar proportion as sugar divided by calories to better capture nutritional aspects for further analysis. The dataset is below:

Univariate Analysis:
We first examined the distribution of individual variables. For example, the histogram of recipe ratings showed that most users give high ratings (mostly 5), resulting in a right-skewed distribution. In another univariate plot, the histogram of sugar proportion (sugar/calories) confirmed our assumption that many recipes have a low percentage of calories from sugar.

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


Interpretation: The rating distribution suggests users are generally very satisfied with recipes, while the sugar proportion plot indicates that most recipes contribute little to daily sugar intake.

Bivariate Analysis:
We explored relationships between pairs of variables to uncover potential associations. One scatter plot between calories and ratings suggested that some high-calorie recipes are rated very highly (a rating of 5) suggesting strong satisfaction from certain users, others receive a rating of 0, reflecting significant dissatisfaction. This split in opinions can be seen as both positive and negative, as it implies that high-calorie recipes evoke strong reactions, whether favorable or unfavorable. 


<iframe
  src="assets/plot4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


Another bivariate analysis grouped contributors by the number of recipes they submitted and their average rating, revealing that even prolific contributors tend to have ratings clustered around 4–5.


<iframe
  src="assets/plot2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>



## Assessment of Missingness



## Hypothesis Testing



## Framing a Prediction Problem

## Baseline Model

## Final Model

## Fairness Analysis

