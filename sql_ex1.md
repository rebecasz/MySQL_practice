https://www.sql-practice.com/

patients: 

Table Info
primary key icon	patient_id	INT
first_name	TEXT
last_name	TEXT
gender	CHAR(1)
birth_date	DATE
city	TEXT
primary key icon	province_id	CHAR(2)
allergies	TEXT
height	INT
weight	INT

doctors : 

primary key icon	doctor_id	INT
first_name	TEXT
last_name	TEXT
specialty	TEXT
Hints

province_names :

primary key icon	province_id	CHAR(2)
province_name	TEXT

admissions :

primary key icon	patient_id	INT
admission_date	DATE
discharge_date	DATE
diagnosis	TEXT
primary key icon	attending_doctor_id	INT


# 1. Show first name, last name, and gender of patients whose gender is 'M' :

SELECT first_name,last_name,gender 
FROM patients
where gender='M'

# 2. Show first name and last name of patients who does not have allergies. (null)

SELECT first_name, last_name
FROM patients
where allergies IS NULL

## 3. Show first name of patients that start with the letter 'C'

SELECT first_name
FROM patients
where first_name LIKE 'C%'

## 4. Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)

SELECT first_name, last_name
FROM patients
where weight BETWEEN 100 and 120

## 5. Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'

UPDATE patients
SET allergies = 'NKA'
where allergies IS null

# 6. Show first name and last name concatinated into one column to show their full name.

select CONCAT( first_name,' ', last_name)
from patients

SELECT first_name || ' ' || last_name
FROM patients;

# 7. Show how many patients have a birth_date with 2010 as the birth year.

select COUNT(patient_id)
from patients
where birth_date BETWEEN '2010-01-01' AND '2010-12-31'

SELECT COUNT(*) AS total_patients
FROM patients
WHERE YEAR(birth_date) = 2010;

SELECT count(first_name) AS total_patients
FROM patients
WHERE
  birth_date >= '2010-01-01'
  AND birth_date <= '2010-12-31'

# 8. Show the first_name, last_name, and height of the patient with the greatest height.

select first_name, last_name, MAX(height)
from patients

SELECT first_name, last_name, height
FROM patients
WHERE height = (
    SELECT max(height)
    FROM patients
  )

# 9. Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000

select * 
from patients
where patient_id IN (1,45,534,879,1000)

# 10. Based on the cities that our patients live in, show unique cities that are in province_id 'NS'?

select distinct(city)
from patients
where province_id='NS'

# 11. Write a query to find the first_name, last name and birth date of patients who has height greater than 160 and weight greater than 70

select first_name, last_name, birth_date
from patients
where height>160 and weight>70

# 12. Write a query to find list of patients first_name, last_name, and allergies where allergies are not null and are from the city of 'Hamilton'

select first_name, last_name, allergies
from patients
where allergies IS NOT NULL and city='Hamilton'

# 13. Show unique birth years from patients and order them by ascending.

SELECT distinct(year(birth_date))
FROM patients
order by birth_date

# 14. Show unique first names from the patients table which only occurs once in the list.
# For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.

SELECT first_name
FROM patients
group by first_name
having count(first_name)=1

SELECT first_name
FROM (
    SELECT
      first_name,
      count(first_name) AS occurrencies
    FROM patients
    GROUP BY first_name
  )
WHERE occurrencies = 1

# 15. Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.

SELECT patient_id, first_name
FROM patients
where first_name like 'S____%s'

# 16. Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.
Primary diagnosis is stored in the admissions table.

SELECT patients.patient_id, patients.first_name, patients.last_name
FROM patients
join admissions on patients.patient_id=admissions.patient_id
where diagnosis='Dementia'

# 17. Display every patient's first_name.
# Order the list by the length of each name and then by alphabetically.

SELECT first_name
FROM patients
order by len(first_name) , first_name asc 

# 18. Show the total amount of male patients and the total amount of female patients in the patients table. Display the two results in the same row.

SELECT 
 (select count(*)  FROM patients where gender = 'M') as male_count,
 (select count(*)  FROM patients where gender = 'F') as female_count


SELECT 
  SUM(Gender = 'M') as male_count, 
  SUM(Gender = 'F') AS female_count
FROM patients

select 
  sum(case when gender = 'M' then 1 end) as male_count,
  sum(case when gender = 'F' then 1 end) as female_count 
from patients;

# 19. Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.

SELECT first_name, last_name, allergies
from patients
where  allergies='Penicillin' or allergies = 'Morphine'
order by allergies ASC, first_name ASC, last_name ASC


# 20. Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.

SELECT patient_id, diagnosis
from admissions
group by patient_id, diagnosis
having count(*) > 1

# 21. Show the city and the total number of patients in the city.
Order from most to least patients and then by city name ascending.

select city, count(patient_id)
from patients
group by city 
order by count(patient_id) desc, city asc

