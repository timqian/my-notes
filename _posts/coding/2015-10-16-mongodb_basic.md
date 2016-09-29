---
layout: post
title: mongodb 小记
tags:
- database
---

## 概念:

mongodb 中数据存储单位叫做  `documents`. `documents`以类似 JSON 的 BSON 键值对方式存储数据.
BSON 是 JSON 的二进制形式, 比 JSON 多了关于数据类型的信息.
`documents` 组成 `collection`. 对应关系型数据库中的 table.

## 常用命令:

- `mongod --dbpath ./data/db`: 开启数据库进程
- `mongo`: 操作数据库


## 读操作(查询): `db.collection.find()`

可以对 `collection` 进行查询.

例: `db.users.find( { age: { $gt: 18 } }, { name: 1, address: 1 } ).limit(5)`
其中

- `{ age: { $gt: 18 } }`是查询条件,
- `{ name: 1, address: 1 }`是 projection, 指定需要的部分
- `limit(5)`是 cursor modifier, 对返回的数据做排序, 数量限制等操作

## 写操作(增删改):

### 增: `db.collection.insert()`: 增加新的 document

### 删: `db.collection.remove()`: 根据查询条件删除 document

### 改: `db.collection.update()`: 拥有三个参数

```
db.users.update(
   { age: { $gt: 18 } }, // 查询条件
   { $set: { status: "A" } }, // update value
   { multi: true } // update option(multi 用来指定是否更新多个 document)
)
```
