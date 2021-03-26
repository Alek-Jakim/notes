## Lecture 0 - Starting from scratch

### What is computer science?
---
* Computer science is fundamentally problem solving.

* We can think of problem solving as the process of taking some input (details about our problem) and generate some output (the solution to our problem).

### Representing numbers
---
* **Unary** - We might start with the task of taking attendance by counting the number of people in a room. With our hand, we might raise one finger at a time to represent each person, but we won’t be able to count very high. This system is called unary, where each digit represents a single value of one.

* **Decimal** - We’ve probably learned a more efficient system to represent numbers, where we have ten digits, 0 through 9. This system is called decimal, or base 10, since there are ten different values that a digit can represent.

* **Binary** - Computers use a simpler system called **binary**, or base two, with only two possible digits, 0 and 1. Each binary digit is also called a **bit**.

Since computers run on electricity, which can be turned on or off, we can conveniently represent a bit by turning some switch on or off to represent a 0 or 1.

* **Transistors** - Inside modern computers, there are not light bulbs but million of tiny switches called transistors that can be turned on and off to represent different values.

In binary, with just two digits, we have powers of two for each place value:

2<sup>2</sup> 2<sup>1</sup> 2<sup>0</sup>

For example:  
![](./bin-ex.png)
2<sup>0</sup> = 1  
2<sup>1</sup> = 2  
2<sup>2</sup> = 4  

And so on...in the end, we add up the numbers above the 1s, in the example above, we add 32 + 16 + 2 = 50.

* **Converting decimal to binary:**  
1. Divide the number by 2.
2. Get the integer quotient for the next iteration.
3. Get the remainder for the binary digit.
4. Repeat the steps until the quotient is equal to 0.

![](./convert-bin.png)

Let's take the number 60, for example:  
60 / 2 = 30 --> the quotient is 30, remainder 0  
30 / 2 = 15 --> the quotient is 15, remainder 0  
15 / 2 = 7 --> the quotient is 7, remainder 1  
7 / 2 = 3 --> the quotient is 3, remainder 1   
3 / 2 = 1 --> the quotient is 1, remainder 1  
1 / 2 = 0 --> the quotient is now 0, remainder 1

So the number 60 converted to binary is 11100