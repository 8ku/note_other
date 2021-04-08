# Tips

## Python读取文本文件数据

- 读文本文件格式：`read_csv` , `read_table`

- 读csv时，默认用逗号分隔，不需要用`sep` 指定分隔符 

- 用`read_table` 读取文件必须用`sep`指定分隔符

- 如果用`read_csv` 读非逗号分隔符的文件，必须用 `sep` 指定分隔符，不然读出来的文件不会被分割开

  ```python
  import pandas as pd
  pd.read_csv('path',sep = ',')
  ```

- 读取文本文件时不用 header 和 names 指定表头时，默认第一行为表头

  ```python
  pd.read_csv('path',sep = ',',header = ['x1','x2','x3','x4','x5'])
  ```

- 用`skiprows`跳过指定行

  ```python
  pd.read_csv('path',skiprows = [rowname1,rowname2])
  ```

  

