---
draft: false
title: "pandas string methods"
date: 2019-01-08
slug: pandas-string-methods
categories:
  - data science
tags:
  - pandas
---

This blog post is based on [lesson 12 ("How do I use string methods in 
pandas?")](https://www.youtube.com/watch?v=bofaC0IckHo&list=PL5-da3qGB5ICCsgW1MxlZ0Hq8LL5U3u9y&index=12) 
from [Data School](https://www.dataschool.io/)'s 
[pandas video series](https://www.dataschool.io/easier-data-analysis-with-pandas/).

## pandas has many string methods available on a Series via `.str.some_method()`
For example:
- `df.series_name.str.upper()` changes all the strings in the Series called 
`series_name` (in the DataFrame called `df`) to uppercase
- `df.series_name.str.title()` changes the strings to title case (first 
character of each word is capitalized)
- String methods on a Series return a Series. In the case of 

  ```python
  df.series_name.str.contains('bar')
  ```

  the `.contains()` method returns a Series of `True`s and `False`s, in which 
  `True` is returned if the string in the Series `series_name` contains `bar` 
  and `False` is returned if the string in the Series `series_name` does not 
  contain `bar`.
- You could easily use the `True`/`False` Series returned by the `.contains()` 
method above to filter a DataFrame. For example:
  
  ```python
  df[df.series_name.str.contains('bar')]
  ```
  
  will return a new DataFrame filtered to only those rows in which the 
  `series_name` Series (aka the column called `series_name`) contains the 
  string `bar`.

You can see all of the `str` methods available in the 
[pandas API reference](https://pandas.pydata.org/pandas-docs/stable/api.html#string-handling).

## String methods can be chained together
For example:

```python
df.series_name.str.replace('[', '').str.replace(']', '')
```

will operate on the Series called `series_name` in the DataFrame called `df`.
The first `.replace()` method will replace `[` with nothing and the second
`.replace()` method will replace `]` with nothing, allowing you to remove 
the brackets from the strings in the Series.

## Many pandas string methods accept regular expressions
The two chained `.replace()` methods in the previous example can be replaced 
with a singular regex `.replace()`, like this:

```python
df.series_name.str.replace('[\[\]]', '')
```

Here, the `.replace()` method is taking the `regex` string 

```python
'[\[\]]'
```

and replacing with nothing. That regular expression can be deconstructed as 
follows:

- the outer brackets `[` and `]` define a character class, meaning that any 
of the characters within those character class brackets will be replaced
- inside the outer brackets is `\[\]`. It represents the two characters 
`[` and `]` which will be replaced. However, since brackets have a special 
meaning in regular expressions, they need to be escaped with backslashes `\ `. 
So the bracket characters to be replaced end up looking like this: 

  ```python
  \[\]
  ```

You can see working code for all of the above examples in my 
[Jupyter notebook](https://github.com/sethschori/jupyter/blob/master/12_string_methods_in_pandas.ipynb)