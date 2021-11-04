# Machine Learning

## 2️⃣ Understanding Data Types

### Data Types

#### Numerical data & Categorical data
**Numerical data** means data that can be measured numerically. (i.e. weight, height, age)   
**Categorical data** means data that can't be measured numerically. (i.e. gender, blood type)

❗ Note that whether data can be **"expressed"** in numbers does not serve as a criterion for distinguishing categorical data and numerical data.   
For example, gender can be expressed in numbers by expressing men as 1 and women as 0.

#### Categorical data - Ordinal data & Norminal data

- **Ordinal data** means data that has meaning in the order of categories. (i.e. credit(A+, A, A-))

- **Norminal data** means data that there is no meaning in the order of categories. (i.e. blood type (A, B, O, AB))

#### Numerical data - Continuous data & Discrete data

- **Continuous data** means numerical data that can has continuous value. (i.e. height, weight)

- **Discrete data** means countable numerical data. (i.e. number of people)

### Summarizing & Visualizing Categorical data

#### Frequency Table

- **Frequency**: The number of observations in each category.

You can get Frequency fom DataFrame by using **value_counts()**.

```python
# drink
#     Attend Name
# 0        1    A
# 1        0    A
# 2        1    A
# 3        1    A
# 4        1    A
# 5        1    B
# 6        1    B
# 7        1    B
# 8        0    B
# 9        0    B
# 10       0    C
# 11       0    C
# 12       1    C
# 13       1    C
# 14       0    C
# 15       1    D
# 16       0    D
# 17       0    D
# 18       0    D
# 19       1    D
# 20       0    E
# 21       0    E
# 22       0    E
# 23       1    E
# 24       0    E

drink_freq = drink[drink['Attend'] == 1]['Name'].value_counts()
# A    4
# B    3
# D    2
# C    2
# E    1
# Name: Name, dtype: int64
```


- **Relative Frequency**: Frequency / Total number of data. **value_counts(normalize = True)**
- **Frequency Table**: A table listing the category, the frequency corresponding to the category, and the relative frequency.

#### Bar Chart

You can visualize Categorical data by **Bar Chart**.

Use **plt.bar()** to draw bar chart.