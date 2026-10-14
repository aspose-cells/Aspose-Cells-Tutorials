---
category: general
date: 2026-10-13
description: Aspose.Cells を使用して Excel を TXT として保存する方法を学びましょう。このガイドでは、Excel を TXT にエクスポートする方法、セルに値を書き込む方法、そして有効数字を設定する方法を、数ステップで解説します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: ja
lastmod: 2026-10-13
og_description: Aspose.CellsでExcelをTXTとして保存。ExcelをTXTにエクスポートし、セルに値を書き込み、桁数を設定する方法を、C#の数行のコードで学びましょう。
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: ExcelをTXTとして保存 – .NET開発者向けステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: C#でAspose.Cellsを使用してExcelをTXTとして保存する方法
url: /ja/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用した C# で Excel を TXT として保存する方法

Excel を **save Excel as TXT** したい場合、このチュートリアルでは 5 分未満で完了する全工程を示します。**export Excel to TXT**、**write value to cell**、そして **set significant digits** を設定して、テキストファイルに期待通りのデータが正確に含まれるようにします。

スプレッドシートを TXT としてエクスポートするのは、下流システムがプレーンテキスト入力のみを受け付ける場合や、ログを生成する必要がある場合、計算結果を人間が読みやすい形でダンプしたい場合に便利です。以下の例は Aspose.Cells v25.10 以降で動作し、任意の .NET 6+ ランタイム上で実行できます。

## 前提条件

* **Aspose.Cells for .NET** のライセンス版（無料トライアルはテストに使用可能）
* .NET 6 SDK 以降がインストールされていること。
* Visual Studio 2022、VS Code、Rider などの IDE。
* 基本的な C# の知識（高度な Excel 自動化の経験は不要）

以下のコマンドで Aspose.Cells の NuGet パッケージをインストールできます。

```bash
dotnet add package Aspose.Cells
```

## 手順 1: ワークブックを作成し、最初のワークシートにアクセスする (save excel as txt)

**save Excel as TXT** を行う際に最初に行うことは `Workbook` オブジェクトを作成することです。このオブジェクトはメモリ上の Excel ファイル全体を表します。

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Why this matters:** `Workbook` クラスはすべてのスプレッドシート操作のエントリーポイントです。新しいワークブックから開始することで、プレーンテキスト出力に影響を与える可能性のある隠れた書式設定を回避できます。

## 手順 2: 高精度の数値をセルに書き込む (write value to cell)

ここで **write value to cell** A1 に数値を書き込む必要があります。`PutValue` メソッドはデータ型を自動的に検出し、数値として格納します。

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Tip:** 後で文字列、日付、または数式を書き込む必要がある場合でも、同じ `PutValue` メソッドが機能します—適切な .NET 型を渡すだけです。

## 手順 3: エクスポートオプションを設定して必要な精度だけを保持する (set significant digits)

TXT ファイルにエクスポートする際、ファイルサイズを小さく保つか、下流の仕様に合わせるために桁数を制限したいことがよくあります。そのために `TxtSaveOptions` クラスは `SignificantDigits` プロパティを提供しています。

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Why you should set significant digits:** この設定がないと、Aspose.Cells は完全な倍精度の値を書き出すため、`12345.6789012345` のような長い文字列になることがあります。`SignificantDigits = 6` を設定すると出力が `12345.7` に切り詰められ、ほとんどのレポート要件に合致します。

## 手順 4: ワークブックを TXT ファイルとしてエクスポートする (export excel to txt)

最後に、先に設定したオプションを使用して `Workbook.Save` を呼び出すことで **export Excel to TXT** を実行します。

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

コードの実行が完了すると、`LimitedDigits.txt` に以下が含まれます。

```
12345.7
```

> **Result verification:** 任意のテキストエディタ（Notepad、VS Code など）でファイルを開き、6 桁の有効数字だけが含まれ、余分なカンマやタブ区切りがないことを確認してください。

## 完全な実行可能サンプル

以下は、コピーして貼り付けるだけで即座に実行できる、自己完結型のコンソールアプリケーションです。

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**各ブロックの説明**

| Block | Purpose |
|-------|---------|
| `using Aspose.Cells;` | `Workbook`、`Worksheet`、`TxtSaveOptions` に必要な Aspose.Cells 名前空間をインポートします。 |
| `Workbook workbook = new Workbook();` | メモリ上に空の Excel ワークブックをインスタンス化します。 |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 に倍精度数値を書き込みます。 |
| `TxtSaveOptions` | TXT エクスポート時の **set significant digits** 動作を設定します。 |
| `workbook.Save(..., txtOptions);` | **export excel to txt** 操作を実行し、プレーンテキストファイルを作成します。 |

## エッジケースと追加のヒント

| シナリオ | 対処方法 |
|----------|---------------|
| **Large worksheets** (多数の行/列) | Unicode が必要な場合は `txtOptions.Encoding = Encoding.UTF8` を使用し、メモリ使用量を抑えるために `Workbook.Save(Stream, txtOptions)` でストリーミング保存することを検討してください。 |
| **Custom delimiters** (カンマ区切り値) | `TxtSaveOptions` には `Separator` もあり、`','` に設定すると TXT 形式のままで CSV スタイルの出力が得られます。 |
| **Preserving formulas** | `txtOptions.ExportFormulas = true` を設定すると、計算結果ではなく数式テキストが書き込まれます。 |
| **Locale‑specific decimal separators** | ヨーロッパのロケール向けに `txtOptions.DecimalSeparator` を `','` に調整します。 |
| **Multiple worksheets** | `workbook.Worksheets` をループし、各シートごとに `Save` を呼び出し、ファイル名にシート名を付加します。 |

## よくある質問

**Q: `SignificantDigits` は丸めですか、それとも切り捨てですか？**  
A: 指定された有効数字の数に基づいて最も近い値に丸められ、出力はその精度で数学的に正確になります。

**Q: メモリストリームに直接エクスポートできますか？**  
A: はい。ファイルパスの代わりに `MemoryStream` インスタンスを使用します: `workbook.Save(stream, txtOptions);`。ファイルシステムに書き込まずに TXT コンテンツを返す必要がある Web API に便利です。

**Q: 元の書式（例: 日付）を保持したい場合はどうすればよいですか？**  
A: `txtOptions.ExportFormattedValues = true` を使用します。これにより、Aspose.Cells は生の値ではなくセルに表示されているテキストを書き込みます。

## 結論

これで、**save Excel as TXT** を行い、精度、書式、出力先を完全に制御する方法が分かりました。4 つの手順（ワークブックの作成、**write value to cell**、**set significant digits**、**export Excel to TXT**）に従うことで、プレーンテキストエクスポートを任意の .NET アプリケーションに組み込むことができます。

次に、**export spreadsheet as TXT with custom delimiters**、**convert Excel to CSV**、**use Aspose.Cells to generate JSON reports** などの関連トピックを探求してください。これらはすべて、本稿で示した基本概念に基づいており、プラットフォーム間のデータ交換に役立つ汎用的なツールキットを提供します。

コーディングを楽しんでください！

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Create New Workbook and Export Excel to TXT with Precision](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Create new workbook – Export Excel to TXT with Full Precision](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}