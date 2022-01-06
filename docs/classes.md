# Classes

>The UltraGen types interface

As said before, UltraGen is a primarily object oriented language - even it has some functional capabilities and is able to be used in a procedural style. Every value in UltraGen is an object. The types are interfaced to the developer by the keyword "class".

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

# 7
# instance use
myClassInstance = new MyClass(0, 1) # executes init constructor
myClassInstance.someInstance() # prints "some instance", "0" and "1"

# static use
MyClass.someStatic() # prints someStatic
MyClass.someFunc() # prints "anonymously assigned
print(MyClass.someVar) # prints "99"
```

### 1 - Declaring a class
The class keyword defining a new type/class.

### 2 - The constructor block
An optional constructor. If not provided, a default constructor with no statements and no arguments is used. If provided, declared parameters is assigned to instance attributes automatically. In this example, `arg1` and `arg2` will be available as instance attributes of object. The usual "class block" that other languages has for defining attributes in UltraGen is the constructor. This is the block where you define the instance attributes of a class as done with `otherAttr`.
The constructor declaration must be followed by the keyword `self` indicating that the method is an instance method.

### 3 - Declaring a static method
The syntax for declaring a static method is very alike a regular function. The difference is you must write a colon and the class to whom that method belongs.

### 4 - Declaring an instance method
The syntax for declaring an instance method is very alike a regular function. The difference is you must write a colon and the class to whom that method belongs and the `self` keyword after the class name. This tells to interpreter to provide a reference to the own object in the function block accessible through the `self` keyword.

### 5 - Declaring static attributes
As class declarations does not has blocks, you declare static attributes as regular variables but with a reference to the class where they belong. As with methods, this can be done in any file. You just must guarantee that all the values you need are available

### 6 - Declaring static methods with anonymous functions
As a static variable can receive any value, this value can also be an annonymous function. The syntax is the same for static variables. Only static methods can be declared this way.

### 7 - Using class/instance methods/attributes in application
For calling methods from class you just need to call them preceeded by the name of the class or the instance according to use. As with regular functions it's possible to chain method calls.

## About UltraGen object orientation

After explaining the syntax for dealing with classes, let's talk about class charateristics in UltraGen.

## Declare methods/static attributes apart from class declarations

It can be done in any file, in any part of application. You only must guarantee that when the file which has the method declared is executed the reference to the class exists.

Example:

`MyClass.ultra`

```ruby
class MyClass
```

`otherFile.ultra`
```ruby
function myFunc() : MyClass
    print("I'm in another file")
end
```

`main.ultra`
```ruby
include 'otherFile.ultra'
# will raise an error
# as MyClass does not exist
```

**How to fix this?**

```ruby
class MyClass

include 'otherFile.ultra'
```

`main.ultra`
```ruby
include 'MyClass.ultra'

MyClass.myFunc()
# no errors. When 'MyClass.ultra' is included, it includes 'otherFile.ultra' without errors
# When 'otherFile.ultra' is executed, the class MyClass is already declared
```

While this may seem a little bit complicated, remember it's not much different from `.pp` or `.inc` files featured in pascal, where you can declare parts of a unit in another file and the files are included during the compilation process.

## UltraGen class features

At this time (and it's something that may change in future) UltraGen does not feature the most of ideas behind OOP. UltraGen does not feature *abstract classes* or *methods*, *interfaces*, *class inheritance*, *traits* and access modifiers.

The first reason for this is because at the OOP point UltraGen is more near from Python, giving the developer the freedom to handle these questions at his own responsibility. That is why it has no *private* or *protected* access modifiers.

The second is that for the purpose UltraGen is mainly built (process views from provided data) this is enough. It's the minimum required for a decent functionality organization. However, some of these features may appear in the interpreter at some time but they are really not a priority now.

## Now it's time for tricks

Even UltraGen does not feature these functionalities, some of them may be emulated using some technics. From now on we'll show some of them.

### Inheritance

Inheritance may be emulated by declaring a function which takes a class (parent), add some functions to it (child) and returns an instance of the "improved" type with new functions declared.

The example shows how this works

```ruby
class Parent

function fromParent() : Parent self
    print('from parent')
end

function ChildOne()
    Klass = Parent
    function fromChild() : Klass self
        print('from ChildOne')
    end
    return new Klass()
end

function ChildTwo()
    Klass = Parent
    function fromChild() : Klass self
        print('from ChildTwo')
    end
    return new Klass()
end

co = ChildOne()
ct = ChildTwo()
p = new Parent()

co.fromChild()
ct.fromChild()

co.fromParent()
ct.fromParent()

co.fromChild()
ct.fromChild()
```

This code has the following output

```text
from ChildOne
from ChildTwo
from parent
from parent
from ChildOne
from ChildTwo
```

Obviously, the bad thing about this trick is that the functions of children classes will be declared every time a new object is instantiated. Our best suggestion for overtaking this lack of feature is to use composition instead of inheritance.

```ruby
class Parent

function someFunction() : Parent self
    print('simulating a super call')
end


function otherFunction() : Parent self
    print('calling other function')
end

class Child

function init(parent) : Child self
end

function someFunction() : Child self
    print("I'll call my 'parent'")
    self.parent.someFunction()
end

parent = new Parent()
child = new Child(parent)

child.someFunction()
child.parent.otherFunction()
```

This prints:

```text
I'll call my 'parent'
simulating a super call
calling other function
```