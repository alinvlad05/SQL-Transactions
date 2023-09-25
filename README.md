# SQL-Transactions
 
These are terms related to data consistency and concurrency issues that can occur in a multi-user database system. Here's an explanation of each:

Dirty Reads:

Definition: A dirty read occurs when one transaction reads data that has been modified but not yet committed by another transaction.
Impact: It can lead to incorrect or inconsistent data because the changes made by the second transaction might be rolled back, leaving the first transaction with data that never should have been visible.

Lost Updates:

Definition: Lost updates happen when two or more transactions concurrently update the same data, and one of them overwrites the changes made by the other, resulting in data loss.
Impact: It can lead to data inconsistency and loss of work. Only one of the concurrent updates is retained, and the changes made by others are lost.

Nonrepeatable Reads:
Definition: Nonrepeatable reads occur when a transaction reads the same data multiple times within its own scope, and the data values change between reads due to other concurrent transactions.
Impact: It can lead to unexpected and inconsistent results within a single transaction because the data read at different points in the transaction may not be consistent with each other.
Example: Transaction A reads a record, then reads the same record again, but Transaction B updates the record in between. Transaction A sees different values for the same record within its own execution.

Phantom Reads:
Definition: Phantom reads happen when a transaction reads a set of rows that satisfy a certain condition, but between subsequent reads within the same transaction, other transactions insert, update, or delete rows that now match or don't match the condition.
Impact: It can lead to unexpected changes in the result set of a query within a single transaction, causing inconsistency.
Example: Transaction A reads all records with a certain attribute value, and then inserts a new record that satisfies the same condition. When it reads the records again, it finds the new record it didn't expect to see.

To mitigate these concurrency issues, database management systems provide different isolation levels (e.g., READ COMMITTED, REPEATABLE READ, SERIALIZABLE) that determine how transactions interact with each other and whether they allow or prevent these types of problems. The choice of isolation level depends on the specific requirements of your application and the trade-off between data consistency and concurrency.

In MySQL, different transaction isolation levels offer varying levels of data consistency and protection against concurrency-related problems. Here's an explanation of the concurrency problems prevented and allowed by each transaction isolation level, as well as the syntax for setting the isolation level:

1. READ UNCOMMITTED:

Dirty Reads: Allowed
Lost Updates: Allowed
Nonrepeatable Reads: Allowed
Phantom Reads: Allowed

This is the lowest isolation level. It allows the most concurrency but provides the least data consistency. Transactions can read uncommitted changes from other transactions, leading to dirty reads, nonrepeatable reads, and phantom reads.

Syntax for setting the isolation level to READ UNCOMMITTED:

SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED;

2. READ COMMITTED:

Dirty Reads: Prevented
Lost Updates: Allowed
Nonrepeatable Reads: Allowed
Phantom Reads: Allowed

In READ COMMITTED, dirty reads are prevented because a transaction can only see committed data. However, it still allows other concurrency issues like lost updates, nonrepeatable reads, and phantom reads.

Syntax for setting the isolation level to READ COMMITTED:

SET TRANSACTION ISOLATION LEVEL READ COMMITTED;

3. REPEATABLE READ:

Dirty Reads: Prevented
Lost Updates: Prevented
Nonrepeatable Reads: Allowed
Phantom Reads: Allowed

REPEATABLE READ prevents dirty reads and lost updates by locking the data that a transaction reads or modifies until the transaction is completed. However, it still allows nonrepeatable reads and phantom reads.

Syntax for setting the isolation level to REPEATABLE READ:

SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;

4. SERIALIZABLE:

Dirty Reads: Prevented
Lost Updates: Prevented
Nonrepeatable Reads: Prevented
Phantom Reads: Prevented

SERIALIZABLE is the highest isolation level, ensuring the strictest data consistency. It prevents all concurrency problems, including dirty reads, lost updates, nonrepeatable reads, and phantom reads. However, it may lead to reduced concurrency.

Syntax for setting the isolation level to SERIALIZABLE:

SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;

The SET TRANSACTION ISOLATION LEVEL statement allows you to specify the desired isolation level for the next transaction within the current session. You can also set the isolation level at the session or global level for all subsequent transactions in that session or across all sessions, respectively.

Remember that the choice of isolation level should be based on the specific requirements of your application, balancing the need for data consistency and concurrency. Higher isolation levels provide stronger consistency but may lead to reduced concurrency, while lower levels allow more concurrency but may introduce potential data consistency issues.
