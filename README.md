# Mental Health in Tech Industry
Mental health is an increasingly important concern in today’s world. It is estimated that 16.2 million adults in the United States, or 6.7 percent of American adults, have had at least one major depressive episode each year. Depression tends to affect people in their prime working years and is one of the top 3 workplace problems.

## Project Description and Research Questions
The purpose of our project is to tackle this problem by evaluating data related to prevalence of mental health disorders in the IT workplace and generate a profile for adults most prone to depression. This will help understand the risk factors that contribute to mental health disorders. The insights can also help guide company policies regarding mental health resources to protect their employees in the workplace. The following list comprise the research questions proposed:
* Investigate the impact of geographical location on the amount or the probability of seeking treatment for mental illnesses.
* Determine the effect of a company’s mental health coverage policy on the amount of employees seeking treatment.
* Investigate the effect of negative workplace sentiment on the number of people seeking treatment.
* Determine whether a person with a history of mental illness is more prone to facing another mental health issue.
* Determine if an employee’s gender influences whether they feel that mental health concerns can be brought up in their workplace.
* Determine factors that are significantly determine the probability of people seeking treatment for mental illness

## Data Collection and Pre-Processing
The dataset for our study has been obtained from https://www.kaggle.com/osmi/mental health in tech 2016. This dataset has 1433 responses from a survey to measure attitudes towards mental health in the IT/tech workplace and examine the frequency of mental health disorders among tech workers. The dataset contains 63 columns, including categorical and text based columns. Data cleaning and feature engineering has been done to select specific columns which are relevant and largely contain non empty values

## Data Cleaning
* Engineered feature negative workplace sentiment: To reduce the complexity of workplace views on mental health 4 columns are reduced to 1. Ensuring that this feature does not have NA values requires omitting 287 rows of data.
* Countries: 53 countries are represented but the observations are not
evenly divided among them. Will only control for the top 5 countries creating indicator
variables 1 or 0 if observations are from them
* Coverage Policy: The variable for mental health coverage policy takes on 4 kinds of values. To control for coverage only need Yes and No. Requires omitting 689 rows
* EDA and Classification: Reducing multiple categories to closely related fewer categories
for simpler analysis and interpretation: Categories 'Somewhat Easy', 'Very Easy' merged as 'Easy', and Categories 'Somewhat difficult', 'Very difficult' merged as 'Difficult'. Merging "Not Eligible" to a "No" Category depending on the context. Merging text based responses like 'No, I don't think it would', 'No, it has not' to a broader category 'No'. Cleaning input responses for gender like "Male", Male","Female"," Woman","Non Binary",Binary","Transgender" to three categories : "M", "F" and "Others". Imputing missing values for predictors. This includes risk of errors due to large amount of categorical data, but a greater emphasis has been given to avoiding dropping of valuable data points.


## Exploratory Data Analysis
**Correlation Matrix** An initial analysis to observe the correlation between the various columns of the data
gave the following matrix:


