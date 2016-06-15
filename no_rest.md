# REST Alternatives

REST with a JSON (or XML) payload is nice and standard and it is easy to write clients for it. However, it is not the most performant solution, and especially for internal API usage (microservices) or for an app with lots of data transfer, there may be better solutions.  Here is a look at some.

## gRPC

This is an efficient rpc library using HTTP/2.0 for communication (reuse auth middleware), and protocol buffers for data transport.

https://husobee.github.io/golang/rest/grpc/2016/05/28/golang-rest-v-grpc.html

https://husobee.github.io/golang/grpc/2016/03/22/grpc-exploration.html

## Kite

This is bi-directional RPC over websockets and service discovery, rolled into one package for orchestrating swarms of microservices.  Can also connect to a browser through a proxy or directly with a js library (this is websockets after all)

https://github.com/koding/kite


## Micro

This is a full-featured framework for building microservices, including service discovery, rpc calls, message brokering, etc. See the list here: https://github.com/micro/micro#the-ecosystem 

They are fully commited to golang, and build on some external services to provide features, notably consul. https://github.com/micro/go-micro#features However, this can be adjusted by plugins, and they support using NATS not only as a message broker, but also for rpc and service discovery: https://blog.micro.mu/2016/04/11/micro-on-nats.html

A nice overview of the project is on the FAQ: https://github.com/micro/micro/wiki/FAQ

## Distributed Systems

Yes, that is the proper name for all these post-REST systems.  There are plenty of interesting CS papers in this area.  Maybe check out:

  * http://bravenewgeek.com/from-the-ground-up-reasoning-about-distributed-systems-in-the-real-world/
  * https://medium.com/@jlouis666/how-to-build-stable-systems-6fe9dcf32fc4#.3j1odjamv
  