# Assignment 2


## Getting Started:
  * Read the README.md file in the redis directory
  * You do not need the redis-server or redis-cli commands as described in your text.
  * Simply start with ./up.bash and ./shell.bash, this will put you into the Redis prompt.

## Day 1
1. (10 points) Read Day 1. Skip section on Unions on page 270. Work through the examples in the text. Save your database to dump.rdb (see README.md).

2. (1 point) What is the URL to Redis' documentation on its commands:
```
https://redis.io/commands/
```

3. (1 point) What is the runtime complexity (in Big-O notation) for LREM?
```
The runtime complexity for LREM is O(n)
```

4. (2 points) Create a structure to hold the value of your address with the key of your first name. For instance, mine would be “heidi”  “CS & IT Department, Herman Hall 207C, Western New England University, Springfield, MA, 01119”. Use the proper Redis command to show that the data has correctly been entered and followed by the results. Show both commands below including the prompts:
```
SET Sri "CS & IT Department, Herman Hall 207C, Western New England University, Springfield, MA, 01119"
OK
127.0.0.1:6379> GET Sri
"CS & IT Department, Herman Hall 207C, Western New England University, Springfield, MA, 01119"
```

5. (2 points) Create a hash structure to hold your WNE user name, first name, last name, and password. Of course provide a fake password. For instance, my data would be: “he302979”, “heidi”, “ellis”, “xxxx”.  Use the proper Redis command to show that the data has correctly been entered followed by the results. Show both commands below including the command prompts:

```
HSET user:Sri username "ss623272" first "Sri Santhi" last "Samineni" password "x23xx"
(integer) 4
127.0.0.1:6379> HGETALL user:Sri
1) "username"
2) "ss623272"
3) "first"
4) "Sri Santhi"
5) "last"
6) "Samineni"
7) "password"
8) "x23xx"
```

6. (2 points) Create a hash that holds your father’s and mother’s names as separate key-value pairs. Use the proper Redis commands to show that the data has correctly been entered followed by the results. Show both commands below including the command prompt:
```
HSET parents:ss623272  father "Srinivas Rao" mother "Vidyadhari"
(integer) 2
127.0.0.1:6379> HGETALL parents:ss623272
1) "father"
2) "Srinivas Rao"
3) "mother"
4) "Vidyadhari"
```

7. (3 points) Use a list to:
    * Create a stack called ‘my_stack’
    * Add elements for pears, apples, peaches
    * Remove the top element
    * Display the list to check that you have removed the proper elements
    * Add oranges to the stack
    * Display the list to check that you have removed the proper elements

Show the commands below including the command prompts:
```
127.0.0.1:6379> LPUSH my_stack pears
(integer) 1
127.0.0.1:6379> LPUSH my_stack apples
(integer) 2
127.0.0.1:6379> LPUSH my_stack peaches
(integer) 3
127.0.0.1:6379> LPOP my_stack
"peaches"
127.0.0.1:6379> LRANGE my_stack 0 -1
1) "apples"
2) "pears"
127.0.0.1:6379> LPUSH my_stack oranges
(integer) 3
127.0.0.1:6379> LRANGE my_stack 0 -1
1) "oranges"
2) "apples"
3) "pears"
```

8.  (3 points)  In class we talked about the problem with name changes. For instance. Jane Ellen Doe might change her name to Jane Ellen Doe Fitzgerald where Ellen Doe becomes Jane’s middle name. Do the following:
    * Create hashes to hold first name of "Jane", middle name of "Ellen" and last names of "Doe".
    * Use Redis’ **transactions** to modify Jane to have a middle name of “Ellen Doe” and a last name of “Fitzgerald”. Remember, we need to ensure atomicity for this action.

Write the commands below including the command prompts:

```
127.0.0.1:6379> HSET person:jane first "Jane" middle "Ellen" last "Doe"
(integer) 3
127.0.0.1:6379> HGETALL person:jane
1) "first"
2) "Jane"
3) "middle"
4) "Ellen"
5) "last"
6) "Doe"
127.0.0.1:6379> MULTI
OK
127.0.0.1:6379> HSET person:jane middle "Ellen Doe"
QUEUED
127.0.0.1:6379> HSET person:jane last "Fitzgerald"
QUEUED
127.0.0.1:6379> EXEC
1) (integer) 0
2) (integer) 0
127.0.0.1:6379> HGETALL person:jane
1) "first"
2) "Jane"
3) "middle"
4) "Ellen Doe"
5) "last"
6) "Fitzgerald"
```

9. (2 points) Create a sorted set that holds the costs of the following items:  Cheetos: $2.99, apple: $1.00, Hershey’s: $3.45, and Coke: $1.79.  Print the set in ascending order.  Reduce the price of Hersheys by $1.00 using the ZINCRBY command. Print the set again in ascending order. Show the Redis commands below including the command prompts:
```
127.0.0.1:6379> ZADD prices 2.99 "Cheetos" 1.00 "apple" 3.45 "Hersheys" 1.79 "Coke"
(integer) 4
127.0.0.1:6379> ZRANGE prices 0 -1 WITHSCORES
1) "apple"
2) "1"
3) "Coke"
4) "1.79"
5) "Cheetos"
6) "2.9900000000000002"
7) "Hersheys"
8) "3.4500000000000002"
127.0.0.1:6379> ZINCRBY prices -1.00 "Hersheys"
"2.4500000000000002"
127.0.0.1:6379> ZRANGE prices 0 -1 WITHSCORES
1) "apple"
2) "1"
3) "Coke"
4) "1.79"
5) "Hersheys"
6) "2.4500000000000002"
7) "Cheetos"
8) "2.9900000000000002"
```

10. (2 points) When using 2-factor authentication, many web sites send the user a link to confirm their identity. These links typically expire within 5 minutes. Reproduce this concept in Redis by storing a key named 'link' whose value is a URL (your choice), that expires in 5 minutes. Do it in a single command. Check to ensure that the link exists. Write the commands below including the command prompts:
```
SET link "https://www.wikipedia.org/" EX 300
OK
127.0.0.1:6379> EXISTS link
(integer) 1
127.0.0.1:6379> TTL link
(integer) 254
```

## Day 2

1. Read the following sections in Day 2. You do not have to "do" them. Just read and study them and know them for the exam. There is nothing to turn in for Day 2.

* Publish-subscribe
* Durability
* Snapshotting
* Append-Only File
* Security
* Master-Slave Replication

## Day 3 - Skip

Submission
1. The following files should contain all your work for this assignment:
    * assignment2.md
    * dump.rdb

 * All work must be committed to your individual GitHub repo to be considered submitted.
 * Confirm your submission by opening your repository in GitHub.
