# nz_vehicle_theft_analysis

## Project Overview
Vehicle theft is a worldwide issue affecting many motorists. This project analyses motor vehicle theft patterns in New Zealand. The aim is to:
* Identify trends in vehicle theft by day, vehicle type, and region.
* Examine how vehicle age impacts theft likelihood.
* Discover which regions have the highest and lowest theft rates.

### Data Sources 
The dataset used in this analysis comes from Maven Analytics.
The cleaning script used to clean and format the data for analysis can be found here.
The clean dataset can be founded here.
All SQL queries can be accessed here.


What day of the week are vehicles most often and least often stolen?

SELECT 
	DATENAME(WEEKDAY, date_stolen) as day_of_week,
	COUNT(*) as num_of_thefts
FROM stolen_vehicles
GROUP BY DATENAME(WEEKDAY, date_stolen)
ORDER BY num_of_thefts DESC

[Click here to view query results](assets/query_results/thefts_by_day.csv)

What types of vehicles are most often and least often stolen? Does this vary by region?
SELECT 
	vehicle_type,
	region,
	COUNT(*) as num_of_thefts
FROM stolen_vehicles s 
JOIN locations l ON s.location_id=l.location_id
GROUP BY vehicle_type, region
ORDER BY num_of_thefts DESC

[Click here to view query results](assets/query_results/thefts_by_vehicle_type_and_region.csv)

What is the average age of the vehicles that are stolen? Does this vary based on the vehicle type?
SELECT 
	vehicle_type,
	COUNT(*) AS num_of_thefts,
	AVG(age) AS avg_age
FROM stolen_vehicles
GROUP BY vehicle_type
ORDER BY num_of_thefts DESC

[Click here to view query results](assets/query_results/avg_age_of_stolen_vehicles_by_type.csv)

Which regions have the most and least number of stolen vehicles? What are the characteristics of the regions?
SELECT
	region,
	population,
	density,
	count(vehicle_id) AS num_of_thefts
FROM stolen_vehicles s 
JOIN locations l ON s.location_id=l.location_id
GROUP BY region, population, density
ORDER BY num_of_thefts DESC

[Click here to view query results](assets/query_results/thefts_by_region.csv)
