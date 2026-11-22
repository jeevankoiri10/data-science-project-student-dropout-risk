# Student Dropout & Macroeconomic Risk Analysis

This project was developed for the **Foundations of Computer Science** course (MSc in Data Science, University of Milano-Bicocca) and submitted by **Jeevan Koiri** to Professors **Gianluca Della Vedova**, **Domenico Giorgio Sorrenti**, and **Davide Cozzi** in partial fulfillment of the course requirements.

## Overview

This repository presents a Python data analysis pipeline that investigates student dropout patterns and behavioral risk factors alongside national macroeconomic indicators. By integrating individual-level student records with the latest country-level GDP per capita data (`ny_gdp_pcap_pp_kd`) from **Our World in Data (OWID)**, the workflow cleans and standardizes cross-dataset country identifiers, constructs a composite student risk score, and evaluates dropout rates across global regions and continents.

## Actual Question Set: 
The dataset [student_dropout_risk_2026.csv.gz](https://www.google.com/search?q=https://drive.google.com/uc%3Fexport%3Ddownload%26id%3D1P6eZPCg1FwpXnbq2Yt52RTdvDLk4PSD9) contains one row for each university student (identified by `person_id`), with demographic, economic, academic and behavioural information. The column `dropout` is `1` if the student has dropped out, `0` otherwise. All columns whose values are `0`/`1` are boolean flags.

### Notes

1. It is mandatory to use GitHub for developing the project.
2. The project must be a Jupyter notebook.
3. There is no restriction on the libraries that can be used, nor on the Python version.
4. All questions on the project **must** be asked in the Discussion forum on the course website.
5. 1, 2, or 3 students can be in each group. You must create the groups by yourself.
6. Avoid explicit `for` loops over the rows of the dataframe, unless the exercise explicitly asks for them.

### 1.

Extract all students that study `Online`, have an `attendance_rate` smaller than 50, and have more than 5 `missed_deadlines`. Store them in a dataframe called `at_risk`.

### 2.

Then compute, for each `course_type`, how many of those students there are and what fraction of them has dropped out. Store the result in a dataframe called `at_risk_by_course`, with columns `students` and `dropout_rate`, sorted by decreasing `dropout_rate`.

### 3.

Add to the dataframe the following columns:

- `pass_rate`: the ratio between `units_passed` and `units_enrolled`;
- `gpa_change`: the difference between `gpa_semester_2` and `gpa_semester_1`;
- `gpa_trend`: a string that is `"improving"` if `gpa_change` is larger than 0.5, `"declining"` if `gpa_change` is smaller than -0.5, and `"stable"` otherwise.

### 4.

Verify that, for every student, `units_passed + units_failed` equals `units_enrolled`; if not, report the rows violating this condition.

### 5.

Compute the dropout rate for each value of `gpa_trend`, and the `person_id` of the 10 students with the largest GPA drop.

### 6.

Partition the students into the following groups, according to `weekly_work_hours`: `0`, `1-10`, `11-20`, `21-30`, `more than 30` (all intervals include both extremes).

### 7.

Build a risk score by summing:

- 2 points if the tuition is not up to date;
- 1 point if `stress_level` is at least 8;
- 1 point if `sleep_hours` is smaller than 5;
- 1 point if the student has a part-time job with more than 20 weekly work hours;
- 2 points if `attendance_rate` is smaller than 60;
- 1 point if `missed_deadlines` is larger than 3.

For each value of the risk score, compute the number of students and the dropout rate.

### 8.

Read the GDP per capita dataset published by Our World in Data directly from the URL

```
https://ourworldindata.org/grapher/gdp-per-capita-worldbank.csv?v=1&csvType=full&useColumnShortNames=true
```

and store it in a dataframe called `gdp`. The column `ny_gdp_pcap_pp_kd` contains the GDP per capita.

Clean the dataset, removing the rows that do not correspond to a single country (e.g. `World`, `High-income countries`). For each country keep only the row with the most recent `year`.

### 9.

Join the GDP data with the students data. Compute the dropout rate for each continent.