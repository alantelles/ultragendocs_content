# Integer

The primitive type for representing integer values in UltraGen. You can refer to the type documentation in respective [doc](/docs/primitive-types).

## Attributes

None

## Methods

>cycle

#### Description

Return one of the arguments according to its index "cycle visiting" them.

#### Returns

`Any` (will depend of indexed argument)

#### Signatures

```php
cycle(Any *args) : Integer self
```

#### Examples

```ruby
x = ['show', 'item', 'of', 'list']
for (6, i)
    print(_i, ':', i.cycle(*x))
end
# 0: show
# 1: item
# 2: of
# 3: list
# 4: show
# 5: item
```
>fixed

#### Description

Returns a string with the integer preceded of a count of zeros until the size passed in argument. If the number has more characters than count, the return is the own number as a string.

#### Returns

`String`

#### Signatures

```php
fixed(Integer count) : Integer self
```

#### Examples

```ruby
print((5).fixed(3))
print((50).fixed(3))
print((500).fixed(3))
print((5000).fixed(3))
# 005
# 050
# 500
# 5000
```

>leftZeros

#### Description

Returns a string with the integer preceded of a count of zeros. This method does not pad the output. It just precedes the number with the number of zeroes passed in argument.

#### Returns

`String`

#### Signatures

```php
leftZeros(Integer count) : Integer self
```

#### Examples

```ruby
x = 90
print(x.leftZeros(2))
# 0090
```

>random

#### Description

Returns a random integer number between 0 and the given limit excluding it. If a negative number is passed the range will be between the number excluding it to 0.

#### Returns

`Integer`

#### Signatures

```php
random(Integer count) : Integer
```

#### Examples

```ruby
for (5, i)
    print(Integer.random(50))
end
for (5, i)
    print(Integer.random(-50))
end
# 0
# 31
# 1
# 30
# 45
# -28
# -19
# -40
# -20
# -25
```