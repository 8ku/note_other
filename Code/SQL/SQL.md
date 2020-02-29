# SQL Tips

## 正则 Regular Expression

- 排除包含字符串 NOT REGEXP

  ```sql
  select * from file where name NOT REGEXP 'something'
  ```

  

## 其他

- 日期范围,如果只写日期,不写时间,只到27日0点0分,如果需要统计到27号一整天,日期往后写一天即可

  ```sql
  SELECT * FROM wechat_record WHERE create_time BETWEEN '2020-02-01' and '2020-02-27'
  ```

  