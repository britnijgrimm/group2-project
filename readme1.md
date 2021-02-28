The dataset we used is from Kaggle.com provided by JoniHoppen 
link to the data: ttps://www.kaggle.com/joniarroba/noshowappointments
Link to the license file: License:https://www.kaggle.com/joniarroba/noshowappointments



Uploaded the data to Amazon servers using S3

Data directory for excell spreadsheet
PatientId-----   Identification of a patient 							int
AppointmentID----Identification of each appointment						int
Gender-----      Male or Female 								char
AppointmentDay---Day of actual appointment							date-time
ScheduledDay-----The day appointment made							date-time
Age---           Age of the patient								int
Neighbourhood----Where the appointment takes place						char						
Scholarship----  Is patient part of social welfare program of Brazil	char
Hipertension---	 If the patient has Hipertension						char
Diabetes----	 If the patient has Diabetes							char
Alcoholism----	 If the patient has Alcoholism							char
Handcap-----	 If the patient Handcapped							char
SMS_received---	 If the patient received SMS 							char
No-show-----	 If the patient showed up for appointment 				        char


We have read the csv data into Pandas and turned into dataframe;


AppointmentID      int64
Gender            object
ScheduledDay      object
AppointmentDay    object
Age                int64
Neighbourhood     object
Scholarship        int64
Hipertension       int64
Diabetes           int64
Alcoholism         int64
Handcap            int64
SMS_received       int64
No-show           object
dtype: object

1-After checking all the unique values AppointmentID became index column

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
Second data file is file we have created by collecting data from Kaggle and google maps. The file contains the neighborhoods median incomes adn lat and long information. This info could help us to crete an interactive map also we could income information for our predictions.

Data Directory for "mean_income_of_neighborhoods.csv"

Neighbourhood    name of the Neighbourhood   					str
Income			 median income for the area  				int
lat, long        latitude and logitude of the neighborhoood			str

We have read the file into pandas dataframe as min_df

Median Income     int64
Lat,  Long       object
dtype: object

Checked for null values 

After data manupulation; a copy of csv file saved to original folder then created connection with PGAdmin uploaded those files as  Appointments and Neighbourhood_data tables.

mans_df.to_sql------name="Appointments" table 
min_df.to_sql  ---- name="Neighbourhood_data" table 

![](https://github.com/britnijgrimm/group2-project/blob/datamanupulation/pgadmintables.JPG)

![](https://github.com/britnijgrimm/group2-project/blob/datamanupulation/Tableau_connection.JPG)
