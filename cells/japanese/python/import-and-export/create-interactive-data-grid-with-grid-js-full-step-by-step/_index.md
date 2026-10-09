---
category: general
date: 2026-06-21
description: Grid.js を使ってインタラクティブなデータグリッドを作成し、ソート、ページネーション、検索機能付きの JSON データテーブルの表示方法を学びましょう。ウェブダッシュボードに最適です。
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: ja
og_description: 数分でインタラクティブなデータグリッドを作成できます。Grid.js を使って、ページネーション、ソート、検索機能付きの JSON
  データテーブルの表示方法を学びましょう。
og_title: Grid.jsでインタラクティブなデータグリッドを作成する – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: Grid.jsでインタラクティブなデータグリッドを作成する – 完全ステップバイステップガイド
url: /ja/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grid.jsでインタラクティブなデータグリッドを作成する – 完全ステップバイステップガイド

バックエンドを書かずに、ユーザーが行をソート、検索、ページングできる **インタラクティブなデータグリッド** を作成する方法を考えたことはありませんか？ あなたは一人ではありません。多くのダッシュボードで最大の課題は、静的な JSON ダンプをスムーズで検索可能なテーブルに変換することです――スプレッドシートのように滑らかで、完全にブラウザ上で動作します。

このチュートリアルでは、**Grid.js の使い方** を使ってプレーンな HTML ページ上に **JSON データテーブルを表示** する方法を順を追って解説します。最後まで読むと、任意のプロジェクトに組み込める動作サンプルが手に入り、ツールバーのカスタマイズや大規模データの扱い方、よくある落とし穴の回避策も学べます。

## 学べること

- 列と行を定義した JSON ファイルを取得する方法。
- ページネーション、ソート、検索、カスタムツールバーを備えた **Grid.js** の初期化方法。
- グリッドをターゲットコンテナにレンダリングする方法。
- オプションの調整：カスタムセルフォーマット、テーマ切替、エラーハンドリング。
- 完全なコピー＆ペースト可能なコードサンプル。

### 前提条件

1. 最新のブラウザ（Chrome、Edge、Firefox） – Grid.js は ES6 機能に依存しています。
2. `grid_data.json` ファイルを含むローカルまたはリモートのフォルダ（フォーマットは後述）。
3. HTML と JavaScript の基本的な知識 – 特別なことは不要で、`.html` ファイルをブラウザで開くことができれば OK。

ビルドツールも npm インストールもサーバーサイドコードも不要です。これが **インタラクティブなデータグリッド** を Grid.js で作成する魅力です：CDN から直接利用できます。

---

## ステップ 1: テーブルを定義する JSON を用意する

最初に必要なのは、Grid.js に列が何で行が何かを伝える JSON ペイロードです。これは **JSON データテーブルを表示** するための設計図と考えてください。以下の最小例を `grid_data.json` として、HTML ファイルと同じディレクトリに保存できます。

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*Why this format?* Grid.js expects `columns` to be an array of strings (or objects for advanced configuration) and `rows` to be an array of arrays where each inner array matches the column order. You can, of course, add more columns or nested objects – Grid.js will render them as long as the shapes line up.

> **Pro tip:** If you’re pulling data from an API, just replace the static `fetch('grid_data.json')` with your endpoint URL. The rest of the code stays the same.

---

## ステップ 2: Grid.js を初期化する – **how to use gridjs** の核心

データソースの準備ができたら、Grid.js をページに組み込み、動作を指示します。ここで実際に **インタラクティブなデータグリッド** の機能（ページネーション、ソート、便利なツールバーボタン）を作ります。

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN から最新の安定版が取得でき、Meri­maid テーマがすぐにクリーンでモダンな外観を提供します。デフォルトスタイルが好みなら `gridjs.min.css` に差し替えても構いません。

次に、`<script>` タグ内で JSON を取得し、グリッドを初期化します：

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### オプションの詳細

| オプション | 機能 | 重要性 |
|------------|------|--------|
| `pagination` | 行をページに分割します（デフォルトはページあたり10行） | 大規模なテーブルでも UI が圧倒されずに使いやすくなります。 |
| `sort` | クリック可能な列ヘッダーで昇順/降順を切り替えます | ユーザーは最高値の行をすぐに見つけられます。 |
| `search` | テキスト入力を追加し、リアルタイムで行をフィルタリングします | データを再読み込みせずに臨時検索が可能です。 |
| `toolbar` | グリッド上部にカスタムボタンやドロップダウンを追加します | 「ヘルプ」や「エクスポート」「リフレッシュ」などの操作に最適です。 |
| `formatter` | セルに生の HTML を返すことができます | ここではメール文字列をクリック可能な mailto リンクに変換しています。 |

