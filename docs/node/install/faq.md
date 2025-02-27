# FAQ

## General

### Is there any benefits for running a node?

There is no financial incentive to run a node, doing so helps increase the security of the network.


### Are nodes visible anywhere?

Public nodes can be seen on [nodespyder](https://ergo.nodespyder.io/). Please note that unless you are running the node on a publicly accessible web-server, your node should be protected by your router. 


- To run a public node see this example [nginx.conf](https://github.com/glasgowm148/ergoscripts/blob/main/misc/nginx.config) available.  
- Using a [remote node](https://github.com/ergoplatform/ergo/blob/master/src/main/resources/mainnet.conf) is insecure, please use them with caution.

### How do I safely shut down?

```
curl -X POST "http://127.0.0.1:9053/node/shutdown" -H "api_key: hello"
```

If you cannot safely shut-down, you can kill the ports. 

```
kill -9 $(lsof -t -i:9053)
kill -9 $(lsof -t -i:9030)
```






## Running the node

### Minimum Requirements

The node uses Java so should work across all operating systems. You can even run on a [Raspberri Pi](/docs/node/install/pi.md). 

> Note that due to the intensive disk I/O, 4-6GB of ram is recommended with a fast SSD, running with the `-Xmx4G` flag on JVM9/11

### Commands

Please see the section on [swagger](../swagger.md)

### Security

Unless you are running the node on a publicly accessible web-server, your node should be protected by your router. 

If you wish to host a public node, there are a few important aspects your wallet and money's safety depends on:

* You should never make the `ergo.conf` file public.
* Sensitive API methods require a security token, which should never be sent over untrusted channels.
* Access to the Ergo REST API must be restricted to known hosts. In particular, the API must not be accessible from the Internet.

### Compiling from source

Instead of downloading the precompiled Ergo jar, you can clone the repository and compile the jar from the source using the [`sbt assembly`](https://www.scala-sbt.org/)  command.


