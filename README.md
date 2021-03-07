# Machine Learning Model
## Description of preliminary data preprocessing
For the preliminary preprocessing the 'PatientId', 'AppointmentID', 'ScheduledDay', 'AppointmentDay', 'Neighbourhood' and 'TimeDelta' columns were dropped. The remaining columns all exist in numerical form. 

## Description of preliminary feature engineering and preliminary feature selection, including the decision-making process
### Processing
- Our dataframe was loaded into JupyterNotebook from a SQL server after it was pre-processed. The Appointments table from th SQL server was used as our primary dataset. The Avg_Neighbourhood_Data was extracted Neighbourhood_data SQL table and added as a data point. 

### Rejected Features
- The initial features selected were the previously processed data that were purely in numerical form. PatientID and Appointment ID would add noise for the regression models as their number values are unlikely to be relevent.  

### Selected Features
- The selected features of Gender,	Scholarship,	Hipertension,	Diabetes,	Alcoholism,	Handcap, Weekday,	SMS_received, Avg_Neighbourhood_Income and TimeDelta could all plausibly have an impact on the No-Show data and were thus used to make predictions.
- No-show	data was the variable we were predicting.

## Description of how data was split into training and testing sets
The data was split using the train_test_split function of the sklearn package using a 0.33 training data fraction.

## Explanation of model choice, including limitations and benefits
The model of choice is logistic regression. In comparison with random forest regression it shows a higher accuracy, f1-score and recall while having identical precision scores. 

## Model Training
- The logistic regression model has been trained on our training data from the train_test_split.
- Previously the model was tested on Gender, SCholarship, Hipertension, Diabetes, Alcoholism, Handicap, Weekday and SMS_received data.
- The factors of Avg_Neighbourhood_income and TimeDelta were added to the dataset. 

## Model Statistics
### Accuracy Score: 0.79
The model makes an accurate guess of the liklihood of No-Show 79% of the time. 
### Precision Score: 0.68
68% of the positives predicted are accurate.
### Recall Score: 0.79
79% of the total positive predictions are predicted.
### F1 - Score: 0.71
Indicates a good balance between recall and precision. 
