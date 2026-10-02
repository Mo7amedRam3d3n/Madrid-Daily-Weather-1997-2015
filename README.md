# 🌤️ Madrid Weather Dashboard (1997 - 2015)

An interactive one-page Power BI dashboard built on 19 years of daily weather observations for Madrid. The project covers the full flow: data cleaning in Power Query, data modeling, DAX measures, and dashboard design.


---

## 🎯 Project Overview

The goal was to turn a raw daily weather dataset into a clear, interactive dashboard that answers questions like:

- 🌡️ What is the average temperature, and how does it change across seasons and years?
- 🔥 When were the hottest and coldest days on record?
- 🌧️ Which months are the wettest and the driest?
- 📊 How do precipitation and temperature move together through the year?

---

## 🗂️ Dataset

- **Granularity:** one row per day
- **Period:** 1 Jan 1997 to 2015
- **Size:** about 6,800 rows after cleaning, 23 columns
- **Columns:** date (`CET` in the raw data, renamed to `Date` in Power Query), max/mean/min temperature, dew point, humidity, sea level pressure, visibility, wind speed, gust speed, precipitation, cloud cover, weather events, and wind direction

---

## 🧹 Data Cleaning (Power Query)

- Cleaned and formatted the column names (for example, removed leading spaces) and renamed the `CET` column to `Date`
- Converted the date column using the English (United States) locale, since dates come in M/D/YYYY format
- Set correct data types for all numeric columns
- Removed the few rows that were missing core readings (temperature, dew point, humidity)
- Replaced empty values in `Events` with `No Event`
- Kept nulls in `Max Gust`, `Visibility`, and `Cloud Cover` instead of filling them, to avoid inventing readings

---

## 🧩 Data Model

- `Weather` (fact table, one row per day)
- `Calendar` (date table with Year, Month, Month Name, Year-Month, Season, Day Name, and Day Number), marked as a date table
- One-to-many relationship from `Calendar[Date]` to `Weather[Date]`
- Month names are sorted by month number, and day names by day number (Mon to Sun)

---

## 🧮 DAX Measures

| Measure | Purpose |
|---|---|
| Avg Temp | Average of daily mean temperature |
| Highest Temp / Lowest Temp | Extreme temperatures in the current selection |
| Hottest Day / Coldest Day | Date of the extreme temperatures |
| Total Precipitation | Sum of precipitation (mm) |
| Wet Days | Number of days with precipitation above zero |
| Avg Humidity / Avg Wind | Averages of daily humidity and wind speed |
| Days Count | Number of days in the current selection |

---

## 📊 Dashboard Features

- 🔢 KPI cards: average temperature, humidity, wet days, precipitation, wind speed, hottest day, coldest day
- 🍂 Seasonal average temperatures (Winter, Spring, Summer, Autumn)
- 📈 Line chart of max, mean, and min temperature by year
- 🌦️ Combo chart of monthly precipitation versus temperature
- 👁️ Average visibility by season
- 🎛️ Slicers for year, season, month, and day of week
- 🔄 A reset button (bookmark) that clears all filters

---

## 💡 Key Insights

- ☀️ The overall average temperature is about **14.7 °C**, with summers near **24 °C** and winters near **6 °C**
- 🔥 The hottest day was **10 Aug 2012** and the coldest was **28 Jan 2005**
- 🌧️ Precipitation peaks in spring and autumn, with **November** the highest and **August** the lowest
- 📉 Yearly temperatures stayed fairly stable across the 19 years

---

## ⚠️ Data Quality Note

Some readings are missing in the source data, especially precipitation, visibility, and cloud cover. Precipitation totals and wet-day counts should be read as lower bounds, since many days list a weather event such as rain with a precipitation value of zero.

---

## 🛠️ Tools

- Power BI Desktop
- Power Query
- DAX
- Visualizations
