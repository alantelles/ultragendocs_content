# Composed types

>The set-like base types for expressing values

## Abstract

The composed core types are **lists** and **dictionaries**. They can contain values of any type and they are accessed by index. If the value referenced is a primitive type the value is retrieved by as a copy. If not a reference for the original object is obtained.

## Lists

The **List** type holds a sequence of values that can be accessed by a numeric index. The start index of a list is **0**. You can access an item from backward using a negative index.

```callout
UltraGen does not have a slice operator. If you need a slice use the [code]slice[/code] method.:info
callout
```

To start a list you only need to declare the values inside the list declaration syntax. To start an empty list you only need to declare a variable with the `[]` value. You can't set a value by an non-existing index directly. For adding elements you must use `append`. Let's see some list examples.

You can use `pop` to drop the last value from index returning them.

```ruby
a = [] # starts an empty list
a.append('item') # set a[0] to 'item'
a[1] = "other" # raises an error
b = [0, 'item', true, ['zero', 'one']] # starts a list with these values
print (b[1]) # retrieving index 1 "item"
print(b[3][1]) # retrieving an index from an index
b[0] = 99 # set the first index of b to 99
v = b.pop() # get the last value of b
# and decreases the length by one
```

Lists values can be distributed to variables using the `unpack` method. This is useful as UltraGen does not provide multiple assignment. This method receives strings and declares variables with their names. Strings must be valid identifiers. *idStrings* syntax are highly suggested here.

```ruby
['some', 'item'].unpack(:a, :b)
print(a) # prints "some"
print(b) # prints "item"
```

```callout
For the sake of semantics, even it's used in this example, do not use it as a generic multi assign function. This method is thought to be used with methods that returns lists.:info
callout
```

You can iterate by lists by passing it as an argument to `for` loop. The values are accessed inside the loop by the name passed as second argument. The index can be accessed by the same name preceded by an underscore `_`, as shown in [basic syntax](/docs/basic-syntax) doc.

## Dicts

Dictionaries of values are expressed by the **Dict** type and have its values accessed by strings. Only strings and *null* in a special case can be used as index for dictionaries. Any type can be a value of a dictionary.

To initialize a Dict you just set its values using the proper syntax. You can start it empty or with values.

To access the values the syntax is the same for lists. You use the variable and the index between brackets. Different from lists, you can set a value directly without append or other auxiliary method.

```ruby
d = {} # an empty dict
e = {:aKey : "value"} # a Dict with values
print(e['aKey']) # retrieving value on aKey index
# note that idStrings can be used seamlessly
# with normal syntax
d['other'] = 1010 # assigning value
# note that differently from list this can be done directly
d.drop('other') # this deletes the key 'other' from dict
```

```callout
The method [code]hasKey[/code] is provided to check if a key exists before trying to retrieve. In addition there's a [code]get[/code] method that receives two arguments. The key and a value to return if key is not found. Default value is [b]null[/b].:success
callout
```

### Special indexes

Despite only strings can be indexes for dictionaries, there are two special cases that are exceptions.

You can set a default value for not found indexes by setting a `null` indexed value.

The null key is not taken account in iterations. The value referenced by null can be accessed by `[null]`.

Another possibility is declare a dictionary with a list as index. This is internally parsed a the value being indexed by any of the elements of the list. All elements must be strings.

```ruby
a = {
    [:key1, :key2, :key3] : 100,
    null : "value not found"
}
print(a[:key1]) # prints 100
print(a[:key2]) # prints 100
print(a[:key3]) # prints 100
print(a["any"]) # prints "value not found"
print(a[null]) # prints "value not found"
```

## Other composed types

These are the basic composed types. Otherwise all objects are composed of attributes of basic or other composed types. Despite of it these will be discussed in a doc which will presents classes.
