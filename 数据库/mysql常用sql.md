1.查找表中多余的重复记录（多个字段）

```
select * from t_userlogin a
where (a.username,a.phone) in (select username,phone from t_userlogin group by username,phone having count (*) > 1)
```



2.删除表中多余的重复记录（多个字段），只留有userid最小的记录

```
delete from t_userlogin a
where (a.username,a.phone) in (select username,phone from t_userlogin group by username,phone having count (*) > 1)
and userid not in (select min(userid) from t_userlogin group by username,phone having count (*)>1)
```

