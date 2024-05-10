# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers


            
# DATA CLEANING
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
data = pd.read_csv("/content/SAMPLEIDS.csv")
data.head()
```
![309139505-87017457-6bc6-447e-b68d-7ce0e74bfdeb](https://github.com/Swetha733N/exno1/assets/122199934/520e5a53-b701-435b-9262-64799b897163)


```
data = pd.get_dummies(data)
data.isnull().sum()
```
![309139475-21080b5a-61e4-4afb-86c4-1784ed9ccad5](https://github.com/Swetha733N/exno1/assets/122199934/70f8484a-a9b8-4b12-b4d4-3fb22dd84e61)


```
columns_with_null = data.columns[data.isnull().any()]
import seaborn as sns
plt.figure(figsize=(10,10))
sns.barplot(columns_with_null)
plt.title("NULL VALUES")
plt.show()
```
![309135329-c97ff983-bca5-401c-bad1-537b54cc593b](https://github.com/Swetha733N/exno1/assets/122199934/32ffd98f-5d53-4c46-ade4-e0020807dbd5)

```
for column in columns_with_null:
    median = data[column].median()  
    data[column].fillna(median, inplace=True)
data.isnull().sum().sum()
```
#IQR
```
import pandas as pd
import seaborn as sns
ir = pd.read_csv("/content/iris (1).csv")
ir.head()
```
![309135437-e0ab58a3-f6c4-4150-9ec1-fc360883f213](https://github.com/Swetha733N/exno1/assets/122199934/04be29ee-8b9c-46b5-b758-2c6880b94206)

```
ir.describe()
```
![309135509-14c52f26-49d7-4773-a3dc-691df7888d24](https://github.com/Swetha733N/exno1/assets/122199934/7be54b9d-0487-492f-a0e9-7bdd9ac0033d)


```
sns.boxplot(x='sepal_width',data=ir)
```
![309135615-3b4d7891-2bb0-4c00-a5f4-02e0be6035f6](https://github.com/Swetha733N/exno1/assets/122199934/35a3dd78-1114-49e9-bd7e-24e4268a475b)

```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![309135740-a525ca98-7554-4860-98cb-b417ec6f6de5](https://github.com/Swetha733N/exno1/assets/122199934/2db9cbc8-7c0a-4b4c-8bb2-e2bf8bf6c419)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```


```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![309135889-8985d070-d77f-4bd7-b9c5-b9f4860ca979](https://github.com/Swetha733N/exno1/assets/122199934/32164cf0-0698-4dcf-a07c-06dd80bdcefd)


```
sns.boxplot(x='sepal_width',data=delid)
```
![309135928-89bb915b-d491-42d2-b988-71cc15bd0a78](https://github.com/Swetha733N/exno1/assets/122199934/e5f848a4-9661-491d-987a-aa6d29bd8550)



# Z SCORE
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```
![309136004-827293f2-76d9-4d1c-a7a3-0c0ea93a0838](https://github.com/Swetha733N/exno1/assets/122199934/4cee25ac-5677-4c52-8866-f80378232e28)


```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```
![309136004-827293f2-76d9-4d1c-a7a3-0c0ea93a0838](https://github.com/Swetha733N/exno1/assets/122199934/807ac824-2934-4cf5-8413-29ce1804c10a)

```
low = q1 - 1.5*iqr
low
```
![307661531-3f341bea-42c2-4cbd-928a-9e1fa576cfaf](https://github.com/aparnabalasubrmanian/exno1/assets/123351172/a62dd212-32e8-4f6e-a9bb-cd4e5be1c40e)
```
high = q3 + 1.5*iqr
high
```
![309136287-74bb2438-286d-417c-9a8f-7511df91f02e](https://github.com/Swetha733N/exno1/assets/122199934/b412f787-e239-4f33-a396-6c0a20781826)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![309136346-e14fa31d-adf2-4da4-aa7f-17beac6b0a1d](https://github.com/Swetha733N/exno1/assets/122199934/0cb37860-64df-46d5-9722-6889dcceb941)

```
z = np.abs(stats.zscore(df['height']))
z
```
![309136397-0bbf349d-f89c-4069-b6dc-bfa65b58d8f1](https://github.com/Swetha733N/exno1/assets/122199934/70dc9fc9-483e-45f3-bcb0-84d54f131bce)



# Result
Thus the outliers are detected and removed in the given file and the final data set is saved into the file.       
