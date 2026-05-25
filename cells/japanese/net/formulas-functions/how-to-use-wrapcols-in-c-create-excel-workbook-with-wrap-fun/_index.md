---
category: general
date: 2026-03-30
description: C#でWRAPCOLSを使用してExcelブックを作成し、Excelにデータを追加し、WRAPROWSも併用しながら数式計算を強制する方法を学びましょう。
draft: false
keywords:
- how to use wrapcols
- create excel workbook c#
- add data to excel
- force formula calculation
- how to use wraprows
language: ja
og_description: C#でWRAPCOLSを使用してExcelブックを作成し、データを追加し、数式の計算を強制し、配列数式にWRAPROWSを活用する方法を学びましょう。
og_title: C#でWRAPCOLSを使用する方法 – 完全ガイド
tags:
- Aspose.Cells
- C#
- Excel Automation
title: C#でWRAPCOLSを使用する方法 – ラップ関数でExcelブックを作成
url: /ja/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で WRAPCOLS を使用する方法 – Wrap 関数で Excel ワークブックを作成する

C# で Excel を自動化するときに **WRAPCOLS の使い方** を疑問に思ったことはありませんか？ あなたは一人ではありません—水平範囲を大量のコードを書かずに垂直配列に変換する必要があると、多くの開発者が壁にぶつかります。良いニュースは、Aspose.Cells がそれをとても簡単にしてくれることです。

このチュートリアルでは、**WRAPCOLS の使い方**、**C# スタイルで Excel ワークブックを作成する方法**、**Excel にデータを追加する方法**、さらに **数式の計算を強制する方法** を示す、完全で実行可能なサンプルを順に解説します。また、逆方向の変換のために **WRAPROWS の使い方** も紹介します。最後まで読むと、すぐに実行できるプログラムと、各手順がなぜ重要かが明確に理解できるようになります。

---

