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

<h2>Data origin and manupulations for No Show Medical Appointments Group2 project</h2>

The dataset we used is from Kaggle.com provided by JoniHoppen 
link to the data: ttps://www.kaggle.com/joniarroba/noshowappointments
Link to the license file: License:https://www.kaggle.com/joniarroba/noshowappointments



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