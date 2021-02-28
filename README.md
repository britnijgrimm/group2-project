# Final Project
## Group 2: Miguel Diaz, Maya Singh, Ren Yildiz, and Britni Grimm
*Final Project for Dataviz Bootcamp*

### Communication Protcols
Because one of our members is located in India, we have been communicating through Slack, WhatsApp, and text message when necessary. We plan to meet one to two times per week via Zoom to discuss challenges, progress and request feedback from the team.

### Presentation
[Prelimary Google Slides draft](https://docs.google.com/presentation/d/1KnfV81sn4rcIU7k441lGYwDic_OFUhTXXSnzvUqHuO4/edit?usp=sharing)

[Preliminary Tablaeu Dashboard](https://public.tableau.com/profile/britni.grimm#!/vizhome/BrazilPublicHealthData/Dashboard1?publish=yes)

**Selected topic:** Attendance data for medical appointments in Brazil

**Reason why they selected their topic:** Miguel already had the data set in mind. Medical services are necessary for our health and well-being.

**Description of their source of data:** Dataset is available on Kaggle. Data provided by Aquarela Advanced Analytics (Brazil).

**Questions they hope to answer with the data:**
- Which neighborhood regions have higher attendance rates for appointments? Can this predict demand for physician services?
- If physicians can predict a certain percentage of no-shows for appointments, could they then schedule additional appointments for the day?
- Can physicians use this data to plan resources?
- Are there certain medical conditions that make patients more likely to show?
- Do age or gender correlate to no-show rates?
- Is Scholarship (social welfare programs) from the government encouraging patients to show for appointments?
- Do regular patients show up more than one-time patients? (This would need more data processing and we can consider it later)

# Machine Learning Model
## Description of preliminary data preprocessing
For the preliminary preprocessing the 'PatientId', 'AppointmentID', 'ScheduledDay', 'AppointmentDay', 'Neighbourhood' and 'TimeDelta' columns were dropped. The remaining columns all exist in numerical form. 

## Description of preliminary feature engineering and preliminary feature selection, including the decision-making process
### Rejected Features
- The initial features selected were the previously processed data that were purely in numerical form. PatientID and Appointment ID would add noise for the regression models as their number values are unlikely to be relevent. 
- ScheduledDay vs AppointmentDay can be used in the future by converting the data to the time between the two points (TimeDelta).
- Neighbourhood will be a useful future parameter to determine impact. 

### Selected Features
- The selected features of Gender,	Scholarship,	Hipertension,	Diabetes,	Alcoholism,	Handcap, Weekday and	SMS_received could all plausibly have an impact on the No-Show data and were thus used to make predictions.
- No-show	data was the variable we were predicting.

## Description of how data was split into training and testing sets
The data was split using the train_test_split function of the sklearn package using a 0.33 training data fraction.

## Explanation of model choice, including limitations and benefits
The model of choice is logistic regression. In comparison with random forest regression it shows a higher accuracy and a higher f-score. 
However, when 'Age' as a category is removed, both logistic regression and random forest regression have nearly identical measurements.

