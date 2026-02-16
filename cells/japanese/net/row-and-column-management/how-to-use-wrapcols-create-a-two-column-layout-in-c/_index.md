---
category: general
date: 2026-02-15
description: C# のワークシートで WRAPCOLS を使用して 2 列レイアウトを作成し、数式を追加し、シーケンス配列を生成する方法 – ステップバイステップガイド
draft: false
keywords:
- how to use wrapcols
- create two column layout
- how to add formula
- how to create columns
- generate sequence array
language: ja
og_description: WRAPCOLS を使用して 2 列レイアウトを作成し、数式を追加し、C# ワークシートでシーケンス配列を生成する方法 – 完全ガイド
og_title: WRAPCOLS の使い方：C# での二列レイアウト
tags:
- CSharp
- ExcelAutomation
- WorksheetFormula
title: WRAPCOLS の使い方：C# で二列レイアウトを作成する
url: /ja/net/row-and-column-management/how-to-use-wrapcols-create-a-two-column-layout-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# WRAPCOLS の使い方: C# で 2 列レイアウトを作成する

Excel 風のワークシート内で手早く 2 列表示が必要なとき、**WRAPCOLS の使い方**を疑問に思ったことはありませんか？ あなただけではありません。生成されたリストを各セルごとにループを書かずにきれいな列に分割しようとして壁にぶつかる開発者は多いです。良いニュースは、`WRAPCOLS` 関数を使えば、`A1` に単一の数式を入れるだけで、Excel（または互換エンジン）が重い処理をやってくれます。

このチュートリアルでは、**数式の追加方法**を解説し、**2 列レイアウトの作成**を行う方法、**列を動的に作成する**方法、さらには **シーケンス配列を生成**する方法を実演します。最後まで読むと、プロジェクトに貼り付けて実行できる完全に動作する C# スニペットが手に入り、すぐに整った 2 列ブロックが表示されます。

## 学習内容

- `WRAPCOLS` の目的と、手動ループに比べて優れた代替手段である理由。  
- C# を使ってワークシートのセルに **数式を追加する** 方法。  
- `SEQUENCE` でシーケンス配列を生成し、`WRAPCOLS` に渡す方法。  
- シートを再計算して数式を即座に評価させるためのヒント。  
- エッジケースの処理（例: 空のワークシート、カスタム列数）。

標準的な Excel 処理パッケージ以外の外部ライブラリは不要です – ここではシンプルな API を持つ **ClosedXML** を使用しますが、概念は EPPlus、SpreadsheetGear、あるいは Google Sheets の API にも応用できます。

---

## 前提条件

- .NET 6.0 以降（コードは .NET Core と .NET Framework でもコンパイル可能）。  
- **ClosedXML** への参照 (`dotnet add package ClosedXML`)。  
- 基本的な C# の知識 – `using` 文やオブジェクト初期化に慣れていること。  

既にブックが開いている場合は、ファイル作成の部分をスキップして数式のセクションに直接進んで構いません。

---

## ステップ 1: ワークシートの設定（列の作成方法）

まず、操作対象となる `Worksheet` オブジェクトが必要です。ClosedXML では `XLWorkbook` から取得します。以下のスニペットは新しいブックを作成し、*Demo* というシートを追加し、分かりやすさのために `worksheet` という名前で参照を取得します。

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // Create a fresh workbook and add a worksheet named "Demo"
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");

            // Rename for clarity – this is the worksheet we’ll manipulate
            var worksheet = ws;   // <-- same object, just a clearer name

            // --------------------------------------------------------------
            // Next step: write the WRAPCOLS formula
            // --------------------------------------------------------------
```

> **なぜリネームするのか？**  
> 変数名を短く保つ（`worksheet`）ことで、後続のコードが読みやすくなります。特に複数の操作をチェーンする場合に有効です。また、ほとんどのドキュメントで見られる命名スタイルと一致し、認知負荷を減らします。

---

## ステップ 2: 数式の記述（数式の追加方法 + シーケンス配列の生成）

さあ、魔法の行です。セル **A1** に数式を配置し、次の 2 つのことを行います：

1. 6 つの数値の **シーケンス配列** を生成する (`SEQUENCE(6)` → 1,2,3,4,5,6)。  
2. その数値を **2 列にラップ** する (`WRAPCOLS(..., 2)`)。

```csharp
            // Write the WRAPCOLS formula into A1
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // --------------------------------------------------------------
            // Finally, force the engine to evaluate the formula
            // --------------------------------------------------------------
