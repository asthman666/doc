# SQL Server Temp Table

### How to use temp table backup table data?

    SELECT * INTO #MyTable_tmp FROM MyTable

### How to get the list of temp tables?

    SELECT * FROM tempdb.sys.tables
    SELECT * FROM tempdb.sys.objects
    
### How to check temp table if exists

    -- double dot is the default schema of the user, which is typically dbo 

    SELECT OBJECT_ID('tempdb..#MyTable_tmp')

    IF OBJECT_ID('tempdb..#MyTable_tmp') IS NOT NULL 
        DROP TABLE #MyTable_tmp

### How to drop temp table

    DROP TABLE #MyTable_tmp

### loop temp table

    select top 10 *, ROW_NUMBER() over (order by primary_key desc) NUM into #tmptable from [db_name].[dbo].[table_name] order by primary_key desc

example 1:

    WHILE (SELECT COUNT(*) From #tmptable) > 0
    BEGIN 
        SELECT TOP 1 @NUM = NUM FROM #tmptable

        -- process logic begin

        -- process logic end

        Delete #tmptable Where NUM = @NUM
    END
    IF OBJECT_ID('tempdb..#tmptable') IS NOT NULL 
        DROP TABLE #tmptable  

example 2:

    DECLARE @I INT
    SET @I = 1
    
    WHILE @I <= ( SELECT MAX(row) FROM #tmptable ) 
    BEGIN
        
        SELECT * FROM #tmptable WHERE NUM = @NUM
                    
        -- process logic begin

        -- process logic end
                    
        SET @I = @I + 1
    END
    IF OBJECT_ID('tempdb..#tmptable') IS NOT NULL 
        DROP TABLE #tmptable

> [What is the equivalent of 'CREATE TABLE … LIKE …" in SQL Server](https://stackoverflow.com/questions/616104/what-is-the-equivalent-of-create-table-like-in-sql-server)

> [explicit-value-for-the-identity-column](https://stackoverflow.com/questions/2005437/an-explicit-value-for-the-identity-column-in-table-can-only-be-specified-when-a)    