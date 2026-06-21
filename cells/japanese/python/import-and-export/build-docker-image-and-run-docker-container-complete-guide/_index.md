---
category: general
date: 2026-06-21
description: Dockerイメージの作成方法と、適切なポートマッピングでDockerコンテナを実行する方法を学びます。Dockerのrunコマンドでのポートマッピングと、Dockerでのポート公開が含まれます。
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: ja
og_description: Dockerイメージをビルドし、正しいポートマッピングでDockerコンテナを実行します。数分でDockerのポートマッピングとポート公開をマスターできます。
og_title: Dockerイメージの構築とDockerコンテナの実行 – 完全ガイド
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
title: DockerイメージのビルドとDockerコンテナの実行 – 完全ガイド
url: /ja/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Docker イメージのビルドと Docker コンテナの実行 – 完全ガイド

シンプルな Web アプリの **docker image をビルド** し、問題なく起動させる方法を知りたくありませんか？同じ壁にぶつかる開発者は多いです。このチュートリアルでは、Dockerfile の作成から正しいポートの公開、`docker run` でポートをホストにマッピングするまでの全工程を順を追って解説します。最後まで読めば、**docker container を正しいポートマッピングで実行** する方法が完全に理解でき、Docker でポートを公開する重要性が分かります。

必要な情報はすべて網羅しています：正確な `docker build` コマンド、**docker build from Dockerfile** の手順、`docker run port mapping` の微妙な違い、そしてコンテナが期待通りにリッスンしているかを確認する簡単なチェックまで。余計な説明は省き、ターミナルにコピペできるハンズオンのステップバイステップガイドです。

## What You'll Achieve

- Node.js（または任意）のアプリ用に最小限の Dockerfile を作成する。  
- 公式 CLI 構文を使って **docker image をビルド** する。  
- Dockerfile の `EXPOSE` と `docker run` の `-p` フラグの違いを理解する。  
- `docker run port mapping` で **docker container を実行** し、`http://localhost:5000` でサービスにアクセスできるようにする。  
- ポート忘れやホスト‑コンテナ間ポート不一致など、よくある落とし穴を診断できるようになる。

### Prerequisites

- Docker Engine がインストール済み（Desktop または Engine 20.10 以上）。  
- コマンドラインの基本操作に慣れていること。  
- 小さな Web アプリ（ここでは 1 行の Python Flask サーバを使用しますが、好きなものに置き換えて構いません）。  

上記が揃っていれば、さっそく始めましょう。

---

## Step 1: Create a Simple Application

まずはコンテナ化する対象を用意します。`myapp` というフォルダを作成し、その中に `app.py` というファイルを置きます。

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

> **Pro tip:** `host="0.0.0.0"` 行は Flask にすべてのインターフェースでリッスンさせる設定で、Docker がホストからのトラフィックを転送できるようにするために必須です。

これでコンテナ内部のポート 5000 でリッスンする小さな Web サービスが完成しました。

## Step 2: Write the Dockerfile (Docker Build from Dockerfile)

次に、Docker がイメージを組み立てる手順を記述した **Dockerfile** を作成します。`app.py` と同じディレクトリに配置してください。

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

ポイントは以下の通りです：

- `FROM python:3.11-slim` は軽量なベースイメージを提供します。  
- `EXPOSE 5000` は **expose port in docker** の指示です。Dockerfile を読む人へのヒントになりますが、ホスト側のポートを実際に開くわけではありません。  
- `CMD` 行はコンテナ起動時に Flask サーバを実行します。

## Step 3: **Build Docker Image** from the Dockerfile

ターミナルを開き、Dockerfile があるディレクトリへ `cd` で移動し、以下を実行します。

```bash
docker build -t myflaskapp .
```

コマンドの意味は次の通りです：

- `docker build` は Dockerfile の指示に基づき **docker image をビルド** する動詞です。  
- `-t myflaskapp` は作成したイメージに覚えやすい名前（タグ）を付けます。後で参照しやすくなります。  
- 末尾の `.` は現在のディレクトリをビルドコンテキストとして使用することを Docker に指示します（Dockerfile と `COPY` されるファイルを探す場所です）。

実行すると次のような出力が表示されます：

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

エラーが出た場合は Dockerfile の構文を再確認し、`app.py` が同じフォルダにあるか確認してください。

### Verify the Image Exists

`docker images` を実行し、`myflaskapp` が一覧にあるか確認します：

```bash
docker images | grep myflaskapp
```

