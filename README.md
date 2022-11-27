# Predicting Financial Delinquency - Days Past Due

## NON-TECHNICAL EXPLANATION OF YOUR PROJECT
This project focuses on predicting financial delinquency based on a borrower's credit or borrowing history, as part of credit scoring. Essentially, we are trying to predict borrowers who are likely to be 90 days past due from their loan. The aim here is to understand how machine learning models can be used for financial delinquency, which is relevant to industries in the financial sector or financial services. It also looks at how common credit or financial history features can be used in predicting delinquency.

## DATA
The data is derived from the "Give Me Some Credit" Kaggle competition hosted by Home Credit, as part of a prediction competition. The dataset can be found in the link below. The contains the historical data of Home Credit customers, with a total of 251503 rows, whereby 150000 records belong to the train set and 101503 records belong to test set that is used in submission. Since we are not entering the competition and merely building a pipeline, we will use the 150000 records for the purposes of this repository instead.

The data is stored in /give_me_some_credit_data/ folder. The main file used for training the model is cs-training.csv and it contains 150000 records.

Link to Kaggle Source:
(https://www.kaggle.com/competitions/GiveMeSomeCredit/overview)


## MODEL 
A summary of the model you’re using and why you chose it. 

The model that is used for this dataset training would be a Random Forest Classifier. The reason for choosing this is as follows:

1. It is easy to interpret by both technical and non-technical users, as we can follow the decision tree and its decision splits
2. Random Forests work well with both categorical and continuous data
3. It is non-parametric in nautre and does not make assumptions about the underlying data
4. It is also more robust to outliers. Since we are dealing with financial delinquency there will potentially be lots of outliers that should not be removed. Hence, we need a more robust model.

## HYPERPARAMETER OPTIMSATION
Description of which hyperparameters you have and how you chose to optimise them. 

In hyperparameter tuning, I have chosen a Gridsearch approach to tune the hyperparameters of the Random Forest Classifier Model. The reason for this optimization is that it will perform an exhaustive search, and find the absolute best set of combinations based on the specified search space.

List of Hyperparameters tuned:
1. Max Depth
2. Minimum Samples Split
3. Minimum Samples Leaf
4. Maximum Features Considered
5. Number of estimators

## RESULTS
In summary, the performance of the model was analyzed based on the classification of whether an individual was deemed to be delinquent with days past due 90 days. In order to assess the model's performance, a few metrics was used. We used a general accuracy score and AUC ROC score to see how the model performs.

We also used a classification report to examine the precision and recall. As we can see in both the training and holdout set, the model has a higher precision but a lower recall but a lower recall for predicting delinquent individuals. This means that while the model does not effectively predict all delinquents, most of those it predicted as delinquent are accurate. The metrics summary report is shown below.

**EVALUATION ON TRAINING DATASET: (131143, 11)**

- Accuracy Score: 0.9385677242220867
- AUC ROC Score: 0.8581265408698437

CLASSIFICATION REPORT OF TRAINING SET:

               precision    recall  f1-score   support

     class 0       0.94      1.00      0.97     24573
     class 1       0.65      0.05      0.10      1651

    accuracy                           0.94     26224


**EVALUATION ON HOLDOUT (UNSEEN) DATASET: (29169, 11)**

- Accuracy Score: 0.9335757908460852
- AUC ROC Score: 0.8683670824829425

CLASSIFICATION REPORT OF HOLDOUT SET:

              precision    recall  f1-score   support

     class 0       0.93      1.00      0.97     13587
     class 1       0.65      0.04      0.08       986

    accuracy                           0.93     14573


## (OPTIONAL: CONTACT DETAILS)
Not Applicable

