---
layout: post
title: Basic Quantum Computing - Quantum Key Distribution
author: Charles Thomas
---

In this post, we're going to take a look at what encryption is and how quantum computing can help with it using quantum key distribution

## Encryption and Keys
Encryption is the art of encoding messages so that other people can't read them. This is extremely useful in all sorts of applications from protecting your WhatsApp messages to securing top secret data.

Encryption relies on the idea of keys: these are pieces of information used to encrypt or decrypt the encrypted data. e.g. to decrypt some encrypted information you need a key.

However, if I want you to decrypt some data that I encrypted then I need to somehow give you the key. But how can I do this in such a way that no one else can get the key?

This is where Quantum Key Distribution comes in


## Quantum Key Distribution
Quantum Key Distribution solves the problem of how Alice and Bob can share a key between them without anyone else being able to find the key.


### Alice sends a qubit
It starts with Alice. She starts by randomly generating a bit which is either 0 or 1. This will be the first bit of her secret key.

She then generates a second random bit. This is going to tell her how to encode the first bit in a qubit for Bob.

If the second bit is 0 then she sends the first bit to Bob as a qubit in the following way:

$$0 \to \ket{0}$$

$$1 \to \ket{1}$$

This is called using the Z basis

If the second bit is 1 then she sends the first bit to Bob as a qubit as:

$$0 \to \ket{+} = \frac{\ket{0} + \ket{1}}{\sqrt{2}}$$

$$1 \to \ket{-} = \frac{\ket{0} - \ket{1}}{\sqrt{2}}$$

This is known as using the X basis

Alice makes a note of her two bits and then sends her qubit to Bob

### Bob receives a qubit
This means Bob receives a qubit in one of 4 states:

$$\ket{0}, \ket{1}, \ket{+}, \ket{-}$$

Bob then generates a random bit himself and makes a note of it. If it is 0 then he will measure in the Z basis, if it is 1 he will measure in the X basis.

If he picks a different basis to the one Alice used to encode the bit then he might get the wrong answer.

For example, if he measures 

$$\ket{+}$$

in the Z basis then since

$$\ket{+} = \frac{\ket{0} + \ket{1}}{\sqrt{2}}$$

He will get 0 50% of the time and 1 50% of the time

And if he measures 

$$\ket{0}$$ 

in the X basis then since

$$\ket{0} = \frac{\ket{0} + \ket{1}}{\sqrt{2}} + \frac{\ket{0} - \ket{1}}{\sqrt{2}} = \frac{\ket{+} + \ket{-}}{\sqrt{2}}$$

He will get + 50% of the time - 50% of the time

## Getting the key
Alice and Bob repeat this process many times - let's say n times.

Alice will then tell Bob and anyone else which basis she used to encode her bit (e.g. her second random bit)

Bob will then check which basis he measured in (e.g. which random bit he generated). If they match then he keeps that result, if he doesn't he gets rid of it. And he announces which ones he had to get rid of.

So in the end they are left with m bits where m < n

## Worked example
This has all been a bit abstract and confusing so let's work through an example.

Alice starts by generating a random bit. She generates 1

She then generates a second random bit. She gets a 0.

So she sends Bob a qubit in the state:

$$\ket{1}$$

Bob receives the qubit. He then generates a random bit. He generates 1 so he measures it in the X basis so he gets a +

They then repeat this process several 4 times which is summarised in the following table

| Number | Alice's First Random Bit | Alice's Second Random Bit | Qubit sent to Bob | Bob's Random Bit | Basis used to measure Qubit | Bob's result |
|--------|--------------------------|---------------------------|-------------------|------------------|-----------------------------|--------------|
| 1      |       1                  |           0               |    $$\ket{1}$$    |        1         |                   X         |  $$\ket{+}$$ |
| 2      |       1                  |           1               |    $$\ket{-}$$    |        1         |                   X         |  $$\ket{-}$$ |
| 3      |       0                  |           0               |    $$\ket{0}$$    |        0         |                   Z         |  $$\ket{0}$$ |
| 4      |       1                  |           0               |    $$\ket{1}$$    |        1         |                   X         |  $$\ket{+}$$ |
| 5      |       0                  |           1               |    $$\ket{+}$$    |        1         |                   X         |  $$\ket{+}$$ |

Now Alice tells the world which basis she used to encode the 5 qubits - e.g. the
shares her second randomly generated bits.

