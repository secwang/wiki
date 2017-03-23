<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [tuneing slow query](#tuneing-slow-query)
  - [show profiling](#show-profiling)
  - [differ between mysql primary key and index](#differ-between-mysql-primary-key-and-index)
  - [charsets debugging](#charsets-debugging)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---
title: "mysql"
date: 2016-09-20 23:00
---
[TOC]

## tuneing slow query
1. open /etc/my.cnf 
2. open slow-query log and modify long_query_time to filter most long query.

```
slow-query-log=1
slow-query-log-file= ~/mysql-slow.log
long_query_time=0.05

```

### show profiling

```
SET profiling = 1;
query;
SHOW PROFILES;
```

### differ between mysql primary key and index 

primary key related with innodb store, every table in innodb with a primary key.
so, we'd better define this by ourself instead of by store engine.

```
 
ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 ROW_FORMAT=DYNAMIC;

id BIGINT(20) PRIMARY KEY NOT NULL AUTO_INCREMENT,


```


### charsets debugging

```
ResultSet rs = null;
try {
    rs = daoHelper.getConnHelper().get().createStatement().executeQuery("SHOW VARIABLES LIKE 'character_set_%'");
    while(rs.next()){
	System.out.println(rs.getString(1)+","+rs.getString(2));
    }
    rs.close();
} catch (Exception e) {
    e.printStackTrace();
}
```
