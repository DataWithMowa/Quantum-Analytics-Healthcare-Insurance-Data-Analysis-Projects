# Car Insurance Policies Dashboard

<img width="944" height="467" alt="image" src="https://github.com/user-attachments/assets/78957bfc-d4ed-4359-8b93-90cc40da5506" />

### 📊 Project Overview

**Who actually files a claim more — men or women? Rich or poor? Educated or not? Or is it something as simple as the car they drive?**

This project analyzes over 37,000 real car insurance policies to find out what actually drives claims, by testing personal demographics against vehicle-level factors.

#### The Approach

Using Excel, I cleaned the raw policy data, built KPI measures for claims and payouts, and tested claim behavior across gender, education, income, coverage zone, and car details to isolate what actually predicts a claim.

### 🕹️ Interactive Dashboard Demo

See the dashboard filters, dynamic metrics, and charts in action below (23-second walkthrough): 

https://github.com/user-attachments/assets/c64a86dc-dd8b-4517-8667-968a7acf94c1

### To see the full live analysis: [Click here](https://lnkd.in/p/eN-CdbgC)

### 💡 Key Data Insights & Discoveries

* Out of 37,542 total policies, 19,158 claims were filed — an average of 0.51 claims per person, or roughly 1 in 2 people. The average claim amount is ₦50,000, and total payouts exceed ₦1.8 billion.
* 80% of cars are used privately, and 20% commercially — and this split holds steady no matter who the driver is.
* **Gender, kids driving, education, coverage zone, and household income showed no meaningful difference in claims.** Everyone files about the same number of claims, for about the same amount, regardless of background.
* **Car make and car color are what actually move the numbers.** Ford stood out with more claims than any other brand, ahead of Chevrolet, Dodge, Toyota, and GMC. Indigo, Aquamarine, and Purple cars also showed slightly higher claim rates than colors like Yellow or Maroon.

### 🛠️ Excel Skills & Dashboard Setup

To turn 37,542 raw policy records into clear business insights, I used Excel's data cleaning, visualization, and interactive dashboard features:

* **Data Cleaning & Preparation:** Reviewed the dataset for quality issues before building anything.
  * Found one ID (56-5402470) reused across two different people with different birthdates, claims, and income — not a true duplicate row, just a reused ID. Left as is.
  * Fixed a misspelling of "Separated" under `marital_status`, which had been entered as "Seperated."
  * Found one `car_year` entry of 1909, standing out against all other years (up to 2013) — likely a typo, left in for now as a flagged entry worth a second look.
  * No blank cells anywhere in the dataset.

* **Key Metric Tracking:** Created KPI cards to highlight the main numbers, including **Total Policies (37,542), Total Claims Filed (19,158), Average Claim Frequency (0.51), Average Claim Amount (₦50,000), and Total Claims Paid (₦1.8B+).**

<img width="684" height="53" alt="image" src="https://github.com/user-attachments/assets/76b73b09-9501-4d7b-9658-6ba8852fd723" />

* **Combo Chart Analysis:** Used combination charts to test claim behavior across personal demographics — gender, kids driving, education, coverage zone, and household income — and against vehicle-level factors — car make and car color — to isolate which ones actually predict a claim.

<img width="826" height="452" alt="image" src="https://github.com/user-attachments/assets/fe104870-80dc-4ee4-8eed-47fecf2911ee" />

* **Interactive Filters:** Added slicers so anyone can click around and filter the dashboard by car make, coverage zone, or other segments instantly.

<img width="128" height="467" alt="image" src="https://github.com/user-attachments/assets/203f2c59-7531-4e21-b769-494f067a69ce" />

### 📈 Strategic Recommendations & Next Steps

* Stop pricing premiums based on personal demographics — gender, education, income, and location showed no real difference in claims behavior, so leaning on them adds bias without adding accuracy.
* Give more weight to vehicle-level factors, especially car make and car color, when setting premiums — that's where the actual risk pattern shows up.
* Compare claims against the total number of policies for each car make and model next, to confirm whether Ford genuinely carries higher risk or simply has more vehicles represented in the dataset.
* Revisit the flagged 1909 `car_year` entry and the reused ID before this data is used for anything beyond exploratory analysis.

### 📂 How to Open and Explore the Workbook

1. You can download the full file here: [Car_Insurance_Policies.xlsx](#)
2. Open the file locally using **Microsoft Excel desktop**.
3. Go to the **Dashboard** Sheet.
4. Use the slicers on the dashboard to filter the charts by car make, coverage zone, or other segments dynamically.

### 🤝 Connect & Support

Thank you for taking the time to go through this project! If you have any questions or feedback, please reach out directly:

* 💼 **LinkedIn:** [Mowaninuola Umarudeen](https://www.linkedin.com/in/mowaninuolaumarudeen/)
* 📧 **Email:** [mowatheanalyst@gmail.com](mailto:mowatheanalyst@gmail.com)

*📈 **Did you find this useful?** Consider giving this repository a ⭐ **Star** if it helped you!*
