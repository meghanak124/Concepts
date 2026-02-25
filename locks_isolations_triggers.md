# Locking Mechanism, Database Isolation Levels, Triggers
- These mechanisms ensure data integrity, consistency, and safe
concurrency handling.

## Locking Mechanism

Locks prevent data inconsistency during concurrent access.

### Shared Lock (Read Lock)

Multiple users can read but not modify.

### Exclusive Lock (Write Lock)

Only one user can modify.

![](https://media.geeksforgeeks.org/wp-content/uploads/20250113111425534576/lock_based_protocol.webp)

------------------------------------------------------------------------

## Database Isolation Levels

### Read Uncommitted

May read uncommitted changes (Dirty Read).

### Read Committed

Reads only committed data.

### Repeatable Read

Rows cannot change during transaction.

### Serializable

Highest level. Transactions execute sequentially.

------------------------------------------------------------------------

## 4. Triggers

A trigger is automatically executed when an event occurs.

Example: CREATE TRIGGER log_update AFTER UPDATE ON employees FOR EACH
ROW INSERT INTO audit_log VALUES (...);
