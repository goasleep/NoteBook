InnoDB 使用一系列的一个或多个的独立文件存储数据，我们称之为表空间（tablespace）。

InnoDB使用MVCC(多版本并发控制)来实现高并发。

InnoDB不能够对索引进行排序，MyISAM可以。

InnoDB提供各种内部优化，包括预读优化，适用性的哈希索引，插入缓存

