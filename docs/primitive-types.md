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

### *idStrings*

There is a syntax sugar for strings that are valid names. They are the **idStrings**. They are ordinary  strings and support all of its methods. The only difference is that they written with a colon followed by a name.

```ruby
x = :aName
print (typeof(x))
# will print "String"
```

This form exists for better semantics in cases where an argument is a string but a form that seems like an identifier is better readable. Let's take a look at this snippet which shows a Router handler definition. Don't matter about the router. Focus at concept.

These definitions require a route, a name for that endpoint and a function as arguments.

```ruby
# the second arg must be a string
router.get('/some/path', 'myRoute', handler)
# now written in idString syntax
router.get('/some/path', :myRoute, handler)
```

In the first form, "myRoute" seems like it could be any literal value. In fact it is but in this context "myRoute" is an identifier of a route. So the idString syntax make this more evident by dropping the quotes.

In your script, you can use this name to reverse return a route with `router.urlFor(:myRoute)`. It's visible that `:myRoute` looks much more like an identifier than `"myRoute"`. Another good case of use is to define or access dictionary keys which presents the same semantics. In the next snippet we're getting hypothetical information from a user as JSON and the fields are *name*, *username*, *age*.

```ruby
resp = Request.get("/user/someone")
user = JSON.parse(resp.text)
print(user[:name])
print(user[:age])
print (user[:age])
```

Again we made the fields look like identifiers with this simples syntax change.

That said, when you're in a case like that, use *idStrings*.

## Boolean

**Boolean** is the type for representing boolean values. They can be only `true` or `false`. The most important thing to talk about this type is to show its "truthy" and "falsy" values. This definition is used in `if` and `while` evaluations.

### Truthy and falsy values

In an `if` or `while` condition, some non-boolean values are taken as true or false so you can write a little less. We call this conventions **truthy** and **falsy**

#### Are truthy:

- Any string with length greater than zero.
- Numerics greater than 0
- A list with length greater than 0
- A non-empty dictionary
- Any object except `null`

#### Are falsy:

- An empty string
- Numerics less than or equal 0
- A list with 0 length
- An empty dictionary
- The `null` object.

Remember that you can't compare different types. So, even though an empty string is evaluated as `false` you can't make a `"" == false` comparison. It will return a type error and advice that you can't compare different types. If you need something like this, type cast the value with `bool`. It uses the same rules to evaluate a value as true or false.

## NullType

This is the type for holding the `null` object. Internally it's not a null pointer reference. Even `null` is an object internally in UltraGen. So, set some variable to `null` does not "dereference" it. It just sets a variable to a value that has no specific value. It's like the `var` declaration in some languages just for initialize some variable. Consider that such statement does not exist in UltraGen. A variable must be initialized with a value. If you don't have one but you need the name to exist, use `null`.

## One step forward

In the next chapter we will talk about the composed types. This mean types who are composed by other but are also core types from UltraGen.
