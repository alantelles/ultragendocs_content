# Basic IO

>Dealing with the input and output streams

## Printing

You can output a message to user in UltraGen by using the function `print` or `inline`. The difference is that `inline` does not put a newline after text. These functions can receive any type and any number of arguments. While printing the arguments they are always casted to it's string representation. These are *core level functions*. This means that they don't are methods of a type or object. All functions that are not closely related to a type are *core functions*.

```ruby
print("go", " away") # prints "go away" and a newline
inline ("Anna") # prints "Anna" without a newline
print(24, " hours") # prints "24 hours"
```

## Input

The `input` function has no arguments. It's used  when you want to get data from the user. This return the data typed and you can assign this value to a variable. The value is always a string.

```ruby
print ("Input some data")
val = input()
```

## The "live" output stream

As said, UltraGen is thought to process plain text, most typically markup. However sometimes you want to output some text for logging or any other purpose and you don't want that text to be shown in process output. For this  purpose, UltraGen feature two output streams. The *stdout* which is fed by `print` or `inline` declarations and the *live* output which is fed by `live` declaration.

```ruby
live "some text"
```

This will add "some text" to the live output. This text will not be sent to *stdout*. In case of an web application this text will be sent to web response. If you are using UltraGen to process text like XML this text will appear in the process result.

The function `saveLive(path)` is provided to allow the live output be saved as a text file at `path`.

When processing plain text scripts the plain text is always part of the live output, including the embedded expressions.

Every scope level of a program has its live output. The default return of a function is its live output. It's worthy to remember because it's in central idea of the suggested way to develop the templates: build templates like components.
