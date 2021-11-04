# Python Data Analysis Practice

## 2️⃣ Advanced contents of python

### lambda function

#### what is lambda?

**lambda** function is anonymous functions that can be created and used at runtime.

```python
def square(x):
    return x * x
    
square = lambda x: x * x
```

You can simplify codes by using lambda functions.

```python
# This code
def get_eng_title(row):
    split = row.split(',')
    return split[1]
    
sorted(movies, key=get_eng_title)

# is same with below :

sorted(movies, key=lambda row: row.split(',')[1])
```

### assert()

**assert** occurs AssertError unless the following condition is True.

```python
assert(1 == 2) # -> AssertError occurs
```

### map()

```python
def get_eng_title(row):
    split = row.split(',')
    return split[1]
    
eng_titles = [get_eng_title(row) for row in movies]

# The code below is almost the same as the code above
# Note that map is not used like 'movies.map(get_eng_title)'!

eng_titles = map(get_eng_title, movies)

# You can use lambda function with map like this :
eng_titles = map(lambda row : row.split(',')[1], movies) 

# But, if you print eng_titles, you can't get the whole array but 'map' object :
print(eng_titles) # <map object at 0x104154f98>

# This is because python calculates each items of eng_titles only when it's required.
print(eng_titles[0]) # python calculates eng_titles[0] at this line, not at the line above.
```

### filter()

```python
words = ['real', 'man', 'rhythm', ...]
r_words = [word for word in words if word.startswith('r')]

# The code below is almost the same as the code above

r_words = filter(lambda word : word.startswith('r'), words)

# But, like map, python doesn't calculate the whole result at the line above.
print(r_words) # <filter object at 0x104154f98>
```
