# Datasheet Summary

## Motivation

- For what purpose was the dataset created? 

The dataset was created by Home Credit and the aim is to build a model dataset that borrowers can use to help make the best financial decisions. As this dataset is hosted as a Kaggle competition, the secondary aim of creating this dataset is to also see the approaches in creating a model that can help predict the probability that somebody will experience financial distress in the next two years. 
This in part to improve the state of the art in credit scoring.

- Who created the dataset (e.g., which team, research group) and on behalf of which entity (e.g., company, institution, organization)? Who funded the creation of the dataset?


The dataset comes from Home Credit, which is an international non-bank financial institution founded in 1997 in the Czech Republic and headquartered in Netherlands.The company operates in 9 countries and focuses on installment lending primarily to people with little or no credit history. It is most likely that Home Credit funded the creation of the dataset, as they used their Historical data on their own borrowers as part of the competition.
 
## Composition

- What do the instances that comprise the dataset represent (e.g., documents, photos, people, countries)? 

The dataset consists of individuals who have utilized Home Credit's borrowing service. We do not know the gender as this was not specified in the dataset. For each instance, it contains documents of borrowers financial history made up of the following:
 1. RevolvingUtilizationOfUnsecuredLines: Total balance on credit cards and personal lines of credit except real estate and no installment debt like car loans divided by the sum of credit limits
 2. Age: Age of borrowers in years
 3. NumberOfTime30-59DaysPastDueNotWorse: Number of times borrower has been 30-59 days past due but no worse in the last 2 years.
 4. DebtRatio: Monthly debt payments, alimony,living costs divided by monthy gross income
 5. MonthlyIncome: Individual's monthly income
 6. NumberOfOpenCreditLinesAndLoans: Number of Open loans
 7. NumberOfTimes90DaysLate: Number of times borrower has been 90 days or more past due.
 8. NumberRealEstateLoansOrLines: Number of mortgage and real estate loans including home equity lines of credit
 9. NumberOfTime60-89DaysPastDueNotWorse: Number of times borrower has been 60-89 days past due but no worse in the last 2 years.
 10. NumberOfDependents: Number of dependents in family excluding themselves (spouse, children etc.)

 Each instance also contains a single binary outcome variable "SeriousDlqin2yrs", {0, 1}, where "1" represents the fact the individual is a person who experienced 90 days past due delinquency or worse. 


- How many instances of each type are there? 

There a total of 251503 instances, whereby 150000 instances belong to the train set and 101503 instancesbelong to test set that is used in submission. Since we are not entering the competition and merely building a pipeline, we will use the 150000 records for the purposes of this repository instead.

- Is there any missing data?

Yes among the 150000 instances that we are using for this project, there are 29731 missing values for "MonthlyIncome" and 3924 missing values for "NumberOfDependents"

- Does the dataset contain data that might be considered confidential (e.g., data that is protected by legal privilege or by    doctor–patient confidentiality, data that includes the content of individuals’ non-public communications)?

Yes, as this dataset contains some credit information or data on individuals borrowing behaviour, which is usually considered as confidential.

## Collection process

- How was the data acquired?

The assumption was that the data was acquired from Home Credit's own pool of borrowers. Apart from this little else is known of the data acquisition process as no other information is provided.

- If the data is a sample of a larger subset, what was the sampling strategy? 

The data is a sample of a larger subset, but there is no information provided on the sampling strategy.

- Over what time frame was the data collected?

There is no information over what time frame was this data collected.

## Preprocessing/cleaning/labelling

- Was any preprocessing/cleaning/labeling of the data done (e.g., discretization or bucketing, tokenization, part-of-speech tagging, SIFT feature extraction, removal of instances, processing of missing values)? If so, please provide a description. If not, you may skip the remaining questions in this section. 

There is no mention if there was any preprocessing/cleaning/labeling of the data done prior to publishing.

- Was the “raw” data saved in addition to the preprocessed/cleaned/labeled data (e.g., to support unanticipated future uses)? 

There is not enough information as to whether the "raw" data was saved, this information is not publicly available.
 
## Uses

- What other tasks could the dataset be used for? 

This datasets could be used for exploratory data analysis or benchmarking financial delinquency algorithms that depend on the same attributes. Alternatively, it could be used to benchmark credit scoring algorithms.

- Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses? For example, is there anything that a dataset consumer might need to know to avoid uses that could result in unfair treatment of individuals or groups (e.g., stereotyping, quality of service issues) or other risks or harms (e.g., legal risks, financial harms)? If so, please provide a description. Is there anything a dataset consumer could do to mitigate these risks or harms? 

There is no public information if there was anyway in which the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses


- Are there tasks for which the dataset should not be used? If so, please provide a description.

The dataset was used to predict financial delinquency for a very specific subset of borrowers. As there is little information on the collection and distribution of demographics, it is not ideal to make any assumptions about this. As such, it should ideally be only used to predict serious financial delinquency in 2 years, within the context of the dataset described above. It should not be used in predicting new populations since we are unsure of the data's representativeness.

## Distribution

- How has the dataset already been distributed? 

The dataset was distributed on Kaggle as part of a prediction competition.

- Is it subject to any copyright or other intellectual property (IP) license, and/or under applicable terms of use (ToU)?  

There is no public information, but since it is on Kaggle it can be assumed to be under a C00: Public Domain license.

## Maintenance

- Who maintains the dataset?

As far as public information goes, it is assumed that the dataset is not maintained since 11 years ago when the competition was held.
