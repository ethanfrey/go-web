# Messaging

HTTP Rest calls, or the more general Request-Reply communication protocol is nice for synchronous calls.  However, when there are many decoupled systems, that just need to notify the next system of their state ("a new image is ready for processing"), this is not the best approach.  A Pub-Sub or Message Queuing protocol is more appropriate in this case.

However, what to use?

Here is an interesting comparison of various messaging queues: http://bravenewgeek.com/dissecting-message-queues/

## Nanomsg

This is a new package with a similar concept to zeromq, but rebuilt from the lessons learned there.  That said, it is not a server, but rather a rather low level library you can use to wire together many components in a distributed system.  It is more complex than needed for many apps that all sit in one data center, but it makes a good reads on the various "scalabilty protocols" they implement, which describe types of communication: http://nanomsg.org/index.html

This compares nanomsg with zeromq and has some nice diagrams of the protocols: http://bravenewgeek.com/a-look-at-nanomsg-and-scalability-protocols/

## NATS (http://nats.io/)

This seems quite the contender for speed and scalability, while offering nice features.  In the above article about disecting message queues, it was clearly the fastest and lowest latency contender for a brokered solution (not nanomsg or zeromq).  It also is a static binary (one file) and offers easy clustering for simple DevOps. The go client also allows using channels for pub/sub, which can be nice for selecting.

A nice overview:
  * http://thenewstack.io/nats-rest-alternative-provides-messaging-distributed-systems/

More documentation:
  * https://github.com/nats-io/gnatsd  (the server)
  * https://github.com/nats-io/nats  (the golang client)
  * http://nats.io/documentation/concepts/nats-queueing/ (queuing)

Why not? The only issues I see is the lack of persistance and "at most once" delivery.  Rather than keeping a log of all messages, and recording which ones were ack-ed after processing, it just makes a best attempt at delivery and doesn't worry about what the subscriber does afterwards.  This is fine in most cases, but if you need "at LEAST once" delivery, then pick another broker, or add some client logic for retrying...


## Kafka?

New big thing from Apache.  Offers guaranteed delivery.  Pretty good throughput (about 30-40% of NATS), but much higher latency, on the order of a few seconds under load.

  * http://kafka.apache.org/

TODO: more analysis

## RabbitMQ

The good, old standby.  But in my experience, not the easiest to monitor or configure, and not the most efficient.