Transaction

* `DBCC USEROPTIONS` 

    Returns the SET options active (set) for the current connection.

    这里有一个`isolation level`选项


* `SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED`

    设置隔离级别

当隔离级别设置成`READ UNCOMMITTED`的时候，是允许脏读取的
当隔离级别设置成`READ COMMITTED`的时候，如果读取的数据中有脏数据，那么会阻塞

> [dbcc-useroptions](https://docs.microsoft.com/en-us/sql/t-sql/database-console-commands/dbcc-useroptions-transact-sql?view=sql-server-ver15)
> [set-transaction-isolation-level-transact-sql](https://docs.microsoft.com/en-us/sql/t-sql/statements/set-transaction-isolation-level-transact-sql?view=sql-server-ver15)
> [sql-server-transaction-locking-and-row-versioning-guide](https://docs.microsoft.com/en-us/sql/relational-databases/sql-server-transaction-locking-and-row-versioning-guide?view=sql-server-ver15#lock-granularity-and-hierarchies)