```

> **何が起きているのか？**  
> `SEQUENCE(6)` は縦方向の配列 `{1;2;3;4;5;6}` を作成します。`WRAPCOLS` はその配列を指定した列数に「ラップ」します—この場合 **2** 列です。結果は 3 行 × 2 列のブロックで、次のようになります：

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

第2引数を **3** に変更すると、代わりに 3 列レイアウトが得られます。これが手動ループなしで **列を作成する方法** の核心です。

---

## ステップ 3: ワークシートの再計算（数式の評価を保証）

ClosedXML は数式を書いた時点では自動的に評価しません。評価を強制するには、ブック（または特定のワークシート）に対して `Calculate()` を呼び出す必要があります。

```csharp
            // Recalculate so the formula is evaluated immediately
            worksheet.Calculate();

            // Optional: save the workbook to inspect the result
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

> **プロのコツ:** 大きなブックを扱う場合、実際に変更があったシートだけに `Calculate()` を呼び出してください。これによりメモリ使用量が削減され、処理が高速化します。

`WrapColsDemo.xlsx` を開くと、**A1:B3** にきれいに 2 列レイアウトが配置されているのが確認できます。行や列をループする追加コードは不要で、`WRAPCOLS` がすべて処理しています。

---

## ステップ 4: 出力の確認（期待結果）

プログラム実行後に生成されたファイルを開くと、次のようになっているはずです：

| A | B |
|---|---|
| 1 | 4 |
| 2 | 5 |
| 3 | 6 |

数値が縦に（すべて列 A に）表示される場合は、数式設定 **後** に `worksheet.Calculate()` を呼び出したか確認してください。一部のエンジンでは `workbook.Calculate()` も必要です。上記スニペットは ClosedXML の組み込み評価器で動作します。

---

## よくあるバリエーションとエッジケース

### 列数の変更

異なる行数で **2 列レイアウト** を作成するには、`SEQUENCE` のサイズまたは `WRAPCOLS` の第2引数を調整するだけです：

```csharp
worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(12), 3)";
```

これにより 4 行 × 3 列のブロック（12 個の数値が 3 列に分割される）が生成されます。

### 動的な列数の使用

列数が変数から取得される場合は、文字列補間で埋め込みます：

```csharp
int colCount = 4;
worksheet.Cell("A1").FormulaA1 = $"=WRAPCOLS(SEQUENCE(8), {colCount})";
```

これで、実行時に適応する **数式の追加方法** が実現しました。

### 空のワークシート

ワークシートが空でも `Calculate()` は機能し、数式は A1 からセルを埋めます。ただし、後で出力範囲と交差する行や列を削除すると `#REF!` エラーが出ることがあります。回避するには、まず対象範囲をクリアしてください：

```csharp
worksheet.Range("A1:Z100").Clear(); // wipes any leftovers
```

### 互換性

`WRAPCOLS` と `SEQUENCE` は Excel の **Dynamic Array** 関数の一部で、Office 365 で導入されました。古い Excel バージョンを対象とする場合、これらの関数は存在せず、手動ループが必要になります。ClosedXML の評価器は最新の Excel 動作を模倣しているため、モダンな環境では安全に使用できます。

---

## 完全動作例（コピー＆ペースト可能）

```csharp
using ClosedXML.Excel;

namespace WrapColsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook & worksheet
            using var workbook = new XLWorkbook();
            var ws = workbook.Worksheets.Add("Demo");
            var worksheet = ws;   // clearer name

            // 2️⃣ Write WRAPCOLS formula that generates a sequence array
            worksheet.Cell("A1").FormulaA1 = "=WRAPCOLS(SEQUENCE(6), 2)";

            // 3️⃣ Force calculation so the formula resolves immediately
            worksheet.Calculate();

            // 4️⃣ Save the file (optional, but handy for verification)
            workbook.SaveAs("WrapColsDemo.xlsx");
        }
    }
}
```

**期待結果:** *WrapColsDemo.xlsx* を開くと、先述の通り 1‑6 の数字が整然と配置された 2 列レイアウトが表示されます。

---

## 結論

ここでは **WRAPCOLS の使い方** を通じて **2 列レイアウトの作成** を行い、プログラムで **数式の追加方法** を実演し、`SEQUENCE` がループなしで **シーケンス配列を生成**できることを確認しました。C# から Excel の動的配列関数を活用することで、コードを簡潔で読みやすく、保守しやすく保てます。

次に試してみるとよいでしょう：

- `ROWS` や `COUNTA` を使った **動的行数の作成**。  
- ClosedXML のスタイリング API を使った **出力のスタイル設定**（罫線、数値書式など）。  
- レイアウト構築後に **CSV へエクスポート** して、下流処理に利用する。

ぜひ試してみて、列数を調整し、どれだけ迅速に複雑なスプレッドシートをプロトタイプできるか体感してください。コーディングを楽しんで！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}