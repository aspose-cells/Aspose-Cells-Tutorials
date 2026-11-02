---
category: general
date: 2026-05-30
description: C# を使用して Excel のテキストボックスのフォントサイズを変更する。ステップバイステップのコードで、Excel のテキストボックスのフォントを素早く変更する方法を学びましょう。
draft: false
keywords:
- change textbox font size
- modify excel textbox font
language: ja
og_description: C# を使用して Excel のテキストボックスのフォントサイズを変更する。このガイドでは、Excel のテキストボックスのフォントを安全かつ効率的に変更する方法を示します。
og_title: C#でExcelのテキストボックスのフォントサイズを変更する – 完全チュートリアル
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  headline: Change Textbox Font Size in Excel with C# – Complete Guide
  type: TechArticle
- description: Change textbox font size in Excel using C#. Learn how to modify excel
    textbox font quickly with step‑by‑step code.
  name: Change Textbox Font Size in Excel with C# – Complete Guide
  steps:
  - name: Why this matters
    text: Opening the workbook via COM gives us a live object model—meaning any change
      we make reflects instantly in the file. Setting `Visible = false` speeds things
      up and avoids popping windows during automation.
  - name: Why we use `TextFrame2`
    text: '`TextFrame2` is the newer object model introduced with Office 2007. It
      supports advanced typographic features and is generally more reliable than the
      older `TextFrame`. Using it ensures our **change textbox font size** operation
      works across modern Excel versions.'
  - name: 1. Change *all* textboxes on a sheet
    text: '```csharp foreach (Excel.Shape s in xlWorksheet.Shapes) { if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
      { var tr = s.TextFrame2.TextRange; tr.Font.Name = fontName; tr.Font.Size = newSize;
      } } ```'
  - name: 2. Identify a textbox by its **Name** instead of index
    text: 'If you gave your textbox a meaningful name (e.g., “TitleBox”), you can
      fetch it directly:'
  type: HowTo
tags:
- Excel Interop
- C#
- Office Automation
title: C#でExcelのテキストボックスのフォントサイズを変更する – 完全ガイド
url: /ja/net/excel-shape-text-modifications/change-textbox-font-size-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Excel のテキストボックスのフォントサイズを変更する – 完全ガイド

C# で Excel のワークシート内の **テキストボックスのフォントサイズを変更** したいですか？ここが正解です。レポートを生成したり、ダッシュボードを作成したり、テンプレートを微調整したりする際に、テキストボックスの外観を調整するだけで、スプレッドシートが格段にプロフェッショナルに見えます。

このチュートリアルでは、サイズだけでなく **excel テキストボックスのフォントを変更** も行います—フォントファミリーや太字、さらには複数のシェイプの処理も考慮します。最後までに、ブックを開くところから COM オブジェクトのクリーンアップまで、プロセスのすべての段階に対応した実行可能なコードスニペットが手に入ります。余計な説明はなく、すぐにプロジェクトに組み込める実用的なコードだけです。

## 前提条件 — 必要なもの

本題に入る前に、以下がマシンにインストールされていることを確認してください。

| 要件 | 重要な理由 |
|------|------------|
| **.NET 6+** (or .NET Framework 4.7.2+) | C# コンパイラとランタイムを提供します。 |
| **Microsoft.Office.Interop.Excel** NuGet パッケージ | Excel とやり取りするために必要な COM インタープロタイプを提供します。 |
| **Excel installed** (any recent version) | Interop レイヤーは Office アプリがインストールされている場合にのみ機能します。 |
| **Basic C# knowledge** | 内容を簡単に追えるようになりますが、各行を丁寧に説明します。 |

これらのいずれかが欠けている場合は、今すぐインストールしてください。ガイドの残りはそれらが揃っていることを前提としています。

## 手順 1: プロジェクトの設定と名前空間のインポート

まず最初に、新しいコンソールアプリを作成（または既存のものに統合）し、Interop 名前空間をインポートします。

```csharp
using System;
using Excel = Microsoft.Office.Interop.Excel;