![How to use WRAPCOLS in C# example](alt="Screenshot showing Excel workbook after using WRAPCOLS in C#")

## 本ガイドでカバーする内容

* Aspose.Cells を使用して新しいワークブックを設定する。
* セルをプログラムで埋める (**add data to Excel**)。
* `WRAPCOLS` 関数を適用して行を列に変換する。
* `WRAPROWS` を使用して列を行に戻す (**how to use wraprows**)。
* エンジンに数式をすぐに評価させる (**force formula calculation**)。
* ファイルを保存し、出力を確認する。

外部ドキュメントは不要です—必要な情報はすべてここにあります。

## C# で WRAPCOLS を使用する方法 – ステップバイステップ実装

以下は完全なソースファイルです。新しいコンソールプロジェクトにコピー＆ペーストし、Aspose.Cells の NuGet パッケージを追加して **F5** を押すだけです。

```csharp
// ------------------------------------------------------------
// How to Use WRAPCOLS in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.Cells;

namespace WrapFunctionsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh workbook (this is how we **create excel workbook c#** style)
            Workbook workbook = new Workbook();

            // 2️⃣ Grab the first worksheet – it's created by default
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ **Add data to Excel**: place two numbers side‑by‑side
            sheet.Cells["A1"].PutValue(1);   // first value
            sheet.Cells["B1"].PutValue(2);   // second value

            // 4️⃣ **How to use WRAPCOLS** – turn the horizontal range A1:B1 into a vertical array
            //    The second argument (1) tells WRAPCOLS to create 1 column per element.
            sheet["C1"].Formula = "WRAPCOLS(A1:B1, 1)";

            // 5️⃣ **How to use WRAPROWS** – the opposite; turn the same range into a horizontal array
            //    Here we ask for 2 rows per element, which produces a single row with both values.
            sheet["C2"].Formula = "WRAPROWS(A1:B1, 2)";

            // 6️⃣ **Force formula calculation** so the workbook reflects the results immediately
            workbook.CalculateFormula();

            // 7️⃣ Save the workbook to disk – change the path to a folder you own
            string outputPath = @"WrapFunctions.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
            Console.WriteLine("Check cells C1 and C2 for the WRAPCOLS / WRAPROWS results.");
        }
    }
}
```

### 各行が重要な理由

| Step | Explanation |
|------|-------------|
| **1️⃣ 新しいワークブックを作成** | これは基礎です。Aspose.Cells は `Workbook` オブジェクトを Excel ファイル全体として扱うため、実質的に **C# スタイルで Excel ワークブックを作成** しています。 |
| **2️⃣ 最初のワークシートを取得** | 新しいワークブックには常に少なくとも1つのワークシート（`Worksheets[0]`）が含まれます。早めに取得することで null 参照の問題を回避できます。 |
| **3️⃣ Excel にデータを追加** | `PutValue` を使用することで、セルの書式設定を気にせず **Excel にデータを追加** できます。数値 `1` と `2` はラップ関数のテストデータです。 |
| **4️⃣ WRAPCOLS の使い方** | `WRAPCOLS(A1:B1, 1)` は、範囲 `A1:B1` の値を垂直に、1 行につき 1 つずつ展開するよう Excel に指示します。結果は `C1` に配置され、下方向に展開されます（`C1`, `C2`, …）。 |
| **5️⃣ WRAPROWS の使い方** | `WRAPROWS(A1:B1, 2)` は逆の動作を行い、水平に展開して、2 つの値を `C2` から始まる単一の行に収めます。 |
| **6️⃣ 数式の計算を強制** | デフォルトでは、Aspose.Cells は計算を Excel でファイルを開くまで遅延させることがあります。`CalculateFormula()` を呼び出すことで **数式の計算を強制** し、保存直後に結果をすぐに取得できます。 |
| **7️⃣ ワークブックを保存** | 最終ステップで全てをディスクに書き込みます。生成された `WrapFunctions.xlsx` を開いて結果を確認してください。 |

---

## C# で Excel ワークブックを作成 – 環境設定

コードを実行する前に、以下のツールが揃っていることを確認してください：

1. **.NET 6.0+** – 最新の LTS バージョンが最適です。
2. **Visual Studio 2022**（または C# 拡張機能付き VS Code）。
3. **Aspose.Cells for .NET** – NuGet でインストール:  
   ```bash
   dotnet add package Aspose.Cells
   ```
4. 出力ファイルを書き込めるフォルダー。

これらの前提条件は最小限です。COM インターロップや Office のインストールは不要で、これが Aspose.Cells がサーバーサイドの Excel 生成に人気の理由です。

## Excel にデータを追加 – ベストプラクティス

プログラムで **Excel にデータを追加** する際は、以下のポイントに留意してください：

* **`PutValue` を使用**して、生の数値や文字列を設定します。データ型を自動的に検出します。
* 大規模プロジェクトでは **セルアドレスのハードコーディングを避ける**—ループや名前付き範囲を使用してスケーラビリティを確保します。
* **セルスタイルは必要最低限に**設定します。スタイル変更はオーバーヘッドがかかります。書式設定が必要な場合は、単一のスタイルオブジェクトを作成し、複数のセルに適用してください。

この小さな例では 2 つの数値だけを挿入していますが、同じパターンは数千行にまで拡張可能です。

## WRAPROWS の使い方 – 水平配列の例

`WRAPCOLS` の逆が必要な場合は、`WRAPROWS` が適しています。構文は次のとおりです：

```
WRAPROWS(source_range, [rows_per_item])
```

* `source_range` – 変換したい範囲。
* `rows_per_item` – オプション。各要素が占める行数を Excel に指示します。デモでは `2` を使用し、2 つの値を単一の行に収めました。

第2引数を変更して試すことができます：

```csharp
// Example: split each value into its own column, three rows per item
sheet["D1"].Formula = "WRAPROWS(A1:B1, 3)";
```

ワークブックを開くと、値が 3 列にわたって展開され、各列に元の数値が必要に応じて繰り返されているのが確認できます。

## 数式の計算を強制 – いつ・なぜ

「本当に `CalculateFormula()` を呼び出す必要があるのか？」と疑問に思うかもしれません。その答えは **はい**、以下の場合です：

* 保存後に計算済みの値を **プログラムで** 読み取る予定がある場合。
* Excel でファイルを開いたときに、正しい結果が既に表示されていることを保証したい場合。
* **ヘッドレス環境**（例：Web API）で実行しており、ユーザーが手動で再計算をトリガーしない場合。

この手順を省略してもワークブックは壊れませんが、セルには計算された値ではなく数式テキスト（`=WRAPCOLS(...)`）が表示され、Excel が再計算するまで結果が反映されません。

## 期待される出力 – 確認ポイント

プログラムを実行し、`WrapFunctions.xlsx` を開くと：

| Cell | Formula | Displayed Value |
|------|---------|-----------------|
| **C1** | `=WRAPCOLS(A1:B1, 1)` | `1`（C1） と `2`（C2） – 縦方向リスト |
| **C2** | `=WRAPROWS(A1:B1, 2)` | `1`（C2） と `2`（D2） – 横方向リスト |

つまり、**C1** から始まる列と **C2** から始まる行が表示されます。これにより、両方のラップ関数が期待通りに動作したことが確認できます。

## エッジケースとバリエーション

| Scenario | What changes? | Suggested tweak |
|----------|---------------|-----------------|
| **大きな範囲 (A1:Z1)** | 垂直に展開する値が増える | `WRAPCOLS` の第2引数を増やすと、グループごとに複数列に展開できます。 |
| **非数値データ** | 文字列も同様に処理される | コード変更不要；`PutValue` は任意のオブジェクトを受け取ります。 |
| **動的範囲** | コンパイル時にサイズが分からない | `sheet.Cells.MaxDataColumn` と `MaxDataRow` を使用してアドレス文字列を構築します。 |
| **複数シート** | 異なるシートでラップ関数を適用する必要がある | 正しいワークシートを参照します（`workbook.Worksheets["Sheet2"]`）。 |

## 現場からのプロティップス

* **Pro tip:** .NET Core 3.1+ を対象とする場合は、ワークブック作成を `using` ブロックでラップして、リソースが速やかに解放されるようにします。
* **Watch out for:** `CalculateFormula()` を呼び出さずに大きな範囲に同じ数式を設定すると、パフォーマンスのボトルネックになる可能性があります。可能な限り数式をバッチ処理してください。
* **Tip:** コード内で計算結果を再取得する必要がある場合は、` 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}