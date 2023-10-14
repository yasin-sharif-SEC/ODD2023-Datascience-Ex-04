# Aim
To read the given data and perform multivariate analysis on them.

# Explanation
This is an another form of data analysis, where the data being analyzed consist of two or more variables.
It involves dealing with numerical and numerical, numerical and categorical, cateegoroical and categorical datas.

# Algorithm
### Step 1
Read the given data.
### Step 2
Remove null values if present.
### Step 3
Using box plot, determine if outliers are present and remove them.
### Step 4
Apply multivariate analysis on suitable columnns in the data.

# Code
```python
import pandas as pd
import numpy as np
import seaborn as sb
import matplotlib.pyplot as plt
from scipy import stats

df3=pd.read_csv('FlightInformation.csv')
df2=pd.read_csv('SuperStore.csv')
df1=pd.read_csv('diabetes.csv')

# diabetes file before cleaning
sb.boxplot(data=df1)
# diabetes file data cleaning
z=np.abs(stats.zscore(df1['Glucose']))
df1c=df1[z<3]
z=np.abs(stats.zscore(df1c['BloodPressure']))
df1c=df1c[z<2]
z=np.abs(stats.zscore(df1c['SkinThickness']))
df1c=df1c[z<3]
z=np.abs(stats.zscore(df1c['Insulin']))
df1c=df1c[z<2]
z=np.abs(stats.zscore(df1c['DiabetesPedigreeFunction']))
df1c=df1c[z<2]
z=np.abs(stats.zscore(df1c['Age']))
df1c=df1c[z<3]
z=np.abs(stats.zscore(df1c['BMI']))
df1c=df1c[z<2]
sb.boxplot(data=df1c)

sb.heatmap(df1c.corr(),annot=True)
sb.barplot(x=df1c['Outcome'],y=df1c['Glucose'])
sb.barplot(x=df1c['Outcome'],y=df1c['Age'])
sb.barplot(x=df1c['Outcome'],y=df1c['BMI'])
plt.figure(figsize=(10,5))
sb.scatterplot(x=df1c['Glucose'],y=df1c['Insulin'],hue=df1c['Outcome'])

# superstore file before cleaning
sb.boxplot(data=df2['Sales'])
# superstore file data cleaning
z=np.abs(stats.zscore(df2['Sales']))
df2c=df2[z<0.8]
sb.boxplot(data=df2c['Sales'])

states=df2c.loc[:,["State","Sales"]]
states=states.groupby(by=["State"]).sum().sort_values(by="Sales")
plt.figure(figsize=(17,7))
sb.barplot(x=states.index,y="Sales",data=states)
plt.xticks(rotation=90)
plt.show()
categ=df2c.loc[:,["Category","Sales"]]
categ=categ.groupby(by=["Category"]).sum().sort_values(by="Sales")
sb.barplot(x=categ.index,y="Sales",data=categ)
region=df2c.loc[:,["Region","Sales"]]
region=region.groupby(by=["Region"]).sum().sort_values(by="Sales")
sb.barplot(x=region.index,y="Sales",data=region)
ship=df2c.loc[:,["Ship Mode","Sales"]]
ship=ship.groupby(by=["Ship Mode"]).sum().sort_values(by="Sales")
sb.barplot(x=ship.index,y="Sales",data=ship)

# flightinformation before cleaning
sb.boxplot(data=df3)
# flightinformation data cleaning
z=np.abs(stats.zscore(df3['Price']))
df3c=df3[z<3]
sb.boxplot(data=df3c)

airline=df3c.loc[:,["Airline",'Price']]
airline=airline.groupby(by=['Airline']).sum().sort_values(by='Price')
sb.barplot(x=airline.index,y='Price',data=airline).set(ylabel='Total Sales')
plt.xticks(rotation = 90)
plt.show()
stop=df3c.loc[:,["Total_Stops",'Price']]
stop=stop.groupby(by=['Total_Stops']).count()
sb.barplot(x=stop.index,y='Price',data=stop).set(xlabel='Total_Stops',ylabel='Count')
```

# Output
### Glucose vs Outcome
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-04/assets/142985837/a946004a-7de4-4a53-a385-ff0575c3adb8)

### Age vs Outcome
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-04/assets/142985837/93181dee-b9ae-4b86-9804-8b911fb8992d)

### BMI vs Outcome
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-04/assets/142985837/40df6453-e9ca-4984-a8a0-c8084ca5e3f2)

### Glucose vs Insulin with Outcome
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-04/assets/142985837/852a6a4b-2af5-422e-9bf2-bcdfbeecdbb6)

### States vs Sales
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-04/assets/142985837/9bfd79cb-dcf7-4928-8a82-b4b85b7bb841)

### Category vs Sales
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-04/assets/142985837/1a92d26e-e66c-498e-a217-3ed94db95717)

### Region vs Sales
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-04/assets/142985837/d79b7827-6bae-45b2-a715-83724e2c51ba)

### Ship mode vs Sales
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-04/assets/142985837/e083391d-67ff-434d-a0c2-ad70562ac2ba)

### Airlines vs Total sales
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-04/assets/142985837/d5e6c52e-e626-4dd6-b31c-bb7b47613116)

### Total stops vs Count
![download](https://github.com/yasin-sharif-SEC/ODD2023-Datascience-Ex-04/assets/142985837/5dd39787-45b0-42ac-8a23-cd6d783b6b62)

# Result
Thus, the given data is read and multivariate analysis is carried on them.


