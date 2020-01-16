# Padas

## DataFrame and Series

- DataFrame：类似关系型数据表，包含行和列

- Series：单一列，DataFrame 中包含一个或多个Series，每个Serise 有一个名称

  ```python
  pd.Series(['a','b','c'])
  ```

  ```python
  city_names = pd.Series(['a','b','c'])
  population = pd.Series([10,11,12])
  
  pd.DataFrame = ({ 'a':city_names, 'b':population })
  ```

- sometimes, you would like to load a file into DataFrame, you could do this like:

  ```python
  city_housing_dataframe = pd.read_csv("path", sep = ",")
  city_housing_dataframe.describe() #show statistics
  ```

- show head

  ```python
  city_housing_dataframe.head()
  ```

- show graphic

  ```python
  city_housing_dataframe.hist('column name') #hist:直方图
  ```

- [访问数据](https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html)

## [NumPy](https://numpy.org/devdocs/)

用于进行科学计算的工具包。

