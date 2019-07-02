# hive中的insert

insert into / insert overwrite 如果插入的数据重复则会进行更新或者覆盖   


```
drop table if exists dev.dev_ide_test_wrj;
create
	table dev_ide_test_wrj
	(
		pv int,
		uv int,
		dt string,
		type1 string,
		type2 string
	)
	ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' STORED AS TEXTFILE; ----每行结尾分隔符
    
```
