---
category: general
date: 2026-06-21
description: 学习如何构建 Docker 镜像并使用适当的端口映射运行 Docker 容器。包括 docker run 端口映射和在 Docker 中暴露端口。
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: zh
og_description: 构建 Docker 镜像并使用正确的端口映射运行 Docker 容器。几分钟内掌握 Docker 运行端口映射和在 Docker 中暴露端口。
og_title: 构建 Docker 镜像并运行 Docker 容器 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to build docker image and run docker container with proper
    port mapping. Includes docker run port mapping and expose port in docker.
  headline: Build Docker Image and Run Docker Container – Complete Guide
  type: TechArticle
- description: Learn how to build docker image and run docker container with proper
    port mapping. Includes docker run port mapping and expose port in docker.
  name: Build Docker Image and Run Docker Container – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Docker Engine installed (Desktop or Engine 20.10+). - Basic familiarity
      with the command line. - A tiny web app (we’ll use a one‑line Python Flask server,
      but you can swap it for anything).'
  - name: Verify the Image Exists
    text: 'Run `docker images` and look for `myflaskapp`:'
  - name: Detaching the Container (Optional)
    text: 'If you don’t want the terminal to be blocked, add `-d` to run in the background:'
  - name: Using `docker run` with Different Host Ports
    text: 'Sometimes you might already have something listening on host port 5000.
      No problem—just map to a different host port:'
  - name: Building Multi‑Stage Images (Advanced)
    text: 'If you ever need a smaller final image, you can **build docker image**
      with a multi‑stage Dockerfile:'
  type: HowTo
tags:
- docker
- containers
- devops
title: 构建 Docker 镜像并运行 Docker 容器 – 完整指南
url: /zh/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 构建 Docker 镜像并运行 Docker 容器 – 完整指南

有没有想过如何为一个简单的 Web 应用 **构建 Docker 镜像**，然后顺利地让它运行起来？你并不孤单——很多开发者在第一次接触容器化时都会遇到同样的难题。在本教程中，我们将完整演示整个流程，从编写 Dockerfile、暴露正确的端口，到使用 `docker run` 将端口映射到主机。完成后，你将清楚地知道如何 **运行 Docker 容器** 并进行正确的端口映射，并了解在 Docker 中暴露端口的重要性。

我们会覆盖所有必需的内容：精确的 `docker build` 命令、如何 **从 Dockerfile 构建 Docker 镜像**、`docker run` 端口映射的细节，以及快速的检查方法，确保容器真的在你期望的端口上监听。没有废话，只有动手实操的逐步指南，你可以直接复制粘贴到终端执行。

## 你将实现的目标

- 为 Node.js（或任意）应用编写一个最小化的 Dockerfile。  
- 使用官方 CLI 语法 **构建 Docker 镜像**。  
- 理解 Dockerfile 中的 `EXPOSE` 与 `docker run` 中 `-p` 标志之间的区别。  
- 使用 `docker run` 端口映射 **运行 Docker 容器**，从而在 `http://localhost:5000` 访问服务。  
- 诊断常见的坑，例如忘记暴露端口或主机‑容器端口不匹配。

### 前置条件

- 已安装 Docker Engine（Desktop 或 Engine 20.10+）。  
- 基本的命令行使用经验。  
- 一个小型 Web 应用（我们将使用一行代码的 Python Flask 服务器，你也可以换成其他语言）。

如果你满足以上条件，下面开始吧。

---

## 第一步：创建一个简单的应用

首先，需要准备一个待容器化的程序。创建一个名为 `myapp` 的文件夹，并在其中放入单个文件 `app.py`：

```python
# app.py
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello from Docker!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

> **小技巧：** `host="0.0.0.0"` 这一行让 Flask 监听所有网络接口，这是 Docker 能够把流量从主机转发进去的前提。

现在，你已经拥有一个在容器内部监听 5000 端口的微型 Web 服务。

## 第二步：编写 Dockerfile（从 Dockerfile 构建镜像）

接下来，需要一个 **Dockerfile** 来告诉 Docker 如何组装镜像。将此文件放在 `app.py` 同目录下：

```dockerfile
# Dockerfile
FROM python:3.11-slim

# Install Flask
RUN pip install flask

# Copy our app into the image
COPY app.py /app/app.py

WORKDIR /app

# Expose the internal port (does NOT publish it yet)
EXPOSE 5000

# Default command to run the app
CMD ["python", "app.py"]
```

需要注意的几点：

- `FROM python:3.11-slim` 为我们提供了一个轻量级的基础镜像。  
- `EXPOSE 5000` **在 Docker 中暴露端口**——它仅是给阅读 Dockerfile 的人提供提示，实际上并不会在主机上打开端口。  
- `CMD` 行在容器启动时运行我们的 Flask 服务器。

## 第三步：**从 Dockerfile 构建 Docker 镜像**

打开终端，`cd` 进入包含 Dockerfile 的文件夹，执行：

```bash
docker build -t myflaskapp .
```

拆解这条命令：

- `docker build` 是动词，用于 **构建 Docker 镜像**，根据 Dockerfile 中的指令生成镜像层。  
- `-t myflaskapp` 为生成的镜像打上一个易记的标签，后续可以直接引用。  
- 末尾的 `.` 表示 Docker 使用当前目录作为构建上下文（即查找 Dockerfile 以及你 `COPY` 的所有文件的地方）。

你应该会看到类似下面的输出：

```
Sending build context to Docker daemon  3.072kB
Step 1/6 : FROM python:3.11-slim
 ---> 3b6c0f...
