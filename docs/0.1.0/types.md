---
description: Typing documentation for VHML
---

# Types

There are many types available that keys can be set to. The following section describes the available types as well as their literal declarations.

## Number

The `number` type represents a real number. The bit width of the number, as well as if the number is signed, unsigned, or floating point, is determined from context. A number literal is any group of numeric digits, containing any number of underscores for formatting (which may be ignored), and either a comma or period for a decimal point. The number can be prefixed with a + for a positive number and a - for a negative number. If either of these signs are present, the value will be assumed to be signed, and if neither is present it will be assumed to be unsigned.

```vhml
num1 = 42 # Valid, interpreted as 42 unsigned integer
num2 = -42.0 # Valid, interpreted as -42 float
num3 = +5_000_000 # Valid, interpreted as 5,000,000 signed integer
num4 = 3_141,5 # Valid, interpreted as 3,141.5 float
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

By default, all numbers are assumed to be in base 10. However, if prefixed with the following sequences, the base is changed.

| **Sequence** | **Base**        |
| ------------ | --------------- |
| 0b, bin      | 2 (binary)      |
| 0o, oct      | 8 (octal)       |
| 0x, 0h, hex  | 16 (Hexdecimal) |

```vhml
hex1 = 0xABABABA
(u32)hex2 = 0hCCCCCC
hex3 = -0x6bi8

oct1 = 0o01234567
oct2 = 0o700

(u8)bin1 = 0b0101010
bin2 = -0b1010101i8 # automatic two's complement
```

If a hex, octal, or binary constant is cast to floating point, it will not be converted to the exact value of the binary string, but instead will convert it to the floating-point number that data represents according to IEEE 754.

```vhml
float0 = 0x40000000f32 # Actual value: 2.0
```



Floating point numbers can use a capital E to express numbers in scientific notation. If an E is present, the number will always be interpreted as a float.

```vhml
float1 = 5E2
invalid = 5E2i8 # Invalid because E has precedence over i8
float2 = -2.0E-7
float3 = -8.1E4
```

Leading or trailing decimal points are valid but discouraged.

```vhml
float4 = .7 # Equivalent to 0.7
float5 = 7. # Equivalent to 7.0
float6 = 3.E+5. # Equivalent to 3.0E+5
```

-0.0 and +0.0 are not equivalent values, and will map according to IEEE 754. The following constants can also be used. With the exception of `e`, these are all case insensitive.

| **Constant** | **Value**                   |
| ------------ | --------------------------- |
| inf, +inf    | Infinity (0x7f800000)       |
| -inf         | -Infinity (0xff800000)      |
| nan, +nan    | Not a Number (0x7fffffff)   |
| -nan         | -Not a Number (0xffffffff)  |
| e            | Euler's number (2.71828...) |
| pi, π        | Pi (3.14159...)             |
| phi, ϕ       | Phi/Golden Ratio (1.61803)  |





