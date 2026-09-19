# weather-impact-analysis-system-


# Weather Impact Analysis System

A comprehensive, pure Python-based command-line analytics prototype designed to process daily meteorological observations, evaluate environmental stress thresholds, generate agricultural risk metrics, and provide actionable business intelligence for commercial farming operations in tropical regions like Nigeria.

---

## Project Background & Problem Statement

In modern agricultural sectors across tropical environments, commercial farming and crop production face severe financial, operational, and supply-chain risks driven by unpredictable climatic variations. Unmonitored environmental shifts—such as extreme thermal spikes, prolonged droughts, and heavy unseasonal downpours—directly threaten field schedules, crop physiology, and daily logistics. 

The core problem this project solves is clear: **Without automated threshold detection, risk scoring, and structured data analysis, agricultural organizations struggle with unmitigated operational downtime, miscalculated field labor, wasted chemical inputs, and unrecovered crop damage.** 

The **Weather Impact Analysis System** was built from the ground up to bridge this gap. By transforming raw daily weather logs into quantifiable, actionable risk intelligence, this system shifts farm management from reactive emergency response to proactive, data-driven planning.

---

##  Development Challenges Faced & Solutions Implemented

Building a complete analytics engine entirely from scratch using pure Python without relying on advanced data science libraries came with specific technical hurdles. Here are the exact challenges faced during development and how they were solved:

### 1. Challenge: Simulating Relational Data Grouping Without SQL or Pandas
* **The Problem:** In standard data analysis, grouping data by location (e.g., getting averages for Lagos vs. Kano) is typically done instantly using SQL `GROUP BY` clauses or Pandas `.groupby()` methods. Because this project strictly prohibited external libraries and databases, organizing and aggregating regional data manually felt complex.
* **The Solution:** We implemented a **nested loop architecture**. An outer loop iterates through our target cities, while an inner loop scans through all 30 records from top to bottom. Whenever the inner loop finds a record matching the city in the outer loop, it extracts, accumulates, and calculates the regional totals and averages from scratch.

### 2. Challenge: Preventing Console Application Crashes from User Typos
* **The Problem:** The system features an interactive 12-option command-line menu. If a user accidentally typed a letter (like "abc") instead of a menu number (like "3"), the raw input would trigger a `ValueError` and crash the entire Python script, forcing the user to restart.
* **The Solution:** We wrapped our user input collection inside **`try` and `except` blocks**. If the user enters invalid text, the code catches the error gracefully, prints a polite warning message (*"Invalid input! Please enter a number between 1 and 12"*), and allows the user to try again without breaking the program.

### 3. Challenge: Avoiding Repetitive Code for Threshold Checking
* **The Problem:** We needed to evaluate different rules for temperature (checking for extreme heat $\ge 35^\circ\text{C}$) and rainfall (checking for heavy downpours) across 30 different records. Writing out separate conditional statements for every single record manually would have created hundreds of lines of messy, repetitive code.
* **The Solution:** We designed modular, reusable **custom functions (`def`)**. By writing the logic once inside dedicated functions like `classify_temperature()` and `classify_rainfall()`, we could call those functions instantly inside a standard loop for every single day's record.

---

##  Step-by-Step Breakdown of the Python Code Components

Every single part of the Python script was written from scratch. Here is a detailed explanation of each component piece by piece:

### 1. The Dataset Container (`weather_data` List of Dictionaries)
* **What it does:** Acts as our internal storage database. 
* **How it works:** We created a main Python list using square brackets `[]`. Inside this list, we placed 30 dictionaries using curly brackets `{}`. Each dictionary represents one day's weather log and uses clear key-value pairs (e.g., `{"date": "2025-04-01", "location": "Lagos", "temperature": 31, "rainfall": 12, "humidity": 80, "wind_speed": 15, "crop_yield": 4.2, "disruption": "No"}`). This ensures the computer never confuses temperature with rainfall.

### 2. Custom Classification Functions (`def`)
* **What it does:** Translates raw numerical data into meaningful qualitative categories.
* **How it works:** 
  * `classify_temperature(temp)`: Uses `if-elif-else` statements to evaluate whether a temperature number is "Moderate", "Hot", or "Extreme Heat".
  * `classify_rainfall(rain)`: Evaluates precipitation numbers to categorize days into "No Rain", "Light Shower", "Moderate Rain", or "Heavy Storm".

