code: exercises-1
title: Exercises
---

type: multiple-choice-question
id: 1
question: |
  What can you infer from the following piece of code? Select all that apply.

  ```
  df['col1'] = 5
  ```
options:
  - text: Add a column named `col1` to DataFrame if one doesn't exist.
    correct: true
  - text: Replace a column named `col1` if it already exists in DataFrame.
    correct: true
  - text: Assign value `5` to column `col1` across all the rows.
    correct: true
  - text: Invalid syntax. The right syntax would be `df[ ['col1'] ] = 5`.
  - text: Invalid syntax. The right syntax would be `df['col1'] = [5]`.

---
type: multiple-choice-question
id: 2
question: |
  Consider the following dataset. It has a list of file names and their size.

  File Name | File Size (in GB)
  - | -
  archive-001.tgz | 0.6
  archive-002.tgz | 1.2
  archive-003.tgz | 0.65

  What are the appropriate pieces of code to change the unit of file size to `MB`?
options:
  - text: |
      `df['File Size (in GB)'] = df['File Size (in GB)'] * 1024`
  - text: |
      `df['File Size (in MB)'] = df['File Size (in GB)'] * 1024`
    correct: true
  - text: |
      `df[['File Size (in MB)']] = df[['File Size (in GB)']] * 1024`
    correct: true

---
type: multiple-choice-question
id: 3
question: |
  Consider the following dataset. It has a list of country codes and sales in USD in that country.

  country | sales
  - | -
  USA | 42000
  UK | 50000
  CH | 12000
  IN | 27000

  If we want to add a new column that provides us the %age of sales in each of these countries, which piece of code would we use?
options:
  - text: |
      `df['percentage_sales'] = (100 * df['sales'])/df['sales'].sum()`
    correct: true
  - text: |
      `df['percentage_sales'] = (100 * df['sales'])/df['sales']`
  - text: |
      `df[:, ['percentage_sales']] = (100 * df['sales'])/df['sales'].sum()`
