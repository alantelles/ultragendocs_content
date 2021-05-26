# Basic syntax

>The UltraGen syntax guide for writing your applications.

Let's now introduce you to the basic UltraGen syntax. UltraGen is a imperative language which programs are composed by statements or blocks of statements and expressions. Statements are delimited by a new line. Blocks are delimited by a line with keyword and an `end` keyword. Expressions are statements that return something.\n\n## Comments\n\nLet's start with comments as we will use it in examples. You comment a line with a `#`. You can comment a block (multiline comment) starting it by `###` and ending with `###!`.

```ruby
# a line of comment
###
A block
Of comment
Also called
Multiline comment
###!
```
# Names
UltraGen is a case-sensitive language. `value` is different from `Value`.
UltraGen valid names must match the regex `^\\$?[_A-Za-z_][A-Za-z0-9_]*$`
Are examples of valid names: `someVar`, `_topZeira`, `fooB4r`, `$mahalo`, `$_STRONG`.
Are invalid names: `5omeVar`, `test$`, `foo-bar`.
Names declared starting with a `$` are constants, that is, its values can't be changed.
## Variables
UltraGen is a dynamically and strongly typed language. You don't need to declare variable or constant type however you can't mix types in operations. Here are some examples.
```ruby
num = 10 # num is assumed to be an integer
num = "It's assumed to be a string"
$drop = 'this is immutable'
$drop = 99 # raises an error
```

## Boolean and null

Boolean values are specified using the words `true` for true values, `false` for false ones.

The null value is represented by keyword `null`.

## Operators

UltraGen supports basic math operations, Boolean operations and concatenation. The operators for these are described below.

### Concatenation

You can concatenate strings with the `+` sign. You can also use the `+=` to append a value to a string.

```ruby
print("hello" + " " + "world")

# will print "hello world"
a = "hello "
b = "world"
a += b
print(a)
# will print "hello world"
```

### Math

Math can be done using the operators `+` for addition, `-` for subtraction, `*` for multiplying, `/` for division, `//` for integer division and `%` for modulus.  The decimal operator is the `.` character.

```ruby
x = 7 + 10 # 17
y = 1.4 - 1 # 0.4
a = 3 * 5 # 15
b = 23 / 5 # 4.6
c = 23 // 5 # 4
d = 23 % 5 # 3
```

UltraGen also supports shortcut for math operators except modulus.

```ruby
x = 10
x += 10 # x is now 20
x -= 5 # x is now 15
x *= 2 # x is now 30
x /= 10 # x is now 3
x //= 2 # x is now 1
```

### Logic

UltraGen supports *and*, *or* and *not* operations through `&&`, `||` and `!` symbols.

```ruby
x = true
y = false
r = x && y # r is false
r = x || y # r is true
r = !x # r is false
```
### Comparisons

UltraGen supports greater than, greater or equal, less than, less or equal, different and equal comparisons. For this purpose the symbols `>`, `>=`, `<`, `<=`, `!=` and `==` respectively are used.

```ruby
a = 10
c = 20
r = a > c # false
r = a < c # true
r = a >= c # false
r = a <= c # true
r = a != c # true
r = a == c # false
```

## Operations precedence and associativeness

UltraGen uses standard mathematics behavior for operations. Multiplication and division are evaluated before addition and subtraction. However operations inside parenthesis have higher precedence. 

Math operations have higher precedence over Boolean operations.

```ruby
r = 2 + 3 * 4 # r is 14
r = 10 - 5 + 3 # r is 8
r = (2 + 3) * 4 # r is 20
r = 8 + 2 > 9 # r is true
```

## Blocks

All blocks are declared by its function in language followed by expressions as arguments, a newline, the block itself, another newline and the `end` keyword.

Here is a function example.

```ruby
function foo(bar)
    print (bar)
    end
```

## Conditionals

`if` is the only conditional available in UltraGen. Comparisons can be done with the following syntax:

```ruby
a = 99
if (a < 100)
    print('less than 100')
end
# will print "less than 100"
```
You can also declare an `else` block to be executed when condition is not attended.

```ruby
a = 99
if (a > 100)
    print('greater than 100')
else
    print('less than 100')
end
# will print "less than 100"
```

You can even use the `elsif` to test other conditions.

```ruby
a = 100
if (a > 100)
    print('greater than 100')
elsif (a == 100)
    print('equal 100')
else
    print('less than 100')
end
# will print "equal 100"
```

## List

Lists are declared with the values separated by `,` and wrapped by a `[` and a `]`.

```ruby
l = [0, 1, 2]
```

## Dictionaries

Dictionaries are declared with its values inside `{` and `}` using a `,` to separate them. Key and value are assigned by a `:`. You can use the *idString* syntax if your key is a valid name.

```ruby
a = {'key': 'value', :otherKey : 1000}
```

>Dictionaries and lists will be more explained ahead.

## Iterations

Iterations in UltraGen can be done through keywords `for` and `while`. 

*For* loop receives can receive a `List`, a `String` or an `Integer` as source and a name to use inside the block that receives the value of each item at current iteration. Additionally, a variable with the same preceded with a `_` is available containing the index.

```ruby
for (["one", "two", "three"], i)
    print('item ', _i, ': ', i)
end
# will print
# item 0: one
# item 1: two
# item 2: three
for ("text", i)
    print('item ', _i, ': ', i)
end
# will print
# item 0: t
# item 1: e
# item 2: x
# item 3: t
for (3, i)
    print('item ', _i, ': ', i)
end
# will print
# item 0: 0
# item 1: 1
# item 2: 2
```

*While* loop is also available receiving a logical expression as condition to still running it's internal block.

```ruby
i = 0
while(i < 3)
    print(i)
    i += 1
end
# will print
# 0
# 1
# 2
```

## You're ready to go now!

For now, you got all basic resources to start to write your UltraGen application. Keep walking through documentation so you can learn more about it.

Good hacking!