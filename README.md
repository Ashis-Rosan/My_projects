# Airline Passengers Satisfactions SQL Project

## Project Overview

**Project Title**: Airline Customers Satisfactions.

Airline Passengers Satisfaction Analysis
This project demonstrates my SQL skills in exploring and analyzing real-world airline Passengers feedback data.
I cleaned the dataset, performed Exploratory Data Analysis (EDA), and answered key business questions using SQL.
This project helped me strengthen my practical data analysis skills and build a solid foundation in SQL.

## Objectives.

**1.** **Set up a retail sales database:-** Create a database and add the given Airline details into it.  
**2.** **Clean the data:-** Find and remove duplicates and any rows that have missing or null values.  
**3.** **Do basic exploratory data analysis (EDA):-** Look at the data to understand patterns, totals, averages, and any odd values.  
**4.** **Answer business questions with SQL:-** Write SQL queries to get useful insights from the Aireline Data.  


## Project Structure.

### 1. Database Setup:-
- **Database creation:-** First, make a database called `Airline_details.`  
- **Table creation:-** Inside that database, create a table also called `Airline_details` to hold the customer data. The table will have columns for different pieces of information such as **:-** ID,	Gender,	Age, Customer_Type,	Type_of_Travel,	Class, Flight_Distance,	Departure_Delay, Arrival_Delay,	Departure_and_Arrival_Time_Convenience,	Ease_of_Online_Booking,	Check_in_Service, Online_Boarding, Gate_Location, On_board_Service, Seat_Comfort, Leg Room_Service, Cleanliness	,Food_and_Drink	In_flight_Service, In_flight_Wifi_Service, In_flight_Entertainment, Baggage_Handling, Satisfaction.  

 ```SQL
CREATE TABLE Airline_details;

create table airline_details(
ID	          int primary key,
Gender	      varchar(10),
Age	           int,
Customer_Type  varchar(30),	
Type_of_Travel	varchar(30),
Class	          varchar(30),
Flight_Distance 	int,
Departure_Delay 	 int,
Arrival_Delay	    int,
Departure_and_Arrival_Time_Convenience int,	
Ease_of_Online_Booking	 int,
Check_in_Service	       int,
Online_Boarding	         int,
Gate_Location            int, 	
On_board_Service	       int,
Seat_Comfort	            int,
Leg_Room_Service	         int,
Cleanliness           	int, 
Food_and_Drink       	int,
In_flight_Service      	int,
In_flight_Wifi_Service    int,	
In_flight_Entertainment  	int,
Baggage_Handling	      int,
Satisfaction         varchar(35)
);
```


### 2. Data Exploration & Cleaning:-

- **Data Count:** Count how many rows (records) are in the dataset. This tells you the total number of entries.  
- **Customer Count:** Count how many different Passengers are in the dataset. This shows the number of unique Passengers.  
- **Category Count:** Find all the different categories (for example, seat class or service type) in the dataset and count them. This tells you how many distinct categories exist.  
- **Null Value Check:** Look for blank or missing values in the data. If a row has missing important information, delete that row so the dataset is clean and accurate.

  ```SQL
  Data count:
  SELECT COUNT(*) FROM Airline_details;

  How many different Passengers :
  SELECT COUNT(DISTINCT Id) FROM Airline_details;

  Customers types:
  SELECT DISTINCT Customer_Type FROM Airline_details;
  
  Type of travels:
  SELECT DISTINCT Type_of_Travel FROM Airline_details;
  
  Finding null Values:
  
   SELECT * FROM airline_details
  WHERE ID	is null
    or Gender	is null
    or Age is null
    or Customer_Type is null	
    or Type_of_Travel	is null
    or Class	is null
    or Flight_Distance	is null
    or Departure_Delay	is null
    or Departure_and_Arrival_Time_Convenience is null
    or Ease_of_Online_Booking	is null
    or Check_in_Service	is null
    or Online_Boarding	is null
    or Gate_Location is null 	
    or On_board_Service	is null
    or Seat_Comfort	is null
    or Leg_Room_Service	is null
    or Cleanliness	is null
    or Food_and_Drink	is null
    or In_flight_Service	is null
    or In_flight_Wifi_Service  is null	
    or In_flight_Entertainment	is null
    or Baggage_Handling	is null
    or Satisfaction  is null ;
  
### 3. Data Analysis & Business Questins:-
These SQL queries were written to answer important business questions. Each query gets a specific piece of information from the data to help the airline understand customers and improve services.
  1. **What is the overall customer satisfaction rate?**
  ```SQL
  SELECT
    Satisfaction,
    COUNT(*) AS Total_Customers,
    ROUND(COUNT(*) * 100.0 / SUM(COUNT(*)) OVER(),2) AS Percentage
  FROM airline_details
  GROUP BY Satisfaction;
