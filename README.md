# Wave Software Development Challenge
This is my solution for the se-challenge-payroll API task.

I have predominantly used the Python programming language for this solution.

## Project Description

My API solution achieves these two goals:

1. Upload a CSV file containing data on the number of hours worked per day per employee
2. Retrieve a report detailing how much each employee should be paid in each _pay period_

## Table of Contents
<details open>
<summary>Show/Hide</summary>
<br>

1. [ Repository Files ](#Repository_Files)
2. [ Schema ](#Schema)    
3. [ Endpoints ](#Endpoints)
4. [ EInstructions ](#Instructions)
   * [ 1. Webscraping, Early EDA, and Cleaning ](#Webscraping_Early_EDA_and_Cleaning)
       * [ Webscraping ](#Webscraping)
       * [ Early EDA and Cleaning](#Early_EDA_and_Cleaning)
   * [ 2. Further EDA and Preprocessing ](#Further_EDA_and_Preprocessing) 
   * [ 3. Modelling and Hyperparameter Tuning ](#Modelling)
   * [ 4. Evaluation ](#Evaluation)
       * [ Future Improvements ](#Future_Improvements)
   * [ 5. Neural Network Modelling ](#Neural_Network_Modelling)
   * [ 6. Revaluation and Deployment ](#Revaluation)
</details>

## Repository Files

<details>
<a name="Repository Files"></a>
<summary>Show/Hide</summary>
<br>
    
* <strong>WaveApp</strong>: folder containing all data files
    * <strong>__init__.py</strong>: python file for intializing flask application
    * <strong>views.py</strong>: python file with CSV_Upload and Payroll_Report endpoints for API
    * <strong>models.py</strong>: python file with that declares models used in schema
* <strong>run.py</strong>: python file to run application
</details>

## Schema

<details>
<a name="Schema"></a>
<summary>Show/Hide</summary>
<br>

ReportDocument:

This table is where all the data from the CSV file is stored. So all the columns: date, hours_worked, employee_id, and job_type, but also an index and the report id to recall archived data from previous CSV uploads.

JobTypes:

This table is where the the job group and the wage for each job group is stored. This is used for calculating the amount paid for employees in the Payroll Report.

Reports:

This table is for archiving the CSV report numbers for retrieving later and to check if an entry exist to avoid re-uploading identical data.
    
</details>

### Endpoints

<details>
<a name="Endpoints"></a>
<summary>Show/Hide</summary>
<br>
    
We've agreed to build an API with the following endpoints to serve HTTP requests:

1. An endpoint for uploading a file.

   /uploadCSV

2. An endpoint for retrieving a payroll report structured in the following way:

   /getPayrollReport

</details>


### Instructions:

<details>
<a name="Instructions"></a>
<summary>Show/Hide</summary>
<br>
    

Please commit the following to this `README.md`:

1. Instructions on how to build/run your application
1. Answers to the following questions:
   - How did you test that your implementation was correct?
   - If this application was destined for a production environment, what would you add or change?
   - What compromises did you have to make as a result of the time constraints of this challenge?

</details>

## Submission Instructions

1. Clone the repository.
1. Complete your project as described above within your local repository.
1. Ensure everything you want to commit is committed.
1. Create a git bundle: `git bundle create your_name.bundle --all`
1. Email the bundle file to [dev.careers@waveapps.com](dev.careers@waveapps.com) and CC the recruiter you have been in contact with.

## Evaluation

Evaluation of your submission will be based on the following criteria.

1. Did you follow the instructions for submission?
1. Did you complete the steps outlined in the _Documentation_ section?
1. Were models/entities and other components easily identifiable to the
   reviewer?
1. What design decisions did you make when designing your models/entities? Are
   they explained?
1. Did you separate any concerns in your application? Why or why not?
1. Does your solution use appropriate data types for the problem as described?
