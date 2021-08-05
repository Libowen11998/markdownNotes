A表

| id   |      |
| ---- | ---- |
| name |      |

B表

| id   |      |
| ---- | ---- |
| a_id |      |
| name |      |

C表

| id   |      |
| ---- | ---- |
| b_id |      |
| name |      |

D表

| id   |      |
| ---- | ---- |
| c_id |      |
| name |      |



```sql
select name from D where c_id in
	(select id from C where b_id=
     (select id from B where a_id=
      select id from A where id=#{id}
     )
    )
    
select name from D where c_id in
(select id from C where b_id=
	select id from B where a_id =#{id}
)
```

