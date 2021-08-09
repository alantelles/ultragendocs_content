# Decorators

>A special case of functions

Decorators are functions declared to receive other functions and involve it with some code to be executed. It's very useful when you need that certain routines be always executed together to the main interest routine. In some languages a function used as decorator is an ordinary function with a function block declared inside and the return of that function. In UltraGen decorators are a special case of functions. A type which holds a block of code, must have a function as the last argument and returns a new function "decorated" by itself.

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
