# Primtive types

>The base types for expressing values in UltraGen

In this article we'll discuss the types used for coding your applications in UltraGen. The base types are Integer, Float, Byte, String, Null, Boolean.

Variables of these types are always accessed by value. At this time you can't define explicitly a mode to access variables. Primitive always by value. Composed types always by reference.

## Numeric

Numeric values are held by the self explanatory **Integer**, **Float** and **Byte** types. The byte type holds an integer between 0 and 255. In fact, when using it, the number has the same behavior of an integer.

Float holds a real number. Internally it's a floating point number with 80-bit precision (the **extended** FreePascal data type). 

Integer holds any operation result that returns an Integer number. Even if a float is involved in operation. If the return is an integer number, the result is an integer.

All numeric types can be mixed in an operation.

## String

The type for storing textual data. Strings are stored as a raw byte stream. That said, the correct output will depend from the viewer expected encoded. Anyway, built-in functions which relies on text match are based on UTF-8 and may fail when using non-ASCII characters. For these cases you can use the **ByteStream** and handle raw bytes very easily.

Literal strings may be enclosed in single or double quotes if they are on same line. You can declare a multiline string using triple quotes. Single quote doesn't need to be escaped inside double quoted literal and vice-versa. Neither single or double quotes need to be escaped. 

```ruby
sq = 'this can have " without problems"
dq = "this can have ' and it's ok"
tq = """this can even
use a newline
inside the string"""
```

The character `\` can be used to escape some character. Some escape combinations produces special features in string.

Combination|Produces
-----|-----
\n|newline
\t|tab
\r|carriage return

When writing strings that are Windows paths you must double the slashes.

```ruby
path = "my\windows\path.exe"
# wrong: the string will be "mywindowspath.exe"
path = "my\\windows\\path.exe"
# this is right
```
However, the most recommended is to use the `path` method from **List** type to handle file paths.

```ruby
path = ['my', 'windows', 'path.exe'].path()
```
