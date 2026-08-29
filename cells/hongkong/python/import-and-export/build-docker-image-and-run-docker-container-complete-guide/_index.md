---
category: general
date: 2026-06-21
description: 學習如何建立 Docker 映像檔並以正確的埠映射執行 Docker 容器。包括 Docker run 的埠映射以及在 Docker 中暴露埠。
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: zh-hant
og_description: 建立 Docker 映像檔並以正確的埠口映射執行 Docker 容器。只需數分鐘，即可掌握 Docker run 的埠口映射並在 Docker
  中公開埠口。
og_title: 構建 Docker 映像並執行 Docker 容器 – 完整指南
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
title: 建立 Docker 映像檔並執行 Docker 容器 – 完整指南
url: /zh-hant/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立 Docker 映像檔並執行 Docker 容器 – 完整指南

有沒有想過要 **build docker image** 一個簡單的 Web 應用，然後順利地讓它跑起來？你並不孤單——許多開發者在第一次接觸容器化時都會卡在同一個地方。在本教學中，我們會一步步說明整個流程，從撰寫 Dockerfile、開放正確的埠口，到最後使用 `docker run` 把埠口映射到主機。完成後，你將清楚知道如何 **run docker container** 並正確設定埠口映射，並了解在 Docker 中開放埠口的重要性。

我們會涵蓋所有你需要的內容：完整的 `docker build` 指令、如何 **docker build from Dockerfile**、`docker run port mapping` 的細節，甚至還會提供快速檢查，確保容器真的在你預期的埠口上監聽。沒有冗長的說明，只有可直接 copy‑paste 到終端機的實作步驟。

## 你將學會什麼

- 為 Node.js（或任何）應用撰寫最小化的 Dockerfile。  
- 使用官方 CLI 語法 **build docker image**。  
- 了解 Dockerfile 中的 `EXPOSE` 與 `docker run` 中 `-p` 旗標的差異。  
- 使用 `docker run port mapping` **run docker container**，讓服務可在 `http://localhost:5000` 取得。  
- 排除常見的問題，例如遺忘開放埠口或主機與容器埠口不匹配。

### 前置條件

- 已安裝 Docker Engine（Desktop 或 Engine 20.10 以上）。  
- 基本的指令列操作經驗。  
- 一個小型的 Web 應用（我們會使用一行的 Python Flask 伺服器，你也可以自行換成其他語言）。

如果你已具備上述條件，讓我們開始吧。

---

## Step 1: 建立簡易應用程式

首先，我們需要一個可以容器化的程式。建立一個名為 `myapp` 的資料夾，並在裡面放入單一檔案 `app.py`：

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

> **小技巧：** `host="0.0.0.0"` 這一行會讓 Flask 監聽所有介面，這是 Docker 轉發流量所必須的設定。

現在，你已經有一個在容器內部監聽 5000 埠口的微型 Web 服務。

## Step 2: 撰寫 Dockerfile（Docker Build from Dockerfile）

接著，我們需要一個 **Dockerfile**，告訴 Docker 如何組建映像檔。把這個檔案放在 `app.py` 同一層目錄：

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

需要注意的地方：

- `FROM python:3.11-slim` 提供我們一個輕量的基礎映像檔。  
- `EXPOSE 5000` **expose port in docker** – 這只是給閱讀 Dockerfile 的人一個提示，實際上不會在主機上開啟埠口。  
- `CMD` 行會在容器啟動時執行 Flask 伺服器。

## Step 3: **Build Docker Image** 從 Dockerfile

打開終端機，`cd` 到放置 Dockerfile 的資料夾，然後執行：

```bash
docker build -t myflaskapp .
```

讓我們拆解這個指令：

- `docker build` 是 **build docker image** 的動作，會根據 Dockerfile 指令建立映像層。  
- `-t myflaskapp` 為產生的映像檔貼上易於辨識的標籤，以便之後引用。  
- 最後的 `.` 表示 Docker 使用目前目錄作為建置上下文（即搜尋 Dockerfile 與 `COPY` 的檔案所在位置）。

執行後，你應該會看到類似以下的輸出：

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

如果出現錯誤，請再次檢查 Dockerfile 語法，並確保 `app.py` 位於同一資料夾內。

### 驗證映像檔是否存在

執行 `docker images`，找尋 `myflaskapp`：

```bash
docker images | grep myflaskapp
```

