code: partially-updating-a-dataframe 
title: Partially Updating a DataFrame
--- |

  So far, we studied methods to add new columns or overwrite existing ones. There are, however, times when we need to make partial updates to columns. The partial updates may need to be made to one or more columns.

  ## Updating a Slice on list

  Before we look at the ways to partially update a column, let's revisit how we partially update a `list` in Python. Here is an example:

---
type: live-code
id: 1
code: |
  fruits_i_like = ['apple', 'orange', 'banana', 'pineapple']
  fruits_i_like[0] = 'pear'
  fruits_i_like
--- |

  One way to read the second line of this code (`fruits_i_like[0] = 'pear'`) is that you are taking a slice of the list `fruits_i_like` and assigning value `'pear'` to that slice. Since, the slice had only one position to fill, we provided only one value. Here is another example that updates multiple values in the slice:

---
type: live-code
id: 2
code: |
  fruits_i_like = ['apple', 'orange', 'banana', 'pineapple']
  fruits_i_like[0:2] = ['pear', 'grapes']
  fruits_i_like
--- |

  `fruits_i_like[0:2]` is a slice with two positions and hence, when we update the slice, we provide two values.

  ## Updating a DataFrame Slice

  For this example, we'll use a hypothetical [temperature dataset](assets/data/temp-multi-metric.csv). This is what the dataset looks like:

  | city          | max_temp | min_temp | metric |
  |---------------|----------|----------|--------|
  | San Francisco | 105      | 25       | F      |
  | San Diego     | 125      | 40       | F      |
  | Los Angeles   | 115      | 35       | F      |
  | New Delhi     | 37       | 24       | C      |
  | Bombay        | 35       | 20       | C      |

  As you can see, the dataset has temperature recordings in two different metric systems (_Fahrenheit_ and _Celsius_). We would like to convert them (`max_temp` and `min_temp`) to a single metric (_Fahrenheit_).

  Let's first import `pandas` and load our dataset:

---
type: live-code
id: 3 
code: |
  import pandas as pd
  df = pd.read_csv('../assets/data/temp-multi-metric.csv')
  df
--- |

  Next thing is to create a slice of the `DataFrame` so that we have only those observations that were made _Celsius_. For this, we can use the `.loc[]` accessor.

---
type: live-code
id: 4
code: |
  df.loc[ df['metric'] == 'C' ]
--- |

  This slice gave us all the four columns from our `DataFrame`. However, what we ant to change are only the two columns: `max_temp` and `min_temp`. We can use the full syntax of `.loc[]` (i.e. `.loc[rows i want, columns i want]`) for our slice:

---
type: live-code
id: 5
code: |
  df.loc[ df['metric'] == 'C', ['max_temp', 'min_temp'] ]
--- |

  So, we have been able to identify the slice of `DataFrame` we want to work with. Next thing is to simply apply the formula for _Celsius_ to _Fahrenheit_ conversion:

---
type: live-code
id: 6 
code: |
  df.loc[ df['metric'] == 'C', ['max_temp', 'min_temp'] ] * 9/5 + 32
--- |

  Excellent, we have got to the point of taking a slice of values where `metric` is _Celsius_ and converting those values into _Fahrenheit_. Now, all that we need to do is assign it back to the `DataFrame`:

---
type: live-code
id: 7
code: |
  df.loc[ df['metric'] == 'C', ['max_temp', 'min_temp'] ] = \
    df.loc[ df['metric'] == 'C', ['max_temp', 'min_temp'] ] * 9/5 + 32

  df
--- |

  One last remaining thing is to change the `metric` to 'F' since all numbers are in _Fahrenheit_ now. That's as simple as:

---
type: live-code
id: 8
code: |
  df['metric'] = 'F'
  df
---
