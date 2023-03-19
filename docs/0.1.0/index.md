---
description: VHML is a configuration file format meant to be like TOML but with more features.
---

# VHML v0.1.0

[TODO: Write more here] VHML is a configuration file format meant to be like TOML but with more features. It's designed to be pretty easy to read while also minimizing the boilerplate parts of configuration files. Although VHML is *like* TOML in many respects, and most VHML parsers can parse some TOML files, VHML is NOT TOML; there are multiple breaking changes

## File Format

- VHML is case sensitive.
- VHML files must be encoded as UTF-8.
- The acceptable space character is Space (U+0020).
- Acceptable tab characters are Tab (U+0009) or four spaces.
- Acceptable newline characters are LF (U+000A) and CR (U+000D). LF followed by CR, or CRLF (U+000D U+000A) is interpreted as one newline, not two.
- Acceptable characters in key names are [TODO]
- Files should end in a newline.
- VHML files should have the `.vhml` file extension.
- VHML files should have the `application/vhml` MIME type.
- The ABNF grammar of VHML is available at [TODO].

## Comments

A hash symbol (#) in a line indicates that the remainder of that line (between the hash and the next newline) will be a single-line comment. It is recommended but not required to have a space after the hash.

```vhml
# This is a full line comment
#comment = "this is a comment"
key = "value" # This is a partial line comment
another = "# This isn't a comment"
```

Multi-line comments are also supported. Any text between the opening character sequence `#[` and the closing character sequence `]#` is interpreted as a comment.

```vhml
key = "#[value" # does not need to be escaped when in quotes
#[
 comment = "this is within a multi-line comment"
 All of the text until the symbol on the next line is a comment.
]#
```

## Key/Value Pairs

A VHML file is, like most configuration file formats, a list of named keys associated with those keys. In VHML, the format `<key> = <value>` is used, where `key` is a valid name for a key (see [File Format](#file-format)) and `value` is a literal or macro associated with a valid type (see [Types](types)).

```vhml
string = "Hello world!"
```

Keys may also be explicitly typed in cases where that may improve clarity (i.e. macros), or to prevent the entry of incorrect data. This can be done by preceding the key with `(type)`.

```vhml
(string)string = "Hello world!" # Valid
(number)number = 42 # Valid
(integer)string2 = "Hello world!" # Invalid
```
