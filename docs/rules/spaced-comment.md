# Requires or disallows a whitespace (space or tab) beginning a comment (spaced-comment)

Some style guides require or disallow a whitespace immediately after the initial `//` or `/*` of a comment.
Whitespace after the `//` or `/*` makes it easier to read text in comments.
On the other hand, commenting out code is easier without having to put a whitespace right after the `//` or `/*`.

## Rule Details

This rule will enforce consistency of spacing after the start of a comment `//` or `/*`. It also provides several
exceptions for various documentation styles.

### Options

The rule takes two options. The first is a string which be either "always" or "never". If you pass `"always"` then the `//` or `/*` must be followed by at least once whitespace. If `"never"` then there should be no whitespace following. The default is `"always"`.

Here is an example of how to configure the rule with this option:

```js
"spaced-comment": [2, "always"]
```

#### Exceptions

This rule can also take a 2nd option, an object with either of the following keys: `"exceptions"` and `"markers"`.

The `"exceptions"` value is an array of string patterns which are considered exceptions to the rule.
Please note that exceptions are ignored if the first argument is `"never"`.

```js
"spaced-comment": [2, "always", { "exceptions": ["-", "+"] }]
```

The `"markers"` value is an array of string patterns which are considered markers for docblock-style comments,
such as an additional `/`, used to denote documentation read by doxygen, vsdoc, etc. which must have additional characters.
The `"markers"` array will apply regardless of the value of the first argument, e.g. `"always"` or `"never"`.

```js
"spaced-comment": [2, "always", { "markers": ["/"] }]
```

The difference between a marker and an exception is that a marker only appears at the beginning of the comment whereas
exceptions can occur anywhere in the comment string.

You can also define separate exceptions and markers for block and line comments:

```js
"spaced-comment": [2, "always", {
    "line": {
        "markers": ["/"],
        "exceptions": ["-", "+"]
    },
    "block": {
        "markers": ["!"],
        "exceptions": ["*"]
    }
}]
```

#### Examples

The following patterns **are** considered warnings:

```js
// When [2, "never"]
// This is a comment with a whitespace at the beginning
```

```js
// When [2, "never"]
/* This is a comment with a whitespace at the beginning */
```


```js
// When [2, "never"]
/* \nThis is a comment with a whitespace at the beginning */
```

```js
// When [2, "always"]
//This is a comment with no whitespace at the beginning
var foo = 5;
```

```js
// When [2, "always"]
/*This is a comment with no whitespace at the beginning */
var foo = 5;
```

```js
// When [2, "always", { "block": { "exceptions": ["-"] } }]
//--------------
// Comment block
//--------------
```

```js
// When [2, "always", { "exceptions": ["-", "+"] }]
//------++++++++
// Comment block
//------++++++++
```

```js
// When [2, "always", { "markers": ["/"] }]
///This is a comment with a marker but without whitespace
```

```js
// When [2, "always", { "exceptions": ["-", "+"] }]
/*------++++++++*/
/* Comment block */
/*------++++++++*/
```

```js
// When [2, "always", { "line": { "exceptions": ["-+"] } }]
/*-+-+-+-+-+-+-+*/
// Comment block
/*-+-+-+-+-+-+-+*/
```

The following patterns **are not** warnings:

```js
// When [2, "always"]
// This is a comment with a whitespace at the beginning
var foo = 5;
```

```js
// When [2, "always"]
/* This is a comment with a whitespace at the beginning */
var foo = 5;
```

```js
// When [2, "always"]
/*\n * This is a comment with a whitespace at the beginning */
var foo = 5;
```

```js
// When [2, "never"]
/*This is a comment with no whitespace at the beginning */
var foo = 5;
```

```js
// When [2, "always", { "exceptions": ["-"] }]
//--------------
// Comment block
//--------------
```

```js
// When [2, "always", { "line": "exceptions": ["-"] } }]
//--------------
// Comment block
//--------------
```

```js
// When [2, "always", { "exceptions": ["-+"] }]
//-+-+-+-+-+-+-+
// Comment block
//-+-+-+-+-+-+-+
```

```js
// When [2, "always", { "exceptions": ["-+"] }]
/*-+-+-+-+-+-+-+*/
// Comment block
/*-+-+-+-+-+-+-+*/
```

```js
// When [2, "always", { "block": { "exceptions": ["-+"] } }]
/*-+-+-+-+-+-+-+*/
// Comment block
/*-+-+-+-+-+-+-+*/
```

```js
// When [2, "always", { "exceptions": ["*"] }]
/****************
 * Comment block
 ****************/
```

```js
// When [2, "always", { "markers": ["/"] }]
/// This is a comment with a marker
```

```js
// When [2, "never", { "markers": ["!<"] }]
//!<This is a comment with a marker
/*!<this is a block comment with a marker
subsequent lines are ignored
*/
```

```js
// When [2, "always", { "markers": ["global"] }]
/*global ABC*/
```

```js
// When [2, "always"]
/**
* I am jsdoc
*/
```

```js
// When [2, "never"]
/**
* I am jsdoc
*/
```

