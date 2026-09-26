# ✈️ Airline Flight Data Analysis & Fare Insights

A complete end-to-end data analytics project that cleans, explores, and visualizes airline flight booking data to uncover fare trends, route popularity, and booking behavior — using **Python (Pandas, NumPy, Matplotlib, Seaborn)** for cleaning/EDA and **Power BI** for interactive dashboarding.

---

## 📌 Project Overview

| | |
|---|---|
| **Project Name** | Airline Flight Data Analysis & Fare Insights |
| **Domain** | Aviation / Travel Analytics |
| **Type** | Data Cleaning → Exploratory Data Analysis → Visualization → BI Dashboard |
| **Tools Used** | Python (Pandas, NumPy, Matplotlib, Seaborn), Jupyter Notebook, Microsoft Excel, Power BI |
| **Dataset Size** | 29,259 rows × 20 columns (post-cleaning) |
| **Status** | ✅ Completed |

This project analyzes airline booking records to answer key business questions such as:
- Which airlines are the most frequently booked, and how do their average fares compare?
- How does ticket price vary by travel class, number of stops, and flight duration?
- Which source–destination routes are the busiest?
- What booking channels and passenger types dominate the data?

---

## 🗂️ Repository Structure

```
airline-flight-analysis/
│
├── data/
│   ├── airline_flight.xlsx              # Raw, uncleaned dataset
│   └── cleaned_airline_flight.csv       # Final cleaned dataset (output of notebook)
│
├── notebooks/
│   └── Airline_Flight_Cleaning.ipynb    # Data cleaning + EDA + visualizations
│
├── dashboard/
│   └── airline_dashboard.pbix           # Power BI interactive dashboard
│
└── README.md                            # Project documentation (this file)
```

> 💡 When pushing to GitHub, place the four uploaded files into the folders above (`data/`, `notebooks/`, `dashboard/`) to keep the repo organized.

---

## 📊 Dataset Description

The raw dataset (`airline_flight.xlsx`) contains flight booking records with the following fields:

| Column | Description |
|---|---|
| `Flight_ID` | Unique identifier for each booking |
| `Airline` | Airline operating the flight (6 unique: AirAsia India, IndiGo, SpiceJet, Go First, Vistara, Air India) |
| `Flight_Number` | Flight number/code |
| `Source` / `Destination` | Departure and arrival cities (10 cities each) |
| `Journey_Date` / `Booking_Date` | Date of travel and date of booking |
| `Departure_Time` / `Arrival_Time` | Scheduled flight times |
| `Duration` | Flight duration (raw text, e.g. `7h 19m`) |
| `Total_Stops` | Number of stops (Non-stop, 1 Stop, 2 Stops) |
| `Class` | Travel class (Economy, Premium Economy, Business) |
| `Ticket_Price` | Fare of the ticket (₹1,300 – ₹34,180) |
| `Seats_Available` | Number of seats available at booking time |
| `Aircraft_Type` | Aircraft model (Boeing 737/787, Airbus A320/A321/A350) |
| `Booking_Channel` | Website, Mobile App, Travel Agent, Online Travel Portal |
| `Passenger_Type` | Business, Leisure, Student, Family |
| `Cancellation_Status` | Completed / Cancelled |

**Engineered columns (added during cleaning):**
| Column | Description |
|---|---|
| `Duration_Minutes` | `Duration` converted from `"Xh Ym"` text format to total minutes |
| `Total_Stops_Num` | `Total_Stops` mapped to numeric form (0, 1, 2) for analysis |

---

## 🧹 Data Cleaning & Analysis Workflow (`Airline_Flight_Cleaning.ipynb`)

The notebook is organized into 10 clearly commented sections, executed sequentially:

### 1. Import Libraries
Load `pandas`, `numpy`, `matplotlib.pyplot`, and `seaborn`.

### 2. Load Dataset
Read the raw `airline_flight.xlsx` file into a DataFrame using `pd.read_excel()`.

### 3. Initial Data Understanding
Inspect the dataset's shape, column names, data types (`.info()`), and summary statistics (`.describe(include="all")`) to understand its structure before cleaning.

### 4. Data Quality Checks
- Count missing values per column and in total
- Check for duplicate rows
- Count unique values per column (`.nunique()`)
- Flag invalid records (e.g., negative `Ticket_Price` or `Seats_Available`)

