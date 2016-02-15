# Routers

## Path

Tango supports 4 forms path:

* static path
```Go
tg.Get("/", new(Action))
tg.Get("/static", new(Action))
```

* named path
```Go
tg.Get("/:name", new(Action))
tg.Get("/(:name)", new(Action))
tg.Get("/:name1/:name2", new(Action))
tg.Get("/:name1-:name2", new(Action))
tg.Get("/(:name1)sss(:name2)", new(Action))
```

* catch-all path
```Go
tg.Get("/*name", new(Action))
tg.Get("/ttt/*name", new(Action))
tg.Get("/sss(*name)", new(Action))
```

* regexp path
```Go
tg.Get("/(:name.*)", new(Action))
tg.Get("/(:name[0-9]+)", new(Action))
tg.Get("/(:name1)-(:name2[0-9]+)", new(Action))
```

## router define

### GET route
```Go
t.Route("GET", "/", new(Action))
```

### custom method route
```Go
type Action struct {}
func (Action) MyPost() {}

t.Route("POST:MyPost", "/", new(Action))
```

### define more route once
```Go
t.Route([]string{"GET:MyGet", "POST"}, "/", new(Action))
```

### define more route once via map
```Go
t.Route(map[string]string{"GET":"MyGet", "POST":"MyPost"}, "/", new(Action))
```

## Router Priority

1. Static router is always first matched before other routers even it was added last.
2. Other routers will order by it's added sequence.

For examples:
```Go
t := tango.Classic()
t.Get("/:name", new(Others))
t.Get("/admin", new(Admin))
t.Run()
```
When you request `/admin`, the `Admin`'s `Get` method will be invoked.

```Go
t := tango.Classic()
t.Get("/:name", new(Admin))
t.Get("/*name", new(Others))
t.Run()
```
When you request `/admin`, the `Admin`'s `Get` method will be invoked. When you request `/admin/ui`, `Others`'s `Get` method will be invoked.

```Go
t := tango.Classic()
t.Get("/*name", new(Admin))
t.Get("/:name", new(Others))
t.Run()
```

`Others`'s `Get` will never be invoked, because all matched requests will be matched to `Admin`'s `Get`.

## Params

The matched params can get By *Context
For named , catch-all or regexp Path: `ctx.Params().Get(":name")`
