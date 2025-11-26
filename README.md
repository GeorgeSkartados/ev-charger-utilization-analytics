# EV Charger Utilization Analytics

## 1. Project Overview

This micro-project analyzes a simulated network of EV charging stations to understand how drivers use charging infrastructure across different locations. The goal is to identify utilization patterns, peak charging hours, customer behavior, and revenue performance using a realistic dataset generated in Python and stored in SQLite.

The project demonstrates end-to-end analytical thinking with:

- **SQL** for data exploration  
- **Python** (pandas + matplotlib) for analysis and visualization  
- **SQLite** for relational data storage  
- **Jupyter Notebook** for a reproducible workflow  

The dataset includes:

- 5 EV charging stations  
- 6 vehicle models  
- 8 customers  
- 223 charging sessions over a 30-day period  

---

## 2. Data Model

The project uses a simple but realistic schema for an EV charging network.

### **stations**
- `station_id` (PK)  
- `name`  
- `city`  
- `max_kw` (maximum charger power)  
- `price_per_kwh`  

### **vehicles**
- `vehicle_id` (PK)  
- `brand`  
- `model`  
- `battery_capacity` (kWh)  
- `year`  

### **customers**
- `customer_id` (PK)  
- `name`  
- `email`  
- `city`  
- `loyalty_member` (0/1)  

### **charging_sessions**
- `session_id` (PK)  
- `station_id` (FK → stations)  
- `vehicle_id` (FK → vehicles)  
- `customer_id` (FK → customers)  
- `start_time`  
- `end_time`  
- `kwh_used`  
- `cost`  
- `payment_status` (`paid`, `failed`, `refunded`)  

All tables and sample data are created directly inside the notebook using Python’s `sqlite3` library.

---

## 3. Business Questions

This analysis focuses on five questions that EV charging operators care about:

1. **Station Utilization**  
   Which stations have the lowest total charging hours?

2. **Demand Patterns**  
   What are the peak charging hours across the network?

3. **Price Elasticity**  
   Do higher charging prices (€/kWh) reduce session duration?

4. **Customer Behavior**  
   Which stations have the most repeat customers?

5. **Financial Performance**  
   What is the average revenue per station per day?

---

## 4. Tech Stack

- **Language:** Python  
- **Database:** SQLite (`sqlite3`)  
- **Libraries:** pandas, matplotlib  
- **Environment:** Jupyter Notebook + conda (Miniconda / Anaconda)  
- **Version Control:** Git + GitHub  

---

## 5. How to Run the Project

### 5.1 Create and activate a conda environment (recommended)


conda create -n microproj python=3.11 -y
conda activate microproj

### 5.2 Install dependencies

conda install jupyter pandas matplotlib -y

### 5.3 Launch Jupyter Notebook

jupyter notebook
ev_charger_analytics.ipynb

### 5.4 Run all cells from top to bottom

The notebook will:

- create the SQLite database (ev_charger_analytics.db)

- build all tables

- generate synthetic charging session data for 30 days

- run all SQL analytical queries

- generate visualizations

- display insights for each business question

## 6. Key Findings
### 6.1 Station Utilization

- Central Plaza Station had the lowest utilization (~36.7 total charging hours).

- Highway Fast Charge 01 was the strongest performer (~62.5 hours).

- Location strongly influences utilization (mall/highway > inner city).

### 6.2 Peak Charging Hours

- Demand peaked at 10–11 AM and 22:00.

- This reflects:

   - daytime commuter charging

   - late-night top-ups

### 6.3 Price vs Session Duration

- Prices ranged from €0.30 to €0.42 per kWh.

- Session duration stayed between ~60–75 minutes regardless of price.

- Scatter plot confirmed no meaningful correlation.

- Drivers charge based on need, not minor price differences.

### 6.4 Customer Repeat Behavior

- Small synthetic dataset (8 customers, 224 sessions) resulted in high repeat rates.

- The method shows how to calculate unique vs repeat users.

- In real data, commuter-heavy stations would likely show higher repeat traffic.

### 6.5 Revenue Performance

- Seaside Mall Chargers: ~€484/month (~€16.13/day) — highest revenue.

- Highway Fast Charge 01: ~€418/month — high traffic from highway placement.

- Central Plaza Station: ~€151/month — lowest utilization and revenue.

- Tech Park Supercharger: highest revenue per session (~€13.91).

## 7. Visualizations

Generated using matplotlib:

- Total Charging Hours by Station

- Charging Sessions by Hour of Day

- Price vs Session Duration (Scatter Plot)

- Total Revenue by Station

## 8. Possible Extensions

- Add weekday/weekend or weather effects

- Queueing / wait-time analysis

- Power BI or Tableau dashboard

- Predict session duration or kWh usage

- Estimate station-level profitability

- Simulate pricing strategies

## 9. Project Files

- ev_charger_analytics.ipynb — full analysis and visuals

- ev_charger_analytics.db — SQLite database (generated automatically)
