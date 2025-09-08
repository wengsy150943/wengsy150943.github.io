---
permalink: /about/
title: "About"
---

程序员，数据库测试相关，不会 AI

---

[旧博客](https://www.cnblogs.com/wengsy150943/)内容随机迁移中。

---

一些做过的事情：

- 一些 python 的[小玩具](https://github.com/wengsy150943/python-toys)
- 汇报过一些数据库的 bug
  - TiDB 分区的 limit 会返回过多值, [issue](https://github.com/pingcap/tidb/issues/41462), fixed
  - TiDB 在 RR 级别下读更新数据有点奇怪, [issue](https://github.com/pingcap/tidb/issues/42487), confirmed
  - TiDB 的`rename index`表现和 MySQL 不一致, [issue1](https://github.com/pingcap/tidb/issues/43650), [issue2](https://github.com/pingcap/tidb/issues/43652)
  - TiDB 的`show create table`表现和 MySQL 不一致, [issue3](https://github.com/pingcap/tidb/issues/43730), comfirmed, duplicate
  - TiDB 和 MySQL 的谓词中括号会影响浮点数的运算结果, [issue1](https://github.com/pingcap/tidb/issues/44154), [issue2](https://bugs.mysql.com/bug.php?id=111142), confirmed
  - MariaDB 的 LOCK IN SHARE MODE 加锁不符合预期, [issue](https://jira.mariadb.org/browse/MDEV-31569)
  - TiDB 对空表查询的基数预估不准确, [issue](https://github.com/pingcap/tidb/issues/44563), confirmed
  - TiDB 的 Multiple Rocksdb 会占用大量磁盘空间,无法有效删除, [issue](https://github.com/pingcap/tidb/issues/44894), fixed
  - TiDB 在某些情况下无法正常创建索引, [issue](https://github.com/pingcap/tidb/issues/45624), confirmed
  - PostgreSQL 对 CHAR 的类型转换不符合预期, [issue](https://www.postgresql.org/message-id/tencent_57E520E634A739CC1F11E471%40qq.com), will not fix
  - TiDB 含子查询的写操作读取了错误的快照, [issue](https://github.com/pingcap/tidb/issues/45677), confirmed
  - TiDB RR 隔离级别下可能读取重复的 unique key, [issue](https://github.com/pingcap/tidb/issues/46900), confirmed, duplicate
  - TiDB DROP DATABASE 不会被阻塞, [issue](https://github.com/pingcap/tidb/issues/46943), confirmed
  - OceanBase 中运算顺序会影响与浮点相关的 JOIN 结果,[issue](https://github.com/oceanbase/oceanbase/issues/1590), will not fix
  - TiDB 的 BLOB 类型的 join 结果不正确, [issue](https://github.com/pingcap/tidb/issues/50393), fixed
  - TiDB(TiFlash)的 BLOB 类型的 join 结果同样不正确, [issue](https://github.com/pingcap/tiflash/issues/8776), fixed
  - TiDB 在 TTL 超时之后可能无法正常结束事务, [issue](https://github.com/pingcap/tidb/issues/49151), fixed
  - TiDB 的 BLOB 类型转换缺失，可能导致结果与 MySQL 不一致, [issue](https://github.com/pingcap/tidb/issues/53943), confirmed
  - TiDB 超时后提交触发 JDBC 断链, [issue](https://github.com/pingcap/tidb/issues/49811), confirmed
  - OceanBase 的 BLOB 类型转换缺失，可能导致结果与 MySQL 不一致, [issue](https://github.com/oceanbase/oceanbase/issues/2018), confirmed
  - OceanBase 在修改租户配置后，无法成功重启租户并卡死, [issue](https://github.com/oceanbase/oceanbase/issues/2138), confirmed
  - OceanBase 含子查询的写操作读取了错误的快照, [issue](https://github.com/oceanbase/oceanbase/issues/2145), will not fix
  - MySQL 自增列的数值越界检查缺失, [issue](https://bugs.mysql.com/bug.php?id=117563), confirmed
  - MySQL 分区 DDL 会导致并发的单个事务死锁回滚, [issue](https://bugs.mysql.com/bug.php?id=117735), confirmed
  - TiDB 无法检测到特定的死锁, [issue](https://github.com/pingcap/tidb/issues/59781), confirmed
  - TiDB playground 异常宕机, [issue](https://github.com/pingcap/tidb/issues/62336), confirmed
  - MariaDB 错误抛出 ERROR 1020 , [issue](https://jira.mariadb.org/browse/MDEV-37208), confirmed
  - MySQL 范围更新部分失败, [issue](https://bugs.mysql.com/bug.php?id=118923), confirmed

