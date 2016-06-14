# JSON Handling

There is a powerful built-in json library in go.  

https://golang.org/pkg/encoding/json/

However, there are a number of tips and tricks.


## Custom marshalling for flexible json encodings

http://choly.ca/post/go-json-marshalling/

http://attilaolah.eu/2013/11/29/json-decoding-in-go/

## Testing JSON

Comparing JSON is no fun.  Or map[string]interface{} either, with varying int/float types.  Luckily there is a good solution (you should use this library for testing anyway):

https://gowalker.org/github.com/stretchr/testify/assert#JSONEq

## More powerful reflection handling

Nice article here https://blog.gopheracademy.com/birthday-bash-2014/advanced-reflection-with-go-at-hashicorp/ and some code https://github.com/mitchellh/mapstructure that can take over the type mapping from standard json.

Why?  Well, if we want to inspect a top level key (eg type) before casting it to a specific type.  Or if we want to see which input keys were unusued, rather than ignoring them.  Example code here: https://godoc.org/github.com/mitchellh/mapstructure#Decode  In particular, look at Metadata for reporting unused variables, Errors for good reporting, and WeeklyTypedInput for handling ints like "123" gracefully. And a number of DecodeHooks that can be used.  Kind of like custom marshalling/unmarshalling of json, but it seems more powerful.