# Binding

Middlware binding provides request data binding and validation for [Tango](https://github.com/lunny/tango).

## Installation

	go get github.com/tango-contrib/binding

## Example

```Go
import (
    "github.com/lunny/tango"
    "github.com/tango-contrib/binding"
)

type Action struct {
    binding.Binder
}

type MyStruct struct {
    Id int64
    Name string
}

func (a *Action) Get() string {
    var mystruct MyStruct
    errs := a.Bind(&mystruct)
    return fmt.Sprintf("%v, %v", mystruct, errs)
}

func main() {
    t := tango.Classic()
    t.Use(binding.Bind())
    t.Get("/", new(Action))
    t.Run()
}
```

Visit `/?id=1&name=2` on your browser and you will find output
```
{1 sss}, []
```
