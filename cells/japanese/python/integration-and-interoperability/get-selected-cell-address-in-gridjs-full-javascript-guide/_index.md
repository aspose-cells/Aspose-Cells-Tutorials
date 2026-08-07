---
category: general
date: 2026-06-30
description: GridJs を使って JavaScript で選択したセルのアドレスを取得し、グリッドセルの値を更新し、入力値を読み取る方法を学びましょう。ステップバイステップのコードとヒント。
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: ja
og_description: 選択したセルのアドレスを取得し、グリッドセルの値を更新し、JavaScriptで入力値を取得します。スムーズな GridJs 統合のために、この完全なガイドに従ってください。
og_title: 選択したセルのアドレス取得 – 完全な GridJs JavaScript チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: GridJsで選択されたセルのアドレスを取得する – 完全なJavaScriptガイド
url: /ja/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 選択されたセルアドレスの取得 – 完全な GridJs JavaScript チュートリアル

GridJs テーブルから **選択されたセルアドレスを取得** したいが、どの API 呼び出しを使えばよいか分からないことはありませんか？ あなただけではありません。多くの管理パネルでは、ユーザーがセルをクリックし、モーダルで値を編集し、グリッドが即座に変更を反映することを期待します。このチュートリアルでは、そのアドレスの取得方法、入力フィールドから新しい価格を読み取る方法、そしてページリロードなしで **グリッドセルの値を更新** する方法を正確に示します。

また、**JavaScript で入力値を読み取る** 正しい方法、エッジケースの処理、更新が完了したらモーダルを閉じる方法もカバーします。最後まで読むと、GridJs を使用する任意のプロジェクトに貼り付けられる自己完結型のスニペットが手に入ります。

## 作成するもの

- GridJs によって動作するシンプルな HTML テーブル。
- セルがクリックされたときに表示される編集モーダル。
- JavaScript で **選択されたセルアドレスを取得** し、ユーザーが入力した価格を取得し、**グリッドセルの値を更新** し、最後にモーダルを非表示にする。

GridJs 以外の外部ライブラリは不要で、コードは最新のブラウザ（Chrome 102 以上、Edge、Firefox）で動作します。ページにすでに GridJs のインスタンスがある場合は、該当部分を直接コピー＆ペーストできます。

## 前提条件

- JavaScript と DOM の基本的な知識。
- GridJs ライブラリがロードされていること（CDN または npm 経由）。
- すでに GridJs グリッドを表示しているページ（最小限の例を示します）。

これらのいずれかが馴染みがない場合でも、パニックになる必要はありません—各ステップに簡単な復習が含まれています。

---

## ステップ 1: HTML スケルトンの設定

まず、テーブルコンテナ、非表示のモーダル、価格入力フィールドを配置します。モーダルはシンプルな CSS クラスで切り替えられます。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **Pro tip:** `#editModal` は最小限の CSS テクニックを使用しています—`active` クラスを追加するだけで表示されます。これを Bootstrap、Tailwind、または既に使用している任意のモーダルコンポーネントに置き換えることができます。

---

## ステップ 2: GridJs の初期化とセルクリックの取得

ここではサンプルデータでグリッドを作成し、セル選択をリッスンします。ユーザーがセルをクリックすると、**選択されたセルアドレスを取得** し、モーダルを開きます。

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **Why this works:** `GridJs.getSelectedCell()` は `"C2"` のような文字列（列 C、行 2）を返します。これを `lastSelectedCell` に保存することで、後で **update grid cell value** を行う際に正確な位置を参照できます。

---

## ステップ 3: 入力フィールドから新しい価格を読み取る

ユーザーが **Save** をクリックしたとき、安全に **JavaScript で入力値を読み取る** 必要があります。このステップでは、入力された価格が正の数であることも検証します。

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **Note:** `parseFloat` を使用すると小数（例: `1.99`）を受け入れられます。`isNaN` ガードは誤って空の送信が行われるのを防ぎます。

---

## ステップ 4: 選択されたセルの値を更新する

これで、先ほど取得したアドレスを使って **grid cell value を更新** します。GridJs の `updateCell` メソッドは Promise を返すので、モーダルを閉じるアクションをチェーンできます。

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **Why use a promise?** GridJs はテーブルの再描画やバックエンドとの同期が必要になる場合があります。Promise が解決されるのを待つことで、グリッドが新しい値を反映した後にのみ UI が非表示になることを保証します。

---

## ステップ 5: キャンセルとエッジケースの処理

堅牢なソリューションは常にユーザーに抜け道を提供します。**Cancel** ボタンは単にモーダルを非表示にし、保存されたアドレスをクリアします。

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### セルが選択されていない場合は？

ユーザーがセルをクリックせずに（プログラムでモーダルを開いたなど）**Save** ボタンを起動した場合、`lastSelectedCell` は `null` になります。`updateSelectedCell` の早期リターンにより、ランタイムエラーが防止され、役立つ警告がログに記録されます。

### 大規模グリッドの取り扱い

ページネーションがあるグリッドでも、`GridJs.getSelectedCell()` は可視行だけでなく絶対アドレス（例: `"B12"`）を返します。これにより、編集された行が別ページにあっても更新が機能します。ただし、更新後に UI が自動的にページを切り替えることはありません—必要な場合は `grid.forceUpdate()` を呼び出すか、手動で適切なページへ移動してください。

---

## 完全な動作例

以下は単一の HTML ファイルにコピー＆ペーストできる完全なコードです。ブラウザで開き、任意のセルをクリックし、価格を変更すると、グリッドが即座に更新されるのが確認できます。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Get Selected Cell Address – GridJs Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal" aria-modal="true" role="dialog">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script>
  // Initialise the grid
  const grid = new gridjs.Grid({
    columns: ['Item', 'Quantity', 'Price'],
    data: [
      ['Apple', 10, 0.5],
      ['Banana', 5, 0.3],
      ['Cherry', 20, 0.2]
    ],
    pagination: { limit: 5 },
    sort: true
  }).render(document.getElementById('grid'));

  let lastSelectedCell = null;

  // Capture cell clicks – this is where we **get selected cell address**
  grid.on('cell', (event) => {
    const address = GridJs.getSelectedCell();   // primary keyword usage
    lastSelectedCell = address;
    document.getElementById('editModal').classList.add('active');
    document.getElementById('price').value = event.target.innerText;
  });

  // Save button – **read input value with JavaScript**
  document.getElementById('saveBtn').addEventListener('click', () => {
    const raw = document.getElementById('price').value;
    const newPrice = parseFloat(raw);
    if (isNaN(newPrice) || newPrice < 0) {
      alert('Please enter a valid positive number.');
      return;
    }
    updateSelectedCell(newPrice);
  });

  // Core update logic – **update grid cell value**
  function updateSelectedCell(value) {
    if (!lastSelectedCell) {
      console.warn('No cell selected – nothing to update.');
      return;
    }
    GridJs.updateCell(lastSelectedCell, value)
      .then(() => {
        document.getElementById('editModal').classList


## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックをカバーしています。各リソースには、完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを探求するのに役立ちます。

- [Excel 全体範囲のアドレス、セル数、オフセットの取得](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Excel 全体範囲のアドレス、セル数、オフセットの取得（German）](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Excel 全体範囲のアドレス、セル数、オフセットの取得（French）](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}