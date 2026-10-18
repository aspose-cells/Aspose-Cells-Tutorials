---
category: general
date: 2026-06-08
description: GridJsにカスタムコンテキストメニューを追加し、CSVファイルのBlobダウンロードでグリッドをCSVにエクスポートします。完全に動作する例については、このステップバイステップのチュートリアルをご覧ください。
draft: false
keywords:
- add custom context menu
- export grid to csv
- download csv file blob
- GridJs context menu
- Flask CSV export
language: ja
og_description: GridJsにカスタムコンテキストメニューを追加し、CSVファイルのBlobでグリッドをエクスポートできます。10分以内に完全な実装方法を学べます。
og_title: GridJsにカスタムコンテキストメニューを追加する – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Add custom context menu to GridJs and export grid to CSV with a download
    CSV file blob. Follow this step‑by‑step tutorial for a fully working example.
  headline: Add Custom Context Menu to GridJs – Complete Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- Python
- Flask
title: GridJsにカスタムコンテキストメニューを追加する – 完全ガイド
url: /ja/python/formulas-and-functions/add-custom-context-menu-to-gridjs-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJs にカスタムコンテキストメニューを追加 – 完全ガイド

GridJs コンポーネントに **カスタムコンテキストメニュー** を追加したいですか？このチュートリアルでは、その手順を詳しく解説し、**download CSV file blob** を使用して **grid を CSV にエクスポート** する方法を示します。簡易的な管理パネルを作る場合でも、本格的なレポートダッシュボードを構築する場合でも、ユーザーが CSV としてデータを取得できる右クリックメニューは、生産性を大幅に向上させます。

このガイドでは、Flask を使った Python 側、Blob を生成する JavaScript ハンドラ、そして GridJs が出力する HTML/JS のすべてをカバーします。最後まで読めば、どのプロジェクトにもすぐに組み込める自己完結型の例が手に入ります。

---

## 必要なもの

- **Python 3.9+** と **Flask** がインストールされていること（`pip install flask`）。
- **gridjs** の Python ラッパー（または直接 JavaScript ライブラリ） – 本ガイドでは、JavaScript API をそのまま映す薄い Python ラッパーを想定しています。
- **async JavaScript**（`fetch`、`Promise`）の基本的な理解 – 心配いりません、各行を解説します。
- お好みのエディタ（VS Code、PyCharm、あるいはシンプルなテキストエディタでも可）。

以上です。余計なフロントエンドビルドツールや Node npm の手順は不要です。単に Flask が GridJs が生成する HTML を配信するだけです。

---

## GridJs にカスタムコンテキストメニューを追加

最初に行うべきことは、GridJs にカスタム右クリックメニューが欲しいことを伝えることです。デフォルトの GridJs には最小限のメニュー（コピー、貼り付けなど）が用意されていますが、これを完全に置き換えることができます。

```python
# Step 1: Create a new workbook that will be displayed in the grid
workbook = Workbook()

# Step 2: Initialise the GridJs component with the workbook
grid_js = GridJs(workbook)

# Step 3: Define a custom context‑menu that includes an "Export CSV" command
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]
```

**Why this matters:**  
Setting `CustomContextMenu` replaces the default list with the one you provide. The string `"Export CSV"` is just a label – the real work happens when the user clicks it, which we’ll wire up in the next step.

> *Pro tip:* Keep the list short. A cluttered context menu defeats the purpose of quick actions.

> **プロのコツ:** メニューは短く保ちましょう。ごちゃごちゃしたコンテキストメニューは、クイックアクションの本来の目的を損ないます。

---

## Blob ダウンロードで Grid を CSV にエクスポート

メニュー項目が用意できたので、サーバーと通信し CSV を取得し **Blob** に変換してダウンロードを強制する JavaScript ハンドラが必要です。ここが **download CSV file blob** というフレーズの出番です。

```python
# Step 4: Attach a JavaScript handler that runs when "Export CSV" is chosen.
#         The handler sends an AJAX request to a server endpoint,
#         receives the CSV file as a Blob, and triggers a download.
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""
```

### ハンドラの詳細解説

| 行 | 何をするか |
|------|--------------|
| `fetch('/export/csv?sheet=' + cell.sheetName)` | Flask のルート（`/export/csv`）を呼び出し、シート名をクエリ文字列として渡します。 |
| `.then(r => r.blob())` | HTTP 応答を **Blob** に変換します。Blob は CSV データを保持するバイナリコンテナです。 |
| `URL.createObjectURL(b)` | ブラウザがファイルのように扱える一時的な URL を生成します。 |
| `a.download = cell.sheetName + ".csv"` | ダウンロードダイアログに表示されるファイル名を設定します。 |
| `a.click()` | 隠しアンカーをプログラム的にクリックし、Blob のダウンロードを促します。 |

> **Why use a Blob?**  
> Browsers can’t directly download raw text returned from `fetch` without turning it into something file‑like. The Blob‑URL trick is the most reliable, cross‑browser way to trigger a **download CSV file blob** without refreshing the page.

> **なぜ Blob を使うのか？**  
> ブラウザは `fetch` で返された生テキストをそのままダウンロードできません。ファイルのような形に変換する必要があります。Blob‑URL を利用する手法は、ページをリロードせずに **download CSV file blob** を実行できる、最も信頼性が高くクロスブラウザ対応の方法です。

---

## Flask バックエンドの設定

