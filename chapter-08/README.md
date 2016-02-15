* Compress

Tango has a default compress handler to compress indicated static files according extensions like `.js`,`.css`,`.html`. Also, you can use some tango ticks to ask action to compress. For example:

```Go
type CompressExample struct {
	tango.Compress // add this for ask compress according request accept-encoding, if no accept-encoding, not compress
}

func (CompressExample) Get() string {
	return fmt.Sprintf("This is a auto compress text")
}

o := tango.Classic()
o.Get("/", new(CompressExample))
o.Run()
```

```Go
type GZipExample struct {
	tango.GZip // add this for ask compress to GZip, if accept-encoding has no gzip, then not compress
}

func (GZipExample) Get() string {
	return fmt.Sprintf("This is a gzip compress text")
}

o := tango.Classic()
o.Get("/", new(GZipExample))
o.Run()
```

```Go
type DeflateExample struct {
	tango.Deflate // add this for ask compress to Deflate, if not support then not compress
}

func (DeflateExample) Get() string {
	return fmt.Sprintf("This is a deflate compress text")
}

o := tango.Classic()
o.Get("/", new(DeflateExample))
o.Run()
```
