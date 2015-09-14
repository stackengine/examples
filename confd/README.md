Confd Examples
==============

This folder contains examples of using Confd with StackEngine for an nginx reverse proxy or haproxy.

You can download confd from http://www.confd.io/. You may need to build confd with gb until the StackEngine backend is accepted into the new release.

To build confd, you will need to install [gb](http://getgb.io) `go get github.com/constabulary/gb`

Clone confd, cd to it and run `gb build all`

To start up confd using StackEngine as a backend, you can run this command:

```
sudo ./bin/confd -backend stackengine -confdir /path/to/examples/confd/haproxy -node <your_stackengine_node_url> -scheme https -auth-token <your_stackengine_auth_token>
```

Example:
```
sudo ./bin/confd -backend stackengine -node mesh-01:8443 -scheme https -auth-token 48de1cc472b6a81f
```

On the stackengine side, you can run this example with a docker image named "karthequian:helloworld/latest" saved as a component called "hello". At config time, map the stack to a dynamic port for the host, and container port to :80. You'll want to call your instance "i1". You can call this something else, but will need to update your toml and tmpl files to associate correctly with appropriate service discovery sections from StackEngine.

To configure haproxy for only one app, add it to the keys section of the `haproxy.toml` file. In this file, there is a commented line `perpool-wordpress-80`. Remove the line `"",` and uncomment this line. The resulting haproxy config should only list the containers up for the "perpool-wordpress-80" application.

Check HAproxy
HAProxy runs a stats page at ${HAPROXY_HOST}:1936. This is helpful for debugging your configuration.
