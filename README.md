# Capstone-Project
# Spark Project: Sparkify
## Table of Contents

- [Introduction](#introduction)
  - [Project Overview](#overview)
  - [Problem Statement](#problem)
  - [Metrics](#metrics)
- [Analysis](#analysis)
  - [Data Exploration](#explore)
  - [Data Visualisation](#visualisation)
- [Methodology](#method)
  - [Data Preprocessing](#preprocessing)
  - [Implementation](#implement)
  - [Refinement](#refine)
- [Conclusion](#conclusion)
  - [Reflection](#reflect)
  - [Challenges](#challenges)
- [Files](#files)
- [Software Requirements](#sw_reqs)
- [Acknowledgement](#ack)

***

<a id="introduction"></a>

## I. Introduction

<a id="overview"></a>

### Project Overview
[Spotify](https://www.spotify.com/) is a Swedish music streaming and media services provider. 
The main project's  aim is to predict users churn for Sparkify (a Spotify-style  a mythical music service).
Like every Internet service Spotify makes money from user activity.
Sparkify's users perform different actions on the service pages. Project's data is a log file. It's mean that the data have more than one record for each user.
The project's full dataset is 12GB, of which you can analyze a mini subset is 128 MB (file mini_sparkify_event_data.json). 

<a id="problem"></a>

### Problem Statement
The case solvation consists of:
- determine target to predict based on the information in 18th feature columns;
- predict users churn.

<a id="metrics"></a>

### Metrics

The dataser has only 225 unique users, 52 of them churned.
The dataset is unbalanced.
If we use accuracy to evaluate a model we will run into a case that
all predictions are churn or not churn.
We have to use F1-Score to
evaluate our model.
<a id="analysis"></a>

## II. Analysis

<a id="explore"></a>

### Data Exploration

The shape of the dataset is 286500 rows and 18 columns.

The filled row shows:

<img src="./images/filled_row.png">

The record display that the user Colin Freeman listened the song Rockpools by Martha Tilston. The dataframe is not a dataset. It is a part of log file. This datafame does not consist of any features could be using for prediction directly.
All of the dataframe columns are using to describe a user or a user action.
We can see the 18th columns in the dataframe and we have to determine which column contains the information about user churn. Actually, the columns listed below include information about:
* artist - a singer name or a group name;
* firstName - a user first name;
* gender - a user gender;
* itemInSession - some identificator or count;
* lastName - a user last name;
* length - in this case a length of a user sessions or a duration of the song;
* level - a free or paid account status;
* location - a user location;
* method - a http method;
* registration - a user registraion date;
* sessionId - a user session identificatior;
* song - a song name;
* status - a request status code response;
* ts - a user session timestamp;
* userAgent - a user browser type;
* userId - a user registration identificatior.

We have to explore dataframe columns.
And the first task is to determine target to predict.
Column 'page' have this information.

<img src="./images/page_values.png" width="30%">

The visiting counts of the 'Cancel' and 'Cancellation Confirmation' are 52. These rows contain the information about churned users.

<a id="visualisation"></a>

### Data Visualisation

All plots you can see at the appropriate part of a jupyter notebook.

<a id="method"></a>

## III. Methodology

<a id="preprocessing"></a>

### Data Preprocessing

1. Handling null values.

Initial dataset has null values in some columns.

 <img src="./images/null_values.png">

We can see that columns 'firstName' and 'LastName' have 8346 null values. Furthermore, the column 'userAgent' includes the 8346 null values too. Nevertheless, the column 'userId' has not null values. We have to check the column 'userId' on invalid data, like an empty row.

An empty row looks like:

 <img src="./images/typical_row_with_null.png" width="50%">
 
 We can see the 'Logged Out' value in the 'auth' column where the 'userId' column value is an empty row.
What the values does the 'auth' column include, except 'Logged Out'?

<img src="./images/row_with_empty_userid.png" width="50%">

The plot show us that the 'auth' column consists of the 'Logged Out' and the 'Guest' values.
We can drop all rows with the 'Logged Out' and the 'Guest' values due to these rows are the audit records and have not the information about a user churn or any user activity.

The remained rows with null values we can not drop due to they have information to predict users churn.

2. Categorical features handling.

Some columns in tha dataset have categorical values. We have to change them to '0' and '1' values using 'dummy' columns.

3. Numerical features.

Each user has different count of listened song, completed sessions. We should create columns contained of users listened songs and completed sessions. These columns describe the users activity. We can call the columns as the first part users activity.

The second part users activity are the visited pages. As we saw earlier the users did not cancel a subscription visited more times the pages 'Add Friend', 'Add to Playlist', 'Save Settings', 'Submit Upgrade', 'Thumbs Up'. We can create some columns to store information about users activity on the pages.

Firstly, we create several pandas dataframes with count of visited pages. Secondly, we create the columns with agregated data in the spark dataframe. Thirdly, we recreate the spark dataframe and drop columns with raw categoric



<a id="implement"></a>

### Implementation

[PySpark's MLlib](https://spark.apache.org//docs/latest/api/python/pyspark.ml.html) has the most common machine learning classification
algorithms. 
In the project we are using three of them:
- [Random Forest Classifier](https://spark.apache.org/docs/latest/ml-classification-regression.html#random-forest-classifier)
- [Logistic Regression](https://spark.apache.org/docs/latest/ml-classification-regression.html#logistic-regression)
- [Gradient Boosting Trees](rhttps://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-tree-classifier)

<a id="refine"></a>

### Refinement

Since the class distribution is highly imbalanced, we will perform random
undersampling to optimize our **F1 score**.


<a id="files"></a>

## V. Files

1. Folders 'images' consist of the images that you saw above.
   
2. The file mini_sparkify_event_data.json is our initial dataset.
    
3. The file Sparkify.ipynb is a jupyter notebook with full project's code.

