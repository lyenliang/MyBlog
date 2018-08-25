title: Python Datetime Conversion
author: lyenliang
tags:
  - python
categories: []
date: 2018-08-24 16:29:00
---
One of the common issues we face when developing a software is dealing with dates and times. For example, after getting a date-time string from an API, we might have to convert it to another format that is easier for humans to read. If the API executes in different places around the world, we will need to take timezone into consideration.

Here, I summarize some of the frequently used functions when handling python `datetime`.

<img src="/images/python/python_datetime.png" alt="Python datetime conversion" style="width: 630px; " />

Let's first talk about the conversion between string and datetime:

### Converting `string` to `datetime`
Use `strptime()` if your want to convert a string to datetime:
```
#!/usr/bin/python3

from datetime import datetime

format = '%Y-%m-%d %H:%M:%S %z'
# the string variable
datetime_str = '2018-05-13 12:34:56 +0800'
# the `datetime` variable
datetime_dt = datetime.strptime(datetime_str, format)

print(type(datetime_dt))  # <class 'datetime.datetime'>
print(datetime_dt)        # 2018-05-13 12:34:56+08:00

```

The meaning of the format codes can be found at [Python's documentation](https://docs.python.org/3/library/datetime.html#strftime-and-strptime-behavior).

### Converting `datetime` to `string`
Use `strftime()` if your want to convert a datetime to string:

```
#!/usr/bin/python3

from datetime import datetime

datetime_dt = datetime.now()  # 2018-08-24 18:00:25.855212
datetime_str = datetime_dt.strftime('%Y-%m-%d %H:%M:%S %z')

print(type(datetime_str)) # <class 'str'>
print(datetime_str)       # 2018-08-24 18:00:25
```

### Changing timezone:

`astimezone()` can be used to change the timezone of a datetime variable:

```
#!/usr/bin/python3

import pytz
from datetime import datetime

# My PC is located in UTC+8 timezone
datetime_dt = datetime.now()    # 2018-08-24 21:35:46.694889 
print(datetime_dt)

datetime_taipei_dt = datetime_dt.astimezone(pytz.timezone('Asia/Tokyo')) # UTC+9

print(datetime_taipei_dt)       # 2018-08-24 22:35:46.694889+09:00  
```

Because my PC is located in UTC+8 timezone, the content of `datetime_dt` represents the time of UTC+8 timezone. Tokyo is located in UTC+9 timezone. That's why there's a 1 hour difference between `datetime_dt` and `datetime_taipei_dt`.

