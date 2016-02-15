# Programming language thing

[![Join the chat at https://gitter.im/liam4/programming-language-thing](https://badges.gitter.im/liam4/programming-language-thing.svg)](https://gitter.im/liam4/programming-language-thing?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

This is a programming language thing (PLT). I created it. It's very new and probably not worth using, but it's a fun project for myself.

## Running

#### In your browser:

PLT only works in Firefox Nightly from what I've tested. You can copy all the code in `main.js` to the [babel REPL](http://babeljs.io/repl) and it should also work.

#### In [Node.js](https://nodejs.org):

First install dependencies:

	npm install

Then to run:

	node --harmony --harmony_destructuring --harmony_default_parameters main.js

## Syntax

Here's a simple example of a program written in PLT:

    print('Hello world!')

    add_one -> fn(x) {
      ^ add(x 1)
    }

    print('The answer to life, the universe, and everything is:')
    print(add_one(41))

Simply put, here are all the pieces of syntax that matter to you:

**Strings:** `'my_string'`
**Numbers:** `123`
**Variables:** `x -> 'baz'`
**Comments:**

    print('hello')
    # This is a comment
    print('okay')
    #print('disabled code [for now]')

Comments are marked by `#` and go to the end of the line.

[Multi-line comment syntax has not been decided on yet.](https://github.com/liam4/programming-language-thing/issues/2)

**Function expressions:** `fn(arg1 arg2 arg3...) {...}`

Note because functions are expressions, you can assign them to variables:

    foo -> fn() {
      ...
    }

**Function calls:** `function_expression(arg1 arg2 arg3...)`

You can think of `args` lining up with `fn_args`:

    fn_args: x  y baz
    args:    42 3
    result:  42 3 [null]

    fn_args: x  y baz
    args:    42 3 7   8
    result:  42 3 7

Extra arguments are ignored; arguments that are not passed are null.

**Function expression returns:** `fn() {... ^ 'baz'}`

`^` will replace all return tokens with the next token's value.
