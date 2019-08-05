# SQL Server Date

### Subtract one day from datetime

    DATEADD(day, -1, GETDATE())

### DATEDIFF
DATEDIFF ( [day|hour|minute|second|millisecond] , startdate , enddate )

    SELECT DATEDIFF(DAY,  '2012-12-12 12:00:00', '2012-12-13 16:00:00') -- return 1

    DECLARE @Start datetime
    DECLARE @End datetime
    SET @Start = GETDATE()
    SET @End = GETDATE()
    SELECT DATEDIFF(millisecond, @Start, @End)

### Convert String to DateTime

    CONVERT(datetime, '2012/12/12 08:30:00')

### [DATEPART](https://docs.microsoft.com/en-us/sql/t-sql/functions/datepart-transact-sql)

This function returns an integer representing the specified datepart of the specified date.

    SELECT DATEPART(YEAR, GETDATE())
    SELECT DATEPART(dd, GETDATE())

### Date Part only from DateTime

    SELECT CONVERT(DATE, GETDATE())

> [how-to-get-date-part-only-from-datetime-in-sql-server](https://sqlhints.com/2013/07/14/how-to-get-date-part-only-from-datetime-in-sql-server/)    
> [how-to-return-only-the-date-from-a-sql-server-datetime-datatype](https://stackoverflow.com/questions/113045/how-to-return-only-the-date-from-a-sql-server-datetime-datatype)

### [MONTH](https://docs.microsoft.com/en-us/sql/t-sql/functions/month-transact-sql)

Returns an integer that represents the month of the specified date.

    MONTH ( date )