# Quick Start

## Installation

Install Tango,

```go
go get github.com/lunny/tango
```

A classic example of Tango is below:

```go
package main

import (
    "errors"
    "github.com/lunny/tango"
)

type Action struct {
    tango.JSON
}

func (Action) Get() interface{} {
    if true {
        return map[string]string{
            "say": "Hello tango!",
        }
    }
    return errors.New("something error")
}

func main() {
    t := tango.Classic()
    t.Get("/", new(Action))
    t.Run()
}
```

And then you can visit `http://localhost:8000` on your web browser, you will get a json result.
```
{"say":"Hello tango!"}
```

If you change the code above from `true` to `false`, you will get another result.
```
{"err":"something error"}
```

Because this code has embbeded `tango.JSON`, so the return value could be converted to json automatically.

## Usage

`Tango` object is the beginning of all the things. Generally, just call ```tango.Classic()```, you will create a Tango object. For example:

```Go
func main() {
    t := tango.Classic()
    t.Use(...)
    t.Get(...)
    t.Run()
}
```

Of course, you can give a custom Log, default outpu is os.StdOut,

```Go
import "github.com/lunny/log"

l := log.New(out, "[tango] ", log.Ldefault())
l.SetOutputLevel(log.Ldebug)
t := tango.Classic(l)
```

Logger is an interface, so you can use your self log component.

You also can call `New` to custom tango. For example for a static web server:

```Go
func main() {
   t := tango.New(tango.Static(tango.StaticOptions{Prefix:"public"}))
   t.Run()
}
```
Then, you can visit your `./public` directory files via web browser.

Also, tango provide `NewWithLog`.

* `NewWithLog(Logger, ...tango.Handler)`
