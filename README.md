# 🚕 Uber_Fares_Dataset_Analysis_PowerBI_Project-prepare-by-assoumpta

## 👤 Project By

*Name:* UWINEZA Assoumpta  
*Student ID:* 26243
*Course:* Introduction to Big Data

---

## 📘 About This Project

In this project, I worked with a real-world dataset from *Uber rides* to understand how prices change based on distance, time, and location. I used *Python* to clean and prepare the data, and then used *Power BI* to build a visual dashboard to help people see the patterns and trends in Uber fares.

---

## 📂 Dataset & Tools Used

- *Dataset Source:* [Uber Fares Dataset on Kaggle](https://www.kaggle.com/datasets/yasserh/uber-fares-dataset)
- *Data Cleaning & Processing:* Python (Pandas)
- *Visualization Tool:* Power BI Desktop
- *My Kaggle Notebook:* [View my work on Kaggle](https://www.kaggle.com/code/assoumptauwineza/assignment-by-using-kaggle/edit)

---

## 🔍 Project Steps

1️⃣ Understanding the Data
2️⃣ Data Transformation
3️⃣ Building the Dashboard

Using Power BI, I created the following visualizations:

- Fare distribution chart
- Distance vs Fare chart
- Time of day analysis
- Rides per weekday
- Monthly ride count
- Pickup map of NYC

---

## 🧽 For Cleaning Process

```python
# Check for missing values
print(df.isnull().sum())

# Drop rows with missing key values
df.dropna(subset=['pickup_datetime', 'pickup_latitude', 'pickup_longitude',
                  'dropoff_latitude', 'dropoff_longitude', 'fare_amount'], inplace=True)

# Remove rows with invalid fare amounts
df = df[(df['fare_amount'] > 0) & (df['fare_amount'] < 1000)]

# Filter latitude and longitude (NYC bounds as rough check)
df = df[(df['pickup_latitude'].between(40, 42)) & 
        (df['pickup_longitude'].between(-75, -72)) &
        (df['dropoff_latitude'].between(40, 42)) &
        (df['dropoff_longitude'].between(-75, -72))]

print("Shape after cleaning:", df.shape)
```
<img width="1143" height="643" alt="Missing values" src="https://github.com/user-attachments/assets/ae18b03f-38d7-4deb-b8a3-fa3ba946fd43" />


```python
from geopy.distance import geodesic

# Convert pickup_datetime to datetime
df['pickup_datetime'] = pd.to_datetime(df['pickup_datetime'])

# Extract temporal features
df['hour'] = df['pickup_datetime'].dt.hour
df['day'] = df['pickup_datetime'].dt.day
df['month'] = df['pickup_datetime'].dt.month
df['weekday'] = df['pickup_datetime'].dt.day_name()
df['year'] = df['pickup_datetime'].dt.year

# Peak hours (7-9 AM or 5-7 PM)
df['is_peak'] = df['hour'].apply(lambda x: 1 if 7 <= x <= 9 or 17 <= x <= 19 else 0)

# Calculate distance (in km)
def calculate_distance(row):
    pickup = (row['pickup_latitude'], row['pickup_longitude'])
    dropoff = (row['dropoff_latitude'], row['dropoff_longitude'])
    return geodesic(pickup, dropoff).km

df['distance_km'] = df.apply(calculate_distance, axis=1)

print(df[['fare_amount', 'hour', 'weekday', 'is_peak', 'distance_km']].head())

<img width="1189" height="575" alt="distance" src="https://github.com/user-attachments/assets/70b063ce-29bb-4885-8048-263d131102f8" />

---

## 📸 Dashboard & Results

### 📷 All Result Images

> Screenshots of key steps and results:

<img width="1189" height="651" alt="Screenshot of powerBI" src="https://github.com/user-attachments/assets/74b8c24e-a837-461e-abe0-8a63ce4f907d" />

---

## 🙋 Contact Me

If you have any suggestions, questions, or feedback:

Email: assoumptauwineza@gmail.com
Phone:0785389150

---

Thank you for visiting my project! 😊
