# Static Files

You have two methods to provide static files. One is middlewares, another is actions.

## middlewares

Static lets you make an one line web server.

```Go
func main() {
    t := tango.New(tango.Static())
    t.Run()
}
```

Then, put your files on `./public` folder. You can visit them directly.
For example:
```
http://localhost/images/logo.png  --> ./public/images/logo.png
```

Of course, you can add yourself `handler` to specify the process.
```Go
func main() {
    t := tango.New()
    t.Use(AuthHandler)
    t.Use(tango.Static())
    t.Run()
}
```

Of course, you can use `StaticOptions` to custom your static, for example:
```
t.Use(tango.Static(tango.StaticOptions{Prefix:"static"}))
```

## Actions

## File Action

```Go
tg := tango.New()
tg.Get("/index.html", tango.File("./public/index.html"))
tg.Run()
```

And then visit `http://localhost:8000/index.html`。

## Dir Action

```Go
tg := tango.New()
tg.Get("/:name", tango.Dir("./public"))
tg.Run()
```

And then visit `http://localhost:8000/test.html`。
