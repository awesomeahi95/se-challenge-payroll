# Wave Software Development Challenge
This is my solution for the se-challenge-payroll API task. I have predominantly used the Python programming language for this solution. I have detailed the [ instructions ](#Instructions) to setup and run the API. I have also explained the files being used, the tools.technologies used, the layout of the database, how the endpoints work, and some evaluation.

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
    * <strong>models.py</strong>: python file with that declares models used in database
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

This table is where all the data from the CSV file is stored. So all the columns from the CSV: ```date```, ```hours_worked```, ```employee_id```, and ```job_group```, and also an ```_id``` and the ```report_id``` to recall archived data from previous CSV uploads.

<strong>Employee</strong>
    
This table is where the ```employee_id``` are stored along with the employee's ```job_group```.
    
<strong>Job</strong>

This table is where the the ```job_group``` and the wage for each job group is stored. This is used for calculating the amount paid for employees in the Payroll Report.

<strong>ReportDocument</strong>

This table is for archiving the CSV report ```report_index``` for retrieving later, and to check if an entry exists to avoid re-uploading identical data.
    
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

2. An endpoint for retrieving a payroll report:

    <strong>/getEmployeePay</strong>
    
    This endpoint will return a JSON object with an employee pay report that looks like this:
    
```
{
    "payrollReport": {
        "employeeReports": [
            {
                "amountPaid": 150.0,
                "employeeId": 1,
                "payPeriod": {
                    "endDate": "2023-11-15",
                    "startDate": "2023-11-01"
                }
            },
            {
                "amountPaid": 220.0,
                "employeeId": 1,
                "payPeriod": {
                    "endDate": "2023-11-31",
                    "startDate": "2023-11-16"
                }
            },
            {
                "amountPaid": 930.0,
                "employeeId": 2,
                "payPeriod": {
                    "endDate": "2023-11-15",
                    "startDate": "2023-11-01"
                }
            },
            {
                "amountPaid": 930.0,
                "employeeId": 2,
                "payPeriod": {
                    "endDate": "2023-12-15",
                    "startDate": "2023-12-01"
                }
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

<strong>Prerequisite is to have Python 3 installed on your Mac or Linux system.</strong>
    
### 1. Check if you have pip
```
pip -V
```
If you do not have pip installed follow <strong>2. Install pip</strong> command then continue. If you have pip installed skip to <strong>3. Install dependencies</strong> command.
    
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
    * I expanded the original time report CSV table structure with a ```report_id``` that I extracted from the CSV file name and an incremental index for entries
    * I used SQLite as it requires no installation or configuration, to keep the app lite
    * I stuck with the universal company practice of keeping the ```employee_id``` as a String (as opposed to an Integer that may traditionally be used for a numerical index)
    
- How did I separate any concerns in my application? 
    * I went for a high level of separation of concerns so the API is not as modular as it could be:
        views - dealing with logic and endpoints
        models - outlining the models for the tables in the sqlite database
        
- How did I test that your implementation was correct?
    * I manually tested the endpoints using Postman POST requests for uploading the CSV to the database and Postman GET requests for retrieving the JSON object for the pay report
    * I created another CSV file with a different ```report_id``` and slightly different data to check how the API endpoints would deal with both previously uploaded CSVs and new CSVs
    
- If this application was destined for a production environment, what would I add or change?
    * Thorough automated tests implemented for more potential error scenarios
    * A frontend where a user would be able to upload a CSV file and also get a table output of the pay report
    * Better separation of concerns using blueprints
    
- What compromises did I have to make as a result of the time constraints of this challenge?
    * I did not approach the API with a Test Driven Development approach - instead I created an API and tested/debugged manually with Postman
    * I had less modularity with the layers of the API as the solution's delivery was prioritized over better practices with separation of concerns which would benefit future development
  
  
</details>
