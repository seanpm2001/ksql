ksql
=====
![Project status](https://img.shields.io/badge/version-0.1.0-green.svg)
[![GoDoc](https://godoc.org/github.com/go-playground/ksql?status.svg)](https://pkg.go.dev/github.com/go-playground/ksql)
![License](https://img.shields.io/dub/l/vibe-d.svg)

**Is a JSON data expression lexer, parser, cli and library.**

#### Requirements
- Go 1.18+

#### How to install CLI
```shell
~ go install github.com/go-playground/ksql/cmd/ksql
```

#### Usage
```go
package main

import (
	"fmt"

	"github.com/go-playground/ksql"
)

func main() {
	expression := []byte(`.properties.employees > 20`)
	input := []byte(`{"name":"MyCompany", "properties":{"employees": 50}`)
	ex, err := ksql.Parse(expression)
	if err != nil {
		panic(err)
	}

	result, err := ex.Calculate(input)
	if err != nil {
		panic(err)
	}
	fmt.Printf("%v\n", result)
}

```

#### Expressions
Expressions support most mathematical and string expressions see below for details:

#### Syntax & Rules

| Token          | Example                  | Syntax Rules                                                                                                                                                                                |
|----------------|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `Equals`       | `==`                     | supports both `==` and `=`.                                                                                                                                                                 |
| `Add`          | `+`                      | N/A                                                                                                                                                                                         |
| `Subtract`     | `-`                      | N/A                                                                                                                                                                                         |
| `Multiply`     | `*`                      | N/A                                                                                                                                                                                         |
| `Divide`       | `/`                      | N/A                                                                                                                                                                                         |
| `Gt`           | `>`                      | N/A                                                                                                                                                                                         |
| `Gte`          | `>=`                     | N/A                                                                                                                                                                                         |
| `Lt`           | `<`                      | N/A                                                                                                                                                                                         |
| `Lte`          | `<=`                     | N/A                                                                                                                                                                                         |
| `OpenParen`    | `(`                      | N/A                                                                                                                                                                                         |
| `CloseParen`   | `)`                      | N/A                                                                                                                                                                                         |
| `OpenBracket`  | `[`                      | N/A                                                                                                                                                                                         |
| `CloseBracket` | `]`                      | N/A                                                                                                                                                                                         |
| `Comma`        | `,`                      | N/A                                                                                                                                                                                         |
| `QuotedString` | `"sample text"`          | Must start and end with an unescaped `"` character                                                                                                                                          |
| `Number`       | `123.45`                 | Must start and end with a valid `0-9` digit.                                                                                                                                                |
| `Boolen`       | `true`                   | Accepts `true` or `false` as a boolean only.                                                                                                                                                |
| `Identifier`   | `.identifier`            | Starts with a `.` and ends with whitespace blank space. This crate currently uses [gjson](https://github.com/tidwall/gjson.rs) and so the full gjson syntax for identifiers is supported.   |
| `And`          | `&&`                     | N/A                                                                                                                                                                                         |
| `Not`          | `!`                      | Must be before Boolean identifier or expression or be followed by an operation                                                                                                              |
| `Or`           | <code>&vert;&vert;<code> | N/A                                                                                                                                                                                         |
| `Contains`     | `CONTAINS `              | Ends with whitespace blank space.                                                                                                                                                           |
| `In`           | `IN `                    | Ends with whitespace blank space.                                                                                                                                                           |
| `StartsWith`   | `STARTSWITH `            | Ends with whitespace blank space.                                                                                                                                                           |
| `EndsWith`     | `ENDSWITH `              | Ends with whitespace blank space.                                                                                                                                                           |
| `NULL`         | `NULL `                  | N/A                                                                                                                                                                                         |



```

#### License

<sup>
Licensed under either of <a href="LICENSE-APACHE">Apache License, Version
2.0</a> or <a href="LICENSE-MIT">MIT license</a> at your option.
</sup>

<br>

<sub>
Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in Proteus by you, as defined in the Apache-2.0 license, shall be
dual licensed as above, without any additional terms or conditions.
</sub>
