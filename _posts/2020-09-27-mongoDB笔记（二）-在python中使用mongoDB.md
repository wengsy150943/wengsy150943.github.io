---
title: "mongoDB笔记（二）-在python中使用mongoDB"
excerpt_separator: "`<!--more-->`"
categories:
  - Blog
tags:
  - mongodb
  - Python
header:
  image: /assets/images/header.jpg
---

> 以下内容均基于 WIN10 环境

## 前提准备

要在 python 中调用 mongoDB，首先需要对应的包 `pymongo`，直接在 pip 或其他环境中下就好了

`pip install pymongo`

由于 mongoDB 在 WIN10 环境下自动启动，所以不需要专门打开。如果没有打开的话，或许可以任务管理器一波？

## 链接数据库

pymongo 是面向对象方式组织的，和 mongoDB 一致，比较令人迷惑的一点是，mongoDB 中的方法都是蛇形命名法，但 pymongo 都是小驼峰命名法。不过只要记住了这一点，转换一下方法名就可以用了。

```python
import pymongo
client = pymongo.MongoClient("mongodb://localhost:27017/")
# OO链接数据库
db = client["database_name"]
# 或 db = client.database_name
# OO获取文档集
test = db["test"]
# 或 test = db.test
```

## 具体操作

后续操作直接对着文档集对象怼即可，其方法名如上所述，就是把 mongoDB 的方法改成蛇形命名法，具体参数和原方法一样，单个文档应该是对应 python 的 `dict`，多个维度对应一个 `dict`的 `list`。

需要注意的一点是，python 的 `dict`的键值必须用引号括起来，这一点和 mongoDB 略有区别，转换代码的时候要先预处理一下。

```python
# 随便举个例子
student_coltu = db.student
# 查询语句，查找所有女生的名字
query = {"gender": "f"}
projection = {"_id": 0,"name":1}
female_name = student_col.find(query,projection)#(query, projection)

student_col.delete_many({})

student =[
   { "name": "Joe","gender": "m", "age": 23, "birthdate": { "day": 15, "month": 3, "year":
1997 }, "hobby": ["football", "basketball", "reading"], "city": "Beijing", "time": [9, 18] },
  { "name": "Kate",  "gender": "f", "age": 22, "birthdate": { "day": 25, "month": 7, "year": 1998
}, "hobby": ["reading", "piano"], "city": "Hangzhou", "time": [8, 17] },
  { "name": "Rose",  "gender": "f", "age": 24, "birthdate": { "day": 3, "month": 3, "year": 1996
}, "hobby": ["basketball", "running", "traveling"], "city": "Shanghai", "time": [9, 19] },
  { "name": "Jason",  "gender": "m", "age": 21, "birthdate": { "day": 17, "month": 12, "year":
1999 }, "hobby": ["cooking", "photography"], "city": "Chengdu", "time": [8, 20] },
  { "name": "Grace",  "gender": "f", "age": 22, "birthdate": { "day": 10, "month": 6, "year":
1998 }, "hobby": ["photography",  "cooking", "drama"], "city": "Nanjing", "time": [9, 18] },
  { "name": "Jessica",  "gender": "f", "age": 22, "birthdate": { "day": 21, "month": 3, "year":
1998 }, "hobby": ["cooking", "piano"], "city": "Shanghai", "time": [10, 19] }
]

student_col.insert_many(student)
```

另一个容易掉的坑是 `find()`的返回对象，其类型是 `pymongo.cursor.Cursor`，但这个对象不存在 `cursor`对象的 `fetchall()/fetchone()`方法（这似乎是对应 `mySQL`的），而且也不能直接输出。但除了这一点以外，它的属性和 `list`基本一致，支持切片（除了步长），`for i in cursor`这种形式的遍历，遍历得到的对象是普通的 `dict`，所以为什么不能直接返回一个 `list`呢？
