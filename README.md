# GameCore.Socket

This project is used to quickly build game services


## How to build

You require the following to build Project:
* JDK8
* Gradle


## Easy Building:
* Tcp Socket Server
* WebSocket Server
* Rpc Server



# Usage


## :: TcpSocket ::

```
public void startTcp() throws Exception{
    //Boot Param
    ConfigEntry conf = ConfigEntry.build().builder("IP","127.0.0.1").builder("PORT",7777);

    //onConnect
    IConnect connecter = new IConnect() {
        @Override
        public void onConnect(Channel channel) {
            log(":: onConnect ::");
        }
    };

    //onDisconnect
    IDisconnect disconnect = new IDisconnect() {
        @Override
        public void onDisconnect(Channel channel) {
            log(":: onDisConnect ::");
        }
    };


    //onMessageReceived
    IData onData = new IData() {
        @Override
        public void onData(ServerMessage message, Channel channel) {
            log(":: onMessageRecive ::");
        }
    };

    //Start Tcp Server
    new com.gamecoder.core.tcp.Booter().start(conf,new TcpBootHandler(Optional.empty(),connecter,disconnect,onData));
}
```


## :: Websocket ::
```
public void startWebSocket() throws Exception{
    //Boot Param
    ConfigEntry conf = ConfigEntry.build().builder("IP","127.0.0.1").builder("PORT",8888);

    //onConnect
    IConnect connecter = new IConnect() {
        @Override
        public void onConnect(Channel channel) {
            log(":: onConnect ::");
        }
    };

    //onDisconnect
    IDisconnect disconnect = new IDisconnect() {
        @Override
        public void onDisconnect(Channel channel) {
            log(":: onDisConnect ::");
        }
    };

    //on Http MessageReceived
    IHttpData httpData = new IHttpData() {
        @Override
        public void onData(FullHttpRequest request, Channel channel) {
            log(":: onHttpMessageReceived ::");
        }
    };

    //on Websocket MessageReceived
    IWebSocketData webSocketData = new IWebSocketData() {
        @Override
        public void onData(ChannelHandlerContext ctx, String data) {
            log(":: onWebSocketMessageReceived ::");
        }
    };

    //Start WebSocket Server
    new com.gamecoder.core.websocket.Booter().start(conf,new WebSocketBootHandler(Optional.empty(),connecter,disconnect,webSocketData,httpData));
}
```


## :: RPC ::
```
public void startRpc() throws Exception{
    //Boot Param
    ConfigEntry conf = ConfigEntry.build().builder("IP","127.0.0.1").builder("PORT",9999);

    //on Http MessageReceived
    IHttpData httpData = new IHttpData() {
        @Override
        public void onData(FullHttpRequest request, Channel channel) {
            log(":: onHttpMessageReceived ::");
        }
    };

    //Start Rpc Server
    new com.gamecoder.core.rpc.Booter().start(conf,new RpcBootHandler(Optional.empty(),httpData));
}
```