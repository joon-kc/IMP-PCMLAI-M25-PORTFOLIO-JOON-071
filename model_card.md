# Model Card 

## Model Description

**Input:** Describe the inputs of your model 

The inputs of the model consists of the following features, associated with an individual's demographic and past borrowing behaviour:

 1. RevolvingUtilizationOfUnsecuredLines (FLOAT): Total balance on credit cards and personal lines of credit except real estate and no installment debt like car loans divided by the sum of credit limits
 2. Age (INT): Age of borrowers in years
 3. NumberOfTime30-59DaysPastDueNotWorse (INT): Number of times borrower has been 30-59 days past due but no worse in the last 2 years.
 4. DebtRatio (FLOAT): Monthly debt payments, alimony,living costs divided by monthy gross income
 5. MonthlyIncome (FLOAT): Individual's monthly income
 6. NumberOfOpenCreditLinesAndLoans (INT): Number of Open loans
 7. NumberOfTimes90DaysLate (INT): Number of times borrower has been 90 days or more past due.
 8. NumberRealEstateLoansOrLines (INT): Number of mortgage and real estate loans including home equity lines of credit
 9. NumberOfTime60-89DaysPastDueNotWorse (INT): Number of times borrower has been 60-89 days past due but no worse in the last 2 years.
 10. NumberOfDependents (INT): Number of dependents in family excluding themselves (spouse, children etc.)

**Output:**

The output of the model consists of a binary classification of either 1 or 0, where "1" represents the positive class, that the individual experienced 90 days past due delinquency or worse. This classification is based on the predicted probabilities that each class belongs to. We can influence the output by adjusting the threshold value (0 to 1), and any probability of belonging in class 1 that exceeds the threshold will be classified as 1.

**Model Architecture:**

The model uses a Random Forest Classifier. Random forest (RF) models make output predictions by combining outcomes from a forest of decision trees (estimators). Below shows a sample architecture of how one of the estimator tree in a random forest looks like. Our decision tree as a maximum depth of 3 with no further splits after that. Diagram below shows the architecture of one of the many decision tree from our random forest

![Screenshot](rf_individualtree.png)

## Performance

To recap, based on business strategy, our model should have a low false postive rate, as we only want to block those whom we are very confident belongs in the positive class. Thus, we want to identify as many true positives as possible. As we have other downstream underwriting risk strategies, we are less concerned about false negatives, as they will be captured later on.

In order to assess the model's performance, we used the following metrics as summarized below. Also, as we are using the underlying predicted probabilities of each class, we set the threshold for defining the positive class. The summary table below uses the default threshold of 0.5. 

**Here we present the summary metrics of the Random Forest Model trained on different data:**
1. Normal Model - Random Forest Model trained on normal training data with no oversampling.
2. Oversampled Model - Random Forest Model trained on training data generated from oversampling

**EVALUATION METRICS SUMMARY TABLE (NORMAL) - Model trained on non-oversampled data**

| Evaluation Metric | Training Data | Test Data |
| ------------- | ------------- | ------------- |
| Accuracy  | 0.93587  | 0.93438  |
| ROC-AUC  | 0.851 | 0.85383  |
| Sensitivity  | 0.01388  | 0.01042  |
| Specificity  | 0.99989  | 0.99927  |
| Precision-Recall (class 0)  | 0.935-0.999  | 0.935-0.999  |
| Precision-Recall (class 1)  | 0.500-0.010  | 0.500-0.010  |

**EVALUATION METRICS SUMMARY TABLE (OVERSAMPLING) - Model trained on oversampled data**

| Evaluation Metric | Training Data | Test Data |
| ------------- | ------------- | ------------- |
| Accuracy  | 0.74012  | 0.74299  |
| ROC-AUC  | 0.85023 | 0.85814  |
| Sensitivity  | 0.79958  | 0.79167  |
| Specificity  | 0.73592  | 0.73958 |
| Precision-Recall (class 0)  | 0.981-0.736  | 0.981-0.740  |
| Precision-Recall (class 1)  | 0.176-0.800  | 0.176-0.792  |

Based on the above, the overall better performing model is the one that is trained on the oversampled data. Although, it has a lower accuracy on the test set, it outperforms the model trained on non-oversampled data in terms of recall. Recall is important to our business strategy as we want to correctly identify individuals in the positive class, given that they are will be 90 days dpd. The model trained on oversampled data also has a more balanced sensitivity and specificity as compared to the model trained on non-oversampled data.


## Limitations

The following factors may degrade the model's performance

1. Extreme Values: Extreme values in some of the specified features can lead to poor predictability especially if these values were not captured in the training data
2. Missing Salary: Missing values in the salary input can lead to poor predictability, as the current strategy assumes that missing values are filled with the median salary
3. Age: Model can only make predictions on individuals older than 18 years old
4. Number of dependents: Missing values for number of dependents will default to 0 during model prediction


## Trade-offs

Models can exhibit performance issues under certain circumstances. Here, we list potential situations where this may occur, and the user should plan accordingly.

1. Random forest models are prone to overfitting and while it will perform well on this dataset, one should be cautious about its accuracy on newer data. Thus, we need to monitor model drift and population stability indexes to measure how much there newer data deviates from the training data
2. Model in general has a high recall for the positive class (Class 1). Thus, the model will excel in conditions where we need to confidently identify true positives at the risk of some false negatives. Model performance will suffer when the strategy calls for higher precision.