Bob now compares that with the basis he used to measure the qubits e.g. did he 
generate the same random bit as Alice so they're left with the following qubits

| Number | Alice's First Random Bit | Alice's Second Random Bit | Qubit sent to Bob | Bob's Random Bit | Basis used to measure Qubit | Bob's result |
|--------|--------------------------|---------------------------|-------------------|------------------|-----------------------------|--------------|
| 2      |       1                  |           1               |    $$\ket{-}$$    |        1         |                   X         |  $$\ket{-}$$ |
| 3      |       0                  |           0               |    $$\ket{0}$$    |        0         |                   Z         |  $$\ket{0}$$ |
| 5      |       0                  |           1               |    $$\ket{+}$$    |        1         |                   X         |  $$\ket{+}$$ |

Bob has gotten rid of qubits 1 and 4. So he tells Alice this.

This means Alice and Bob now share a secret key of 100

## Eavesdroppers
But how can Alice and Bob be sure that no one intercepted the qubits that Alice sent to Bob.

Well if someone, say Eve, did manage to intercept the qubit she wouldn't know what basis it is in.
Since Alice doesn't tell anyone that until after Bob receives all the qubits.

This means she can't make a copy of the qubit because of the [no cloning theorem]({% post_url 2023-09-23-QC-Course-No-Cloning %}).

And if she tries to measure it herself there is a 50% chance she'll pick the wrong basis.
If she picks the wrong basis then she will disturb the state so when Bob measures it he will get 
a random result.

To see the outcomes let's take a look at this table

| Alice's Basis | Eve's Basis | Bob's Basis | Outcome                                                          |
|---------------|-------------|-------------|------------------------------------------------------------------|
| Z             | Z           | Z           | Eve gets to know what Alice sent Bob without disturbing anything |
| Z             | X           | Z           | Eve randomly gets 0 and 1 but tampers with Bob's result          |
| Z             | Z           | X           | Alice's and Bob's basis don't match so discarded                 |
| Z             | X           | X           | Alice's and Bob's basis don't match so discarded                 |
| X             | Z           | Z           | Alice's and Bob's basis don't match so discarded                 |
| X             | X           | Z           | Alice's and Bob's basis don't match so discarded                 |
| X             | Z           | X           | Eve randomly gets 0 and 1 but tampers with Bob's result          |
| X             | X           | X           | Eve gets to know what Alice sent Bob without disturbing anything |

Let's now just look at the cases where Alice and Bob don't discard the 
bits (since in those cases it doesn't matter what Eve has done)

| Alice's Basis | Eve's Basis | Bob's Basis | Outcome                                                          |
|---------------|-------------|-------------|------------------------------------------------------------------|
| Z             | Z           | Z           | Eve gets to know what Alice sent Bob without disturbing anything |
| Z             | X           | Z           | Eve randomly gets 0 and 1 but tampers with Bob's result          |
| X             | Z           | X           | Eve randomly gets 0 and 1 but tampers with Bob's result          |
| X             | X           | X           | Eve gets to know what Alice sent Bob without disturbing anything |

So there is a 50% chance that Eve can know a bit of the secret which means
that Eve can know about half our secret key on average.

But Alice and Bob can try to detect her. When Eve picks the wrong basis, she causes the 
qubit to collapse into a random state so when Bob measures it again, he will
get a random result. So there is 50% that when Bob does his measurement it won't
match Alice's.

To see this let's imagine Alice sends Bob 1 in the Z basis so sends the qubit:

$$\ket{1}$$

Eve picks the wrong basis so measures this in the X basis. Since

$$\ket{1} = \frac{\ket{+}-\ket{-}}{\sqrt{2}}$$

She measures + 50% and - 50% of the time. Let's assume she measures +

So Bob will then receive

$$\ket{+} = \frac{\ket{0}+\ket{1}}{\sqrt{2}}$$

He then does a measurement in the Z basis so he could get 0 or he could get 1.

So to try and detect the evaesdropper, Alice and Bob take the first k bits of their secret key
and compare them (this means the first k bits are no longer secret). If
any of them don't match then they know that someone has been eavesdropping. 
So they can start the whole process again

## Summary

So in summary, we have looked at how Alice and Bob can share a secret key
between them and then detect any eavesdroppers so they know their key is secure.

If you enjoyed this post please do give me a follow (if you're reading this on medium)
or sign up to my newsletter [here](https://charliethomas.substack.com/)
