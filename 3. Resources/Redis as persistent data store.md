---
tags:
  - backend
  - redis
source:
  - https://www.youtube.com/watch?v=WQ61RL1GpEE
  - https://www.youtube.com/watch?v=a4yX7RUgTxI
type:
  - "[[TILT]]"
created: 2023-10-16T19:27:00
areas:
  - "[[Database]]"
archived: false
---
# How Redis persist data

## Snapshotting (RDB)

Similar to snapshot feature found in PostgreSQL

## Append Only File (AOF)

Every operations are being recorded down and then replayed to recover up to the present state
![[Untitled.png]]
Similar to how PostgreSQL uses Write Ahead Log (WAL)

## Defining data with user namespace

E.g. user:xxx as key to store email address

Then we can use KEYS user:* to list all keys that are in the target namespace, this will lock up Redis, not recommended in production

## Sequential Scan

Use SCAN command to iterate through cursors. E.g. SCAN 0 MATCH “user:*”

## Scenario: to get the user id with given email

- Set the key and value pair with email “user_email” as namespace E.g. “user_emai:test@gmail.com” “user_id”
- Then use GET [KEY] to perform query
- With this we can check if any user registered with the given email

## Redis Hashes (like dictionary / json)

- Use HMSET for insertion
![[Untitled 1.png]]

- Use HGETALL for retrieval
![[Untitled 2.png]]

- Use HSET to add field
![[Untitled 3.png]]

- Use HDEL to remove field
![[Untitled 4.png]]
- If the given key has no more field, it will be deleted too

## Redis sorted sets

- Use ZADD for upserting records, 10 is the record value to be sorted
![[Untitled 5.png]]

- Use ZSCORE to retrieve the relevant value
![[Untitled 6.png]]
 
- Use ZINCRBY for upserting records, if the record exists, it will increase by defined value, else new record is being initialized
- Use ZRANGE to sort in ascending orders
- Use ZREVRANGE to sort in descending orders, starting from first to last item
![[Untitled 7.png]]

- Use ZRANGEBYSCORE to filter between ranges, while sorting them, same goes to ZREVRANGEBYSCORE
- +inf means no upper bound, -inf means no lower bound (0)
![[Untitled 8.png]]

## Unique Constraints

- Use SADD to add records
- Use SISMEMBER to check for existing records, if return 1 means the record does exist, else 0
- Requires storing related data throughout 2 different data structures, might add complexity to the data model
![[Untitled 9.png]]

## Transactions (Atomic write)

- Prevent data to be left in partial state
- Solves race condition
- Use WATCH key, this will discard any changes coming from another client, meaning that only the first change will be committed
- Use MULTI to enter transaction mode, noted by (TX)

# Summary

- Redis does not have logical groupings or schemas.
- If data set is small or if speed is crucial, Redis may be worth the additional cost of memory.
- Typically Redis is being used in conjunction with PostgreSQL as a caching layer before the database itself.

# Top 5 Redis Use Cases 

<iframe width="560" height="315" src="https://www.youtube.com/embed/a4yX7RUgTxI?si=dovzSVs0lnshE4gm" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


