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

# Coding and Output
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
data = pd.read_csv("/content/SAMPLEIDS.csv")
data.head()
```

![328031641-c3cfdaef-729a-4e01-987f-c07f055b6097](https://github.com/Swetha733N/exno1/assets/122199934/f7527b66-a5d9-4014-bb86-0fe39e9fdd49)


```
data.isnull().sum()
```
![328031654-07839fb5-b540-40da-8b00-37f26b1269df](https://github.com/Swetha733N/exno1/assets/122199934/95961173-c24a-4259-a2ca-35ae3aafc4c9)

```
columns_with_null = data.columns[data.isnull().any()]
import seaborn as sns
plt.figure(figsize=(10,10))
sns.barplot(columns_with_null)
plt.title("NULL VALUES")
plt.show()
```
![328031663-b1edc442-94f5-44c1-80ba-110843e2d764](https://github.com/Swetha733N/exno1/assets/122199934/2590a6f6-bffc-4e8b-be7e-4773961ffdbd)


```
median = data[column].median()
data[column].fillna(median, inplace=True)
data.isnull().sum().sum()
```

![328031682-97e8461a-8aa4-4218-9ca1-cefa64aaed70](https://github.com/Swetha733N/exno1/assets/122199934/3292ce83-2456-4824-8d15-893ea7223bd8)


```
import pandas as pd
import seaborn as sns
ir = pd.read_csv("/content/iris.csv")
ir.head()
```

![328031704-d166387a-6b8c-4980-bc26-b4f7903473fb](https://github.com/Swetha733N/exno1/assets/122199934/3a19592c-341d-42fc-8385-23a47468b587)


```
ir.describe()
```

![328031722-2c53c970-ffe8-4999-adec-cc237c28c104](https://github.com/Swetha733N/exno1/assets/122199934/079ec807-4a1d-419d-8bf2-dff8d1af08ed)

```
sns.boxplot(x='sepal_width',data=ir)
```

![328031736-75e10a75-59c4-4cef-85c7-7806b61f5ac6](https://github.com/Swetha733N/exno1/assets/122199934/b93d3b38-3b56-43a9-b5f1-5048c3d340c0)


```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```

![328031759-b8780026-b359-470a-b38a-bf41876132bd](https://github.com/Swetha733N/exno1/assets/122199934/3200b1c5-c244-4da8-ae45-19fef275ac9a)


```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```

![328031770-a30e69d4-2c6a-4dd4-b5ff-e05cba073877](https://github.com/Swetha733N/exno1/assets/122199934/baebdc1f-3e6f-4cf5-abf3-b4b9d0a3b2a1)


```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```

![328031790-fd3decd6-f88c-4918-804d-47e67ec47413](https://github.com/Swetha733N/exno1/assets/122199934/27bf6bbf-f5a7-40a8-82d7-9c3e0582d133)


```
sns.boxplot(x='sepal_width',data=delid)
```
![328031802-d87bc370-90e3-496e-8f65-00537e7da6c3](https://github.com/Swetha733N/exno1/assets/122199934/091dae6c-ecf6-4c20-ab84-541e26278abd)


```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("/content/heights.csv")
dataset
```

![328031814-854b68a0-eb20-4888-9e0f-f49b36c829a8](https://github.com/Swetha733N/exno1/assets/122199934/c2450932-e252-44ad-aa71-f20af49b4408)


```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```

```
iqr = q3-q1
iqr
```

![328031829-f00e0e01-b651-47de-9ed8-9a829f11ca91](https://github.com/Swetha733N/exno1/assets/122199934/90295f76-4e91-4805-b9ad-72b5a9791030)


```
low = q1 - 1.5*iqr
low
```
![328031848-0982c2b2-066d-4a51-859e-504bbaf9aa90](https://github.com/Swetha733N/exno1/assets/122199934/8c1accdc-21ac-4862-8904-a4318759ad55)

```
high = q3 + 1.5*iqr
high
```

![328031867-46626b10-2a30-4ee4-92d2-ba5180ab1dd1](https://github.com/Swetha733N/exno1/assets/122199934/a75a8e88-1293-447f-a4c0-a8d0bc1338a2)


```
df.duplicated()
```
![328031912-55921ef3-d88a-4e42-993b-14f6eb97dd65](https://github.com/Swetha733N/exno1/assets/122199934/fdca7e7c-82bd-484f-a293-b6c6372716d5)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```

![328031927-793e3f4b-c4e7-43e7-bc82-1120d819cb04](https://github.com/Swetha733N/exno1/assets/122199934/aca781d7-28db-4b52-b6ff-c3704851b712)


```
z = np.abs(stats.zscore(df['height']))
z
```

![328031943-07ab8105-8d9c-49f7-b8f6-df8d966ba14b](https://github.com/Swetha733N/exno1/assets/122199934/1029b5ef-7d0f-4f66-a5f3-3e1614b92f97)

# Result
Thus the outliers are detected and removed in the given file and the final data set is saved into the file.
