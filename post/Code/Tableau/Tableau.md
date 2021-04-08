# Tableau

* TOC
{: toc}

## 日期

### 显示当月

```sql
if DATEDIFF('month',[日期],{MAX([日期])}) <= 0
then "当月"
ELSE "非当月"
END
```




