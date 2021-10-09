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
The script included is actually executed not only his names are imported. That is, if you write something in global scope, it will be executed. In case of a template, it will rendered at include time.:info
callout
```

```callout
 UltraGen handles the use of [b]slash[/b] as separator in Windows. No need to convert it replace.:info
callout
```

## Isolating scopes

The best way to isolate scopes is to think your external script as a library and write it as a class. Different from Java or other languages the script file names have nothing to do with class names. Neither there is a helper which relate names in a script with its names.

## Even templates?

Yes. It's a good practice to declare your templates as functions to enclose them and have control about when they are rendered and about passed arguments.

```html
# template at root scope
# temp_root.ultra
<h1>{{ title }}</h1>
```

```html
# template at function scope
# temp_func.ultra
@function h1(title)
    <h1>{{ title }}</h1>
@end
```
```ruby
title = 'some title'
include 'temp_root.ultra'
# will render the template at include
```
```ruby
include 'temp_func.ultra'
# will not render
h1('some title')
# now it's rendered
```

If you have a group of related templates in different files you can have a structure like this

```
- templates
|-- UsersTemplates
|---- _init.ultra
   |-- index.ultra
   |-- show.ultra
```

And your files can be like this:

```ruby
# _init.ultra
class UsersTemplates
include 'templates/UsersTemplates/index.ultra'
include 'templates/UsersTemplates/show.ultra'
```

```ruby
# index.ultra
@function index() : UsersTemplates
Index of users
@end
```

```ruby
# show.ultra
@function show() : UsersTemplates
Show a user
@end
```

And finally, to include all templates from Users.

```
# index.ultra
include 'templates/UsersTemplates'
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

This function is available thinking of libraries or customized environments where you can have a set of modules in your applications project (something like the node_modules) and can refer to a modules repository just changing the module path add. It's suggested you don't use it for your own application paths.

## The *load* keyword

Additionally there's a `load` keyword used to add functionalities to you script. However, this is for internal types loading and has no function to any part written by developer. Conventionally, every internal type is loaded by a script and available to developer through `include`. Taken `@Core.Markdown` for example, this is what we have.

```ruby
load Markdown
```

So, in your script you write `include @Core.Markdown` and the internal type load action is abstracted.

While it's syntactically allowed, you should not use `load` directly in your script. The reason is because the types often have more methods declared in the including file as we can see in the next example in `@Core.Request`.

```ruby
load Request 
function postJson(url, data, headers={}) : Request 
    headers['Content-Type'] = 'application/json'
    req = Request.post(url, JSON.create(data), headers)
    return req
end 

function getJson() : Response self 
    return JSON.parse(self.text) 
end
```

If you write a `load` directly in your script these methods wouldn't be available.

## Setting up default loaded types

As said, every time you run a UltraGen script the module `@Core` is included. This module is the script at `build/modules/Core/_init.ultra`. It has a bunch of include statements for including other modules. If you want to make a module available to every script you execute or even drop some of the defaults just change this file. However, it's suggested you don't remove a include since as any application is supposed to rely on default release configuration of this file.


