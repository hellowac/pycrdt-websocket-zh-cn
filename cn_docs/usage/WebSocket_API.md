传递给 `WebsocketProvider` 和 `WebsocketServer.serve` 的 WebSocket 对象必须实现以下 API，该 API 被定义为 [协议类](../reference/WebSocket.md)：

```py
class WebSocket:

    @property
    def path(self) -> str:
        # 例如，可以是 URL 路径
        # 或者是房间标识符
        return "my-roomname"

    def __aiter__(self):
        return self

    async def __anext__(self) -> bytes:
        # 异步迭代器，用于接收消息
        # 直到连接关闭
        try:
            message = await self.recv()
        except Exception:
            raise StopAsyncIteration()

        return message

    async def send(self, message: bytes):
        # 发送消息
        pass

    async def recv(self) -> bytes:
        # 接收消息
        return b""
```