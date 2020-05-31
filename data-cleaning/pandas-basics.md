# 🎉 Key Concept of Pandas

I think in general, a complete genomic data analysis can be divide into three parts: 

1. **Data cleaning**: reform your data into a format that can be the direct input of your analysis steps
2. **Data analysis**: all the fancy computations~
3. **Data visualization**: visualize your computed results, to better tell a story

In practice, these three parts usually intermingled, but the coding / computational knowledge for each part is quite different. Here in this chapter, **we are talking about the data cleaning part**. Data cleaning is probably the most time consuming and tedious step for genomic data analysis. Luckily in python, we have the Pandas package to help with that. Pandas is like the "Excel" of python. It's such a versatile package that can handle anything organized in a tabular format.

I think the best way to learn pandas is through practice. However, let me give you an overview and some learning resources before diving into real coding.

## Learning Resource Recommendation

1. [10 minutes to pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/10min.html), which is from pandas official documentation. This page can give you a minimum introduction to pandas, although it takes more than 10 mins 🤪. 
2. [Python for Data Analysis 2nd version](http://shop.oreilly.com/product/0636920050896.do) \([中文版](https://seancheney.gitbook.io/python-for-data-analysis-2nd/)\). This is my introduction book to pandas, the author is also the original author of the Pandas package. **If you fully understand this book, you are ready for any data cleaning works in python**.
3. [Pandas official documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/index.html). Once you finished 1 and 2, reading the tedious official documentation will further teach you how to write minimum but fastest code to accomplish the jobs. Because you've been prepared with all basic knowledge with pandas, the documentation might be a bit less tedious now.

## Pandas is based on numpy

Numpy is the basic package for almost all data science applications in python. It provides the most fundamental data structure `numpy.ndarray` in python, an N-dimensional array type. While Pandas is a package about upper-level tabular data manipulation, both Series and Dataframe from **pandas use numpy array internally to store the data**. To some extent, Pandas is just like a higher-level wrapper of numpy.

You don't need to know everything about numpy before you start to learn pandas or further analysis, but **keep this dependency relationship in mind** is important. In addition, there are several important notes based on this dependency relationship:

1. Data in Pandas Series or Dataframe all belong to certain **data types** \(int64, float64, object, etc.\). Most of them inherited from numpy since pandas used it to store data. This is numpy [dtypes](https://numpy.org/doc/stable/reference/arrays.dtypes.html) documentation.
2. Many pandas operation also inherited from numpy, for example, how to [use vectorized calculation to replace for-loop](https://www.oreilly.com/library/view/python-for-data/9781449323592/ch04.html) to run faster drastically; how to [use broadcast to simplify code](https://pandas.pydata.org/pandas-docs/stable/getting_started/basics.html#matching-broadcasting-behavior) and also run faster. It's OK if you don't know what these are right now. These are all original numpy functions, but you can also learn it from pandas later. And once you become familiar with pandas, you will also understand most of the numpy grammars!

### My suggestions about the leaning path for pandas + numpy

1. Read a very brief numpy introduction, like Chapter 4 of the Python for Data Analysis book above.
2. Learn pandas first, during learning pandas, if you find any unknown numpy concepts, try to google it to get a basic idea.
3. Once you are most familiar with pandas \(e.g., finish the book above\), congratulations, you are also comfortable with most numpy operations. All you need to do is go through [numpy documentation](https://numpy.org/doc/stable/user/quickstart.html) to learn it systematically. 

## Pandas is all about three data structures

### Series \(1-D\)

Series is a 1-D vector of data, the basic data components of pandas.

Important facts about Series:

* Series has a dtype attribute indicating data types. Usually, series contains certain data with the same data type \(int64, float32, etc.\), but it also supports mixed datatypes through the "object" dtype. Most data types are defined as numpy

```text
In [1]: import pandas as pd

In [2]: int_series = pd.Series([1, 2, 3])

In [3]: int_series
Out[3]:
0    1
1    2
2    3
dtype: int64

In [4]: int_series.dtype
Out[4]: dtype('int64')

In [5]: mix_series = pd.Series([1, 2, '3'])

In [6]: mix_series.dtype
Out[6]: dtype('O')

In [7]: mix_series
Out[7]:
0    1
1    2
2    3
dtype: object

# prove that pandas use numpy to store data
In [9]: int_series.values
Out[9]: array([1, 2, 3])

In [10]: type(int_series.values)
Out[10]: numpy.ndarray
```

* Series has index, which stores a "name" of every value in the series

```text
In [11]: int_series.index
Out[11]: RangeIndex(start=0, stop=3, step=1)

In [12]: int_series.index = ['a', 'b', 'c']

In [13]: int_series
Out[13]:
a    1
b    2
c    3
dtype: int64

In [14]: int_series['a']
Out[14]: 1

```

### Dataframe \(2-D\)

Dataframe is a 2-D table. It is the main entry point of pandas. If you select one row or one column from dataframe, it gives you a Series.

```python
In [15]: df = pd.DataFrame([[1, 2, 3], [4, 5, 6]], 
                           index=['r1', 'r2'], 
                           columns=['c1', 'c2', 'c3'])

In [16]: df
Out[16]:
    c1  c2  c3
r1   1   2   3
r2   4   5   6

# select 1 column give you a Series
In [17]: df['c1']
Out[17]:
r1    1
r2    4
Name: c1, dtype: int64

# select 1 row give you a Series
In [19]: df.loc['r1']
Out[19]:
c1    1
c2    2
c3    3
Name: r1, dtype: int64
```

Important facts about dataframe:

* Dataframe has two indexes. One is for each row names, one is for each column names. They can be accessed like this:

```python
# this is row index
In [20]: df.index
Out[20]: Index(['r1', 'r2'], dtype='object')

# this is column index
In [21]: df.columns
Out[21]: Index(['c1', 'c2', 'c3'], dtype='object')
```

* `Dataframe.dtypes` refer to data type of each column, this is because we **usually** \(but not always\) use rows to represent observations and use columns to represent features. Observation \(like one sample in your experiment\) and have multiple features with different dtypes, but a single feature usually has consistent dtype for all observations. 

```python
In [22]: df.dtypes
Out[22]:
c1    int64
c2    int64
c3    int64
dtype: object
```

### Index \(Name of the values/rows/columns\)

As said above, both Series and Dataframe must have index, it can be meaningful names, or it can be default numbers if names are not provided. **Index is a very important concept in pandas**. It is the most different feature between pandas data structure and python list or numpy array.

A simple index only contains one name per item. However, one can also use combinatorial names to create [MultiIndex for Series or Dataframe](https://pandas.pydata.org/pandas-docs/stable/user_guide/advanced.html#advanced). MultiIndex is a bit more complicated, let's not discuss here. But the basic idea is that **all items in pandas have name\(s\) and the name\(s\) store in the index object.**

## Pandas provide two ways of selecting data

Selecting data from a whole dataframe is a major topic of data cleaning. This [page](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html) from pandas documentation or Chapter 4 of the book above has more detailed discussion and examples of this topic. Here I want to emphasize some key points:

* Pandas support list like slicing to select data - use position \(int number\) and the `iloc` method.

```python
# select a row by posiiton
In [23]: df.iloc[0]
Out[23]:
c1    1
c2    2
c3    3
Name: r1, dtype: int64

# select a column by position
In [26]: df.iloc[:,1]
Out[26]:
r1    2
r2    5
Name: c2, dtype: int64
```

* Because pandas data structures all have indexes, so all of them also support selecting data by name and the `loc` method.

```python
# select a column by name
In [27]: df['c1']  # this is equal to df.loc[:, 'c1']
Out[27]:
r1    1
r2    4
Name: c1, dtype: int64

# select a row by name
In [28]: df.loc['r1']
Out[28]:
c1    1
c2    2
c3    3
Name: r1, dtype: int64
```

* **Most importantly**, pandas support selecting data by a bool vector, which allows you to construct complex filters and apply easily onto your data.

```python
# apply bool list selection to column
In [30]: bool_list = [True, False, False]

In [31]: df.loc[:, bool_list]
Out[31]:
    c1
r1   1
r2   4

In [32]: df.loc['r1', bool_list]
Out[32]:
c1    1
Name: r1, dtype: int64


# create bool series through vecotrized comparison
In [33]: bool_series = df.loc['r1'] > 2

In [34]: bool_series
Out[34]:
c1    False
c2    False
c3     True
Name: r1, dtype: bool

# apply bool series selection onto dataframe columns
In [35]: df.loc[:, bool_series]
Out[35]:
    c3
r1   3
r2   6
```

There are also several other ways to select data. All of them combine allows you to do what every subsetting you want on your data. 

Remembering all these different methods will take some time. It might be frustrated to try and learn at the beginning, this is why we say data cleaning is the most tedious part 😂, but it is also essential, so keep practicing ;\)





