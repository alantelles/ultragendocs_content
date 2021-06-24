# String

For representing textual data in UltraGen we use the type **String**. The syntax is already discussed on docs section. Strings are internally stored as a byte stream. That said, you have no concern about encoding while setting a string. However, some internal functions expect UTF-8 strings and may have some a behavior different than expected. If you need to do a "low level" operation in strings you can use the ByteStream type. Another thing worth to remember is that when accessing a character of string by its index or iterating through them with for each byte is visited. If your character has 2 bytes the access may not be what you expect.

## Attributes

None

## Methods

>join

#### Description

Creates a string from a list using the string instance as glue.

#### Returns

`String`

#### Signatures

```php
join(List list) : String self
```

#### Examples

```ruby
m = ['join', 'this', 'string']
glued = ' '.join(m)
print(glued)
# join this string
```

>split

#### Description

Creates a list from splitting a string with string given in *splitter* as split point. If no splitter is given a list with each character is returned.

#### Returns

`List`

#### Signatures

```php
split() : String self
split(String splitter) : String self
```

#### Examples

```ruby
m = "split this string"
spl= m.split(' ')
print(spl)
# ['split', 'this', 'string']
```