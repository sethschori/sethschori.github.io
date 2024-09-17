---
draft: false
title: "Renaming and Removing Columns in pandas DataFrames"
date: 2019-01-01
slug: renaming-and-removing-columns
categories:
  - data science 
tags:
  - pandas
---

## Renaming columns
Four methods for renaming columns in a pandas DataFrame:

### 1. Rename specific columns
 
`foo.rename(columns={}, inplace=True)`

Pass a dict of columns to be renamed. For example:

```python
foo.rename(columns={'old_col1': 'new_col1',
                    'old_col2': 'new_col2'},
                    inplace=True)
```

### 2. Rename all the column names

Set `.columns` to a list of all of the new column names. For example:

```python
foo.columns = ['new_col1', 'new_col2']
```

### 3. Rename the columns when reading in a file

For example:

```python
foo_new_names = ['new_col1', 'new_col2']
foo = pd.read_csv(data_file.csv,
                  names=foo_new_names,
                  header=0)
```

Note that in addition to setting the `names` parameter to a list of the new 
column names, you must also set `header=0` to indicate that you're replacing 
the existing column names in the 0th row (if the 0th row is a header row).

### 4. Replace existing spaces in column names with underscores:

```python
foo.columns = foo.columns.str.replace(' ', '_')
```

## Removing columns (and rows)
Here is the general syntax:

```python
foo.drop(col_str_or_list_of_strs,
         axis=1,  # 0 axis is rows, 1 axis is cols
         inplace=True)
```

to drop a single column:

```python
foo.drop('col_name',
         axis=1,
         inplace=True)
```

to drop multiple columns:

```python
foo.drop(['col1', 'col2'],
         axis=1,
         inplace=True)
```

to drop a single row (data row 0):

```python
foo.drop(0,  # int identifying the data row
         axis=0,
         inplace=True)
```

to drop multiple rows (data rows 1 and 2):

```python
foo.drop([1, 2],  # list of ints identifying the data rows
         axis=0,
         inplace=True)
```