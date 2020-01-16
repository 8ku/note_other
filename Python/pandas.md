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
  city_housing_dataframe.describe() #show results
  ```

  