namespace ExcelTextboxDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll call the helper method that does the heavy lifting.
            ChangeTextboxFontSize(@"C:\Temp\Sample.xlsx", "Sheet1", 0, 14, "Calibri");
        }
    }
}
```

> **Pro tip:** .NET 6+ を対象にしている場合は、`dotnet add package Microsoft.Office.Interop.Excel` で `Microsoft.Office.Interop.Excel` パッケージを追加してください。これにより `Excel` エイリアスが正しく解決されます。

## 手順 2: ワークブックを開き、対象のワークシートを取得

次に、Excel を起動し、ファイルを開き、テキストボックスが配置されているシートを指定する必要があります。これを `try/finally` ブロックでラップすることで、エラーが発生しても COM オブジェクトが確実に解放されます。

```csharp
static void ChangeTextboxFontSize(string workbookPath,
                                  string sheetName,
                                  int textboxIndex,
                                  double newSize,
                                  string fontName)
{
    Excel.Application xlApp = null;
    Excel.Workbook xlWorkbook = null;
    Excel.Worksheet xlWorksheet = null;

    try
    {
        xlApp = new Excel.Application
        {
            // Keep Excel hidden; set to true if you want to watch the changes.
            Visible = false,
            DisplayAlerts = false
        };

        xlWorkbook = xlApp.Workbooks.Open(workbookPath);
        xlWorksheet = xlWorkbook.Worksheets[sheetName] as Excel.Worksheet;
        if (xlWorksheet == null)
            throw new ArgumentException($"Worksheet '{sheetName}' not found.");
```

### 重要な理由

COM 経由でワークブックを開くとライブオブジェクトモデルが取得でき、変更は即座にファイルに反映されます。`Visible = false` を設定すると処理が高速化され、オートメーション中にウィンドウがポップアップするのを防げます。

## 手順 3: テキストボックスのシェイプを取得

Excel ではテキストボックスは `Shapes` コレクション内の `Shape` オブジェクトとして扱われ、専用の `TextBox` コレクションは存在しません。そのため、以下のコードはオンラインで見たスニペットとは少し異なる形になっています。

```csharp
        // Excel stores all drawing objects (including textboxes) in the Shapes collection.
        Excel.Shapes shapes = xlWorksheet.Shapes;

        // Guard against an out‑of‑range index.
        if (textboxIndex < 0 || textboxIndex >= shapes.Count)
            throw new IndexOutOfRangeException("Textbox index is out of range.");

        // Grab the specific shape; we assume it’s a textbox.
        Excel.Shape textboxShape = shapes.Item(textboxIndex + 1); // COM collections are 1‑based.
        if (!textboxShape.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
            throw new InvalidOperationException("Selected shape is not a textbox.");
```

> **Watch out:** `Shapes` コレクションは 1 ベースなので、渡す zero‑based の `textboxIndex` に `+1` を加えます。これを忘れると “index out of range” エラーが発生し、デバッグが困難になります。

## 手順 4: テキストボックスのフォントサイズ（と名前）を変更

ここでいよいよ **テキストボックスのフォントサイズを変更** します。`TextFrame2` プロパティを使用すると、`Font.Name` や `Font.Size` などのリッチテキスト書式設定オプションにアクセスできます。

```csharp
        // Access the text range inside the textbox.
        Excel.TextRange2 textRange = textboxShape.TextFrame2.TextRange;

        // Change the font name – this also “modifies excel textbox font”.
        textRange.Font.Name = fontName;

        // Change the font size – the core of our tutorial.
        textRange.Font.Size = newSize;

        // Optional: make the text bold for extra emphasis.
        // textRange.Font.Bold = Microsoft.Office.Core.MsoTriState.msoTrue;
```

### `TextFrame2` を使用する理由

`TextFrame2` は Office 2007 で導入された新しいオブジェクトモデルです。高度な組版機能をサポートし、従来の `TextFrame` よりも信頼性が高いです。これを使用することで、**テキストボックスのフォントサイズを変更** 操作が最新の Excel バージョンでも動作することが保証されます。

## 手順 5: 保存、クリーンアップ、検証

フォントを調整した後は、変更を保存し、すべての COM 参照を解放する必要があります。クリーンアップを省略すると、バックグラウンドに Excel プロセスが残ってしまうことがあります。

```csharp
        // Save the workbook – you can also use SaveAs to create a copy.
        xlWorkbook.Save();

        Console.WriteLine($"Successfully changed textbox font size to {newSize} pt and font to '{fontName}'.");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error: {ex.Message}");
    }
    finally
    {
        // Release COM objects in reverse order of creation.
        if (xlWorksheet != null) System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorksheet);
        if (xlWorkbook != null)
        {
            xlWorkbook.Close(false);
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlWorkbook);
        }
        if (xlApp != null)
        {
            xlApp.Quit();
            System.Runtime.InteropServices.Marshal.ReleaseComObject(xlApp);
        }

        // Force garbage collection to clean up any remaining RCWs.
        GC.Collect();
        GC.WaitForPendingFinalizers();
    }
}
```

> **Pro tip:** 多数のワークシートで **excel テキストボックスのフォントを変更** 必要がある場合は、内部ロジックを `Workbook.Worksheets` を反復するループでラップしてください。各シートごとに `textboxIndex` をリセットすることを忘れないでください。

## エッジケースの処理 — 複数のテキストボックスとシェイプが見つからない場合

実務で使用されるスプレッドシートは、たいてい1つだけのテキストボックスではありません。以下に、メソッド全体を書き直すことなく採用できる2つの簡単な戦略を示します。

### 1. シート上の *すべて* のテキストボックスを変更

```csharp
foreach (Excel.Shape s in xlWorksheet.Shapes)
{
    if (s.Type.HasFlag(Excel.MsoShapeType.msoTextBox))
    {
        var tr = s.TextFrame2.TextRange;
        tr.Font.Name = fontName;
        tr.Font.Size = newSize;
    }
}
```

### 2. インデックスではなく **Name** でテキストボックスを特定

テキストボックスに意味のある名前（例: “TitleBox”）を付けている場合、直接取得できます。

```csharp
Excel.Shape namedBox = xlWorksheet.Shapes.Item("TitleBox");
namedBox.TextFrame2.TextRange.Font.Size = newSize;
```

どちらのアプローチも、ブックの構造に関係なく、**excel テキストボックスのフォントを変更** を正確に行えます。

## ビジュアル概要（オプション）

簡単なビジュアルヒントが欲しい場合は、以下の図をイメージしてください。

![Excel ワークシートでハイライトされたテキストボックスを示すスクリーンショット – テキストボックスのフォントサイズを変更する方法のデモ](change-textbox-font-size.png)

*Alt text:* *Excel でテキストボックスのフォントサイズを変更 – ハイライトされたテキストボックスがフォント変更の準備ができています。*

## 完全な動作例

すべてをまとめると、以下の単一ファイルをコンソールプロジェクトにコピー＆ペーストしてすぐに実行できます（ファイルパスとシート名を更新するだけです）。



## 次に学ぶべきこと

- [Excel のフォントサイズを変更する](/cells/english/net/working-with-fonts-in-excel/changing-font-size/)
- [Aspose.Cells .NET を使用して Excel のセルのフォントサイズをカスタマイズする方法 | 完全ガイド](/cells/english/net/formatting/customize-font-size-excel-aspose-cells-dotnet/)
- [Aspose.Cells for .NET を使用して Excel のフォントスタイルを設定する方法（ステップバイステップガイド）](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}