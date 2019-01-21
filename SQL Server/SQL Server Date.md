# [SQL Server Date](http://asthman.me/article/137)

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

    SELECT DATEPART(YEAR, GETDATE())
    select DATEPART(dd, GETDATE())