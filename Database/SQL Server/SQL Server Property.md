# SQL Server Property

## find login username

    SELECT USER_NAME()

## find the sql server version

    SELECT @@VERSION

## find the database_id 

    select DB_ID()

    select DB_ID(N'db_name')

## find the object_id

    select OBJECT_ID(N'table_name')