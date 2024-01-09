# Bank Loan Classification Analysis 

## Introduction

###  Dream Housing Finance company deals in all kinds of home loans. They have presence across all urban, semi urban, and rural areas. Dream Housing Finance company wants to automate the loan eligibility process (real time) based on customer detail provided while filling online application forms. Customer first applies for home loan and after that company validates the customer eligibility for loan. 
### This classification analysis will allow Dream Housing Finance Company to automate their loan eligibility process to identify the customers that are eligible for loan amounts so that they can specifically target these customers. Dream Housing Finance Company can then use this data to immediately deny loan applications or submit for further review. Automating the loan approval process will significantly reduce hours spent by underwriters reviewing loan applications, in addition to improving the precision of loan eligibility identification. 


## Data Used 

### The dataset used for this analysis comes from Kaggle.
https://www.kaggle.com/datasets/madhansing/bank-loan2

### The data is divided into two parts. One part is used for training data, the other is used for testing data.
#### madfhantr.csv ( This is our Training data)
#### madhante.csv ( This is our Testing data)


## Feature Descriptions

1. Loan_Id ( Uninque loan ID)

2. Loan_Status ( Loan approved Yes or No. This is our dependent, or target feature. This feature is dependent on all of the other feature                    that follow, called independent features.)

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

### We proceed to import the data into a dataframe and view its contents in order to have a basic idea of the features we are working with. 
#### madfhantr.csv ( This is our Training data)
#### madhante.csv ( This is our Testing data)

### We combine the applicant and coapplicant income features into one feature, as these are closely related.

### As we look at the data we notice that there are some missing values in a few of the columns that we will later decide whether to drop or to replace.

### We notice that there is a class imbalance between the loans that have been approved and the loans that have not. We need to be wary of that fact as we proceeed as our model may end up being bias towards approving the loan as it is most common. This also makes us aware of the metrics that we want to use as accuracy may not be the best indicator as a dummy classifier that could predict the majority class should have a 68% level of accuracy. We instead will use precision as a metric which will insure the bank is not burdened with unwanted risk when providing loans to applicants.