# 22. Show first name, last name and role of every person that is either patient or doctor.
The roles are either "Patient" or "Doctor"

select first_name, last_name, 'Patient' as role from patients
union ALL
select first_name, last_name, 'Doctor'  as role from doctors

# 23. Show all allergies ordered by popularity. Remove NULL values from query.

select allergies, count(allergies) 
from patients
where allergies not null
group by allergies
order by count(allergies) desc 

# 24. Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.

select first_name, last_name, birth_date
from patients
where birth_date between '1970-01-01' and '1979-12-31'
order by birth_date asc

# 25. We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in decending order
# EX: SMITH,jane

select CONCAT( UPPER(last_name), ',', LOWER(first_name))
from patients
order by first_name desc

# 26. Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.

select province_id, sum(height)
from patients
group by province_id
having sum(height) >=7000


# 27. Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'

select max(weight)-min(weight)
from patients
where last_name='Maroni'
group by last_name


# 28. Show all of the days of the month (1-31) and how many admission_dates occurred on that day. Sort by the day with most admissions to least admissions.

select DAY(admission_date), count(day(admission_date))
from admissions
group by day(admission_date)
order by count(admission_date) desc 

# 29. Show all columns for patient_id 542's most recent admission_date.

select *
from admissions
where patient_id=542 
group by patient_id
having max(admission_date)

# 30. Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria:
# - patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.
# - attending_doctor_id contains a 2 and the length of patient_id is 3 characters.

select patient_id, attending_doctor_id, diagnosis
from admissions
where (patient_id % 2 <> 0 AND attending_doctor_id in (1, 5, 19)) or (attending_doctor_id like '%2%' and len(patient_id)=3)


# 31. Show first_name, last_name, and the total number of admissions attended for each doctor.
# Every admission has been attended by a doctor.

select doctors.first_name, doctors.last_name, count(admissions.attending_doctor_id)
from doctors
join admissions on admissions.attending_doctor_id=doctors.doctor_id
group by doctors.doctor_id

# 32. For each doctor, display their id, full name, and the first and last admission date they attended.

select doctors.doctor_id, CONCAT(doctors.first_name,' ', doctors.last_name), MIN(admissions.admission_date), max(admissions.admission_date)
from doctors
join admissions on admissions.attending_doctor_id=doctors.doctor_id
group by doctors.doctor_id

# 33. Display the total amount of patients for each province. Order by descending.

select province_names.province_name, COUNT(patients.patient_id)
from patients
join province_names on patients.province_id=province_names.province_id
group by province_names.province_name
order by COUNT(patients.patient_id) desc

# 34. For every admission, display the patient's full name, their admission diagnosis, and their doctor's full name who diagnosed their problem.

select CONCAT(patients.first_name,' ',patients.last_name), admissions.diagnosis, CONCAT(doctors.first_name,' ',doctors.last_name)
from patients
join admissions on patients.patient_id=admissions.patient_id
join doctors on admissions.attending_doctor_id=doctors.doctor_id

# 35. display the first name, last name and number of duplicate patients based on their first name and last name.
# Ex: A patient with an identical name can be considered a duplicate.

select first_name, last_name, count(CONCAT(first_name,last_name))
from patients
group by CONCAT(first_name,last_name)
having count(CONCAT(first_name,last_name))>1

# 36. Display patient's full name, height in the units feet rounded to 1 decimal, weight in the unit pounds rounded to 0 decimals, birth_date, gender non abbreviated.
# Convert CM to feet by dividing by 30.48.
# Convert KG to pounds by multiplying by 2.205.

SELECT 
    CONCAT(first_name, ' ', last_name),
    ROUND(height / 30.48, 1),
    ROUND(weight * 2.205, 0),
    birth_date,
    CASE
        WHEN gender = 'M' THEN 'MALE'
        ELSE 'FEMALE'
    END AS gender
FROM patients;

# 37. Show patient_id, first_name, last_name from patients whose does not have any records in the admissions table. (Their patient_id does not exist in any admissions.patient_id rows.)

select patient_id, first_name, last_name
from patients
where patient_id not in (select distinct(patient_id) from admissions)

# 38. Show first name, last name, and the full province name of each patient.
# Example: 'Ontario' instead of 'ON'

select patients.first_name, patients.last_name, province_names.province_name
from patients
join province_names ON patients.province_id=province_names.province_id


# 39.Show the total number of admissions

select count(*)
from admissions

# 40. Show all the columns from admissions where the patient was admitted and discharged on the same day.

select *
from admissions
where admission_date = discharge_date

# 41. Show the patient id and the total number of admissions for patient_id 579.

select patient_id , count(*)
from admissions
where patient_id=579

# 42. Show all of the patients grouped into weight groups.
# Show the total amount of patients in each weight group.
# Order the list by the weight group decending.
# For example, if they weight 100 to 109 they are placed in the 100 weight group, 110-119 = 110 weight group, etc.

