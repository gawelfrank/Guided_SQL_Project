# Guided SQL Project — Data Analyst Job Market Analysis

## Introduction

This project is a guided SQL portfolio project focused on analyzing Data Analyst job postings using PostgreSQL. The purpose of this project is to demonstrate my ability to write structured SQL queries, extract meaningful insights from real-world datasets, and present findings clearly for business and analytical decision-making.

The analysis focuses on identifying high-paying Data Analyst roles, determining which skills are most in-demand, and understanding which skills provide the highest salary value. This project was completed using PostgreSQL and Visual Studio Code (VS Code) as the primary query environment.

This repository is part of my professional development journey toward becoming a Data Analyst and showcases my SQL querying, analytical thinking, and data exploration skills.

---

## Background

The demand for Data Analysts continues to grow rapidly across industries. However, understanding which skills are most valuable, both in terms of demand and salary, is critical for career planning and workforce insights.

This project analyzes job posting data to answer key questions such as:

- What are the highest-paying Data Analyst jobs?
- What skills are required for the highest-paying roles?
- Which skills are most in demand?
- Which skills command the highest salaries?
- Which skills offer the best combination of high demand and high salary?

---

## Tools I Used

- **PostgreSQL**  
  Database system used for storing and querying job posting data

- **Visual Studio Code (VS Code)**  
  SQL query editor and development environment

- **SQL**  
  Used for data extraction, joins, aggregations, and analysis

- **Git & GitHub**  
  Version control and portfolio hosting

- **ChatGPT**  
  Used as a learning and productivity support tool to improve understanding, refine queries, and enhance documentation

---

## The Analysis

This project explores the Data Analyst job market through several focused SQL analyses.

### Top Paying Data Analyst Jobs

This query identifies the highest-paying Data Analyst roles based on average yearly salary.

```sql
SELECT
    job_title,
    job_location,
    salary_year_avg,
    job_posted_date
FROM job_postings_fact
WHERE
    job_title_short = 'Data Analyst'
    AND salary_year_avg IS NOT NULL
ORDER BY salary_year_avg DESC
LIMIT 10;
```

**Insight:**  
High-paying Data Analyst roles are often associated with companies that require strong technical skills and experience with data tools and platforms.

---

### Skills Required for Top Paying Jobs

This query identifies the skills required for the highest-paying Data Analyst roles.

```sql
SELECT
    skills_dim.skills,
    job_postings_fact.salary_year_avg
FROM job_postings_fact
JOIN skills_job_dim
    ON job_postings_fact.job_id = skills_job_dim.job_id
JOIN skills_dim
    ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_postings_fact.job_title_short = 'Data Analyst'
    AND job_postings_fact.salary_year_avg IS NOT NULL
ORDER BY salary_year_avg DESC;
```

**Insight:**  
Higher-paying roles frequently require technical skills such as SQL, Python, cloud technologies, and business intelligence tools.

---

### Most In-Demand Skills

This analysis identifies which skills appear most frequently in job postings.

```sql
SELECT
    skills_dim.skills,
    COUNT(skills_job_dim.skill_id) AS demand_count
FROM skills_job_dim
JOIN skills_dim
    ON skills_job_dim.skill_id = skills_dim.skill_id
JOIN job_postings_fact
    ON skills_job_dim.job_id = job_postings_fact.job_id
WHERE job_postings_fact.job_title_short = 'Data Analyst'
GROUP BY skills_dim.skills
ORDER BY demand_count DESC
LIMIT 10;
```

**Insight:**  
SQL, Excel, Tableau, and Power BI are consistently among the most in-demand skills.

---

### Highest Paying Skills

This analysis identifies which skills are associated with the highest average salaries.

```sql
SELECT
    skills_dim.skills,
    AVG(job_postings_fact.salary_year_avg) AS avg_salary
FROM skills_job_dim
JOIN skills_dim
    ON skills_job_dim.skill_id = skills_dim.skill_id
JOIN job_postings_fact
    ON skills_job_dim.job_id = job_postings_fact.job_id
WHERE
    job_postings_fact.salary_year_avg IS NOT NULL
    AND job_postings_fact.job_title_short = 'Data Analyst'
GROUP BY skills_dim.skills
ORDER BY avg_salary DESC
LIMIT 10;
```

**Insight:**  
Skills related to advanced analytics, programming, and cloud platforms tend to offer higher salary potential.

---

### Optimal Skills (High Demand + High Salary)

This analysis identifies skills that provide the best combination of strong demand and high salary.

```sql
SELECT
    skills_dim.skills,
    COUNT(skills_job_dim.skill_id) AS demand_count,
    AVG(job_postings_fact.salary_year_avg) AS avg_salary
FROM skills_job_dim
JOIN skills_dim
    ON skills_job_dim.skill_id = skills_dim.skill_id
JOIN job_postings_fact
    ON skills_job_dim.job_id = job_postings_fact.job_id
WHERE
    job_postings_fact.salary_year_avg IS NOT NULL
    AND job_postings_fact.job_title_short = 'Data Analyst'
GROUP BY skills_dim.skills
ORDER BY demand_count DESC, avg_salary DESC
LIMIT 10;
```

**Insight:**  
SQL, Python, and BI tools provide the strongest balance between demand and earning potential.

---

## What I Learned

Through this project, I developed and strengthened the following skills:

**SQL Skills**

- Writing SELECT, WHERE, GROUP BY, ORDER BY, and JOIN queries
- Using aggregate functions such as COUNT() and AVG()
- Combining multiple tables using relational joins
- Writing efficient and readable SQL queries

**Analytical Skills**

- Translating business questions into SQL queries
- Identifying trends in job market data
- Evaluating relationships between skills and salary
- Drawing meaningful conclusions from data

**Technical Workflow**

- Using PostgreSQL as a query environment
- Writing SQL queries in VS Code
- Organizing a professional GitHub project
- Using Git for version control

---

## Conclusions

This project demonstrates how SQL can be used to extract meaningful insights from real-world job market data.

**Key Takeaways:**

- SQL is the most essential skill for Data Analysts
- Specialized technical skills often lead to higher salaries
- High-demand skills provide the best career opportunities
- SQL enables effective analysis and decision-making using structured data

This project reflects my ability to analyze datasets, write professional SQL queries, and present insights clearly.

---

## Transparency Statement

This project was completed as part of my learning journey toward becoming a Data Analyst.

This project was guided by instructional material from **Luke Barousse’s SQL course**, which provided the overall learning structure and project framework.

However, all SQL queries, analysis, and implementation were written and executed independently by me to develop and demonstrate my own SQL skills.

I also used **ChatGPT as a learning and productivity tool** to:

- Improve understanding of SQL concepts
- Refine explanations and documentation
- Improve clarity and professionalism

This project represents my independent learning and skill development.

---

## Project Structure

```
Guided_SQL_Project/
│
├── README.md
│
├── sql_queries/
│   ├── 1_top_paying_jobs.sql
│   ├── 2_skills_for_top_paying_jobs.sql
│   ├── 3_most_in_demand_skills.sql
│   ├── 4_highest_paying_skills.sql
│   └── 5_optimal_skills.sql
│
└── notes/
    └── analysis_notes.md
```

---

**Author:** Frank Gawel  
**Database:** PostgreSQL  
**Environment:** VS Code  
**Project Type:** SQL Portfolio Project  
**Career Goal:** Data Analyst
