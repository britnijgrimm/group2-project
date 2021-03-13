# Final Project
### Group 2: Miguel Diaz, Maya Singh, Ren Yildiz, and Britni Grimm
*Final Project for Dataviz Bootcamp*

## Presentation
[Presentation](https://docs.google.com/presentation/d/1KQvsMLWR1pu0SqHGXU11xStyfQeG35imJ3Y69KPRyFs/edit#slide=id.gc56ac6f202_2_5)

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

## Dashboard
[Storyboard in Google Slides](https://docs.google.com/presentation/d/1yOO8OgxVIXWpHmmV2ujA7bumW2M0-66zk7i5WoHMizA/edit#slide=id.gc397379e9a_0_118)

[Tableau Dashbaord](https://public.tableau.com/profile/britni.grimm#!/vizhome/NeighbourhoodData_16152641297450/FinalDash?publish=yes)

After designing and confirming the connections we have started working on our dashbard and visuals.

![Data](https://github.com/britnijgrimm/group2-project/blob/dashbord/screenshots/full%20data.JPG)


### Pulling Data and Woking with Data 
We pulled the data from AWS with orginal connection;

Lattidue and Longitude field needed some attention.  We had to split lat,long field on Neighbourhood_data table also change the data type from text to geographical.

Then we created different dashbords with income, age, gender, vs No show data and created our storybord. 
You can access the dashbourd at following address.

![tableau_map](https://github.com/britnijgrimm/group2-project/blob/dashbord/screenshots/Neighbourhood%20Info.JPG)


If you look at the data you will recognize that income, age , sex are the top data points affecting the cancelations. The topic will be expalined in details in our main presentaion.

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

