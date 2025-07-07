![image](https://github.com/user-attachments/assets/da6a42d2-05f4-4f45-9044-4d29de957c1c)
# UFO-Shape-Prediction-Project

## Overview
This repository contains a machine learning project that predicts the shape of UFO sightings using both sighting and weather data, inspired by an investigation into extraterrestrial patterns in the United States.

## Summary of Workdone 
This project aims to classify the shape of unidentified flying objects (UFOs) reported across the United States. The dataset includes various features such as geographic location, time of sighting, and duration at the time of each report. To improve the model's predictive power, additional features like urban vs. rural, weekday/weekend classification, and historial weather data was added.

My approach framed this as a multi-class classification task, where the model must predict one of several possible shape categories. There were over 70 diffferent classes initially, then it got narrowed done to 6, then 3. Several models were tested, including logistic regression, random forest, and XGBoost, with and without label regrouping and class rebalancing strategies.

The best performing model was a rebalanced XGBoost classifier, trained on a simplified 3-class label set. It achieved:

- Accuracy: 42%
- F1 Score: 0.38%
  
While another model scored a higher accuray, this model achieved the highest F1 score, which I believe is more important since there was a class imbalance. 

### Data
- Type: Tabular CSV dataset
- Inputs:
    - Original Features: sighting date, time, city, state, latitude, longitude, shape, comments, duration (hrs/min), duration (seconds), date posted
    - Weather Features: temperature, pressure, cloud cover (weather information retrieved from historical weather API)
    - Engineered Features:
        - day_type: whether the sighting occured on a weekday or weekend
        - area_type: whether the sighting occured in an urban or rural area, this was based on proximity to major cities
        - all categoical features were custom binned

  - Target: UFO shape
    - Original: 70+ unique values found in shape column
    - Simplified: 6 class categorical label
    - Further Simplified: 3 class categorical label, for improved classification performance

  - Size:~50,000 records

  - Train-Test Split: 80% training, 20% test

  
#### Preprocessing/Cleanup 
To prepare the data for modeling, several cleaning and transformation steps were performed: 
  - dropped rows with missing or invalid values
  - merged the original UFO dataset with the weather dataset, which was obtained from scraping historical weather data from an API
  - dropped unnecessary columns to reduce noise
  - feature engineering (day_type, area_type, binning)
  - target transformation 

### Problem Formulation 
This data had a prominenet class imbalance. The image below shows all the unique values found in the original UFO sightings dataset.
![Screen Shot 2025-07-06 at 7 35 21 AM](https://github.com/user-attachments/assets/0853253b-2449-4354-aee6-3fd73264747b)

This data also contained sightings from around the world. As you can see, they were mainly in the Continenetal United States.

![Screen Shot 2025-07-06 at 7 36 52 AM](https://github.com/user-attachments/assets/31058a09-d4c6-4bd5-a3b0-e1988532e31d)

After my first model performed poorly,I decided to remove all sightings that were outside of the US because I felt like that introduced noise. 

![Screen Shot 2025-07-06 at 7 38 10 AM](https://github.com/user-attachments/assets/d8462d22-cd10-499d-b580-bdab1da1e820)

The image below shows a trend that UFO sightings happened disproportionately more in the 2010's. This leads me to think that sightings are a complex cultural phenomenon. 

![Screen Shot 2025-07-06 at 7 37 30 AM](https://github.com/user-attachments/assets/208274c0-ee26-4150-b6c2-caac0d19bb36)

### Training 

### Performance Comparison 

### Conclusions

### Future Work 

## How to reproduce results 

### Overview of files in repository 

### Software Setup 

### Data 

#### Training and Performance Evaluation 
Training and evaluation is carried out in the better_accuracy.ipynb file. Just run the code. 

## Citations
Shah, Bilal Ali. “UFO Dataset: Predicting UFO Sightings in the US.” Medium, October 25, 2023. https://medium.com/@24020041/ufo-dataset-predicting-ufo-sightings-in-the-us-7539c95e75a8.


