![image](https://github.com/user-attachments/assets/da6a42d2-05f4-4f45-9044-4d29de957c1c)
# UFO-Shape-Prediction-Project

## Overview
This repository contains a machine learning project that predicts the shape of UFO sightings using both sighting and weather data, inspired by an investigation into extraterrestrial patterns in the United States.

## Summary of Workdone 
This project aims to classify the shape of unidentified flying objects (UFOs) reported across the United States. The dataset includes various features such as geographic location, time of sighting, and duration at the time of each report. To improve the model's predictive power, additional features like urban vs. rural, weekday/weekend classification, and historial weather data was added.

My approach framed this as a multi-class classification task, where the model must predict one of several possible shape categories. There were over 70 diffferent classes initially, then it got narrowd done to 6, then 3. Several models were tested, including logistic regression, random forest, and XGBoost, with and without label regrouping and class rebalancing strategies.

The best-performing model was a rebalanced XGBoost classifier, trained on a simplified 3-class label set. It achieved:
- Accuracy: ~42%
- F1 Score (macro avg): ~0.38, significantly outperforming other models

### Data

#### Preprocessing/Cleanup 

### Problem Formulation 

### Training 

### Performance Comparison 

### Conclusions

### Future Work 

## How to reproduce results 

### Overview of files in repository 

### Software Setup 

### Data 

### Training 

#### Performance Evaluation 

## Citations

