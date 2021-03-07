# Final Project
### Group 2: Miguel Diaz, Maya Singh, Ren Yildiz, and Britni Grimm
*Final Project for Dataviz Bootcamp*

## Presentation
[Working Google Slides Presentation Draft](https://docs.google.com/presentation/d/1KQvsMLWR1pu0SqHGXU11xStyfQeG35imJ3Y69KPRyFs/edit#slide=id.gc56ac6f202_2_5)

## Dashboard
[Storyboard in Google Slides](https://docs.google.com/presentation/d/1yOO8OgxVIXWpHmmV2ujA7bumW2M0-66zk7i5WoHMizA/edit#slide=id.gc397379e9a_0_118)

[Preliminary Tableau Dashboard](https://public.tableau.com/profile/ren5313#!/vizhome/NeighbourhoodData/AgevsNo_sh0w?publish=yes)

**Selected topic:** Attendance data for medical appointments in Brazil

**Reason why we selected our topic:** One of our team members had pre-selected this dataset. The group agreed that exploring medical appointment attendence data is of the essence with the recent strain COVID-19 has placed on healthcare networks scross the globe.

**Description of our source of data:** Dataset is available on [Kaggle](https://www.kaggle.com/joniarroba/noshowappointments). Data provided by JoniHoppen with Aquarela Advanced Analytics (Brazil).

**Questions we set out to answer through exploratory and machine learning analysis this data:**
- Which neighborhood regions have higher attendance rates for appointments? Can this predict demand for physician services?
- Can physicians can predict a certain percentage of no-shows for appointments? Could they then schedule additional appointments for the day?
- Can physicians use this data to plan resources such as nurses and support staff?
- Are there certain medical conditions that are more likely to cause patients to miss appointments?
- Do age or gender correlate to no-show rates?
- Can we determine if Scholarship via [Bolsa Família](https://en.wikipedia.org/wiki/Bolsa_Fam%C3%ADlia) from the encouraging patients to show for appointments?)
- Do returning patients show up more than one-time patients? (This would need more data processing and we can consider it later)
- Do regular patients show up more than one-time patients? (This would need more data processing and we can consider it later)

## Machine Learning Model
### Description of preliminary data preprocessing
For the preliminary preprocessing the 'PatientId', 'AppointmentID', 'ScheduledDay', 'AppointmentDay', 'Neighbourhood' and 'TimeDelta' columns were dropped. The remaining columns all exist in numerical form. 

### Description of preliminary feature engineering and preliminary feature selection, including the decision-making process
**Processing**
- Our dataframe was loaded into JupyterNotebook from a SQL server after it was pre-processed. The Appointments table from th SQL server was used as our primary dataset. The Avg_Neighbourhood_Data was extracted Neighbourhood_data SQL table and added as a data point. 

**Rejected Features**
- The initial features selected were the previously processed data that were purely in numerical form. PatientID and Appointment ID would add noise for the regression models as their number values are unlikely to be relevent.  

**Selected Features**
- The selected features of Gender,	Scholarship,	Hipertension,	Diabetes,	Alcoholism,	Handcap, Weekday,	SMS_received, Avg_Neighbourhood_Income and TimeDelta could all plausibly have an impact on the No-Show data and were thus used to make predictions.
- No-show	data was the variable we were predicting.

### Description of how data was split into training and testing sets
The data was split using the train_test_split function of the sklearn package using a 0.33 training data fraction.

### Explanation of model choice, including limitations and benefits
The model of choice is logistic regression. In comparison with random forest regression it shows a higher accuracy, f1-score and recall while having identical precision scores. 

### Model Training
- The logistic regression model has been trained on our training data from the train_test_split.
- Previously the model was tested on Gender, SCholarship, Hipertension, Diabetes, Alcoholism, Handicap, Weekday and SMS_received data.
- The factors of Avg_Neighbourhood_income and TimeDelta were added to the dataset. 

### Model Statistics
**Accuracy Score: 0.79**
The model makes an accurate guess of the liklihood of No-Show 79% of the time. 
**Precision Score: 0.68**
68% of the positives predicted are accurate.
***Recall Score: 0.79**
79% of the total positive predictions are predicted.
**F1 - Score: 0.71**
### Accuracy Score: 0.79
The model makes an accurate guess of the liklihood of No-Show 79% of the time. 
### Precision Score: 0.68
68% of the positives predicted are accurate.
### Recall Score: 0.79
79% of the total positive predictions are predicted.
### F1 - Score: 0.71
Indicates a good balance between recall and precision. 

The model of choice is logistic regression. In comparison with random forest regression it shows a higher accuracy and a higher f-score. 
However, when 'Age' as a category is removed, both logistic regression and random forest regression have nearly identical measurements.


## Data pre-processing for No Show Medical Appointments

<br>Uploaded the data to Amazon servers using S3
Data Header	Data Meaning				Type

![image](https://user-images.githubusercontent.com/55123056/109426497-cd3e3100-79a2-11eb-93b8-171c27b0ca44.png)
			

<br>
<br>We have read the csv data into Pandas and turned into dataframe;
<br>
<br>


![image](https://user-images.githubusercontent.com/55123056/109426109-a0891a00-79a0-11eb-9381-e19d67004f83.png)

<br>
<br>1-After checking all the unique values AppointmentID became index column

		len(mans_df.AppointmentID.unique())
		mans_df.set_index('AppointmentID', inplace = True)
		
2-Checked for all null values

		for column in mans_df.columns:
		print(f"Column {column} has {mans_df[column].isnull().sum()} null values")
		
3-Replaced date-time with date

		mans_df["ScheduledDay"] = pd.to_datetime(mans_df.ScheduledDay)
		mans_df["AppointmentDay"] = pd.to_datetime(mans_df.AppointmentDay)
		
		
4-Created AppointmentDay column by day number

		WeekDay=mans_df["AppointmentDay"].dt.weekday
		mans_df["WeekDay"]=WeekDay


5-Created TimeDelta by calculating the difference between appointmentday and scheduledday

		time_delta=mans_df.AppointmentDay.dt.dayofyear-mans_df.ScheduledDay.dt.dayofyear
		
		
6-Gender and No-show columns turned into integer values

		mans_df['Gender'] = mans_df['Gender'].map({'F': 1, 'M': 0})
		mans_df['No-show'] = mans_df['No-show'].map({'No': 1, 'Yes': 0})

7-Turned the data to csv

 to get a copy before sending to sql


.......................................................................
<br>Second data file is file we have created by collecting data from Kaggle and google maps. The file contains the neighborhoods median incomes adn lat and long information. This info could help us to crete an interactive map also we could income information for our predictions.
<br>
<br>Data Directory for "mean_income_of_neighborhoods.csv"
<br>
![image](https://user-images.githubusercontent.com/55123056/109426845-818c8700-79a4-11eb-8226-c751609a3efe.png)

<br>
<br>
We have read the file into pandas dataframe as min_df
<br>
<br>
<br>Median Income     int64
<br>Lat,  Long       object
<br>dtype: object

<br>Checked for null values 

<br>After data manupulation; a copy of csv file saved to original folder then created connection with PGAdmin uploaded those files as  Appointments and Neighbourhood_data tables.

<br>mans_df.to_sql------name="Appointments" table 
<br>min_df.to_sql  ---- name="Neighbourhood_data" table 

<br>![](https://github.com/britnijgrimm/group2-project/blob/datamanupulation/pgadmintables.JPG)

<br>![](https://github.com/britnijgrimm/group2-project/blob/datamanupulation/Tableau_connection.JPG)
