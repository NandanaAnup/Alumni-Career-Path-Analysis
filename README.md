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





















