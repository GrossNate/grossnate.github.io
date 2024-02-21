---
layout: post
title: "Notes for the JS139 assessment"
date: 2024-02-19 17:00:00 -0600
---

## `var` and **scope**

- declaring a `var` at the **top level** of a program creates a property on the
  global object (e.g. `global` or `window`); it won't do that inside a function
- `var` is **function-scoped** - i.e. it doesn't care about your blocks of curly
  braces (but remember, not everything in curly braces is a block)
- Good grief, a `var` declaration within a block scope declares the variable
  even if the code in the block doesn't run (but doesn't initialize it except to
  `undefine`).
- `let` is **block-scoped** (remember, technically the body of a function isn't
  a block, but that's kind of a distinction without a difference)
- Scope vocab, in case it's important:
  1. "Declared scope" is either **block scope** or **function scope** and is
     determined only by whether it's `let`, `const`, or `class` (the former) or
     `var` or `function` (the latter).
  2. "Visibility scope" is determined by whether the variable is accessible
     globally or locally (could be further divided into "local function" or
     "local block"); the definition says this is about whether the variable is
     "visible" but it's unclear how this is particularly helpful relative to
     lexical scope.
  3. "Lexical scope" is about what variables are accessible. It includes **inner
     scope** and **outer scope**.

## hoisting

- don't nest function declarations inside non-function blocks as you may get
  inconsistent behavior. Use function expressions if you have to do this.
- Order is roughly:
  1. function declarations
  2. var // undefined
  3. class declarations (using let) // TDZ
  4. let/const // TDZ
- Don't forget the "Temporal Dead Zone"
- **creation phase** - where JavaScript figures out all the variables that are
  used, figures out where they'll be in scope - i.e. it does hoisting.
- **execution phase** code runs line-by-line

## Closures

- a function and any variables that are in lexical scope when it was defined and
  that it needs
- **partial function application** is a useful example of closures
- `bind` is a helpful way to add an argument (e.g. `func.bind(null, arg1)`)
- Note: you can say "partially applied function" but don't say "partial
  function" because that means something different
- Note: partial function application requires a reduction in the number of
  arguments
- Things closures are good for: callbacks, partial function application,
  creating private data, and more . . .

## IIFEs

Important distinction! Look at these two concepts:

- can use to make private _scope_ (making sure your variable names, including
  function names, don't conflict with other variables in the program)
- can use to make private _data_ (don't necessarily need them, but can make the
  code shorter) - this is encapsulation, not scope!

## Modules

- Benefits of using modules:
  - Shorter files for easier navigation
  - Fewer conflicts when editing
  - More reusable code
  - Better encapsulation
- Creating a module: `module.exports = variableName;`
- Using a module: `const varName = require("./path/to/module");`

## Exceptions

- **exception handler** is the `try/catch` statements
- You should only use exceptions to hande exceptional conditions - not normal
  stuff like invalid user input.
  - Throw when an event occurs that should not be ignored or when a condition is
    truly anomalous
  - Catch only those errors that you can handle. Re-throw the error if you can't
    handle it.
- `catch` blocks should do as little as possible

## Side effects

A function call that does any of the following has **side effects**:

1. **side effects through reassignment** - reassigns a non-local variable
2. **side effects through mutation** - mutates the value of any object
   referenced by a non-local variable
3. **side effects through input/output** - reads or writes to any data entity
   (files, network connections, etc.) that is non-local to your program. Note
   that this includes:
   1. reading from the keyboard
   2. writing to the console
   3. accessing the system date (`new Date()`)
   4. generating a random number (`Math.random()`)
4. **side effects through exceptions** - raises an exception without catching
   and handling it.
5. **side effects through other functions** - calls another function that has
   side effects that are not confined to the current function.

**Pure functions** have no side effects and always return the same value for the
same set of inputs. Note that LS basically considers a function to be pure if
it's always pure _when used as intended_ (in practice, though, functions that
are pure are always pure regardless of the arguments passed in).

## Testing

- When setting up, need to do `touch jest.config.js`
- Watch out: your file needs to be named ending with `.test.js` and that's
  `test` singular - Jest will fail if it's plural.
- Write tests to prevent **regression**
- Vocab:
  - **test suite** - all the tests for a project
  - **test** - specific situation you're trying to test.

## Packaging code

## Regex

Just in case: https://launchschool.com/books/regex/read/introduction
