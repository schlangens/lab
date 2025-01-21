## Tip Calculator Project
We're going to build a tip calculator.

If the bill was $150.00, split between 5 people, with 12% tip.

Each person should pay:

(150.00 / 5) * 1.12 = 33.6

After formatting the result to 2 decimal places = 33.60

## Data types
- String
- Integer
- Float
- Boolean

Pulling a certain element out of a string is called subscripting.

### Subscripting
- ``print("Hello"[0])``

You can use negative numbers
- ``print("Hello"[-1])``
- This will pull the last character.

### String
- ``print("123" + "345")``

### Integer = Whole Number
- ``print(123 + 345)``

### Large Integers
- ``print(123_456_789)

### Float = Floating Point Number
- ``print(3.14159)``.  Anything with a decimal, a decimal can float around

### Boolen (T/F)
- ``print(True)``
- ``print(False)``

### TypeError, Checking and Conversion
TypeError: These occur when you are using the wrong data type. e.g.``len(12345)``.
Because you can only give the ``len()`` function Strings. It will refuse to work and give you a TypeError if you give it a number (Integer).


### Typechecking
You can check the data type with the following:
- ``type("Hello")``

- ``print(type("abc))``
- ``print(type(123))``
- ``print(type(3.13))``
- ``print(type(True))``

### Type Conversion (Type casting)
Convert the data type to what we want.
- ``int("123")``
- ``print(int("123" + int("456"))``
A ValueError is when we try to convert something that we can not. For instance making a string "abc" into ``int``. 

- ``int()``
- ``float()``
- ``str()``
- ``bool()``

```
name_of_the_user = input("Enter your name")
length_of_name = len(name_of_the_user)
```

- Check the datatypes from the TypeError

```
print(type("Number of letters in your name: ")) #str
print(type(length_of_name)) #int
```

- We have to convert to str then concatenate

```
print("Number of letters in your name: " + str(length_of_name))
```