```
**Only about 43.4% customers are satisfied, while 56.6% are dissatisfied.**

   2. Which travel class has the highest satisfaction?
```SQL
SELECT
    Class,
    Satisfaction,
    COUNT(*) AS Total
FROM airline_details
GROUP BY Class, Satisfaction;
```
**Business-class customers are the happiest group. There are 10,943 business-class customers in total, and they have the highest satisfaction compared to other classes.**

3. Which travel class has the most dissatisfied customers?
```SQL
SELECT
    Class,
    COUNT(*) AS Dissatisfied_Customers
FROM airline_details
WHERE Satisfaction='Neutral or Dissatisfied'
GROUP BY Class;
```
**Economy-class customers are the most unhappy group with the total number of 18,994.**  

4. Which age group is most satisfied?
   
```SQL
SELECT
type_of_travel,
    CASE
        WHEN Age < 25 THEN 'Young'
        WHEN Age BETWEEN 25 AND 45 THEN 'Adult'
        ELSE 'Senior'
    END AS Age_Group,
    Satisfaction,
    COUNT(*) AS Customers
FROM airline_details
GROUP BY type_of_travel,Age_Group, Satisfaction;
```
**Middle-aged (Adult) business travelers are usually happier with the airline**   

5. Do returning customers show higher satisfaction?
``` SQL
SELECT
    Customer_Type,
    Satisfaction,
    COUNT(*) AS Total
FROM airline_details
GROUP BY Customer_Type, Satisfaction;
```
**Returning customers are more satisfied than first-time customers.**

6. Which type of travel has the highest satisfaction?
```SQL
SELECT
    Type_of_Travel,
    Satisfaction,
    COUNT(*) AS Total
FROM airline_details
GROUP BY Type_of_Travel, Satisfaction;
```
**Business travelers are more happier with the airline than people traveling for personal reasons.**

7. Does food quality affect satisfaction?
```SQL
SELECT
    Satisfaction,
    AVG(Food_and_Drink) AS Avg_Food_Rating
FROM airline_details
GROUP BY Satisfaction;
```
**Food quality directly impacts passenger experience.**    

8. Which Customer Segment Travels the Longest Distance?
```SQL
SELECT
    Type_of_Travel,
    AVG(Flight_Distance) AS Avg_Distance
FROM airline_details
GROUP BY Type_of_Travel;
```
**People who travel for business usually fly longer distances compared to people who travel for personal reasons**

9. Which Class Has the Best Seat Comfort Rating?
```SQL
SELECT
    Class,
    AVG(Seat_Comfort) AS Avg_Comfort
FROM airline_details
GROUP BY Class
ORDER BY Avg_Comfort DESC;
```
**Business Class is the most comfortable seating option on a flight.**

10. Which gender has higher satisfaction?
```SQL
SELECT
    Gender,
    Satisfaction,
    COUNT(*) AS Total
FROM airline_details
GROUP BY Gender, Satisfaction;
```
**Male passengers have a slightly higher satisfaction rate (44.01%) than female passengers (42.90%).**
## Conclusion

This analysis helped identify the main factors that affect airline customer satisfaction.
To improve customer satisfaction, the airline should reduce delays, enhance Economy Class services, and strengthen loyalty programs.
These improvements can help increase customer satisfaction, retain more customers, and support business growth.


























