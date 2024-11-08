# 贡献指南

本章节专为希望贡献代码的开发者准备，关于 `pycrdt-websocket` 的贡献指南。

除非另有说明，所有命令应从仓库根目录运行。

## 开发者安装

推荐使用像 [pixi](https://prefix.dev/docs/pixi/overview) 这样的包管理工具。
你需要安装 `pip` 和 `npm`：

```bash
pixi init
pixi add pip nodejs
pixi shell
```

要以可编辑模式安装此项目，并安装运行测试和构建文档所需的可选依赖项：

```bash
pip install -e ".[test,docs]"
```

## 文档

要构建文档并启动服务器：

```bash
mkdocs serve
```

然后在浏览器中打开 [http://127.0.0.1:8000](http://127.0.0.1:8000)。

## 集成测试

首先必须安装 NPM 测试依赖项：

```bash
cd tests/
npm install
cd ..
```

运行集成测试：

```bash
pytest -v
```

## 运行特定的测试文件：

```bash
pytest tests/<文件名>
```

有用的 `pytest` 选项包括：

- `-rP`：打印所有标准输出，默认情况下通过测试时标准输出是隐藏的。
- `-k <测试名称>`：通过测试函数名（而非文件名）运行特定的测试函数。
```