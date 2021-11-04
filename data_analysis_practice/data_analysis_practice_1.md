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

Use .items() to convert Dictionary into **array of tuples**.

```python
accounts.items() #[("kdhong", "Kildong Hong")]
for username, name in accounts.items():
    print(username + " - " + name) # kdhong - KildongHong
```

### JSON

JSON means **JavaScript Object Notation**.   
JSON is the most standard way to exchange data in a web environment.

#### Conversion between JSON and Dictionary

Use **loads()** to convert JSON to Dictionary, and use **dumps()** to convert Dictionary to JSON.

```python
def jsonfile_to_dic(filename):
    with open(filename) as file:
        json_string = file.read()
        
        return json.loads(json_strin)

def dictionary_to_json(dictionary, filename):
    with open(filenamem, 'w') as file:
        file.write(json.dumps(dictionary))
```

### Set

#### Creating Set
```python
set1 = {1, 2, 3}
set2 = set([1, 2, 3])
set3 = {3, 2, 3, 1} # -> {1, 2, 3}
```

#### .add, .update, .remove, .discard
```python
num_set = {1, 3, 5, 7}
num_set.append(9)
num_set.update([3, 15, 4]) # -> append several items
num_set.remove(7) # -> item you want to erase must be in set
num_set.discard(13) # -> if item you want to erase is not in set, discard does nothing.
```

### in, len
```python
num_set = {1, 3, 5, 7}
print(6 in num_set)
print(len(num_set))
```

#### Set Operation

```python
union = set1 | set2
intersection = set1 & set2
diff = set1 - set2
xor = set1 ^ set2
```

### CSV

#### What is CSV?

CSV means **Comma Separated Value**. CSV files store data separated by comma.

```python
# movies.csv
# 국문 제목,영문 제목,개봉 연도
다크나이트,The Dark Knight,2008
겨울왕국,Frozen,2013
슈렉,Shrek,2001
슈퍼맨,Superman,1978
```

Data can be separated by different characters.
```python
다크나이트|The Dark Knight|2008
겨울왕국|Frozen|2013
```

If data contains comma, the data must be enclosed in quotes.

```python
먹고 기도하고 사랑하라,"Eat, Pray, Love",2010
"헬로우, 뉴욕","Hello, New York",2013
```

CSV consumes less capacity than JSON to store the same data.
```python
# movies.csv
아이언맨,Iron Man,2008
겨울왕국,Frozen,2013

#movies.json
[{"ko": "아이언맨", "en": "Iron Man", "year": 2008},
{"ko": "겨울왕국", "en": "Frozen", "year": 2013}]
```
 
#### Reading & Processing CSV

You can use **.reader(filename, delimiter)** to divide the contents of the CSV file by line and separate it based on the delimeter.

```python
import csv

def print_csv(filename):
    with open(filename) as file:
        reader = csv.reader('file, delimiter=',')
        for row in reader:
            # row is an array containing data of the CSV file's one row
            print(row[0])
            print(row[1])
            # ...
```

#### Conversion from CSV to JSON

First, convert CSV to array of dictionary using **csv.reader**.   
Then, use **json.dumps** to convert the array of dictionaries to JSON file.

```python
def CSV_to_JSON(src_file, dst_file):
    arr = []
    with open(src_file) as src:
        reader = csv.reader(src, delimiter=',')
        
        for row in reader:
            data = {
                "a": row[0],
                "b": row[1],
                # ...
            }
            arr.append(data)
    
    with open(dst_file, 'w') as dst:
        dst.write(json.dumps(arr))
```