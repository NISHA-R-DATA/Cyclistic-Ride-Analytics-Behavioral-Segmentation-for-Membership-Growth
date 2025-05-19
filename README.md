![title_image](https://github.com/user-attachments/assets/e63e5938-58da-4ea7-b322-c65066ac807c)


## 📘 Project Overview 
This project presents a **comprehensive analysis** of Cyclistic’s **2023 bike-share dataset**, which includes over **5.7 million ride records**. Utilizing **Python** as the primary tool—leveraging **Pandas** for efficient **data preprocessing** and **Matplotlib** and **Seaborn** for clear, impactful **visualizations**—the analysis uncovers **actionable insights** grounded in data.

The focus of the analysis is to explore differences in **ride patterns** between **casual users** and **annual members**. Key trends related to **ride behavior**, **trip duration**, and **station popularity** were identified, revealing distinct **user preferences** that can guide **business strategy**.

Based on these findings, **targeted recommendations** were developed to encourage the **conversion of casual riders into annual subscribers**. The approach emphasizes clear communication of **data-driven insights**, ensuring the results are accessible and relevant to both **technical teams** and **business stakeholders**.

---

## 📑 Table of Contents
1. [Business_Problem](https://github.com/NISHA-R-DATA/Cyclistic-Ride-Analytics-Behavioral-Segmentation-for-Membership-Growth?tab=readme-ov-file#-business-problem)
2. [Data_Source_Overview]
3. [Tools_&_Libraries]
4. [Methodology]
5. [Key_Insights]
6. [Strategic Recommendations]
7. [Conclusion]

---

## ❓ Business Problem
**Cyclistic** aims to **expand** its **annual membership base** by uncovering **actionable insights** into the **behaviors** and **usage patterns** of **casual riders**. By analyzing **detailed trip data**, the company seeks to develop **data-driven marketing strategies** that effectively **target** and **convert** casual users into **loyal**, **long-term members**.

---

## 📁 Dataset Overview
This project leverages publicly available trip data from **Cyclistic**, a Chicago-based bike-share service operated through the Divvy system. The dataset spans the **entire 2023 calendar year**, offering a comprehensive foundation for analyzing ridership patterns and user behavior across seasons and bike types.

### Core Columns
- **ride_id**: Unique identifier for each trip.
- **rideable_type**: Type of bike used (classic bike, electric bike, and docked bike).
- **started_at / ended_at**: Timestamps marking trip start and end.
- **start_station_name / end_station_name**: Station names where trips began and ended.
- **start_station_id / end_station_id**: Station identifiers.
- **start_station_lat / start_station_long and end_station_lat / end_station_long**: Geolocation coordinates of start and end stations.
- **member_casual**: User type classification (annual member or casual rider).

---

## 🛠️ Tools & Libraries
- **Language**: Python
- **Libraries**:
  - **pandas, datetime** – Data wrangling and feature engineering
  - **matplotlib, seaborn, plotly** – Data visualization
  - **glob, os** – File management
  - **CategoricalDtype** – Plot ordering

---

## Methodology:
This section outlines the **end-to-end process** followed to acquire, clean, transform, and analyze Divvy bike-share trip data for the year 2023.

### 📥 1. Data Acquisition
- Downloaded 12 months of trip data (2023) from the public Amazon S3 bucket `divvy-tripdata`.

### 🧹 2. Data Integration and Preprocessing
- **Loaded and Combined Data**
  - Used Python (pandas) to read and concatenate all monthly files into a single DataFrame (~5.7 million rows).
- **Initial Data Checks**
  - Verified schema consistency, assessed null values, and inspected data types.
- **Handled Missing Values**
  - Identified missing values in `start_station_name` and `end_station_name`.
  - Created a mapping reference dataset linking station IDs with their respective latitude, longitude, and names.
  - Used geolocation coordinates to impute missing station names.
  - Flagged records with missing `end_station_lat` and `end_station_lng` as "Unknown" to preserve data integrity.
- **Converted Data Types**
  - Converted `started_at` and `ended_at` to datetime objects to support time-based analysis.

### 🧽 3. Data Cleaning
- **Dropped Incomplete Rows**
  - Removed records with null values in essential columns (`started_at`, `ended_at`, and `member_casual`).
- **Filtered Invalid Rides**
  - Calculated ride duration (`ride_length`) in minutes.
  - Removed rides with zero or negative durations (~88,950 rows) to ensure analytical accuracy.

### ⚙️ 4. Feature Engineering
Derived new features from the `started_at` timestamp to enable detailed temporal analysis:
- **day_of_week** – Day name (e.g., Monday, Tuesday)
- **day_type** – Weekday or Weekend
- **month_name** – Month name
- **hour_of_day** – Hour (0–23)
- **hour_label** – 12-hour formatted string (e.g., 1 AM, 2 PM)
  - Applied categorical ordering to `hour_label` for accurate chronological plotting.

### 📊 5. Exploratory Data Analysis (EDA)
Used matplotlib, seaborn, and plotly to uncover user behavior patterns:
- **Ride Frequency & Temporal Trends**:
  - Analyzed monthly ride volumes by user type.
  - Identified peak usage hours and weekday/weekend trends for each segment.
- **Ride Duration Analysis**:
  - Compared average ride lengths by user type across days, months, and hours.
- **Station Usage Patterns**:
  - Identified top start and end stations for casual vs. member users.
- **Bike Type Preferences**:
  - Examined usage distribution of classic vs. electric bikes across user segments.

---

## 🔍 Key Insights

### 1. Total Ride Count by User Type



![Total_Ride_Count](https://github.com/user-attachments/assets/5a9a6dff-c312-4e75-b963-1fe4e54958a3)



- **Annual members** constitute **64%** of rides; **casual riders** contribute **36%**.
- Casual users represent a **significant portion**, indicating a **large conversion opportunity**.
- Removal of **1.5% invalid/zero-duration rides (88,950 rides)** suggests **data quality issues** or **anomalous behavior**.



### 2. Monthly Ride Trends by User Type

![Monthly_Ride_Patterns](https://github.com/user-attachments/assets/8cd3bd83-e789-4b2e-bdd4-9272a54656c2)




- **Strong seasonality**:
  - **Summer surge (May–August)**: Casual rides jump **5.3×** (from **61K in March** to **326K in July**).
  - Members show **steady increases**, peaking at **454K rides in August**.
  - **Winter decline (Nov–Feb)**: Significant drop, especially for casuals (**<52K rides**), highlighting **weather sensitivity** and **low winter engagement** among casual riders.
- Members maintain **high usage** (**>140K monthly rides**) **year-round**, indicating **habitual** and **retained users**.

### 3. Rides by Day of Week by User Type

![Ride_User_Type](https://github.com/user-attachments/assets/0c8181d7-28ee-4461-9ced-a8df4dced5bb)



- Members **peak midweek (Tue–Thu)**, averaging **575K rides/day**, consistent with **commuting patterns**. Weekend usage dips, **lowest on Sundays**.
- Casual riders **peak weekends**, especially **Saturday (405K)** and **Sunday (331K)**, pointing to **leisure** and **recreational use**.

### 4. Ride Volume by Hour (Weekday vs Weekend)

![weekday_ride_volume](https://github.com/user-attachments/assets/54d65934-053e-4435-a29c-9b2eab885242)


![weekend_ride_volume](https://github.com/user-attachments/assets/128a81f3-46ce-425b-82e1-3da38fc217d7)



- **Weekdays**:
  - Members show **commute peaks** at **8 AM** and **5 PM**.
  - Casual riders **peak later (~5 PM)** with **lower morning volume**.
  - Members ride **3–4× more** than casuals during **morning commute hours (6 AM–10 AM)**.
  - **Late-night (12 AM–4 AM)** rides are **low overall**, but **casuals slightly dominate**, possibly **social rides**.
- **Weekends**:
  - Ride volumes **flatten**.
  - Casuals **surpass members** between **12 PM–4 PM**, peaking at **3 PM**, confirming **recreational usage**.
  - Casuals also show more **late-night activity** on weekends.

### 5. Average Ride Duration by User Type

![Avg_Ride](https://github.com/user-attachments/assets/75a3708b-23f3-48d7-8f09-91b7ee126970)



- Casual riders average **28.7 minutes**, **over twice** that of members (**12.7 minutes**).
- Indicates **casuals prioritize leisure and exploration**, while **members focus on short, purpose-driven trips** (commutes, errands).

### 6. Average Ride Duration by Day of Week


![Avg_Ride_Week](https://github.com/user-attachments/assets/2ed793c9-1f72-4a0d-b062-de562111b7d0)



- Casual durations **rise on weekends**, peaking at **33.4 minutes on sundays**.
- Members maintain **consistent durations (~12–14 minutes)** throughout the week, with **slight weekend increases**, suggesting **occasional leisure use** but **overall routine trips**.

### 7. Average Ride Duration by Hour — Weekday vs Weekend


![weekday_avg](https://github.com/user-attachments/assets/2133ea5c-1780-45f0-84e7-4978bfd17fda)



![weekend_Avg](https://github.com/user-attachments/assets/28698c48-3fca-4c4b-9826-26dec4cd2c8d)



- **Weekdays**:
  - Casual riders have **longer rides throughout**, peaking at **36.6 minutes around 3 AM**.
  - Duration **dips during commute hours**, indicating some **short casual trips**.
  - Members’ durations remain **stable**, with a **slight evening increase**.
- **Weekends**:
  - Both groups **ride longer**.
  - Casuals average **32–35+ minutes**, peaking at **5 PM (35.2 min)** and showing a **48.7-minute spike at 4 AM** (possible **outliers** or **leisure riders**).
  - Members **peak around 13–15 minutes**.

### 8. Average Ride Duration by Month


![Month_Avg](https://github.com/user-attachments/assets/cf1c160a-4512-4650-842b-27fc2d66c39b)



- Casual durations **peak in summer** (**August: 35.7 minutes**) and remain **consistently longer** than members.
- Members’ durations show **modest summer increase** (**~14 minutes in August**).
- Both groups’ durations **drop in winter**, with **casuals still averaging 20+ minutes**, indicating **winter leisure rides**.
- **Transition months (April, October)** show duration changes **aligned with weather**.

### 9. Station Usage and Spatial Patterns


![topstations](https://github.com/user-attachments/assets/934a0138-cf43-408b-9b92-ff355ce96d9d)


![end_stations](https://github.com/user-attachments/assets/7bf48d9e-10c7-4e46-998c-047e09f0b843)



- **Shared key hubs**: Aberdeen St & Monroe, Albany Ave & Belmont, Ashland Ave & Belle Plaine, etc.
- Casual users **cluster around tourist landmarks** and **scenic spots** (Millennium Park, lakefront), indicating **recreational use**.
- Members **cluster near residential and workplace transit hubs** (e.g., 900 W Harrison St, Clinton St & Washington Blvd), supporting **commuting patterns**.
- **Spatial distribution** confirms **members inland daily corridors** vs **casuals waterfront/tourist areas**.

### 10. Bike Type Usage Patterns


![bike type usage](https://github.com/user-attachments/assets/4336000c-7bdc-466a-92c8-71f3d17a1cf2)



- Members use **electric and classic bikes almost equally (~1.8 million rides each)**, showing **versatile habitual usage**.
- Casual users **favor electric bikes** (**1.08 million rides**) over classic (**870K**), highlighting **preference for assisted riding**.
- **Docked bikes** used **exclusively by casual riders** (**77K rides**), implying docked systems serve **tourists** or **occasional users**.
- Member usage indicates **routine**, **frequent riding** with **flexible bike preferences**; casual users **lean towards convenience**.

## Summary
- **Distinct behavioral, temporal, and spatial differences** between members and casual riders inform **targeted marketing, fleet management,** and **user engagement strategies**.
- Members are **habitual riders** focused on **commuting and errands**, with **stable usage year-round**.
- Casual riders are **recreational users, weather-sensitive, peaking on weekends and summer**, with **longer rides** and **preference for electric and docked bikes**.
- **Significant potential** to **convert casual riders into members** by emphasizing **value propositions** addressing **seasonal and leisure usage**.
- **Key station hubs** and **bike preferences** provide **actionable insights** for **infrastructure planning** and **promotions**.

---
## 🎯 Strategic Recommendations
Based on the insights obtained, the following marketing strategies are recommended to convert casual riders into annual members:

1. **Seasonal Membership Promotions**:Launch limited-time summer membership discounts to capitalize on peak ridership from May through September.
2. **Weekend-Focused Campaigns**: Design campaigns emphasizing cost-effective, unlimited weekend rides to attract leisure riders.
3. **Geo-Targeted Advertising**: Deploy advertisements near popular casual rider hubs such as Millennium Park, Navy Pier, and Lakefront Trail to promote membership benefits.
4. **In-App Cost Comparison Alerts**: Implement real-time ride tracking that shows casual users how much they could save by switching to an annual plan during longer rides.
5. **Trial Membership Offers**: Introduce 30-day trial memberships or "membership lite" options to lower commitment barriers.
6. **Personalized Messaging Based on Ride Behavior**: Use app and email notifications triggered by frequent or long-duration casual rides to promote tailored membership offers.
7. **Electric Bike Perk Promotions**: Highlight the lower per-minute cost and extended access to e-bikes available exclusively to members to convert electric bike users.
8. **Member Perks Awareness Campaigns**: Use clear visuals—such as infographics and reels—to educate riders on membership perks like unlimited 45-minute rides, priority docking, and advanced app features.
9. **Local Partnership Bundles**: Partner with hotels, events, and attractions to offer bundled deals, such as “Stay & Ride” or “Tourist Membership Pass.”
10. **Gamified Incentives for Casual Users**: Reward frequent riders with perks like “ride X times, earn a free month” to encourage commitment.

---

## 🏁 Conclusion:
This project provided an **in-depth analysis** of **Cyclistic’s 2023 bike-share data**, revealing clear **behavioral differences** between **casual riders** and **annual members**. **Casual users** primarily ride for **leisure**, with **longer trips** and **seasonal peaks**, while **members** show consistent, **commute-focused patterns** year-round. These insights highlight key opportunities for **targeted marketing** to convert casual riders into **loyal members**. By leveraging **seasonal promotions**, **geo-targeted campaigns**, **personalized messaging**, and **member perks**, Cyclistic can effectively **increase membership** and **optimize rider engagement**. The analysis underscores the value of **data-driven strategies** in enhancing **user retention** and driving **business growth**.

---

