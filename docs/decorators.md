# Decorators

>A special case of functions

Decorators are functions declared to receive other functions and involve it with some code to be executed. It's very useful when you need that certain routines be always executed together to the main interest routine. In some languages a function used as decorator is an ordinary function with a function block declared inside and the return of that function. In UltraGen decorators are a special case of functions. A type which holds a block of code, must have a function as the last argument and returns a new function "decorated" by itself.

## The basics

You can define a decorator as shown below.

```ruby
decorator myWrapper(f)
    print("code before")
    f()
    print("code after")
end
```

For using the decorator you must declare or reference a function and assign it to a reference (typically a name). That reference can so be called after.

```ruby
# coming from previous example
function myFunc()
    print ('my func here')
end
myDecorated = myWrapper(myFunc)
# myDecorated is the myFunc function
# decorated by myWrapper
# now I can call it
myDecorated()
# code before
# my func here
# code after
```

You can also use an anonymous functions can be used as argument.

```ruby
myDecorated2 = myWrapper (function()
    print('anonymous')
end)
myDecorated2()
# code before
# anonymous
# code after
```

## Decorator parameters

Decorators can be declared with other parameters besides the decorated function. They can be used in the "decorator lines" of function However it doesn't accept variable arguments.

```ruby
decorator myWrapper2(arg, f)
    print("code before 2")
    print(arg)
    f()
    print("code after 2")
end

myFunc = myWrapper2 (2500, function()
    print('this is my func')
end)
myFunc()
# code before 2
# 2500
# this is my func
# code after 2
```

```callout
Decorators must be declared with at least one parameter. The last argument of a decorator is always expected to be a function.:info
callout
```

As you can figure, the decorated function call must follow it's own signature. And you can define parameters in decorated function too.

```ruby
# using previous decorator
funcWithArgs = myWrapper(function(num)
    print(num)
end)
funcWithArgs (9000)
# code before
# 9000
# code after
```

## Stacking decorators

As a decorator call returns a function you can "stack" decorations.

```ruby
# using previous
stacked = myWrapper(
    myWrapper2(1000, 
    function ()
        print("stacked")
    end))
stacked()
# code before
# code before 2
# 1000
# stacked
# code after 2
# code after
```

# Parameters types

Similarly to functions, decorator parameters can also be type hinted. However, the type is checked only at the function call.

```ruby
decorator typedWrapper(String x, fn)
    print(x.upper())
    fn()
end

right = typedWrapper ("ok", function()
    print("inner")
end)

right()
# OK
# inner

wrong = typedWrapper (900, function()
    print("won't run")
end)
# no error raised yet

wrong()
# raises an error due to wrong type
```

Decorator are also first-class citizens, so it has the same reference possibilities as functions.

Decorators can only be declared as core members. However, as will be seen ahead, they can be assigned to class methods by its name.

## Name masking in Decorators

It's possible to mask names in decorators. For understanding this we must analyze how UltraGen decorators work. When you decorate a function you are literally calling a decorator execution. A decorator execution defines a new anonymous function which is the decorator function receiving the decorated function passed as one of it's "internal parameters". The parameters of a decorator call are passed to a specific part of function definition internally stored as "decorator parameters". The next example illustrates it.

```callout
As said, decorator calls defines anonymous functions. This is why you need to assign a decorated function to a variable for calling it later.:info
callout
```

```ruby
decorator wrapper(fn)
    print('before')
    fn()
    print('after')
end

function wrapped()
    print('wrapped')
end

# doing this
decorated = wrapper(wrapped)

# is similar to this
function decorated(fn=wrapped)
    print('before')
    fn()
    print('after')
end

# and the call of 'decorated'
decorated()
# before
# wrapped
# after
```

Very straightforward and not much worthy of concerns until this point. However when parameters enter to the scene things can get a little messy. What would happen if parameters of decorator and decorated function had the same names?

```ruby
decorator wrapper(arg, fn)
    print('before')
    print(arg)
    fn()
    print('after')
end

function wrapped(arg)
    print('wrapped ', arg)
end

# doing this
decorated = wrapper(1000, wrapped)

# is similar to this
function decorated(arg=1000, fn=wrapped)
    print('before')
    print(arg)
    fn(arg)
    print('after')
end

# and the call of 'decorated' with an argument
decorated(500)
# before
# 500
# wrapped 500
# after
```

Very certainly this was not what you want. When defining a decorated function it was expected that the execution would use the value passed in decorator call. The `arg` name was masked by the `arg` name declared in function.

There is no solution for this besides just use a name in decorator which will not probably be used in decorated parameters definition. There is no style guide defined for this. A *dunder* is a suggested choice. A constant parameter (declared with `$`) can also be a choice if possible.

A tip about it is that because of how UltraGen treat scopes, variables of decorator function can be accessed in decorated function. However, it's suggested you don't abuse of this because of the increase of coupling.

And so, we finished the sections about UltraGen blocks of code. In the next we will know about modularizing applications with `include`.