### 5. Create Working Copy
Duplicate the raw DataFrame into `cleaned_airline_flight` so the original data stays untouched for auditability.

### 6. Data Cleaning
| Step | Action |
|---|---|
| 6.1 Remove Duplicates | Drop exact duplicate rows |
| 6.2 Check Column Names | Verify column naming consistency |
| 6.3 Standardize Text Columns | Strip whitespace and title-case fields like `Airline`, `Source`, `Destination`, `Class`, `Aircraft_Type`, `Booking_Channel`, `Passenger_Type`, `Cancellation_Status` |
| 6.4 Convert Date Columns | Parse `Journey_Date` and `Booking_Date` into proper `datetime` format using `pd.to_datetime()` with `errors="coerce"` |
| 6.5 Check Data Types | Validate dtypes after conversion |
| 6.6 Handle Missing Values | Fill categorical columns with **mode**, numeric columns (`Ticket_Price`, `Seats_Available`) with **median**, and date columns with **median date** |
| 6.7 Convert Duration to Minutes | Custom function parses `"7h 19m"` style strings into a single numeric `Duration_Minutes` column |
| 6.8 Convert Stops to Numeric | Map `Total_Stops` text values (`Non-stop`, `1 Stop`, `2 Stops`) to numeric `Total_Stops_Num` |
| 6.9 Final Cleaning Validation | Re-check shape, missing values, and duplicates to confirm the dataset is clean |

### 7. Save Cleaned Dataset
Export the cleaned DataFrame to `cleaned_airline_flight.csv` for downstream use in Power BI and further analysis.

### 8. Exploratory Data Analysis (EDA)
- **8.1 Airline Analysis** — flight counts and average fare per airline
- **8.2 Source & Destination Analysis** — busiest departure/arrival cities
- **8.3 Class Analysis** — distribution and average fare per travel class
- **8.4 Stops Analysis** — flight counts and fare trends by number of stops
- **8.5 Top 10 Routes** — most frequently booked source–destination pairs

### 9. Python Visualizations
| Chart | Insight |
|---|---|
| Bar chart — Flights by Airline | Booking volume per airline |
| Histogram — Fare Distribution | Overall spread of ticket prices |
| Pie chart — Class Distribution | Share of Economy vs Premium Economy vs Business |
| Box plot — Price by Stops | How fares vary with number of stops |
| Scatter plot — Price vs Duration | Relationship between flight duration and fare |
| Heatmap — Correlation Matrix | Correlation between numeric features |

### 10. Final Python Validation
A final sanity check confirming the cleaned dataset's shape, zero missing values, and zero duplicates before handoff to Power BI.

---

## 📈 Power BI Dashboard (`airline_dashboard.pbix`)

The cleaned dataset (`cleaned_airline_flight.csv`) feeds an interactive Power BI dashboard featuring:
- Airline-wise booking and revenue comparisons
- Route-level (Source → Destination) performance
- Fare trends by class, stops, and booking channel
- Filters/slicers for airline, class, passenger type, and cancellation status

> Open `airline_dashboard.pbix` in **Power BI Desktop** to explore the dashboard interactively.

---

## ⚙️ How to Run This Project

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn jupyter openpyxl
```

### Steps
1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/airline-flight-analysis.git
   cd airline-flight-analysis
   ```
2. **Place the raw data** — ensure `airline_flight.xlsx` is in the `data/` folder (update the file path in the notebook's Section 2 if needed, e.g. `data/airline_flight.xlsx` instead of `/content/...`).
3. **Run the notebook**
   ```bash
   jupyter notebook notebooks/Airline_Flight_Cleaning.ipynb
   ```
   Run all cells sequentially — this regenerates `cleaned_airline_flight.csv`.
4. **Open the dashboard** — launch `dashboard/airline_dashboard.pbix` in Power BI Desktop (refresh the data source to point to the newly generated CSV if the path changed).

---

## 🔑 Key Insights

- The dataset covers **6 airlines**, **10 source cities**, **10 destination cities**, and flights throughout **2026**.
- Ticket prices range from **₹1,300 to ₹34,180**, with clear fare premiums for Business class and non-stop flights.
- The cleaned dataset has **zero missing values and zero duplicate rows**, making it analysis-ready.
- Flight duration and number of stops both show a visible relationship with ticket price, explored via the box plot, scatter plot, and correlation heatmap.

---

⭐ If you find this project useful, consider giving the repository a star!
