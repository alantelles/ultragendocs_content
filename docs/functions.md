# Functions

>Declaring reusable code blocks

**Function** is the UltraGen type for storing code blocks. They are defined by the keyword `function` followed by a valid name or by parentheses on case of closures.

For calling functions, you must use the name followed by parentheses.

```ruby
function hello() # declaring at root scope
    print('hello')
end
hello() # calling function
# hello
```

```callout
A thing worth to note as already said in primitive types doc and different from many languages the return of this function is an empty string and not null as the default return of a function is its live stream.:success
callout
```

Functions can be declared with parameters so can be executed with arguments. Parameters are declared in a sequence of valid names inside parentheses.

```ruby
function greet(name)
    print("Hello, ", name)
end
greet("Alan") # Hello, Alan
```

You can set default values to parameters by writing `param=someValue`. Any expression can be used. 

```ruby
function greet(name="Stranger")
    print("Hello, ", name)
end
greet() # Hello, Stranger
greet("Alan") # Hello, Alan
```

```callout
You can't declare a parameter without a default value after a parameter with a default value.:warning
callout
```

You can declare a function with a variable number of parameters adding a __*__ after the closing parentheses. The arguments after the positional parameters are available inside the function via the `$varArgs` variable which is a list.

```ruby
function vari(a)*
    print(a)
    print($varArgs)
end
vari(100, 99, 98, 97)
# 100
# [99, 98, 97]
```

It's also provided a variable called `$funcArgs` which is a list that holds all arguments used in function call, including variable arguments.

```ruby
function vari(a)*
    print(a)
    print($varArgs)
    print($funcArgs)
end
vari(100, 99, 98, 97)
# 100
# [99, 98, 97]
# [100, 99, 98, 97]
```

```callout
These special names are more useful when declaring decorators which will be seen ahead.:success
callout
```

## Referencing functions by name

A function is a [first-class citizen](https://en.m.wikipedia.org/wiki/First-class_citizen) in UltraGen. It means that it can be assigned to a variable and accessed like any other value. However built-in internal functions are an exception to this. The name of a function is an accessible name. And a function can be a value referenced by any reference entity.

```ruby
function someBlock()
    print('this is a block')
end
otherName = someBlock
# note the lack of parentheses
# we're referring to value of name someBlock
# not executing someBlock
otherName() # this is a block'
# we are executing otherName
# which points to function defined with someBlock name
```

## Anonymous functions

UltraGen also allows declaring of anonymous functions. The syntax is the same, with same possibilities but without the use of a name.

```ruby
myFunc = function ()
    print("I'm anonymous")
end
myFunc() # I'm anonymous
```

## Assigning anonymous functions to other references

Even though we're using names to show these features, any reference index can be used such as lists or dictionaries values. They are called using it's reference followed by parentheses.

```ruby
funcDict = {
    'f1': function ()
        print("This is the F1")
    end,
    'f2': function () 
        print("This is the F2")
    end
}
funcDict['f1']() # This is the F1
myIndex = 'f2'
funcDict[myIndex]() # This is the F2

funcList = []
funcList.append(function ()
    print("I'm in list")
end)
funcList.append([])
funcList[1].append(function ()
    print("I'm inside the list inside the list")
end)
funcList[0]() # I'm in list
funcList[1][0]() # I'm inside the list inside the list
```

## Getting functions attributes

You can get some information of the functions through the function type attributes.

At the current version of UltraGen are available the `$paramCount` which returns the number of parameters used in declaration and the `$isVarArgs` which tells if the function is declared with support to variable arguments.

## Expanding lists when calling function

If you function is declared with various parameters you can expand lists when calling it. The expanded arguments must match the number of declared parameters. To expand lists preceed the list with a __*__(asterisk).

```ruby
function multi(a, b, c)
    print(a, b, c)
end
function multi2(a, b, c, d, e, f)
    print(*$funcArgs)
end
vals = ["val1", true, 99]
multi(*vals, "mid", *range(2)) # val1 true 99 mid 0 1
```

## Conclusion

One thing to remember is that all described features also apply to methods.

Names starting with `$` are also valid to functions and are also treated as constants.

Now that you know how to use functions in UltraGen we will pass to two special cases of functions with some caveats. Decorators and lambdas.

