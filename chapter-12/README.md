# Events

## Installation

```
go get github.com/tango-contrib/events
```

## Usage

Your can execute your codes before and after struct methods:
```Go
type EventAction struct {
	tango.Ctx
}

func (c *EventAction) Get() {
	c.Write([]byte("get"))
}

func (c *EventAction) Before() {
	c.Write([]byte("before "))
}

func (c *EventAction) After() {
	c.Write([]byte(" after"))
}

func main() {
    t := tango.Classic()
    t.Use(events.Events())
    t.Get("/", new(EventAction))
    t.Run()
}
```
