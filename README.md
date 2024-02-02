# Reducing Hotel Cancellation Rates

The goal of the project was to address the challenge of high hotel cancellation rates by developing predictive models using logistic regression and decision trees. The chosen model for implementation was logistic regression due to its interpretability and effectiveness in binary classification tasks.

## Objective:
The primary objective was to create models that could accurately predict the likelihood of a hotel booking being canceled. By understanding the factors influencing cancellations, hotels could proactively manage reservations and optimize resource allocation.

The F1 Score was selected as the main metric to compare the model results as it is the harmonic mean of the precision and recall. It thus symmetrically represents both precision and recall in one metric.

## Data Collection:
A comprehensive dataset was collected over a two (2) year period, encompassing a range of features such as booking source, lead time, room type, and historical cancellation patterns. This dataset provided the necessary information to train and validate the predictive models.


## Exploratory Data Analysis (EDA):
Prior to model development, an exploratory data analysis was conducted to gain insights into the distribution of features, identify potential correlations, and understand patterns within the dataset. EDA played a crucial role in guiding feature selection and preprocessing, and it showed that most cancellations happened to reservations booked far in advance.

EDA focused on answering six (6) leading questions:

    1. What are the busiest months in the hotel?
    
![Popular_Months](https://github.com/DJEyerman/Hotel-Cancellation-Project/assets/38670302/1927ce62-5c00-440c-8bf1-cc42023f768b)

    • The busiest months for the hotel were between April 2018 and the end of October 2018.
    • September and October 2017 and 2018 also seem to be very popular.


    2. Which market segment do most of the guests come from?
![Cancellations](https://github.com/DJEyerman/Hotel-Cancellation-Project/assets/38670302/9f1fc97b-b7fc-4f25-87b4-9119b81301a6)

    • 63.99% of the guests come from the Online market segment
    • 29.02% from the Offline market segment


    3. What percentage of bookings are canceled?
![Overall_Cancel](https://github.com/DJEyerman/Hotel-Cancellation-Project/assets/38670302/3f780d39-d4fb-4ac8-8597-83e42d3189cd)

    • Not canceled: 67.23% 
    • Canceled: 32.76%


    4. Is there any correlation between booking lead time and cancellations?
![LeadTime_Cancel](https://github.com/DJEyerman/Hotel-Cancellation-Project/assets/38670302/cb8aa771-9f4b-459a-97c1-95c80a8103a3)

    • Bookings made with shorter lead times are less likely to cancel
    • Bookings made with a longer lead times are more likely to cancel 


    5. Repeating guests are the guests who stay in the hotel often and are important to brand equity. What percentage of repeating guests cancel?
  
![Repeat_Cancel](https://github.com/DJEyerman/Hotel-Cancellation-Project/assets/38670302/a93eb693-7304-4b0d-93bc-b801779cd9ab)

    • Less than 1% of repeating guests cancel. 


    6. Many guests have special requirements when booking a hotel room. Do these requirements affect booking cancellation?
![Special_Requests](https://github.com/DJEyerman/Hotel-Cancellation-Project/assets/38670302/2089b94d-6f02-4488-810f-18220150fb0a)

    • The more special requests, the high probably of a guest not canceling
    • 32.76% of guests without any special requests cancel their reservation 
    

## Data Preprocessing: 
    • The data did not include any null values. 
    • While the data did include some outliers, they were not treated as any treatment would fundamentally 
    change the data and therefore the results. 
    • Multicollinearity was tested and the VIF score for the data was under 5 indicating there is no 
    Multicollinearity in the data.  
    • Six (6) columns with a p-value greater and 0.05 were dropped from the data set. 


## Feature Engineering:
Based on insights from EDA, relevant features were selected and engineered to enhance the predictive power of the models. This step involved transforming and creating variables that better captured the complexities of the hotel booking process.


##Logistic Regression Model:
A logistic regression model was chosen for its simplicity and interpretability. This model was trained on the dataset to predict the probability of a booking resulting in a cancellation. Coefficients from the logistic regression aided in understanding the impact of each feature on the cancellation likelihood.

The logistic model was run with a default threshold of 0.5 and then with thresholds of 0.37 and 0.42.  

The threshold of 0.37 was determined by plotting a ROC-AUC curve on the training set and then computing the threshold. 

![ROC_Curve](https://github.com/DJEyerman/Hotel-Cancellation-Project/assets/38670302/6b890f8d-8625-4792-9bc2-95e794fb63cb)

The threshold of 0.42 was determined by plotting a Precision-Recall curve and interpreting the results. 

![Precision_Recall_Curve](https://github.com/DJEyerman/Hotel-Cancellation-Project/assets/38670302/a5aad7cd-258e-49c3-bb82-c50a3a7bd8d4)

The logistic regression model with a threshold of 0.42 had the best F1 Score, Recall, and Precision between the training and test data sets. 
![Logistic_Regression_Results](https://github.com/DJEyerman/Hotel-Cancellation-Project/assets/38670302/aab57dad-03ff-42cd-88c5-f04428065001)


## Decision Tree Model:
To improve model performance, a decision tree model was implemented. Decision trees excel in capturing nonlinear relationships and interactions among features. 

An initial decision tree was built to serve as a baseline for subsequent tuning of the model.  The F1 score of the baseline model was 0.991171 which points to an overfit model.  

The model was then tuned using the Pre-Pruning using GridSearchCV model with parameters to limit the maximum depth, maximum leaf nodes, and the minimum number of sample splits.  This yielded an F1 score of 0.753971 which is a definite improvement over the baseline F1 score, but there is still room for improvement. 

The model was then separately tuned using the Cost Complexity model to identify the decision tree branches that contributed the least to the overall model.  This yielded an F1 score of 0.856073 which is between the baseline F1 score and the pre-pruning F1 score.  

![Decision_Tree_Results](https://github.com/DJEyerman/Hotel-Cancellation-Project/assets/38670302/ba51b983-fc84-4318-b9f0-6f2fa46cdf86)


## Model Evaluation and Validation:
Both the logistic regression and decision tree models were rigorously evaluated using metrics such as accuracy, precision, recall, and the area under the Receiver Operating Characteristic (ROC) curve. The models were validated on a separate dataset to ensure generalizability.

The logistic regression model with a threshold of 0.42 had the best F1 Score, Recall, and Precision between the training and test data sets and therefore was selected as the model to implement. 


## Business Impact:
The Logistic Regression with a 0.42 Threshold successfully identified influential factors in hotel cancellations, offering valuable strategic insights. These insights empowered hotel management to implement targeted interventions, optimize pricing strategies, and enhance the overall customer booking experience.


## Actionable Insights:
    • Guests are more likely not to cancel if they make the reservation directly with the hotel
    • There are 46.08% of reservations with a lead time longer than 65 days
        ◦ Reservations with lead times longer than 60 days are 65% more likely to be canceled
    • There are 18.98% of reservations with a lead time of 10 days or less
        ◦ These reservations have the lowest chance of cancellations
    • The current cancellation rate is 32.76% which is lower than the average of 40%
    • Online booking cancellation rate is 71.31% of the total cancellations
        ◦ This is the largest source of cancellations
        ◦ Most likely, guests are booking at many hotels and selecting the one with the best rate
    • Offline booking cancellations rate is 26.53%


## Conclusion:
By employing decision trees as the core modeling technique, this data science project delivered a practical solution to the pervasive challenge of hotel booking cancellations. The insights gleaned from the model serve as a foundation for data-driven decision-making, allowing the hotel industry to proactively address and reduce cancellation rates.
