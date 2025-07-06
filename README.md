# 📊 Hr_Analyysis_Powerbi_For_ Palmoria_Group_HR_System. (Power BI Data Analysis)

**Tools**: Power BI, DAX, Power Query   
[![Power BI](https://img.shields.io/badge/-Power_BI-F2C811?logo=powerbi)]()  
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)  
![PALMORIA DSA PROJECT 2](https://github.com/user-attachments/assets/cba8a02e-8a7f-4bd1-a38b-15b83d0215c9)
![PALMORIA DSA PROJECT 4](https://github.com/user-attachments/assets/00f6536a-dcb2-451b-8c25-0c6625396f2d)
![PALMORIA DSA PROJECT 3](https://github.com/user-attachments/assets/31b6b051-a97a-4168-9777-9cbb18cbdf35)
![PALMORIA DSA PROJECT 1](https://github.com/user-attachments/assets/f0e819d4-9760-4f9a-97c1-05cda76b0576)
![PALMORIA DSA PROJECT 5](https://github.com/user-attachments/assets/79afccde-330b-48ee-b2b5-c67770ca3782)

HR analytics dashboards for Palmoria Group | Power BI + DAX | Employee performance, turnover, and recruitment insights  
This project delves into Palmoria Group's Human Resources data, leveraging Power BI to transform raw employee and bonus policy information into actionable insights. Through robust data modeling, DAX calculations, and interactive visualizations, I've created a comprehensive HR dashboard designed to empower management with a clear understanding of workforce demographics, compensation structures, performance trends, and the financial implications of bonus policies. This system supports data-driven decision-making for talent management, compensation adjustments, and strategic HR planning.

Table of Contents
 * 🔍 Project Overview
 * 📊 Dataset Insights
 * 📋 Core Analytical Questions & Approaches
 * 📈 Key Business Discoveries & Impact
 * 🛠️ Technologies Utilized
 * 🚀 Project Structure
 * 📸 Visuals & Dashboard Snapshot
 * ⭐ My Analytical Toolkit in Action
 * 📬 Connect with Me

🔍 Project Overview
As a Data Analyst, this project served as a hands-on experience in building a dynamic Power BI HR dashboard. My primary goal was to provide transparent and insightful views into Palmoria Group's employee data, highlighting key trends and patterns in gender distribution, performance ratings, salary structures, minimum wage compliance, and bonus payouts. This system aims to enable HR and leadership to make more informed and equitable decisions, fostering data-driven improvements in employee welfare and organizational efficiency.

📊 Dataset Insights
My analysis was conducted on two proprietary datasets provided by Palmoria Group:
 * Palmoria Group emp-data.csv: This is the primary employee dataset containing 946 unique employee records across various key attributes.
* Highlights of the Data Fields:
* Name, Gender, Department, Salary, Location, Rating
* Data Cleaning and Transformation Applied:
* Missing Gender values replaced with 'Undisclosed'.
* 'N/A' gender values replaced with 'Undisclosed'.
* Rows with missing Salary or Department removed.
* Department values 'NULL' removed.
* Palmoria Group Bonus Rules.xlsx - Bonus Rules.csv: This dataset outlines the department-specific bonus percentages based on performance ratings.
* Highlights of the Data Fields:
* Department, Very Poor, Poor, Average, Good, Very Good (bonus percentages for each rating).
* Data Transformation Applied:
* Unpivoted the performance rating columns (Very Poor to Very Good) into a single 'Rating' column and a 'Bonus_Percentage' column, transforming the data from a wide to a long format.

📋 Core Analytical Questions & Approaches
To derive meaningful insights, I tackled a series of business-centric HR questions, employing various Power BI functionalities and DAX logic:
| Analytical Question | Power BI/DAX Approach & Logic Used |
|---|---|
| • How to calculate the overall gender distribution in the organization. | DAX Measure: COUNTROWS(Table) / CALCULATE(COUNTROWS(Table), ALL(Table)) for overall percentage. COUNTROWS(FILTER(Table, Table[Gender] = "Female")) for specific gender count. |
| • How to calculate gender distribution by region. | DAX Measure with CALCULATE(COUNTROWS(Table), ALLEXCEPT(Table, Table[Location])) for regional total, and COUNTROWS(FILTER(Table, Table[Gender] = "Female" && Table[Location] = "Abuja")) for specific gender/region count. |
| • How to calculate gender distribution by department. | DAX Measure with CALCULATE(COUNTROWS(Table), ALLEXCEPT(Table, Table[Department])) for department total, and COUNTROWS(FILTER(Table, Table[Gender] = "Male" && Table[Department] = "Sales")) for specific gender/department count. |
| • What is the total number of employees after cleaning? | DAX Measure: COUNTROWS(FILTER('Employee Table', NOT(ISBLANK('Employee Table'[Salary])) && 'Employee Table'[Department] <> "NULL")) |
| • How many unique departments exist? | DAX Measure: DISTINCTCOUNT('Employee Table'[Department]) |
| • What is the distribution of performance ratings across the organization? | DAX Visual: Use 'Rating' column on an axis and 'Count of Employees' (simple COUNTROWS measure) as values. |
| • What is the average salary by department? | DAX Measure: AVERAGE('Employee Table'[Salary]) |
| • What is the total salary budget for the company? | DAX Measure: SUM('Employee Table'[Salary]) |
| • What is the percentage of employees at each performance rating level? | DAX Measure: COUNTROWS(FILTER('Employee Table', 'Employee Table'[Rating] = "Good")) / COUNTROWS('Employee Table') |
| • What is the overall gender pay gap? | DAX Measures: [Average Salary Male] - [Average Salary Female] where each average is a CALCULATE(AVERAGE('Employee Table'[Salary]), 'Employee Table'[Gender] = "Male"). |
| • How does the gender pay gap vary by department? | DAX Measure: Use AVERAGE salary measure with 'Department' and 'Gender' on axes. Can create a calculated column for Gender Pay Gap within a department. |
| • How does the gender pay gap vary by region? | DAX Measure: Similar to departmental pay gap, but using 'Location' instead of 'Department'. |
| • How many employees are paid below the new minimum wage of ₹90,000? | DAX Measure: COUNTROWS(FILTER('Employee Table', 'Employee Table'[Salary] < 90000)) |
| • What is the distribution of salaries across predefined bands (e.g., ₹20,000-₹29,999, etc.)? | DAX Calculated Column: Create a 'Salary Band' column using nested IF statements based on Salary. Then use this column in visuals. |
| • How do the salary distributions by bands differ across regions? | DAX Visual: Use 'Salary Band' and 'Location' on axes, with 'Count of Employees' as values. |
| • What is the individual bonus amount for each employee? | DAX Calculated Column: Merge 'Employee Table' with 'Bonus Rules Table' on 'Rating' and 'Department'. Then Salary * Related('Bonus Rules Table'[Bonus_Percentage]). Handle unmapped ratings (e.g., 'Not Rated') by setting bonus to 0. |
| • What is the total pay (salary + bonus) for each employee? | DAX Calculated Column: 'Employee Table'[Salary] + 'Employee Table'[Bonus_Amount] |
| • What is the total bonus amount to be paid out per region? | DAX Measure: CALCULATE(SUM('Employee Table'[Bonus_Amount]), ALLEXCEPT('Employee Table', 'Employee Table'[Location])) |
| • What is the total salary (inclusive of bonus) to be paid out per region? | DAX Measure: CALCULATE(SUM('Employee Table'[Total_Pay]), ALLEXCEPT('Employee Table', 'Employee Table'[Location])) |
| • What is the grand total bonus amount for the entire company? | DAX Measure: SUM('Employee Table'[Bonus_Amount]) |
| • What is the grand total salary (inclusive of bonus) for the entire company? | DAX Measure: SUM('Employee Table'[Total_Pay]) |

📈 Key Business Discoveries & Impact
My analysis yielded several significant insights, offering valuable perspectives for Palmoria Group's HR strategies:
 * Gender Distribution Insights: The organization shows a relatively balanced gender distribution overall, though distinct variations are observable at the regional and departmental levels.
 * Performance Rating Trends: "Good" emerged as the most common performance rating across all genders, but notable differences exist in the distribution of "Poor," "Good," and "Very Good" ratings between male and female employees. No "Excellent" ratings were found in the dataset.
 * Addressing the Gender Pay Gap: A pervasive male-favored pay gap was identified across the entire organization, evident in all regions and most departments. Specific departments like Business Development, Human Resources, and Product Management showed significant disparities, warranting targeted intervention by management to promote equitable compensation.
 * Minimum Wage Non-Compliance: A critical finding revealed that a substantial portion of employees (69.13%) are paid below the new minimum wage of $$90,000$. This highlights an urgent need for salary adjustments to comply with regulations and ensure fair compensation across all departments and regions.
 * Comprehensive Compensation Planning: The integrated analysis of salary, performance ratings, and bonus rules allowed for precise calculation of individual and total bonus payouts, providing a clear financial projection for compensation planning at both regional and company-wide levels.

🛠️ Technologies Utilized
This project was developed primarily using Microsoft Power BI, demonstrating proficiency in:
 * Data Transformation & Preparation:
* Power Query Editor (for data cleaning, type conversions, handling missing values, and unpivoting the bonus rules data).
   * Python scripting for advanced data preparation (if any complex transformations were needed before loading into Power BI).
 * Data Modeling & Relationships:
   * Establishing relationships between employee data and bonus rules tables.
   * Creating a robust star schema for efficient analysis.
 * DAX (Data Analysis Expressions):
   * Developing calculated columns for new metrics (e.g., Bonus_Amount, Total_Pay, Salary_Band).
 * Writing measures for aggregations and KPIs (e.g., Average Salary, Total Bonus, Employees Below Min Wage).
 * Applying filtering and context manipulation for dynamic insights.
 * Interactive Data Visualization & Reporting:
 * Designing intuitive and interactive dashboards.
 * Utilizing various chart types (bar charts, pie charts, column charts, tables, cards).
 * Implementing slicers and drill-through capabilities for user-driven data exploration.
 * Data Source: CSV files (Palmoria Group emp-data.csv, Palmoria Group Bonus Rules.xlsx - Bonus Rules.csv).

🚀 Project Structure
This GitHub repository is structured to provide a clear overview and access to all project components:
 * Palmoria Group HR Dashboard.pbix: The core Power BI Desktop file, containing the data model, all DAX calculations, and the interactive dashboard.
 * data/: A dedicated folder containing the raw data files (Palmoria Group emp-data.csv, Palmoria Group Bonus Rules.xlsx - Bonus Rules.csv).
 * screenshots/: A dedicated folder housing high-quality images that showcase key dashboard views and charts.
 * README.md: This comprehensive document, serving as the project's executive summary and guide.

📸 Visuals & Dashboard Snapshot
Below are snapshots from the interactive Power BI dashboard, providing a glimpse into the generated insights:

![PALMORIA DSA PROJECT 3](https://github.com/user-attachments/assets/31b6b051-a97a-4168-9777-9cbb18cbdf35)
A comprehensive view of the interactive HR dashboard, showcasing key performance indicators for workforce demographics and compensation.

![PALMORIA DSA PROJECT 1](https://github.com/user-attachments/assets/f0e819d4-9760-4f9a-97c1-05cda76b0576)
A visualization illustrating the gender pay gap across different departments, highlighting areas for intervention.

![PALMORIA DSA PROJECT 5](https://github.com/user-attachments/assets/79afccde-330b-48ee-b2b5-c67770ca3782)
A chart depicting salary distribution across bands and the number of employees falling below the new minimum wage threshold.

![PALMORIA DSA PROJECT 2](https://github.com/user-attachments/assets/cba8a02e-8a7f-4bd1-a38b-15b83d0215c9)

![PALMORIA DSA PROJECT 4](https://github.com/user-attachments/assets/00f6536a-dcb2-451b-8c25-0c6625396f2d)

⭐ My Analytical Toolkit in Action: Foundations & Growth
This project serves as a clear demonstration of my growing analytical capabilities and the foundational skills I'm actively building. It highlights my practical application of core data analysis principles to real-world challenges:
 * Data Integration & Transformation: I effectively leveraged Power Query to integrate multiple data sources, perform complex cleaning steps, and transform raw data into a structured format suitable for analysis. This involved crucial steps like unpivoting and handling missing values.
 * Robust Data Modeling & DAX: I successfully designed and implemented a robust data model within Power BI, defining relationships and creating powerful DAX measures and calculated columns. This allowed for dynamic aggregations, complex conditional logic, and the creation of new, insightful metrics.
 * Building Interactive Visualizations: I designed and implemented a dynamic and intuitive Power BI dashboard. By integrating diverse visual elements and interactive slicers, I learned to transform complex data into clear, compelling narratives, empowering user-driven exploration of HR trends.
 * Translating Data into Actionable Insights: A key focus for me was learning to articulate data findings into clear, actionable recommendations. This involved developing my ability to discern patterns, identify opportunities (e.g., gender pay gap, minimum wage non-compliance), and frame insights within the context of business challenges, directly informing potential HR strategies.
 * Structured Problem-Solving: I approached a diverse set of analytical questions systematically, from understanding demographic breakdowns to complex bonus calculations. This hands-on experience reinforced my structured and thorough approach to data-driven problem-solving.

📬 Connect with Me
I'm continuously learning and excited to connect with fellow data enthusiasts and professionals. Please feel free to reach out for questions, feedback on my work, or potential collaborations as I continue my journey in data analytics!
 * Obadire Samuel Abimbola
 * Email: samuelobadire176@gmail.com
 * Phone: +234 8025363954
 * LinkedIn: https://ng.linkedin.com/in/obadire-samuel-77397011a
