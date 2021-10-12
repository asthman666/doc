# How to get the data that count by minute order by the minute datetime?

1. Need to know how to convert datetime to accurate to minute format
    
        SELECT FORMAT(getdate(), 'yyyy-MM-dd HH:mm') 

2. Try to group by it and order by it

        SELECT COUNT(*) "count", FORMAT(transactiondate, 'yyyy-MM-dd HH:mm') "minute"
        FROM salesTransaction  
        where transactiondate > '2021-09-28 07:00:00.000'
        GROUP BY FORMAT(transactiondate, 'yyyy-MM-dd HH:mm')
        ORDER BY 2;
