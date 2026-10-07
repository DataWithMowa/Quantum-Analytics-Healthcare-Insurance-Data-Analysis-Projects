# Health Insurance Coverage Dashboard

<img width="943" height="465" alt="Dashboard Health Insurance" src="https://github.com/user-attachments/assets/a6413c64-99fa-40b1-b23a-412d1d0f9e50" />

### 📊 Project Overview

**Did the Affordable Care Act actually reduce the number of uninsured Americans — and what made some states succeed more than others?**

This project analyzes uninsured rates, Medicaid enrollment, marketplace coverage, and employer coverage across all 50 states and DC, comparing 2010 (before the ACA) to 2015–2016 (after it took effect).

#### The Approach

Using Power BI, I cleaned the raw state-level data, fixed a calculation error I found in the source file, built KPI measures, and put together an interactive dashboard to explore how Medicaid expansion, marketplace access, and employer coverage each played into the drop in uninsured Americans.

### 🕹️ Interactive Dashboard Demo

See the dashboard filters, dynamic metrics, and charts in action below (39-second walkthrough):

https://github.com/user-attachments/assets/60798dd9-517b-4323-bbb5-352efcf2ba37

### To see the full live analysis: [Click here](https://lnkd.in/p/ep3GMA45)

### 💡 Key Data Insights & Discoveries

1. **The ACA Worked, Nationally:** The national uninsured rate dropped from **15.50% in 2010 to 9.40% in 2015** — a **6.10 percentage-point decline** in five years.
2. **Nevada Improved the Most:** Nevada's uninsured rate fell by **10.30 percentage points**, the single biggest decline of any state in the dataset.
3. **Medicaid Expansion Was the Biggest Driver:** **9 of the top 10 states with the largest declines expanded Medicaid.** Florida was the one exception — it leaned on the marketplace and tax credits instead.
4. **Running Your Own Marketplace Mattered Less Than Expected:** Only **4 of the top 10 best-performing states** ran their own state marketplace; the other 6 relied on the federal Healthcare.gov system.
5. **Most Coverage Still Comes From Employers:** Employer-provided insurance covers **172.3 million people** — far more than the marketplace (11.1 million) or the Medicaid enrollment growth (16.1 million) combined.

### 🛠️ Power BI Skills & Dashboard Setup

To turn a 52-row state dataset into a reliable before/after comparison, I used Power BI's data cleaning, data modeling, DAX, and dashboard features:

* **Data Cleaning & Preparation (Power Query):** Loaded `Health Insurance.csv` and cast each column to its correct type — percentages for the uninsured rates, whole numbers for enrollment and coverage counts, currency for the average tax credit, and a true/false flag for Medicaid expansion.

* **Fixing a Calculation Error in the Source Data:** The original **Uninsured Rate Change (2010–2015)** column recorded the national figure as **+6.0%** — implying the uninsured rate went *up*. Checking the real numbers (15.50% in 2010 → 9.40% in 2015) showed it should have been a **6.10-point decrease**. I removed the bad column entirely and replaced it with a calculated one: `[Uninsured Rate (2015)] - [Uninsured Rate (2010)]`, so every row's change value is now derived directly from its own two rates instead of trusted as given.

* **Adding Marketplace Type Manually:** The dataset had no column for whether a state ran its own insurance marketplace or used the federal Healthcare.gov system. I built a separate **Marketplace** table by hand, tagging all 52 rows **YES/NO** (13 states YES), and merged it into the main table with a `Table.NestedJoin` on **State**.

<img width="932" height="383" alt="image" src="https://github.com/user-attachments/assets/fe26b1ce-16b1-4055-b215-1eedf3c5d8e3" />

* **Data Modeling:** Two tables — **Health Insurance** (the main state-level table) and **Marketplace** (the manually-tagged lookup) — connected by a one-to-one relationship on **State**.

<img width="665" height="291" alt="image" src="https://github.com/user-attachments/assets/2641c7e5-3c92-4cd9-bbfb-1fc017749bd5" />

* **DAX Measures:**

| Measure | What it does | DAX |
|---|---|---|
| **Expanded States Count Out Of 51** | Counts states (excluding the national "United States" row) that expanded Medicaid | `CALCULATE(COUNTROWS('Health Insurance'), 'Health Insurance'[State Medicaid Expansion (2016)] = TRUE(), 'Health Insurance'[State] <> "United States")` |

<img width="632" height="34" alt="image" src="https://github.com/user-attachments/assets/168429f5-3796-44ad-8717-1544886b489c" />

* **Key Metric Tracking:** Created KPI cards to highlight the main numbers, including **National Uninsured Rate 2010 (15.50%), National Uninsured Rate 2015 (9.40%), Uninsured Rate Change (−6.10 points), States That Expanded Medicaid (32 of 51), and States With Their Own Marketplace (13 of 51).**

* **Chart Analysis:** Built visuals to rank states by uninsured-rate change, compare Medicaid enrollment in 2013 vs 2016, and break down coverage sources (employer, marketplace, Medicaid) by scale.

* **Interactive Slicers:** Added slicers for **State Medicaid Expansion** and **State Health Insurance Marketplace**, letting users filter the dashboard down to expansion vs. non-expansion states, or state-run vs. federal marketplace states.

### 📈 Strategic Recommendations & Next Steps

* **Prioritize Medicaid expansion first in any future coverage push** — it consistently outperformed marketplace access alone, appearing in 9 of the top 10 best-performing states.
* **Don't assume a state marketplace is necessary** — only 4 of the top 10 states ran one, so the bigger lever is clearly expansion, not marketplace ownership.
* **Study Florida as its own case**, since it achieved a strong decline (8 points) without formal Medicaid expansion, through heavy marketplace enrollment (1.53M people) and tax credits (1.43M people) plus organic Medicaid growth (540K people, 2013–2016).
* **Always verify source totals before publishing a story on them** — the fixed Uninsured Rate Change column is a reminder that one bad sign in a data entry can completely flip a narrative.
* **Expect the uninsured rate to keep falling, but more slowly** going forward, since the 2014 Medicaid expansion wave was a one-time policy jump rather than a repeating annual trend.

### 📂 How to Open and Explore the Dashboard

1. You can download the full file here: [Health_Insurance_Coverage_Dashboard.pbix](#)
2. Open the file locally using Power BI Desktop.
3. Go to the Dashboard page.
4. Use the Medicaid Expansion and State Marketplace slicers to filter all the charts.
5. Hover over the state ranking chart to compare uninsured-rate declines side by side.

### 🤝 Connect & Support

Thank you for taking the time to go through this project! If you have any questions or feedback, please reach out directly:

* 💼 **LinkedIn:** [Mowaninuola Umarudeen](https://www.linkedin.com/in/mowaninuolaumarudeen/)
* 📧 **Email:** [mowatheanalyst@gmail.com](mailto:mowatheanalyst@gmail.com)

*📈 **Did you find this useful?** Consider giving this repository a ⭐ **Star** if it helped you!*
