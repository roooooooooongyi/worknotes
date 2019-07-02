# HiveTask   
## 1. oneday(1)表示今天，oneday(0)表示昨天oneday(-1)表示前天。
```
import sys
import os
import datetime
import time
from HiveTask import HiveTask

sys.path.append(os.getenv('HIVE_TASK'))  # add environment variable HIVE_TASK path to system
ht = HiveTask()


# day_dt = ht.data_day_str

date_1 = ht.oneday(-7)
date_2 = ht.oneday(-1)
date_3 = ht.oneday(0)
date_4 = ht.oneday(1) # today 2019/7/2
date_5 = ht.oneday(2)
# print(day_dt)
print("="*8)
print("date_1", date_1)
print("date_2", date_2)
print("date_3", date_3)
print("date_4", date_4)
print("date_5", date_5)
print("="*8)
```


```
========

date_1 2019-06-24

date_2 2019-06-30

date_3 2019-07-01

date_4 2019-07-02

date_5 2019-07-03

========
```

## 2. 在IDE python开发环境中为hive添加时间
将时间变量 **start_dt** 通过 **'"""+start_dt+"""'** 的形式嵌入hive代码中！否则无法正确插数据。    
start_dt变量赋值有两种方式，今天是2019年7月2日，那么19年6月30日有如下两种表达方法：              
start_dt = oneday(-1)          
start_dt = '2019-06-30'          
表名等变量需要通过 **"""+table_name+"""** 形式插入，注意不要加''符号。                
```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

import sys
import os
import datetime
import time
from HiveTask import HiveTask

sys.path.append(os.getenv('HIVE_TASK'))  # add environment variable HIVE_TASK path to system
ht = HiveTask()

table_name = 'dev.dev_ide_test_wrj'
part_dt = ht.oneday(1)
start_dt = '2019-06-18'
#start_dt = ht.oneday(-7)
end_dt = ht.oneday(1)

sql_query = """
set hive.optimize.cp=true;
set hive.optimize.pruner=true;
set hive.limit.optimeize.enable=true;
set hive.limit.row.max.size=1000000;
set hive.limit.optimize.limit.file=10;
set hive.exec.parallel=true;
set hive.exec.parallel.thread.number=16;
set hive.merge.mapfiles = true;
set hive.merge.mapredfiles = true;
set hive.merge.size.per.task=256000000;
set hive.merge.smallfiles.avgsize = 256000000;
set mapred.max.split.size=256000000;
set mapred.min.split.size.per.node=256000000;
set mapred.min.split.size.per.rack=256000000;
set hive.input.format=org.apache.hadoop.hive.ql.io.CombineHiveInputFormat;
set hive.join.emit.interval = 2000;
set hive.mapjoin.size.key = 20000;
set hive.mapjoin.cache.numrows = 20000;
set hive.exec.reducers.bytes.per.reducer=2000000000;
set hive.exec.reducers.max=999;
set hive.map.aggr=true;
set hive.groupby.mapaggr.checkinterval=100000;
set hive.auto.convert.join = true;
set hive.exec.dynamic.partition.mode = nonstrict;
set hive.exec.dynamic.partition = true;
insert overwrite table """+table_name+"""
    select
	pv,
	uv,
	dt,
	'daogou_sx'type1,
	'29' type2
from
	dev.dev_neirongdaogou_sx_sc_zzsy_orc
where
    dt >='"""+start_dt+"""'
    and dt <='"""+end_dt+"""'
group by
	pv,
	uv,
	dt
"""
ht.exec_sql(schema_name = 'dev',  sql = sql_query)

```
