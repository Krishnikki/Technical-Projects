# Data Science Salary Estimator 
  Author: Y Krishna Teja 23M0036@iitb.ac.in

  # Problem Statement
  In the dynamic landscape of data science, determining a competitive and equitable salary for professionals is a complex challenge. This project addresses this issue by employing advanced data science techniques to develop a salary estimation model tailored to data science roles. Leveraging a dataset consisting of over a thousand job descriptions scraped from Glassdoor, along with features quantifying skill preferences, the project seeks to create a predictive model that accurately estimates data science salaries.

  # Data Set used
  **Dataset Description:**

The dataset utilized in this project is a comprehensive collection of job descriptions obtained from Glassdoor, a prominent job search and company review platform. This dataset is tailored to data science roles and forms the foundation for developing a predictive salary estimation model. It encompasses a diverse range of job descriptions from various industries and locations, capturing the nuances of skill requirements and job expectations.

**Dataset Content:**

The dataset contains a multitude of attributes that capture essential information from each job description. These attributes include, but are not limited to:

- Job Title: The title of the data science role advertised in the job description.
- Company: The name of the company or organization offering the position.
- Job Description Text: The textual content describing the responsibilities, qualifications, and expectations of the data science role.
- Skills Emphasis: Indicators quantifying the emphasis placed on specific skills such as Python, Excel, AWS, and Spark within the job description.

**Dataset Preparation:**

The dataset undergoes several stages of preparation to ensure its suitability for analysis and model development:

1. **Web Scraping:** Data is collected using web scraping techniques from Glassdoor, capturing a wide array of job descriptions for data science roles across industries and regions.
2. **Data Cleaning:** The collected data is cleaned to remove irrelevant or duplicate entries, correct inconsistencies, and handle missing values.
3. **Text Preprocessing:** Natural language processing techniques are applied to preprocess the job description text, including tokenization, stopword removal, and stemming to enhance the quality of textual features.
4. **Feature Engineering:** Skill emphasis indicators are generated to quantify the importance of specific skills mentioned in the job descriptions.

**Dataset Utilization:**

The dataset serves as the core input for the development of the predictive salary estimation model. By leveraging the attributes captured in the dataset, the project aims to build a model that accurately estimates salaries for data science roles based on job description content and skill emphasis. The dataset allows for the exploration of how various skills impact salary expectations in the data science job market.

The utilization of this dataset underscores the project's data-driven approach to addressing the challenge of salary estimation, providing valuable insights that contribute to informed salary negotiations and equitable compensation practices within the field of data science.

# Steps 
* Scraped over 1000 job descriptions from glassdoor using python and selenium
* Engineered features from the text of each job description to quantify the value companies put on python, excel, aws, and spark. 
* Optimized Linear, Lasso, and Random Forest Regressors using GridsearchCV to reach the best model. 


## Code and Resources Used 
**Python Version:** 3.6  
**Packages:** pandas, numpy, sklearn, matplotlib, seaborn, selenium, flask, json, pickle  
**For Web Framework Requirements:**  ```pip install -r requirements.txt```  

## Web Scraping
Tweaked the web scraper github repo (above) to scrape 1000 job postings from glassdoor.com. With each job, we got the following:
*	Job title
*	Salary Estimate
*	Job Description
*	Rating
*	Company 
*	Location
*	Company Headquarters 
*	Company Size
*	Company Founded Date
*	Type of Ownership 
*	Industry
*	Sector
*	Revenue
*	Competitors 

## Data Cleaning
After scraping the data, I needed to clean it up so that it was usable for our model. I made the following changes and created the following variables:

*	Parsed numeric data out of salary 
*	Made columns for employer provided salary and hourly wages 
*	Removed rows without salary 
*	Parsed rating out of company text 
*	Made a new column for company state 
*	Added a column for if the job was at the company’s headquarters 
*	Transformed founded date into age of company 
*	Made columns for if different skills were listed in the job description:
    * Python  
    * R  
    * Excel  
    * AWS  
    * Spark 
*	Column for simplified job title and Seniority 
*	Column for description length 

## EDA
I looked at the distributions of the data and the value counts for the various categorical variables. Below are a few highlights from the pivot tables. 

![alt text](https://github.com/PlayingNumbers/ds_salary_proj/blob/master/salary_by_job_title.PNG "Salary by Position")
![alt text](https://github.com/PlayingNumbers/ds_salary_proj/blob/master/positions_by_state.png "Job Opportunities by State")
![alt text](https://github.com/PlayingNumbers/ds_salary_proj/blob/master/correlation_visual.png "Correlations")

## Model Building 

First, I transformed the categorical variables into dummy variables. I also split the data into train and tests sets with a test size of 20%.   

I tried three different models and evaluated them using Mean Absolute Error. I chose MAE because it is relatively easy to interpret and outliers aren’t particularly bad in for this type of model.   

I tried three different models:
*	**Multiple Linear Regression** – Baseline for the model
*	**Lasso Regression** – Because of the sparse data from the many categorical variables, I thought a normalized regression like lasso would be effective.
*	**Random Forest** – Again, with the sparsity associated with the data, I thought that this would be a good fit. 

## Model performance
The Random Forest model far outperformed the other approaches on the test and validation sets. 
*	**Random Forest** : MAE = 11.22
*	**Linear Regression**: MAE = 18.86
*	**Ridge Regression**: MAE = 19.67
 



