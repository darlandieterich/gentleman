# gentleman/query [![Build Status](https://travis-ci.org/h2non/gentleman.png)](https://travis-ci.org/h2non/gentleman) [![GitHub release](https://img.shields.io/github/tag/h2non/gentleman.svg)](https://github.com/h2non/gentleman/releases) [![GoDoc](https://godoc.org/github.com/h2non/gentleman?status.svg)](https://godoc.org/github.com/h2non/gentleman) [![API](https://img.shields.io/badge/api-beta-green.svg?style=flat)](https://godoc.org/github.com/h2non/gentleman)

gentleman's plugin to easily manage HTTP query params.

## Installation

```bash
go get -u gopkg.in/h2non/gentleman.v0/plugins/query
```

## API

See [godoc](https://godoc.org/github.com/h2non/gentleman/plugins/query) reference.

## Example

```go
package main

import (
  "fmt"
  "gopkg.in/h2non/gentleman.v0"
  "gopkg.in/h2non/gentleman.v0/plugins/query"
  "gopkg.in/h2non/gentleman.v0/plugins/url"
)

func main() {
  // Create a new client
  cli := gentleman.New()

  // Define the base URL to use
  cli.Use(url.BaseURL("http://httpbin.org"))
  cli.Use(url.Path("/get"))

  // Define a custom query param
  cli.Use(query.Set("foo", "bar"))

  // Remove a query param
  cli.Use(query.Del("bar"))

  // Perform the request
  res, err := cli.Request().End()
  if err != nil {
    fmt.Printf("Request error: %s\n", err)
    return
  }
  if !res.Ok {
    fmt.Printf("Invalid server response: %d\n", res.StatusCode)
    return
  }

  fmt.Printf("Status: %d\n", res.StatusCode)
  fmt.Printf("Body: %s", res.String())
}
```

## License

MIT - Tomas Aparicio