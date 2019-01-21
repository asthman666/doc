# Clustered and Nonclustered Indexes Described

An index is an on-disk structure associated with a table or view that speeds retrieval of rows from the table or view. An index contains keys built from one or more columns in the table or view. These keys are stored in a structure (B-tree) that enables SQL Server to find the row or rows associated with the key values quickly and efficiently.

一个索引就是一个在磁盘上的结构体，它和一个表或者一个视图关联，可以加速从表中或者视图中读取行。一个索引包含的关键键是从表中或者视图中的一个或者多个字段建立的。这些关键键使用一种结构(B-tree)用来使SQL Server找到和这些关键键有关联的行更快更有效。

A table or view can contain the following types of indexes:

一个表或者视图可以包含下面的一些索引类型：

Clustered

簇索引

Clustered indexes sort and store the data rows in the table or view based on their key values. These are the columns included in the index definition. There can be only one clustered index per table, because the data rows themselves can be stored in only one order.

簇索引依赖他们的键值来排序和存储表或者视图的数据。它们是一些包括索引定义的一些列。一张表只能有一个簇索引，因为数据行本身只能按照一种顺序来存储。

The only time the data rows in a table are stored in sorted order is when the table contains a clustered index. When a table has a clustered index, the table is called a clustered table. If a table has no clustered index, its data rows are stored in an unordered structure called a heap.

当一张表包含一个簇索引的时候，一张表的数据行是按照一种排序被存储的。当一张表有一个簇索引的时候，这张表被叫做一个簇表。如果一张表没有簇索引，它的数据行以一种叫做堆的无序结构被存储。

Nonclustered

非聚集

Nonclustered indexes have a structure separate from the data rows. A nonclustered index contains the nonclustered index key values and each key value entry has a pointer to the data row that contains the key value.

非聚集索引有一个结构体来分隔数据行的。一个非聚集索引包含非聚集索引键并且每个键值体有一个指针指向包含这个键值的数据行。

The pointer from an index row in a nonclustered index to a data row is called a row locator. The structure of the row locator depends on whether the data pages are stored in a heap or a clustered table. For a heap, a row locator is a pointer to the row. For a clustered table, the row locator is the clustered index key.

在一个非聚集索引的一个指向数据行的索引行的指针被叫做行定位器。行定位器的结构依赖于数据页被存储在堆里或者一个簇表里。对于堆，一个行定位器是一个指向行的指针。对于一个簇索引表，行定位器是一个簇索引键。

You can add nonkey columns to the leaf level of the nonclustered index to by-pass existing index key limits, and execute fully covered, indexed, queries. For more information, see Create Indexes with Included Columns. For details about index key limits see Maximum Capacity Specifications for SQL Server.


Both clustered and nonclustered indexes can be unique. This means no two rows can have the same value for the index key. Otherwise, the index is not unique and multiple rows can share the same key value. For more information, see Create Unique Indexes.

簇索引和非聚集索引都可以是唯一的。这意味着对于索引键，没有两行可以有相同的值。另一种说法是，一个索引不是唯一的，那么多行可以分享相同的键值。

Indexes are automatically maintained for a table or view whenever the table data is modified.

当表的数据发生改变时，表和视图的索引可以被自动维护。

See Indexes for additional types of special purpose indexes.

Indexes and Constraints

索引和约束

Indexes are automatically created when PRIMARY KEY and UNIQUE constraints are defined on table columns. For example, when you create a table and identify a particular column to be the primary key, the Database Engine automatically creates a PRIMARY KEY constraint and index on that column. For more information, see Create Primary Keys and Create Unique Constraints.

当主键和唯一约束被定义在表的列上时，索引被自动的创建。例如，当你创建一个表并且定义了一个特殊的列作为主键，数据库引擎自动在这个列上创建一个主键约束和索引。

How Indexes are used by the Query Optimizer

索引如何被搜索优化器使用

Well-designed indexes can reduce disk I/O operations and consume fewer system resources therefore improving query performance. Indexes can be helpful for a variety of queries that contain SELECT, UPDATE, DELETE, or MERGE statements. Consider the query SELECT Title, HireDate FROM HumanResources.Employee WHERE EmployeeID = 250 in the AdventureWorks2012 database. When this query is executed, the query optimizer evaluates each available method for retrieving the data and selects the most efficient method. The method may be a table scan, or may be scanning one or more indexes if they exist.

好的索引设计可以减少磁盘的I/O操作并且耗费很少的系统资源来提升语句效率。索引对于很多类语句都有用，包含SELECT,UPDATE,DELETE或者MERGE语句。

When performing a table scan, the query optimizer reads all the rows in the table, and extracts the rows that meet the criteria of the query. A table scan generates many disk I/O operations and can be resource intensive. However, a table scan could be the most efficient method if, for example, the result set of the query is a high percentage of rows from the table.

当执行一个表扫描时，语句优化器会读取一张表的所有数据，并且提取出符合语句条件的行。一个表的扫描会产生很多磁盘的I/O操作并且造成资源紧张。然而，一个表的扫描有可能是非常有效的，如果语句的结果集占有整张表的行的比例很高的时候。

When the query optimizer uses an index, it searches the index key columns, finds the storage location of the rows needed by the query and extracts the matching rows from that location. Generally, searching the index is much faster than searching the table because unlike a table, an index frequently contains very few columns per row and the rows are in sorted order.

当一个语句优化器使用一个索引时，它搜索索引键的列，找到存储这些行的位置并且从位置中提取出符合条件的行。通常来说，搜索索引会比搜索表快很多，因为不像一张表，一个索引通常每一行包含很少的列并且行是按照一种排序排列的。

The query optimizer typically selects the most efficient method when executing queries. However, if no indexes are available, the query optimizer must use a table scan. Your task is to design and create indexes that are best suited to your environment so that the query optimizer has a selection of efficient indexes from which to select. SQL Server provides the Database Engine Tuning Advisor to help with the analysis of your database environment and in the selection of appropriate indexes.

