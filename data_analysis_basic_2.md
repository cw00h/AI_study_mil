# Python Data Analysis Basic

## 2️⃣ Basics of pandas

### What is pandas?
**pandas** is a library designed based on **NumPy**, which can effectively process and store structured data.

### Series
Enhanced version of Numpy's array. Series have both Data and Index.   
Series holds values in form of **ndarray**.

```python
import pandas as pd
data = pd.Series([1, 2, 3, 4])
print(data)

# 0    1
# 1    2
# 2    3
# 3    4
# dtype: int64

print(type(data)) # <class 'pandas.core.series.Series'>
print(data.values) # [1 2 3 4]
print(type(data.values)) # <class 'numpy.ndarray'>

data = pd.Series([1, 2, 3, 4], dtype = "float") # You can designate type of Series using "dtype" parameter
print(data.dtype) # float64

data = pd.Series([1, 2, 3, 4], index = ['a', 'b', 'c', 'd'])
data['c'] = 5 #You can designate index and access items by using the index

population_dict= {
    'china': 141500,
    'japan': 12718,
    'korea': 5180,
    'usa': 32676
}
population = pd.Series(population_dict) #You can create Seriers using Dictionary
```

### DataFrame

Data of multiple **series** gathered in rows and columns.

```python
population_dict= {
    'china': 141500,
    'japan': 12718,
    'korea': 5180,
    'usa': 32676
}
population = pd.Series(population_dict)

gdp_dict= {
    'china': 1409250000,
    'japan': 516700000,
    'korea': 169320000,
    'usa': 2041280000,
}
gdp= pd.Series(gdp_dict)

country = pd.DataFrame({
    'gdp': gdp,
    'population': population
})
print(country)
#              gdp  population
# china  1409250000      141500
# japan   516700000       12718
# korea   169320000        5180
# usa    2041280000       32676

#You can also create DataFrame using Dictionary.
data = {
    'country': ['china','japan','korea','usa'],
    'gdp': [1409250000,516700000, 169320000, 2041280000],
    'population': [141500,12718, 5180, 32676]}
}
country = pd.DataFrame(data)
country = country.set_index('country')

print(country.shape) # (4, 2)
print(country.size) # 8
print(country.ndim) # 2
print(country.values) 
# [[1409250000     141500]
#  [ 516700000      12718]
#  [ 169320000       5180]
#  [2041280000      32676]]

# Defining name of DataFrame's index & column
country.index.name = "Country"
country.columns.name = "Info"

print(country.index)
# Index(['china', 'japan', 'korea', 'usa'], dtype='object', name='Country’)
print(country.columns)
# Index(['gdp', 'population'], dtype='object', name='Info')

#Saving & Loading DataFrame
country.to_csv("./country.csv")
country = pd.read_csv("./country.csv")
```

### Dealing with datas in DataFrame

#### .loc
```python
# Indexing using .loc
country.loc['china']
# gdp           1409250000
# population        141500
# Name: china, dtype: int64

# Slicing using .loc
country.loc['japan':'korea', :'population']
# gdp  population
# japan  516700000       12718
# korea  169320000        5180
```

#### .iloc
```python
# Indexing using .iloc
country.iloc[0]
# gdp           1409250000
# population        141500
# Name: china, dtype: int64

# Slicing using .iloc
country.iloc[1:3, :2]
# gdp  population
# japan  516700000       12718
# korea  169320000        5180
```

#### Selecting Columns   

You can select columns using **column's name**.
```python
country['gdp'] # -> returns Series
# china    1409250000
# japan     516700000
# korea     169320000
# usa      2041280000
# Name: gdp, dtype: int64

country[['gdp']] # -> This is fancy indexing, so it returns DataFrame
# gdp
# china  1409250000
# japan   516700000
# korea   169320000
# usa    2041280000
```

#### Using **Masking** & **query** to select row
```python
country[country['population'] < 10000] # Using Masking
# gdp  population
# korea  169320000        5180

country.query("population > 100000") # Using query
# gdp  population
# china  1409250000      141500
```
#### Using **numerical operators** on columns   

You can use **numerical operators** on Series like numpy array.
```python
gdp_per_capita = country['gdp'] / country['population']
# china     9959.363958
# japan    40627.457147
# korea    32687.258687
# usa      62470.314604
# dtype: float64
```

#### Adding new column   

You can add new column by assigning Series like below.
```python
country['gdp per capita'] = gdp_per_capita
# gdp  population  gdp per capita
# china  1409250000      141500     9959.363958
# japan   516700000       12718    40627.457147
# korea   169320000        5180    32687.258687
# usa    2041280000       32676    62470.314604
```

#### Adding data & Editing data in DataFrame

```python
df = pd.DataFrame(columns = ['이름', '나이', '주소']) #Create DataFrame

# Adding & Editing data
df.loc[0] = ['길동', '26', '서울'] #Adding data using List
df.loc[1] = {'이름':'철수', '나이':'25', '주소':'인천'} #Adding data using Dictionary
df.loc[1, '이름'] = '영희' #Editing data
# 이름  나이  주소
# 0  길동  26  서울
# 1  영희  25  인천

# Adding new column initialized as NaN
df['전화번호'] = np.nan # Adding new column & initializing it as NaN
df.loc[0, '전화번호'] = '01012341234' # Editing data
# 이름  나이  주소         전화번호
# 0  길동  26  서울  01012341234
# 1  영희  25  인천          NaN
```

#### .drop: *Deleting column*

If the value of **axis** is 1, drop deletes **column**, and drop deletes **row** if axis is 0.   
If the value of **inplace** is True, drop changes original, and if it is false, drop doesn't change the original.
```python
df.drop('전화번호', axis = 1, inplace = True)
# 이름  나이  주소
# 0  길동  26  서울
# 1  영희  25  인천
```
