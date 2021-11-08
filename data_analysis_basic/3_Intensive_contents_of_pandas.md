# Python Data Analysis Basic

## 3️⃣ Intensive contents of pandas

### Dealing with data in DataFrame

#### .sort_index: *Sorting DataFrame based on index*

If the value of axis is 0, sort_index sorts DataFrame based on row's index, and if it is 1, sort_index sorts DataFrame based on column's index.
```python
df = df.sort_index(axis = 0)
df = df.sort_index(axis = 1, ascending = False) # You can sort whether in ascending or descending order
```

#### .sort_values: *Sorting DataFrame based on columns*

Enter the name of column you want to sort & whether you want to sort it in ascending order.
```python
df.sort_values('col1', ascending = True)
```

You can sort based on several columns.   
At this time, the **previously entered column** is **first used as a criterion** and sorted.
```python
df.sort_values(['col2', 'col1'], ascending = [True, False])
# First, it sorts df based on col2 in ascending order.
# Next, it sorts df based on col1 in descending order.
```

### Functions for analyzing DataFrames - Aggregation functions

#### count: *Checking the number of data*

count checks the number of data **except for NaN** by default.   
count returns **Series**.

```python
data = {
    'korean': [50, 60, 70],
    'math': [10, np.nan, 40]
}
df = pd.DataFrame(data, index = ['a', 'b', 'c'])
# korean  math
# a      50  10.0
# b      60   NaN
# c      70  40.0

df.count(axis = 0) # Count according to column
# korean    3
# math      2
# dtype: int64

df.count(axis = 1) # Count according to row
# a    2
# b    1
# c    2
# dtype: int64
```

#### max, min

max, min **exculdes NaN**, and is **based on column** by default.   
max, min returns **Series** which is of **float64** dtype.

```python
data = {
    'korean': [50, 60, 70],
    'math': [10, np.nan, 40]
}
df = pd.DataFrame(data, index = ['a', 'b', 'c'])
# korean  math
# a      50  10.0
# b      60   NaN
# c      70  40.0

df.max()
# korean    70.0
# math      40.0
# dtype: float64

df.min()
# korean    50.0
# math      10.0
# dtype: float64
```

#### sum, mean

sum, mean **exculdes NaN**, and is **based on column** by default.   
sum, mean returns **Series** which is of **float64** dtype.

```python
data = {
    'korean': [50, 60, 70],
    'math': [10, np.nan, 40]
}
df = pd.DataFrame(data, index = ['a', 'b', 'c'])
# korean  math
# a      50  10.0
# b      60   NaN
# c      70  40.0

df.sum()
# korean    180.0
# math       50.0
# dtype: float64

df.mean()
# korean    60.0
# math      25.0
# dtype: float64
```

You can use **axis**, **skipna** parameter.
```python
df.sum(axis = 1) # -> returns sum of row
# a     60.0
# b     60.0
# c    110.0
# dtype: float64

df.mean(axis = 1, skipna = False) # -> includes NaN
# a    30.0
# b     NaN
# c    55.0
# dtype: float64
```

You can replace NaN to particular value using **fillna**.
```python
B_avg = df['math'].mean()
print(B_avg) # 25.0

# Replace NaN to B_avg
df['math'] = df['math'].fillna(B_avg)

# mean
df.mean(axis = 1, skipna = False)
# a    30.0
# b    42.5 -> no longer returned as NaN
# c    55.0
# dtype: float64
```

### Grouping

#### .groupby
When you want to count based on the conditions, use **.groupby**.
```python
df = pd.DataFrame({
    'data1' : range(6),
    'data2' : [4, 4, 6, 0, 6, 1],
    'key' : ['A', 'B', 'C', 'A', 'B', 'C']
})

# data1  data2 key
# 0      0      4   A
# 1      1      4   B
# 2      2      6   C
# 3      3      0   A
# 4      4      6   B
# 5      5      1   C

df.groupby('key').sum()
# data1  data2
# key              
# A        3      4
# B        5     10
# C        7      7

df.groupby(['key', 'data1']).sum() //you can group by several columns
# data2
# key data1       
# A   0          4
#     3          0
# B   1          4
#     4          6
# C   2          6
#     5          1
```

#### .aggregate

You can use several aggregation functions by once using **.aggregate**.   
.aggregate gets an **array of functions** or **dictionary of column and functions** as arguments, where the basic aggregate functions should be written by their name or their name with quotation marks like **min** or **'min'**, and the functions of numpy should be written with *np.* like **np.median**.   
.aggregate returns **DataFrame**.

```python
df.groupby('key').aggregate(['min', np.median, max])
# data1            data2           
#       min median max   min median max
# key                                  
# A       0    1.5   3     0    2.0   4
# B       1    2.5   4     4    5.0   6
# C       2    3.5   5     1    3.5   6

df.groupby('key').aggregate({'data1': 'min', 'data2' : np.sum}) # returns min for data1 & sum for data2
# data1  data2
# key              
# A        0      4
# B        1     10
# C        2      7
```

#### .filter

Note: At here, **.filter** means *[pandas.core.groupby.DataFrameGroupBy.filter]*(https://pandas.pydata.org/docs/reference/api/pandas.core.groupby.DataFrameGroupBy.filter.html?highlight=filter#pandas.core.groupby.DataFrameGroupBy.filter).

You can filter DataFrame's subgroup according to custom function using **.filter**. The function must return **Boolean**.

```python
def filter_by_mean(x):
    return x['data2'].mean() > 3
    
df.groupby('key').mean()
# data1  data2
# key              
# A      1.5    2.0
# B      2.5    5.0
# C      3.5    3.5

df.groupby('key').filter(filter_by_mean)
# data1  data2 key
# 1      1      4   B
# 2      2      6   C
# 4      4      6   B
# 5      5      1   C
# Items whose key is A were excluded!
```

#### .apply
You can apply custom functions to grouped data by **groupby**.
```python
df.groupby('key').apply(lambda x: x.max() - x.min())
# data1  data2
# key              
# A        3      4
# B        3      2
# C        3      5
```

#### get_group
You can bring data according to key value from grouped data using **get_group**.
```python
df = pd.read_csv("./univ.csv")
df.head() # -> shows top 5 data
# 시도 학교명
# 0     충남      충남도립청양대학
# 1     경기      한국복지대학교
# 2     경북      가톨릭상지대학교
# 3     전북      군산간호대학교
# 4     경남      거제대학교

df.groupby("시도").get_group("충남")
# After grouping according to "시도", return the DataFrame consisting only of items whose "시도" value is "충남".
# 시도 학교명
# 0     충남      충남도립청양대학
# 44    충남      신성대학교
# 60    충남      백석문화대학교
#...

len(df.groupby("시도").get_group("충남")) # 94
```

