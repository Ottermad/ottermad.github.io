---
layout: post
title: Batches In Cassandra
author: Charles Thomas
---

Batches in Cassandra are an often misunderstood topic and this will hopefully serve as a guide to beginners to help them make sense of them.

In order to understand batches you first have to get your head around partitions. In Cassandra, data is distributed across several computers; to work out which computers a record lives on it has a partition key which is a combination of one or more columns which is used to work out which computers to store the data on.

The partition key forms part of the primary key which is used to uniquely identify every row in a tabe.

For example if I have the following table:
```
CREATE TABLE users (
	user_id text,
	email text,
	name text
	PRIMARY KEY ((user_id), email)
);
```

The primary key is made up of two columns, the user_id and an email. This means every row in the table will have a unique combination of user_id and email. But notice how user_id has an extra set of brackets around it. This means it is the partition key. So this means the user_id will be used to work out which computers the data is stored on.

This means the records:
```
(user_a, dave@test.com, Dave)
(user_b, bob@test.com, Bob)
```

could be stored on different computers since they have different partition keys. Where as the records
```
(user_a, dave@test.com, Dave)
(user_a, david@test.com, David)
```

Will be stored on the same computers because they have the same partition key.

Now we’ve talked about partition keys, we're now able to talk about batches. In Cassandra there are two types of batches: logged and unlogged batches. Unlogged batches are the simplest to understand so we’ll start by looking at them.

Let’s assume I want to write the following two rows to my table:
```
(user_a, dave@test.com, Dave)
(user_a, david@test.com, David)
```

Normally, to do this you would do two writes to Cassandra. So first you would run:
```
INSERT INTO users (user_id, email, name) VALUES (user_a, dave@test.com, Dave);
```

Then you would run:

```
INSERT INTO users (user_id, email, name) VALUES (user_a, david@test.com, David);
```

However, unlogged batches, offer an alternative, they allow you group two writes together. This means you can do:
```
BEGIN UNLOGGED BATCH;
INSERT INTO users (user_id, email, name) VALUES (user_a, dave@test.com, Dave);
INSERT INTO users (user_id, email, name) VALUES (user_a, david@test.com, David);
APPLY BATCH;
```

To understand how this is different from two separate writes we need to understand the concept of co-ordinator nodes in Cassandra. When a client makes a query to Cassandra all the data is sent to a random node in the cluster. This node is known as the coordinator node for that query and it’s job is to look at the partition keys involved for that query and send the queries to nodes that are responsible for those partitions.

When you do two separate writes you usually send each write to a different coordinator node in the cluster, however, when you do an unlogged batch both writes go through the same coordinator node. This begs the question, is this a good thing or a bad thing?  If each write is to the same partition then you may not get this reduction in performance and instead you’ll get both writes applied to nodes together which gives you atomicity and isolation.

However, if multiple partitions are involved then this means one co-ordinator node has to work out the nodes responsible for several partitions which means it does more work this often reduces performance. You also do not get atomicity because the writes could either fail on the set of nodes responsible for one partition but succeed on the nodes for the second partition. Nor do you get isolation because the two sets of writes could be applied at different times.

So what happens if you need atomicity for multiple partitions? Cassandra offers a solution to this in the form of logged batches. Logged batches guarantee atomicity for multiple writes although they do not provide isolation (meaning you may see some of the writes before you see others). They work by first writing the operations to be done to a batchlog which is then sent to two other nodes. Then it will try to perform all the operations in the batchlog, however, if it fails then since the batchlog has been replicated to two other nodes, one of the other nodes will aim to complete the operation. This guarantees that the writes in the batchlog will eventually be performed. However, this is very expensive and can lead to performance issues.

To perform a logged batch you can use the syntax:
```
BEGIN BATCH;
INSERT INTO users (user_id, email, name) VALUES (user_a, dave@test.com, Dave);
INSERT INTO users (user_id, email, name) VALUES (user_b, bob@test.com, Bob);
APPLY BATCH;
```

Hopefully, this explains unlogged batches for single and multiple partitions and logged batches for multiple partitions (Note: you cannot perform logged batches for single partitions because the unlogged batch already provides atomicity)


