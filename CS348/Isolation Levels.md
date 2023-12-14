---
dg-publish: true
---
# Isolation Levels
## Level 3
**[[Schedules#Serializable Schedules|Serializability]]**: Realized by [[Two-Phase Locking#Strict Two-Phase Locking| strict 2PL]] with table level locks

## Level 2

> [!tip] Level 3 without coarse grain lock

**Repeatable Read:** Realized by strict 2PL with tuple level locks only
*Phantom tuples may occur*

## Level 1

> [!tip] Level 2 without share locks

**Cursor Stability:** Realized by strict 2PL with tuple level exclusive locks only
* Same query executed twice in a transaction can produce different answers
* No repeatable read

## Level 0

> [!tip] No locks

* Transaction queries may read uncommitted updates

