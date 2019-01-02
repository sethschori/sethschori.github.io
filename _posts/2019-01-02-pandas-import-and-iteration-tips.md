---
layout: post
title:  "pandas Import and Iteration Tips"
date:   2019-01-02 10:52:00 -0500
categories: data-science
---
This post is based on my takeaways from a [Q & A video](https://youtu.be/B-r9VuK80dk)
from [Data School](https://www.dataschool.io/).

## Import tips

### Reading only certain columns during import with `usecols` argument
The `usecols` argument can take a list of column names (`str`s) or column 
positions (`int`s). For example:

```python
# column names
foo = pd.read_csv(data_file,
                  usecols=['col_name1', 'col_name2'])
```

```python
# column positions
foo = pd.read_csv(data_file,
                  usecols=[0, 3])
```

### Reading a sample of rows during import with `nrows` argument
The `nrows` argument reads the first n rows of a file. For example, to only 
import the first three rows from a file:

```python
foo = pd.read_csv(data_file,
                  nrows=3)
```

### Importing columns based on data type using `.select_dtypes()`, `include`,  and numpy
The `select_dtypes()` method on a DataFrame allows you to select which 
datatypes you want to keep in a DataFrame. The `include` argument on the 
`select_dtypes()` method indicates which columns you want to include. 
In this example, using numpy allows you to specify `np.number` which includes 
number types `int64`, `float64`, etc.:

```python
import numpy as np
foo = pd.read_csv(data_file)
foo = foo.select_dtypes(include=[np.number])
```

## Iteration tips

### Iteration through a Series
This is incredibly easy, and just like iterating over any iterable in Python.
 For example:

```python
for city in foo.City:  # foo is a pandas DataFrame
    print(city)
```

### Iteration through a DataFrame with `.iterrows()`
Using the DataFrame `.iterrows()` method is similar to `enumerate` in python:

```python
for index, row in foo.iterrows():  # foo is a pandas DataFrame
    print(index, row.City, row.State)
```