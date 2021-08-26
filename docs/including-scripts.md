# Including scripts

> Modularizing your applications

UltraGen provide the keyword `include` that allows you to embed other scripts. There are two ways to declare the script whose will be included. The first is passing the path of file.

```ruby
include 'path/to/file.ultra'
# it can use a reference
somePath = 'path/to/otherPath.ultra'
include somePath
```

The script is imported at same scope of the caller. Their live stream is also added to live stream of its caller. The same applies if it's a plain text script. The plain text is sent to caller's live stream.

```callout
Be aware that because of this behavior include can cause name masking because of the names being imported at same scope.:warning
callout
```

```callout
The script included is actually executed not only his names are imported. That is, if you write something in global scope, it will be executed.:info
callout
```

```callout
 UltraGen handles the use of **slash** as separator in Windows. No need to convert it replace.:info
callout
```

## Isolating scopes

The best way to isolate scopes is to think your external script as a library and write it as a class. Different from Java or other languages the script file names have nothing to do with class names. Neither there is a helper which relate names in a script with its names.

If you don't want to enclose your script in a class there's an alternative. The *scoped include*. You can pass a name which will be declared as a class to hold your included names. This can be done as shown.

```ruby
# included.ultra

vari = 'a variable'
function myFunc()
    print('myfunc')
end
```

```ruby
# includer.ultra
include 'included.ultra' : MyScope
# all names of included will be available
# as static attributes of MyScope
print(MyScope.vari) # a variable
MyScope.myFunc() # myfunc
```

## Modules

UltraGen provides a convenient way to include files to you script. The modules. Including modules uses an alternative notation and depends on some configuration. There are some paths which UltraGen interpreter treats internally as **modules path**. Supposing you have scripts in '/myLibs/modules'. When including scripts in these paths you can write the following:

```ruby
include @Path.To.File
```

This will be resolved to '/myLibs/modules/Path/To/File.ultra' at first. If this file doesn't exist it will search for '/myLibs/modules/Path/To/File/_init.ultra'. It's similar to the Python `__init__.py` or JS `index.js`. This way is good when you want to include many files of your module but not all. You can expose many files to the including script but some will be seen only internally. If these both don't exist it will search for '/myLibs/modules/Path/To/File' folder. If found, all of the scripts at root level will be included. If none of these were found the interpreter will raise an error.

As you must have noticed, the dots are replaced by bars internally. So, it's clear how to structure and reference your files.

For declaring your location as a *searchable* module path use the `addModulePath` function.

```ruby
addModulePath('/myLibs/modules')
include @Path.To.File
```
 You can add many paths as you want but be aware that the search direction is from last to first added. This can be a problem if you have files with same relative path.
