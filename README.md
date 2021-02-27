# Machine Learning Model
## Description of preliminary data preprocessing
For the preliminary preprocessing the 'PatientId', 'AppointmentID', 'ScheduledDay', 'AppointmentDay', 'Neighbourhood' and 'TimeDelta' columns were dropped. The remaining columns all exist in numerical form. 

## Description of preliminary feature engineering and preliminary feature selection, including the decision-making process

## Description of how data was split into training and testing sets
The data was split using the train_test_split function of the sklearn package using a 0.33 training data fraction.

## Explanation of model choice, including limitations and benefits
The model of choice is logistic regression. In comparison with random forest regression it shows a higher accuracy and a higher f-score. 
However, when 'Age' as a category is removed, both logistic regression and random forest regression have nearly identical measurements.
