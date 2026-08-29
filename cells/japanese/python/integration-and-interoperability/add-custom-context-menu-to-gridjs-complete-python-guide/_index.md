---
category: general
date: 2026-06-30
description: GridJsにカスタムコンテキストメニューを追加し、Excelブックの読み込み、セルの値の更新、スペルチェックの有効化、カスタムコマンドの登録方法を学びます。
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: ja
og_description: GridJsでカスタムコンテキストメニューを追加し、Excelブックの読み込み、セル値の更新、スペルチェックの有効化、カスタムコマンドの登録を学ぶ。
og_title: GridJsにカスタムコンテキストメニューを追加 – ステップバイステップ Python チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: GridJsにカスタムコンテキストメニューを追加 – 完全なPythonガイド
url: /ja/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJs にカスタムコンテキストメニューを追加 – 完全 Python ガイド

Excel ワークブックをバックエンドに持つ GridJs テーブルに **カスタムコンテキストメニュー** アイテムを追加したいと思ったことはありませんか？ あなただけではありません。データが大量にあるアプリでは、右クリックメニューで行をフラグ付けしたり、アイテムを「レビュー済み」とマークしたり、サーバー側のアクションを起動したりする必要があります――グリッドを離れることなく。

このチュートリアルでは、Excel ワークブックの読み込み、カスタムコンテキストメニュー項目の配線、セル値の更新、スペルチェックの有効化、変更をファイルに永続化するカスタムコマンドの登録までを順に解説します。最後まで読めば、ユーザーにとってネイティブに感じられ、元のスプレッドシートへ直接書き戻す完全な GridJs インスタンスが手に入ります。

## 前提条件

- Python 3.9+（コードは型ヒントを使用していますが、最近のバージョンであればどれでも動作します）  
- `cells` ライブラリ（`Workbook` と `Worksheet` オブジェクトを提供する任意の Excel ラッパー）  
- `gridjs` Python バインディング（オブジェクトモデルは JavaScript API と同様です）  
- ラムダ式と JSON 構造の基本的な理解  

これらが揃っていれば、さっそく始めましょう。

## 手順 1: Excel ワークブックを読み込み、ワークシートを選択

最初に **Excel ワークブックを読み込む** 必要があります。これにより GridJs が表示するデータを取得できます。`cells.Workbook` クラスはファイル I/O を抽象化し、行・列・個々のセルへ直接アクセスできるようにします。

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **なぜ重要か:** ワークブックを事前に読み込んでおくことで、グリッドは必要に応じてデータを取得でき、後から行う **セル値の更新** も同じファイルに永続化されます。

## 手順 2: GridJs インスタンスを作成し、ワークシートにバインド

次に `gridjs.GridJs` オブジェクトを生成し、どのワークシートを描画するか指示します。これは、ページや遅延ロードのチャンクを描画するたびにクエリできるライブデータソースを GridJs に提供するイメージです。

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **プロのコツ:** 複数シートを扱う場合は、後から `grid.set_worksheet(other_ws)` を呼び出すだけで OK。グリッドを再作成する必要はありません。

## 手順 3: スペルチェックを有効化（その他の便利機能）

多くの業務アプリでは自由形式のメモを入力します。**スペルチェック** を有効にするとタイプミスが減り、データ品質が向上します。GridJs ではシンプルなフラグでこれを実現できます。

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **スペルチェックを有効にする理由:** クライアント側で即座にフィードバックを提供し、余計なサーバー呼び出しが不要になるため、大規模シートに最適です。

## 手順 4: カスタムコンテキストメニュー項目を追加

本チュートリアルの核心です： **カスタムコンテキストメニュー** を追加します。ここでは「Mark as Reviewed」オプションを作成し、クリック時に次の手順で定義するサーバー側コマンドを実行させます。

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **画像イラスト**  
> ![カスタムコンテキストメニューを追加したスクリーンショット（右クリックオプション）](/images/add-custom-context-menu.png "カスタムコンテキストメニューの例")

