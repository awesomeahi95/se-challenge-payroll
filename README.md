# Wave Software Development Challenge
This is my solution for the se-challenge-payroll API task.

I have predominantly used the Python programming language for this solution.

## Project Description

My API solution achieves these two goals:

1. Upload a CSV file containing data on the number of hours worked per day per employee
2. Retrieve a report detailing how much each employee should be paid in each _pay period_

## Repository Files

<details>
<a name="Repository Files"></a>
<summary>Show/Hide</summary>
<br>
    
* <strong>[ WaveApp ]</strong>: folder containing all data files
    * <strong>1.tripadvisor_scraped_hotel_reviews.csv</strong>: webscraped data before any changes
    * <strong>2.hotel_reviews_structured.csv</strong>: data after balancing and cleaning
    * <strong>3.x_train_data.csv</strong>: training data with x values from preprocessed dataset
    * <strong>3.y_train_data.csv</strong>: training data with y values from preprocessed dataset
    * <strong>4.x_test_data.csv</strong>: test data with x values from preprocessed dataset
    * <strong>4.y_test_data.csv</strong>: test data with y values from preprocessed dataset
* <strong>[ Images ](https://github.com/awesomeahi95/Hotel_Review_NLP/tree/master/Images)</strong>: folder containing images used for README and presentation pdf
* <strong>[ Models ](https://github.com/awesomeahi95/Hotel_Review_NLP/tree/master/Models)</strong>: folder containing trained models saved with pickle
    * <strong>Adabooost.pkl, Decision Tree.pkl, KNN.pkl, Logistic Regression.pkl, Naive Bayes.pkl, Neural Network.pkl, Random Forest.pkl, Stacking.pkl, SVM.pkl, Voting.pkl, XGBoost.pkl</strong>
* <strong>[ Tripadvisor_Webscrape ](https://github.com/awesomeahi95/Hotel_Review_NLP/tree/master/Tripadvisor_Webscrape)</strong>: folder containing all webscraping files
    * <strong>Tripadvisor</strong>: folder containing .py files and spiders used
        * <strong>spiders</strong>: folder containing spider files and datasets
            * <strong>hotels.py</strong>: main spider .py file for scraping hotel reviews from Tripadvisor
            * <strong>tripadvisor_scraped_hotel_reviews.csv</strong>: csv file with data to be used for project
        * <strong>_init_.py, items.py, middlewares.py, pipelines.py, settings.py: default scrapy files used for webscrape</strong>
    * <strong>scrapy.cfg</strong>: scrap config file
* <strong>[ 1.Webscraping_Early_EDA_and_Cleaning.ipynb ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/1.Webscraping_Early_EDA_and_Cleaning.ipynb)</strong>: notebook with early data exploration and data manipulation
* <strong>[ 2.Further_EDA_and_Preprocessing.ipynb ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/2.Further_EDA_and_Preprocessing.ipynb)</strong>: notebook with feature engineering and nlp preprocessing
* <strong>[ 3.Modelling_and_Hyperparameter_Tuning.ipynb ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/3.Modelling_and_Hyperparameter_Tuning.ipynb)</strong>: notebook with all the models created
* <strong>[ 4.Evaluation ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/4.Evaluation.ipynb)</strong>: notebook with final model selection, testing, and model evaluation
* <strong>[ 5.Neural_Network_Modelling ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/5.Neural_Network_Modelling.ipynb)</strong>: notebook with an extra model training using neural networks
* <strong>[ 6.Revaluation_and_Deployment ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/6.Revaluation_and_Deployment.ipynb)</strong>: notebook comparing old best model and NN model, and deployment
* <strong>[ Classification.py ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/Classification.py)</strong>: contains classes with classifcation methods
* <strong>[ Ensemble.py ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/Ensemble.py)</strong>: contains classes with ensemble methods
* <strong>[ Helpers_NN.py ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/Helpers_NN.py)</strong>: contains methods used to help with neural network processes
* <strong>[ Hilton_Hotel_App.py ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/Hilton_Hotel_App.py)</strong>: contains script to run app
* <strong>[ Hilton__Hotel_Presentation.pdf ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/Hilton_Hotel_Presentation.pdf)</strong>: presentation summarising project case, processese, and findings
* <strong>[ Procfile ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/Procfile)</strong>: file supporting Heroku application
* <strong>[ requirements.txt ](https://github.com/awesomeahi95/Hotel_Review_NLP/blob/master/requirements.txt)</strong>: dependencies for heroku application
</details>

## Models

ReportDocument:

This table is where all the data from the CSV file is stored. So all the columns: date, hours_worked, employee_id, and job_type, but also an index and the report id to recall archived data from previous CSV uploads.

JobTypes:

This table is where the the job group and the wage for each job group is stored. This is used for calculating the amount paid for employees in the Payroll Report.

Reports:

This table is for archiving the CSV report numbers for retrieving later and to check if an entry exist to avoid re-uploading identical data.

### What your API must do:

We've agreed to build an API with the following endpoints to serve HTTP requests:

1. An endpoint for uploading a file.

   - This file will conform to the CSV specifications outlined in the previous section.
   - Upon upload, the timekeeping information within the file must be stored to a database for archival purposes.
   - If an attempt is made to upload a file with the same report ID as a previously uploaded file, this upload should fail with an error message indicating that this is not allowed.

2. An endpoint for retrieving a payroll report structured in the following way:

   _NOTE:_ It is not the responsibility of the API to return HTML, as we will delegate the visual layout and redering to the front end. The expectation is that this API will only return JSON data.

   - Return a JSON object `payrollReport`.
   - `payrollReport` will have a single field, `employeeReports`, containing a list of objects with fields `employeeId`, `payPeriod`, and `amountPaid`.
   - The `payPeriod` field is an object containing a date interval that is roughly biweekly. Each month has two pay periods; the _first half_ is from the 1st to the 15th inclusive, and the _second half_ is from the 16th to the end of the month, inclusive. `payPeriod` will have two fields to represent this interval: `startDate` and `endDate`.
   - Each employee should have a single object in `employeeReports` for each pay period that they have recorded hours worked. The `amountPaid` field should contain the sum of the hours worked in that pay period multiplied by the hourly rate for their job group.
   - If an employee was not paid in a specific pay period, there should not be an object in `employeeReports` for that employee + pay period combination.
   - The report should be sorted in some sensical order (e.g. sorted by employee id and then pay period start.)
   - The report should be based on all _of the data_ across _all of the uploaded time reports_, for all time.

As an example, given the upload of a sample file with the following data:

   | date       | hours worked | employee id | job group |
   | ---------- | ------------ | ----------- | --------- |
   | 4/1/2023   | 10           | 1           | A         |
   | 14/1/2023  | 5            | 1           | A         |
   | 20/1/2023  | 3            | 2           | B         |
   | 20/1/2023  | 4            | 1           | A         |

A request to the report endpoint should return the following JSON response:

   ```json
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

We consider ourselves to be language agnostic here at Wave, so feel free to use any combination of technologies you see fit to both meet the requirements and showcase your skills. We only ask that your submission:

- Is easy to set up
- Can run on either a Linux or Mac OS X developer machine
- Does not require any non open-source software
- Includes all the source code you write for the submission, including any models used for setting up your database

### Documentation:

Please commit the following to this `README.md`:

1. Instructions on how to build/run your application
1. Answers to the following questions:
   - How did you test that your implementation was correct?
   - If this application was destined for a production environment, what would you add or change?
   - What compromises did you have to make as a result of the time constraints of this challenge?

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
