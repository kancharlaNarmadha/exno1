# Exno:1 Data Cleaning and Outlier Detection & Removal


# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
## STEP 1: Read the given Data

## STEP 2: Get the information about the data

## STEP 3: Remove the null values from the data

## STEP 4: Save the Clean data to the file

## STEP 5: Remove outliers using IQR

## STEP 6: Use zscore of to remove outliers

# Coding and Output
# Data cleaning
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![image](https://github.com/user-attachments/assets/33fd269c-57d3-439d-bd47-f73261761cda)

```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/d5c0ab6d-b48e-492d-9f0c-edb7734ffa9b)
```
df.isnull().any()
```
![image](https://github.com/user-attachments/assets/4b93b23a-e7a7-47fd-b6ac-2268be000754)

```
df.dropna()
```
![image](https://github.com/user-attachments/assets/4d84a8fe-013e-4607-8c04-f315efd4fc23)

```
df.fillna(0)
```
![image](https://github.com/user-attachments/assets/99ee70a7-422c-4fdf-8409-45d2a2b968e6)
```
df.fillna(method = 'ffill')
```
![image](https://github.com/user-attachments/assets/88f2c98a-5dd6-4f3d-baed-524b9392cb46)

```
df.fillna(method ='bfill')
```
![image](https://github.com/user-attachments/assets/8f920355-eaca-4789-b0d6-7b9e14c678be)
```
df_dropped = df.dropna()
df_dropped
```
![image](https://github.com/user-attachments/assets/1c425a62-cd3a-487c-a10d-bfaf12c44604)

# IQR(Inter Quartile Range)
```
import pandas as pd
ir=pd.read_csv("/content/iris.csv")
ir
```
![image](https://github.com/user-attachments/assets/0dad9f70-f216-4bc5-b993-af18a21323cf)
```
ir.describe()
```
![image](https://github.com/user-attachments/assets/6ce17986-1734-4186-878a-ebc102965ecf)
```
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
```
![image](https://github.com/user-attachments/assets/1f52a30a-a88c-41a2-b0ff-f8ef2e9782fb)

```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
print(c3)
```
![image](https://github.com/user-attachments/assets/f0602676-54ad-431a-b3c1-139d174a5024)
```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![image](https://github.com/user-attachments/assets/09fc0bdf-7446-4d1a-bd68-88e268b1d468)
```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/user-attachments/assets/a8836e61-4c4b-40ed-8f45-3f0f8ad135c4)
```
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/user-attachments/assets/931e260c-8cba-4215-9de5-4e5bf0fb8a44)

# Z-Score

```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```
![image](https://github.com/user-attachments/assets/415c3def-78b8-49a3-8bf2-dba2b652a1e5)
```
df = pd.read_csv("/content/heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```
![image](https://github.com/user-attachments/assets/58d5e26c-f112-437a-9c86-a694b6ad975c)
```
low = q1 - 1.5*iqr
low
```
![image](https://github.com/user-attachments/assets/ccb9af50-5150-4030-844c-7ad23724e0a2)
```
high = q3 + 1.5*iqr
high
```
![image](https://github.com/user-attachments/assets/83b0a8a6-4f5c-4824-a7c6-d5f209614370)
```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![image](https://github.com/user-attachments/assets/ef28106e-ff5b-4107-80f4-d638ee00c6fa)
```
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/user-attachments/assets/0ba8233b-ad63-4044-abd6-8652bceece98)
```
df1 = df[z<3]
df1
```
![image](https://github.com/user-attachments/assets/cd1f59f5-706f-40ee-a4df-d54a216d9d5c)


# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
