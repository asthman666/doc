### Read Committed is the default isolation level in PostgreSQL.

* A SELECT query (without a FOR UPDATE/SHARE clause) sees only data committed before the query began; it never sees either uncommitted data or changes committed during query execution by concurrent transactions.

* In effect, a SELECT query sees a snapshot of the database as of the instant the query begins to run. However, SELECT **does see** the effects of previous updates executed within its own transaction, even though they are not yet committed.

* Also note that two successive SELECT commands can see different data, even though they are within a single transaction, if other transactions commit changes after the first SELECT starts and before the second SELECT starts.

`UPDATE`, `DELETE`, `SELECT FOR UPDATE`, and `SELECT FOR SHARE` commands behave the same as `SELECT` in terms of searching for target rows: they will only find target rows that were committed as of the command start time. However, such a target row might have already been updated (or deleted or locked) by another concurrent transaction by the time it is found. **In this case, the would-be updater will wait for the first updating transaction to commit or roll back (if it is still in progress).** If the first updater rolls back, then its effects are negated and the second updater can proceed with updating the originally found row. If the first updater commits, the second updater will ignore the row if the first updater deleted it, otherwise it will attempt to apply its operation to the updated version of the row. The search condition of the command (the WHERE clause) is re-evaluated to see if the updated version of the row still matches the search condition. If so, the second updater proceeds with its operation using the updated version of the row. In the case of `SELECT FOR UPDATE` and `SELECT FOR SHARE`, this means it is the updated version of the row that is locked and returned to the client.

See the preceding description, we could design a case for preventing the stock of product from becomming negative.

BEGIN
    UPDATE product SET stock = stock - $quantity WHERE product_id = 100 and stock >= $quantity
    -- if effected data > 1  => you're able to purchase the product
    -- if effected data == 0 => you're unable to purchase the product since the out of stock
COMMIT

> [https://www.postgresql.org/docs/current/transaction-iso.html](transaction-iso)
