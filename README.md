# Wave Software Development Challenge
This is my solution for the se-challenge-payroll API task. I have predominantly used the Python programming language for this solution. I have detailed the [ instructions ](#Instructions) to setup and run the API. I have also explained the files being used, the tools used, the layout of the database, how the endpoints work, and some evaluation.

## Project Description

My API solution achieves these two goals:

1. Upload a CSV file containing data on the number of hours worked per day per employee
2. Retrieve a report detailing how much each employee should be paid in each _pay period_

## Table of Contents
<details open>
<summary>Show/Hide</summary>
<br>

- [ Repository Files ](#Repository_Files)
- [ Technologies Used ](#Technologies_Used)
- [ Models ](#Models)    
- [ Endpoints ](#Endpoints)
- [ Instructions ](#Instructions)
- [ Evaluation ](#Evaluation)

</details>

<a name="Repository_Files"></a>
## Repository Files

<details open>
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

<details open>
<summary>Show/Hide</summary>
<br>

* Python 
* Flask
* SQLAlchemy
* SQLite
  
</details>

<a name="Models"></a>
## Models

<details open>
<summary>Show/Hide</summary>
<br>

<p align="center">
  <img src="https://github.com/awesomeahi95/se-challenge-payroll/blob/master/ModelsImage.png" width=600>
</p>    
    
<strong>TimeReportEntry</strong>

This table is where all the data from the CSV file is stored. So all the columns: ```date```, ```hours_worked```, ```employee_id```, and ```job_group```, but also an ```_id``` and the ```report_id``` to recall archived data from previous CSV uploads.

<strong>Employee</strong>
    
This table is where the ```employee_id``` are stored along with the employee's ```job_group```.
    
<strong>Job</strong>

This table is where the the ```job_group``` and the wage for each job group is stored. This is used for calculating the amount paid for employees in the Payroll Report.

<strong>ReportDocument</strong>

This table is for archiving the CSV report ```report_index``` for retrieving later and to check if an entry exist to avoid re-uploading identical data.
    
</details>

<a name="Endpoints"></a>
## Endpoints

<details open>
<summary>Show/Hide</summary>
<br>
    
We've agreed to build an API with the following endpoints to serve HTTP requests:

1. An endpoint for uploading a file.

    <strong>/uploadCSV</strong>

    When a new time report CSV is uploaded to this endpoint it will upload the CSV data to the sqlite database and return a String ```Successfully Uploaded```. If a time report ```time-report-{report_id}.csv``` has already been uploaded with the same ```report_id``` it will not be uploaded to the database and will return a String ```Time Report Entry Previously Submitted, Please Try Another File```.

2. An endpoint for retrieving a payroll report structured in the following way:

    <strong>/getEmployeePay</strong>
    
    This endpoint will return a JSON object with an employee pay report that looks like this:
    
```
{
  "payrollReport": {
    "employeeReports": [
      {
        "employeeId": "1",
        "payPeriod": {
          "startDate": "2023-01-01",
          "endDate": "2023-01-15"
        },
        "amountPaid": "$300.00"
      },
      {
        "employeeId": "1",
        "payPeriod": {
          "startDate": "2023-01-16",
          "endDate": "2023-01-31"
        },
        "amountPaid": "$80.00"
      },
      {
        "employeeId": "2",
        "payPeriod": {
          "startDate": "2023-01-16",
          "endDate": "2023-01-31"
        },
        "amountPaid": "$90.00"
      }
    ]
  }
}
```

</details>

<a name="Instructions"></a>
## Instructions:

<details open>
<summary>Show/Hide</summary>
<br>

<strong>Prerequisite is to have Python 3 installed.</strong>
    
### 1. Check if you have pip
```
```
If you do not have pip installed follow <strong>2. Install pip</strong> command then continue. If you have pip installed skip to <strong>3. Install dependencies</strong>.
    
### 2. Install pip
```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python3 get-pip.py
```
    
### 3. Install dependencies
```
pip install -r requirements.txt 
```
    
### 4. Run app
```
python3 run.py
```
    
</details>

<a name="Evaluation"></a>
## Evaluation

<details open>
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
