1.查找表中多余的重复记录（多个字段）

```mysql
select * from t_userlogin a
where (a.username,a.phone) in (select username,phone from t_userlogin group by username,phone having count (*) > 1)
```

2.删除表中多余的重复记录（多个字段），只留有userid最小的记录

```mysql
delete from t_userlogin a
where (a.username,a.phone) in (select username,phone from t_userlogin group by username,phone having count (*) > 1)
and userid not in (select min(userid) from t_userlogin group by username,phone having count (*)>1)
```

3.插入其他表中不重复的数据

```mysql
insert into t_student_sos(username) select username from t_student_basic where username not in (select username from t_student_sos);
```

