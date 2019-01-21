# sql server Tips

### Concept

**DDL** is **Data Definition Language** : it is used to define data structures.

For example, with SQL, it would be instructions such as create table, alter table, ...


**DML** is **Data Manipulation Language** : it is used to manipulate data itself.

For example, with SQL, it would be instructions such as insert, update, delete, ...    

### Escape single quotes in SQL 'LIKE' command

    SELECT TOP 1 * FROM Customer WHERE LastName LIKE '%''%';

### System

    -- Find SQLServer Version
    SELECT @@VERSION

    -- Find names of the ServerName and ServiceName
    SELECT @@SERVERNAME AS 'Server Name', @@SERVICENAME AS 'Service Name' 
    
    -- Find names of the HostName and LoginUser
    SELECT HOST_NAME() AS HostName, SUSER_NAME() LoggedInUser
    
    -- Find all instance names (Command Prompt)
    reg query "HKLM\Software\Microsoft\Microsoft SQL Server\Instance Names\SQL

    -- Detect READ_COMMITTED_SNAPSHOT is enabled?
    SELECT is_read_committed_snapshot_on FROM sys.databases WHERE name= 'YourDatabase'

    -- Detect current transaction level? 
    DBCC useroptions
    
### Tip

    -- Default join behaviour test is inner join
    DECLARE @A TABLE (x INT)
    INSERT INTO @A
        SELECT 1 UNION ALL
        SELECT 2

    DECLARE @B TABLE (x INT)
    INSERT INTO @B
        SELECT 2 UNION ALL
        SELECT 3

    SELECT 
        A.x AS 'A.x', 
        B.x AS 'B.x'
    FROM @A A
    JOIN @B B
        ON A.x = B.x

### Recursion

    WITH [Dates] as (
    SELECT convert(datetime, '1/20/2017') as [Date]
    UNION ALL
    SELECT DATEADD(DAY, 1, [Date])
    FROM [Dates]
    WHERE [Date] < '12/21/2017'
    ) SELECT
        * from [Dates]
    option (maxrecursion 0)

> 参考:

- [How to find current transaction level?](https://stackoverflow.com/questions/1038113/how-to-find-current-transaction-level)     

- [How to detect READ_COMMITTED_SNAPSHOT is enabled?](https://stackoverflow.com/questions/51969/how-to-detect-read-committed-snapshot-is-enabled)   

- [What is the default T-SQL JOIN behaviour, INNER or OUTER?](https://stackoverflow.com/questions/23500481/what-is-the-default-t-sql-join-behaviour-inner-or-outer)

- [How to find Stored Procedures execution time in SQL Server?
](https://stackoverflow.com/questions/7766880/how-to-find-stored-procedures-execution-time-in-sql-server)
    

