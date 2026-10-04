# ✈️ Airline Flight Data Analysis & Fare Insights

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?logo=matplotlib&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0)
![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?logo=powerbi&logoColor=black)

End-to-end analysis of a 30,000-record airline flight dataset, from data cleaning and quality checks in Python to exploratory analysis of fares, airlines, routes, and cancellations, and an interactive Power BI dashboard.

## Table of Contents
- [Project Structure](#project-structure)
- [Objective](#objective)
- [Dataset](#dataset)
- [Workflow](#workflow)
- [Data Cleaning](#1-data-cleaning)
- [Exploratory Data Analysis](#2-exploratory-data-analysis-eda)
- [Power BI Dashboard](#3-power-bi-dashboard)
- [Key Insights](#key-insights)
- [Recommendations](#recommendations)
- [Data Quality Notes](#data-quality-notes)
- [Tools & Technologies](#tools--technologies)
- [How to Use](#how-to-use)
- [Author](#author)

## Project Structure

```
├── airline_flight.xlsx               # Raw dataset
├── Airline_Flight_Cleaning.ipynb     # Data cleaning, EDA and visualizations (Jupyter/Colab)
├── cleaned_airline_flight.csv        # Cleaned dataset (output of the notebook)
├── airline_dashboard.pbix            # Power BI interactive dashboard
└── README.md
```

| File | Link |
|---|---|
| Raw data | [airline_flight.xlsx](airline_flight.xlsx) |
| Cleaning + EDA notebook | [Airline_Flight_Cleaning.ipynb](Airline_Flight_Cleaning.ipynb) |
| Cleaned data | [cleaned_airline_flight.csv](cleaned_airline_flight.csv) |
| Power BI dashboard | [airline_dashboard.pbix](airline_dashboard.pbix) |

## Objective

Understand how ticket prices vary by airline, class, stops, and route, find the busiest routes and airlines, measure cancellations, and present the results in a dashboard that supports pricing and capacity decisions.

## Dataset

- **Size:** 30,000 raw records and 18 columns (29,259 records and 20 columns after cleaning)
- **Coverage:** 6 airlines, 10 cities, 3 travel classes, 5 aircraft types, 4 booking channels, 4 passenger types
- **Journey dates:** January to December 2026
- **Columns:** Flight_ID, Airline, Flight_Number, Source, Destination, Journey_Date, Booking_Date, Departure_Time, Arrival_Time, Duration, Total_Stops, Class, Ticket_Price, Seats_Available, Aircraft_Type, Booking_Channel, Passenger_Type, Cancellation_Status
- **Columns created:** Duration_Minutes, Total_Stops_Num
- **Source:** [ADD dataset name and link]

## Workflow

```
Raw Data → Data Quality Checks → Data Cleaning (Python) → EDA (Python) → Interactive Dashboard (Power BI)
```

## 1. Data Cleaning

- Loaded the raw dataset and checked shape, data types, missing values, duplicates, and invalid values (negative prices or seats)
- Found **6,933 missing values across 17 columns** and **298 duplicate rows** in the raw data
- Standardized text columns (trimmed spaces, fixed inconsistent case such as "economy" and "Economy")
- Converted Journey_Date and Booking_Date to datetime
- Removed rows with a missing Airline and removed duplicate records
- Filled the remaining missing values: mode for categorical columns, median for numeric columns, median date for date columns
- Created **Duration_Minutes** (from text like "7h 19m") and **Total_Stops_Num** (Non-stop = 0, 1 Stop = 1, 2 Stops = 2)
- Final validation: 29,259 records, no missing values, no duplicates

## 2. Exploratory Data Analysis (EDA)

Python analysis with pandas, Matplotlib, and Seaborn. Full code: [Airline_Flight_Cleaning.ipynb](Airline_Flight_Cleaning.ipynb)

### Airlines: who flies the most, and do fares differ by airline?

IndiGo has the most flights (29.9% of the total), but average fares are almost the same across all six airlines (₹10,776 to ₹11,233).

### Class: how much does travel class change the fare?

Business class costs about 3x Economy. Business is only 9.7% of flights but 23.4% of total ticket value.

### Fare distribution and number of stops

Most fares fall between ₹4,000 and ₹15,000, with a smaller group of high fares from Business class. Non-stop flights cost more than flights with stops.

### Routes: which routes are busiest?

Ahmedabad to Hyderabad is the busiest route (408 flights). Traffic is spread evenly across many routes.

### Cancellations and seasonality

About 7.7% of flights are cancelled, and the rate is similar across airlines. Monthly flight volume is steady through 2026.

## 3. Power BI Dashboard

Interactive dashboard with KPI cards, charts, and filters for airlines, routes, classes, and fares. File: [airline_dashboard.pbix](airline_dashboard.pbix) (open in Power BI Desktop)

## Key Insights

- 🎫 **Overall:** 29,259 flights with a total ticket value of ₹32.2 Cr. The average ticket price is ₹11,004 and the median is ₹10,020.
- 🛫 **IndiGo leads in volume** with 8,759 flights (29.9%), followed by Air India (6,418) and Vistara (4,823). Go First has the fewest (2,215).
- 💺 **Class drives price, not airline.** Average fare is ₹26,586 for Business, ₹14,771 for Premium Economy, and ₹8,950 for Economy, while airline averages differ by only ~4% (₹10,776 to ₹11,233).
- 💰 **Business class punches above its weight:** 9.7% of flights bring 23.4% of ticket value. Economy is 84.3% of flights and 68.6% of ticket value.
- 🔁 **Stops:** Non-stop flights average ₹11,509, compared with ₹10,439 for 1 stop and ₹10,036 for 2 stops. The same pattern holds inside Economy (₹9,475, ₹8,385, ₹7,816), so it is not only a class effect.
- ⏱️ **Fares do not change with flight duration or booking lead time** (correlation close to zero), which is unusual for real airline pricing.
- 🗺️ **Routes:** Ahmedabad → Hyderabad is the busiest route (408 flights). Ahmedabad is the top source city (3,326 flights) and Hyderabad is the top destination (3,286).
- ❌ **Cancellations:** 2,253 flights (7.7%) were cancelled. Airline rates range from 7.0% (SpiceJet) to 8.0% (IndiGo). Online Travel Portal bookings (8.2%) and Leisure and Student passengers (about 8.2%) cancel slightly more than others.
- 📅 **Seasonality:** Monthly flights range from 2,259 (February) to 2,771 (July), and average fare stays between ₹10.9K and ₹11.2K every month.

## Recommendations

- **Grow premium cabins:** Business class gives 23.4% of ticket value from 9.7% of flights, so upgrade offers from Economy and Premium Economy can lift revenue without adding flights.
- **Test time-based pricing:** Fares in this data do not rise for last-minute bookings, so a pricing test with higher late-booking fares and early-bird discounts is a clear opportunity.
- **Reduce cancellations where they are highest:** Online Travel Portal bookings and Leisure and Student passengers cancel slightly more, so reminders or flexible-fare options could target these groups.
- **Add capacity on busy routes:** Ahmedabad → Hyderabad and other routes with 360+ flights are candidates for more frequency.

## Data Quality Notes

Checks run on the cleaned data that are worth knowing before using it:

- 224 records have a Booking_Date after the Journey_Date (booking lead time is negative)
- 74 records have the same Source and Destination city
- 290 records have an "Unknown" Flight_Number
- Ticket prices show almost no relationship with duration or booking lead time, which suggests the dataset may be simulated

## Tools & Technologies

| Layer | Tools | Where it is used in this repo |
|---|---|---|
| Data Cleaning | Python, pandas, NumPy | [Airline_Flight_Cleaning.ipynb](Airline_Flight_Cleaning.ipynb) |
| EDA & Visualization | Matplotlib, Seaborn, Google Colab | [Airline_Flight_Cleaning.ipynb](Airline_Flight_Cleaning.ipynb) |
| Dashboard | Power BI Desktop (KPI cards, charts, filters) | [airline_dashboard.pbix](airline_dashboard.pbix) |

## How to Use

1. Clone the repo
   ```bash
   git clone https://github.com/sravanipulugujju/[ADD-REPO-NAME].git
   cd [ADD-REPO-NAME]
   ```
2. Upload `airline_flight.xlsx` to Google Colab (the notebook reads it from `/content/`)
3. Run `Airline_Flight_Cleaning.ipynb` to clean the data, run the EDA, and save `cleaned_airline_flight.csv`
4. Open `airline_dashboard.pbix` in Power BI Desktop to explore the interactive dashboard

## Author

**Pulugujju Sravani** | Data Analyst (Fresher) | MCA 2026

- LinkedIn: [linkedin.com/in/sravani-pulugujju-b08b523a4](https://www.linkedin.com/in/sravani-pulugujju-b08b523a4)
- GitHub: [github.com/sravanipulugujju](https://github.com/sravanipulugujju)
- Email: sravanipulugujju26@gmail.com

Feedback and suggestions are welcome. Feel free to fork, explore, and reach out!
