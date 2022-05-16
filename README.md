# Wave Software Development Challenge
This is my solution for the se-challenge-payroll API task. I have predominantly used the Python programming language for this solution.

## Project Description

My API solution achieves these two goals:

1. Upload a CSV file containing data on the number of hours worked per day per employee
2. Retrieve a report detailing how much each employee should be paid in each _pay period_

## Table of Contents
<details open>
<summary>Show/Hide</summary>
<br>

1. [ Repository Files ](#Repository_Files)
2. [ Technologies Used ](#Technologies_Used)
3. [ Schema ](#Schema)    
4. [ Endpoints ](#Endpoints)
5. [ Instructions ](#Instructions)
6. [ Evaluation ](#Evaluation)

</details>

<a name="Repository_Files"></a>
## Repository Files

<details>
<summary>Show/Hide</summary>
<br>
    
* <strong>WaveApp</strong>: folder containing all data files
    * <strong>__init__.py</strong>: python file for intializing flask application
    * <strong>views.py</strong>: python file with CSV_Upload and Payroll_Report endpoints for API
    * <strong>models.py</strong>: python file with that declares models used in schema
* <strong>run.py</strong>: python file to run application
    
</details>

<a name="Technologies_Used"></a>
## Technologies Used:

<details>
<summary>Show/Hide</summary>
<br>

  
</details>

<a name="Schema"></a>
## Schema

<details>
<summary>Show/Hide</summary>
<br>

ReportDocument:

This table is where all the data from the CSV file is stored. So all the columns: date, hours_worked, employee_id, and job_type, but also an index and the report id to recall archived data from previous CSV uploads.

JobTypes:

This table is where the the job group and the wage for each job group is stored. This is used for calculating the amount paid for employees in the Payroll Report.

Reports:

This table is for archiving the CSV report numbers for retrieving later and to check if an entry exist to avoid re-uploading identical data.
    
</details>

<a name="Endpoints"></a>
## Endpoints

<details>
<summary>Show/Hide</summary>
<br>
    
We've agreed to build an API with the following endpoints to serve HTTP requests:

1. An endpoint for uploading a file.

   /uploadCSV

2. An endpoint for retrieving a payroll report structured in the following way:

   /getPayrollReport

</details>

<a name="Instructions"></a>
## Instructions:

<details>
<summary>Show/Hide</summary>
<br>

</details>

<a name="Evaluation"></a>
## Evaluation

<details>
<summary>Show/Hide</summary>
<br>
  
- What design decisions did I make when designing your models/entities?

- How did I separate any concerns in my application? 

- How did I test that your implementation was correct?
    
- If this application was destined for a production environment, what would I add or change?
    
- What compromises did I have to make as a result of the time constraints of this challenge?
  
  
</details>

## Submission Instructions

1. Clone the repository.
1. Complete your project as described above within your local repository.
1. Ensure everything you want to commit is committed.
1. Create a git bundle: `git bundle create your_name.bundle --all`
1. Email the bundle file to [dev.careers@waveapps.com](dev.careers@waveapps.com) and CC the recruiter you have been in contact with.
