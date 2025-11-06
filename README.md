# 🩺 Medical Cost Analysis Project

**Tools Used:** Jupyter Notebook, Python (Pandas, Matplotlib, Scikit-learn, SQLAlchemy), PostgreSQL, Power BI, Excel

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


## ⚙️ How to Run
- Clone the repository:
  git clone https://github.com/Nurofenkkk/Insurance-analysis-project.git
  cd Insurance-analysis-project

- Install dependencies:
  pip install -r requirements.txt

- Run Jupyter Notebook:
  jupyter notebook p4.ipynb

- Database connection (optional):
  Update the connection string in the notebook:
  engine = create_engine("postgresql+psycopg2://<username>:<password>@localhost:5432/<database>")
  
- Power BI visualization:
  Open project1.pbix in Power BI Desktop.
  Data is already connected (read-only).

## 🖥️ Example Code Snippet

import pandas as pd
from sklearn.linear_model import LinearRegression

# Load dataset
df = pd.read_csv('Medical Costs (pro Aktivitu 4).csv')

# Feature engineering
df['sex_male'] = (df['sex'] == 'male').astype(int)

def bmi_category(bmi):
    if pd.isna(bmi):
        return 'unknown'
    elif bmi < 18.5:
        return 'underweight'
    elif bmi < 25:
        return 'normalweight'
    elif bmi < 30:
        return 'overweight'
    elif bmi < 35:
        return 'obesity'
    else:
        return 'highobesity'

df['bmi_category'] = df['bmi'].apply(bmi_category)

# Normalization
df['charges_minmax'] = (df['charges'] - df['charges'].min()) / (df['charges'].max() - df['charges'].min())
df['charges_zscore'] = (df['charges'] - df['charges'].mean()) / df['charges'].std()

# Impute missing age using regression
train = df[df['age'].notna()]
model = LinearRegression().fit(train[['charges']], train['age'])
df.loc[df['age'].isna(), 'age'] = model.predict(df.loc[df['age'].isna(), ['charges']])
