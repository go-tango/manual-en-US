# Handler

Handler is the middleware of tango. In tango, almost everything will be Handler. Write your Handlers are easy.

```Go
type Handler interface {
    Handle(*tango.Context)
}
```

For example:
```Go
func MyHandler() tango.HandlerFunc {
    return func(ctx *tango.Context) {
        fmt.Println("this is my first tango handler")
        ctx.Next()
    }
}

t := tango.Classic()
t.Use(MyHandler())
t.Run()
```

Another form:
```
type HelloHandler struct {}

func (HelloHandler) Handle(ctx *tango.Context) {
    fmt.Println("before")
    ctx.Next()
    fmt.Println("after")
}

t := tango.Classic()
t.Use(new(HelloHandler))
t.Run()
```

Also, you can directly use a function as your handler:
```Go
tg.Use(func(ctx *tango.Context){
    fmt.Println("before")
    ctx.Next()
    fmt.Println("after")
})
```

For compitable, tango supports your old form handler via UseHandler()

```Go
tg.UseHandler(http.Handler(func(resp http.ResponseWriter, req *http.Request) {

}))
```
Old handler will be called before action invoked.

# Call stack
When a request call by tango, below is the call stack:
```
tango.ServeHttp
|--Handler1
      |--Handler2
            |-- ...HandlerN
                      |---Action(If matched)
                ...HandlerN--|
         Handler2 ----|
   Handler1--|
(end)--|
```

In your Handler, all codes before `ctx.Next()` will be called before Action(If matched) will be called. All codes after `ctx.Next()` will be called after Action(If matched) called.

Of course, If your handler **DO NOT** call `ctx.Next()`. All call stack after will be not executed.
