---
category: general
date: 2026-06-30
description: PythonのExcelグリッドにカスタムコンテキストメニューを追加し、更新されたファイルを保存しながらセルに値を書き込む。右クリックメニューの作成方法とPythonスタイルでセルの値を更新する方法を学びましょう。
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: ja
og_description: Pythonでカスタムコンテキストメニューを追加し、Excelセルに値を書き込んで更新されたExcelファイルを保存します。このガイドでは、GridJsを使って右クリックメニューを作成する方法を解説します。
og_title: Pythonでカスタムコンテキストメニューを追加する – ステップバイステップチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Pythonでカスタムコンテキストメニューを追加する – 完全ガイド
url: /ja/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pythonでカスタムコンテキストメニューを追加 – 完全ガイド

Python から提供しているスプレッドシートグリッドに **カスタムコンテキストメニュー** を追加したいと思ったことはありませんか？たとえば、ユーザーがセルを右クリックしたときに「レビュー済みとしてマーク」ボタンが表示され、Excel のセルに値を書き込み、更新されたブックを保存する、といった操作を Web UI から離れずに実現したい場合です。

このチュートリアルでは、まさにそれを構築します。**GridJs** によるカスタム右クリックメニュー、**excel セルに値を書き込む** サーバーサイドハンドラ、そして **更新された excel ファイルを保存** する最終ステップです。最後まで実装すれば、Flask、FastAPI、Django のいずれのプロジェクトにも組み込める再利用可能なパターンが手に入ります。

> **なぜ重要か？**  
> カスタムコンテキストメニューを追加すると、データレビューのワークフローがスムーズになり、手動でのコピー＆ペーストが減ります。さらに、**cell value を python 方式で更新** する方法が身につくので、Excel 自動化の基本スキルが向上します。

## 前提条件

- Python 3.9+（コードは 3.10 でも動作します）  
- Excel ファイル操作のための `openpyxl`  
- `gridjs` Python ラッパー（またはフロントエンド用の JS ライブラリ）  
- 基本的な Web フレームワーク（ここでは Flask の例を使用）  
- プロジェクトフォルダに `sample.xlsx` という名前のブックファイルがあること  

不足しているものがあれば、次を実行してください。

```bash
pip install openpyxl flask gridjs
```

それでは始めましょう。

---

## Step 1 – カスタムコンテキストメニューを追加: GridJs の初期化とワークシートのバインド

最初に行うべきことは、`GridJs` インスタンスを起動し、操作対象のワークシートを指定することです。ここで **add custom context menu** というフレーズがコードに初めて登場し、以降のすべての処理の土台となります。

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**何が起きているのか？**  
`grid.set_worksheet(ws)` は GridJs に `ws` のデータをデータソースとして使用させます。以後、追加するコンテキストメニューの変更は自動的に同じワークシートを対象にするため、UI とファイルが同期した状態を保てます。

> **プロのコツ:** ワークブックは読み書きモードで一度だけ開くようにしましょう。リクエストハンドラ内で何度も開くと、Windows 環境でファイルロックの問題が発生しやすくなります。

---

## Step 2 – Excel セルに値を書き込む: メニュー項目のアクション定義

グリッドの準備ができたら、ユーザーがカスタムコマンドを選択したときに **excel セルに値を書き込む** 必要があります。ここでは「Mark as Reviewed」というメニュー項目を追加し、識別子 `markReviewed` を付与します。この識別子はクライアント側の JavaScript がサーバーに送信するキーになります。

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**なぜカスタム識別子を使うのか？**  
識別子を使うことで UI のテキストとサーバー側ロジックが分離され、ラベルを変更してもバックエンドコードを触る必要がなくなります。また、**create right‑click menu** の操作が明示的かつ再利用可能になります。

---

## Step 3 – 右クリックメニューを作成: サーバーサイドハンドラの登録

メニュー項目を用意したら、ユーザーがクリックしたときに GridJs が何をすべきかを指示します。ここで **create right‑click menu** の機能を実装し、Python へリクエストを返すようにします。

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

留意点は次の通りです。

1. **`ws[cell_address] = "Reviewed"`** は **cell value を python 方式で更新** する最もシンプルな方法です。内部的に `openpyxl` が A1 形式のアドレスを行・列インデックスに変換します。  
2. ハンドラは小さな JSON ペイロードを返します。GridJs はステータス指標を期待しているので、必要に応じてエラーメッセージなどを追加できます。

次に識別子とハンドラを紐付けます。

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**セルが空または保護されている場合は？**  
- 空セルは問題ありません。`openpyxl` が自動的に作成します。  
- シートが保護されている場合は、先に保護を解除（`ws.protection.sheet = False`）するか、`PermissionError` を捕捉してください。

---

## Step 4 – Python でセルの値を更新: ワークブックを保存して変更を永続化

値を書き込むだけでは不十分です。**更新された excel ファイルを保存** して、変更が現在のセッションを超えて残るようにしなければなりません。ここで UI からディスクへの往復を完了させます。

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**別フォルダに保存する理由**  
`output/` ディレクトリに保存すれば、元のテンプレートがそのまま残り、監査ログとしても活用しやすくなります。デプロイ環境に合わせてパスは調整してください。

> **注意点:** 同時に多数のユーザーがアクセスする場合は、`wb.save()` の周りにスレッドセーフなロック（`threading.Lock`）を設けてレースコンディションを防止しましょう。

---

## Step 5 – クライアント設定 JSON を生成し、全体を接続

最後に、フロントエンドの GridJs インスタンスが使用する JSON を生成します。この JSON にはワークシートデータ **と** カスタムメニュー定義が含まれます。

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

`config_json` を HTML に埋め込めば、GridJs は「Mark as Reviewed」エントリがすべてのセルで右クリック可能な状態でグリッドを描画します。

### 完全な Flask 例

以下は、すべての要素を組み合わせた最小限の Flask アプリです。実行後、`http://localhost:5000` にアクセスし、任意のセルを右クリックするとカスタムメニューが表示されます。

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**期待される結果:**  
- 任意のセルを右クリック → 「Mark as Reviewed」が表示される。  
- それをクリック → セルの内容が “Reviewed” に変わる。  
- `output/sample-updated.xlsx` に新しい値が保存されている。

---

## よくある質問とエッジケース

| 質問 | 回答 |
|------|------|
| *複数のカスタムアクションが必要な場合は？* | `grid.settings.context_menu.custom_items` にオブジェクトを追加し、各々に固有の識別子を登録すれば OK です。 |
| *ハンドラに追加データ（例: 行 ID）を渡せますか？* | 可能です。クライアント側で JSON ペイロードにキーを追加し、`on_custom_command` 内で `request` から取得します。 |
| *非同期フレームワークでも使えますか？* | もちろんです。`on_custom_command` を async 関数にし、`aiofiles` などを使って `await wb.save(...)` とすれば動作します。 |
| *メニューアイコンのスタイルは？* | 任意の Material‑Icons 名（例: `"icon": "edit"`）を指定すれば、フロントエンドが自動でフォントを読み込みます。 |
| *大規模なブックの場合は？* | 必要なシートだけをロードし、`openpyxl.iter_rows()` で行をストリーミングすればメモリ使用量を抑えられます。 |

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースは完全なコード例とステップバイステップの解説が付属しており、API の追加機能習得や別実装アプローチの探求に役立ちます。

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}