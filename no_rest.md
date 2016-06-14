# REST Alternatives

REST with a JSON (or XML) payload is nice and standard and it is easy to write clients for it. However, it is not the most performant solution, and especially for internal API usage (microservices) or for an app with lots of data transfer, there may be better solutions.  Here is a look at some.

## gRPC

This is an efficient rpc library using HTTP/2.0 for communication (reuse auth middleware), and protocol buffers for data transport.

https://husobee.github.io/golang/rest/grpc/2016/05/28/golang-rest-v-grpc.html

https://husobee.github.io/golang/grpc/2016/03/22/grpc-exploration.html

## Kite

This is bi-directional RPC over websockets and service discovery, rolled into one package for orchestrating swarms of microservices.  Can also connect to a browser through a proxy or directly with a js library (this is websockets after all)

https://github.com/koding/kite

