# HiveTask   

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
date_4 = ht.oneday(1)
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
