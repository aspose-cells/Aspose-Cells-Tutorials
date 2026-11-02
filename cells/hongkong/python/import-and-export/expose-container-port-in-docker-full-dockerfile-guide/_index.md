---
category: general
date: 2026-06-21
description: 在 Docker 中公開容器埠位，同時設定工作目錄並複製應用程式原始碼。一步一步學習如何將 Python API 容器化。
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: zh-hant
og_description: 在 Docker 中公開容器埠口，設定工作目錄，並將您的原始碼複製到容器內。本教學示範如何將 Python API Docker 化。
og_title: 在 Docker 中公開容器端口 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Expose container port in Docker while setting the working directory
    and copying your app source. Learn how to dockerize a Python API step‑by‑step.
  headline: Expose Container Port in Docker – Full Dockerfile Guide
  type: TechArticle
- description: Expose container port in Docker while setting the working directory
    and copying your app source. Learn how to dockerize a Python API step‑by‑step.
  name: Expose Container Port in Docker – Full Dockerfile Guide
  steps:
  - name: 1. Changing the Host Port
    text: 'Sometimes port 5000 is already in use on your machine. No problem—just
      change the host side of the mapping:'
  - name: 2. Multi‑Stage Builds for Smaller Images
    text: If you don’t need the full Aspose.Cells runtime in production, you can create
      a multi‑stage build that compiles assets in a heavy image then copies only the
      runtime bits into a lightweight `python:3.11-slim` final stage. This reduces
      the final image size dramatically.
  - name: 3. Using Docker Compose
    text: 'For more complex setups (e.g., a database alongside the API), put the same
      instructions into a `docker-compose.yml`:'
  - name: 4. Environment Variables
    text: 'If your API needs configuration (like a secret key), pass them at runtime:'
  type: HowTo
- questions:
  - answer: Check the logs with `docker logs api_container`. A common mistake is forgetting
      `host="0.0.0.0"` in Flask.
    question: Container exits immediately?
  - answer: Verify with `docker ps` and `netstat -tulpn`. Use a different host port
      as shown above.
    question: Port already in use?
  - answer: Ensure your `requirements.txt` is present before the `RUN pip install`
      step, or add the packages directly in the Dockerfile.
    question: Missing dependencies?
  type: FAQPage
tags:
- Docker
- Python
- API
title: 在 Docker 中公開容器端口 – 完整 Dockerfile 指南
url: /zh-hant/python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Docker 中公開容器埠 – 完整 Dockerfile 指南

有沒有想過在將 Python API 容器化時，如何 **expose container port**？你並不孤單。大多數開發者都會遇到同樣的問題：應用在本機可以正常執行，但一旦跑在 Docker 內部，外部就無法存取。本文將一步步示範完整的 Dockerfile，除了 **expose container port**，還會涵蓋 **set working directory docker**、**dockerfile copy app**、**copy source into container** 等所有讓你 **dockerize python api** 的關鍵步驟，讓你輕鬆上手。

我們會先從一個簡易的 Flask 應用開始，接著從頭建構 Docker 映像，說明每一行指令的意義，最後執行容器並測試 `http://localhost:5000/health`。完成後，你將擁有可直接推送至任何 Registry 的正式環境 Docker 映像。

## 前置條件

在開始之前，請確保你已具備以下環境：

- 已安裝 Docker Engine ≥ 20.10（Windows/macOS 可使用 Docker Desktop，Linux 則安裝 Docker Engine）。
- 具備 Python 與 Flask（或任何相容 WSGI 框架）的基本概念。
- 有可編輯 Dockerfile 與 Python 程式碼的文字編輯器或 IDE（如 VS Code、PyCharm 等）。

除了官方 Aspose.Cells Python.NET 基礎映像提供的套件外，無需額外的函式庫。

## 步驟 1：建立最小化的 Python API

首先，撰寫一個簡易的 Flask 服務，稍後我們會 **dockerize python api**。將以下程式碼存成 `api_server.py`，放在一個空資料夾內。

```python
# api_server.py
from flask import Flask, jsonify

app = Flask(__name__)

@app.route("/health")
def health():
    return jsonify(status="OK", message="API is running")

if __name__ == "__main__":
    # Listen on all interfaces so Docker can forward the port
    app.run(host="0.0.0.0", port=5000)
```

為什麼要設定 `host="0.0.0.0"`？在容器內部，`localhost` 只指向容器本身。將綁定位址改為 `0.0.0.0` 代表 Flask 會接受任何網路介面的連線，這是之後 **expose container port** 必須的前置條件。

## 步驟 2：選擇適當的基礎映像

本教學使用 Aspose 官方的 **Aspose.Cells Python.NET base image**（`aspose/cells-pythonnet:6.22`）。此映像已內建 .NET 執行環境、Python 3.9 以及 Aspose.Cells 套件，若你的 API 需要 Excel 處理功能，正好合適。

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

如果不需要 Aspose，你可以改用 `python:3.11-slim`。其餘 Dockerfile 內容保持不變。

## 步驟 3：**Dockerfile Copy App** – 將原始碼複製到容器內

接下來要把程式碼帶入映像，這正是 **dockerfile copy app** 發揮作用的地方。

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

` . ` 代表建置上下文——也就是執行 `docker build` 時所在的資料夾。一次性複製全部內容會同時帶入 `requirements.txt`（若有）以及任何靜態資源。若想打造更精簡的映像，可自行列出實際需要的檔案。

