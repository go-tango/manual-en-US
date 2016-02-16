# Session Tracker

Tracker is the session's track methods. Default tracker is `CookieTracker` which store SessionID on the cookie. And we provide `HeaderTracker`. For example:

```Go
sess := session.New(session.Options{
	Tracker: session.NewHeaderTracker(session.DefaultSessionIdName),
	MaxAge: sessionTimeout,
})
```

HeaderTracker will read the http request's Header which named `session.DefaultSessionIdName` to track the session.
