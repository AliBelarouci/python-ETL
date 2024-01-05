## Introduction¶

Many countries speak Arabic; however, each country has its own dialect, the aim of this task is to build a model that predicts the dialect given the text.

## Guidelines

- You are given a dataset which has 2 columns, id and dialect.
- Target label column is the “dialect”, which has 18 classes.

* The “id” column will be used to retrieve the text, to do that, you need to call this API by a POST request. https://recruitment.aimtechnologies.co/ai-tasks
* The request body must be a JSON as a list of strings, and the size of the list must NOT exceed 1000.
* The API will return a dictionary where the keys are the ids, and the values are the text, here is a request and response sample.

## ETL Preparation

**What's ETL ? It's a generic term for moving data one place to another place**

ETL stands for ;

- Extract

- Transform

- Load

## 1. Import Python libraries

```python
import pandas as pd
import numpy as np
import requests
import json
import re
```

## 2. Extracting data

The first step in an ETL pipeline is extraction. Data comes in all types of different formats, csv files, json files, xml files, SQL databases, and the web.

Here, I will do both extracting data from csv files and using APIs

- Load dialect_dataset.csv into a dataframe and inspect the first few lines.
- Load messages.csv to get this dataset run the code in request.py

**Load** dialect_dataset.csv

```python
dialect_dataset =  pd.read_csv("./dialect_dataset.csv")
dialect_dataset
```

### 2. Transform

The second step in an ETL pipeline is Transformation. Transformation usually involves many processes,like;

- combining data
- cleaning data
- working with encodings
- removing duplicate rows
- create dummy variable

**Duplicated**

- Check how many duplicates are in this dataset.
- Drop the duplicates.
- Confirm duplicates were removed.

```python
dialect_dataset.duplicated().sum()
```

**Categorical Variable**
Machine learning models require all input and output variables to be numeric.This means that if your data contains categorical data, you must encode it to numbers before you can fit and evaluate a model.

**pd.get_dummies()**

- pros
  - performs dummy encoding in a single line of code.
  - it returns a pandas data frame with clean column names.
- cons
  - It cannot learn the characteristics from the training data and hence is unable to propagate its findings onto the test dataset.
  - If the total number of unique values in a categorical column is not the same for my train set vs test set, you’ll get errors.In other words,if The categorical feature of the training data dosn't have the same feature of the test data may or may not have all the feature values, which may cause data mismatch issues while modeling.
  ```python
  dialect_dataset = pd.get_dummies(data=dialect_dataset, columns=['dialect'])
  dialect_dataset
  ```
