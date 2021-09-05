---
layout: post
title: An Introduction To Kafka
author: Charles Thomas
---
* Idempotency: If a producer writes a message and see a network error it cannot know if this error happened before or after the message was committed. You can turn on a setting so that the broker assigns each producer an ID and deduplicates messages using a sequence number that is sent by the producer along with every message (we can only guarantee idempotent production within a single producer session)

## What is Kafka?
Apache Kafka is an events streaming platform. This means it provides 3 keys features: 
* The ability to write events
* The ability to store those events durably 
* The ability to read back those events

This allows you to move data between differently applications in order to build bigger pieces of software. For instance, you might write an event to Kafka every time a user updates their email address then read that event in your analytics software to allow it work out how often people change their email.

## How is Kafka set up?
Kafka consists of 3 main pieces: 
* Producers - this is any piece of software that writes data to Kafka - this might be your production application
* Consumers - this is any piece of software that reads data to Kafka
* Brokers - these are the servers that store the data e.g. Kafka itself

You can have many copies of each of these. For example, you may have multiple instances of your application that write data to several brokers. Then that data is read from multiple brokers by many copies of your analytics software.

## Events
Events (also called messages) in Kafka are the pieces of data you write. Each event belongs to a topic. In our previous example, our events that correspond to a user updating their email could belong to a `user_email_updated` topic.

Within a topic, events are split into partitions. Each event belong to one partition. Partitions have two key properties:
* They're ordered - within in partition all events are stored and read in a consistent order 
* They're replicated - we'll cover this below.

## Replication
Because you can have multiple brokers, you can store an event multiple times so it is not lost in the case of a broker failure. The smallest thing you can replica in Kafka is a partition. You can configure how many times a partition should be replicated. So if you configure a partition to have a replication factor of 3, the entire partition will be stored on 3 different brokers. 

Replication in Kafka uses a leader-follower model. This means each partition is assigned a leader broker and then a number of follower brokers (a broker can be the leader for one partition and the follower for others). When a write occurs it first goes to the leader then is replicated to the followers. Only once it has been replicated to the followers is the write considered 'committed' and will be available for consumers to read.

## Writing messages
To write a message the producer has to specify a topic and a partition for the message. The topic is specified by the user. 

To figure out which partition the message should belong to there are several options which the user can use. You could specify the partition at random - this is useful if you do not care about reading the messages in order and just want to spread the load out. Alternatively, you could use a hash function which takes in a key then hashes it to work out which partition to use. For example, if I wanted all the events for a user to belong to the same partition I could hash the user's ID to figure out which partition to use.

Finally, a producer also needs to know which broker is the leader for the partition it wants to write to. Thankfully, each broker keeps a record of the leader for each partition. So a producer only has to contact any broker and ask them.

When a producer writes a message it can choose whether or not to wait for the message to be committed (replicated to the followers). This determined by the acks setting.

## Reading messages
Consumers are responsible for reading messages from Kafka. Every consumer belongs a consumer group. A consumer group is responsible for reading a topic (you can have multiple consumer groups consuming the same topic). Each consumer within a consumer group will be assigned a number of partitions and only it will read those partitions. 

For example, if topic A has partitions 1,2 and 3 and consumer group B has two consumers X and Y. Then consumer X may be assigned the partitions 1 and 2 and consumer Y will be assigned the partition 3. This means the consumer group will read the whole partition but a given consumer will only read part of it.

Every partition stored ordered as an ordered log on the broker. A consumer reading a partition does so by specifying what position in the log it wants to read (this is called the offset). A consumer can read the log in order by just increasing its offset. It can also replay old messages by resetting the offset.

The offset a consumer is currently on can be stored in Kafka in order to allow the consumer to restart after a crash.

When reading a message, the consumer has a choice. It can persist its offset (either to Kafka or some other data store) before it process a message or it can process the message and then persist the offset. 

If it persists the offset first then this leads to "at-most-once" semantics. This means each message will be processed at most once but messages may be not be processed at all. This would happen in the case where a consumer writes the offset, then crashes and then on restarts increments the offset so the message it was originally is not processed.

If it persists the offset after processing the message this creates "at-least-once" semantics. This means every message will be processed but some may be processed multiple times. This would occur when a consumer reads a message, processes it then crashes before it can store the offset. This means when it restart it will reread that message.

## In order consumption
One of the popular reasons to use Kafka is because it allows you to consume messages in order. This is because each partition is stored as an ordered log and therefore can be read in order. 

Therefore, it you have a set of messages you want to make sure are consumed in order when you have to make sure they are assigned to the same partition. In practice, this means making sure they all have a common key you can hash to work out what partition they should go to. This is often the ID of entity they're related to. For example, if you are storing a list of changes to a user you might use the user id as the key.s

## Exactly once

## Further reading
* https://www.microsoft.com/en-us/research/wp-content/uploads/2017/09/Kafka.pdf
* https://kafka.apache.org/documentation/#semantics
* https://docs.google.com/document/d/11Jqy_GjUGtdXJK94XGsEIK7CP1SnQGdp2eF0wSw9ra8/edit
* https://medium.com/@jaykreps/exactly-once-support-in-apache-kafka-55e1fdd0a35f