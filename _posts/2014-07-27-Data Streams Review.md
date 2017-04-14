---
layout: post
title: Data Streams Review
description: Everything is a stream
modified: 2014-07-27
category: article
imagefeature: pipes.jpg
tags: [reactive, streams]
comments: true
share: true
---

### What is a Stream?
In general stream is an ephemeral flow of data, possibly unbounded in size. More specifically, it is an active process, that involves moving and transforming data. Nice and fun explanation I've found for streams lies [here](http://howtonode.org/streams-explained).

### When do you need Streams?
* Bulk data transfer.
* Real-time data sources.

### Reactive Streams
Reactive Streams is an initiative to provide a standard for asynchronous stream processing with non-blocking back pressure on the JVM. [^1] Lack of backpressure for streaming data means if there's a step that's producing faster than the next step can consume, eventually the entire system will crash. If you have a TCP connection with orders coming in and you need to perform some processing to it before passing it on to another connection, you need to make sure you aren't pulling things off the inbound connection faster than you are able to send to the outbound connection. If you don't, then you'll risk blowing the JVM up with an OutOfMemoryError. [^2]

[^1]: <http://www.reactive-streams.org>

[^2]: [Real-Time Data Streaming Gets Standardized](http://readwrite.com/2014/04/17/real-time-data-streaming-viktor-klang-typesafe-reactivestreams-jvm)

### Streams specification and implementations:
[Streams specification](https://github.com/reactive-streams/reactive-streams)

* Akka streams [(docs)](http://akka.io/docs/) [(template)](https://github.com/typesafehub/activator-akka-stream-scala#master)
* RxJava [(github)](https://github.com/ReactiveX/RxJava)
* Reactor composable [(github)](https://github.com/reactor/reactor)


### Core concepts

#### Upstream
The end where data comes from.

#### Downstream 
The end where data comes to.

#### Back-pressure
A means of flow-control, a way for consumers of data to notify a producer about their current availability, effectively slowing down the upstream source to match their consumption speeds. In the context of Akka Streams back-pressure is always understood as non-blocking and asynchronous

#### Push behavior
Behavior in which systems take events and push them through a signal network to achieve a result.

#### Pull behavior
Behavior in which systems wait until the result is demanded, and work backwards through the network to retrieve the value. demanded.

#### Dynamic Push-Pull
Push behavior when consumer is faster
Pull when producer is faster

#### Codec
Component that converts a stream from one type to another.

#### Source
A processing stage with exactly one output, emitting data elements whenever downstream processing stages are ready to receive them.

#### Sink
A processing stage with exactly one input, requesting and accepting data elements possibly slowing down the upstream producer of elements

#### Flow
A processing stage which has exactly one input and output, which connects its up- and downstreams by transforming the data elements flowing through it.

