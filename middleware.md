# Middleware

Middleware is like the trusty sidekick of any webapp, doing all the routine work, so we can just get down to coding the real logic.  How does this work in go?

## Stacking middleware

We need some way to add multiple layers of middleware on top of a handler. There are some answers.

The best way to explain this concept is to see this demo how to chain middleware:
  * https://husobee.github.io/golang/http/middleware/2015/12/22/simple-middleware.html

This is a new hot way to chain them:
  * https://github.com/urfave/negroni

Or a minimalistic form:
  * https://github.com/justinas/alice


## Context

Since most handlers just have request and response, how do we pass information between levels (like the logged in user from auth middleware down into handler function that wants the current user...).  Most contexts are implemeneted as `map[interface{}]interface{}`, to leave the logic to you.

*Gorilla*

They provide a nice global context object, you just have to remember to clean it up at the end of every request.
	* http://www.gorillatoolkit.org/pkg/context

*Native golang*

As of golang 1.7, every http.Request object will have this as an extra field.  Probably the easiest way in the future:
	* https://github.com/golang/go/issues/14660#issuecomment-217195496
	* https://godoc.org/golang.org/x/net/context

*Custom Framework*

If you use a custom framework (Gin, Beego, etc.), it probably has this backed in as an extra argument.  Look at your docs.