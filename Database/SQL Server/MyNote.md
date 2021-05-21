1. 变量名使用的陷阱
   
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

2. left join之后inner join

        declare @student Table ( id int, name varchar(255) )
        insert into @student (id, name) values (1, 'noah')
        insert into @student (id, name) values (2, 'beata')                

        declare @major Table ( id int, majorname varchar(255) )
        insert into @major (id, majorname) values (1, 'English')
        insert into @major (id, majorname) values (2, 'Chinese')
        insert into @major (id, majorname) values (3, 'Math')

        declare @studentscore Table (id int, studentid int, majorid int, score int)
        insert into @studentscore values (1, 1, 1, 60), (2, 1, 2, 80), (3, 2, 3, 100)

        select s.name, m.majorname, sc.score 
		from @student as s
        left join @studentscore as sc
                inner join @major as m on m.id = sc.majorid
        on s.id = sc.studentid

        select s.name, m.majorname, sc.score 
		from @student as s
        left join @studentscore as sc on s.id = sc.studentid
        left join @major as m on m.id = sc.majorid        

        -- result:

        name	majorname	score
        noah	English	60
        noah	Chinese	80
        beata	Math	100

        name	majorname	score
        noah	English	60
        noah	Chinese	80
        beata	Math	100
        beata	NULL	70
                