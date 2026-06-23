---
category: general
date: 2026-06-21
description: Dockerで作業ディレクトリを設定し、アプリのソースをコピーしながらコンテナのポートを公開します。Python APIをステップバイステップでDocker化する方法を学びましょう。
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: ja
og_description: Dockerでコンテナのポートを公開し、作業ディレクトリを設定し、ソースをコンテナにコピーします。このチュートリアルでは、Python
  APIをDocker化する方法を示します。
og_title: Dockerでコンテナポートを公開する – 完全ガイド
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
title: Dockerでコンテナのポートを公開する – 完全Dockerfileガイド
url: /ja/python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dockerでコンテナポートを公開 – 完全Dockerfileガイド

Python APIをコンテナ化する際に **expose container port** する方法を疑問に思ったことはありませんか？ あなたは一人ではありません。多くの開発者が同じ壁にぶつかります：ローカルではアプリが動作しても、Docker内部に入れると外部からアクセスできなくなるのです。このチュートリアルでは、**expose container port** だけでなく **set working directory docker**、**dockerfile copy app**、**copy source into container** も行う完全なDockerfileを順に解説し、**dockerize python api** に必要なすべての要素を手軽に実装できるようにします。

まずは小さなFlaskアプリから始め、ゼロからDockerイメージを構築し、各命令を解説し、最後にコンテナを実行して `http://localhost:5000/health` にアクセスできるようにします。最後までで、任意のレジストリにプッシュできる本番環境向けDockerイメージが手に入ります。

## 前提条件

- Docker Engine ≥ 20.10 がインストールされていること（Windows/macOS では Docker Desktop、Linux では Docker Engine が動作すれば OK）。
- Python と Flask（または任意の WSGI 互換フレームワーク）に基本的に慣れていること。
- Dockerfile と Python コードを編集できるテキストエディタまたは IDE（VS Code、PyCharm など）。

公式の Aspose.Cells Python.NET ベースイメージが提供するもの以外に追加のライブラリは必要ありません。

## ステップ 1: 最小限の Python API を作成

まず、後で **dockerize python api** するための小さな Flask サービスを書きます。これを空のフォルダーに `api_server.py` として保存してください。

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

`host="0.0.0.0"` はなぜでしょうか？ コンテナ内部では `localhost` はコンテナ自身を指します。`0.0.0.0` にバインドすることで Flask は任意のネットワークインターフェースからの接続を受け入れ、後の **expose container port** 手順に必須となります。

## ステップ 2: 適切なベースイメージを選択

この例では Aspose の公式 **Aspose.Cells Python.NET base image**（`aspose/cells-pythonnet:6.22`）を使用します。すでに .NET ランタイム、Python 3.9、Aspose.Cells ライブラリが同梱されており、API が Excel 操作を必要とする場合に最適です。

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

Aspose が不要な場合は `python:3.11-slim` に置き換えても構いません。Dockerfile の残りの部分は同じです。

## ステップ 3: **Dockerfile Copy App** – ソースをコンテナにコピー

次に、コードをイメージに持ち込む必要があります。ここで **dockerfile copy app** 命令が活躍します。

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

`.` はビルドコンテキスト（`docker build` を実行するフォルダー）を表します。すべてをコピーすることで `requirements.txt`（存在すれば）や静的アセットも含められます。よりスリムなイメージが欲しい場合は、実際に必要なファイルだけを列挙してください。

## ステップ 4: **Set Working Directory Docker** – 作業ディレクトリを定義

コピー後、Docker に以降のコマンドを実行する場所を指示します。これが **set working directory docker** のステップです。

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

なぜ必要かというと、後でフルパスを入力する手間が省けます（例: `python /app/api_server.py` の代わりに `python api_server.py`）。また、イメージを後で読む人にとってコンテナのファイルシステム構造が分かりやすくなります。

## ステップ 5: Python 依存関係をインストール（任意だが推奨）

API が外部パッケージに依存している場合は `requirements.txt` を作成し、別レイヤーでインストールします。これによりキャッシュが有効になります。

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

条件分岐により `requirements.txt` がなくてもビルドが失敗しないようにしています—上記の最小例では便利です。

## ステップ 6: **Expose Container Port** – API を外部からアクセス可能にする

いよいよ本題の **expose container port** です。これにより Docker にコンテナがリッスンするポートを指示し、実行時のポートマッピングを可能にします。

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

