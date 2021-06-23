# Getting started

>Get started to UltraGen basic concepts and know what you can do with it.

UltraGen is a object oriented scripting language with support to plain text for template processing purposes. Initially it was designed for generating XML for use in some media managers machines used in broadcast TV production. The need of more control over processing than just "templating" was perceived. At this time the scripting capabilities we're added to engine. Soon it was noticed that as it's used for processing XML it could be used to process HTML and send it as http responses. At this point UltraGen was redesigned as a script language with template processing capabilities.

Additionally, many resources for building web applications are implemented. Handle requests, a embedded web server, sessions control, and others.

Another feature is the possibility of use UltraGen scripts fully integrated with FreePascal applications due it's fully written in FreePascal. It turns possible to use it with other frameworks or in any project where you need text processing or any other thing you prefer to write in UltraGen than FreePascal. For this, UltraGen provides interfaces that allow the Pascal programmer have to deal the minimum possible with internal UltraGen implementation.

UltraGen is a cool language to learn and easy and simple to master. It was designed exactly with this purpose: to be agile and accessible. You can jump directly to [tutorials](/docs/simple-web-page) or know the [language specifications](/docs/basic-syntax) before.

## Cheatsheet

Hello, World!
```ruby
print('Hello, World!')
# print at console(stdout)
```

Hello, World! (adding to http response)
```ruby
live 'Hello, World!'
```

Variables and types
```ruby
a = 'text' # string
a = 10 # int
a = 10.5 # float
a = true # boolean
a = null # null
a = """this is
a multiline string"""
```

Calling methods
```ruby
a = 'Hello, World!'
print(a.upper())
# HELLO, WORLD!
```

Loops
```ruby
# for com listas
for (['item1', 'item2', 'item3'], i)
    print(i) # prints the element
    print(_i) # prints the index
end

# for com strings
for ('a string', i)
    print(i) # prints the character (see primitive-types for details)
    print(_i) # prints the index
end

#for com inteiros
for (10, i)
    print(i) # prints the iteration index
    print(_i) # prints the same
end

x = 0
while(x < 10)
    print(x)
    x += 1
end
```

Lists and dictionaries
```ruby
# lists
a_list = ['item1', 'item2', 'item3']

# dictionaries
a_dict = {
    'key1': 'value1',
    'key2': 'value2',
    a_list: 'value for any element in a_list',
    null: "default value for a key that doesn't exists"
}
```

Embedded in plain text
```html
@header = 'My Website'
@body = 'THIS IS MY WEBSITE'
<h1>{{ header }}</h1>
<p>{{ body.lower() }}</p>
```

Will print
```html
<h1>My Website</h1>
<p>this is my website</p>
```

Passing a closure as value
```ruby
myFunc = function()
    print('Hello')
end

function machine(fn)
    fn()
end

myFunc()
machine(function()
    print("it's a closure")
end)
# Hello
# it's a closure
```

Decorators
```ruby
decorator wrapper(fn)
    print("inside decorator")
    fn()
end

wrapped = wrapper(function()
    print('a decorated function')
end)

wrapped()
# inside decorator
# a decorated function

```