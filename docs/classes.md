# Classes

>The UltraGen types interface

As said before, UltraGen is a primarily object oriented language - even I has some functional capabilities and is able to be used in a procedural style. Every value in UltraGen is an object. The types are interfaced to the developer by the keyword "class".

```callout
The words class and type will be used interchangeably and refer to the same feature.:info
callout
```
## Syntax

To create a class you just need to declare it with the class keyword and the name of the class which must follow the UltraGen valid name rule.

```ruby
class MyClass
```

### "Where's the block?"

Different from other languages UltraGen syntax doesn't define a block for declaring the attributes of your class. From now on the syntax for declaring class components will be presented.

## Full example

For this feature, a full explained example will fit better for illustrating classes declaration.

```ruby
# 1
class MyClass

# 2
function init(arg1, arg2) : MyClass self
    self.otherAttr = "some attribute"
end

# 3
function someStatic() : MyClass
    print("some static")
end

# 4
function someInstance() : MyClass self
    print("some instance")
    print(self.arg1)
    print(self.arg2)
end

# 5
MyClass.someVar = 99

# 6
MyClass.someFunc = function()
    print('anonymously assigned')
end
```

1. The class keyword defining a new type/class
2. An optional constructor. If not provided, a default constructor with no statements and no arguments is used. If provided, declared parameters is assigned to instance attributes automatically.