### 3. The Risk-Scoring Engine (`calculate_risk_score()`)
* **What it does:** Combines multiple environmental factors into a single quantitative risk score for each day.
* **How it works:** The function looks at temperature spikes, high wind speeds, and heavy rainfall together, assigning penalty points. It then translates the total score into a risk category: *Low Risk, Moderate Risk, High Risk,* or *Critical Risk*.

### 4. Aggregation & Summary Loops (`for` loops)
* **What it does:** Scans the entire dataset to calculate overall statistics.
* **How it works:** A standard `for` loop walks through all 30 dictionaries sequentially, adding up total rainfall, finding the highest and lowest temperatures, and calculating overall dataset averages.

### 5. The Location Leaderboard (Nested Loops)
* **What it does:** Ranks agricultural regions from highest risk to lowest risk.
* **How it works:** Uses an outer loop to cycle through the cities (Lagos, Kano, Ibadan) and an inner loop to check every record. It groups matching records together, calculates regional averages, and sorts them into a clean leaderboard.

### 6. The Interactive Menu & Safety Loop (`while` loop + `try-except`)
* **What it does:** Powers the user-facing command-line interface.
* **How it works:** A `while choice != 12:` loop keeps the application running continuously so the user can check different menus without restarting the script. Combined with `try-except`, it provides a bulletproof user experience.

---

##  Data Scope & Source Transparency

A frequent and critical question asked by evaluators during reviews is: *"The data is based on ground observations—where did we get the data from, and how is it structured?"*

### 1. Data Source & Transparency
To be completely transparent, the data used for this educational prototype is **not** pulled from live, official government meteorological stations or real-time external APIs. Instead, it is a **carefully designed simulated educational dataset** created specifically to model realistic Nigerian agricultural and climatic conditions. It allows us to demonstrate core software engineering and data analysis principles before connecting to enterprise-grade databases.

### 2. Dataset Composition & Scope
The dataset comprises **30 daily weather observation records** spanning across April and May 2025. These records are evenly distributed across **three key agricultural zones in Nigeria**:
* **Lagos:** Representing coastal, high-rainfall, and humid southern conditions.
* **Ibadan:** Representing transitional rainforest-savanna agricultural dynamics.
* **Kano:** Representing arid, extreme-heat northern agricultural environments.

### 3. The Six Core Environmental & Operational Parameters
Every single record comprehensively tracks **six key variables**:
1. **Temperature (°C):** Measures ambient thermal levels to isolate extreme heat stress events (specifically tracking days $\ge 35^\circ\text{C}$).
2. **Rainfall (mm):** Measures precipitation volumes to track cumulative wet-season impact, flood risks, and soil waterlogging potential.
3. **Humidity (%):** Measures relative atmospheric moisture levels affecting plant physiology, transpiration rates, and fungal disease spread.
4. **Wind Speed (km/h):** Measures wind velocity to track severe gusts, storm potential, and physical crop lodging risks.
5. **Crop Yield (tons/hectare):** Tracks agricultural productivity performance relative to regional weather exposure.
6. **Operational Disruption (Yes/No):** A binary tracking status recording whether weather conditions caused work stoppages, transport delays, or field downtime.

---

##  Major Analytical Findings & Results

When our analytical scripts ran across the 30 records, several critical insights emerged:

* **Regional Climatic Divergence:** 
  **Kano** exhibited extreme vulnerability to thermal stress, recording the dataset's peak temperature of **41°C** (on May 10, 2025) alongside lower baseline crop yields due to heat pressure. Conversely, **Lagos** experienced maximum hydrological volume, logging up to **110 mm** of rainfall in a single day (May 20, 2025) and higher humidity levels. **Ibadan** maintained a relatively balanced transitional microclimate.
* **Temporal Risk Shift (April vs. May):** 
  When comparing time periods, total recorded rainfall across the sample doubled from April to May (rising from 160 mm to 280 mm). This environmental shift directly drove total operational disruption days up from 5 days in April to 9 days in May.
