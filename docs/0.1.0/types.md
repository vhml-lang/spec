---
description: Typing documentation for VHML
---

# Types

There are many types available that keys can be set to. The following section describes the available types as well as their literal declarations.

## Number

The `number` type represents any real number. **The maximum and minimum values as well as the precision are implementation specific**, though typically the Number type will be able to be deserialized as either a 64-bit signed integer or a 64-bit IEEE 754 floating point number depending on the presence of a decimal point. A number literal is any group of numeric digits, containing any number of underscores for formatting (which may be ignored), and either a comma or period for a decimal point.

```vhml
(number)num1 = 42 # Valid, interpreted as 42 integer
(number)num2 = -42.0 # Valid, interpreted as -42 float
(number)num3 = 5_000_000 # Valid, interpreted as 5,000,000 integer
(number)num4 = 3_141,5 # Valid, interpreted as 3,141.5 float
```

The Number literal may also be followed by a short sequence to declare its type and number of bits (not unlike Rust). The following sequences are valid:

| **Number of bits** | **Signed Integer** | **Unsigned Integer** | **Floating Point** |
| ------------------ | ------------------ | -------------------- | ------------------ |
| **8**              | i8                 | u8                   | f8                 |
| **16**             | i16                | u16                  | f16                |
| **32**             | i32                | u32                  | f32                |
| **64**             | i64                | u64                  | f64                |
| **128**            | i128               | u128                 | f128               |

```vhml
(number)num5 = 42f64 # Valid
(number)num6 = 42.0u16 # Highly discouraged, will cause loss of precision
(number)num7 = 42u8 # Valid
```

These sequences may also be used as standalone types.

```vhml
(f64)num5 = 42 # Valid
(u16)num6 = 42.0 # Highly discouraged
(u8)num7 = 42 # Valid
```
