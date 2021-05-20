1. 如何使用变量名
   
        declare @student Table ( id int, name varchar(255) )
        insert into @student (id, name) values (1, 'noah')

        declare @field varchar(255) = 'id'
        declare @rowid varchar(255) = '1'
        declare @tablename varchar(255) = 'student'


        select * from @student where @field = @rowid 
        -- select * from @student where 'id' = '1'

        select * from @student where id = 1 -- correct

        select * from @tablename where id = 1
        -- select * from 'student' where id = 1 
