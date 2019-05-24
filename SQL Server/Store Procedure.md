# Store Procedure

## How to return string value from stored procedure

    CREATE PROCEDURE [dbo].[testone] ( @i VARCHAR(50), @r varchar(50) out )
    AS
    BEGIN
        IF @i IS NULL
        BEGIN
            PRINT 'ERROR: You must specify input'
            RETURN(1)
        END
        set @r = 'Hello, ' + @i
        return 0
    END

    GO

    declare @r varchar(50)
    declare @rc int
    declare @input varchar(50) = 'World'
    exec @rc = [dbo].[testone] @input, @r out
    print 'return value ' + @r
    print 'return code ' + convert(varchar, @rc)

> [how-to-return-string-value-from-the-stored-procedure](https://stackoverflow.com/questions/6450194/how-to-return-string-value-from-the-stored-procedure)

> [Return Data from a Stored Procedure
](https://docs.microsoft.com/en-us/sql/relational-databases/stored-procedures/return-data-from-a-stored-procedure?view=sql-server-2017)

> [Return Codes](https://docs.microsoft.com/en-us/sql/relational-databases/stored-procedures/return-data-from-a-stored-procedure?view=sql-server-2017#examples-of-return-codes)
