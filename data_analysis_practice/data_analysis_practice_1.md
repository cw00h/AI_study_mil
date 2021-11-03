# Python Data Analysis Practice

## 1️⃣ String functions

### Basic String functions

#### .startswith()

```python
word = "superman"
print(word.startswith('super')) # True
```

#### .split()
.split  **does not** change original value.

```python
intro = "My name is elice."
print(intro.split()) # ["My", "name", "is", "elice."]

fruits = "Apple,pear,banana"
print(fruits.split(',')) #["Apple", "pear", "banana"]

numbers = "   1    2   3   "
print(numbers.split()) #['1', '2', '3']
print(numbers.split(' ')) # ['', '', '', '1', '', '', '', '2', '', '', '3', '', '', '']
```

#### .lower()

.lower **does not** change original value.

```python
intro = "My name is Elice!"
print(intro.upper()) # "MY NAME IS ELICE!"
print(intro.lower()) # "my name is elice!"
print(intro) # "My name is Elice!"
```

#### .replace()

.replace **does not** change original value.

```python
intro = "My name is Elice."
print(intro.replace('Elice', 'Mike')) # "My name is Mike."
print(intro) # "My name is Elice."
```

## 2️⃣ Data type Conversion

### Dictionary

#### Dictionary vs. List

Dictionary is some kind of **hash table**, so you can find value by key much faster than **List**. 

```python
# {id: name}
accounts = {
    "kdhong.elice" : "Kildong Hong",
    # ...
}

print(accounts["kdhong.elice"])

accounts = [
    ("kdhong.elice", "Kildong Hong"),
    # ...
]

for id_, name in accounts:
    if id_ == "kdhong.elice":
        print(name)
```

#### Key in Dictionary

Key in Dictionary must be **immutable**. (i.e. Tuple, String, ...)

#### in

```python
accounts = {
    "kdhong" : "Kildong Hong"
}
print("kdhong" in accounts) # True
print("cw00h" in accounts) # False
```

#### Iterating Dictionary

Use .items() to converse Dictionary into **array of tuples**.

```python
accounts.items() #[("kdhong", "Kildong Hong")]
for username, name in accounts.items():
    print(username + " - " + name) # kdhong - KildongHong
```

### JSON

JSON means **JavaScript Object Notation**.   
JSON is the most standard way to exchange data in a web environment.

#### Conversion between JSON and Dictionary

Use **loads()** to converse JSON to Dictionary, and use **dumps()** to converse Dictionary to JSON.



