Checking the datatypes in python
--------------------------------
x = 2
isinstance(x, int)
True

type(x)

x == "Hello" #This will check for the string, if the x type is not string it return false

is operator in python
---------------------
Comparision is done by the is operator

x = 2
x is int


Python data types
----------------
Integer: python integers are theoritically inifinite in size, infact integer size is limited by the size of yours computers memory
binary: 0b11111
octal : 0o1111
hexadecimal: 0x123, Binary, octal, hexadecimal are the types of the python integer data types

Int can also used to convert the hexadecimal string representation to number just like
myvalue = int('AB2', 16)
int(True) => 1
int(False) => 0


Float
-----
float('123.13') => 123.13
float(12.3) => 12.3
float(False) => 0.0

decimal
----------
Python float data types suffer from the precision, so python also supports the decimal use that one.

fractions
----------
Decimal and rational fractions are used to alleviate the issue posed by the floating point arithmetic

complex data types 
--------------------
python also supports the complex data types

Boolean
--------
Python also supports the boolean data types which are True, and False, default value is False
bool() yields the False value
Integer with the 0 values are false and anything else is True
Float with the 0.0 value is also false and other is true

bitwise operation in python
-----------------------------
Python also support bitwise operation
1. & ->  bitwise ading
2. | ->  bitwise oring
3. ^ ->  bitwise not
4. ~ ->  bitwise xor
6. << -> bitwsie left shift
7. >> -> bitwise right shift

None
-----
The none type represent the null object
None is the default return value of the python 
None is considered to have the boolean value of False



pthon collections types
========================
Python has, list, dictionary, tuple, sets, bytes, string 
A standard module collections provides several other specialized collections types,
