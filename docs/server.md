# VolView 服务器指南

VolView服务器扩展了具有远程处理功能的VolView查看器。它与基于python的代码集成，并将该功能直接暴露在查看器中。

## 快速开始

要开始使用这个VolView服务器示例，有两个部分:服务器和查看器。

### 启动服务器

最简单的入门方法是安装 [Poetry](https://python-poetry.org/) 并创建一个新的Python环境来运行VolView服务器。

```
cd ./server/
poetry install
```
VolView代码库在 `server/examples/` 中提供了几个示例api，它们与VolView查看器中的远程函数示例一起工作。

- `server/examples/example_api.py`: 终端示例的基本集合
- `server/examples/example_class_api.py`: 终端使用类的示例

要使用样例API运行服务器，请运行以下命令。

```
cd ./server/
poetry run python -m volview_server -P 4014 ./examples/example_api.py
```

### 运行Viewer

我们首先需要告诉查看器服务器在哪里运行。复制 `.env.example` 到 `.env` 并编辑服务器URL为以下值:

```
VITE_REMOTE_SERVER_URL=http://localhost:4014/
```

在与服务器终端分开的终端中，我们将运行该应用程序。

```
npm install
npm run build
npm run preview
```

预览服务器可在 http://localhost:4173/ 上获得。导航到 “Remote Functions” 选项卡，探索由 `examples/example_api.py` 脚本定义的可用远程功能。

- 添加数字:添加两个数字的简单API
- 随机数:通过获取一个随机数的琐事来演示异步API支持。
- 进度:通过一个简单的定时进度计数器演示异步生成器。
- 中值过滤器:对当前图像运行中值过滤器。演示ITK和VTK图像序列化以及客户端存储访问，以及在子进程中运行ITK过滤器以避免线程阻塞。

## 深入的指导

本指南将介绍如何安装、使用、自定义和部署VolView
服务器。

### Server Installation

VolView服务器通过[Poetry](https://python-poetry.org/)进行设置。要手动安装依赖项，请阅读`pyproject.Toml`文件并从 `[tool.poem.dependencies]` 条目中提取依赖项。
如果你正在使用 Poetry，你可以继续安装依赖并设置VolView环境，如下所示:

```
cd ./server/
poetry install
```

### 编写自己的api

首先，下面是一个非常简单的RPC API的定义，它将两个数字相加。

```python
from volview_server import VolViewApi

volview = VolViewApi()

@volview.expose
def add(a: int, b: int):
    return a + b
```

The `volview.expose` decorator exposes the `add` function with the public name
`add`. A custom public name can be passed in via `volview.expose(name)`.

`volview.expose` 装饰器将 `add` 函数公开为公共名称 `add`。一个自定义的公共名称可以通过 `volview.expose(name)` 传入。
```python
# Accessible via the RPC name "my_add" 可通过RPC名称“my_add”访问
@volview.expose("my_add")
def add(a: int, b: int):
    return a + b
```

#### 自定义对象编码

如果已经编码了具有本地Python表示的对象，则可以添加自定义序列化器和反序列化器来正确处理这些对象。

序列化器/反序列化器函数应该返回转换后的结果，或者在没有应用转换的情况下传递输入。


```python
from datetime import datetime
from volview_server import VolViewApi

DATETIME_FORMAT = "%Y%m%dT%H:%M:%S.%f"

def decode_datetime(obj):
    if "__datetime__" in obj:
        return datetime.strptime(obj["__datetime__"], DATETIME_FORMAT)
    return obj

def encode_datetime(dt):
    if isinstance(dt, datetime):
        return {"__datetime__": dt.strftime(DATETIME_FORMAT)}
    return dt

volview = VolViewApi()
volview.serializers.append(encode_datetime)
volview.deserializers.append(decode_datetime)

@volview.expose
def echo_datetime(dt: datetime):
    print(type(dt), dt)
    return dt
```

#### 异步支持

asyncio支持异步方法。

```python
import asyncio
from volview_server import VolViewApi

volview = VolViewApi()

@volview.expose
async def sleep():
    await asyncio.sleep(5)
    return "woke up"
```

#### 通过流式异步生成器取得进度

如果公开的方法是异步生成器，则该函数将自动视为流方法。流式方法通过 `client.stream(...)` 而不是 `client.call(...)` 调用。查看 `client.stream` 流文档获取更多细节。

```python
import asyncio
from volview_server import VolViewApi

volview = VolViewApi()

@volview.expose
async def progress():
    for i in range(100):
        yield { "progress": i }
        await asyncio.sleep(0.1)
```

#### 访问客户端存储

RPC方法可以使用 `get_current_client_store(store_name)` 访问客户端应用程序存储。该特性允许服务器控制调用客户机并进行修改，例如添加新图像、更新注释、切换已查看的图像等等。

使用此功能的一个示例是 `examples/example_api.py` 中的 `medianFilter` RPC示例。

```python
import asyncio
from volview_server import VolViewApi

volview = VolViewApi()

@volview.expose
async def access_client():
    store = get_current_client_store('images')
    image_id_list = await store.idList

    new_image = create_new_itk_image()
    await store.addVTKImageData('My image', new_image)
```

#### RPC 路由器

RPC路由器允许自定义处理RPC路由。例如，路由方法可以位于命名空间或限定作用域的场景中，比如类。如果需要，路由器也可以扩展以进一步定制。

关于如何使用 `RpcRouter` 类以及如何将路由器添加到 `VolViewApi`，请参阅 `examples/example_class_api.py`。
### 从客户端调用 RPC 方法

VolView在服务器存储中保留了一个全局客户端对象，可以通过 `const
{ client } = useServerStore()` 访问。

使用 `result = await client.call(endpoint, [arg1, arg2, ...])` 调用服务器端RPC端点。
```js
const result = await client.call('add', [1, 2])
```
使用 `await client.stream(endpoint, onStreamData)` 调用服务器端RPC流。

```typescript
const onStreamData = (data: StreamData) => {
  const { progress } = data
  console.log('current progress: ', progress)
}

let done = false
await client.stream('progress', onStreamData)
let done = true
```

### 部署

VolView服务器自带基于http的服务器，可以通过 `volview_server` 模块运行。

```
python -m volview_server [...options] api_script.py
```

默认情况下， `volview_server` 期望 `api_script.py` 模块包含 `volview` 符号。如果VolView API在不同的名称下，请将其添加到模块文件名的末尾，并使用冒号。

```python
from volview_server import VolViewApi

my_volview_api = VolViewApi()
...
```

```
python -m volview_server [...options] api_script.py:my_volview_api
```
服务器支持 [python-socketio 支持的部署策略](https://python-socketio.readthedocs.io/en/latest/server.html#deployment-strategies)以及公开与ASGI兼容的中间件。

#### ASGI

`VolViewApi` 对象可以作为ASGI兼容框架或服务器的中间件。

```
from volview_server import VolViewApi

app = SomeASGIApp()

# 添加VolView中间件
volview = VolViewApi()
app = VolViewApi(app)
```

VolView API的路径可以自定义，以及许多其他属性。
公开的关键字参数为 `VolViewApi(app, server_kwargs={}, asgi_kwargs={})` 。
- `server_kwargs`:参见<https://python-socketio.readthedocs.io/en/latest/api.html#asyncserver-class>
- `asgi_kwargs`:参见<https://python-socketio.readthedocs.io/en/latest/api.html#asgiapp-class>
- 
##### FastAPI中间件示例

FastAPI是一个兼容 ASGI 的web框架。本指南将介绍在 `examples/example_fastapi.py` 中找到的FastAPI示例。

首先安装 `FastAPI` 和 `uvicorn[standard]`。

```
python -m pip install FastAPI 'uvicorn[standard]'
```
要启动FastAPI服务器，使用 `uvicorn`，如下所示。
```
uvicorn examples.example_fastapi:app
```
编辑VolView `.env` 文件指向FastAPI服务器:
```
VITE_REMOTE_SERVER_URL=http://localhost:8000/
```

重新构建VolView查看器应用程序并导航到 "Remote Functions" 选项卡以验证服务器是否正常工作。

###### 改变 socket.io 路径

如果默认 `https://your-host/socket.io/` 路径与现有路由冲突，VolView 可以配置为使用不同的路径。在本指南中，我们将重命名默认的 `/socket.io/` 为 `/my-custom-path/`。

在服务器端，VolView中间件必须配置新路径，如下所示。

```python
app.add_middlware(volview, asgi_kwargs={"socketio_path": "/my-custom-path"})
```
然后，必须更新VolView客户端服务器URL以匹配。下面的代码将服务器URL设置为 `.env` 的文件。

```
VITE_REMOTE_SERVER_URL=http://localhost:8000/my-custom-path
```

重新启动服务器和客户端以验证是否实现了成功的连接。

#### Python-socketio 支持的部署策略

您可以遵循[部署策略](https://python-socketio.readthedocs.io/en/latest/server.html#deployment-strategies)
由python-socketio项目支持，该项目为VolView服务器提供动力。为此，您需要访问底层的socket.io
实例。

```python
from volview_server import VolViewApi
from volview_server.rpc_server import RpcServer

volview = VolViewApi()
...

server = RpcServer(volview, ...)
# 检索 socket.io 实例
sio = server.sio
sio.attach(...)
```