# readercomp : Go package for comparing two finite io.Reader (e.g. files)

[![GoDoc](https://godoc.org/github.com/stevegt/readercomp?status.svg)](https://godoc.org/github.com/stevegt/readercomp)
[![Build Status](https://github.com/stevegt/readercomp/workflows/run%20tests/badge.svg)](https://github.com/stevegt/readercomp/actions?workflow=run%20tests)
[![Coverage Status](https://coveralls.io/repos/github/stevegt/readercomp/badge.svg?branch=main)](https://coveralls.io/github/stevegt/readercomp?branch=main)
[![Go Report Card](https://goreportcard.com/badge/github.com/stevegt/readercomp)](https://goreportcard.com/report/github.com/stevegt/readercomp)

## Why?

Comparing files (or more generally two finite `io.Reader`) is not
trivial, due to edge-cases like short reads and the way errors
(including `EOF`) are returned by calls to `Read` according to the
[interface specification](https://pkg.go.dev/io/#Reader).

This package tries to deliver a solid implementation for these cases.

This fork of @hlubek's [excellent package](https://github.com/hlubek/readercomp) 
was modified by @stevegt to add more information for troubleshooting
in the case of an io.Reader comparison mismatch; specifically, it adds
a ReaderCompError type that includes the failing buffers and size
data.

## Install

```
go get github.com/stevegt/readercomp
```

## Example

```go
package main

import (
	"fmt"
	"log"
	"os"

	"github.com/stevegt/readercomp"
)

func main() {
	result, err := readercomp.FilesEqual(os.Args[1], os.Args[2])
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println(result)
}
```

## License

MIT.