## 步驟 4：**Set Working Directory Docker** – 設定工作目錄

完成複製後，我們告訴 Docker 後續指令的執行位置，這就是 **set working directory docker** 的步驟。

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

這樣做有什麼好處？可以省去之後每次都寫完整路徑（例如 `python api_server.py` 而非 `python /app/api_server.py`），同時讓容器檔案系統結構對其他開發者更易讀。

## 步驟 5：安裝 Python 相依套件（可選但建議）

若你的 API 需要外部套件，請先建立 `requirements.txt`，並在獨立層級安裝。這樣可以提升快取效能。

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

此條件式可避免在沒有 `requirements.txt` 時建置失敗，對於前面的最小範例非常實用。

## 步驟 6：**Expose Container Port** – 讓 API 能被外部存取

現在來到重點：**expose container port**。此指令告訴 Docker 容器會監聽哪個埠口，從而在執行時支援埠口映射。

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

需要注意的是，`EXPOSE` 只是一個文件化提示；實際的埠口映射發生在 `docker run -p` 時。但宣告埠口是最佳實踐，且有助於 Docker Compose 等工具自動轉發正確的埠口。

## 步驟 7：定義啟動指令

最後，我們告訴 Docker 如何啟動 API，使用 `CMD` 指令。

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

採用 JSON 陣列形式可避免 Shell 解析問題，讓指令更具可移植性。

## 完整 Dockerfile 回顧

將上述所有片段組合起來，即成為可直接 copy‑paste 的完整 Dockerfile：

```dockerfile
# Step 1: Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22

# Step 2: Copy your application source code into the container
COPY . /app

# Step 3: Set the working directory to the application folder
WORKDIR /app

# Optional: Install Python dependencies if you have a requirements file
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi

# Step 4: Expose the port your API server will listen on
EXPOSE 5000

# Step 5: Define the command to start the API server
CMD ["python", "api_server.py"]
```

> **小技巧**：若有大量相依套件，請將 `COPY` 行放在 `RUN pip install` 之前。Docker 會快取已安裝套件的層級，之後只要程式碼變更就不會重新安裝全部套件。

## 步驟 8：建置 Docker 映像

在包含 `Dockerfile` 與 `api_server.py` 的資料夾開啟終端機，執行：

```bash
docker build -t my-python-api .
```

Docker 會逐層顯示建置過程，若有快取層則會直接使用。建置成功後會看到 `Successfully tagged my-python-api:latest`。

## 步驟 9：執行容器並驗證埠口映射

現在啟動容器，將內部的 `5000` 埠映射到主機的 `5000`（或其他你想要的埠口）：

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` 代表以分離模式執行。
- `-p 5000:5000` 告訴 Docker 把主機的 5000 埠轉發到容器的 5000 埠——正是 **expose container port** 所預先宣告的埠口。

接著使用 `curl` 測試端點：

```bash
curl http://localhost:5000/health
```

預期輸出：

```json
{
  "status": "OK",
  "message": "API is running"
}
```

若看到上述 JSON，恭喜你已成功 **dockerize python api**，且埠口已可對外存取。

## 常見情境與處理方式

### 1. 更改主機埠口

有時候主機的 5000 埠已被佔用，沒關係，只要改變映射的主機埠即可：

```bash
docker run -d -p 8080:5000 my-python-api
```

此時瀏覽 `http://localhost:8080/health` 仍會正常運作，容器內部仍監聽 5000 埠。

### 2. 多階段建置以縮小映像

若正式環境不需要完整的 Aspose.Cells 執行環境，可採用多階段建置：在較重的映像中編譯資產，然後只把執行時所需的檔案複製到輕量的 `python:3.11-slim` 最終階段，顯著減少最終映像大小。

### 3. 使用 Docker Compose

若需要更複雜的環境（例如同時啟動資料庫），可將相同指令寫入 `docker-compose.yml`：

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Compose 會自動遵循 `EXPOSE` 指令，無需再次手動設定埠口映射。

### 4. 環境變數

若 API 需要設定（例如密鑰），可在執行時傳入環境變數：

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

在 Python 程式中可透過 `os.getenv("SECRET_KEY")` 取得。

## 除錯小技巧

- **容器立即退出？** 使用 `docker logs api_container` 查看日誌。常見錯誤是忘記在 Flask 中設定 `host="0.0.0.0"`。
- **埠口已被佔用？** 可用 `docker ps` 以及 `netstat -tulpn` 檢查，然後改用不同的主機埠。
- **缺少相依套件？** 確認 `requirements.txt` 已放在 `RUN pip install` 前，或直接在 Dockerfile 中加入套件安裝指令。

## 重點回顧

我們從簡易的 Flask 應用開始，選擇穩定的基礎映像，使用 **dockerfile copy app** 把程式碼帶入容器，透過 **set working directory docker** 確保執行路徑一致，宣告 `EXPOSE 5000` 以 **expose container port**，最後以 `CMD` 啟動服務。建置與執行後，即得到一個可直接部署的 **dockerize python api**。

## 下一步？

- 在 Dockerfile 中加入 **健康檢查**（`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`）。
- 實作將日誌輸出至 stdout，讓 Docker 能自動收集。
- 為 API 加上 HTTPS 保護。

## 接下來該學什麼？

以下教學與本篇內容密切相關，能進一步擴充你的 API 技能與實作方式，每篇皆提供完整範例與逐步說明。

- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}