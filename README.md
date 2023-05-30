# Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment


## AIM :

To Perform Data Science Process on a complex dataset and save the data to a file.

## ALGORITHM :

### STEP 1 :

Read the given Data

### STEP 2 :

Clean the Data Set using Data Cleaning Process

### STEP 3 :

Apply Feature Generation/Feature Selection Techniques on the data set

### STEP 4 :

Apply EDA /Data visualization techniques to all the features of the data set

## CODE:

### DEVELOPED BY : ABRIN NISHA A 
### REG NO : 212222230005
```
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
data=pd.read_csv("/content/StudentsPerformance - StudentsPerformance.csv.csv")
print(data)

data.info()

data.isnull().sum()
```

### data cleaning 

```
data['test preparation course']=data['test preparation course'].fillna(data['test preparation course'].mode()[0])
data['math score']=data['math score'].fillna(data['math score']).fillna(data['math score'].mean())
data['writing score']=data['writing score'].fillna(data['writing score']).fillna(data['reading score'].median())

data.isnull().sum()

data.describe()

data.head()
```
### removing outliers
```
Q1=data['math score'].quantile(0.25)
Q3=data['math score'].quantile(0.75)
IQR=Q3-Q1
lower=Q1-1.5*IQR
upper=Q3+1.5*IQR
df=data[(data['math score']>=lower) & (data['math score']<=upper)] 
print(df)   #new dataframe.


outliers=data[(data['math score']<lower) | (data['math score']>upper)] 
print(outliers)

df.shape
```
### Feature generation
```
from sklearn.preprocessing import OrdinalEncoder,LabelEncoder
df1=df.copy()
r=['group A','group B','group C','group D','group E']
enc=OrdinalEncoder(categories=[r])
enc.fit_transform(df1[['race/ethnicity']])
df1['neword1']=enc.fit_transform(df1[['race/ethnicity']])
df1 


df2=df1.copy()
le=LabelEncoder()
df2['neword2']=le.fit_transform(df2['race/ethnicity'])
df2

from sklearn.preprocessing import OneHotEncoder
df3=df.copy()
ohe=OneHotEncoder(sparse=False)
enc=pd.DataFrame(ohe.fit_transform(df3[['lunch']]))
df3=pd.concat([df3,enc],axis=1)
df3.head()

!pip install --upgrade category_encoders
from category_encoders import BinaryEncoder
be=BinaryEncoder()
df4=df.copy()
newdata=be.fit_transform(df4['test preparation course'])
df4=pd.concat([df,newdata],axis=1)
df4.head()
```

### heatmap 
```
data.corr()
plt.subplots(figsize=(7,5))
sns.heatmap(data.corr(),annot=True)
```
### Data visualization

### Scatter plot of math score vs. reading score
```
plt.scatter(data['math score'], data['reading score'])
plt.xlabel('Math Score')
plt.ylabel('Reading Score')
plt.title('Math Score vs. Reading Score')
plt.show()

sns.barplot(x='gender',y='reading score',data=df)

sns.boxplot(x="math score",data=df)
```

## OUTPUT :

### Dataset :

![Screenshot 2023-05-30 185314](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/4a03c31a-3126-484f-96e8-8db466b5902f)

### data.info() :
 
![Screenshot 2023-05-30 185325](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/2e724424-8a1c-4e43-a785-8c5f61845171)

### data.isnull().sum() :

![Screenshot 2023-05-30 185443](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/6af1029c-32a4-43e8-ac66-6d70dfdd8f6c)

### After removing null values :

![Screenshot 2023-05-30 185619](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/2dc5627a-5dda-48ce-97e8-ee43c4a5dbcd)

### data.describe() :
![Screenshot 2023-05-30 185702](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/0fc2360b-b5d3-4498-9ef7-ba5e896a48e1)

### data.head() :

![Screenshot 2023-05-30 185845](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/92fff830-153d-494d-bedd-1042a72b6f61)

### New data after removing outliers :

![Screenshot 2023-05-30 185856](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/e2744dc4-5593-4a0a-a3df-7157c2fe3549)

### Outliers :

![Screenshot 2023-05-30 185909](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/4d9cef8b-bd0e-4eb6-bddd-7361fdfeb160)

### df.shape() :

![Screenshot 2023-05-30 190226](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/9fb2c28a-d082-493c-8fbf-83d62826e21e)

### Ordinal Encoding :

![Screenshot 2023-05-30 190356](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/69939284-4aa1-4fc8-a534-d625e8478685)

### Label Encoding :

![Screenshot 2023-05-30 190417](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/3b0a1a6c-2b31-481a-a769-cd31041c2850)

### OneHot Encoding :

![Screenshot 2023-05-30 190624](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/c05836fd-0907-489d-9702-3ff57a839622)

### Binary Encoding :

![Screenshot 2023-05-30 190635](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/88c2dbe6-ee28-43c3-bca8-3543101c1833)

### Heatmap :

![Screenshot 2023-05-30 190746](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/5d14354a-e37c-4243-8002-ba989a57e356)

### Scatterplot :

![Screenshot 2023-05-30 190820](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/2b3bd6e8-c533-402d-a927-cc4ce110176e)


### Barplot :

![Screenshot 2023-05-30 190839](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/bbfe46b3-8af7-4811-bd82-3c7f615174ee)

### Boxplot :

 ![Screenshot 2023-05-30 190848](https://github.com/Abrinnisha6/Ex-10-Data-Science-Process-on-Complex-Dataset-Assignment/assets/118889454/029d0b3f-907d-421c-946d-603bd2313d88)



## RESULT :


Hence, Data Science Process is performed on a complex dataset and saved the data to a file.