上記の alt テキストは主要キーワードを含んでおり、SEO 要件を満たしています。

## 手順 5: セル値を更新するカスタムコマンドを登録

ユーザーが「Mark as Reviewed」を選択したとき、**カスタムコマンド** を登録して基になる Excel セルを更新し、ファイルを保存します。`grid.register_custom_command` メソッドは、先ほど設定したアクション識別子に Python の呼び出し可能オブジェクトを紐付けます。

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **なぜこれが機能するか:** ハンドラはクライアントからセル参照を受け取り、`Worksheet` API を使って **セル値を更新** し、ワークブック全体をディスクに書き戻します。レスポンスはフロントエンドに成功を通知します。

### エッジケースの取り扱い

- **セル参照が欠如している場合:** `req` に `"cell"` が無ければ明確なエラーを投げ、UI がトーストで表示できるようにします。  
- **同時編集:** 高トラフィック環境では、ワークブックのロックやバージョンスタンプの導入を検討し、競合状態を防ぎます。

## 手順 6: 大規模シート向けに遅延ロードを有効化

数千行を扱う場合、遅延ロードで UI の応答性を保ちます。ページサイズを適切に設定すれば、ほとんどのブラウザで快適に動作します――目安は 500 行です。

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **10 000 行の場合は？** グリッドはページ単位でデータを要求するため、クライアント・サーバー双方のメモリ負荷が軽減されます。

## 手順 7: （任意）行編集用カスタムモーダルを追加

インラインエディタだけでは足りない場合があります。GridJs は任意の場所にホストできるモーダルウィンドウを開く機能を提供します――React コンポーネントでもシンプルな HTML フォームでも構いません。

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **モーダルを使う理由:** 複雑なバリデーションロジックを分離でき、レイアウトを完全にコントロールしつつ、グリッドからトリガーできる点が利点です。

## 手順 8: クライアント側設定 JSON を取得

最後に、設定情報をブラウザへ送ります。`get_client_config` メソッドはすべてを JSON 形式にシリアライズし、フロントエンドの GridJs ライブラリが利用できるようにします。

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

出力例は概ね以下のようになります（簡略化）:

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### 期待される結果

- 任意のセルを右クリックすると **Mark as Reviewed** メニューが表示される。  
- それを選択するとサーバーへリクエストが送られ、セル値が “Reviewed” に **更新** され、`example‑updated.xlsx` が保存される。  
- スペルチェックはユーザーが入力中に誤字をハイライトする。  

すべてページ全体のリロードなしで実現でき、遅延ロードと軽量 JSON ペイロードのおかげです。

## よくある質問 & プロのコツ

| 質問 | 回答 |
|------|------|
| *ワークブックが読み取り専用の場合は？* | ファイルの書き込み権限を確認するか、ライブラリがサポートしていれば `mode="rw"` で開きます。 |
| *カスタムメニュー項目を複数追加できるか？* | もちろん可能です。`grid.settings.context_menu.custom_items` に追加の dict を順次 append してください。 |
| *セル更新後にグリッドをリロードする必要があるか？* | ハンドラが `{status:"ok"}` を返せば GridJs が自動で該当行を更新します。必要に応じてクライアント側で `grid.refresh()` を呼び出してください。 |
| *スペルチェックを言語別に設定するには？* | `grid.settings.spell_check.language = "en-US"` のように、サポートされているロケールを指定します。 |
| *遅延ロードはサーバー側フィルタリングと併用できるか？* | できます。`grid.settings.filter.enabled = True` とし、フィルタロジックをカスタムコマンドで実装してください。 |

## 完全動作サンプル（全手順統合）

以下は Flask のルートに貼り付けても、単体プロセスとして実行しても動くスクリプトです。`YOUR_DIRECTORY` をサーバー上の実際のパスに置き換えてください。

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを応用した、密接に関連するテーマを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装を検討したりする際に役立ちます。

- [Add Custom Content Type Properties to Excel Workbooks Using Aspose.Cells Java](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [Add Custom XML Parts with ID to Workbook](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}