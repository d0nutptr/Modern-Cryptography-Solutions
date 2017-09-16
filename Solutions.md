# Solutions to Exercises in *Modern Cryptography: Theory and Practice*

## Chapter 1
1) **What is the difference between a protocol and an algorithm?**
* *A protocol is a well-defined procedure that involves two or more participating parties.*
* *An algorithm is a well-defined procedure that an entity uses to complete a computation or goal oriented processes.*
2) **In Prot 1.1 Alice can decide HEADS or TAILS. This may be an unfair advantage for some applications. Modify the protocol so that Alice can no longer have this advantage. Hint: let a correct guess decide the side.**

    In the original protocol, Alice, effectively, acts as the coin flipping mechanism. With or without bias, Alice decides the state of the coin. It is up to Bob to determine the face of the coin. If Alice is biased, Bob has an increased chance in determining the 

    Using the hint *"let a correct guess decided the side"* we can determine that the author wanted us to base HEADS or TAILS off of the correctness of Bob's guess. With this in mind, 
