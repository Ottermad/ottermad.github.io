---
layout: post
title: Concurrent Programming and Distributed Systems 
author: Charles Thomas
---

# Concurrent Programming
What is concurrency? Concurrency is all about getting a computer doing many things at the same time. You may have come across the idea that computers have multiple cores - it would be nice if we could use all them at the same time to speed things up. Additionally, a lot of tasks that computers do involve a lot of waiting around, for example, if a program has to make a network request, e.g. fetch some data over the internet, then that program is doing nothing while it waits. It would be more efficient if we could have our program do something else while it's waiting. The key idea of concurrency is break down our program into small chunks that can run independently.

## Python and GIL
Different programming languages support concurrency to different amounts. One common challenge that interpreted languages ,like Python, face is called Global Interpreter Lock. The idea here is that in an interpreted language works by having a program called the interpreter read a line of code then immediately executing it before moving onto the next line. 

This makes it hard to do concurrency as you need to have multiple copies of interpreter - one for each unit of code which is running at the same time.

## Golang Introduction
To get around this, we are going to working in Go, a nicer language for learning about concurrency. I'm going to assume you haven't seen Go before but it's fairly easy to read so let's dive in. To follow along you can use your browser by going to [https://go.dev/play/](https://go.dev/play/)

Let's start by writing hello world

```go
package main

import (
    "fmt"
)

func main() {
    fmt.Println("Hello world")
}
```

Going line by line, the 1st line is just something that tells the Go compiler this is a file it should try and run. Then we have some import statements, these are similar to other programming languages. Finally, we have our main function which is the first thing the computer runs when it executes our code.

Now let's look at how to write functions in Go.

```go
package main

import (
    "fmt"
    "time"
)

func say(s string) {
    for i := 0; i < 5; i++ {
        time.Sleep(100 * time.Millisecond)
        fmt.Println(s)
    }
}

func main() {
    say("Hello")
    say("World")
}
```

This works the same as def in Python, the only key difference is that Go is statically typed which means that variables have an associated type and we have to tell the program what type something is.

## Go-routines
As a gentle, introduction to concurrency we would like to run our calls to the say function at the same time. This easy to do:

```go
package main

import (
    "fmt"
    "time"
)

func say(s string) {
    for i := 0; i < 5; i++ {
        time.Sleep(1000 * time.Millisecond)
        fmt.Println(s)
    }
}

func main() {
    go say("Hello")
    say("World")
}
```

All we had to do was add the keyword go and then that function will execute on its own. In Go, these two functions are said to be running on different go-routines. You can think of a go-routine as a independently executing task.

## Speeding things up with concurrency
To look at a slightly more useful example of concurrency, let's write a simple program to search a list

```go
package main

import (
    "fmt"
)

func search(list []int, target int) bool {
    for _, item := range list {
        if (item == target) {
            return true
        }
    }
    return false
}

func main() {
    list := []int{1,2,3,4,5}
    fmt.Println(search(list, 3))
    fmt.Println(search(list, 0))
}
```


## Communicating between go-routines
To speed it up, we can split our list up into smaller pieces and search each piece separately

```go
package main

import (
    "fmt"
)

func search(list []int, target int) bool {
    fmt.Printf("I'm searching %v for %d\n", list, target)
    for _, item := range list {
        if (item == target) {
            return true
        }
    }
    return false
}

func search_concurrent(list []int, target int) bool {
    midpoint := len(list) / 2
    first_half := list[:midpoint]
    second_half := list[midpoint:]
    in_first_half := search(first_half, target)
    in_second_half := search(second_half, target)
    return in_first_half || in_second_half
}


func main() {
    list := []int{1,2,3,4,5}
    fmt.Println(search_concurrent(list, 3))
    fmt.Println(search_concurrent(list, 0))
}
```

We would like to do search each piece at the same time and we can use the go keyword to do that. However, we need some way of getting our results back from each independently searching go-routine. To do this, we will use what is called a channel. 

A channel can be thought of pipe that can be used to send data from one go routine to another

```go
package main

import (
    "fmt"
)

func search(list []int, target int, c chan bool) {
    fmt.Printf("I'm searching %v for %d\n", list, target)
    for _, item := range list {
        if (item == target) {
            c <- true
        }
    }
    c <- false
}

func search_concurrent(list []int, target int) bool {
    c := make(chan bool)
    midpoint := len(list) / 2
    first_half := list[:midpoint]
    second_half := list[midpoint:]
    go search(first_half, target, c)
    go search(second_half, target, c)
    in_first_half, in_second_half := <- c, <- c
    return in_first_half || in_second_half
}


func main() {
    list := []int{1,2,3,4,5}
    fmt.Println(search_concurrent(list, 3))
    fmt.Println(search_concurrent(list, 0))
}
```

What we have done is create a channel that accepts booleans (true or false values) and then passed it our search function. Our search function then puts either true or false onto the channel. Then we get the data back out and once we have gotten two pieces of data back out from the channel we use them.


## Concurrency Issues
Let's now look another example. We will write a simple bank account program that allows us to move money between accounts.

```go
package main

import (
    "fmt"
)

type Account struct {
    name string
    balance float32
}

func move_money(from *Account, to *Account, amount float32) {
    if (from.balance >= amount) {
        to.balance += amount
        from.balance -= amount
    } else {
        fmt.Println("Not enough money")
    }
}

func main() {
    alice := &Account{name: "Alice", balance: 50}
    bob := &Account{name: "Bob", balance: 30}
    fmt.Printf("%v %v \n", alice, bob)
    move_money(alice, bob, 10)
    fmt.Printf("%v %v \n", alice, bob)
    move_money(bob, alice, 50)
    fmt.Printf("%v %v \n", alice, bob)
}
```

Now we would like to do many transactions at the same time. So let's do this

```go
package main

import (
    "fmt"
    "time"
)

type Account struct {
    name string
    balance float32
}

func move_money(from *Account, to *Account, amount float32, delay time.Duration) {
    if (from.balance >= amount) {
        to.balance += amount
        time.Sleep(delay)
        from.balance -= amount
    } else {
        fmt.Println("Not enough money")
    }

}

func main() {
    alice := &Account{name: "Alice", balance: 50}
    bob := &Account{name: "Bob", balance: 30}
    fmt.Printf("%v %v \n", alice, bob)
    go move_money(alice, bob, 10, time.Millisecond*100)
    go move_money(alice, bob, 50, 0)
    time.Sleep(time.Millisecond * 1000)

    fmt.Printf("%v %v \n", alice, bob)
}
```

We shall see why we have added the delay function to be able to simulate one of our go-routines, pausing randomly for a little bit. This is entirely possible even if we didn't put the delay function in and we'll look at some examples of how this happens in the real world later. 

Now, when we run this code, we see something not great - Alice ends up with a negative balance. This is because the first go-routine checks Alice's balance and sends the money to Bob but then pauses before it deducts the money from Alice. This gives the second go-routine to check Alice's balance and decide she has enough money to do the transaction. So both transactions happen.


### Locks
We would like to solve this problem and one way to do it is make sure only one go-routine can read/write to people's balances at once. We can do this using the concept of a mutex (also called a lock)

```go
package main

import (
    "fmt"
    "time"
    "sync"
)

type Account struct {
    name string
    balance float32
    lock sync.Mutex
}

func move_money(from *Account, to *Account, amount float32, delay time.Duration) {
    from.lock.Lock()
    to.lock.Lock()
    if (from.balance >= amount) {
        to.balance += amount
        time.Sleep(delay)
        from.balance -= amount
    } else {
        fmt.Println("Not enough money")
    }
    from.lock.Unlock()
    to.lock.Unlock()
}

func main() {
    alice := &Account{name: "Alice", balance: 50}
    bob := &Account{name: "Bob", balance: 30}
    fmt.Printf("%v %v \n", alice, bob)
    go move_money(alice, bob, 10, time.Millisecond*100)
    go move_money(alice, bob, 50, 0)
    time.Sleep(time.Millisecond * 1000)

    fmt.Printf("%v %v \n", alice, bob)
}
```

The idea is that each account has a lock associated with it and when we call Lock, any other go-routine has to wait before it get access to that lock. 

### Deadlocks
This solved our original problem but it has introduced another, to make it more obvious what the problem is let's tweak our code a little bit

```go
package main

import (
    "fmt"
    "time"
    "sync"
)

type Account struct {
    name string
    balance float32
    lock sync.Mutex
}

func move_money(from *Account, to *Account, amount float32, delay time.Duration) {
    from.lock.Lock()
    time.Sleep(delay)
    to.lock.Lock()
    if (from.balance >= amount) {
        to.balance += amount
        from.balance -= amount
    } else {
        fmt.Println("Not enough money")
    }
    from.lock.Unlock()
    to.lock.Unlock()
}

func main() {
    alice := &Account{name: "Alice", balance: 50}
    bob := &Account{name: "Bob", balance: 30}
    fmt.Printf("%v %v \n", alice, bob)
    go move_money(alice, bob, 10, time.Millisecond*100)
    go move_money(bob, alice, 20, 0)
    time.Sleep(time.Millisecond * 1000)

    fmt.Printf("%v %v \n", alice, bob)
}
```

Notice that nothing seems to happen - no money is moved. This is because the two go-routines that move the money get deadlocked. What this means is that one of them is waiting for Alice's lock and the other is waiting for Bob's lock but those locks are held by the other so are never released.

## Stop the World Pauses
Finally, let's talking quickly about how these random pauses can actually occur in real life. One of the most famous reasons these can occur is called stop the world pauses

# Distributed Systems
## Why might we want distributed systems
We've talked about how to get a program doing many things at once and now we're going to expand this idea to having many programs spread across multiple machines all working together

Can anyone think of any reasons why we might want to do this?

It usually boils down to 2 reasons

* Scalability
* Reliability


## Databases
We're also going to assume that all applications are basically databases in the sense that we want to be able to read data from them and then write data back to them.

## Reliability
We're going to discuss reliability first. 

So let's start with the simplest application where we have one database on one computer. How could we make this more reliable?

### Primary/Secondary Setups
One idea is to have a backup. But how do we keep our backup in sync? 

One option is to stream data from the primary database to the back up. But can anyone see any problems with this?

Well, there is always a slight delay between our primary and our backup. So it's always possible our main database will fail before a write is completed to the backup.

### Leaderless
How can we get around this? Well one solution is to only consider a write successful only if we can write to both. Then we do a read from one of the two.

But can anyone see the problem with this? Well it doesn't actually make us any more reliable - if we can't write to both nodes then we can't actually complete our write so we're not more reliable.

But what happens if we use 3 databases and say a write is successful if we write to 2/3. This way we can afford to lose 1 of nodes and we can keep writing to our database.

Let's talk a bit more about reading. Let's imagine, when we want to do a read, we read from only 1 of the 3 nodes. What are the problems? 

Well for a write to succeed it only needs to be written to 2/3 of the nodes so if we read from a single node it might not have the data we're looking for. How can we solve this?

One way is to read from all 3 and then do a vote. We compare the 3 answers from all 3 nodes if one result wins 2/3 of the vote - we take that to be the right answer. Otherwise we can't do the read.

Can we every not be able to do a read? Well if one of the nodes is offline then we could write to 2/3 and drop 1 of those 2. Then the missing one could come back online so when we do a read we get 2 different values.

Is there any other case?

One option is our writes happen in different orders? 

To explain why this can happen we need to talk about networks. The thing to understand is networks can have random delays: cables can be different lengths, switches can go wrong. So if we try to do write A and then write B they might arrive at different nodes at different times and importantly in different orders.

So if we do 3 writes very close together, they could occur in 3 different orders on the 3 nodes. So when we try to read back the data, we get 3 different answers so our vote never works.

Can we prevent this somehow? One way is to get the writer to put a timestamp on each of the operations, then we can use the timestamp, to determine if we should do the write.

However, this can create problems and this is because of clock-skew. Clock-skew is the idea that computer clocks are unreliable. Firstly, over time, the physical hardware can drift and run slightly fast or slightly slow. Secondly, computers clock may not be set correctly and keeping them in sync is hard. There is a protocol called NTP usually used to keeping computer clocks but it has some quirks - including one where time can go backwards.

This means if we have one client writing to one record it might be okay but if we have multiple clients writing to the same record we could run into problems.

We would like to solve this - we would like that if we do a write then it will have definitely happened and happened in a definitive order. This is called the problem of distributed consensus and is what we look at this afternoon.

## Scalability
Now let us turn to the problem of scalability. When we need to scale a system it is usually for two reasons

* Too much throughput (e.g. too many reads/writes) for a single computer
* Too much data for a single computer


## Data
Let's assume we have too much data for a single computer. We need to split our data up some how so it's not all on one computer. 

One way to do this is to put all the data for a particular entity on a particular database. For example, I put all the data for business A on database A, the data for business B on database B and so on. 

This approach works and it is called sharding. But it runs into a couple of problems. Firstly, what happens if I need to do queries over entities on different databases? Secondly, I need to know which database to use for a particular entity. This oftens means my application becomes more complex to handle this. But it can be done and Instagram even did it.

A second approach is called consistent hashing. In this approach, we take each table in our database and pick a column(s) to use a key. Then we use this value of this key for each row to decide which nodes to store the data on.

However, this means to read back a particular row we need to know the key for that row so we can find the nodes it is on.

### Throughput
Now, let's turn to the situation where we can store the data but we have too many read requests.

One solution is caching. So we have a separate really fast (usually in-memory) copy of some of our data. Then when we want to read our data we check our super-fast cache and only if it's not there do we go check our database. 

Can anyone see a problem with this? We might read stale/out-of-date data. This brings us (briefly) onto the topic of cache invalidation. This is how do we decide when data in the cache is out of date and should be removed?

One common approach, is to say after a particular time period, let's kick the piece of data from the cache. This prevents anything from getting too stale. 

Another approach, often used in combination, with the previous one is that when we do a write use that write to kick data out of the cache.

Let's now talk about another potential approach. Let's go back to our primary/secondary database set up. If we have too many reads then we could start reading from our back up. We could also have many backups doing the same thing

But what if we're not okay with stale reads? Well that is more subtle but we can use it by combining what we did we did in the reliability section and the too much data scalability section.

Let's start with 9 nodes. Let's use our technique of consistent hashing to make sure each piece of data is on 3 of the 9 nodes. Now when we do a read, we can use the key to only query 3/9 of the nodes. This means we can spread out the reads over several computers.

We can go even further and combine it from our techniques in the reliability section to make sure our reads and writes work as we expect. 

These are the ideas that underlie several popular databases including Cassandra and DynamoDB.