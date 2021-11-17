# gRPC
[Official pages](https://grpc.io/docs/what-is-grpc/introduction/)

gRPC is a modern open source high performance Remote Procedure Call (RPC) framework that can run in any environment. It can efficiently connect services in and across data centers with pluggable support for load balancing, tracing, health checking and authentication. It is also applicable in last mile of distributed computing to connect devices, mobile applications and browsers to backend services.

An RPC is a valid design choice when purely automated operation is more important than evolution and scalability (in Internet time and on an Internet scale).

We can use [BloomRPC](https://github.com/uw-labs/bloomrpc) to test our gRPC services.

![[gRPC.png]]

By default, gRPC uses [[Protocol Buffers]], Google’s mature open source mechanism for serializing structured data (although it can be used with other data formats such as JSON). Here’s a quick intro to how it works. If you’re already familiar with protocol buffers, feel free to skip ahead to the next section.