# NAT / LoadBalancer Simulator

In order to test NAT and LoadBalancer specific situations, this module contains a simple simulator implementation for a NAT and/or LoadBalancer. It offers an API for own test-implementations, and two example applications.

Usage:

```shell
java -jar cf-nat-<version>.jar [localinterface]:port destination:port [destination2:port2 ...] [-d<messageDropping%>|[-f<messageDropping%>][-b<messageDropping%>]] [-s<sizeLimit>]
```

The NAT receives UDP messages on the local interface and port, creates outgoing sockets for each source endpoint of the received messages, and forwards the message using the new outgoing socket (source-NAT). If the outgoing socket receives a message back, that is the "backwarded" using the local-interface and port.

The NAT waits on the console input. If a newline is read, the NAT reassigns new outgoing sockets
for the entries.

If more than one destination is given, the LoadBalancer is activated.
The LoadBalancer receives UDP messages on the local interface and port, creates outgoing sockets for each source endpoint of the received messages and selects a destination randomly from the provided ones, and forwards the message using the new outgoing socket (source-NAT). If the outgoing socket receives a message back, that is the "backwarded" using the local-interface and port.

The LoadBalancer waits on the console input. If a newline is read, the LoadBalancer reassigns new randomly selected destination to the entries.
