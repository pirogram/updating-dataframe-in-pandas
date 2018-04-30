code: add-update-remove-columns
title: Add/Update/Remove Columns
--- |

  One of the common operation in data cleaning phase is mutating columns. We either transform the values of a column (e.g. change _Fahrenheit_ to _Celsius_) or create new columns from the values of an existing one (e.g. extract hashtags from tweets). Some times, we can also delete a column from the `DataFrame`.

  For the purpose of illustrating the operations, we'll use a very simple and small dataset: [temperature.csv](assets/data/temperature.csv). This is how it looks like:

  | city          | max_temp | min_temp |
  |---------------|----------|----------|
  | San Francisco | 105      | 25       |
  | San Diego     | 125      | 40       |
  | Los Angeles   | 115      | 35       |
  | Santa Barbara | 112      | 33       |
  | San Jose      | 110      | 30       |

  ## Updating a Column

  We can start with loading the dataset:

---
type: live-code
id: 1
code: |
  import pandas as pd
  df = pd.read_csv('assets/data/temperature.csv')
  df
--- |

  In the current dataset, temperature is recorded as _Fahrenheit_. Let's say, we prefer to work with _Celsius_. The following code would give us a `Series` with `max_temp` in celsius:

---
type: live-code
id: 2
code: |
  max_temp_celsius = (df['max_temp'] - 32) * 5/9
  max_temp_celsius
--- |

  We can now overwrite the existing `max_temp` column in our `DataFrame` with the new series `max_temp_celsius`:

---
type: live-code
id: 3
code: |
  df['max_temp'] = max_temp_celsius
  df
--- |

  As you can see, `max_temp` column in `df` has the temperature in celsius now. We could have also done it all in a single line:

---
type: live-code
id: 4
code: |
  df['min_temp'] = (df['min_temp'] - 32) * 5/9
  df
--- |

  Now, even `min_temp` column has values in _Celsius_ instead of _Fahrenheit_.

  ## Adding Columns

  Let's say, we want to add another column to our `DataFrame` called `range`. It is the difference between `max_temp` and `min_temp` for a given city. This is how we can add a new column to our `DataFrame`:

---
type: live-code
id: 5
code: |
  df['range'] = df['max_temp'] - df['min_temp']
  df
--- |

  Since, `range` column did not exist in the `DataFrame`, a new column was added.

  ## Broadcasting

  When assigning values to a column, we can also leverage the broadcasting behavior.

---
type: live-code
id: 6
code: |
  df['temp_metric'] = 'Celsius'
  df
--- |

  ## Removing Columns

  Let's say, we are done playing with the `range` column and we would prefer to get rid of it. We can use the `del` keyword to delete a column from `DataFrame`:

---
type: live-code
id: 7
code: |
  del(df['range'])
  df
---