Step 2/6 : RUN pip install flask
 ---> Using cache
 ---> 9e2b7a...
...
Successfully built 1c2d3e4f5g6h
Successfully tagged myflaskapp:latest
```

如果出现错误，请再次检查 Dockerfile 语法，并确保 `app.py` 与 Dockerfile 位于同一文件夹。

### 验证镜像是否存在

运行 `docker images` 并查找 `myflaskapp`：

```bash
docker images | grep myflaskapp
```

你会看到类似的内容：

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

恭喜——你已经成功 **构建 Docker 镜像**！

## 第四步：使用端口映射 **运行 Docker 容器**

镜像准备好后，就可以 **运行 Docker 容器**，让 Flask 应用能够从主机访问。使用 `-p` 标志进行 **docker run 端口映射**：

```bash
docker run -p 5000:5000 myflaskapp
```

解释：

- 第一个 `5000`（左侧）是 **主机端口**。  
- 第二个 `5000`（右侧）是我们之前在 Dockerfile 中 **暴露的容器端口**。  
- Docker 会把你机器上的 `localhost:5000` 流量转发到容器内部的 5000 端口。

你应该会看到 Flask 的启动日志：

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

打开浏览器访问 `http://localhost:5000`，会看到 “Hello from Docker!”——容器已经按预期提供服务。

### 将容器置于后台（可选）

如果不想让终端被占用，可以添加 `-d` 参数让容器在后台运行：

```bash
docker run -d -p 5000:5000 myflaskapp
```

以后可以使用 `docker stop <container-id>` 停止它。

## 第五步：深入了解 – **在 Docker 中暴露端口** 与 **Docker Run 端口映射** 的区别

`EXPOSE` 指令和 `-p` 标志很容易被混淆，但它们的作用不同：

| 概念 | 功能说明 | 是否在主机上打开端口？ |
|------|----------|------------------------|
| `EXPOSE`（Dockerfile 中） | 记录容器**打算**监听的端口。 | **否** – 仅元数据。 |
| `-p host:container`（docker run） | 创建 NAT 规则，将主机端口流量转发到容器端口。 | **是** – 实际的端口转发。 |

如果忘记写 `EXPOSE`，`docker run -p` 仍然可以工作，只是失去了对下游使用者的文档提示。相反，如果只写 `EXPOSE` 而不使用 `-p`，服务将无法从主机访问。

### 使用不同主机端口的 `docker run`

有时主机的 5000 端口已经被占用。没关系，只需映射到其他主机端口：

```bash
docker run -p 8080:5000 myflaskapp
```

此时应用可以通过 `http://localhost:8080` 访问，而容器内部仍然监听 5000 端口。这种灵活性正是 **docker run 端口映射** 的核心优势。

## 第六步：常见坑点与边缘案例

| 问题 | 症状 | 解决方案 |
|------|------|----------|
| 忘记 `EXPOSE` | 新手无法判断需要映射哪个端口。 | 添加 `EXPOSE 5000`（或你的应用使用的端口）。 |
| 使用错误的主机端口 | 浏览器返回 “connection refused”。 | 确认 `-p` 左侧的端口与实际访问的端口匹配。 |
| 容器启动后崩溃 | 没有日志，容器瞬间退出。 | 使用 `docker logs <container-id>` 查看错误信息；常见原因是缺少依赖或 `CMD` 写错。 |
| 主机端口已被占用 | Docker 报错 “bind: address already in use”。 | 换一个主机端口（如 `-p 8080:5000`）。 |
| 未绑定到 `0.0.0.0` | 服务只能在容器内部访问。 | 在 Flask 中设置 `host="0.0.0.0"`；其他框架也有类似配置。 |

### 构建多阶段镜像（进阶）

如果需要更小的最终镜像，可以使用多阶段 Dockerfile **构建 Docker 镜像**：

```dockerfile
# Stage 1: Build
FROM python:3.11-slim AS builder
RUN pip install --target=/app flask
COPY app.py /app/

# Stage 2: Runtime
FROM python:3.11-slim
COPY --from=builder /app /app
WORKDIR /app
EXPOSE 5000
CMD ["python", "app.py"]
```

该技巧会剔除构建阶段的层，生成更精简的镜像——非常适合生产环境。

## 第七步：清理

实验结束后，进行清理：

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

清理可以防止磁盘膨胀，保持 Docker 环境整洁。

---

## 结论

现在，你已经掌握了 **构建 Docker 镜像** 与 **运行 Docker 容器** 的完整工作流，并了解了正确的 **docker run 端口映射** 与 **在 Docker 中暴露端口** 的区别。通过这些知识，你可以自信地将任何服务容器化，并让它们从主机或更广泛的网络中访问。

接下来可以尝试将 Flask 应用换成 Go 二进制文件，使用 `-e` 添加环境变量，或通过 `docker push` 将刚构建的镜像推送到 Docker Hub。天地无限，而你已经获得了 DevOps 世界中的新超能力。

祝你玩得开心！


## 接下来该学习什么？

以下教程涵盖了与本指南紧密相关的主题，帮助你在已有技术基础上进一步提升。每篇资源都提供完整可运行的代码示例和逐步解释，助你掌握更多 API 功能并探索替代实现方式。

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}