フロントエンドハンドラは `/export/csv` エンドポイントを期待しています。以下はシート名を受け取り、ワークブックからデータを取得し、CSV をストリームとして返す最小限の Flask ビューです。

```python
from flask import Flask, request, Response
import csv
import io

app = Flask(__name__)

# Assume `workbook` is a global object we created earlier
# (in a real app you’d probably fetch it from a database or session)
@app.route('/export/csv')
def export_csv():
    sheet_name = request.args.get('sheet', 'default')
    # Retrieve the sheet data – this is pseudo‑code; replace with your actual API
    sheet = workbook.get_sheet(sheet_name)

    # Convert rows to CSV in memory
    output = io.StringIO()
    writer = csv.writer(output)
    writer.writerow(sheet.headers)          # Header row
    writer.writerows(sheet.rows)            # Data rows

    # Create a Flask response with the correct MIME type
    csv_bytes = output.getvalue().encode('utf-8')
    return Response(
        csv_bytes,
        mimetype='text/csv',
        headers={'Content-Disposition': f'attachment;filename={sheet_name}.csv'}
    )
```

### 重要ポイント

- **`io.StringIO`** は、ファイルシステムに触れずにメモリ上で CSV を構築できるようにします。
- **`Content‑Disposition`** は、ブラウザにファイルが添付ファイルであることを伝え、ファイル名を提案します。フロントエンドでも `a.download` を設定していますが、サーバ側で設定しておくことで、JS を使用しないクライアントへのフォールバックになります。
- このルートは意図的にシンプルです。後で認証や権限チェック、巨大データセット向けのストリーミングなどを追加できます。

---

## クライアント側で Grid を描画

コンテキストメニューとバックエンドが整ったら、最後のステップは GridJs コンポーネントを描画し、HTML/JS をブラウザに送ることです。

```python
# Step 5: Render the grid to obtain the full HTML/JS needed on the client side
html_output = grid_js.Render()
print(html_output)   # Sends the HTML/JS to the client (e.g., in a Flask view)
```

Flask のビューでは通常次のように書きます:

```python
@app.route('/')
def index():
    html_output = grid_js.Render()
    return f"""
    <!doctype html>
    <html>
    <head>
        <title>Grid with Custom Context Menu</title>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
    </head>
    <body>
        {html_output}
    </body>
    </html>
    """
```

ページが読み込まれると、GridJs がテーブルを構築し、カスタムコンテキストメニューを注入します。先ほど定義した JavaScript ハンドラもすぐに使用可能です。任意のセルを右クリックし **Export CSV** を選択すると、シート名を付けた CSV ファイルがブラウザからダウンロードされます。

---

## 完全動作例（全ファイル）

以下は新しいフォルダにコピー＆ペーストできる、完全に実行可能なコードです。Flask をインストール（`pip install flask`）し、`python app.py` を実行してください。

**`app.py`**

```python
from flask import Flask, request, Response
import csv, io

# Mock classes to simulate the GridJs wrapper – replace with the real library
class Workbook:
    def __init__(self):
        self.sheets = {"Sheet1": Sheet()}
    def get_sheet(self, name):
        return self.sheets.get(name, self.sheets["Sheet1"])

class Sheet:
    def __init__(self):
        self.headers = ["ID", "Name", "Score"]
        self.rows = [
            [1, "Alice", 85],
            [2, "Bob", 92],
            [3, "Charlie", 78],
        ]

class GridJs:
    def __init__(self, workbook):
        self.workbook = workbook
        self.CustomContextMenu = []
        self.CustomContextMenuHandler = ""
    def Render(self):
        # Very simplified HTML – real GridJs would generate a lot more
        return f'''
        <div id="grid"></div>
        <script>
            const grid = new gridjs.Grid({{
                columns: {self.workbook.get_sheet("Sheet1").headers},
                data: {self.workbook.get_sheet("Sheet1").rows},
                search: true,
                pagination: true,
                customContextMenu: {self.CustomContextMenu},
                customContextMenuHandler: {self.CustomContextMenuHandler}
            }}).render(document.getElementById("grid"));
        </script>
        '''

app = Flask(__name__)

# Initialise workbook and grid
workbook = Workbook()
grid_js = GridJs(workbook)

# ==== Step 3: Custom context menu ====
grid_js.CustomContextMenu = ["Copy", "Paste", "Export CSV"]

# ==== Step 4: Handler that downloads a CSV blob ====
grid_js.CustomContextMenuHandler = """
function(action, cell) {
    if (action === "Export CSV") {
        fetch('/export/csv?sheet=' + cell.sheetName)
            .then(r => r.blob())
            .then(b => {
                const url = URL.createObjectURL(b);
                const a = document.createElement('a');
                a.href = url;
                a.download = cell.sheetName + ".csv";
                a.click();
            });
    }
}
"""

@app.route('/')
def index():
    html_output = grid_js.Render()
    return f'''
    <!doctype html>
    <html>
    <head>


## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基にした、密接に関連するテーマを扱っています。各リソースには、ステップバイステップの解説と完全に動作するコード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Aspose Cells Java のカスタムパーサーで CSV ファイルをロード](/cells/hindi/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)
- [Java コードで CSV エクスポート](/cells/hindi/java/excel-import-export/csv-export-java-code/)
- [Aspose Cells .NET で Excel CSV の空白行をエクスポート](/cells/hindi/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}