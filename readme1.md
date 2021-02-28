The dataset we used is from Kaggle.com provided by JoniHoppen 
link to the data: ttps://www.kaggle.com/joniarroba/noshowappointments
Link to the license file: License:https://www.kaggle.com/joniarroba/noshowappointments



<br>Uploaded the data to Amazon servers using S3
<html>
 <head>
   <title>Working with HTML Tables</title>
 </head>
 <body>
   <table>				<!-- create an table object -->
     <tr>				<!-- "tr" represents a row -->
       <th>Name</th>	<!-- use "th" to indicate header row -->
       <th>Date of Birth</th>
       <th>Weight</th>
     </tr> 
     <tr>				<!-- once again use tr for another row -->
       <td>Mary</td>	<!-- use "td" henceforth for normal rows -->
       <td>12/13/1994</td>
       <td>130</td>
     </tr>    
				
     <tr>
	     <th>Data directory for excell spreadsheet</th>
     </tr> 
	<tr><td>PatientId</td><td>Identification of a patient</td><td>int</td>
<br>-----   Identification of a patient 							int
<br>AppointmentID----Identification of each appointment						int
<br>Gender-----      Male or Female 								char
<br>AppointmentDay---Day of actual appointment							date-time
<br>ScheduledDay-----The day appointment made							date-time
<br>Age---           Age of the patient								int
<br>Neighbourhood----Where the appointment takes place						char						
<br>Scholarship----  Is patient part of social welfare program of Brazil	char
<br>Hipertension---	 If the patient has Hipertension						char
<br>Diabetes----	 If the patient has Diabetes							char
<br>Alcoholism----	 If the patient has Alcoholism							char
<br>Handcap-----	 If the patient Handcapped							char
<br>SMS_received---	 If the patient received SMS 							char
<br>No-show-----	 If the patient showed up for appointment 				        char
   </table>
 </body>
</html>
<table>
<br>
<br>
<br>We have read the csv data into Pandas and turned into dataframe;
<br>
<br>

<br>AppointmentID      int64
<br>Gender            object
<br>ScheduledDay      object
<br>AppointmentDay    object
<br>Age                int64
<br>Neighbourhood     object
<br>Scholarship        int64
<br>Hipertension       int64
<br>Diabetes           int64
<br>Alcoholism         int64
<br>Handcap            int64
<br>SMS_received       int64
<br>No-show           object
<br>dtype: object
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
<br>Neighbourhood    name of the Neighbourhood   					str
<br>Income			 median income for the area  				int
<br>lat, long        latitude and logitude of the neighborhoood			str
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
