# sqlm

[![Go Reference](https://pkg.go.dev/badge/github.com/cavlabs/sqlm.svg)](https://pkg.go.dev/github.com/cavlabs/sqlm)
[![Support Go 1.18+](https://img.shields.io/badge/Go-1.18+-blue.svg?style=flat-square)](https://go.dev/doc/devel/release)
[![Release](https://img.shields.io/github/v/release/cavlabs/sqlm.svg?style=flat-square)](https://github.com/cavlabs/sqlm/releases)
[![Go Report Card](https://goreportcard.com/badge/github.com/cavlabs/sqlm?style=flat-square)](https://goreportcard.com/report/github.com/cavlabs/sqlm)
[![Issues](https://img.shields.io/github/issues/cavlabs/sqlm.svg?style=flat-square)](https://github.com/cavlabs/sqlm/issues)
[![PRs](https://img.shields.io/github/issues-pr/cavlabs/sqlm.svg?style=flat-square)](https://github.com/cavlabs/sqlm/pulls)
[![License: MIT](https://img.shields.io/github/license/cavlabs/sqlm.svg?style=flat-square)](https://github.com/cavlabs/sqlm?tab=MIT-1-ov-file#readme)

A lightweight and extensible SQL templating and mapping tool for Go.

## Key features

<img src="docs/assets/logo.svg" alt="sqlm logo" align="right" width="180px"/>

- Supports complex SQL template syntax (conditional statements, loops, variable substitution)
- Flexible dynamic condition construction, similar to MyBatis Mapper style
- Lightweight, zero-intrusive, easy to integrate
- Compatible with various database drivers (MySQL, PostgreSQL, SQLite, etc.)
- Provides simple API for quick start

## Getting started

### Prerequisites

sqlm requires [Go](https://go.dev/) version [1.18](https://go.dev/doc/devel/release#go1.18) or above.

### Getting sqlm

With [Go's module support](https://go.dev/wiki/Modules#how-to-use-modules), `go [build|run|test]` automatically fetches
the necessary dependencies when you add the import in your code:

```sh
  import "github.com/cavlabs/sqlm"
```

Alternatively, use `go get`:

```sh
  go get -u github.com/cavlabs/sqlm
```

### Coding with sqlm

A basic example:

```go
package main

import (
	"fmt"

	"github.com/cavlabs/sqlm"
)

func main() {
	// Define a conditional SQL template
	tpl := `
SELECT id, name, age FROM users
WHERE 1=1
{{ if .Name }}
  AND name = '{{ .Name }}'
{{ end }}
{{ if .MinAge }}
  AND age >= {{ .MinAge }}
{{ end }}
    `

	params := map[string]any{
		"Name":   "Alice",
		"MinAge": 20,
	}

	sql, err := sqlm.Render(tpl, params)
	if err != nil {
		panic(err)
	}

	fmt.Println("Generated SQL:")
	fmt.Println(sql)
}
```

## Roadmap

- [ ] Add SQL syntax parsing optimization
- [ ] Support more conditional expressions and functions
- [ ] Add SQL pre-compilation and injection protection
- [ ] Provide richer examples and plugin system
- [ ] Etc.

## Contributing

Contributions are welcome! Please follow the [CONTRIBUTING.md](CONTRIBUTING.md) guidelines.

## License

MIT License © 2025 [cavlabs/sqlm](https://github.com/cavlabs/sqlm)