# Analytics Jobs Overview and Key Metrics
This dashboard, designed using 2024(?) data courtesy of Luke Barousse, provides information on job prevalence, salary, skill and degree information on top data career categories (e.g. data analyst, data scientist, machine learning engineer). It can be used by aspiring data professionals to gain insight on the most relevant skills to acquire, general information about number of job postings, reasonable salary expectations, etc.

## Page 1 - Overview
![Overview](/analytics_jobs_dashboard/ajd_project_page1.png)

This page displays 10 of the top job categories in the data field (left bar chart), listed in descending order of job counts within the set (>450k total jobs in the data set). It also displays ranked median yearly salaries for those 10 top job categories (right bar chart). The top card displays total job count, the top skill associated with job postings in that job title (all titles by default), and frequency of occurence for that skill within job postings. The top card can be filtered for a specific job title, by left clicking on that job's associated bar in either bar chart. Right clicking or hovering over a job's specific bar can allow for a detailed drillthrough for that specific job title.

## Page 2 - Job Specific Drillthrough
![Job_Specific_Metrics](/analytics_jobs_dashboard/ajd_project_page2.png)

This page features specific metrics for a selected job title from page 1, including the number of jobs with that title in the data set, % of those jobs which mention a formal degree in the posting, % of those jobs which contain direct mention of salary information. Below these cards are a bar chart displaying the 10 most frequently listed skills for that specific job within their respective job postings, and a gauge outputting salary range and median salary for the selected job.

### Tools Used
- Power BI
- DAX
- Drillthrough
- Tooltips
