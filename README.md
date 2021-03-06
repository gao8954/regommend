regommend
=========

Recommendation engine for Go

## Installation

Make sure you have a working Go environment. See the [install instructions](http://golang.org/doc/install.html).

To install regommend, simply run:

    go get github.com/muesli/regommend

To compile it from source:

    git clone git://github.com/muesli/regommend.git
    cd regommend && go build && go test -v

## Example
```go
package main

import (
	"github.com/muesli/regommend"
	"fmt"
)

func main() {
	// Accessing a new regommend table for the first time will create it.
	books := regommend.Table("books")

	booksChrisRead := make(map[interface{}]float64)
	booksChrisRead["1984"] = 5.0
	booksChrisRead["Robinson Crusoe"] = 4.0
	booksChrisRead["Moby-Dick"] = 3.0
	books.Add("Chris", booksChrisRead)

	booksJayRead := make(map[interface{}]float64)
	booksJayRead["1984"] = 5.0
	booksJayRead["Robinson Crusoe"] = 4.0
	booksJayRead["Gulliver's Travels"] = 4.5
	books.Add("Jay", booksJayRead)

	recs, _ := books.Recommend("Chris")
	for _, rec := range recs {
		fmt.Println("Recommending", rec.Key, "with score", rec.Distance)
	}

	neighbors, _ := books.Neighbors("Chris")
	...
}
```

To run this example, go to example/ and run:

    go run example.go

## Development
API docs can be found [here](http://godoc.org/github.com/muesli/regommend).
