# Flash

Middleware flash is a tool for share data between requests for [Tango](https://github.com/lunny/tango).

## Installation

    go get github.com/tango-contrib/flash

## Simple Example

```Go

import "github.com/tango-contrib/session"

type FlashAction struct {
    flash.Flash
}

func (x *FlashAction) Get() {
    x.Flash.Set("test", "test")
}

func (x *FlashAction) Post() {
   x.Flash.Get("test").(string) == "test"
}

func main() {
    t := tango.Classic()
    sessions := session.Sessions()
    t.Use(flash.Flashes(sessions))
    t.Any("/", new(FlashAction))
    t.Run()
}
```
