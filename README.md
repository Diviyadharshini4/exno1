# NAME : A.DIVIYADHARSHINI
# REG NO: 212224040080
# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Import the required Python libraries.

STEP 2: Load the dataset from the CSV file.

STEP 3: Display the dataset details and check for missing values.

STEP 4: Remove duplicate records and fill missing values.

STEP 5: Identify outliers using the IQR method.

STEP 6: Detect outliers using the Z-score method.

STEP 7: Save the cleaned dataset into a new CSV file.

STEP 8: Display the final result and confirm that the dataset is saved successfully.

# Coding and Output
  ```         
import numpy as np
import pandas as pd
from scipy import stats
df=pd.read_csv("Data_set.csv")
print(df.isnull().sum())
cols=['rating','current_overall_rank','watchers']
for col in cols:
    df[col]=df[col].interpolate()
new_cols=['show_name','aired_on','original_network']
for col in new_cols:
    df[col] = df[col].fillna(df[col].mode()[0])
print(df.isnull().sum())

```
<img width="1083" height="447" alt="image" src="https://github.com/user-attachments/assets/026c89a9-e1da-4ca3-9a83-ce136d642f4e" />

```
import pandas as pd
import numpy as np
from scipy import stats

df = pd.read_csv("SAMPLEIDS.csv")

print(df.head())
print(df.shape)
print(df.columns)
print(df.info())
print(df.isnull().sum())
print(df.duplicated().sum())

df = df.drop_duplicates()


for col in df.select_dtypes(include="number").columns:
    if df[col].isnull().any():
        df[col] = df[col].fillna(df[col].median())

for col in df.select_dtypes(include="object").columns:
    if df[col].isnull().any() and not df[col].mode().empty:
        df[col] = df[col].fillna(df[col].mode()[0])

print(df.isnull().sum())

for col in df.select_dtypes(include="number").columns:
    Q1 = df[col].quantile(0.25)
    Q3 = df[col].quantile(0.75)
    IQR = Q3 - Q1
    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR
    outliers = df[(df[col] < lower) | (df[col] > upper)]
    print("\nIQR outliers in", col)
    print(outliers[[col]])

for col in df.select_dtypes(include="number").columns:
    z = np.abs(stats.zscore(df[col], nan_policy="omit"))
    outliers = df[z > 3]
    print("\nZ-score outliers in", col)
    print(outliers[[col]])

df.to_csv("SAMPLEIDS_cleaned.csv", index=False)

print("Cleaned dataset saved successfully!")

```
<img width="945" height="766" alt="image" src="https://github.com/user-attachments/assets/e3482ef6-0c81-41ea-b779-8d8938c061ed" />

<img width="757" height="740" alt="image" src="https://github.com/user-attachments/assets/d1947629-aa1f-41b3-8772-c20fc5a38ed1" />

<img width="710" height="762" alt="image" src="https://github.com/user-attachments/assets/e18716e6-485d-4cd2-a83c-dd7ed77dbc4f" />

<img width="947" height="642" alt="image" src="https://github.com/user-attachments/assets/8c605e90-4d7b-42cd-81ba-ef66508d0e8f" />


```
import pandas as pd
import numpy as np
from scipy import stats

df = pd.read_csv("heights.csv")

print(df.head())
print(df.describe())
print(df.isnull().sum())

for col in df.select_dtypes(include="number").columns:
    Q1 = df[col].quantile(0.25)
    Q3 = df[col].quantile(0.75)
    IQR = Q3 - Q1

    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR

    outliers = df[(df[col] < lower) | (df[col] > upper)]

    print("\nUnusual measurements using IQR in", col)
    print(outliers[[col]])

for col in df.select_dtypes(include="number").columns:
    z = np.abs(stats.zscore(df[col], nan_policy="omit"))
    outliers = df[z > 3]

    print("\nUnusual measurements using Z-score in", col)
    print(outliers[[col]])

```
<img width="715" height="592" alt="image" src="https://github.com/user-attachments/assets/7edafcf1-3ed0-4163-a36e-9a8774aa931e" />

```

import pandas as pd
import numpy as np
from scipy import stats

df = pd.read_csv("iris.csv")

print(df.head())
print(df.describe())

num_cols = df.select_dtypes(include="number").columns

for col in num_cols:
    Q1 = df[col].quantile(0.25)
    Q3 = df[col].quantile(0.75)
    IQR = Q3 - Q1

    lower = Q1 - 1.5 * IQR
    upper = Q3 + 1.5 * IQR

    outliers = df[(df[col] < lower) | (df[col] > upper)]

    print("\nIQR outliers in", col)
    print(outliers[[col]])

for col in num_cols:
    z = np.abs(stats.zscore(df[col], nan_policy="omit"))
    outliers = df[z > 3]

    print("\nZ-score outliers in", col)
    print(outliers[[col]])
    
```
<img width="800" height="752" alt="image" src="https://github.com/user-attachments/assets/d534a222-82fb-403b-8f7c-8c8ae4191ef6" />

<img width="797" height="510" alt="image" src="https://github.com/user-attachments/assets/19e2fff5-2b22-4b71-bf19-093999e652d3" />


```

import pandas as pd

df = pd.read_csv("Loan_data.csv")

print(df.head())
print(df.info())
print(df.isnull().sum())
print(df.duplicated().sum())

df = df.drop_duplicates()

num_cols = ["ApplicantIncome", "CoapplicantIncome", "LoanAmount","Credit_History","Loan_Amount_Term"]
cat_cols = ["Gender", "Married", "Education", "Self_Employed", "Property_Area","Dependents"]

for col in num_cols:
    if col in df.columns:
        df[col] = df[col].fillna(df[col].median())

for col in cat_cols:
    if col in df.columns:
        df[col] = df[col].fillna(df[col].mode()[0])
        df[col] = df[col].str.strip()

print("\nMissing values after cleaning:")
print(df.isnull().sum())

print("\nCleaned dataset:")
print(df.head())

df.to_csv("Loan_data_cleaned.csv", index=False)

print("Cleaned dataset saved successfully!")

```
<img width="1006" height="762" alt="image" src="https://github.com/user-attachments/assets/5f17cdac-bb6f-46d7-8471-f0b7485db435" />

<img width="958" height="737" alt="image" src="https://github.com/user-attachments/assets/7d736dd8-108d-4341-a6f4-8ed4f06779dc" />

<img width="768" height="498" alt="image" src="https://github.com/user-attachments/assets/f98b913c-ae85-439e-9417-3e78cc6a6ae3" />


# summary

In this experiment, I learned how to perform data cleaning using Python and Pandas. I checked the dataset for missing values and duplicate records and handled missing values using the median and mode. I also learned to identify outliers using the IQR and Z-score methods. Finally, I saved the cleaned dataset into a new CSV file. This experiment helped me understand how data cleaning improves data quality and prepares data for further analysis.

# Result

   Thus the given data have been read and performed data cleaning and saved the cleaned data to a file.
