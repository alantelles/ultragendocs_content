# Characteristics

>A little talk about UltraGen

In this topic we will talk about characteristics and expected behaviors of UltraGen.

## Overall

UltraGen is a object oriented language. Every type in UltraGen is a descendant from internal type `TInstanceOf`, even *null*, which is an instance of `TNullInstance`.

Only integers, bytes and floats can be mixed in an operation. Other types mismatches will generate an error. Operations between an integer and a float will have as result the type who can hold the value. If the result is float, the type of result will be a `Float`. If result is integer the type will be an `Integer`. The result of operations using `Byte` will be always casted to `Integer`.

In the next snippet is shown the result of some operations. As you will see at the last line, this rule applies to logical and comparisons operations too.

```ruby
x = 7 + 10 # ok, result is Integer
y = 0.4 - 1 # ok, result is Float
z = 0.4 + 0.6 # ok, result is Integer
a = 3 * 5 # ok, 15
b = 12 / 5 # ok, 2.4
c = 12 // 5 # ok, 2
w = 1 + 'tries' # error, type mismatch
d = 5 < "a string" # error, type mismatch
e = x && true # error, type mismatch
```

Additionally, only basic types - except `null` can be used in operations. You can't do operations with lists or dictionaries. For handling these types you must use their methods.

## "Why so serious?"

UltraGen philosophy is to balance between the ease of use and semantics. That said, any construction that may depend of much "interpreting" is avoided. Things that may lead you to questions like "what will happen now?" and unintentionally turn your logic error prone. An example is a dictionary comparison. Does it makes sense? How can I say two dictionaries are equal? They point to the same address? They have the same keys? The same values? The same pairs? The order of keys matter? It's the same about lists. Or how can I compare a string to an integer? Or to null? 10 is greater than "string"? Why? For you and others developers who will reach your code don't have these questions, we think it's better that anytime you need to do things like this you do this explicitly.

## On the other way, flexibility

Despite of the before topic, there are some times that UltraGen is sure of what should happen and do the string coercion for you. So, when you use the `live` statement the arguments are all casted to string. When setting headers from response or request you don't need to worry about this too.

Other time where UltraGen "relies on developer" is on the classes implementation. You can't declare attributes or methods in classic or instance scope. All attributes are declared in "type" scope. Instantied objects and the classes can access the same attribute

## More?

If you understand that other characteristics of language are worthy no note in this article, please open an [issue](https://github.com/alantelles/ultragendocs_content/issues/new) with you suggestion.
