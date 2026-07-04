---
category: general
date: 2026-07-03
description: Aspose.Cells を使用して、編集可能なテキストボックス付きで Excel ファイルを PowerPoint にエクスポートする方法
  – XLSX を PPTX に変換するステップバイステップガイド
draft: false
keywords:
- how to export excel
- create powerpoint from excel
- editable text boxes
- convert xlsx to pptx
- presentation export options
language: ja
og_description: 編集可能なテキストボックス付きでExcelをPowerPointにエクスポートする方法。C# の PresentationExportOptions
  を使用して XLSX を PPTX に変換する方法を学びましょう。
og_title: ExcelをPowerPointにエクスポートする方法 – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  headline: How to Export Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export Excel files to PowerPoint with editable text boxes using
    Aspose.Cells – step‑by‑step guide for converting XLSX to PPTX.
  name: How to Export Excel to PowerPoint – Complete Guide
  steps:
  - name: Navigate to a slide that originated from a worksheet.
    text: Navigate to a slide that originated from a worksheet.
  - name: Click on a text box—notice you can edit the text directly.
    text: Click on a text box—notice you can edit the text directly.
  - name: Adjust the shape’s size or color; the changes persist.
    text: Adjust the shape’s size or color; the changes persist.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Office Automation
title: ExcelをPowerPointにエクスポートする方法 – 完全ガイド
url: /ja/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel を PowerPoint にエクスポートする方法 – 完全ガイド

Ever wondered **Excel をエクスポートする方法** data directly into a PowerPoint deck without losing editability? You’re not alone. In this tutorial we’ll show you a practical way to **create PowerPoint from Excel** while keeping text boxes and shapes fully editable.

We’ll walk through every line of code, explain why each setting matters, and finish with a PowerPoint file you can open and tweak right away. By the end, you’ll be able to **convert XLSX to PPTX** in a single method call, and you’ll understand how the **presentation export options** control the outcome.

## 必要なもの

- **.NET 6.0**（or any recent .NET version）をマシンにインストールしてください。  
- **Aspose.Cells for .NET** の **ライセンス**（無料トライアルでもテストは可能）。  
- C# の基本的な知識—特別なスキルは不要で、コンソールアプリや小さなライブラリを作成できれば十分です。  
- スライドデッキに変換したい Excel ワークブック（`input.xlsx`）。

以上です。余計なツールや COM インターロップは不要で、純粋なマネージドコードだけです。