`EXPOSE` はあくまでドキュメント上のヒントであり、実際のマッピングは `docker run -p` 実行時に行われます。それでもポートを宣言しておくことはベストプラクティスであり、Docker Compose などのツールが自動的に正しいポートを転送できるようになります。

## ステップ 7: 起動コマンドを定義

最後に、Docker に API の起動方法を指示します。これが `CMD` 命令です。

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

JSON 配列形式を使用することでシェル解釈の問題を回避し、コマンドの移植性が向上します。

## 完全な Dockerfile のまとめ

すべての要素を組み合わせた、コピー＆ペースト可能な完全な Dockerfile を示します。

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

> **プロのコツ:** 依存関係が多い場合は `RUN pip install` 行の前に `COPY` 行を置きましょう。Docker はインストール済みパッケージのレイヤーをキャッシュするため、コード変更後の再ビルドで全てを再インストールする必要がなくなります。

## ステップ 8: Docker イメージをビルド

`Dockerfile` と `api_server.py` があるフォルダーでターミナルを開き、以下を実行します。

```bash
docker build -t my-python-api .
```

Docker は各ステップをストリーム表示し、可能な限りキャッシュされたレイヤーを示します。問題なく完了すれば `Successfully tagged my-python-api:latest` と表示されます。

## ステップ 9: コンテナを実行しポートマッピングを確認

次にコンテナを起動し、内部ポート `5000` をホストの `5000`（または任意のホストポート）にマッピングします。

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` はデタッチドモードで実行します。
- `-p 5000:5000` はホストのポート 5000 をコンテナのポート 5000 に転送するよう Docker に指示します—まさに **expose container port** 指示が用意した通りです。

`curl` でエンドポイントをテストできます：

```bash
curl http://localhost:5000/health
```

期待される出力:

```json
{
  "status": "OK",
  "message": "API is running"
}
```

この JSON が表示されたらおめでとうございます—**dockerized python api** に成功し、ポートがアクセス可能になりました。

## よくあるケースと対処法

### 1. ホストポートの変更

マシンでポート 5000 が既に使用中の場合があります。問題ありません—マッピングのホスト側だけ変更すれば OK です。

```bash
docker run -d -p 8080:5000 my-python-api
```

これでコンテナは依然として `5000` をリッスンしつつ、`http://localhost:8080/health` が動作します。

### 2. 小さなイメージのためのマルチステージビルド

本番環境でフルの Aspose.Cells ランタイムが不要な場合、重いイメージでアセットをビルドし、最終ステージの軽量 `python:3.11-slim` にランタイム部分だけをコピーするマルチステージビルドを作成できます。これにより最終イメージサイズが大幅に削減されます。

### 3. Docker Compose の使用

API とデータベースなど、より複雑な構成の場合は同じ指示を `docker-compose.yml` に記述します：

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Compose は自動的に `EXPOSE` 指示を尊重するため、ポートマッピングを再度記述する必要はありません。

### 4. 環境変数

API が設定（例: シークレットキー）を必要とする場合は、実行時に渡します：

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

Python 側では `os.getenv("SECRET_KEY")` で取得できます。

## デバッグのヒント

- **コンテナがすぐに終了する？** `docker logs api_container` でログを確認してください。よくあるミスは Flask で `host="0.0.0.0"` を忘れることです。
- **ポートがすでに使用中？** `docker ps` と `netstat -tulpn` で確認し、上記のように別のホストポートを使用してください。
- **依存関係が欠如している？** `RUN pip install` 手順の前に `requirements.txt` が存在することを確認するか、Dockerfile に直接パッケージを追加してください。

## まとめ

シンプルな Flask アプリから始め、堅牢なベースイメージを選択し、**dockerfile copy app** でコードを内部に持ち込み、**set working directory docker** でクリーンに実行できるようにし、`EXPOSE 5000` を宣言して **expose container port** を行い、`CMD` でサービスを起動しました。イメージをビルド・実行することで、誰でもプルして実行できる完全に機能する **dockerize python api** が手に入りました。

## 次にやること

- Dockerfile に **ヘルスチェック** を追加（`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`）。
- ログを stdout に出力するよう実装し、Docker が取得できるようにする。
- HTTPS で API を保護する。

## 次に学ぶべきことは？

以下のチュートリアルは本ガイドで示した手法を応用した、密接に関連するトピックを扱っています。各リソースは完全な動作コード例とステップバイステップの解説を含み、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}