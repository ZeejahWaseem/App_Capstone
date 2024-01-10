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

8. Coapplicantincome ( Co Applicant income)

9. LoanAmount ( Loan amount in thousands)

10. Credit_History ( Credit history meets guidelines yes or no, represented by values of 1 or 0)

11. Loan_Amount_Term ( Term of loan in months)

12. Property_Area ( Semiurban, Urban, Other)

13. Self_Employed ( Self Employed, Yes or No)


## Exploratory Data Analysis

We proceed to import the data into a dataframe and view its contents in order to have a basic idea of the features we are working with. 
madfhantr.csv ( This is our Training data)
madhante.csv ( This is our Testing data)

We combine the applicant and coapplicant income features into one feature, as these are closely related.

As we look at the data we notice that there are some missing values in a few of the columns that we will later decide whether to drop or to replace.
 
We notice that there is a class imbalance between the loans that have been approved and the loans that have not. We need to be wary of that fact as we proceeed as our model may end up being bias towards approving the loan as it is most common. This also makes us aware of the metrics that we want to use as accuracy may not be the best indicator as a dummy classifier that could predict the majority class should have a 68% level of accuracy. We instead will use precision as a metric which will insure the bank is not burdened with unwanted risk when providing loans to applicants.

*Image

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







