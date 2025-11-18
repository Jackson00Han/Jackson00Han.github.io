---
title: "COVID-19 Admission Urgency Prediction"
excerpt: "Predicting the urgency of hospital admission for COVID-19 patients from symptom onset using EDA-driven features and classic ML models : KNN, logistic regression. <br/><img src='/images/covid.png' style='max-width:400px;width:100%;height:auto;display:block;'>"
collection: portfolio
featured: false
date: 2023-10-01
permalink: /portfolio/item-4/
lang: en
ref: covid-urgency
---

This project is the **capstone project** for the course *Introduction to Data Science with Python* (Harvard/edX).  
The goal is to predict **how urgently a COVID-19 patient will need hospital admission** based on information available at the onset of symptoms.

[Repo](https://github.com/Jackson00Han/Data-Science-Project-Diary/blob/main/projects/Data_Science_edx/8.%20capstone%20project/4.%20roc/roc.ipynb)

To better understand the data, I first performed **exploratory data analysis (EDA)**.  
A few patterns stood out:

- patients aged **40–50** had the highest demand for hospital beds  
- **fever** was the most common symptom among urgent cases  

Using ROC curves as the main evaluation tool, I then built and compared two classic models:

- **k-Nearest Neighbors (KNN)**
- **Logistic Regression**

For each model, I discussed how different **decision thresholds** would be chosen under different real-world scenarios (e.g. limited hospital capacity vs. minimizing missed emergencies).

![](/images/covid.png)