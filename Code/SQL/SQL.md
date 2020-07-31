# SQL Tips

## 正则 Regular Expression

- 转换字段类型

  ```sql
  select label_name,(case goal_value when '' then 0 else cast (goal_value as decimal) end ) 
  from label_goal_value as gv
  --使用case写判断，把字符串形式的goal_value转换成decimal型
  ```

  

- 字段拼接

  ```sql
  --select concat_ws('连接符'，连接字段，连接字段) as a
  SELECT CONCAT_WS("-", "SQL", "Tutorial", "is", "fun!") AS a;
  --output:SQL-Tutorial-is-fun!
  ```

  

- 包含

  ```sql
  select select * from file where name ~'something|somethingelse'
  ```

  

- 排除包含字符串 NOT REGEXP（MYSql）

  ```mysql
  select * from file where name NOT REGEXP 'something|somethingelse'
  ```

  

## 其他

- 日期范围,如果只写日期,不写时间,只到27日0点0分,如果需要统计到27号一整天,日期往后写一天即可

  ```sql
  SELECT * FROM wechat_record WHERE create_time BETWEEN '2020-02-01' and '2020-02-27'
  ```

  