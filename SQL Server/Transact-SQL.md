# Transact-SQL

DECLARE

    DECLARE @gender varchar(30);   
    
    DECLARE @find varchar(30) = 'Man%';
    
    DECLARE @lastName varchar(30), @firstName varchar(30), @rows int;

    DECLARE @age INT;
    
SET

	SET @gender = 'Fema';
	
	SET @gender += 'le';
	
	SET @rows = (SELECT COUNT(*) FROM Customer);  

    SET @age = 18;
	
SELECT

    SELECT @gender = 'Man';
    
    -- If CustomerID 1000 does not exists, @gender will retain its present value.
    SELECT @gender = Gender FROM Customer WHERE CustomerID = 1000;
    
    -- If CustomerID 1000 does not exists, @gender will be NULL
    SELECT @gender = (SELECT Gender FROM Customer WHERE CustomerID = 1000);


GETDATE

    SELECT GETDATE() as "Now"

IF 

    IF @gender IS NOT NULL
    BEGIN
        { sql_statement | statement_block }
    END

    IF Boolean_expression   
       { sql_statement | statement_block }   
    [ ELSE   
       { sql_statement | statement_block } ]   

To define a **statement block**, use the control-of-flow keywords `BEGIN` and `END`.

    IF Boolean_expression   
        BEGIN
            statement_block
        END            
    [ ELSE   
        BEGIN
            statement_block
        END ]


WHILE

    DECLARE @cnt INT = 0;

    WHILE @cnt < 3
    BEGIN
        PRINT @cnt
        SET @cnt = @cnt + 1;
    END;

CONVERT

    CONVERT(VARCHAR, 1)

    CONVERT(INT, '1')

RTRIM 

Returns a character string after truncating all trailing spaces.

    RTRIM('Hello World   ') -- return 'Hello World'

SUBSTRING

    DECLARE @Letters CHAR(5) = 'AEIOU'
    DECLARE @Letter CHAR(1)
    SET @Letter = SUBSTRING(@Letters, ABS(CHECKSUM(NEWID()) % 5) + 1, 1)
    PRINT @Letter 

BIT

    DECLARE @YOUNG BIT
    SET @YOUNG = 1
    IF @YOUNG = 1
        PRINT 'OK'
    ELSE
        PRINT 'NOT OK'