# Global Trends in Mental Health Disorders Dashboard

<img width="943" height="465" alt="Mental Health" src="https://github.com/user-attachments/assets/7ccff91a-fde6-496b-9350-87cd5bbb54c2" />

### 📊 Project Overview

**Which mental health disorders affect the most people, and has that changed over time?**

This project analyzes 45,276 prevalence records across 231 countries and regions, covering seven disorders — Depression, Anxiety, Bipolar disorder, Schizophrenia, Eating disorders, Drug use disorders, and Alcohol use disorders — from 1990 to 2017.

#### The Approach

Using Power BI, I cleaned a messy Kaggle dataset, rebuilt a usable population table out of a mislabeled column in the same file, built KPI measures, and put together an interactive dashboard to explore how disorder prevalence moves across countries, regions, and years.

### 🕹️ Interactive Dashboard Demo

See the dashboard filters, dynamic metrics, and charts in action below (XX-second walkthrough):

https://github.com/user-attachments/assets/79c74f1e-e33a-4781-81fa-80d7702ffea9

### To see the full live analysis: [Click here](https://lnkd.in/p/exQRZS8n)

### 💡 Key Data Insights & Discoveries

* Across all seven disorders, the average prevalence rate is 1.59% — but that number hides a wide spread between disorders, so it's best read alongside the breakdown below, not on its own.
* **Anxiety disorders carry the heaviest average load at 3.99%**, just ahead of Depression (3.50%). Both sit far above Alcohol use disorders (1.59%), Drug use disorders (0.86%), Bipolar disorder (0.72%), Eating disorders (0.24%), and Schizophrenia, the lowest at 0.21%.
* **New Zealand recorded the single highest prevalence rate in the dataset**, at just under 9% for Anxiety disorders, repeating at that level every year from 2000 to 2004.
* The dataset covers 231 countries and regions over a full 28-year window (1990–2017), giving enough history to compare disorder trends decade by decade.

### 🛠️ Power BI Skills & Dashboard Setup

To turn one messy Kaggle CSV into a clean, usable model, I used Power BI's data cleaning, data modeling, DAX, and dashboard features:

* **Data Cleaning & Preparation (Power Query):** Loaded `Mental health Depression disorder Data.csv` and cleaned it before building anything.
  * Renamed `Entity` to **Country Name**, cast the 7 disorder percentage columns and `Year` to numeric types
  * Removed rows with errors in `Year` and filtered out any `Depression (%)` values below 0, then filtered the data down to `Year >= 1990`
  * Added a **Country VS Region** column, using a blank `Code` to flag a row as a "Region" (e.g. World, continents) instead of a "Country"
    
<img width="304" height="377" alt="image" src="https://github.com/user-attachments/assets/1d9dc119-4ef2-478f-89b3-1f5163a88188" />

  * Built two versions of the cleaned table for two different jobs:
    * **Mental health Data** — unpivoted the 7 disorder columns into two columns, **Disorder Type** and **Prevalence**, then split off the "(%)" suffix from each disorder name. This long format is what powers country/disorder comparisons.
      
<img width="926" height="386" alt="image" src="https://github.com/user-attachments/assets/c654cab8-755d-471b-81cb-f67914db00b0" />

    * **Mental health Disorder Data** — kept the 7 disorder columns side by side (wide format), which is what powers the headcount measures below.

<img width="923" height="382" alt="image" src="https://github.com/user-attachments/assets/86797ca9-b5d6-4d9c-9001-2afdfc7b9258" />

* **Rebuilding Population from a Mislabeled Column:** The source file had no clean population column. I found that population figures were sitting inside the **Eating disorders (%)** column of a different block in the same CSV, mixed in with the real percentage values. I pulled that block out into its own `Population By Country` table, renamed the column to **Population**, and filtered it to values **greater than 1,000** — since real eating-disorder percentages are always under 100, this cleanly separated the population numbers from the actual percentages. I then merged `Population` into `Mental health Disorder Data` with a left outer join on Country Name + Year.

<img width="931" height="401" alt="image" src="https://github.com/user-attachments/assets/ba70b64b-5e92-4c87-8159-263b76d344af" />

* **Data Modeling:** Built a `Calendar` table (`CALENDAR(1990-01-01, 2017-12-31)`) and connected it to both `Mental health Data[Year]` and `Mental health Disorder Data[Year]` with one-directional, one-to-many relationships, so a single date-based slicer can filter across both tables at once. Also added a small calculated **"Top N countries"** table (`GENERATESERIES(5, 20, 5)`) to drive a dynamic Top-N ranking visual.

<img width="710" height="278" alt="image" src="https://github.com/user-attachments/assets/fe5f7fb4-7b47-4f1d-b3e5-253f48c11cb7" />

<img width="178" height="169" alt="image" src="https://github.com/user-attachments/assets/f640c6a1-81e1-4dd7-9588-59e0b1ee3e4f" />

* **DAX Measures:** Kept all measures in one dedicated `Measures (2)` table:

