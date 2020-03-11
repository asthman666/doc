**The general idea of B-Tree is that**

* all the values are stored in order
* each leaf page is the same distance from the root.

Because B-Trees store the indexed columns in order, they're useful for searching for ranges of data.

InnoDB uses a **B+Tree** structure

**Clustered Indexes**

When a table has a clustered index, its rows are actually stored in the index's leaf pages.

InnoDB clusteres the data by the primary key.

solidDB and InnoDB are the only ones that support clustered indexes.

It is best to avoid random clustered keys. For example, using UUID values is a poor choice from a performance sandpoint: it makes clustered index insertion random(page split), which is a worst-case scenario.

**nonclustered Indexes**

A leaf node doesn't store a pointer to the referenced row's physical location; rather, it stores the row's primary key values. 

accesses require two index lookups instead of one


**MyISAM vs InnoDB**

MyISAM will be faster when use index to query than innodb, since MyISAM all index are same struct but Innodb has clustered and nonclustered indexes.

When insert, more indexes number, MyISAM cost more time than Innodb.

**Why range condition makes MySQL ignore any further columns in the index**

