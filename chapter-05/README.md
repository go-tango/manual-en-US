# Logger

Logger is an interface, default it will use (https://github.com/lunny/log)[https://github.com/lunny/log] as log implement if you do not define your own log.

```Go
type Logger interface {
	Debugf(format string, v ...interface{})
	Debug(v ...interface{})
	Infof(format string, v ...interface{})
	Info(v ...interface{})
	Warnf(format string, v ...interface{})
	Warn(v ...interface{})
	Errorf(format string, v ...interface{})
	Error(v ...interface{})
}
```

You can custom your log
```Go
l := log.New(out, "[tango] ", log.Ldefault())
l.SetOutputLevel(log.Ldebug)
t := tango.Classic(l)
t.Run()
```
