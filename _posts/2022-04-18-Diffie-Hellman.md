\section{Modular arithmetic}
* Zp are integers {0, 1, 2,...., 1-p}
* We let it operations wrap around
* Modulo 7: 6 + 1 = 0
* Congruent if a = b mod p
* If calculation performed mod p we can reduce at each step
* Reduction modulo p is very useful when performing calculations on a computer, since it allows us to represent values in a fixed number of bits
* Curve25519 uses arithmetic modulo the prime number p = 2^255 − 19

\section{Group Theory}
* Set of elements E
* Associative 
* Identity
* Inverse
* Abelian Group - commutative 

\section{Diffie Hellman}
* Allows two parties (Alice and Bob) to establish a shared secret by communicating over an insecure channel, under the assumption that the adversary can only observe but not modify the communication.
* g^k is the group operator applied to g k times
* Alice wants to send message to Bob
* Bob has public key g^k where k is picked randomly by Bob and g is public
* Alice gets Bob's public key g^k
* Alice picks random integer j
* Alice computes g^j and (g^k)^j
* Alice sends g^j to Bob
* Alice encrypts message to using (g^k)^j as the key and sends it to Bob
* Bob now has k, g^j and the encrypted message
* Bob computes (g^j)^k
* (g^j)^k = (g^k)^j
* Therefore Bob can decrypt the message

\subsection{Security assumption}
* g, g^k is public

* Channel is insecure
* Therefore g^j and the encrypted message may also be known by someone other than Alice or Bob
* It must be hard to work out k given g and g^k otherwise (g^j)^k could easily computed and the message decryped (hardness of discrete logs)
* It also most be hard computing (g^j)^k must be hard given only g, g^k and g^j (CDH)
* Also given g, g^j and g^k it must be hard to guess g^j^k Formally (g, g^j, g^k, g^j^k) must have nearly the same probability has (g, g^j, g^k, g^z) where z is random (DDH)