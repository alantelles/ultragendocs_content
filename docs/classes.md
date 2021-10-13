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
function someStatic() : MyClass
    print("some static")
end

# 3
function someInstance() : MyClass self
    print("some instance")
end
```

(To be continued)
