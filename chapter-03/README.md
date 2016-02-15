# Context

Context has many convenient method for complete your work.

## `Req()`
Get *Request object.

## `Forms()`
Get query value by query key. See [Forms](Forms)

## `Cookies()`
Get Cookies object.

## `SecureCookies()`
Get secure Cookies.

## `ServeFile()`
Send file to web browser.

## `ServeJson()`
Send Json to web browser.

## `ServeXml()`
Send Xml to web browser.

## `Download()`
Download some file.

## `SaveToFile()`
Save uploaded file to disk file.

## `Params()`
Get router's matched params.

## `Action()`
If executor is a struct, then return the pointer of struct, or return nil.

## `Redirect()`
Write redirect to web browser.

## `NotModified()`
Return 304.

## `Unauthorized()`
Return unauthorized.

## `NotFound()`
Return 404

## `Abort()`
Return customized error.