![How to export excel to PowerPoint diagram](https://example.com/placeholder.png "Diagram showing the flow of how to export excel data into PowerPoint")

## 手順 1: Aspose.Cells のインストールとプロジェクトの設定

To **Excel をエクスポートする方法** you first need the library that makes it possible. Open a terminal in your project folder and run:

```bash
dotnet add package Aspose.Cells
```

This pulls the latest Aspose.Cells package from NuGet. The library bundles everything you need for **presentation export options**, so you won’t have to reference Office Interop assemblies.

> **プロのコツ:** .NET Framework を対象にする場合は、互換性の問題を避けるために適切な NuGet バージョン（例: `Aspose.Cells.NET`）を使用してください。

## 手順 2: Excel ワークブックの読み込み

Now that the library is in place, let’s load the source file. The `Workbook` class represents the whole Excel document.

```csharp
using Aspose.Cells;

// Step 2: Load the Excel workbook
Workbook workbook = new Workbook(@"C:\Data\input.xlsx");
```

*なぜ重要か:* ワークブックの読み込みは、**convert XLSX to PPTX** ワークフローの最初のステップです。`Workbook` オブジェクトはシート、チャート、セルの書式設定を保持しており、これらは後で PowerPoint オブジェクトにマッピングできます。

## 手順 3: Presentation Export Options の設定（編集可能なテキストボックス）

Here’s where the magic happens. By default, Aspose.Cells exports shapes as static images. To keep them **editable text boxes**, you must enable the right flag.

```csharp
// Step 3: Create presentation export options and enable editable shapes
PresentationExportOptions exportOptions = new PresentationExportOptions
{
    ExportEditableObjects = true // Makes text boxes and shapes editable in the PPTX
};
```

> **なぜ `ExportEditableObjects` を有効にするのか？**  
> このプロパティが `true` の場合、Aspose.Cells は各 Excel の図形を PowerPoint のネイティブな図形に変換します。つまり、生成された `.pptx` を PowerPoint で開き、テキストを編集したり、ボックスのサイズを変更したり、色を変えたりできるようになります。これは **create PowerPoint from Excel** で期待される動作そのものです。

## 手順 4: ワークブックを PowerPoint にエクスポート

With the workbook loaded and options configured, the final line saves the file as a PowerPoint presentation.

```csharp
// Step 4: Export the workbook to a PowerPoint file using the configured options
workbook.Save(@"C:\Data\output.pptx", SaveFormat.Pptx, exportOptions);
```

*結果として:* `output.pptx` ファイルには、デフォルトでシートごとに 1 枚のスライドが含まれます。各スライドは元のシートのレイアウトを反映し、Excel で配置したすべてのテキストボックスが PowerPoint では **editable text box** として扱われます。

## 手順 5: 結果を確認し、必要に応じて調整

Open `output.pptx` in Microsoft PowerPoint:

1. ワークシートから生成されたスライドへ移動します。  
2. テキストボックスをクリックすると、直接テキストを編集できることがわかります。  
3. 図形のサイズや色を調整すると、変更が保持されます。

If something looks off, consider these adjustments:

- **特定のシートだけをエクスポート:** 保存前に `workbook.Worksheets.RemoveAt(index)` を使用します。  
- **スライドレイアウトの制御:** `exportOptions.ExportAllSheetsAsSlide = false` に設定し、手動でスライドを追加します。  
- **チャートの書式を保持:** エクスポート前にシートにチャートを配置しておくと、自動的に PowerPoint のチャートに変換されます。

## よくある落とし穴と回避策

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| 図形が画像になる | `ExportEditableObjects` がデフォルト（`false`）のまま | Step 3 のように `ExportEditableObjects = true` を設定します。 |
| ワークシートが欠落 | `Save` が不要なシートを削除する前に呼び出された | エクスポート前に不要なシートを削除または非表示にします。 |
| ファイルサイズが大きい | 図形と一緒に高解像度画像が埋め込まれている | 必要に応じて `exportOptions.ImageResolution = 150` を使用し DPI を下げます。 |
| PowerPoint の互換性警告 | 古い Aspose.Cells バージョンを使用している | 最新の NuGet パッケージにアップグレードします（PPTX 2016+ をサポート）。 |

## 完全な動作例

Below is the complete program you can copy‑paste into a console app. It includes all steps, error handling, and comments.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // 1️⃣ Load the Excel workbook (convert XLSX to PPTX starts here)
                string inputPath = @"C:\Data\input.xlsx";
                Workbook workbook = new Workbook(inputPath);
                Console.WriteLine("Workbook loaded successfully.");

                // 2️⃣ Configure export options – make text boxes editable
                PresentationExportOptions exportOptions = new PresentationExportOptions
                {
                    ExportEditableObjects = true,
                    // Optional: tweak image resolution to keep file size reasonable
                    ImageResolution = 150
                };
                Console.WriteLine("Export options configured (editable text boxes enabled).");

                // 3️⃣ Save as PowerPoint
                string outputPath = @"C:\Data\output.pptx";
                workbook.Save(outputPath, SaveFormat.Pptx, exportOptions);
                Console.WriteLine($"File saved as PowerPoint: {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error during conversion: {ex.Message}");
                // In a real app you might log the stack trace or rethrow.
            }
        }
    }
}
```

**コンソールに期待される出力:**

```
Workbook loaded successfully.
Export options configured (editable text boxes enabled).
File saved as PowerPoint: C:\Data\output.pptx
```

生成された `output.pptx` を開くと、各ワークシートがスライドに変換され、Excel で追加したすべての図形が **editable text box** として即座に調整可能であることが確認できます。

## まとめ: Excel を迅速かつクリーンにエクスポートする方法

We’ve covered the entire **how to export excel** process—from installing Aspose.Cells, through configuring **presentation export options**, to finally **convert XLSX to PPTX** with fully editable content. The key takeaways are:

- `PresentationExportOptions.ExportEditableObjects = true` を使用して、図形を編集可能に保ちます。  
- `Workbook.Save` メソッドが主要な処理を行うため、COM インターロップは不要です。  
- オプション設定（画像解像度、シート選択など）を調整して結果を微調整できます。

## 次にやるべきことは？

If you enjoyed turning spreadsheets into slides, you might also want to explore:

- **Embedding charts** をネイティブな PowerPoint チャートとして埋め込む（`exportOptions.ExportChartAsShape = false`）。  
- **Applying a custom slide master** after export to match corporate branding.  
- **Automating batch conversions** for dozens of files using a simple `foreach` loop.  

These topics are built on the same fundamentals we just covered, so you’re already on solid ground.

---

問題が発生した場合や、このパターンを自分のプロジェクトで拡張した方法を共有したい場合は、遠慮なくコメントを残してください。コーディングを楽しみ、Excel と PowerPoint のシームレスな橋渡しを体験してください！

## 次に学ぶべきことは？

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose.Cells for .NET を使用して Excel を PowerPoint に変換する方法：完全ガイド](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Aspose.Cells .NET を使用して Excel にテキストボックスを追加・アクセスする方法 | ステップバイステップガイド](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [Aspose.Cells を使用して .NET で Excel ファイルをエクスポートする方法：包括的ガイド](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}