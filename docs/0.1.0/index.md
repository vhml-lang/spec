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

```
# This is a full line comment
#comment = "this is a comment"
key = "value" # This is a partial line comment
another = "# This isn't a comment"
```

Multi-line comments are also supported. Any text between the opening character sequence `#[` and the closing character sequence `]#` is interpreted as a comment.

```
key = "#[value" # does not need to be escaped when in quotes
#[
	comment = "this is within a multi-line comment"
	All of the text until the symbol on the next line is a comment.
]#
```

## Key/Value Pairs

A VHML file is, like most configuration file formats, a list of named keys associated with those keys. In VHML, the format `<key> = <value>` is used, where `key` is a valid name for a key (see [File Format](#File Format)) and `value` is a literal or macro associated with a valid type (see [Types](#Types)).

```
string = "Hello world!"
```

Keys may also be explicitly typed in cases where that may improve clarity (i.e. macros), or to prevent the entry of incorrect data. This can be done by following the key with `: type`.

```
string: string = "Hello world!" # Valid
number: number = 42 # Valid
string2: integer = "Hello world!" # Invalid
```



##  Types

There are many types available that keys can be set to. The following section describes the available types as well as their literal declarations.

### Number

The `number` type represents any real number. **The maximum and minimum values as well as the precision are implementation specific**, though typically the Number type will be able to be deserialized as either a 64-bit signed integer or a 64-bit IEEE 754 floating point number depending on the presence of a decimal point. A number literal is any group of numeric digits, containing any number of underscores for formatting (which may be ignored), and either a comma or period for a decimal point.

```
num1: number = 42 # Valid, interpreted as 42 integer
num2: number = -42.0 # Valid, interpreted as -42 float
num3: number = 5_000_000 # Valid, interpreted as 5,000,000 integer
num4: number = 3_141,5 # Valid, interpreted as 3,141.5 float
```

The Number literal may also be followed by a short sequence to declare its type and number of bits (not unlike Rust). The following sequences are valid:

| **Number of bits** | **Signed Integer** | **Unsigned Integer** | **Floating Point** |
| ------------------ | ------------------ | -------------------- | ------------------ |
| **8**              | i8                 | u8                   | f8                 |
| **16**             | i16                | u16                  | f16                |
| **32**             | i32                | u32                  | f32                |
| **64**             | i64                | u64                  | f64                |
| **128**            | i128               | u128                 | f128               |

```
num5: number = 42f64 # Valid
num6: number = 42.0u16 # Highly discouraged, will cause loss of precision
num7: number = 42u8 # Valid
```

These sequences may also be used as standalone types.

```
num5: f64 = 42 # Valid
num6: u16 = 42.0 # Highly discouraged
num7: u8 = 42 # Valid
```