| Measure | What it does | DAX |
|---|---|---|
| **Countries Tracked** | Counts every distinct country/region | `DISTINCTCOUNT('Mental health Disorder Data'[Country Name])` |
| **Years Covered** | Counts every distinct year | `DISTINCTCOUNT('Mental health Disorder Data'[Year])` |
| **AVG Prevalence %** | Average prevalence across all disorders combined | `AVERAGE('Mental health Data'[Prevalence])` |
| **AVG Depression %** | Average Depression prevalence | `AVERAGE('Mental health Disorder Data'[Depression (%)])` |
| **AVG Anxiety Disorder %** | Average Anxiety prevalence | `AVERAGE('Mental health Disorder Data'[Anxiety disorders (%)])` |
| **AVG Alcohol Use Disorder %** | Average Alcohol use prevalence | `AVERAGE('Mental health Disorder Data'[Alcohol use disorders (%)])` |
| **AVG Drug Use Disorder %** | Average Drug use prevalence | `AVERAGE('Mental health Disorder Data'[Drug use disorders (%)])` |
| **AVG Bipolar Disorder %** | Average Bipolar disorder prevalence | `AVERAGE('Mental health Disorder Data'[Bipolar disorder (%)])` |
| **AVG Eating Disorder %** | Average Eating disorder prevalence | `AVERAGE('Mental health Disorder Data'[Eating disorders (%)])` |
| **AVG Schizophrenia %** | Average Schizophrenia prevalence | `AVERAGE('Mental health Disorder Data'[Schizophrenia (%)])` |
| **Highest Prevalence Country** | Returns the country with the single highest recorded rate | `VAR CountriesOnly = FILTER(...) VAR MaxPrev = MAXX(CountriesOnly, [Prevalence]) RETURN CALCULATE(SELECTEDVALUE([Country Name]), FILTER(CountriesOnly, [Prevalence] = MaxPrev))` |
| **Total Population (Latest Year)** | Sums population for countries only, in the most recent year | `CALCULATE(SUM([Population]), [Year] = MAX([Year]), [Country VS Region] = "Country")` |
| **Depression / Anxiety / Alcohol Use / Drug Use / Bipolar / Eating Disorder / Schizophrenia Headcount** | Estimated number of people affected, per disorder | `SUMX('Mental health Disorder Data', [Disorder %] / 100 * [Population])` |
| **Top N countries Value** | Reads the selected value from the Top N slicer (defaults to 10) | `SELECTEDVALUE('Top N countries'[Top N countries], 10)` |

<img width="292" height="311" alt="image" src="https://github.com/user-attachments/assets/c5d2c5a3-8c92-41fd-9d9a-54894d991b41" />

* **Key Metric Tracking:** Created KPI cards to highlight the main numbers, including **Countries Tracked (231), Years Covered (28), AVG Prevalence % (1.59%), and Highest Prevalence Country (New Zealand).**

<img width="439" height="55" alt="image" src="https://github.com/user-attachments/assets/7f706ad0-fb6e-4241-96e1-a9148e9663fd" />

* **Chart Analysis:** Built visuals to compare average prevalence by disorder type, trace prevalence trends across the 1990–2017 window, and rank countries using the dynamic Top N slicer.

* **Interactive Slicers:** Added slicers for **Country VS Region, Disorder Type, and Top N countries**, letting users filter the whole dashboard down to a specific country/region, disorder, or ranking size.

<img width="233" height="50" alt="image" src="https://github.com/user-attachments/assets/df7f259a-af51-4d6f-ae4a-8aa15c13c173" />

### 📈 Strategic Recommendations & Next Steps

* **Treat the combined "AVG Prevalence %" (1.59%) as a summary number only.** It averages seven very different disorders together (ranging from 0.21% to 3.99%), so it should always be shown next to the per-disorder breakdown, never alone.
* **Re-check the Headcount measures before publishing them.** Summing `Disorder % × Population` across every row adds up population across all 28 years *and* across overlapping Country/Region rows (e.g. "World" alongside its own countries), which inflates the totals well past the real 2017 world population. These should be rewritten to calculate at a single year and Country-only filter, the same way **Total Population (Latest Year)** already does.
* **Flag single-year prevalence spikes with care.** New Zealand's "highest prevalence" result is Anxiety disorders holding steady near 9% for five straight years (2000–2004) — worth confirming this is a genuine trend and not a data entry repeat before calling it out as a standout finding.
* **Document the Population rebuild clearly for anyone else opening this file.** The Population By Country table depends on a value-range filter (`> 1000`) to separate population figures from percentages in a mislabeled column — a fragile fix that would break if the source file changes shape.

### 📂 How to Open and Explore the Dashboard

1. You can download the full file here: [Mental_Health_Disorder_Project.pbix](https://github.com/DataWithMowa/Quantum-Analytics-Healthcare-Insurance-Data-Analysis-Projects/tree/main/Global%20Trends%20in%20Mental%20Health%20Disorders%20Power%20BI%20Project/Full%20Project)
2. Open the file locally using Power BI Desktop.
3. Go to the Dashboard page.
4. Use the Year and Disorder Type slicers to filter all the charts.
5. Hover over the prevalence trend chart to compare how each disorder has moved from 1990 to 2017.

### 🤝 Connect & Support

Thank you for taking the time to go through this project! If you have any questions or feedback, please reach out directly:

* 💼 **LinkedIn:** [Mowaninuola Umarudeen](https://www.linkedin.com/in/mowaninuolaumarudeen/)
* 📧 **Email:** [mowatheanalyst@gmail.com](mailto:mowatheanalyst@gmail.com)

*📈 **Did you find this useful?** Consider giving this repository a ⭐ **Star** if it helped you!*
