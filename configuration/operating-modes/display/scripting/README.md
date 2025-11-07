---
description: This page describes the syntax and possibilities with scripting.
---

# Scene Scripts

Each scene and link is executing scripts to decide what to show on displayboards.

Scripting is based on the powerful [Scriban scripting language](https://github.com/scriban/scriban). You can find more information here:

* Language Overview: [Here](https://github.com/scriban/scriban/blob/master/doc/language.md)
* Built-in Functions: [Here](https://github.com/scriban/scriban/blob/master/doc/builtins.md)

Different than stated in the official scriban docs, Remote Redirect is not changing the casing of variables or functions. Even more, you can use `string.ends_with`or `string.EndsWith`, whereas the later is preferred as it means the declaration of the method is not touched.

The following script will output "Hello World":

```
{{ "Hello World" }}
```

The following script will take the current time and pads it to 12 characters and center aligns it if need be. This is possible by using the `|` pipe character: The expression to the left is forwarded to a function that is given by the name after the pipe. The forwarded argument will be the first in the function arguments list:

```
{{ Clock | TrimPad 12 "Center" }}
```

Without using piping, you can also use a traditional way of calling methods:

```
{{ TrimPad Clock  12 "Center" }}
```