你會看到類似的結果：

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

恭喜，你已成功 **built docker image**！

## Step 4: **Run Docker Container** 並設定埠口映射

映像檔已備妥，現在可以 **run docker container**，讓 Flask 應用從主機可存取。使用 `-p` 旗標執行 **docker run port mapping**：

```bash
docker run -p 5000:5000 myflaskapp
```

說明：

- 左側的 `5000` 為 **host port**（主機埠口）。  
- 右側的 `5000` 為我們先前在 Dockerfile 中 **expose port in docker** 的 **container port**（容器埠口）。  
- Docker 會把你機器上的 `localhost:5000` 流量轉發到容器內的 5000 埠口。

執行後，你應該會看到 Flask 的啟動日誌：

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

打開瀏覽器，前往 `http://localhost:5000`，你會看到 “Hello from Docker!”——容器已如預期提供服務。

### 背景執行容器（可選）

如果不想讓終端機被卡住，可加入 `-d` 讓容器在背景執行：

```bash
docker run -d -p 5000:5000 myflaskapp
```

之後可使用 `docker stop <container-id>` 停止它。

## Step 5: 深入探討 – **Expose Port in Docker** 與 **Docker Run Port Mapping** 的差別

`EXPOSE` 指令與 `-p` 旗標常被混淆，但兩者的目的不同：

| Concept | What it does | Does it open the port on the host? |
|---------|--------------|------------------------------------|
| `EXPOSE` (in Dockerfile) | 文件化容器 **intends** 監聽的埠口。 | **No** – 只是 metadata。 |
| `-p host:container` (docker run) | 建立 NAT 規則，將主機埠口流量轉發至容器埠口。 | **Yes** – 真正的埠口轉發。 |

如果忘記寫 `EXPOSE`，`docker run -p` 仍然可運作，只是失去對下游使用者的說明文件。相反地，僅寫 `EXPOSE` 而不使用 `-p`，服務則無法從主機存取。

### 使用不同的 Host Port 執行 `docker run`

有時主機的 5000 埠口已被佔用，沒關係，只要改用其他埠口即可：

```bash
docker run -p 8080:5000 myflaskapp
```

此時應用仍在容器內的 5000 埠口運行，但可透過 `http://localhost:8080` 存取。這種彈性正是 **docker run port mapping** 的核心優勢。

## Step 6: 常見問題與邊緣案例

| Issue | Symptom | Fix |
|-------|---------|-----|
| Forgetting `EXPOSE` | 新手無法判斷要映射哪個埠口。 | 加入 `EXPOSE 5000`（或你的應用使用的埠口）。 |
| Using the wrong host port | 瀏覽器顯示 “connection refused”。 | 確認 `-p` 左側的埠口與你要連線的埠口相同。 |
| Container crashes on start | 沒有日誌，容器立即退出。 | 執行 `docker logs <container-id>` 查看錯誤訊息；常因缺少相依或 `CMD` 錯誤。 |
| Port already in use on host | Docker 顯示 “bind: address already in use”。 | 改用其他主機埠口（例如 `-p 8080:5000`）。 |
| Not binding to `0.0.0.0` | 服務只能在容器內部存取。 | 在 Flask 中設定 `host="0.0.0.0"`；其他框架亦有類似設定。 |

### 建構多階段映像檔（進階）

若需要更小的最終映像檔，可使用多階段 Dockerfile **build docker image**：

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

此技巧會移除建置階段的層級，產生更精簡的映像檔——非常適合上線環境。

## Step 7: 清理

實驗結束後，記得清理資源：

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

清理可以避免磁碟空間膨脹，保持 Docker 環境整潔。

---

## 結論

現在你已掌握 **build docker image** 與 **run docker container**，並能正確使用 **docker run port mapping**。了解 **expose port in docker** 與 `-p` 旗標的運作方式後，你可以自信地將任何服務容器化，並讓它從主機或更廣的網路存取。

接下來可以嘗試把 Flask 換成 Go 二進位檔、使用 `-e` 加入環境變數，或是將剛建好的映像檔推送至 Docker Hub（`docker push`）。只要持續練習，你的 DevOps 超能力將不斷升級。

祝你玩得開心！

## 接下來該學什麼？

以下教學與本指南緊密相關，能幫助你進一步掌握 API 功能與其他實作方式，並提供完整可執行的程式碼範例與逐步說明。

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}