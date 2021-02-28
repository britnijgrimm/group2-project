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
