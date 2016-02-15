# Router Group

Group let's you simple your routers.

There are two ways to use `Group`:
```Go
g := tango.NewGroup()
g.Get("/1", func() string {
    return "/1"
})
g.Post("/2", func() string {
    return "/2"
})

o := tango.Classic()
o.Group("/api", g)
```

Then `/api/1` will match function 1 and `/api/2` will match function 2.

The second way:
```Go
o := tango.Classic()
o.Group("/api", func(g *tango.Group) {
    g.Get("/1", func() string {
	return "/1"
    })
    g.Post("/2", func() string {
	return "/2"
    })
})
```
Then `/api/1` will match function 1 and `/api/2` will match function 2.

Of course, `Group` can has children `Group`:
```Go
o := tango.Classic()
o.Group("/api", func(g *tango.Group) {
    g.Group("/v1", func(cg *tango.Group) {
        cg.Get("/1", func() string {
	    return "/1"
        })
        cg.Post("/2", func() string {
	    return "/2"
        })
    })
})
```
Then `/api/v1/1` will match function 1 and `/api/v2/2` will match function 2.

Sometimes, we only split routers logically, but they has same parent router. Then we can only put blank string to make virtual Groups:
```Go
o := tango.Classic()
o.Group("", func(g *tango.Group) {
    g.Get("/1", func() string {
	return "/1"
    })
})

o.Group("", func(g *tango.Group) {
    g.Post("/2", func() string {
	return "/2"
    })
})
```
Then `/1` will match function 1 and `/2` will match function 2.

Last, you can add middlewares to a group.
```Go
o := tango.Classic()
o.Group("/api/v1", func(g *tango.Group) {
    g.Use(handlers...)
    g.Get("/1", func() string {
    return "/1"
    })
})
```
