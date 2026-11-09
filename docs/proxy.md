# Reverse proxy

Rig ships a reverse proxy. It is the front door for a session and the front door for a deploy.

The repo config names the routes: which host and path forward to which service, which routes are WebTransport, which are WebSocket, which are plain HTTP. Rig generates the proxy config from that. The agent does not write a proxy file.

The proxy speaks HTTP/3, HTTP/2, and HTTP/1.1 on the same listener. WebTransport and secure WebSocket are first-class. They are not a bolted-on module that breaks when the framing changes. REST is the same listener.

It is written in Rust. It is a standalone binary. In a session it runs on the bridge. In a deploy the same binary is what the pipeline places into Kubernetes, ECS, or the Azure container service. The config is the same. The rendering is the plugin.

YARP is not used. Current nginx and Envoy builds are not used for the WebTransport path. The proxy is Rig's because those do not handle WebTransport correctly, and the deploy has to be the same binary the session already ran.

The agent asks for a route change by editing the repo config. Rig reloads the proxy. A route that does not match a service is an error on the panel, not a 502 the agent has to discover.