出力例は次の通りです：

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

おめでとうございます！**docker image をビルド** に成功しました。

## Step 4: **Run Docker Container** with Port Mapping

イメージができたので、**docker container を実行** し、Flask アプリをホストからアクセスできるようにします。`-p` フラグで **docker run port mapping** を行います：

```bash
docker run -p 5000:5000 myflaskapp
```

説明：

- 左側の `5000` が **ホストポート** です。  
- 右側の `5000` が先ほど `EXPOSE` した **コンテナポート** です。  
- Docker はマシン上の `localhost:5000` からコンテナ内部のポート 5000 へトラフィックを転送します。

起動ログに Flask のメッセージが表示されます：

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

ブラウザで `http://localhost:5000` にアクセスすると “Hello from Docker!” が表示されます。コンテナが期待通りにトラフィックを提供できていることが確認できます。

### Detaching the Container (Optional)

ターミナルを占有したくない場合は、`-d` オプションでバックグラウンド実行できます：

```bash
docker run -d -p 5000:5000 myflaskapp
```

後で停止したいときは `docker stop <container-id>` を実行します。

## Step 5: Deep Dive – **Expose Port in Docker** vs. **Docker Run Port Mapping**

`EXPOSE` 命令と `-p` フラグは混同しやすいですが、目的は異なります：

| Concept | What it does | Does it open the port on the host? |
|---------|--------------|------------------------------------|
| `EXPOSE` (in Dockerfile) | コンテナが **リッスンする予定** のポートを文書化します。 | **No** – メタデータとしてだけ扱われます。 |
| `-p host:container` (docker run) | ホストポートからコンテナポートへの NAT ルールを作成し、トラフィックを転送します。 | **Yes** – 実際にポートが開かれます。 |

`EXPOSE` を省略しても `docker run -p` は機能しますが、下流の利用者にとって有益なドキュメントが失われます。逆に `EXPOSE` のみで `-p` を使わないと、ホストからはサービスにアクセスできません。

### Using `docker run` with Different Host Ports

ホスト側でポート 5000 がすでに使用中の場合でも問題ありません。別のホストポートにマッピングすれば OK です：

```bash
docker run -p 8080:5000 myflaskapp
```

この場合、コンテナ内部は依然として 5000 をリッスンしていますが、ホストからは `http://localhost:8080` でアクセスできます。これが **docker run port mapping** の柔軟性です。

## Step 6: Common Pitfalls & Edge Cases

| Issue | Symptom | Fix |
|-------|---------|-----|
| `EXPOSE` を忘れる | 新しい開発者がどのポートをマッピングすべきか分からない | `EXPOSE 5000`（または使用するポート）を追加する |
| ホストポートを間違える | ブラウザで “connection refused” が表示される | `-p` の左側（ホストポート）が正しいか確認する |
| コンテナ起動時にクラッシュ | ログが出ず、コンテナがすぐに終了する | `docker logs <container-id>` でエラーメッセージを確認。依存関係不足や `CMD` の誤りが原因になることが多い |
| ホストでポートが使用中 | Docker が “bind: address already in use” と出す | 別のホストポートに変更（例：`-p 8080:5000`） |
| `0.0.0.0` にバインドしていない | コンテナ内部からしかサービスにアクセスできない | Flask では `host="0.0.0.0"` を設定する。他のフレームワークでも同様の設定が必要 |

### Building Multi‑Stage Images (Advanced)

より小さな最終イメージが必要な場合は、マルチステージ Dockerfile で **docker image をビルド** できます：

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

この手法はビルド時のレイヤーを除去し、軽量なイメージを生成します。プロダクション環境に最適です。

## Step 7: Clean Up

実験が終わったら環境を整理しましょう：

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

不要なイメージやコンテナを削除することで、ディスク容量の肥大化を防ぎ、Docker 環境をすっきり保てます。

---

## Conclusion

これで **docker image をビルド** し、**docker container を正しいポートマッピングで実行** する一連のフローが身につきました。**expose port in docker** と `-p` フラグの違いを理解すれば、任意のサービスをコンテナ化し、ホストやネットワーク上から確実にアクセスできるようになります。

次は何をしますか？Flask アプリを Go バイナリに置き換えてみる、`-e` で環境変数を渡す、あるいは `docker push` でイメージを Docker Hub にプッシュするなど、可能性は無限です。DevOps の新たなスーパーパワーを手に入れた今、思いのままにコンテナを操りましょう。

Happy container


## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}