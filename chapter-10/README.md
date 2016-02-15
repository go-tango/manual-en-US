# Session

Session is a session middleware for [Tango](https://github.com/lunny/tango).

## Backend Supports

Currently session support some backends below:

* Memory - memory as a session store
* [Redis](http://github.com/tango-contrib/session-redis) - redis server as a session store
* [Ledis](http://github.com/tango-contrib/session-ledis) - ledis server as a session store
* [nodb](http://github.com/tango-contrib/session-nodb) - nodb as a session store
* [ssdb](http://github.com/tango-contrib/session-ssdb) - use ssdb server as a session store

## Installation

    go get github.com/tango-contrib/session

## Simple Example

```Go
package main

import (
    "github.com/lunny/tango"
    "github.com/tango-contrib/session"
)

type SessionAction struct {
    session.Session
}

func (a *SessionAction) Get() string {
    a.Session.Set("test", "1")
    return a.Session.Get("test").(string)
}

func main() {
    o := tango.Classic()
    o.Use(session.New(session.Options{
        MaxAge:time.Minute * 20,
        }))
    o.Get("/", new(SessionAction))
}
```
For other store,
```Go
func main() {
    o := tango.Classic()
    o.Use(session.New(session.Options{
        MaxAge:time.Minute * 20,
        Store: redistore.New(Options{
			Host:    "127.0.0.1",
			DbIndex: 0,
			MaxAge:  30 * time.Minute,
		},
        }))
    o.Get("/", new(SessionAction))
}
```
