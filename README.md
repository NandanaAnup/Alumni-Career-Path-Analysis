# 🎓 Alumni Career Path Analysis
# 🎯 Objective
This project aims to analyze the career trends of alumni from College A and College B, focusing on their course completion year and chosen paths such as Higher Studies, Self-Employment, or Service/Job. It demonstrates SQL skills such as database schema creation, data import, cleaning data by removing null values, string manipulation for consistent naming, cursor usage for data fetching, and career percentage calculations.
# 📝 Project Structure
* Schema Creation: Creating the alumni database schema.
* Data Import: Importing six alumni career-related CSV files into MySQL tables.
* Data Cleaning: Removing null values and creating clean views.
* String Manipulation: Converting names to lowercase using procedures.
* Cursor Procedures: Fetching alumni names using cursors.
* Career Choice Analysis: Calculating career choice percentages for both universities.
# Tasks
### 1. Create new schema as alumni
```MySql
CREATE SCHEMA alumni;
USE alumni;
```
 .csv files have been imported in mysql
### 2. Run SQL command to see the structure of six tables
```MySql
USE alumni;
DESC college_a_hs;
DESC college_a_se;
DESC college_a_sj;
DESC college_b_hs;
DESC college_b_se;
DESC college_b_sj;
```
### 3. Perform data cleaning on table College_A_HS and store cleaned data in view College_A_HS_V, Remove null values. 
```MySql
CREATE VIEW college_a_hs_v AS SELECT * FROM college_a_hs
WHERE RollNo IS NOT NULL AND
LastUpdate IS NOT NULL AND Name IS NOT NULL AND
FatherName IS NOT NULL AND MotherName IS NOT NULL AND
Batch IS NOT NULL AND Degree IS NOT NULL AND PresentStatus IS NOT NULL AND HSDegree IS NOT NULL AND
EntranceExam IS NOT NULL AND Institute IS NOT NULL AND Location IS NOT NULL;

SELECT * FROM college_a_hs_v;
```
### 4. Perform data cleaning on table College_A_SE and store cleaned data in view College_A_SE_V, Remove null values.
```MySql
CREATE VIEW college_a_se_v AS SELECT * FROM college_a_se
WHERE RollNo IS NOT NULL AND
LastUpdate IS NOT NULL AND Name IS NOT NULL AND
FatherName IS NOT NULL AND MotherName IS NOT NULL AND
Batch IS NOT NULL AND Degree IS NOT NULL AND PresentStatus IS NOT NULL AND
Organization IS NOT NULL AND Location IS NOT NULL;

SELECT * FROM college_a_se_v;
```
### 5. Perform data cleaning on table College_A_SJ and store cleaned data in view College_A_SJ_V, Remove null values.
```MySql
CREATE VIEW college_a_sj_v AS SELECT * FROM college_a_sj
WHERE RollNo IS NOT NULL AND
LastUpdate IS NOT NULL AND Name IS NOT NULL AND
FatherName IS NOT NULL AND MotherName IS NOT NULL AND
Batch IS NOT NULL AND Degree IS NOT NULL AND
PresentStatus IS NOT NULL AND Organization IS NOT NULL AND
Designation  IS NOT NULL AND Location IS NOT NULL;

SELECT * FROM college_a_sj_v;
```
### 6. Perform data cleaning on table College_B_HS and store cleaned data in view College_B_HS_V, Remove null values.
```MySql
CREATE VIEW college_b_hs_v AS SELECT * FROM college_b_hs WHERE RollNo IS NOT NULL AND
LastUpdate IS NOT NULL AND Name IS NOT NULL AND FatherName IS NOT NULL AND MotherName IS NOT NULL AND
Branch IS NOT NULL AND Batch IS NOT NULL AND Degree IS NOT NULL AND PresentStatus IS NOT NULL AND 
HSDegree IS NOT NULL AND EntranceExam IS NOT NULL AND Institute IS NOT NULL AND Location IS NOT NULL;

SELECT * FROM college_b_hs_v;
```
### 7. Perform data cleaning on table College_B_SE and store cleaned data in view College_B_SE_V, Remove null values.
```MySql
CREATE VIEW college_b_se_v AS SELECT * FROM college_b_se WHERE RollNo IS NOT NULL AND
LastUpdate IS NOT NULL AND Name IS NOT NULL AND FatherName IS NOT NULL AND MotherName IS NOT NULL AND
Branch IS NOT NULL AND Batch IS NOT NULL AND Degree IS NOT NULL AND PresentStatus IS NOT NULL AND 
Organization IS NOT NULL AND Location IS NOT NULL;

SELECT * FROM college_b_se_v;
```
### 8.Perform data cleaning on table College_B_SJ and store cleaned data in view College_B_SJ_V, Remove null values.
```MySql
CREATE VIEW college_b_sj_v AS SELECT * FROM college_b_sj WHERE RollNo IS NOT NULL AND
LastUpdate IS NOT NULL AND Name IS NOT NULL AND FatherName IS NOT NULL AND MotherName IS NOT NULL AND
Branch IS NOT NULL AND Batch IS NOT NULL AND Degree IS NOT NULL AND PresentStatus IS NOT NULL AND 
Organization IS NOT NULL AND  Designation IS NOT NULL AND Location IS NOT NULL;

SELECT * FROM college_b_sj_v;
```
### 9. Make procedure to use string function/s for converting record of Name, FatherName, MotherName into lower case for views (College_A_HS_V, College_A_SE_V, College_A_SJ_V, College_B_HS_V, College_B_SE_V, College_B_SJ_V) 
```MySql
DELIMITER $$
CREATE PROCEDURE LowerCase ()
BEGIN
SELECT LOWER(Name) Name , LOWER(FatherName) FatherName, LOWER(MotherName) MotherName FROM college_a_hs;
SELECT LOWER(Name) Name, LOWER(FatherName) FatherName, LOWER(MotherName) MotherName FROM college_a_se;
SELECT LOWER(Name) Name, LOWER(FatherName) FatherName, LOWER(MotherName) MotherName FROM college_a_sj;
SELECT LOWER(Name) Name, LOWER(FatherName) FatherName, LOWER(MotherName) MotherName FROM college_b_hs;
SELECT LOWER(Name) Name, LOWER(FatherName) FatherName, LOWER(MotherName) MotherName FROM college_b_se;
SELECT LOWER(Name) Name, LOWER(FatherName) FatherName, LOWER(MotherName) MotherFather FROM college_b_sj;
END $$
DELIMITER ;

CALL LowerCase();
```
### 10. Write a query to create procedure get_name_collegeA using the cursor to fetch names of all students from college A.
```MySql
DELIMITER $$
CREATE PROCEDURE get_name_collegeA (
INOUT getnameA TEXT(40000)   )
BEGIN
     DECLARE finished INT DEFAULT 0;
     DECLARE getnamelistA VARCHAR(16000) DEFAULT "" ;
     
     DECLARE getnamedetailA 
            CURSOR FOR
                 SELECT Name from college_a_hs UNION SELECT Name from college_a_se UNION 
				 SELECT Name from college_a_sj;
                 
	 DECLARE CONTINUE HANDLER 
     FOR NOT FOUND SET finished = 1;
     
     OPEN getnamedetailA;
     
     getloop:
     LOOP
		FETCH getnamedetailA INTO getnamelistA;
        IF finished = 1 THEN
            LEAVE getloop;
		END IF;
        SET getnameA = CONCAT(getnamelistA," ; ",getnameA);
		END LOOP getloop;
        CLOSE getnamedetailA;
END $$
DELIMITER ;

SET @getnameA = "";
CALL get_name_collegeA(@getnameA);
SELECT @getnameA NamesA;
```
### 11. Write a query to create procedure get_name_collegeB using the cursor to fetch names of all students from college B.
```MySql
DELIMITER $$
CREATE PROCEDURE get_name_collegeB (
INOUT getnameB TEXT(40000)   )
BEGIN
     DECLARE finished INT DEFAULT 0;
     DECLARE getnamelistB VARCHAR(16000) DEFAULT "" ;
     
     DECLARE getnamedetailB 
            CURSOR FOR
                 SELECT Name from college_b_hs UNION SELECT Name from college_b_se UNION 
				 SELECT Name from college_b_sj;
                 
	 DECLARE CONTINUE HANDLER 
     FOR NOT FOUND SET finished = 1;
     
     OPEN getnamedetailB;
     
     getloop:
     LOOP
		FETCH getnamedetailB INTO getnamelistB;
        IF finished = 1 THEN
            LEAVE getloop;
		END IF;
        SET getnameB = CONCAT(getnamelistB," ; ",getnameB);
		END LOOP getloop;
        CLOSE getnamedetailB;
END $$
DELIMITER ;

SET @getnameB = "";
CALL get_name_collegeB(@getnameB);
SELECT @getnameB NamesB;
```
### 12. Calculate the percentage of career choice of College A and College B Alumni-- (w.r.t Higher Studies, Self Employed and Service/Job)Note: Approximate percentages are considered for career choices.
```MySql
SELECT ('Higher Studies') 'Career_choice',(SELECT COUNT(*) FROM college_a_hs )/((SELECT COUNT(*)  FROM college_a_hs) + (SELECT COUNT(*)  FROM college_a_se)
+ (SELECT COUNT(*)  FROM college_a_sj))*100 'College_A_Percentage',
(SELECT COUNT(*) FROM college_b_hs )/((SELECT COUNT(*)  FROM college_b_hs) + (SELECT COUNT(*)  FROM college_b_se)
+ (SELECT COUNT(*)  FROM college_b_sj))*100 'College_B_Percentage' UNION 
SELECT 'Self_Employed',(SELECT COUNT(*) FROM college_a_se )/((SELECT COUNT(*)  FROM college_a_hs) + (SELECT COUNT(*)  FROM college_a_se)
+ (SELECT COUNT(*)  FROM college_a_sj))*100 'College_A_Percentage',
(SELECT COUNT(*) FROM college_b_se )/((SELECT COUNT(*)  FROM college_b_hs) + (SELECT COUNT(*)  FROM college_b_se)
+ (SELECT COUNT(*)  FROM college_b_sj))*100 'College_B_Percentage'UNION
SELECT 'Service Jobs',(SELECT COUNT(*) FROM college_a_sj )/((SELECT COUNT(*)  FROM college_a_hs) + (SELECT COUNT(*)  FROM college_a_se)
+ (SELECT COUNT(*)  FROM college_a_sj))*100 'College_A_Percentage',
(SELECT COUNT(*) FROM college_b_sj )/((SELECT COUNT(*)  FROM college_b_hs) + (SELECT COUNT(*)  FROM college_b_se)
+ (SELECT COUNT(*)  FROM college_b_sj))*100 'College_B_Percentage';
```
# 📖 Conclusion
This project highlights my ability to apply SQL for real-world alumni career data analysis, including schema design, data cleaning, string manipulation, and cursor-based procedures. By calculating and comparing career choice percentages between two colleges, it demonstrates structured problem-solving, advanced query handling, and the skill to transform data into meaningful insights.




















