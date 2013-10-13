
# brace-expansion

[Brace expansion](https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html), 
as known from sh/bash, in JavaScript.

[![build status](https://secure.travis-ci.org/juliangruber/brace-expansion.png)](http://travis-ci.org/juliangruber/brace-expansion)

[![testling badge](https://ci.testling.com/juliangruber/brace-expansion.png)](https://ci.testling.com/juliangruber/brace-expansion)

## Example

```js
var expand = require('brace-expansion');

// expand comma seperated lists
console.log(expand('file-{a,b,c}.jpg'));
// => ['file-a.jpg', 'file-b.jpg', 'file-c'.jpg]

console.log(expand('-v{,,}'));
// => ['-v', '-v', '-v']

// expand ranges
console.log(expand('file{0..2}.jpg'));
// => ['file0.jpg', 'file1.jpg', 'file2.jpg']

// characters work too
console.log(expand('file-{a..c}.jpg'));
// => ['file-a.jpg', 'file-b.jpg', 'file-c.jpg']

// backwards iteration
console.log(expand('file{2..0}.jpg'));
// => ['file2.jpg', 'file1.jpg', 'file0.jpg']

// custom increment values
console.log(expand('file{0..4..2}.jpg'));
// => ['file0.jpg', 'file2.jpg', 'file4.jpg']

// also with characters
console.log(expand('file-{a..e..2}.jpg'));
// => ['file-a.jpg', 'file-c.jpg', 'file-e.jpg']

// optional padding
console.log(expand('file{00..10..5}.jpg'));
// => ['file00.jpg', 'file05.jpg', 'file10.jpg']

// nested expansion
console.log(expand('{{A..C},{a..c}}'));
// => ['A', 'B', 'C', 'a', 'b', 'c']

console.log(expand('ppp{,config,oe{,conf}}'));
// => ['ppp', 'pppconfig', 'pppoe', 'pppoeconf']
```

## API

```js
var expand = require('brace-expansion');
```

### var expanded = expand(str)

Return an array of all possible and valid expansions of `str`. If none are
found, `[str]` is returned.

Valid expansions are:

```js
/^(.*,)+(.+)?$/
// {a,b,...}
```

A comma seperated list of options, like `{a,b}` or `{a,{b,c}}` or `{,a,}`.

```js
/^-?\d+\.\.-?\d+(\.\.-?\d+)?$/
// {x..y[..incr]}
```

A numeric sequence from `x` to `y` inclusive, with optional increment.
If `x` or `y` start with a leading `0`, all the numbers will be padded
to have equal length. Negative numbers and backwards iteration work too.

```js
/^-?\d+\.\.-?\d+(\.\.-?\d+)?$/
// {x..y[..incr]}
```

An alphabetic sequence from `x` to `y` inclusive, with optional increment.
`x` and `y` must be exactly one character, and if given, `incr` must be a
number.

For compatibility reasons, the string `${` is not eligible for brace expansion.

## Installation

With [npm](https://npmjs.org) do:

```bash
npm install brace-expansion
```

## License

(MIT)

Copyright (c) 2013 Julian Gruber &lt;julian@juliangruber.com&gt;

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies
of the Software, and to permit persons to whom the Software is furnished to do
so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
