---
layout: post
title: An Introduction To Kafka
author: Charles Thomas
---

Apache Kafka is a very powerful piece of software. But it can very confusing to get started with. The aim of this post is to outline the structure of Kafka and how it might be helpful to you.

## What is Kafka?
Apache Kafka is an events streaming platform. This means it provides 3 keys features: 
* The ability to write events
* The ability to store those events durably 
* The ability to read back those events

This allows you to move data between applications to build bigger pieces of software. For instance, you might write an event to Kafka every time a user updates their email address. Then read that event in your analytics software to allow it work out how often people change their email.

## How is Kafka set up?
Kafka consists of 3 main pieces: 
* Producers - this is any piece of software that writes data to Kafka  e.g.  your production application
* Consumers - this is any piece of software that reads data from Kafka
* Brokers - these are the servers that store the data e.g. Kafka itself

You can have many copies of each of these. For example, you may have multiple instances of your application which write data to several brokers. Then that data is read from multiple brokers by many copies of your analytics software.

## Events
Events (also called messages) in Kafka are the pieces of data you write. Each event belongs to a topic. In our previous example, our events that correspond to a user updating their email could belong to a `user_email_updated` topic.

Within a topic, events are split into partitions. Each event belong to one partition. Partitions have two key properties:
* They're ordered - within a partition all events are stored and read in a consistent order 
* They're replicated - we'll cover this below.

## Replication
Because you can have multiple brokers, you can store an event multiple times. This means it is not lost in the case of a broker failure. The smallest thing you can replica in Kafka is a partition. You can configure how many times a partition is replicated. If you configure a partition to have a replication factor of 3, the entire partition will be stored on 3 different brokers. 

Replication in Kafka uses a leader-follower model. This means each partition is assigned a leader broker and  many follower brokers . A broker can be the leader for one partition and the follower for others. 

When a write occurs it first goes to the leader then is replicated to the followers. Once it has been replicated to the followers the write considered 'committed' and will be available for consumers to read.

## Writing messages
To write a message the producer has to specify a topic and a partition for the message. The topic is specified by the user. 

To figure out which partition the message should belong to there are several options. You can specify the partition at random - this is useful if you do not care about reading the messages in order and want to spread the load out. Or, you can use a hash function which takes in a key then hashes it to work out which partition to use. For example, if I wanted all the events for a user to belong to the same partition I could hash the user's ID to figure out which partition to use.

Finally, a producer also needs to know which broker is the leader for the partition it wants to write to. Thankfully, every broker keeps a record of the leader for each partition. So a producer only has to contact any broker and ask them.

When a producer writes a message it can choose whether to wait for the message to be committed (replicated to the followers). This determined by the acks setting.

## Duplicate messages
It is possible to write duplicate messages to Kafka. Imagine the case where a producer sends the request to write a message to Kafka. It then crashes before it receives its response. When it restarts it could try and write the message again. In some cases you do not want duplicate messages.

To prevent this you can turn on a setting so that the broker assigns each producer an ID (which is static) and sequence number (which increases over time). When a producer writes a message it sends its ID and sequence number alongside the message. Kafka can then deduplicate messages using that have the same sequence number and producer ID.

## Reading messages
Consumers are responsible for reading messages from Kafka. Every consumer belongs a consumer group. 

A consumer group handles reading a topic (you can have multiple consumer groups consuming the same topic). Each consumer within a consumer group will be assigned a number of partitions and only it will read those partitions. 

For example, imagine topic A has partitions 1,2 and 3 and consumer group B has two consumers X and Y. Then consumer X may be assigned the partitions 1 and 2 and consumer Y will be assigned the partition 3. This means the consumer group will read the whole partition but a given consumer will only read part of it.

Every partition stored as an ordered log on the broker. A consumer reading a partition does so by specifying what position in the log it wants to read (this is called the offset). A consumer can read the log in order by increasing its offset. It can also replay old messages by resetting the offset.

The offset a consumer is currently on can be stored in Kafka to allow the consumer to restart after a crash.

When reading a message, the consumer has a choice. It can persist its offset (either to Kafka or some other data store) before it process a message. Or it can process the message and then persist the offset. 

If it persists the offset first then this leads to "at-most-once" semantics. This means each message will be processed at most once but messages may be not be processed at all. This would happen in the case where a consumer writes the offset then crashes. On restart it increments the offset so the message is skipped.

If it persists the offset after processing the message this creates "at-least-once" semantics. This means every message will be processed but some may be processed multiple times. This would occur when a consumer reads a message, processes it then crashes before it can store the offset. This means when it restart it will reread that message.

## In order consumption
One of the popular reasons to use Kafka is because it allows you to consume messages in order. This is because each partition is stored as an ordered log and therefore can be read in order. 

Therefore, if you have a set of messages you want to make sure are consumed in order when you have to make sure they are assigned to the same partition. In practice, this means making sure they all have a common key you can hash to work out what partition they should go to. This is often the ID of entity they're related to. For example, if you are storing a list of changes to a user you might use the user id as the key.s

## Exactly once
It is also possible to get "exactly-once" semantics using Kafka. This means you can guarantee that each message will be processed exactly once. This is different to the "at-most-once" or "at-least-once" semantics discussed above. 

To do this you need the ability to process your message and store that you've processed it (normally done by storing the offset) in one operation. This way either you process and store it that you've processed it or you do nothing at all. 

There are several ways to go about this. If you are using the events from Kafka to update a relational database, you could store the offset in the same database. This way you could use a transaction to do your original write and update the offset in one go.

Alternatively, Kafka itself offers the ability to write a group of messages in a transaction. This means you can send several messages to Kafka and either they will all be written or none of them will be. This means if you use Kafka to store the output of your processing and to store your offsets you can also achieve exactly once semantics.

You will also need to have enabled impotency on your writes as discussed above.

## Summary
Hopefully, you now have a better understanding of Kafka and you can get started with using it.

## Further reading
* https://www.microsoft.com/en-us/research/wp-content/uploads/2017/09/Kafka.pdf
* https://kafka.apache.org/documentation/#semantics
* https://docs.google.com/document/d/11Jqy_GjUGtdXJK94XGsEIK7CP1SnQGdp2eF0wSw9ra8/edit
* https://medium.com/@jaykreps/exactly-once-support-in-apache-kafka-55e1fdd0a35f