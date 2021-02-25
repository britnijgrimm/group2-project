# group2-project
Final Project for Dataviz Bootcamp

The dataset we used is from Kaggle.com provided by JoniHoppen 
link to the data: ttps://www.kaggle.com/joniarroba/noshowappointments
Link to the license file: License:https://www.kaggle.com/joniarroba/noshowappointments

For the beginnind the idea is to put the excell file into Amazon services S3 then pull the data from there into Pandas
Uploaded the data to Amazon servers using S3

Data directory for original excell spreadsheet
PatientId-----   Identification of a patient 							int
AppointmentID----Identification of each appointment						int
Gender-----      Male or Female 										char
AppointmentDay---Day of actual appointment								date-time
ScheduledDay-----The day appointment made								date-time
Age---           Age of the patient										int
Neighbourhood----Where the appointment takes place						char						
Scholarship----  Is patient part of social welfare program of Brazil	char
Hipertension---	 If the patient has Hipertension						char
Diabetes----	 If the patient has Diabetes							char
Alcoholism----	 If the patient has Alcoholism							char
Handcap-----	 If the patient Handcapped								char
SMS_received---	 If the patient received SMS 							char
No-show-----	 If the patient showed up for appointment 				char




As the database in RDS publicly accessable with shared username and password team members can access to data anytime to pull and work with it.

So far all the connections are working however I (cirle person Ren ) am having trouble hiding the secret keys. So far I was not able to fix the issue. Next week we will work on hiding the keys if still does not work we will change the schema.



