# Capstone-Project
# Spark Project: Sparkify
## Table of Contents

- [Introduction](#introduction)
  - [Project Overview](#overview)
  - [Problem Statement](#problem)
  - [Metrics](#metrics)
- [Analysis](#analysis)
  - [Data Exploration](#explore)
  - [Data Visualisation](#data_viz)
- [Methodology](#method)
  - [Data Preprocessing](#data_prep)
  - [Implementation](#implement)
  - [Refinement](#refine)
- [Conclusion](#conclusion)
  - [Reflection](#reflect)
  - [Challenges](#challenges)
- [Files](#files)
- [Software Requirements](#sw_reqs)
- [References](#refs)
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

The dataser has only  **225** unique users, **only 52** churned **(23.5%).**
The dataset is unbalanced.
If we use accuracy to evaluate a model we will run into a case that
all predictions are churn or not churn.
. We have to use **F1-Score** to
evaluate our model.
