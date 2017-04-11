# Return Values

According func or method's return values, returnHandle will automatically write content to ResponseWriter.

The return value could be below types or interfaces:

* `string`
Will convert string to []byte and write to ResponseWriter

* `[]byte`
Write to ResponseWriter

* `error`
If error is not nil, Write header 500 and the content is error.Error()

* `AbortError`
if AbortError, Write header AbortError.Code and the content is AbortError.Error()

And if you have an anonymous `tango.JSON` or `tango.XML`, the return value could be:

* `error`
If it's Json, will reproduce {"err": err.Error()}

* `map`
If it's Json, will reproduce json

* `slice`
* `structs`
will reproduce json

For example, we will write a json response.

```Go
type Action struct {
    tango.JSON
}

var i int
func (Action) Get() interface{} {
   if i == 0 {
       i = i + 1
       return map[string]interface{}{"i":i}
   }
   return errors.New("could not visit")
}

func main() {
    t := tango.Classic()
    t.Any("/", new(Action))
    t.Run()
}
```

Of course you can also add HTTP status on return values. For example,

```Go
type Action struct {
    tango.JSON
}

var i int
func (Action) Get() (int, interface{}) {
   if i == 0 {
       i = i + 1
       return 200, map[string]interface{}{"i":i}
   }
   return 500, errors.New("could not visit")
}

func main() {
    t := tango.Classic()
    t.Any("/", new(Action))
    t.Run()
}
```