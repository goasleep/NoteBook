查询缓存机制

缓存是放在内存当中的。

#### 如何查询命中缓存的

缓存查询策略：全局扫描。

不放入缓存的情况：使用不确定的值。如NOW()，CURRTEN_DATE()等

使用缓存会有额外的开销：

- 读之前要查询缓存是否命中
- 将结果存储缓存
- 在写数据的时候，需要将相关的缓存设置失效
- 事务机制会使缓存失效

#### 查询缓存如何使用内存

查询缓存分为两部分，一部分是管理结构，大约为40KB，一部分是缓存块。

数据是一条一条地放入缓存中的。

#### 什么时候使用缓存

适合那一些消耗大量资源但是占用存储空间小的操作。如COUNT()



