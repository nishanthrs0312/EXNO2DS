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
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from google.colab import files

uploaded = files.upload()

filename = list(uploaded.keys())[0]
df = pd.read_csv(filename)

print("Original Dataset:")
print(df.head())

print("\nDataset Information:")
print(df.info())

print("\nMissing Values:")
print(df.isnull().sum())


df['Age'] = df['Age'].fillna(df['Age'].median())

df['Embarked'] = df['Embarked'].fillna(df['Embarked'].mode()[0])

if 'Cabin' in df.columns:
    df.drop('Cabin', axis=1, inplace=True)

print("\nDataset after handling null values:")
print(df.isnull().sum())


plt.figure(figsize=(8, 5))
sns.boxplot(x=df['Age'])
plt.title("Boxplot of Age")
plt.show()

plt.figure(figsize=(8, 5))
sns.boxplot(x=df['Fare'])
plt.title("Boxplot of Fare")
plt.show()


Q1 = df['Fare'].quantile(0.25)
Q3 = df['Fare'].quantile(0.75)

IQR = Q3 - Q1

Lower_Bound = Q1 - 1.5 * IQR
Upper_Bound = Q3 + 1.5 * IQR

print("\nLower Bound:", Lower_Bound)
print("Upper Bound:", Upper_Bound)

df = df[(df['Fare'] >= Lower_Bound) & (df['Fare'] <= Upper_Bound)]

print("\nDataset after removing outliers:")
print(df.head())

print("\nDataset Shape:", df.shape)


plt.figure(figsize=(6, 4))
sns.countplot(x='Survived', data=df)
plt.title("Survival Count")
plt.show()

plt.figure(figsize=(6, 4))
sns.countplot(x='Sex', data=df)
plt.title("Gender Count")
plt.show()

plt.figure(figsize=(6, 4))
sns.countplot(x='Pclass', data=df)
plt.title("Passenger Class Count")
plt.show()


sns.displot(data=df, x='Age', kde=True)
plt.title("Age Distribution")
plt.show()

sns.displot(data=df, x='Fare', kde=True)
plt.title("Fare Distribution")
plt.show()


cross_tab = pd.crosstab(df['Sex'], df['Survived'])

print("\nCross Tabulation of Sex and Survived:")
print(cross_tab)


numeric_df = df.select_dtypes(include=np.number)

plt.figure(figsize=(10, 8))
sns.heatmap(numeric_df.corr(), annot=True, cmap='coolwarm', fmt='.2f')

plt.title("Correlation Heatmap")
plt.show()


print("\nFinal Cleaned Dataset:")
print(df.head())

print("\nFinal Dataset Shape:")
print(df.shape)

print("\nEDA COMPLETED SUCCESSFULLY!")

```

<img width="1667" height="830" alt="image" src="https://github.com/user-attachments/assets/25645dac-e89a-4836-b325-8f66e438e251" />
<img width="1572" height="768" alt="image" src="https://github.com/user-attachments/assets/c9086a42-9af4-40f5-90e5-355721669d16" />
<img width="807" height="587" alt="image" src="https://github.com/user-attachments/assets/f655e421-d29e-4d27-936f-15421ead102a" />
<img width="806" height="596" alt="image" src="https://github.com/user-attachments/assets/69fcc0dc-09ee-4376-a483-b9bc882ddb49" />
<img width="696" height="870" alt="image" src="https://github.com/user-attachments/assets/44aa0eed-8e05-4a5a-b3e9-8c848c640811" />
<img width="546" height="778" alt="image" src="https://github.com/user-attachments/assets/cf5c3852-7779-4505-b50c-e2171c684142" />
<img width="412" height="833" alt="image" src="https://github.com/user-attachments/assets/5aa0a4ea-3183-4a8b-8aec-c29e9ba7764b" />
<img width="662" height="660" alt="image" src="https://github.com/user-attachments/assets/82eadba1-4b81-4fee-903c-2f366f78340e" />
<img width="660" height="388" alt="image" src="https://github.com/user-attachments/assets/0cac26c1-7dce-4012-a6a8-348f1629d36a" />



# RESULT

The given Titanic dataset was successfully loaded, cleansed, and analyzed using Python. Missing values were handled using median and mode imputation.Thus, data cleansing, outlier removal, and exploratory data analysis were successfully performed on the dataset.
