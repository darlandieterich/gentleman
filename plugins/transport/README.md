# gentleman/transport [![Build Status](https://travis-ci.org/h2non/gentleman.png)](https://travis-ci.org/h2non/gentleman) [![GitHub release](https://img.shields.io/github/tag/h2non/gentleman.svg)](https://github.com/h2non/gentleman/releases) [![GoDoc](https://godoc.org/github.com/h2non/gentleman?status.svg)](https://godoc.org/github.com/h2non/gentleman) [![API](https://img.shields.io/badge/api-beta-green.svg?style=flat)](https://godoc.org/github.com/h2non/gentleman)

gentleman's plugin to easily define the HTTP transport to be used by `http.Client`.

## Installation

```bash
go get -u gopkg.in/h2non/gentleman.v0/plugins/transport
```

## API

See [godoc](https://godoc.org/github.com/h2non/gentleman) reference.

## Example

```go
package main

import (
  "fmt"
  "net/http"
  "gopkg.in/h2non/gentleman.v0"
  "gopkg.in/h2non/gentleman.v0/plugins/transport"
)

func main() {
  // Create a new client
  cli := gentleman.New()

  // Define the default HTTP transport
  cli.Use(transport.Set(http.DefaultTransport))

  // Perform the request
  res, err := cli.Request().URL("http://httpbin.org/headers").End()
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