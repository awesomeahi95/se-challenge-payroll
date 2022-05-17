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
3. [ Models ](#Models)    
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
* <strong>requirements.txt</strong>: text file with dependencies for running application
    
    
</details>

<a name="Technologies_Used"></a>
## Technologies Used:

<details>
<summary>Show/Hide</summary>
<br>

  
</details>

<a name="Models"></a>
## Models

<details>
<summary>Show/Hide</summary>
<br>

TimeReportEntry:

This table is where all the data from the CSV file is stored. So all the columns: date, hours_worked, employee_id, and job_group, but also an _id and the report_number to recall archived data from previous CSV uploads.

Employee:
    
This table is where the employee_id(s) are stored along with the employee's job_group
    
Job:

This table is where the the job_group and the wage for each job group is stored. This is used for calculating the amount paid for employees in the Payroll Report.

ReportDocument:

This table is for archiving the CSV report numbers/indexes for retrieving later and to check if an entry exist to avoid re-uploading identical data.
    
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

   /getEmployeePay

</details>

<a name="Instructions"></a>
## Instructions:

<details>
<summary>Show/Hide</summary>
<br>

1. Check if you have Python 3
```
python --version
```
If Python 2.x.x follow '1.1. Python 3 Upgrade Command' command then continue. If python 3.x.x ignore '1.1. Python 3 Upgrade Command' command and continue.
    
1.1. Python 3 Upgrade Command
```
```
    
2. Check if you have pip
```
```
If you do not have pip follow '2.1. Install pip' command then continue. If you have pip installed ignore '2.1. Install pip' command and continue.
    
2.1. Install pip
```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py
```
    
3. Install requirements.txt file to get required packages for running API.
```
pip install -r requirements.txt 
```
    
4. Run app.
```
python3 run.py
```
    
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
