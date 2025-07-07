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
The primary evaluation metric for this multi-class classification task is the F1-score, along with accuracy, precision, and recall. Given the class imbalance in the dataset, the macro-averaged F1-score is the most reliable indicator of performance.

![Unknown](https://github.com/user-attachments/assets/21232bae-f8e1-4589-af37-ff694cbc7358)

![Screen Shot 2025-07-06 at 5 18 28 PM](https://github.com/user-attachments/assets/3ba6e8c1-9388-45bf-b596-4ef1c1735dfb)

### Conclusions
Grouped shape categories significantly improved model performance.
When I grouped the original 6 shape labels into 3 broader categories (light, structured, and weird), classification performance improved across all models, especially in precision and recall. Using compute_sample_weight to address class imbalance led to higher F1-scores for the structured and weird categories, which were previously underperforming due to fewer examples. Among all models tested, the XGBoost classifier on grouped and rebalanced data achieved the best macro F1-score (0.38), making it the most effective model for this classification task. Binning weather features, encoding location zones, and distinguishing between urban/rural areas all contributed to more meaningful inputs for the models.

While the results may not be groundbreaking, I’m genuinely proud of the progress made throughout this project. I was able to explore the dataset in depth, apply thoughtful preprocessing techniques, and improve performance through feature engineering and label grouping. That said, I’ve come to believe this problem may not be one that model tuning alone can solve. The nature of UFO sightings is inherently subjective, noisy, and complex, making it difficult to extract clear, predictive patterns. Still, this project was a valuable exercise in understanding how data characteristics can limit model performance, and I’m glad I had the opportunity to work through it.


### Future Work 
I have several ideas for continued work. One next step would be to collect more reliable structured data, such as census information, air traffic records, or environmental data, which could provide stronger context for each sighting. Another idea is to reevaluate how I chose bin my cateogorical labels and classes. 


## How to reproduce results 
- Download and place the original datasets into the appropriate data/ folder. This includes: scrubbed.csv, weather_final_full.csv
- Open and run the notebook initial_cleaning.ipynb to clean and prepare the dataset.
- Next, open and run the bettering_accuracy.ipynb notebook. This will encode features, train multiple models, apply label grouping, and report evaluation metrics.


### Overview of files in repository 

### Software Setup 
| Package           | Version (or Latest) |
|-------------------|---------------------|
| `pandas`          | >= 1.5              |
| `numpy`           | >= 1.22             |
| `matplotlib`      | >= 3.5              |
| `seaborn`         | >= 0.11             |
| `scikit-learn`    | >= 1.1              |
| `xgboost`         | >= 1.7              |
| `geopy`           | >= 2.3              |
| `plotly`          | >= 5.14             |
| `jupyter`         | (for running notebooks) |

---


### Data Download
To download the scrubbed.csv, you can simply download the zip file from Kaggle. 
https://www.kaggle.com/datasets/NUFORC/ufo-sightings


#### Training and Performance Evaluation 
Training and evaluation is carried out in the better_accuracy.ipynb file. Just run the code. 


## Citations
Shah, Bilal Ali. “UFO Dataset: Predicting UFO Sightings in the US.” Medium, October 25, 2023. https://medium.com/@24020041/ufo-dataset-predicting-ufo-sightings-in-the-us-7539c95e75a8.


