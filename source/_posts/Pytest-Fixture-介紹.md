title: Pytest Fixture 介紹
author: lyenliang
date: 2022-05-06 23:06:08
tags:
---
在用 pytest 寫測試時，可能有些程式碼每個測試一開始都需要執行，像是建立資料庫連線：


```
import mysql.connector

def test_read_db():
    # mydb 在兩個 test 裡都有出現
    mydb = mysql.connector.connect(
        host="localhost",
        user="yourusername",
        password="yourpassword"
    )
    mycursor = mydb.cursor() 
    mycursor.execute("SELECT * FROM customers")
    myresult = mycursor.fetchall()
    for x in myresult:
        print(x)

def test_update_db():
	# mydb 在兩個 test 裡都有出現
    mydb = mysql.connector.connect(
        host="localhost",
        user="yourusername",
        password="yourpassword"
    )
    mycursor = mydb.cursor()
    sql = "UPDATE customers SET address = 'Canyon 123' WHERE address = 'Valley 345'"
    mycursor.execute(sql)
    mydb.commit()
    print(mycursor.rowcount, "record(s) affected")
```

這些重複的程式碼如果只需要寫一次的話，想必可以讓你的 code 讀起來較輕鬆，日後維護也比較方便。

這時可以考慮用 pytest 的 fixture 功能來避免程式碼重複。

```
import pytest
import mysql.connector

@pytest.fixture
def mydb():
    return mysql.connector.connect(
        host="localhost",
        user="yourusername",
        password="yourpassword"
    )

def test_read_db(mydb):
    mycursor = mydb.cursor()
    mycursor.execute("SELECT * FROM customers")
    myresult = mycursor.fetchall()
    for x in myresult:
        print(x)

def test_update_db(mydb):
    mycursor = mydb.cursor()
    sql = "UPDATE customers SET address = 'Canyon 123' WHERE address = 'Valley 345'"
    mycursor.execute(sql)
    mydb.commit()
    print(mycursor.rowcount, "record(s) affected")
```

在上面的 code 裡，你可以發現我把原本的 `mydb` 轉成以下程式碼

```
@pytest.fixture
def mydb():
    return mysql.connector.connect(
        host="localhost",
        user="yourusername",
        password="yourpassword"
    )
```

然後將 `mydb` 當作參數傳給 test function，這樣 test function 還是可以使用 `mydb`，且 `mydb` 只要建立一次就可以。
