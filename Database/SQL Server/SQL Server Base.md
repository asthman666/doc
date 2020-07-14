# SQL Server Base

    create table test_questiontype (
        questiontypeid INT IDENTITY PRIMARY KEY,
        questiontypename varchar(50) null
    )

    GO

    create table test_question (
        questionid INT IDENTITY PRIMARY KEY,
        questiontypeid int null FOREIGN KEY REFERENCES test_questiontype (questiontypeid),
        questionname varchar(255) null
    )

    GO

    insert into test_question (questiontypeid, questionname) values (null, 'How old are you?')
    insert into test_questiontype values ('item')
    insert into test_question (questiontypeid, questionname) values (1, 'Would you like to buy this one?')

    GO

    select * from test_question

> [foreign-key-relationships](https://docs.microsoft.com/en-us/sql/relational-databases/tables/create-foreign-key-relationships)