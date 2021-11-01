# Classification Web Application of Disaster Messages

In this project, you'll analyze disaster data from [Figure Eight](https://www.figure-eight.com/) to build a model for an API that classifies disaster messages.


### Table of Contents

1. [Project Objectives](#objectives)
2. [Project Description](#descriptions)
3. [Installation](#installation)
4. [Folder Structure](#files)
5. [Instructions](#instructions)

## Project Objectives<a name="objectives"></a>

The aim of this project is to classify disaster messages into categories.  We start by analyzing disaster data collected from [Figure Eight Website](https://www.figure-eight.com/) and build a model that could access using API interface to classify new disaster messages. 
Web application allows the users to input a new message and get classification results in several categories. The web application also displays visualizations of the data.

## Project Descriptions<a name = "descriptions"></a>
The project has three componants which are:

**1st componant is ETL Pipeline:** `etl_pipeline.py` file contain the script to create ETL pipline which:
  - Loads the `messages` and `categories` datasets from csv files into dataframes
  - Merges the two datasets into single dataframe using id 
  - Cleans the data and remove doublcates
  - Stores clean data into a SQLite database file to be used in ML pipeline later

**2nd componant is ML Pipeline:** `ml_pipeline.py` file contain the script to create ML pipline which:
  - Loads data from the SQLite database file
  - Splits the dataset into training and test sets
  - Builds a text processing and machine learning pipeline
  - Trains and tunes a model using GridSearchCV
  - Outputs the performance results of the test set
  - Exports the final model as a pickle file

**3rd componant is Web Application:** the web app enables the user to enter a disaster message, and then view the categories of the message.
The web app also contains some visualizations that describe the data. 
  - Loads the model from pickle file  
  - Build Web UI and show data statistics 
  - Wait for user message
  - Classify user message 
  - display result as list of related categories of the user message   


## Installation <a name="installation"></a>

All libraries are available in Anaconda base distribution of Python versions 3.*. The used libraries are:

- pandas : used to load data 
- nltk : used for textual data analysis
- sklearn : used for building classfication model 
- pickle : used to store model into file
- Flask : used for builing web application 
- plotly : used to create chart
- sqlite3 : used to store clean and analyize data 
- sqlalchemy : used to create database 
- re : to search data based on regulare expression 
- sys : used internally by obove packages


## Folder Structure <a name="files"></a>
The files structure is arranged as below:

	- README.md: read me file
	- ETL Pipeline Preparation.ipynb: contains ETL pipeline preparation code
	- ML Pipeline Preparation.ipynb: contains ML pipeline preparation code
	- workspace
		- \app\
			- run_local.py: flask file to run the app
		- \app\templates
			- master.html: main page of the web application 
			- go.html: result web page
		- \data
			- disaster_categories.csv: categories dataset
			- disaster_messages.csv: messages dataset
			- DisasterResponse.db: disaster response database
			- etl_pipeline.py: ETL process
		- \models
			- ml_pipeline.py: classification code
			- classifier.pkl: classification model pickle file

## Instructions <a name="instructions"></a>
To execute the app follow the instructions:
1. To set up database and model: run the following commands in the project's root directory.

    - Execute ETL pipeline pthon code for cleaning data then storing it into sqllite database
        `python data/process_data.py data/disaster_messages.csv data/disaster_categories.csv data/DisasterResponse.db`
    - Execute machine learning pipeline to trains classifier and save the model into pickle file
        `python models/train_classifier.py data/DisasterResponse.db models/classifier.pkl`

2. To run web app, exeute the command in the app's directory root after copying classifier.pkl into the models subfolder 
    `python run_local.py`

3. Go to http://localhost:5001/
