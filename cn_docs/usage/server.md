服务器通过 [WebsocketServer](../reference/WebSocket_server.md) 连接多个 `YDoc`。

下面是使用 [websockets](https://websockets.readthedocs.io) 库的代码示例：

```py
import asyncio
from websockets import serve
from pycrdt_websocket import WebsocketServer

async def server():
    async with (
        WebsocketServer() as websocket_server,
        serve(websocket_server.serve, "localhost", 1234),
    ):
        await asyncio.Future()  # 永久运行

asyncio.run(server())
```

Pycrdt-websocket 也可以与 [ASGI](https://asgi.readthedocs.io) 服务器一起使用。下面是使用 [Uvicorn](https://www.uvicorn.org) 的代码示例：

```py
# main.py
import asyncio
import uvicorn
from pycrdt_websocket import ASGIServer, WebsocketServer

websocket_server = WebsocketServer()
app = ASGIServer(websocket_server)

async def main():
    config = uvicorn.Config("main:app", port=5000, log_level="info")
    server = uvicorn.Server(config)
    async with websocket_server:
        task = asyncio.create_task(server.serve())
        while not server.started:
            await asyncio.sleep(0)

        await asyncio.Future()  # 永久运行

asyncio.run(main())
```