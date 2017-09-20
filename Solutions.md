# Solutions to Exercises in *Modern Cryptography: Theory and Practice*

## Chapter 1
1) **What is the difference between a protocol and an algorithm?**
* *A protocol is a well-defined procedure that involves two or more participating parties.*
* *An algorithm is a well-defined procedure that an entity uses to complete a computation or goal oriented processes.*
2) **In Prot 1.1 Alice can decide HEADS or TAILS. This may be an unfair advantage for some applications. Modify the protocol so that Alice can no longer have this advantage. Hint: let a correct guess decide the side.**

    We use the hint, **let a correct guess decide the side** [of the coin], to derive a new protocol.
    
    **PREMISE**: 
    
        Alice and Bob have agreed to use a "magic function" f with properties as specified in Property 1.1.    
        Additionally, a correct guess by Bob is to represent HEADS and an incorrect guess is TAILS.
        
    1. Alice picks a large, random integer `x` and computes `f(x)`.
    2. Alice reads `f(x)` to Bob. Alice also informs Bob of her call, HEADS or TAILS.
    3. Bob tells Alice his guess of `x` as even or odd.
    4. Alice reads `x` to Bob.
    5. Bob verifies `f(x)` and sees the correctness or incorrectness of his guess, resulting in HEADS or TAILS respectively.
    
3) **Let function `f` map from the space of 200-bit integers to that of 100 bit ones with the following mapping rule: 
    ![](https://latex.codecogs.com/gif.latex?f%28x%29%5Cstackrel%7Bdef%7D%7B%3D%7D%28%5Ctext%7Bthe%20most%20significant%20100%20bits%20of%20%7Dx%29%5C%20%5Coplus%5C%20%28%5Ctext%7Bthe%20least%20significant%20100%20bits%20of%20%7Dx%29)**
    1. Is `f` efficient?
    
        Yes. Xor operations are very fast.
    2. Does `f` have the "Magic Property I"?
    
        For `f` to have "Magic Property I", it must satisfy two conditions:
        1. Given `x` it is easy to compute `f(x)`.
        2. Given `f(x)` it is impossible to extrapolate information about `x`.
        
        Since we are focused primarily on determining the parity of `x`, we can limit our simple analysis to 4 distinct cases. Both the 100th and 200th bit are 1's, both are 0's, and each case in which they differ from each other. By building a simple truth table (see below) we can see that parity of the original number's parity bit is not leaked via this hash function assuming all bits are randomly set.
        
        | 100th bit | Parity bit    |  A ^ B    |
        | --------- | ----------    | ------    |
        | 1         | 1             | 0         |
        | 1         | 0             | 1         |
        | 0         | 1             | 1         |
        | 0         | 0             | 0         |
        
        So, yes, `f` has "Magic Property I"
        
    3. Does `f` have the "Magic Property II"?
    
        For `f` to have "Magic Property II" `f(x)` must produce distinct outputs for every input `x`. Upon simple observation we can immediately tell that this is impossible because the domain is ![](https://latex.codecogs.com/gif.latex?2%5E%7B200%7D) and the range is ![](https://latex.codecogs.com/gif.latex?2%5E%7B100%7D) which means that a significant number of collisions must exist. Additionally, we can prove this further by providing a counter example to "Magic Property II". 
        
        ![Counter-example to Magic Property II for Question 1.3.3](https://latex.codecogs.com/gif.latex?%5C%5C%20f%28111...1%29%20%3D%20000...0%5C%5C%20f%28000...0%29%20%3D%20000...0)
        
    4. Can this function be used in Prot 1.1?
    
        No, this function cannot be used for `f` in Prot 1.1 because it does not meet the requirements as stated by the premise.
        
4) **Is an unbroken cryptographic algorithm more secure than a known broken one? If not, why?**

    Generally, no, but it depends. Cryptographic algorithms can be broken to varying degrees so just because an algorithm has been "broken" doesn't mean it is useless or significantly worse off. In fact, due to the fact that the algorithm was broken, we know that it must have been investigated to some degree. Additionally, the degree in which the algorithm has been broken can be an indication to the underlying strength of the algorithm. However, sometimes a proof by reduction to contradiction can be done on unbroken crypto which allows some degree of confidence. 
    
5) **Complex systems are error-prone. Give an additional reason for a complex security system to be even more error-prone.**

    There are plenty of answers that could be used here. One example could be that added complexity invites implementation errors.
