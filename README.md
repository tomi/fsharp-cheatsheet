# F# Cheat sheet

## Table of Contents

-   [F# Interactive](#F-interactive)
-   [Bindings](#Bindings)
-   [Numeric Data Types](#Numeric-Data-Types)
    -   [Numeric operators](#Numeric-operators)
    -   [Numeric conversion](#Numeric-conversion)

*   [Characters](#Characters)
*   [Strings](#Strings)
    -   [String formatting](#String-formatting)
*   [Option type](#Option-type)

## F# interactive

Termination with `;;` causes execution.

| Command        |  Description                    | Example                       |
| -------------- | ------------------------------- | ----------------------------- |
| `#help`        | Show help                       | `#help;;`                     |
| `#load`        | Load code into the session      | `#load “@D:\MyCode\File.fs;;` |
| `#r`           | Load assembly into the session  | `#r "System.Configuration";;` |
| `#I`           | Add a path to the include paths | `#I @"D:\MyCode";;`           |
|  `#time "on"`  | Enable timing of commands       | `#time "on";;`                |
|  `#time "off"` | Disable timing of commands      | `#time "off";;`               |
| `#quit`        | Quit the interactive            | `#quit;;`                     |

## Bindings

| Binding       | Description                 | Example                               |
| ------------- | --------------------------- | ------------------------------------- |
| `let`         | Immutable binding           | `let a = 1`                           |
| `let mutable` | Create a mutable binding    | `let immutable a = 1; a <- 20`        |
| `ref`         | Creates a reference cell    | `let cell = ref 0; cell := 100`       |
| `use`         | Mechanism for `IDisposable` | `use disposable = createDisposable()` |

## Numeric Data Types

| F# Type             | .NET type                    | Range                                                             | Suffix   |
| ------------------- | ---------------------------- | ----------------------------------------------------------------- | -------- |
| `bool`              | `System.Boolean`             | `true`, `false`                                                   | `b`      |
| `byte`              | `System.byte`                | 0...255                                                           | `uy`     |
| `sbyte`, `int8`     | `System.SByte`               | -128...127                                                        | `y`      |
| `int16`             | `System.Int16`               | -32,768...32,767                                                  | `s`      |
| `uint16`            | `System.UInt16`              | 0...65,535                                                        | `us`     |
| `int`, `int32`      | `System.Int32`               | –231...231–1                                                      |          |
| `uint`, `uint32`    | `System.UInt32`              | 0...232–1                                                         | `u, ul`  |
| `int64`             | `System.Int64`               | –263...263–1                                                      | `L`      |
| `uint64`            | `System.UInt64`              | 0...264–1                                                         | `UL`     |
| `decimal`           | `System.Decimal`             | –296–1...296–1                                                    | `M`      |
| `float`, `double`   | `System.Double`              | 64-bit double precision number precise to approximately 15 digits |          |
| `float32`, `single` | `System.Single`              | 32-bit single precision number precise to approximately 7 digits  | `F`, `f` |
| `bigint`            | `System.Numerics.BigInteger` | No defined lower or upper bound                                   | `I`      |
| `nativeint`         | `System.IntPtr`              | 32-bit platform-specific integer                                  | `n`      |
| `unativeint`        | `System.UIntPtr`             | 32-bit unsigned platform-specific integer                         | `un`     |

### Numeric operators

| Operator | Description                                                                     |
| -------- | ------------------------------------------------------------------------------- |
| +        | Unary positive (does not change the sign of the expression). Unchecked addition |
| -        | Unary negation (changes the sign of the expression). Unchecked subtraction      |
| \*       | Unchecked multiplication                                                        |
| /        | Unchecked division                                                              |
| %        | Unchecked modulus                                                               |
| \*\*     | Unchecked exponent (valid only for floating-point types)                        |
| =        | Equality                                                                        |
| >        | Greater than                                                                    |
| <        | Less than                                                                       |
| >=       | Greater than or equal                                                           |
| <=       | Less than or equal                                                              |
| <>       | Not equal                                                                       |
| &&&      | Bitwise AND                                                                     |
| \|\|\|   | Bitwise OR                                                                      |
| ^^^      | Bitwise exclusive OR                                                            |
| ~~~      | Bitwise negation                                                                |
| <<<      | Bitwise left shift                                                              |
| >>>      | Bitwise right shift                                                             |

### Numeric conversion

Each type has an equally named conversion function, e.g. `float`.

## Characters

```fsharp
let a = 'a'
let copyrightSign = '\u00A9'
```

## Strings

```fsharp
let str = "string"
let verbatimString = @"Hello, my name is ""Kevin"""
let tripleQuotedString = """<person name="Kevin" age="33" />"""
```

### String formatting

Common format tokens

| Token      | Description                                                                 |
| ---------- | --------------------------------------------------------------------------- |
| `%A`       | Prints any value with F#’s default layout settings                          |
| `%b`       | Formats a Boolean value as true or false                                    |
| `%c`       | Formats a character                                                         |
| `%d`, `%i` | Formats any integer                                                         |
| `%e`, `%E` | Formats a floating-point number with scientific notation                    |
| `%f`       | Formats a floating-point number                                             |
| `%g`, `%G` | Shortcut for %e or %f; the more concise one will be selected automatically. |
| `%M`       | Formats a decimal value                                                     |
| `%o`       | Octal                                                                       |
| `%O`       | Prints any value by calling its ToString method                             |
| `%s`       | Formats a string                                                            |
| `%x`       | Lowercase hexadecimal                                                       |
| `%X`       | Uppercase hexadecimal                                                       |

Numeric string format modifiers

| Modifier | Effect                                                                 | Example   | Result         |
| -------- | ---------------------------------------------------------------------- | --------- | -------------- |
| 0        | When used in conjunction with a width, pads any extra space with zeros | `"%010d"` | `"0000000123"` |
| -        | Left-justifies the text within the available space                     | `"%-10d"` | `"123 "`       |
| +        | Prepends a positive sign if the number is positive                     | `"%+d"`   | `"+123"`       |
| (space)  | Prepends a space if the number is positive                             | `"% d"`   | `" 123"`       |

Excerpt From: Dave Fancher. “The Book of F#: Breaking Free with Managed Functional Programming.” iBooks.

## Option type

```fsharp
// Type definition
type Option<'a> =
   | Some of 'a
   | None

// Example usage
let noName = None
let name = Some "Kevin"

// Pattern matching
match name with
| Some x -> printfn "the name is %s" x
| None -> printfn "the name is None"
```
