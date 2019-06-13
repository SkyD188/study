### mysql常用总结

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'd'; 

给d这个用户在，*.*，所有表中的，所有字段，所有的权限

show GRANTs for 'rest_admin'@'%' 查询某个用户的权限

mysqldump -u root -p news > news.sql 导出数据库>导出 <导入

-- 多个字段实现搜索
select username,name from t_student_basic where concat(username,name) like '%罗%' 


create index 索引名称 on 表（表字段）

EXPLAIN  
SELECT 列 FROM 表;
show WARNINGS; -- 数据库调优

FROM_UNIXTIME  -- 时间mysql
substr 
substring 
-- 截取字符，用法不一样，具体百度下
从字符串的第 4 个字符位置开始取，只取 2 个字符。
mysql> select substring('example.com', 4, 2);
```

