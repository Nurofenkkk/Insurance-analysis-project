# 🩺 Medical Cost Analysis Project

**Tools Used:** Jupyter Notebook, Python (Pandas, Matplotlib, Scikit-learn), PostgreSQL, Power BI  
**Dataset:** U.S. medical insurance cost data (CSV format)

## 📌 Project Summary

This project focuses on preprocessing, analyzing, and visualizing medical insurance cost data. The workflow includes:

- **Data Cleaning & Feature Engineering:**
  - Loaded raw CSV data using Pandas.
  - Created a binary feature `sex_male` to encode gender.
  - Categorized BMI values into five groups: *underweight*, *normalweight*, *overweight*, *obesity*, and *highobesity*.
  - Applied **Min-Max normalization** and **Z-score standardization** to the `charges` column.
  - Imputed missing `age` values using both **mean imputation** and **linear regression** based on `charges`.

- **Visualization:**
  - Used Matplotlib to plot the distribution of BMI categories.
  - Created interactive dashboards in **Power BI**, including:
    - Average charges by age and smoker status.
    - Count of BMI categories.
    - Z-score normalized charges by age.

- **Database Integration:**
  - Exported the processed dataset to a **PostgreSQL** database using SQLAlchemy.
  - Connected the database to **Power BI** for dynamic reporting (read-only access due to credential protection).

## 🧠 Key Skills Demonstrated
- Data preprocessing and transformation
- Feature engineering and regression modeling
- Data visualization and storytelling
- Integration of Python with SQL and BI tools
