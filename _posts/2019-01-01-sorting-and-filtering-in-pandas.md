---
layout: post
title:  "Sorting and filtering in pandas"
date:   2019-01-01 22:22:00 -0500
categories: data-science
---
## Sorting

### Sorting a Series using dot notation
This is a simple as:
```python
foo.col_name.sort_values()
```

To sort in descending order:
```python
foo.col_name.sort_values(ascending=False)
```

Note that the `.sort_values()` method does not change the underlying sort order
. It is a method on a Series that returns a sorted Series.

### Sorting a DataFrame by a single Series
This is even simpler than the first example!

```python
foo.sort_values('col_name')
```

### Sorting a DataFrame by multiple Series
Simply pass a list of the column names you want to sort by:

```python
foo.sort_values(['col_name1', 'col_name2'])
```

## Filtering

### Filtering rows based on a single column criteria

Filtering by a single column criteria is easy in pandas:

```python
foo[foo.col_name >= 42]
```

To understand how this works, please see my 
[Jupyter notebook about filtering](https://github.com/sethschori/jupyter/blob/master/08_filtering_rows_by_column_value.ipynb), 
which is based on 
[Data School's pandas video about filtering](https://www.youtube.com/watch?v=2AFGPdNn4FM&list=PL5-da3qGB5ICCsgW1MxlZ0Hq8LL5U3u9y&index=8).

### Filtering rows based on multiple column criteria

Each criterion must be enclosed in parentheses and chain together with 
either `&` (AND) or `|` (OR). For example:

```python
foo[(foo.col_name1 >= 42) & (foo.col_name2 == 'Bar')]
```

To use multiple OR criteria for the same column, you can use the `isin` 
method. For example:

```python
foo[(foo.col_name1 >= 42) & (foo.col_name2.isin(['Bar', 'Baz', 'Boz']))]
```
