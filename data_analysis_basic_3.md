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

