# Multiple Tango

Dispacth middleware let you composite your multiple tango.

# Example

```Go
import (
    "github.com/lunny/tango"
    "github.com/tango-contrib/dispatch"
)

func main() {
    logger := tango.NewLogger(os.Stdout)
    t1 := tango.NewWithLog(logger)
    t2 := tango.NewWithLog(logger)

    dispatch := dispatch.New(map[string]*tango.Tango{
        "/": t1,
        "/api/": t2,
    })

    t3 := tango.NewWithLog(logger)
    t3.Use(dispatch)
    t3.Run(":8000")
}
```
