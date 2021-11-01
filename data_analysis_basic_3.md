# Python Data Analysis Basic

## 3️⃣ Intensive contents of pandas

### Dealing with data in DataFrame

#### .sort_index: *Sorting DataFrame based on index*

If the value of axis is 0, sort_index sorts DataFrame based on row's index, and if it is 1, sort_index sorts DataFrame based on column's index.
```python
df = df.sort_index(axis = 0)
df = df.sort_index(axis = 1, ascending = False) # You can sort whether in ascending or descending order
```