SELECT count(patient_id) , FLOOR(weight / 10) * 10 
FROM patients
group by FLOOR(weight / 10) * 10 
order by weight desc

# 43. Show patient_id, weight, height, isObese from the patients table.
# Display isObese as a boolean 0 or 1.
# Obese is defined as weight(kg)/(height(m)2) >= 30.
# weight is in units kg.
# height is in units cm.

SELECT patient_id, weight, height, 
case
     when weight/POWER(height/100.0,2) >= 30 then 1
     else 0
end as isobese
FROM patients


# 44. Show patient_id, first_name, last_name, and attending doctor's specialty.
# Show only the patients who has a diagnosis as 'Epilepsy' and the doctor's first name is 'Lisa'
# Check patients, admissions, and doctors tables for required information.

SELECT patients.patient_id, patients.first_name, patients.last_name, doctors.specialty
from patients
join admissions on patients.patient_id=admissions.patient_id
join doctors on admissions.attending_doctor_id=doctors.doctor_id
where admissions.diagnosis='Epilepsy' and doctors.first_name='Lisa'

# 45. All patients who have gone through admissions, can see their medical documents on our site. Those patients are given a temporary password after their first admission. Show the patient_id and temp_password.
# The password must be the following, in order:
# -patient_id
# -the numerical length of patient's last_name
# -year of patient's birth_date

SELECT distinct(patients.patient_id), concat(patients.patient_id,len(patients.last_name),year(patients.birth_date))
from patients
inner join admissions on patients.patient_id=admissions.patient_id  

# Each admission costs $50 for patients without insurance, and $10 for patients with insurance. All patients with an even patient_id have insurance.
# Give each patient a 'Yes' if they have insurance, and a 'No' if they don't have insurance. Add up the admission_total cost for each has_insurance group.

SELECT 
	case WHEN patient_id % 2 = 0 then 'Yes'
    else 'No'
END as Insurrance,
SUM(CASE WHEN patient_id % 2 = 0 Then 
    10
ELSE 
    50 
END) as cost_after_insurance
from admissions
group by Insurrance 


select has_insurance,sum(admission_cost) as admission_total
from
(
   select patient_id,
   case when patient_id % 2 = 0 then 'Yes' else 'No' end as has_insurance,
   case when patient_id % 2 = 0 then 10 else 50 end as admission_cost
   from admissions
)
group by has_insurance

# 47. Show the provinces that has more patients identified as 'M' than 'F'. Must only show full province_name

select province_names.province_name
from province_names
join patients on patients.province_id=province_names.province_id
group by province_names.province_name
HAVING
  SUM(gender = 'M') > SUM(gender = 'F');

# 48. We are looking for a specific patient. Pull all columns for the patient who matches the following criteria:
# - First_name contains an 'r' after the first two letters.
# - Identifies their gender as 'F'
# - Born in February, May, or December
# - Their weight would be between 60kg and 80kg
# - Their patient_id is an odd number
# - They are from the city 'Kingston'

select *
from patients
where
	first_name like '__r%' and 
    gender = 'F'and 
    MONTH(birth_date) IN (2, 5, 12)
    weight between 60 and 80 and 
    patient_id % 2 = 1 and
    city = 'Kingston'

# 49. Show the percent of patients that have 'M' as their gender. Round the answer to the nearest hundreth number and in percent form.

SELECT CONCAT(
  ROUND(
    (SUM(CASE WHEN gender = 'M' THEN 1 ELSE 0 END) * 100.0) / COUNT(*), 2),'%'
) AS Percentage_of_Males
FROM patients;

# 50. For each day display the total amount of admissions on that day. Display the amount changed from the previous date.

SELECT
 admission_date,
 count(admission_date) as admission_day,
 count(admission_date) - LAG(count(admission_date)) OVER(ORDER BY admission_date) AS admission_count_change 
FROM admissions
 group by admission_date

# 51. Sort the province names in ascending order in such a way that the province 'Ontario' is always on top.

SELECT province_name 
from province_names
ORDER BY 
  CASE WHEN province_name = 'Ontario' THEN 0 ELSE 1 END,
  province_name ASC;

select province_name
from province_names
order by
  province_name = 'Ontario' desc,
  province_name

# 52. We need a breakdown for the total amount of admissions each doctor has started each year. Show the doctor_id, doctor_full_name, specialty, year, total_admissions for that year.

SELECT
  d.doctor_id as doctor_id,
  CONCAT(d.first_name,' ', d.last_name) as doctor_name,
  d.specialty,
  YEAR(a.admission_date) as selected_year,
  COUNT(*) as total_admissions
FROM doctors as d
  LEFT JOIN admissions as a ON d.doctor_id = a.attending_doctor_id
GROUP BY
  doctor_name,
  selected_year
ORDER BY doctor_id, selected_year






