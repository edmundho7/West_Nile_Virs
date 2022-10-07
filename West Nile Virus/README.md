# Project 4 - West Nile Virus Prediction

## Introduction
West Nile virus (WNV) is the leading mosquito-borne disease in the United States West Nile virus is most commonly spread to humans through infected mosquitos. Around 20% of people who become infected with the virus develop symptoms ranging from a persistent fever, to serious neurological illnesses that can result in death.


In 2002, the first human cases of West Nile virus were reported in Chicago. By 2004 the City of Chicago and the Chicago Department of Public Health (CDPH) had established a comprehensive surveillance and control program that is still in effect today.

Every week from late spring through the fall, mosquitos in traps across the city are tested for the virus. The results of these tests influence when and where the city will spray airborne pesticides to control adult mosquito populations.

For this Kaggle competition, we are given weather, location, testing, and spraying data. The purpose of this challenge is to predict when and where different species of mosquitos will test positive for West Nile virus. In turn, solving our Problem Statement.

## Problem Statement

West Nile Virus (WNV) is the leading cause of mosquito-borne disease in the continental United States. It is most commonly spread to people by the bite of an infected mosquito and there are no vaccines to prevent or medications to treat WNV in people. 

As a group of Data Scientist from Chicago Department of Public Health (CDPH), we will predict when and where different species of mosquitos will test positive for West Nile Virus Through our studies, we hope to help the City of Chicago and CPHD to have more cost-efficient and effective way of deploying pesticides in order to prevent transmission of this potentially deadly virus. 

## Datasets
-	Train and Test Data
-	Spray Data
-	Weather Data
-	Map Data


##	Data Imbalance

As the given data is heavily imbalanced, with 95% of the data indicated as negative WNV, resulting in poor performance from predicting the positive WNV cases.  
In order to address the issue of data imbalance, an over-sampling method called SMOTE (Synthetic Minority Oversampling Technique) is adopted for all the classifier models. As such, AUC score will be the main metrics used to assess the best model as compared accuracy.

## Model Evaluation/Metrics
|   Model |   Train score |   Test score |   Generalisation |   Accuracy |   Precision |   Recall |   Specificity |      F1 |   ROC AUC |
|--------------:|--------------:|-------------:|-----------------:|-----------:|------------:|---------:|--------------:|--------:|----------:|
|Logistic Regression (no SMOTE|         0.947 |        0.946 |            0.106 |      0.946 |       0.5     |    0.015     |         0.999 | 0.029     |    0.8203 |
|Logistic Regression|         0.957 |        0.928 |            3.030  |      0.928 |       0.253 |    0.182 |         0.970  |   0.212 |    0.7949 |
|Random Forest Classification|         0.951 |        0.866 |           8.938 |      0.866 |       0.171 |    0.394 |         0.892 |   0.238 |    0.8208 |
|Decision Tree Classification|         0.985 |        0.878 |           10.863 |      0.878 |       0.142 |    0.255 |         0.913 |   0.182  |    0.5997 |
|Multinomial Naive Bayes Classification|         0.834 |        0.785 |            5.875 |      0.785 |       0.152 |    0.664          |0.791 |   0.247 |    0.8181 |
|k-Nearest Neighbour Classification|         0.901 |        0.638 |           29.190 |      0.638 |       0.088 |    0.613 |         0.640 |   0.154 |    0.6813  |
|AdaBoost Classification|        0.960 |        0.913 |            4.167 |      0.913 |       0.224 |    0.241 |         0.950 |   0.242 |    0.8328 |
|XGBoost Classification|         0.969 |        0.889 |            8.256 |      0.889 |       0.187 |    0.321 |         0.921 |   0.236 |    0.8319 |
|Gradient Boosting Classification|         0.981 |        0.915 |            6.728 |      0.915 |       0.199 |    0.197 |         0.955 |   0.198 |    0.8000 |

Classification models, unlike regression models have multiple metrics which results may be based on. Accuracy is used when the True Positives and True negatives are more important while F1-score is used when the False Negatives and False Positives are crucial. F1 score is usually handy for imbalanced datasets (as its calculated based on Precision and Recall). Lastly, for the area under curve of a ROC curve, it measures the usefulness of a test in general, where a greater area means a more useful test, the areas under ROC curves are used to compare the usefulness of tests. AUC metric measure performance for the classification problem at various threshold settings.

For the purpose of solving our problem statement, we will be considering the following criterias to select the best performing model:

1. ROC AUC score > 0.8 
2. Generalisation < 5% 
3. F1 score 

<br>Based on the above criterias, we have selected AdaBoost+SMOTE. 

- **ROC AUC** of 0.8328 infers that the model has a good capability of classifying the positive class in the dataset.
- **Generalisation Score** of 4.167% means that the model has the ability to properly adapt to new, previously unseen data, drawn from the same distribution as the one used to create the model.
- **Recall** of 0.241. The high recall score means our modell succeeds well in finding all the positive cases in the data, even though it may also wrongly identify some negative cases as positive cases.
- **F1 score** of 0.242. As F1 Score is an average of Precision and Recall, it means that the F1 score gives equal weight to Precision and Recall. All the models does not have a great F1 Score. However, our model has a good balance of both Precision and Recall. 

## Conclusion 
Using ADABoost (our best performing model), we achieved an ROC_AUC score of  0.8328 and F1 score of 0.242. Feature importance of our model showed that location features (Latitude & Longitude) as well as weather features (DewPoint, ResultDir, Temperature & SunHours) ranked the highest. This indicates that WNV is most likely to occur at given locations and under certain weather conditions. Our interpretation for these features to score high could be attributed to denser locations which gives the mosquitoes more opportunities for breeding as well as seasonal cycles where temperatures are ideal for the Culex species to thrive such as Summer. Therefore spray efforts should be concentrated at these locations when weather conditions are right.


## Recommendations
1. Through our cost-benefit analysis, the projected cost of spraying would be financially justified as long as it prevents more than 64 individuals from being hospitalized due to the West Nile Virus.

2. Though our costing assumptions are completely straightforward, we believe that there are other more cost-effective techniques that may be applied in conjunction to spraying such as creating awareness amongst the community. These initiatives may be performed through campaigns, education programs and home visits/checks.

3. Explore further in detail on deploying targeted spray areas from our model predictions. This will in turn help directly reduce the cost of spraying efforts across Chicago (such as the random spray cluster at High Ridge Knolls Park). However, as the current spray datasets does not substantially quantify the spraying efforts, more evidence (from a better designed and documented spraying regime) would be recommended.


