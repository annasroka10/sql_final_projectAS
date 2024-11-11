# sql_final_projectAS
SQL final project
/******************************/
/***** Final project SQL *****/
/******************************/

My final project contains 2 tables gym_members_exercise_trackkingAS and gym_members_exercise_trackingAS1. I wrote following 6 queries. 






/***** Problem 1 *****/

-- Write a query that shows all the members from gym_members_exercise_trackingAS
-- Order by their name alphabetically
-- Who is the first member shown?
SELECT *
FROM gym_members_exercise_trackingAS1 gmeta 
order by Name_initials;




/***** Problem 2 *****/

-- Write a query that counts how many members are females and males

SELECT gender, COUNT(*) 
from gym_members_exercise_trackingAS1 gmeta 
group by Gender;




/***** Problem 3 *****/

-- Write a query to find the oldest member
-- Show their age and name
-- How many tournaments have been played at Acapulco Lanes, Red Rooster Lanes, and Thunderbird Lanes?

SELECT  Name_initials , MAX(age) as Max_Age 
FROM gym_members_exercise_trackingAS1 gmeta;






/***** Problem 4 *****/

-- Write a query to determine the average avg_calories_burned
-- Round the average calories_burned to the nearest whole number and display as Avg_cal_burned
-- Group by the memberid and order by average rcalories_burned from largest to smallest
-- What is the memberid of the member with the highest average calories_burned? 1962SK69
select Memberid , AVG(Calories_Burned) AS avg_calories_burned 
FROM gym_members_exercise_trackingAS gmeta 
group by Memberid 
ORDER BY avg_calories_burned DESC;



/***** Problem 5 *****/

-- Write a script to join the gym_members_exercise_trackingAS1 and gym_members_exercise_trackingAS by their memberid
-- show only memebers that were born between 1990 and 2000 inclusive 
SELECT *
FROM gym_members_exercise_trackingAS1 g1 
join gym_members_exercise_trackingAS g on g.Memberid = g1.Memberid 
WHERE g1.DOB BETWEEN '1990' and '2000'
ORDER BY Memberid, g1.Name_initials;


/***** Problem 6 *****/
--write a query using CTE
WITH cte AS (
 SELECT *
 FROM gym_members_exercise_trackingAS
 WHERE calories_burned > 100)
SELECT g1.memberid, g1.gender, g1.name_initials, g1.age, g.Calories_Burned, g."Session_Duration (hours)", ROUND(AVG(Calories_Burned/"Session_Duration (hours)"),2) AS avg_caloriesburned 
FROM gym_members_exercise_trackingAS1 g1
Join gym_members_exercise_trackingAS g on g1.memberid = g.memberid
WHERE g1.Gender = 'Female'
AND g1.Age BETWEEN 50 and 60
AND g.memberid IN (SELECT memberid FROM cte)
group by g.Memberid 
order by g.Calories_Burned DESC;




