# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT
~~~    
# ----------------------------------------
# Step 1: Import Required Packages
# ----------------------------------------
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

# ----------------------------------------
# Step 2: Load the Dataset
# ----------------------------------------
data = pd.read_csv("titanic_dataset.csv")

print("\nDataset Loaded Successfully\n")
print(data.head())
print("\nDataset Info:\n")
print(data.info())
print(data.describe())

<img width="939" height="761" alt="Screenshot 2026-03-09 111518" src="https://github.com/user-attachments/assets/aadf7017-3908-448f-88fc-59369322e4e7" />

# ----------------------------------------
# Step 3: Data Cleansing - Handle Missing Values
# ----------------------------------------
for column in data.columns:
    if data[column].dtype == 'object':
        data[column] = data[column].fillna(data[column].mode()[0])   # Mode for categorical
print("\nMissing values handled successfully.\n")

<img width="490" height="123" alt="Screenshot 2026-03-09 111608" src="https://github.com/user-attachments/assets/3d965dfe-421f-426d-a8a6-6664281ab42e" />

# ----------------------------------------
# Step 4: Boxplot to Analyze Outliers (Age & Fare)
# ----------------------------------------
plt.figure(figsize=(6,4))
sns.boxplot(x=data["Age"])
plt.title("Boxplot - Age")
plt.show()

plt.figure(figsize=(6,4))
sns.boxplot(x=data["Fare"])
plt.title("Boxplot - Fare")
plt.show()

<img width="642" height="526" alt="Screenshot 2026-03-09 111652" src="https://github.com/user-attachments/assets/a16d80af-9904-4858-9448-cf71983ed4e0" />
<img width="705" height="555" alt="Screenshot 2026-03-09 111658" src="https://github.com/user-attachments/assets/6e92c41e-cf10-49fb-a770-d612a4b81313" />

# ----------------------------------------
# Step 5: Remove Outliers Using IQR Method
# ----------------------------------------
def remove_outliers_iqr(df, column):
    Q1 = df[column].quantile(0.25)
    Q3 = df[column].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    return df[(df[column] >= lower) & (df[column] <= upper)]

data = remove_outliers_iqr(data, "Age")
data = remove_outliers_iqr(data, "Fare")

print("Outliers removed using IQR method.\n")
<img width="458" height="56" alt="Screenshot 2026-03-09 111736" src="https://github.com/user-attachments/assets/edee5743-625d-49ad-af7d-def75fb726b0" />

# ----------------------------------------
# Step 6: Countplot for Categorical Data
# ----------------------------------------
plt.figure(figsize=(6,4))
sns.countplot(x="Survived", data=data)
plt.title("Countplot - Survival Distribution")
plt.show()

plt.figure(figsize=(6,4))
sns.countplot(x="Sex", data=data)
plt.title("Countplot - Gender Distribution")
plt.show()

plt.figure(figsize=(6,4))
sns.countplot(x="Pclass", data=data)
plt.title("Countplot - Passenger Class Distribution")
plt.show()

<img width="770" height="543" alt="Screenshot 2026-03-09 111813" src="https://github.com/user-attachments/assets/f8a5567f-37da-4ff0-ae7a-172fea688705" />
<img width="817" height="547" alt="Screenshot 2026-03-09 111818" src="https://github.com/user-attachments/assets/dc9fc5b8-5f19-444d-9f9d-4e500e6b2ab0" />
<img width="805" height="552" alt="Screenshot 2026-03-09 111824" src="https://github.com/user-attachments/assets/d157565b-6a36-4172-bba1-2c670354b993" />

# ----------------------------------------
# Step 7: Displot for Univariate Distribution
# ----------------------------------------
sns.displot(data["Age"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Age Distribution")
plt.show()

sns.displot(data["Fare"], kde=True, height=4, aspect=1.5)
plt.title("Displot - Fare Distribution")
plt.show()
<img width="806" height="547" alt="Screenshot 2026-03-09 112102" src="https://github.com/user-attachments/assets/2e33605b-d374-42ff-a663-855da4f4bdfa" />
<img width="809" height="553" alt="Screenshot 2026-03-09 112109" src="https://github.com/user-attachments/assets/66e5232e-cf6e-4e01-bc4b-fbb6cf10be8f" />

# ----------------------------------------
# Step 8: Cross Tabulation
# ----------------------------------------
print("\nCross Tabulation: Sex vs Survived\n")
print(pd.crosstab(data["Sex"], data["Survived"]))

print("\nCross Tabulation: Pclass vs Survived\n")
print(pd.crosstab(data["Pclass"], data["Survived"]))

<img width="416" height="388" alt="Screenshot 2026-03-09 112206" src="https://github.com/user-attachments/assets/66cfa100-1ab8-4a24-832b-745fe82842b5" />

# ----------------------------------------
# Step 9: Heatmap for Correlation Analysis
# ----------------------------------------
plt.figure(figsize=(8,6))
correlation_matrix = data.select_dtypes(include=np.number).corr()
sns.heatmap(correlation_matrix, annot=True, cmap="coolwarm")
plt.title("Correlation Heatmap - Titanic Dataset")
plt.show()

<img width="899" height="736" alt="Screenshot 2026-03-09 112242" src="https://github.com/user-attachments/assets/64094582-9694-4d43-9af9-8cabddfddb8d" />

~~~
# RESULT
    Thus we have performed Exploratory Data Analysis on the given data set.
