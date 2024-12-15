субд постгрес 

### Read Commited

```sql
BEGIN TRANSACTION ISOLATION LEVEL READ COMMITTED;
SELECT * FROM accounts WHERE name = 'Tyler Durden'; // Prints 10
-- Execute parallelly:
-- BEGIN TRANSACTION ISOLATION LEVEL READ COMMITTED;
-- UPDATE accounts SET balance = balance + 1 WHERE name = 'Tyler Durden';
-- COMMIT; 
SELECT * FROM accounts WHERE name = 'Tyler Durden'; // Prints 11 
COMMIT;
```

### Repeatable Read

```sql
BEGIN TRANSACTION ISOLATION LEVEL REPEATABLE READ;
SELECT * FROM accounts WHERE name = 'Tyler Durden'; // Prints 10
-- Execute parallelly:
-- BEGIN TRANSACTION ISOLATION LEVEL REPEATABLE READ;
-- UPDATE accounts SET balance = balance + 1 WHERE name = 'Tyler Durden';
-- COMMIT; 
SELECT * FROM accounts WHERE name = 'Tyler Durden'; // Prints 10
COMMIT;
SELECT * FROM accounts WHERE name = 'Tyler Durden'; // Prints 11
```

### Serializable Read

```sql
-- Сессия 1
BEGIN TRANSACTION ISOLATION LEVEL SERIALIZABLE;
SELECT * FROM accounts; -- Получаем сумму 2000
-- Execute parallelly:
-- BEGIN TRANSACTION ISOLATION LEVEL SERIALIZABLE;
-- UPDATE accounts SET balance = balance - 1 WHERE name = 'Tyler Durden';
-- COMMIT; 
UPDATE accounts SET balance = balance + 1 WHERE name = 'Tyler Durden';
COMMIT; -- ROLLBACKS DUE TO CONCURRENT UPDATE ERROR
```
