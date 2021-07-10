# join

## Description

Concatenates a list with the elements of a string with string given in *glue* as split point. If no glue is given space is used. List elements are casted to string.

## Returns

`String`

## Signatures

```php
join() : String
join(String splitter) : String
```

## Examples

```ruby
m = '+'.join(["one", "two"])
print(m)
# one+two.
```
