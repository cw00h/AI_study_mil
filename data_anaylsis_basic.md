# Python Data Analysis Basic

## Numpy

### What is Numpy?

Numpy means **Numerical Python**. It is a library that helps to deal with large multi-dimensional arrays in python.   
You can deal with array **without for or while loops**. Numpy supports **fast calculation**, and uses memory more **efficiently** than **python List**.

### Creating an array in Numpy

```python
import numpy as np
np_arr = np.array(range(5))
print(np_arr) # [0 1 2 3 4] -> each items are divided by space!
print(type(np_arr)) #<class 'numpy.nadarray'>
```

### dtype: *Array's data type*

You can only contain items of same type in an array.

```python
arr = np.array([0, 1, 2, 3, 4], dtype=float) #you can designate type of items in the array using 'dtype'
print(arr) #[0. 1. 2. 3. 4.]
print(arr.dtype) #'float64'
print(arr.astype(int)) #[0 1 2 3 4] #You can create new arr casted to different type using 'astype'
```

### ndim & shape: *dimension-related property of ndarray*

```python
list = [0, 1, 2, 3]
arr = np.array(list)
print(arr.ndim) #1
print(arr.shape) #(4,)
```

Notice that shape of ndarray is returned in the form of **tuple**.

```python
list = [[0,1,2],[3,4,5]]
arr = np.array(list)
print(arr.ndim) #2
print(arr.shape) #(2, 3)
print(arr.size) #6 -> number of items in arr
print(len(arr)) #2 -> length of arr

arr.shape = 3, 2 #You can reshape arr by changing arr.shape!
print(arr.shape) #(3, 2)
print(arr.size) #6
print(len(arr)) #3
```

### indexing

```python
x = np.arange(7)
print(x) #[0 1 2 3 4 5 6]
print(x[3]) #3
print(x[7]) # IndexError: index 7 is out of bounds
x[0] = 10
print(x) # [10 1 2 3 4 5 6]
```

```python
x = np.arange(13)
x.shape = 3, 4
print(x)
#[[0 1 2 3]
  [4 5 6 7]
  [8 9 10 11]]
print(x[2, 3]) # 11
```

### slicing

```python
x = np.arange(1, 13, 1)
x.shape= 3, 4
print(x)
# [[ 1  2  3  4]
#  [ 5  6  7  8]
#  [ 9 10 11 12]]
print(x[1:2,:2:3]) # [[5]]
print(x[1:,:2]) # [[ 5  6]
                #  [ 9 10]]
```

### Boolean indexing

```python
x = np.arange(7)

print(x) #[0 1 2 3 4 5 6]

#Boolean mask
print(x < 3) #[True True True False False False False]
print(x > 7) #[False False False False False False False]

#Boolean indexing
print(x[x < 3]) #[0 1 2]
print(x[x % 2 == 0]) #[0 2 4 6]
```

### Fancy indexing 
**Fancy indexing** means passing an **array of indices** to access multiple array elements at once

```python
x = np.arange(7)
print(x) #[0 1 2 3 4 5 6]

print(x[[1, 3, 5]]) # [1 3 5]

x = np.arange(1, 13, 1).reshape(3, 4)
print(x)
# [[ 1  2  3  4]
#  [ 5  6  7  8]
#  [ 9 10 11 12]]

print(x[[0, 2]])
# [[ 1  2  3  4]
#  [ 9 10 11 12]]
  
print(x[[0, 2], [1, 3]])
# [ 2 12]

print(x[0:2, 2])
# [3 7]

print(x[[0,2],2])
# [3 11]

print(x[[0,2], :2])
# [[ 1  2]
#  [ 9 10]]

print(x[1:, [2, 0, 1]])
# [[ 7  5  6]
#  [11  9 10]]
```
