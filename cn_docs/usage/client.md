客户端通过 [WebsocketProvider](../reference/WebSocket_provider.md) 连接他们的 `YDoc`。

下面是使用 [websockets](https://websockets.readthedocs.io) 库的代码示例：

```py
import asyncio
import y_py as Y
from websockets import connect
from pycrdt_websocket import WebsocketProvider

async def client():
    ydoc = Y.YDoc()
    async with (
        connect("ws://localhost:1234/my-roomname") as websocket,
        WebsocketProvider(ydoc, websocket),
    ):
        # 对远程 ydoc 的更改会应用到本地 ydoc。
        # 对本地 ydoc 的更改会通过 WebSocket 发送，并广播给所有客户端。
        ymap = ydoc.get_map("map")
        with ydoc.begin_transaction() as t:
            ymap.set(t, "key", "value")

        await asyncio.Future()  # 永久运行

asyncio.run(client())
```