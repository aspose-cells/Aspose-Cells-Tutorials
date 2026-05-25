---
category: general
date: 2026-02-26
description: 埋め込みフォント付きでワークブックをPDFにエクスポートし、さらにC#でチャートをPowerPointにエクスポートします。ピボットテーブルのワークシートをコピーし、ワークブックをPPTXとして保存する方法を学びましょう。
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: ja
og_description: 埋め込みフォント付きでワークブックを PDF にエクスポートし、C# でチャートを PowerPoint にエクスポートします。ピボットテーブルをコピーして
  PPTX として保存する手順をステップバイステップでご案内します。
og_title: ワークブックをPDFにエクスポート – 完全C#ガイド
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: ワークブックをPDFにエクスポート – 完全C#ガイド
url: /ja/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

produce final output.

Be careful with bullet points: keep dash and spacing.

Also blockquote > **Pro tip:** etc. Translate "Pro tip" maybe keep as is? It's a phrase, but we can translate "Pro tip" to "プロのヒント". Keep bold formatting.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Workbook to PDF – Complete C# Guide

Excel がインストールされていないステークホルダーとレポートを共有する必要がある場合、ワークブックを PDF にエクスポートすることは一般的な要件です。このチュートリアルでは、**チャートを PowerPoint にエクスポート**する方法、**ピボットテーブルのワークシートをコピー**する方法、そしてフォントを埋め込んで PDF が画面上のデザインと全く同じになるようにする方法も紹介します。  

一部の PDF が元のレイアウトを失ったり、PowerPoint のスライドで図形が欠落したりすることに疑問を抱いたことはありませんか？その原因は多くの場合、エクスポート時のオプション設定が不足しているためです。このガイドを読み終える頃には、これらの問題をすべて解消する再利用可能な C# メソッドが手に入り、手動でのコピー＆ペーストや設定調整に悩む必要がなくなります。

## What You’ll Learn

- ワークブックの作成、Smart Marker 式の追加、そして処理方法。  
- データソースを壊さずに **ピボットテーブルのワークシートをコピー**する方法。  
- **チャート、図形、テキストボックスを PowerPoint プレゼンテーションにエクスポート**し、編集可能な状態を保つ方法。  
- PDF エクスポート時に **標準フォントを埋め込む**ことで、どのマシンでも同一の描画を実現する方法。  
- `save workbook as pptx` アプローチを使用して **ワークブックを PPTX として保存**する方法。  

これらはすべて、執筆時点での最新バージョン（23.11）の Aspose.Cells と Aspose.Slides .NET ライブラリで動作します。外部ツールやポストプロセススクリプトは不要で、純粋な C# だけです。

> **プロのヒント:** すでにプロジェクトで Aspose を使用している場合は、コードスニペットをそのまま貼り付けて使用できます。そうでない場合は、まず NuGet パッケージ `Aspose.Cells` と `Aspose.Slides` を追加してください。

## Prerequisites

- .NET 6.0 以降（コードは .NET Framework 4.7.2 でも動作します）。  
- Visual Studio 2022（またはお好みの IDE）。  
- NuGet 経由でインストールした Aspose.Cells .NET と Aspose.Slides .NET。  
- C# と Excel の概念（Smart Markers や PivotTables）に関する基本的な知識。

---

![ExcelブックをPDFにエクスポートする図](export-workbook-to-pdf.png "PDFとPPTXの出力を示すExcelブックのPDFエクスポートワークフロー")

## Export Workbook to PDF – Step‑by‑Step Implementation

以下は、実行可能な完全サンプルです。ワークブックを作成し、Smart Marker 式を注入、処理し、ピボットテーブルの範囲をコピーし、最後に PDF と PowerPoint の両方を保存します。

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### Why This Works

1. **Smart Marker processing** により、JSON や DataTable など任意のデータソースからループを書かずにワークブックを埋め込めます。  
2. **DetailSheetNewName** は部門ごとに別シートを作成し、部門別タブをすっきり整理します。  
3. **Copying the range** (`sourceRange.Copy`) はピボットテーブルの *キャッシュも含めて* 複製するため、コピーシートは元と同様に機能します。  
4. **PresentationOptions** の `ExportCharts`、`ExportShapes`、`ExportTextBoxes` により、Aspose はこれらのオブジェクトを PowerPoint のネイティブ要素としてレンダリングし、編集可能性を保持します。  
5. **PdfSaveOptions.EmbedStandardFonts** は、元フォントがインストールされていないマシンでも PDF が同一に表示されるようにします。

