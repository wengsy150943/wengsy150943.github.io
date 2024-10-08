---
permalink: /about/
title: "About"
---
程序员，数据库测试相关，不会AI

---

[旧博客](https://www.cnblogs.com/wengsy150943/)内容随机迁移中。

---

一些做过的事情：

- 一些python的[小玩具](https://github.com/wengsy150943/python-toys)
- 汇报过一些数据库的bug
  - TiDB 分区的limit会返回过多值，[issue](https://github.com/pingcap/tidb/issues/41462), fixed
  - TiDB在RR级别下读更新数据有点奇怪，[issue](https://github.com/pingcap/tidb/issues/42487)
  - TiDB的`rename index`表现和MySQL不一致, [issue1](https://github.com/pingcap/tidb/issues/43650),[issue2](https://github.com/pingcap/tidb/issues/43652)
  - TiDB的`show create table`表现和MySQL不一致,[issue3](https://github.com/pingcap/tidb/issues/43730)
  - TiDB和MySQL的谓词中括号会影响浮点数的运算结果,[issue1](https://github.com/pingcap/tidb/issues/44154),[issue2](https://bugs.mysql.com/bug.php?id=111142), confirmed
  - MariaDB的LOCK IN SHARE MODE 加锁不符合预期,[issue](https://jira.mariadb.org/browse/MDEV-31569)
  - TiDB对空表查询的基数预估不准确,[issue](https://github.com/pingcap/tidb/issues/44563), confirmed
  - TiDB的Multiple Rocksdb会占用大量磁盘空间,无法有效删除,[issue](https://github.com/pingcap/tidb/issues/44894), fixed
  - TiDB在某些情况下无法正常创建索引,[issue](https://github.com/pingcap/tidb/issues/45624), confirmed
  - PostgreSQL 对CHAR的类型转换不符合预期,[issue](https://www.postgresql.org/message-id/tencent_57E520E634A739CC1F11E471%40qq.com), will not fix
  - TiDB 含子查询的写操作读取了错误的快照,[issue](https://github.com/pingcap/tidb/issues/45677), confirmed
  - TiDB RR隔离级别下可能读取重复的unique key,[issue](https://github.com/pingcap/tidb/issues/46900), confirmed, duplicate
  - TiDB DROP DATABASE不会被阻塞,[issue](https://github.com/pingcap/tidb/issues/46943), confirmed
  - OceanBase中运算顺序会影响与浮点相关的JOIN结果,[issue](https://github.com/oceanbase/oceanbase/issues/1590), will not fix
  - TiDB的BLOB类型的join结果不正确,[issue](https://github.com/pingcap/tidb/issues/50393), fixed
  - TiDB(TiFlash)的BLOB类型的join结果同样不正确,[issue](https://github.com/pingcap/tiflash/issues/8776), confirmed
  - TiDB在TTL超时之后可能无法正常结束事务,[issue](https://github.com/pingcap/tidb/issues/49151), fixed
  - TiDB的BLOB类型转换缺失，可能导致结果与MySQL不一致, [issue](https://github.com/pingcap/tidb/issues/53943), confirmed
  - OceanBase的BLOB类型转换缺失，可能导致结果与MySQL不一致, [issue](https://github.com/oceanbase/oceanbase/issues/2018), confirmed
  - OceanBase在修改租户配置后，无法成功重启租户并卡死, [issue](https://github.com/oceanbase/oceanbase/issues/2138)

