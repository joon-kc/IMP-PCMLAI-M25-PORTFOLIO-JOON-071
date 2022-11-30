# 90 Days Past Due - Predicting Financial Delinquency in Borrowers

## **NON-TECHNICAL EXPLANATION OF PROJECT**

This project focuses on predicting financial delinquency based on a borrower's credit or borrowing history. Essentially, we want to identify borrowers who are likely to be 90 days past due (dpd), and deny them the loan or service. These borrowers are assigned to the positive class (class 1). Thus, we want to train a classification model that can predict individuals in the positive class. Based on business requirements, our model should have a low false postive rate, as we only want to block those whom we are very confident about, as the first layer of defense.


## **DATA**
The data is derived from the "Give Me Some Credit" Kaggle competition hosted by Home Credit, as part of a prediction competition. The dataset can be found in the link below. The contains the historical data of Home Credit customers, with a total of 251503 rows, whereby 150000 records belong to the train set and 101503 records belong to test set that is used in submission. Since we are not entering the competition and merely building a pipeline, we will use the 150000 records for the purposes of this repository instead.

The data is stored in /give_me_some_credit_data/ folder. The main file used for training the model is cs-training.csv and it contains 150000 records.

Link to Kaggle Source:
(https://www.kaggle.com/competitions/GiveMeSomeCredit/overview)


## **MODEL** 
A summary of the model you’re using and why you chose it. 

The model that is used for this dataset training would be a Random Forest Classifier. The reason for choosing this is as follows:

1. It is easy to interpret by both technical and non-technical users, as we can follow the decision tree and its decision splits
2. Random Forests work well with both categorical and continuous data
3. It is non-parametric in nautre and does not make assumptions about the underlying data
4. It is also more robust to outliers. Since we are dealing with financial delinquency there will potentially be lots of outliers that should not be removed. Hence, we need a more robust model.

## **HYPERPARAMETER OPTIMSATION**
Description of which hyperparameters you have and how you chose to optimise them. 

In hyperparameter tuning, I have chosen a Gridsearch approach to tune the hyperparameters of the Random Forest Classifier Model. The reason for this optimization is that it will perform an exhaustive search, and find the absolute best set of combinations based on the specified search space.

Summary Table of Hyperparameters tuned:

| Hyperparameter | Variable Name | Definition |
| ------------- | ------------- | ------------- |
| Number of Estimators | `n_estimators`  | The number of trees in the forest  |
| Max Depth  | `max_depth`  | The maximum depth of the tree  |
| Minimum Samples Split | `min_samples_split` | The minimum number of samples required to split an internal node  |
| Maximum Leaf Nodes  | `max_leaf_nodes`  | Sets a condition on the splitting of the nodes in the tree and hence restricts the growth of the tree. Best nodes are defined as relative reduction in impurity  |
| Maximum Features  | `max_features`  | The number of features to consider when looking for the best split  |

## **RESULTS**

To recap, based on business strategy, our model should have a low false postive rate, as we only want to block those whom we are very confident belongs in the positive class. Thus, we want to identify as many true positives as possible. As we have other downstream underwriting risk strategies, we are less concerned about false negatives, as they will be captured later on.

Metrics used:
1. AUC-ROC: The ROC curve plots the True Positive Rate against the False Positive Rate at various threshold values. The Area Under the Curve (AUC) measures the classifier's ability to distinguish between classes. Generally speaking, the higher the AUC (closer to 1.0), the better the performance of the model in distinguishing between the positive and negative class.
2. Precision: Precision measures the ratio between the true positives and all the positives. 
3. Recall (Sensitivity): Recall measures the ratio of positive instances that are correctly detected.
4. Specificity: Refers to the probability that a true negative is correctly identified.
5. Accuracy score: Measures the number of correct predictions in relation to the total number of predictions made

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

## (OPTIONAL: CONTACT DETAILS)
Not Applicable

