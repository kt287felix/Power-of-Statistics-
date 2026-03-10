# 📊 Power of Statistics — Descriptive Statistics with Python

## About This Project

Statistics is the backbone of data analysis. Before building models or drawing conclusions, every data analyst must first **understand their data** — and descriptive statistics is how you do that.

This project explores **descriptive statistics using Python** on a real-world education dataset from India, covering district-wise literacy rates across 680 districts for the academic year **2015–16**. Through this work, I practiced computing and interpreting key statistical measures that reveal the shape, center, and spread of data.

---

## 📁 Dataset

**Source:** Education in India — District-wise (2015–16)
**Download:** 👉 [https://www.kaggle.com/datasets/rajanand/education-in-india?resource=download](https://www.kaggle.com/datasets/rajanand/education-in-india?resource=download)

> ⚠️ **You will download a `.zip` file from Kaggle. Unzip it first.** Then locate `2015_16_Districtwise.csv` and save it in your working folder as `education_districtwise.csv` before running the notebook.

---

## ⚙️ Step 0 — Set Your Working Directory First

> 🔴 This is the **most important setup step** and the most common cause of errors. Always do this before loading any data.

**How to find your folder path (Windows):**
1. Open the folder where you saved your CSV file
2. **Right-click** on an empty space inside the folder
3. Select **Properties**
4. Under the **Location** tab, copy the path shown
5. Paste it into the code below

```python
import os
os.chdir('C:\\Users\\YourName\\Downloads\\your_folder')  # paste your path here (Windows)
# os.chdir('/Users/yourname/Downloads/your_folder')      # Mac / Linux
```

> 💡 On Windows, replace any single backslashes `\` in the copied path with double backslashes `\\` — for example `C:\Users\John` becomes `C:\\Users\\John`.

This tells Python exactly where to look for your CSV file. Without it, `read_csv()` will fail with a `FileNotFoundError`. You can confirm it worked with:

```python
print(os.getcwd())
```

---

## 📦 Libraries

```python
import os
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

---

## 📖 The Analysis

### Loading the Data

```python
education_districtwise = pd.read_csv('education_districtwise.csv')
education_districtwise.head(6)
```

The dataset spans **680 rows and 819 columns**, capturing everything from school counts to population figures across every district in India. The key column for this analysis is `OVERALL_LI` — the overall **literacy rate (%)** per district.

---

### The `describe()` Function — Your First Stop

One of the most powerful tools for getting to know your data quickly is the `describe()` function. A single line reveals a full statistical picture:

```python
education_districtwise['OVERALL_LI'].describe()
```

```
count    634.000000
mean      73.395189
std       10.098460
min       37.220000
25%       66.437500
50%       73.490000
75%       80.815000
max       98.760000
```

In one call, `describe()` surfaces the **count, mean, standard deviation, minimum, three quartiles, and maximum** — everything you need to understand the distribution of a numerical variable at a glance.

> 💡 Notice the mean (~73.4%) and median (~73.5%) are nearly identical. This tells us the literacy rate distribution is **roughly symmetric** — no extreme skew pulling the average away from the center.

`describe()` also works on **categorical columns**, but returns different statistics:

```python
education_districtwise['STATNAME'].describe()
```

```
count              680
unique              36
top       UTTAR PRADESH
freq               75
```

For text data, Python instead returns the **count, number of unique values, the most frequent value (top), and its frequency** — equally useful for understanding categorical distributions.

---

### Individual Functions for Deeper Control

While `describe()` gives you everything at once, Python also provides **individual functions** for each statistic. These become essential when you want to **compute further or build logic** on top of a specific measure.

#### Measures of Central Tendency

Central tendency tells you *where* your data is centered:

```python
mean_literacy_rate   = education_districtwise['OVERALL_LI'].mean()
median_literacy_rate = education_districtwise['OVERALL_LI'].median()
blocks_mode          = education_districtwise['BLOCKS'].mode()

print("Mean Literacy Rate:",   mean_literacy_rate)    # 73.395%
print("Median Literacy Rate:", median_literacy_rate)  # 73.490%
print("Mode of BLOCKS:",       blocks_mode)           # 6
```

| Function | What It Measures | When to Use It |
|----------|-----------------|----------------|
| `mean()` | Arithmetic average | General center, when no extreme outliers |
| `median()` | Middle value | When outliers are present — more robust |
| `mode()` | Most frequent value | Categorical or discrete data |

Earlier in the program, `mean()` and `median()` were used together specifically to **detect outliers** — if the mean pulls far from the median, it signals skewed data or extreme values worth investigating.

---

#### Measures of Dispersion

Dispersion tells you *how spread out* your data is around the center:

```python
std_dev  = education_districtwise['OVERALL_LI'].std()
variance = education_districtwise['OVERALL_LI'].var()
range_li = education_districtwise['OVERALL_LI'].max() - education_districtwise['OVERALL_LI'].min()

print("Standard Deviation:", std_dev)   # 10.098
print("Variance:",           variance)  # 101.979
print("Range:",              range_li)  # 61.54
```

| Function | What It Measures |
|----------|-----------------|
| `std()` | Average distance of each value from the mean |
| `var()` | Square of standard deviation — amplifies spread |
| `max() - min()` | Full span of the data from lowest to highest |

> 💡 The `min()` and `max()` functions are especially powerful when **used together** — combining them gives you the **range**, which captures the total spread of your data in a single number. Here, literacy rates span **61.54 percentage points** (37.22% to 98.76%), revealing a dramatic inequality in education outcomes across Indian districts.

---

## 🔑 Key Takeaways

- **`describe()`** is your fastest tool for a full statistical overview — numerical and categorical alike
- Python's **individual stat functions** (`mean()`, `median()`, `std()`, `var()`, `min()`, `max()`) give you precision and flexibility when you need to go further
- **Mean vs Median** comparison is a quick and reliable outlier detection technique
- Combining `min()` and `max()` to compute **range** is a practical example of how individual functions unlock further computation
- India's district-level literacy data shows a **73% average rate** but a **61-point range** — statistics that together tell a much richer story than either would alone

---

## 📂 Repository Structure

```
📁 Power-of-Statistics/
│
├── Power_of_Statistics.ipynb    ← Jupyter Notebook with full analysis
├── education_districtwise.csv   ← Dataset (download & unzip from Kaggle)
└── README.md                    ← This file
```

---

## 👤 Author

Aspiring Data Analyst | Google Advanced Data Analytics Certificate — Coursera
