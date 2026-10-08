---
category: general
date: 2026-02-23
description: C#でプログラム的に新しいブックを作成し、セルに数式を追加します。EXPANDの使い方を学び、Excelブックを簡単に保存できます。
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: ja
og_description: C#でプログラム的に新しいブックを作成し、セルに数式を追加、EXPANDの使い方を学び、数秒でExcelブックを保存します。
og_title: C#で新しいワークブックを作成 – 数式を追加してExcelファイルを保存
tags:
- C#
- Excel Automation
- Aspose.Cells
title: C#で新しいワークブックを作成 – 数式を追加してExcelファイルを保存
url: /ja/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で新しいブックを作成 – 数式を追加して Excel ファイルを保存

Excel を開かずにコードから **新しいブック** オブジェクトを作成したいと思ったことはありませんか？ あなただけではありません。レポートやエクスポート、クイックデータダンプなど、オンザフライでスプレッドシートを生成する必要がある開発者は多いです。  

良いニュースです！ 本ガイドでは、**新しいブックを作成**し、**セルに数式を追加**し、数行の C# だけで **Excel ブックを保存**する方法を正確に示します。また、**EXPAND の使い方**にも踏み込み、手動でコピーすることなく動的配列を生成できるようにします。最後まで読めば、**プログラムで Excel ファイルを作成**し、ユーザーや下流サービスに配布できるようになります。

## 前提条件

- .NET 6.0 以降（任意の最新 .NET ランタイムで可）
- Aspose.Cells for .NET（無料トライアルまたはライセンス版） – 本ライブラリが以下で使用する `Workbook` と `Worksheet` クラスを提供します。
- C# の基本的な構文理解 – 深い Excel 知識は不要です。

これらが揃っていれば完璧です！ まだの場合は NuGet から Aspose.Cells を取得してください（`Install-Package Aspose.Cells`）で準備完了です。

---

## 手順 1: 新しいブックを作成 – 基礎

まず、空のブックオブジェクトをインスタンス化します。これは、全く何も入っていない新規 Excel ファイルを開くイメージです。

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **重要ポイント:** `Workbook` クラスはすべての Excel 操作のエントリーポイントです。新しいインスタンスを作成することで、シート、スタイル、数式用のメモリが確保され、ファイルシステムに触れることなく操作できます。

---

## 手順 2: 最初のワークシートにアクセス

新しいブックはデフォルトで 1 枚のシート（*Sheet1*）が付属しています。ここからデータや数式を配置します。

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **プロのコツ:** 複数シートが必要な場合は `workbook.Worksheets.Add("MySheet")` を呼び出し、返される `Worksheet` オブジェクトを使用してください。

---

## 手順 3: セルに数式を追加 – EXPAND を使用

さあ、楽しいパートです。数式を挿入します。`EXPAND` 関数は、静的配列を大きな自動拡張範囲に変換したいときに最適です。

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### EXPAND 数式の仕組み

| 引数 | 意味 |
|------|------|
| `{1,2,3}` | ソース配列（横方向に並んだ 3 つの数値） |
| `5` | 結果として得たい行数 |
| `1` | 結果として得たい列数（縦方向に保つため 1） |

Excel がこの数式を評価すると、**縦方向**のリストが生成されます。

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **なぜ EXPAND を使うのか？** 手動でコピーしたり VBA ループを書いたりする必要がなくなります。関数がデータを動的に再形成するため、スプレッドシートがより堅牢で保守しやすくなります。

---

## 手順 4: Excel ブックを保存 – 結果を永続化

数式を配置したら、最後にブックをディスクに書き出します。書き込み権限のある任意のフォルダーを指定できます。

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **期待される結果:** `ExpandFormula.xlsx` を Excel で開くと、セル `A1` に拡張された配列が表示されます。数式自体はセルに残っているので、元の配列を編集すれば出力が自動的に更新されます。

---

## 任意: プログラムで出力を検証

Excel を手動で開きたくない場合は、値を読み戻して期待通りか確認できます。

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

上記を実行すると次のように出力されます。

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## よくある質問とエッジケース

| 質問 | 回答 |
|------|------|
| **EXPAND をもっと大きなソース配列で使えますか？** | もちろんです。`{1,2,3}` を任意の定数やセル範囲に置き換えるだけです。例: `EXPAND(A1:C1,10,1)` |
| **横方向の結果が欲しい場合は？** | 行・列の引数を入れ替えてください。`EXPAND({1,2,3},1,5)` は 1 行 5 列の配列を生成します。 |
| **古い Excel バージョンでも動作しますか？** | `EXPAND` は Excel 365/2021 以降で利用可能です。旧バージョンの場合は `INDEX`/`SEQUENCE` で配列をシミュレートする必要があります。 |
| **`workbook.CalculateFormula()` を呼び出す必要がありますか？** | 必要ありません。Aspose.Cells は保存時に自動で数式を評価するため、値は即座に表示されます。 |
| **保存前にシートを複数追加したい場合は？** | `workbook.Worksheets.Add("SecondSheet")` を呼び出し、新しいシートで同様のセル操作を繰り返してください。 |

---

## 完全動作サンプル

以下はそのまま実行可能なプログラムです。コンソールアプリに貼り付け、出力パスを調整して **F5** を押すだけです。

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**コンソールに期待される出力:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

生成されたファイルを開くと、列 **A** に同じ数値が配置されていることが確認できます。

---

## ビジュアルサマリー

![新しいブック作成例](create-new-workbook.png "C# で新しいブックを作成した際のスクリーンショット")

*画像は、EXPAND の結果が表示された新規生成ブックを示しています。*

---

## 結論

これで **新しいブックを作成**し、**セルに数式を追加**し、**Excel ブックを保存**する方法が C# で分かりました。**EXPAND の使い方**をマスターすれば、手作業なしで動的配列を生成でき、あらゆる自動化シナリオで **プログラムで Excel ファイルを作成**できるようになります。

次は何をしますか？ 定数配列を範囲参照に置き換えてみたり、`EXPAND` の次元を変えて実験したり、シート間で複数の数式を連鎖させてみましょう。同じパターンはチャート、スタイリング、ピボットテーブルにも応用できるので、ぜひ探求を続けてください。

問題があればコメントで教えてください。コーディングを楽しみながら、プログラム的な Excel の力を活用しましょう！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}