* **Risk Leaderboard Ranking:** 
  Based on our custom multi-variable risk-scoring model, **Kano** emerged as the highest-risk operational zone in the sample, averaging a high-risk score profile due to its intense thermal exposure and stress factors.

---

##  Industrial Applications & Climate Relevance

Evaluators frequently ask: *What are the industrial applications, and how can we apply this to climate?* While our project runs on a small prototype dataset, the underlying logic has massive real-world applications across three major industries:

1. **Commercial Farming & Crop Protection:** 
   Agricultural enterprises can deploy this system to monitor thermal and hydrological stress across different farm locations in real time. When temperatures cross critical thresholds (like extreme heat above $35^\circ\text{C}$) or heavy rainfall threatens soil saturation, managers can automatically trigger irrigation or protect sensitive crops before damage occurs.
2. **Climate Resilience & Early-Warning Systems:** 
   Government bodies or environmental agencies focused on climate change can scale this tool to act as a regional early-warning system. Just as our Location Leaderboard identified Kano as a high-risk zone, climate analysts can use this risk-scoring model to identify vulnerable rural communities heading into drought or flood seasons, allowing them to pre-position emergency relief.
3. **Supply Chain & Field Operations Scheduling:** 
   Agribusinesses suffer heavy financial losses when unexpected weather halts transport or field labor. Companies can use our disruption-tracking logic to build dynamic labor schedules—halting fertilizer application, spraying, or transit ahead of heavy storm forecasts to prevent input wastage and keep workers safe.

---

## Strategic Recommendations

Based on our Observation-Interpretation-Recommendation framework, we developed three major strategic solutions for farm and business managers:

1. **Regional Infrastructure Alignment (Fitting the Solution to Geography):**
   * *For Kano (High-Heat Zone):* Immediate investment in heat-tolerant crop varieties, artificial irrigation networks, and shade-netting infrastructure to protect plants from severe thermal stress.
   * *For Lagos & Ibadan (Heavy-Rainfall Zones):* Prioritizing high-capacity drainage channels and raised seedbed systems so that floodwater flows away safely instead of waterlogging crops.
2. **Dynamic Labor Scheduling & Disruption Protocols:** 
   Since our data proved that operational disruptions consistently happened on days with higher rainfall and stronger winds, farm managers should use weather forecasts to dynamically shift high-labor activities (such as fertilizer application, spraying, and harvesting) *before* heavy storms arrive, eliminating financial waste and protecting workers.
3. **Risk Prioritization & Future System Scalability:** 
   Because Kano scored the highest average risk score in our sample, leadership must prioritize it for early-warning attention, constant monitoring, and specialized emergency support relative to other regions.

---

## Future Scalability: How the System Automatically Updates

When asked how this system will automatically update instead of relying on static simulated data, the technical roadmap involves three major upgrades:
1. **Relational Databases:** Migrating from hardcoded Python dictionaries to database systems like PostgreSQL or SQLite where incoming daily data can be stored securely.
2. **Live Weather APIs:** Connecting our script to live meteorological data feeds—such as automated APIs from official bodies like the **Nigerian Meteorological Agency (NiMet)**—to pull fresh temperature, rainfall, and wind data daily without manual typing.
3. **Automated Data Pipelines:** Using libraries like Pandas to ingest live data streams automatically, run our custom risk-scoring and threshold functions in the background, and instantly push updated alerts or dashboard visuals to farm managers.


---

##  Getting Started & Running the Code

1. Clone the repository to your local machine:
   ```bash
   git clone [https://github.com/saadah-the-analyst/weather-impact-analysis-system.git](https://github.com/saadah-the-analyst/weather-impact-analysis-system.git)

Ensure you have Python and Jupyter Notebook installed.

2. Open your terminal or Jupyter Notebook environment and open your file:
⁠weather-impact-analysis-management-system.ipynb⁠

Run the notebook cells step-by-step or use the "Run All" feature to explore weather summaries, risk alerts, and regional leaderboards.

# Author
 Muhyideen Saadah Aduke
 Data Analyst & Agricultural Science Specialist
