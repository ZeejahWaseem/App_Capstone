# Bank Loan Classification Analysis 

## Introduction

Dream Housing Finance company deals in all kinds of home loans. They have presence across all urban, semi urban, and rural areas. Dream Housing Finance company wants to automate the loan eligibility process (real time) based on customer detail provided while filling online application forms. Customer first applies for home loan and after that company validates the customer eligibility for loan. 
    
This classification analysis will allow Dream Housing Finance Company to automate their loan eligibility process to identify the customers that are eligible for loan amounts so that they can specifically target these customers. Dream Housing Finance Company can then use this data to immediately deny loan applications or submit for further review. Automating the loan approval process will significantly reduce hours spent by underwriters reviewing loan applications, in addition to improving the precision of loan eligibility identification. 


## Data Used 

The dataset used for this analysis comes from Kaggle.

https://www.kaggle.com/datasets/madhansing/bank-loan2

The data is divided into two parts. One part is used for training data, the other is used for testing data.

madfhantr.csv ( This is our Training data)

madhante.csv ( This is our Testing data)


## Feature Descriptions

1. Loan_Status ( Loan approved Yes or No. This is our dependent, or target feature. This feature is dependent on all of the other feature                    that follow, called independent features.)

2. Loan_Id (Unique Loan Id)

3. Gender ( Male or Female)

4. Married ( Applicant Married, Yes or No)

5. Education (Applicant Education, Graduate/ Under Graduate)

6. Dependents ( Number of Dependents)

7. ApplicantIncome ( Applicant income)

8. Coapplicantincome ( Co-Applicant income)

9. LoanAmount ( Loan amount in thousands)

10. Credit_History ( Credit history meets guidelines yes or no, represented by values of 1 or 0)

11. Loan_Amount_Term ( Term of loan in months)

12. Property_Area ( Semiurban, Urban, Other)

13. Self_Employed ( Self Employed, Yes or No)


## Exploratory Data Analysis

We begin our analysis by importing the data into a dataframe and view its contents in order to have a basic idea of the features we are working with. 

madfhantr.csv ( This is our Training data)

madhante.csv ( This is our Testing data)

We combine the applicant and coapplicant income features into one feature, as these are closely related.

As we look at the data we notice that there are some missing values in a few of the columns that we will later decide whether to drop or to replace.
 
Continuing forward with the data we notice that there is a class imbalance between the loans that have been approved and the loans that have not. We need to be wary of that fact as we proceed because our model may end up being bias towards approving the loan since it is most common. This also makes us aware of the metrics that we want to use, accuracy might not be the best indicator as a dummy classifier that could predict the majority class should have a 68% level of accuracy. We instead will use precision as a metric which will insure the bank is not burdened with unwanted risk when providing loans to applicants. The precison metric will lower the incidents of false positives, that is to say loan applicantions being sent for futher review when they should be automatically denied.


![alt text](Images/Approval Status - Credit History.PNG.png)

Using and plotting a correlation matrix using seaborn we can view the relationship between some features to get a better understanding of our data.

*Image


## Data Cleaning

Our first cleaning step is to check for missing values.

We notice that there are some null values and for the categorial variables we choose to replace them with the mode or the most common    value. We are going to create a function to turn replace the null values with the mode.

Looping through the categorical columns using the function we built and replacing the null values with the mode.

After replacing all of the categorical variables, we will now deal with the numerical variables.

Normally for Numerical variables we would be inclined to take the mean, however we can see that the loan amount terms are specific amounts and taking the average would not make much sense. We also know that there are outliers for the loan amount therefore we can use the same function to replace the values with the mode for the numerical variables.

Next we transform the categoricals variables into numbers and encode them in order for our algorithm to properly interpret them.

We use the label encoder function to transform the categorical variables that are binary.

Then we loop through the categories and encode them.

We next use the get dummies function to encode the singular column that is not binary. Normally we would use OHE but its a singular column thats is a series therefore the get dummies function works better.