> **Why this approach?** By keeping the grid configuration declarative, you can easily tweak behaviour without touching the core rendering logic. This is the recommended way to **how to use Grid.js** for most projects.

---

## ステップ 3: グリッドをページにレンダリングする

スクリプトの最後の行 `grid.render(document.getElementById('grid-container'))` が、HTML 本文の任意の場所に配置した `<div>` に完全に機能するテーブルを注入します：

```html
<div id="grid-container"></div>
```

以上です。ページが読み込まれると、ブラウザが JSON を取得し、Grid.js インスタンスを構築して、インタラクティブなテーブルを画面に描画します。初回ロード以降のリフレッシュやサーバー呼び出しは不要です。

---

## オプション: スタイルとテーマの調整

デフォルトの Meri­maid テーマが好みでなければ、組み込みテーマ（`gridjs.min.css`）に切り替えるか、独自の CSS を記述できます。例えば、ヘッダー背景を淡いグレーにしたい場合は次のようにします：

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

このスニペットを `<style>` タグ内または外部スタイルシートに追加してください。Grid.js は標準的な CSS セレクタを尊重するため、フォント・色・余白などを自由にコントロールできます。

---

## よくある落とし穴と回避策

| 落とし穴 | 症状 | 対策 |
|----------|------|------|
| 別ドメインから JSON を取得する際の **CORS エラー** | ブラウザコンソールに “Blocked by CORS policy” と表示 | JSON を同一オリジンにホストするか、サーバーで CORS を有効化してください。 |
| **大規模データで遅延** | スクロールがカクつき、ページネーションが遅くなる | `server` ページネーション (`pagination: { server: { url: (prev, page, limit) => … } }`) を使用するか、行を遅延ロードしてください。 |
| **ツールバーボタンが表示されない** | `toolbar.enabled: true` にしてもボタンが見えない | Grid.js バージョン 2.0 以上を使用していることを確認してください。古いバージョンはツールバー API が異なります。 |
| **メールリンクがクリックできない** | フォーマッタがプレーンテキストを返す | 例のように `gridjs.html(...)` を返してください。 |

これらの問題に早めに対処すれば、後々のデバッグに費やす時間を大幅に削減できます。

---

## 完全動作例（コピー＆ペースト可能）

以下は `index.html` として保存できる完全な HTML ファイルです。ブラウザで開くと、**インタラクティブなデータグリッド** のデモが表示され、**JSON データテーブルを表示** しながらソート、検索、ヘルプボタンが利用できます。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Create Interactive Data Grid with Grid.js</title>
  <!-- Grid.js core library -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Optional theme – Meri­maid -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Simple custom styling */
    body { font-family: Arial, sans-serif; margin: 20px; }
    .gridjs-container { max-width: 900px; margin: auto; }
    .gridjs-th { background-color: #f0f8ff; }
  </style>
</head>
<body>
  <h1>Create Interactive Data Grid with Grid.js</h1>
  <p>This page demonstrates how to <strong>display JSON data table</strong> using Grid.js. Feel free to edit <code>grid_data.json</code> and refresh.</p>

  <!-- Grid will be rendered here -->
  <div id="grid-container"></div>

  <script>
    // Load JSON data and initialise Grid.js
    fetch('grid_data.json')
      .then(r => r.json())
      .then(data => {
        const grid = new gridjs.Grid({
          columns: data.columns.map(col => {
            // Custom formatter for Email column
            if (col === 'Email') {
              return {
                name: col,
                formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
              };
            }
            return col;
          }),
          data: data.rows,
          pagination: { enabled: true, limit: 5 },
          sort: true,
          search: true,
          toolbar: {
            enabled: true,
            items: [
              {
                type: 'button',
                text: 'Formula Help',
                onClick: () => alert('Hover over a cell to see its formula description.')
              }
            ]
          }
        });

        // Render the grid
        grid.render(document.getElementById('grid-container'));
      })
      .catch(err => console.error('Error loading grid data:', err));
  </script>
</body>
</html


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを扱っています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得したり、プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Java 用 Aspose.Cells で Excel データ検証リストを作成する方法：ステップバイステップガイド](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [.NET 用 Aspose.Cells で Excel にチェックボックスを作成する方法 | データ検証チュートリアル](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Java 用 Aspose.Cells で Excel に XML データを作成・インポートする](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}