![Correlation Matrix](https://github.com/svellaichamy3/MentalHealthTechIndustry/blob/main/images/EDA1.PNG)

We can see that “Diagnosed Medical condition Med Prof” is highly correlated to “Current Mental Illness”, “Past Mental Illness” and “Family History Mental Illness”. Other categorical variables like Gender, Country and Work style are not included because a numerical correlation cannot be calculated.
To observe the effect between Current Mental Illness, Diagnosed Mental Illness
and other categorical columns, bar graphs were generated as follows:


![EDA2](https://github.com/svellaichamy3/MentalHealthTechIndustry/blob/main/images/EDa2.PNG)

- USA, UK and Australia are one of the top few countries with highest percentage of employees suffering
from mental illness or seeking medical help. help.(Australia does however have very few data points and the
analysis may not be very representative of the truth)
- There seems to be a larger percentage of employees categorized under the "Other" gender category. It
could mean that the LGBTQ community faces a greater risk for suffering from mental illness at a tech
workplace.
- There seems to be no significant effect of the work style (remote or not) on mental condition.


Some other interesting graphs show the effect of society’s response to mental health
discussions. It is seen clearly that when there is a negative response from coworkers or unsupportive
response from the company, employees are more prone to having a mental illness


![EDDA3](https://github.com/svellaichamy3/MentalHealthTechIndustry/blob/main/images/EDA3.PNG)



## Models

### Poisson Regression
A Poisson regression model can be useful in determining
the effect of certain factors on a response count variable.The dataset does not inherently contain a count response
variable.Aggregating a variable such as treatment or illness, the
dataset can be transformed into count data format.The Poisson model will be used to see the effect of
geographic location, negative workplace sentiment, and
providing coverage on the number of people seeking
treatment and the number of diagnosed mental illnesses. Will be used for descriptive interpretation of the coefficients
and the F test will be used for testing coefficients’
significance, so a dispersion calculation is not needed.

### Logistic Regression
To answer our research questions, 2 Logistic regression
models will be built : To predict probability of employee's current mental illness, To predict the probability of him/her seeking treatment for mental
health issues. Missing data among predictors have been imputed to avoid
dropping data points that would have other significant
predictors. Relevant factors(like Past mental illness, Employer's take on
mental illness, Previous Employers, Age, Gender, Family
History etc.) have been considered for the models. p value of the factors will be used to determine their
statistical significance. Model results will be used to descriptively interpret the
coefficients against the response variable.
### Random Forest


_Algorithm:_
Decision Trees and their extension Random
Forests are robust and easy to interpret machine
learning algorithms for both classification and
regression tasks.

_Analysis:_
**Variable Importance:** The chart shows us a list of variables in decreasing order of their predictive power towards the built Randomforest model. **Evaluation** The Receiver Operating Characteristic is a plot that can be used to determine the performance and robustness of a binary or multi class classifier. The x axis is the false positive rate (FPR) and the y axis is the true positive rate (TPR). This ensures we are taking into account the accuracies of both classes while classifying.

## Results and Discussion

### Poisson Regression: 
The expected number of mental illnesses in the U.S. is higher than the expected number of individuals in
other countries outside of the top 5 countries with observations. The expected number of mental illnesses in Canada, Denmark, and the Netherlands are each lower
than the expected number of countries outside of the top 5 countries with observations. The expected number of mental illnesses is higher when employees have a negative experience concerning mental health at their work. The expected number of people seeking treatment is greater in the United States than in other countries outside of the top 5 countries with observations. The expected number of those seeking treatment is greater when employer's provide coverage for mental health visits. 2.275 is the amount to add to the coverage coefficient to get the coefficient for individuals living in the U.S. Therefore, employer's providing coverage in the U.S. will have a multiplied effect on the number of people seeking treatment in the U.S.
 
### Logistic Regression:
"Current Mental Illness" Vs Predictors


![Log1](https://github.com/svellaichamy3/MentalHealthTechIndustry/blob/main/images/Log1.PNG)
Interpretation:
- Previous employers that weighed mental health seriously reduced the odds of mental
illness among employees as compared to employers that do not take mental health
seriously.
_Somewhat seriously weighed concerns : Reduced odds of illness by 0.350; Very seriously weighed concerns : Reduced odds of illness by 0.76_

- Past Mental illness is significant in determining a person's current mental illness.
_Employee without Past mental illness : Reduced odds of current illness by 0.24_


- Age contributes to a person's mental illness._Person with higher age : Reduced odds of illness by 0.023_
- Gender or family history has no effect on a person's mental illness.

"Employees Seeking Treatment" Vs Predictors

![Log2](https://github.com/svellaichamy3/MentalHealthTechIndustry/blob/main/images/Log2.PNG)
Interpretation:
- Employers that discuss mental illness with their employees increase the chances of
employees seeking treatment for depression.
 _Employer who discussed concerns : Increased odds of employee seeking treatment by 0.540_
- Employees awareness on Mental health benefits increases chances of seeking treatment. _Employee aware of health benefits : Increased odds of seeking treatment by 0.742_
- Past mental illness significantly impacts employees seeking treatment for depression. _Person with prior mental illness : Increases odds of seeking treatment by 0.853_

### Random Forest:
Problem Statement: To identify factors that increase the risk of Mental illness
Dependent Variable: Respondents who currently having a
mental illness or are diagnosed for a mental illness by a
mental health professional.
Predictor variables: We see different categories of
predictors in the dataset:
* Variables pertaining to current employers
* Variables pertaining to previous employers
* Variables pertaining to personal characteristics

We initially build individual Randomforest models for each category letting us have a closer look within the category.

![RF1](https://github.com/svellaichamy3/MentalHealthTechIndustry/blob/main/images/RF1.PNG)

In both cases of previous and current employers, employees who perceive that a discussion around mental health could causes negative consequence on Mental Health are more likely to be affected. 
Employees with past mental illnesses are more susceptible to have a mental illness

![RF2](https://github.com/svellaichamy3/MentalHealthTechIndustry/blob/main/images/RF2.PNG)

The predictive model with the variables listed has an accuracy of ~87%

We see that of all the factors, the 'Past Mental
Illness' seems to be a very important factor
meaning, this variable highly predicts the risk of
an individual.

The top subsequent factors are variables
belonging to a mix of different categories and
hence highlights the importance of all categories.


## Summary
* The expected number of mental illnesses is statistically greater in the U.S. over other countries.
* Employers offering benefits packages including mental health resources increases the number of employees seeking treatment.
* An employee with a past mental illness has a significantly higher chance of a recurring illness.
* Employers weighing mental health seriously have reduced the chances of depression among employees as compared to employers that do not take mental health seriously.
* Employee's awareness on mental health benefits increases their chances of seeking treatment.

## Recommendation to Tech Cmpanies
Employers discussion of mental health in the workplace and promoting a positive attitude about discussing mental health is very important, and its absence can lead to a
greater presence of mental illnesses. Employers are highly recommended to offer their employees coverage for mental health visits, especially if the company is in the United States and if their employee has had a history of mental illness in the past