結果として生成されるのは `FinalReport.pdf` と `FinalPresentation.pptx` の 2 ファイルで、メール送信、アーカイブ、任意のビューアでの表示時に品質が失われません。

## Export Charts to PowerPoint (Save Workbook as PPTX)

レポートにチャートが含まれている場合、PowerPoint で編集可能にしたいことが多いでしょう。`PresentationOptions` クラスが鍵です。以下はチャートエクスポート部分だけを抜粋したコードです。

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**内部で何が起きているか？** Aspose は各 Excel チャートを PowerPoint のネイティブチャートに変換し、系列、軸タイトル、書式設定をすべて保持します。静的画像としてエクスポートするよりもはるかに優れており、受け手は後からデータポイントを調整できます。

## Copy Pivot Table Worksheet Without Losing Data

ピボットテーブルは、隠れたキャッシュに依存しているためエクスポート時に最も扱いが難しい部分です。シンプルな `Copy` メソッドが機能するのは、Aspose が可視範囲 **と** 基礎となるキャッシュオブジェクトの両方をコピーするからです。

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **注意:** 同一ブック内の新しいシートにピボットテーブルだけが必要な場合は、先述の `sourceRange.Copy` アプローチの方が軽量で、別ブックを作成する手間が省けます。

## Embed Fonts for PDF Export – Why It Matters

元フォントがインストールされていないマシンで PDF を開くと、文字がずれたり改行が変わったり、文字が消失したりします。`EmbedStandardFonts = true` を設定すると、Aspose は最も一般的なフォント（Arial、Times New Roman など）を PDF ストリームに直接埋め込みます。

カスタムフォントを使用している場合は、`PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll` に切り替えてください。例は以下の通りです。

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

これで受信者全員が、設計どおりのレイアウトを正確に閲覧できます—サプライズはありません。

## Full Working Example Recap

すべてをまとめると、先に示した完全プログラムは次の処理を行います。

1. **Creates** a workbook with Smart Marker placeholders.  
2. **Processes** the markers, generating a detail sheet named after the department.  
3. **Copies** a range that contains a pivot table to a new worksheet, preserving its functionality.  
4. **Exports** the workbook to PowerPoint, keeping charts, shapes, and text boxes editable.  
5. **Exports** the same workbook to PDF while embedding standard fonts for reliable rendering.

プログラムを実行し、生成されたファイルを開くと以下が確認できます。

- **PDF**: 鮮明なテーブル、埋め込まれたフォント、Excel ソースと同一のビジュアルスタイル。  
- **PowerPoint**: 編集可能なチャートで、PowerPoint 上で右クリック → *Edit Data* が可能。図形も完全に操作可能な状態です。

---

## Frequently Asked Questions (FAQ)

**Q: Does this work with .NET Core?**  
はい—Aspose.Cells と Aspose.Slides はクロスプラットフォームです。.NET 6 以降をターゲットにすれば、Windows、Linux、macOS で同じコードが動作します。

**Q: What if I need to export only a subset of sheets?**  
`Workbook.Save` に `SaveOptions` を使用し、`SheetNames` で出力シートを指定できます。例: `new PresentationOptions { SheetNames = new[] { "Copy" } }`.

**Q: Can I encrypt the PDF?**  
もちろん可能です。`Save` を呼び出す前に `PdfSaveOptions.EncryptionDetails` にパスワードを設定してください。

**Q: My pivot table uses an external data source—will copying break the link?**  
コピー操作はキャッシュを含みますが、外部接続自体は含みません。そのためピボットはオフラインで機能しますが、元データソースへの再更新は行われません。ライブ更新が必要な場合は、ソースデータも併せてエクスポートしてください。

---

## Next Steps & Related Topics

- **Dynamic Data Sources** – JSON や DataTable を Smart Markers に流し込み、リアルタイムレポートを作成する方法を学びましょう。  
- **Advanced PDF Styling** – Explore `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}