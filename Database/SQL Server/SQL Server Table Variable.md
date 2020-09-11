* 表变量在批处理结束后自动被清除

    DECLARE @tb1 Table (
        Id INT,
        Name VARCHAR(100),
        Age INT
    )

    INSERT INTO @tb1 VALUES (1, 'Nick', 20)

    SELECT * FROM @tb1


[declare-local-variable](https://docs.microsoft.com/en-us/sql/t-sql/language-elements/declare-local-variable-transact-sql?view=sql-server-ver15)