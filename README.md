# analyzing_data_with_pandas.py
# Assignment: Analyzing Data with Pandas and Visualizing Results with Matplotlib
# Author: [Jessica Chepkemoi]
# Date: [9th September 2025]

import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.datasets import load_iris

# Task 1: Load and Explore Dataset

iris = load_iris(as_frame=True)
df = iris.frame
df['species'] = iris.target_names[iris.target]

print("First 5 rows:")
print(df.head())

print("\nDataset info:")
print(df.info())

print("\nMissing values:")
print(df.isnull().sum())

# Clean missing values (if any)
df = df.dropna()


# Task 2: Basic Data Analysis

print("\nSummary statistics:")
print(df.describe())

print("\nAverage petal length per species:")
print(df.groupby("species")["petal length (cm)"].mean())


# Task 3: Data Visualization

sns.set(style="whitegrid")

# 1. Line chart
plt.figure(figsize=(8,5))
plt.plot(df.index, df["sepal length (cm)"], label="Sepal Length")
plt.title("Line Chart: Sepal Length Trend")
plt.xlabel("Index (as time)")
plt.ylabel("Sepal Length (cm)")
plt.legend()
plt.show()

# 2. Bar chart
plt.figure(figsize=(8,5))
sns.barplot(x="species", y="petal length (cm)", data=df, estimator="mean", ci=None)
plt.title("Bar Chart: Avg Petal Length per Species")
plt.xlabel("Species")
plt.ylabel("Petal Length (cm)")
plt.show()

# 3. Histogram
plt.figure(figsize=(8,5))
plt.hist(df["sepal length (cm)"], bins=15, color="skyblue", edgecolor="black")
plt.title("Histogram: Sepal Length Distribution")
plt.xlabel("Sepal Length (cm)")
plt.ylabel("Frequency")
plt.show()

# 4. Scatter plot
plt.figure(figsize=(8,5))
sns.scatterplot(x="sepal length (cm)", y="petal length (cm)", hue="species", data=df)
plt.title("Scatter Plot: Sepal vs Petal Length")
plt.xlabel("Sepal Length (cm)")
plt.ylabel("Petal Length (cm)")
plt.legend(title="Species")
plt.show()


# Error Handling Example

try:
    df_test = pd.read_csv("non_existent_file.csv")
except FileNotFoundError:
    print("Error: The dataset file was not found. Please check the file path.")


# Findings / Observations

# Setosa has the smallest petals; Virginica has the largest.
# Sepal length is roughly normally distributed.
# Sepal length and petal length are positively correlated.

