# Programming language thing

[![Join the chat at https://gitter.im/liam4/programming-language-thing](https://badges.gitter.im/liam4/programming-language-thing.svg)](https://gitter.im/liam4/programming-language-thing?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

This is a programming language thing (PLT). I created it. It's very new and probably not worth using, but it's a fun project for myself.

## Running

#### In your browser:

PLT only works in Firefox Nightly from what I've tested. You can copy all the code in `plt.js` to the [babel REPL](http://babeljs.io/repl) and it should also work. If you're lazy like me you can use the sloppy CodeMirror editor I made [here](http://liam4.github.io/programming-language-thing/codemirror/). More info [here](doc/Using_the_CodeMirror_Editor.md).

Add this somewhere in your HTML file:

	<script src="./plt.js"></script>

Now you have access to `plt`, as described later.

#### In [Node.js](https://nodejs.org):

First install dependencies:

	npm install
	
Now you can run `.plt` scripts like so:

	npm run plt <file>
	# npm run plt examples/hello.plt

You can `require` it in your own projects like so:

	const plt = require('./plt.js')

Note you'll need to run `node` with these Harmony V8 arguments (to add support for ES6+):

	node --harmony --harmony_destructuring --harmony_default_parameters

## A pit (but no fall)

(i.e. Application Programming Interface Thing)

PLT comes with a tiny API for running programs with JavaScript.

**On browsers that support it,** you can just load `plt.js` with a `<script>` tag:

	<script src="path/to/plt.js"></script>

You'll probably need to build `plt.js` with Babel first, though. I'm a bit too lazy to do that for you, and if you're too lazy to do it as well, I've been developing PLT in [Firefox Nightly](https://nightly.mozilla.firefox) so opening `workspace.html` will work in that.

**Using Node,** you can just `require` PLT:

	const plt = require('path/to/plt.js');

---

At this point you should have an object called `plt`. It's really a function with some properties `assign`ed, so you can treat as an object or a function.

Here's a basic usage example:

	plt(`# my program`)

If you're interested in how it works, `plt` is a shortcut for this:

* Parse the code - `parsed = parse(code)`
* Interpret the parsed code - `result = interp(parsed)`
* Return the result - `return result`

`parse` and `interp` are available as methods of `plt`.

There's also another method called `init`, which initializes variables PLT will need. It takes an object as it's parameter, which can have these properties:

* `console = window.console`: The console to log to. Needs to implement a method called `log`.

## Syntax

Here's a simple example of a program written in PLT:

    print('Hello world!')

    add_one => fn(x) {
      ^ add(x 1)
    }

    print('The answer to life, the universe, and everything is:')
    print(add_one(41))

Simply put, here are all the pieces of syntax that matter to you:

**Strings:** `'my_string'`
**Numbers:** `123`
**Variables:** `x => 'baz'` `x` (see also: [Assign vs Change](doc/Assign_vs_Change.md))
**Comments:**

    print('hello')
    # This is a comment
    print('okay')
    #print('disabled code [for now]')

Comments are marked by `#` and go to the end of the line.

You can also use mulit/in-line comments, wrapping with `#:` and `:#`:

    #: We aren't using this for now
    print('hello')
    :#
    print('Welcome!' #: Lovely. :#)

**Function expressions:** `fn(arg1 arg2 arg3...) {...}`

Note because functions are expressions, you can assign them to variables:

    foo => fn() {
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
