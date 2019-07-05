### mysql常用总结

```mysql
给d这个用户在，*.*，所有表中的，所有字段，所有的权限
	GRANT ALL PRIVILEGES ON *.* TO 'd'; 

show GRANTs for 'rest_admin'@'%' 查询某个用户的权限

mysqldump -u root -p news > news.sql 导出数据库>导出, <导入

-- 多个字段实现搜索
select username,name from t_student_basic where concat(username,name) like '%dhy%' 

group_concat()　 可以对分组的结果中的某个字段进行字符串连接。结果会用","连接

create index 索引名称 on 表（表字段）

EXPLAIN
SELECT 列 FROM 表;
show WARNINGS; -- 数据库调优

TIMESTAMPDIFF(DAY,time,time) 用来算天 年

date_format()用来修改时间格式
UNIX_TIMESTAMP() -- 转换为时间戳 把date转为时间戳
FROM_UNIXTIME() -- 把时间戳转为date
FROM_UNIXTIME(time,%Y-%m-%d)  -- 时间戳转换为时间 字符串形式 加格式
1970-01-01 08:00:00 时间是从八点开始 这个时间就是计算机规定的0时间
substr 
substring 
-- 截取字符，用法不一样，具体百度下
从字符串的第 4 个字符位置开始取，只取 2 个字符。
mysql> select substring('example.com', 4, 2);

相当于if else
	select (case 字段 when 值 then 值 else 值 end) from 表
	
	case when then else end
select if(username='a',"男","女") as ssva from t_demo

    IF search_condition THEN   
        statement_list    
    [ELSEIF search_condition THEN]    
        statement_list ...    
    [ELSE   
        statement_list]    
    END IF   

select CASE sex WHEN 1 THEN '男' ELSE '女' END as sex from t_name where id = '1'  



where是唯一一个直接从磁盘获取数据的时候就开始判断的条件，从磁盘取出一条记录，开始进行where判断，如果判断的结果成立，则保存到内存中，如果判断失败，则直接放弃。
where不可以使用别名判断，having可以（原因就是因为where是磁盘读数据，磁盘数据没有别名）

limit 从0开始显示多少条,从一个参数显示的后面开始显示多少条


```

