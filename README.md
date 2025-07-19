🌧️ Rainfall Prediction Classifier
I built and evaluate a Machine Learning model to predict rainfall in Melbourne area Australian based on hisorical weather data.

📌 Project Overview
Dataset: [Weather Dataset](https://www.kaggle.com/datasets/jsphyg/weather-dataset-rattle-package/) (from Kaggle).\
Column definitions are from the [Australian Bureau of Meteorology](http://www.bom.gov.au/climate/dwo/IDCJDW0000.shtml).


We focused on localized weather data for Melbourne, MelbourneAirport, and Watsonia (within ~20 km of each other).

Summary of what i did\
Data Source and Preparation\
The dataset covers daily weather observations from 2008 to 2017.

Dropped rows with missing values, leaving 56,420 records.

Renamed column "**RainTomorrow**" to "**RainToday"** and "**RainToday**" to "**RainYesterday**" to model today’s rainfall using yesterday’s and other metrics.

Filtered the dataset to Melbourne, Melbourne Airport, and Watsonia (within 20 km) to make a localized model.

Added a Season feature by mapping each date to Summer, Autumn, Winter, or Spring.

Target Balance\
RainToday counts:

No: 5,766

Yes: 1,791
- It rains about 24% of days in the dataset.
- A naïve guess of “No rain” would already be right 76% of the time.

Modeling Workflow\
Feature Engineering: Numeric features scaled; categorical features one‑hot encoded using a ColumnTransformer.

Train/Test Split: 80/20, with stratification to preserve class balance.

Models Trained:
- Random Forest Classifier (with GridSearchCV)
- Logistic Regression (as comparison)

Hyperparameter Tuning: 5‑fold Stratified CV on a parameter grid for each model.

Results\
Model	Test Accuracy	Notes\
Random Forest	84%	Best performance overall.
Logistic Regression	83%	Less biased to imbalance, but slightly lower accuracy.

Random Forest Classification Report\
<img width="690" height="166" alt="Screenshot 2025-07-19 at 4 59 42 AM" src="https://github.com/user-attachments/assets/c91c775f-a2b5-46cf-a614-8910e2d7be88" />

Confusion Matrix (Random Forest):\
<img width="624" height="459" alt="Screenshot 2025-07-19 at 5 00 03 AM" src="https://github.com/user-attachments/assets/2252b50e-63c1-4b78-a9ba-24c0ad123cea" />

Feature Importance\
<img width="690" height="374" alt="Screenshot 2025-07-19 at 5 00 41 AM" src="https://github.com/user-attachments/assets/c63d8b4b-bf8c-47c6-bcab-0bb2e6aae87e" />

In the future importance chart, the humidity3pm is a great feature that strongly determines if it is going to rain.

Logistic Regression Classification Report\
<img width="602" height="150" alt="Screenshot 2025-07-19 at 5 01 04 AM" src="https://github.com/user-attachments/assets/d042ff01-54ca-484f-9c5a-ea213c970185" />

Confusion Matrix (Logistic Regression):\
<img width="650" height="484" alt="Screenshot 2025-07-19 at 5 01 24 AM" src="https://github.com/user-attachments/assets/2f7c7a47-8bc3-443d-96ba-dd1913dd229b" />

Key Takeaways\
Random Forest performed slightly better overall (84% vs 83%).

Logistic Regression handled imbalance more evenly but had lower recall for rainy days.

Humidity3pm emerged as the most important feature in the Random Forest model.