We confirm all data types are correct.

Then we combined applicant income with both coaplicant income and the monthly installment. This was done because these three features are closely related, and it is generally best practice to limit features when possible.

We notice that we have two features of the type object, we will drop the Loan_ID before loading it into the X value. As for the dependents we need to either drop it or change it from strings into numbers.

The categories for the dependents columns are just numbers that have been set as catogories, we just need to replace them with their numerical counterparts. We will proceed to loop through them and replace them.

Next is a sanity check to see if we have elimated all the categorical variables.

All categorical variables have been eliminated.

Data cleaning is complete, we proceed to modeling.


## Modeling

Modeling preparation begins by splitting the data into a train test split. Then assign the data a random_state of 42, this will ensure consistant results.

We then proceed to scale the model after splitting it in order to prevent data from leaking into the test set.

We will first start off with a dummy classifier with the most frequent class being the strategy to evaluate the model.

We optain a accurracy of about 65% but we know that is not the best metric to use as blindly predicting will lead us to at least a 65% accuracy we also need to make sure that the model doesn't favor the majority class therefore we will be using precision as our main metric while viewing and trying to improve other metrics as well such as recall.

Retrieving the precision score yields a score of roughly 65% as well.

We then print a classification report to confirm all metrics.

Next we can start the actual modeling by trying different classifying algorithms, starting with the decision tree model.

The decision tree classifier yields an improvement of about 11% in the precision score, from roughly 65% to 76%.

We try to improve the model further by using grid search.

While we don't see an improvement in the precision score after using grid search we do see an improvement in other metrics such as the f1 score. With the improvment of the f1 score we will consider grid search successful in giving us a better model.

We create a confusion matrix to better visualize the data.

*Image

Our next modeling attempt to improve the classification will be the random forest classifier model.

We got a slightly better precision score from random forest model (roughly 77%). 

Grid search is next used to tune some parameters with the hope of further improving our precision score.

Grid search did not improve our precision but it did improve recall. We stick with the original random forest classifier model without grid search as precision is still our target metric, not recall.

We create another confusion matrix to visualize our current metrics.

*Image

The next modeling technique we use is the XGBoost Classifier model.

XGBoost slightly improves our precison score.

XGBoost with grid search further improves the precison score to it's highest level of 79%, and improves the f1 score to it's highest level of 77%.

Again we create a confusion matrix to visualize these metrics.

*Image

We then check the XGboost model for overfitting and notice that there is a lot of overfitting in our model. This overfitting can be seen by obserrving that our training precision is much higher than our testing precision.

Next we'll look at the features that the model believes were important when making a decision.

*Image(Feature importance)

The feature importances shows us that credit history, the property areas, and loan amount term are the most important features to our model.

Once we found the most important features we can take a deeper look at them through visualizations that will allow us to make recommendations to the company.

*Image(Credit History)

We can see that those with a good credit history where approved for the loan while those with a bad credit history where more ofthen rejected than approved.

*Image(Property_Area)

We notice that Semi Urban areas have the most likely hood of having an application approved, while those in rural areas are most likely to be rejected.

*Image(Loan_Amount_Term)

Lastly we notice that the standard loan amount term which is 360 months has the highest likely hood of being approved.


## Conclusion

By using our most effective classification model (XGBoost) Dream Housing Finance Company will be able to automate their loan eligibility process in the most efficient way possible. Considerable time spent by underwritters will be saved, and precision will be increased. This increase in precison will lower the incidents of false positives in the loan process. False positives in this case being loan applicants being sent to further review for a loan when they should automatcally be denied. Credit risk for Dream Housing Finance Company will be greatly mitigated by using the XGBoost ML model to identify and measure the factors that most directly correlate to a borrower defaulting on their credit obligations.


## Constraints

The XGboost model appears to be overfitting. This overfitting can be seen by observing that our training precision is much higher than our testing precision. This overfitting is an issue that will be addressed by further tuning for future iterations of model use.





















