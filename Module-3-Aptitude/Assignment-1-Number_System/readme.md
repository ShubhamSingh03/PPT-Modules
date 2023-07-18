# Assignment-1 Questions & Solutions

## Divisibility

💡 **Question-1:**  Which one of the following numbers is divisible by 99?
a) 3572404 b) 135792 c) 913464 d) 114345

💬 **Solution-1:** Option D) 114345 is div. by 99

<hr/>

💡 **Question-2:** If n is an integer, what is the remainder when (2n + 2)<sup>2</sup>
is divided by 4?

💬 **Solution-2:** 

```
(2n + 2)^2 = (2n + 2) * (2n + 2)
= 4n^2 + 4n + 4

remainder when (4n^2 + 4n + 4) is divided by 4 is 0
```

<hr/>

💡 **Question-3:** Find two nearest numbers to 19506 which are divisible by 9?

💬 **Solution-3:** Two nearest numbers to 19506 that are divisible by 9 are *19497* and *19512*.

<hr/>

💡 **Question-4:**  What is the value of M and N respectively if M39048458N is divisible by 8 and 11, where M and N are single digit integers?

💬 **Solution-4:** 

```
To find the values of M and N such that M39048458N is divisible by 8 and 11, we can apply the divisibility rules for these two numbers.

Now let's look at the number M39048458N.

Divisibility by 8:
To check the divisibility by 8, we need to examine the last three digits, which are "458." This number is not divisible by 8 because 458 is not a multiple of 8.

Divisibility by 11:
Next, let's apply the divisibility rule for 11. The alternating sum of the digits is:

(3 - 9 + 0 - 4 + 8 - 4 + 5 - 8) = -3

Since -3 is not a multiple of 11, the entire number M39048458N is not divisible by 11.

Since M39048458N is not divisible by either 8 or 11, there are no single-digit integer values for M and N that satisfy the given condition.
```

<hr/>

💡 **Question-5:** How many pairs of X and Y are possible in the number 763X4Y2, if the number is divisible by 9?

💬 **Solution-5:** 

```
For the number to be divisible by 9, the sum must be divisible by 9. Therefore: (7 + 6 + 3 + X + 4 + Y + 2) ≡ 0 (mod 9)

Simplifying: (22 + X + Y) ≡ 0 (mod 9)

Now, let's find all the possible values of X and Y that make (22 + X + Y) divisible by 9.

The possible pairs of X and Y that satisfy this condition are:

1. X = 1, Y = 4 (22 + 1 + 4 = 27, which is divisible by 9)
2. X = 2, Y = 3 (22 + 2 + 3 = 27, which is divisible by 9)
3. X = 3, Y = 2 (22 + 3 + 2 = 27, which is divisible by 9)
4. X = 4, Y = 1 (22 + 4 + 1 = 27, which is divisible by 9)

So, there are four pairs of X and Y (1 and 4, 2 and 3, 3 and 2, 4 and 1) that make the number 763X4Y2 divisible by 9.
```

<hr/>


💡 **Question-6:** When the integer n is divided by 8, the remainder is 3. What is the remainder if 6n is divided by 8?

💬 **Solution-6:** 

```
When the integer n is divided by 8, the remainder is 3 as: n ≡ 3 (mod 8)

Now, we need to find the remainder when 6n is divided by 8.

Step 1: Express 6n in terms of n
6n = 6 * (n ≡ 3 (mod 8))

Step 2: Distribute the 6 on the right side of the congruence
6n ≡ 6 * 3 (mod 8)

Step 3: Calculate 6 * 3
6 * 3 = 18

Step 4: Find the remainder when 18 is divided by 8
18 ÷ 8 = 2 with a remainder of 2

So, the remainder when 6n is divided by 8 is 2.
```

<hr/>

💡 **Question-7:** If the product 4864 x 9P2 is divisible by 12, then what is the value of P?

💬 **Solution-7:** 

```
To determine the value of P, we need to find the possible values of P that make the product 4864 x 9P2 divisible by 12.

Divisibility Rule for 12:
A number is divisible by 12 if it is divisible by both 3 and 4.

Step 1: Check divisibility by 4
A number is divisible by 4 if its last two digits form a multiple of 4.

Since 4864 is divisible by 4 (64 is a multiple of 4), we can conclude that 4864 x 9P2 is divisible by 4 for any value of P.

Step 2: Check divisibility by 3
A number is divisible by 3 if the sum of its digits is divisible by 3.

Let's find the sum of the digits in 9P2: 9 + P + 2 = 11 + P

For 4864 x 9P2 to be divisible by 3, (11 + P) must be divisible by 3.

Possible values of P that make (11 + P) divisible by 3 are P = 1 and P = 2.

Therefore, the possible values of P are 1 and 2.
```

<hr/>

💡 **Question-8:** ) If the number 7X86038 is exactly divisible by 11, then the smallest whole number in place of X?

💬 **Solution-8:** 

```
Applying Divisibility rule of 11 for the number 7X86038:

Alternating sum = (7 - X + 8 - 6 + 0 - 3 + 8) = (22 - X)

For the number to be divisible by 11, the alternating sum must be divisible by 11. Therefore: (22 - X) ≡ 0 (mod 11)

The smallest whole number value of X that makes (22 - X) divisible by 11 is X = 0.

Let's check: Alternating sum = (22 - 0) = 22

Since 22 is divisible by 11, the number 7X86038 is exactly divisible by 11 when X = 0.
```

<hr/>

💡 **Question-9:** If an integer n is divisible by 3, 5 and 12, what is the next larger integer divisible by all these numbers?
a) n<sup>2</sup> b) n + 180 c) 2n d) n + 60

💬 **Solution-9:** Option B)

<hr/>

💡 **Question-10:**  What is the product of the largest and the smallest possible values of M for which a number 5M83M4M1 is divisible by 9?

💬 **Solution-10:** 

```
For 5M83M4M1 to be divisible by 9, the sum of its digits (21 + 3M) must be divisible by 9.

So, 21 + 3M ≡ 0 (mod 9)

To find the possible values of M, we need to find the multiples of 3 between 21 and 9 (as the result must be divisible by 9).

Multiples of 3 between 21 and 9 are 21 and 18.

So, the possible values of M are:

1) M = 0 (if 21 + 3M = 21, which is divisible by 9).
2) M = 3 (if 21 + 3M = 30, which is divisible by 9).

Now, we need to find the product of the largest and smallest possible values of M:

Product = Largest M * Smallest M
        = 3 * 0
        = 0

So, the product of the largest and smallest possible values of M is 0.
```

<hr/>