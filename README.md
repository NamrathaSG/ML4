# Holiday Packages 

## Introduction 

You are hired by a tour and travel agency which deals in selling holiday packages. You are provided details of 872 employees of a company. Among these employees, some opted for the package and some didn't. You have to help the company in predicting whether an employee will opt for the package or not on the basis of the information given in the data set. Also, find out the important factors on the basis of which the company will focus on particular employees to sell their packages.

## Exploratory Data Analysis 

Loading the data file, we see that the first column is a serial number and we drop the column. Then looking at duplicates we see that there are no duplicate rows. Also, there are no NULL values in data. Shape of our data frame is 872 x 7.

Our of 7 variables, the dependent variable Holiday_Package and Foreigner are Categorical variables. All other variables are continuous. Analysing continuous variables, we see that salary and no_young_children seem to have more outliers than the others.

Going by definition of Skewness:
Fairly Skewed (between -0.5 and 0.5).

Moderately Skewed (between -1 and – 0.5 or between 0.5 and 1).
Highly Skewed (less than -1 or greater than 1). None of them seem to be highly skewed.
Fairly Skewed: age and education
Moderately Skewed: no_older_children Highly Skewed: no_young_children and salary

Mean and median are pretty close to each other except for no_young_children and Salary

Going by definition of Kurtosis (Normal distribution has a Kurtosis of 3 and Kurtosis value higher than 3 means the distribution has a thicker tail than a normal distribution), we see that age_education and no_older_children are normally distributed. Salary and no_older_children have thicker tails. 

## Modelling and Inference 

We have considered employee opting for Holiday_Package (yes) as class =1 and employee not opting for Holiday_Package (no) as class 0. Considering this, these are the definitions.
Train
Accuracy: 0.6721
ROC_AUC Score: 0.7405
 
True Positive – Employees choosing holiday package and our model predicting that they will choose Holiday Package True Negative – Employees NOT choosing holiday package and model predicting that they will not choose package. False Positive - Employees NOT choosing holiday package and model predicting that they will choose package.
False Negative - Employees choosing holiday package and our model predicting that they will not choose package.
1. Logistic regression Train and Test accuracies ( 0.5213 Vs 0.5382 ) are approximately the same. So we don’t have any over/under fitting issue.
2. LDA Train and Test accuracies ( 0.6721 Vs 0.6412 ) are approximately the same. So, we don’t have any over/under fitting issue.
3. LDA accuracy is better than that for Logistic Regression. So LDA is a better model for this data.
4. Logistic Regression Recall for Class 1 is 0.08 which is pretty bad. LDA Recall is 0.56 which is also bad but is much
better than that for Logistic Regression.
5. Both Logistic Regression and LDA are not giving good prediction. So, the next recommendation is to try
QuadraticDiscriminantAnalysis. I tried that and the accuracy of train data did not change much. It remained at
0.67. So that did not improve the model too.
6. Looking at the coefficients of LDA model.

['Salary', 'age', 'education', 'no_young_children', 'no_older_children', 'foreigner']
[-1.47549548e-05, -5.43037831e-02, 7.59653739e-02, -1.42854644e+00, -4.63592980e-02, 1.62390347e+00]

We see that features “foreigner” and “no_young_children” are the two good predictors with values 1.6 and -1.4. So we ask the company to give more importance to these features.
7. In this scenario, it is not very clear if the company is more concerned about Type I or Type II error. My guess would be Type II error. Considering this, recall is more important than accuracy. We need to reduce type II error. (Employee chooses a holiday package and our model predicts that employee will not choose package. This will be an additional unplanned burden on the company). Since the recalls are not good in both models, my recommendation to the company would be to collect more data and not make any predictions using the model we created with data in hand. We could also ask the company to collect additional features for prediction. May be, if we knew when was the last time employee had opted or gone on a holiday.

