## Python Basics

#### Math Operators (from Highest to Lowest Precedence)

* Exponent - 2 ** 3 = 8

* Modulus/remainder - 22 % 8 = 6

* Integer division/floored quotient - 22 // 8 = 2

* Division - 22 / 8 = 2.75

* Multiplication - 3 * 5 = 15

* Subtraction - 5 - 2 = 3   

* Addition - 2 + 2 = 4

---

#### Common Data Types

* Integers: -2, -1, 0, 1, 2, 3, 4, 5

* Floating-point numbers -1.25, -1.0, ‑-0.5, 0.0, 0.5

* Strings: 'a', 'aa', 'aaa', 'Hello!', '11 cats'

#### String Concatenation

```python
>>>'Alice' + 'Bob'
'AliceBob'
```

If you try to use the + operator on
a string and an integer value, Python will not know how to handle this, and
it will display an error message.

When the * operator is used on one string
value and one integer value, it becomes the string replication operator.

```python
>>> 'Alice' * 5
'AliceAliceAliceAliceAlice'
```

The * operator can be used with only two numeric values (for multiplication)
or one string value and one integer value (for string replication).

#### Storing Values In Variables

A variable is like a box in the computer’s memory where you can store a
single value.

```python
x = 10

spam = 'Hello World'

pi = 3.14
```

A variable is initialized (or created) the first time a value is stored in it u.
After that, you can use it in expressions with other variables and values v.
When a variable is assigned a new value w, the old value is forgotten (overwriting).

There are 3 important rules to follow when naming variables: 

1. It can be only one word.
2. It can use only letters, numbers, and the underscore (_) character.
3. It can’t begin with a number.

#### Useful functions

### print()

```python
print('Hello World')
```
You can also use this function to put a blank line on the screen; just call print() with
nothing in between the parentheses.

### input()

The `input()` function waits for the user to type some text on the keyboard
and press enter.

You can think of the input() function call as an expression that evaluates
to whatever string the user typed in.

### len()

You can pass the len() function a string value (or a variable containing a
string), and the function evaluates to the integer value of the number of
characters in that string.

```python
>>> print(len('hello'))

5
```

### str()

The `str()` function can be passed an integer value and will evaluate to a string value version of it:

```python
>>> print('I am ' + str(29) + ' years old.')

I am 29 years old.
```

### int()

The int() method returns an integer object from any number or string.

```python
>>> int('42')
42
```

The `int()` function is also useful if you need to round a floating-point
number down.


```python
>>> int(7.7)
7
>>> int(7.7) + 1
8
```

### float()

The float() method returns a floating point number from a number or a string.

```python
>>> float('3.14')
3.14
>>> float(10)
10.0
```

---
### Text and Number Equivalence

Although the string value of a number is considered a completely different
value from the integer or floating-point version, an integer can be equal to a
floating point.

```python
>>> 42 == '42'
False
>>> 42 == 42.0
True
>>> 42.0 == 0042.000
True
```
