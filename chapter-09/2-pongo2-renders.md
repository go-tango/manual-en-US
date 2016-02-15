# Pongo2 template engine

Middleware tpongo2 is a [pongo2](https://github.com/flosch/pongo2).**v3** template engine support for [Tango](https://github.com/lunny/tango).

## Installation

    go get github.com/tango-contrib/tpongo2

## Simple Example

```Go
package main

import (
    "github.com/lunny/tango"
    "gopkg.in/flosch/pongo2.v3"
    "github.com/tango-contrib/tpongo2"
)

type RenderAction struct {
    tpango2.Renderer
}

func (a *RenderAction) Get() error {
    return a.RenderString("Hello {{ name }}!", pongo2.Context{
        "name": "tango",
    })
}

func main() {
    o := tango.Classic()
    o.Use(tpango2.New())
    o.Get("/", new(RenderAction))
}
```
