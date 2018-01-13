---
title: sql语句格式化
date: 2018-01-08 16:32:06
tags:
- sql
- js 
- formatter
categories:
- 前端
---

# 介绍 #
这是格式化sql的JavaScript插件，能对sql字符串进行格式化，用于前端展示sql。
下面是github地址：
[https://github.com/zeroturnaround/sql-formatter](https://github.com/zeroturnaround/sql-formatter "github地址")

# 用法 #
可以用前端模块化引用，也可以全局引用。

```
sqlFormatter.format("SELECT *", {
    language: "n1ql", // Defaults to "sql"
    indent: "    "   // Defaults to two spaces
});
```


其中，language为：
- sql-Standard SQL
- n1ql-Couchbase N1QL
- db2-IBM DB2

支持占位符功能：

```
// Named placeholders
sqlFormatter.format("SELECT * FROM tbl WHERE foo = @foo", {
    params: {foo: "'bar'"}
}));

// Indexed placeholders
sqlFormatter.format("SELECT * FROM tbl WHERE foo = ?", {
    params: ["'bar'"]
}));
```


结果：

```
SELECT
      *
    FROM
      tbl
    WHERE
      foo = 'bar'
```


# 关于引用问题 #

```
if(typeof exports === 'object' && typeof module === 'object')
		module.exports = factory();
	else if(typeof define === 'function' && define.amd)
		define([], factory);
	else if(typeof exports === 'object')
		exports["sqlFormatter"] = factory();
	else
		root["sqlFormatter"] = factory();
```


可以自由选择模块加载类型，最后的就是全局变量模式。


