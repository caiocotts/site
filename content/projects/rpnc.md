+++
date = 2026-03-20T12:46:54-04:00
title = "rpnc"
math = true
description = "An RPN calculator for the CLI"
tech = ["Golang"]
repo = "https://github.com/caiocotts/rpnc"
+++

## What is it?

rpnc is a calculator for your terminal that uses reverse polish notation (RPN),
which is inspired by my Hewlett Packard model 28S advanced scientific
calculator, and written in pure Go.

Here's a little demo of how one could calculate $\frac{543}{(123+74)^2}$ using
rpnc:

{{<figure src="https://files.caiocotts.com/rpnc/demo.gif" class="centered">}}

The result is printed onto the terminal once you exit the program.

You can read up on how RPN works more in depth in this post, but in simple
terms, it's a way to write mathematical expressions without the need for
parentheses.

Currently it can perform all the fundamental operations that a regular
calculator can like: adding, subtracting, multiplying, and dividing. In
addition, it has functions for manipulating its stack like: `swap`, `dup`,
`roll`, and `drop`.

My vision for this project is much more than just a simple little calculator app
however.

## Vision

I intend to make rpnc fully programmable just like my aforementioned 28S. I will
be extending it to be able to interpret reverse polish LISP (RPL) programs. The
calculator will have another mode in addition to its current interactive mode.
This new mode, the interpreter mode, will allow users to evaluate expressions
from .rpl files, or directly from the command line like
`rpnc eval -f ./example.rpl` and `rpnc eval "543 123 74 + 2 ^ /"`

Much like the 28S, it will also have a directory hierarchy and a custom menu
where users can save functions that they wish to have direct access to instead
of having to type them out:

{{<figure src="https://files.caiocotts.com/rpnc/custom_menu.png" class="centered">}}

Since there are no dedicated buttons for things like these on a keyboard, I plan
to make menu items accessible via CTRL modifiers. So in the case of the image
above for example, the user would press ctrl+1 and ctrl+2 to access the `MOD`
and `SWAP` menu items respectively.

## Where Can You Get It?

Look no further than my git [repo](https://github.com/caiocotts/rpnc) :)

## Other Neat Things

Implementing the RPL interpreter is a pretty interesting task. As I started
studying about interpreters, I started to notice in other languages, like Go for
instance, the same techniques that I had read about. Like tokenization of
strings during lexical analysis.

Taken from token.go in token package of Go's standard library:

```go
// The list of tokens.
const (
	// Special tokens
	ILLEGAL Token = iota
	EOF
	COMMENT

	literal_beg
	// Identifiers and basic type literals
	// (these tokens stand for classes of literals)
	IDENT  // main
	INT    // 12345
	FLOAT  // 123.45
	IMAG   // 123.45i
	CHAR   // 'a'
	STRING // "abc"
	literal_end
    .
    .
    .
    ADD // +
	SUB // -
	MUL // *
	QUO // /
	REM // %
    .
    .
    .
)
```

The specific book I chose to read to help me implement RPL is called
[_Crafting Interpreters_](https://craftinginterpreters.com/) by Robert Nystrom.
It's a step-by-step on how to build a language from scratch, but worded in a
conversational tone. I highly recommend it.
