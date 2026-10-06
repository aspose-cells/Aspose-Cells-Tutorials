---
category: general
date: 2026-03-22
description: ExcelをPowerPointにエクスポートする方法、印刷範囲を設定する方法、編集可能なグラフやOLEオブジェクトを含むPPTXとしてExcelを保存する方法を、数ステップで学びましょう。
draft: false
keywords:
- export excel to powerpoint
- set print area excel
- save excel as pptx
- editable charts PowerPoint
- OLE objects export
language: ja
og_description: Excel を PowerPoint にすばやくエクスポートします。このチュートリアルでは、Excel の印刷範囲の設定方法と、編集可能なチャートや
  OLE オブジェクトを含む PPTX として Excel を保存する方法を紹介します。
og_title: ExcelからPowerPointへエクスポート – 完全なC#ガイド
tags:
- Aspose.Cells
- C#
- Office Automation
title: Excel から PowerPoint へエクスポート – 完全 C# ガイド
url: /ja/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel を PowerPoint にエクスポート – 完全 C# ガイド

**Excel を PowerPoint にエクスポート**したいですか？ここが正解です。週次の営業デッキを作成する場合でも、レポートパイプラインを自動化する場合でも、Excel のワークシートを PowerPoint のスライドデッキに変換すれば、コピー＆ペースト作業に費やす時間を何時間も削減できます。  

このチュートリアルでは、**export excel to powerpoint** だけでなく、**set print area Excel** と **save excel as pptx** の方法も示すハンズオン例を通して、スライド上のチャートや OLE オブジェクトが完全に編集可能な状態で保持される手順を解説します。最後まで実行すれば、手動で調整することなくプロフェッショナルな `.pptx` ファイルを生成できる C# プログラムが手に入ります。

## 必要な環境

- **.NET 6+**（最近の .NET ランタイムであればどれでも可；コードは C# 10 構文を使用）
- **Aspose.Cells for .NET** – エクスポートを実現するライブラリ。NuGet から取得できます（`Install-Package Aspose.Cells`）。
- 少なくとも 1 つのチャートまたは OLE オブジェクトを含む Excel ワークブック（サンプルファイル `ChartAndOle.xlsx` をコードで使用）。
- お好みの IDE（Visual Studio、Rider、VS Code など）。

以上です。COM インタープロや Office のインストールは不要です。  

> **なぜライブラリを使うのか？**  
> 組み込みの Office Interop は脆弱で、サーバーに Office が必要になり、ベクターベースで編集可能な形状が欲しいときにラスタ画像が生成されがちです。Aspose.Cells は重い処理をすべて担い、PowerPoint でもすべてを編集可能な状態で保持します。

---

## Step 1: Load the Excel Workbook  

まずソースファイルをメモリに読み込みます。`Workbook` クラスは Excel ファイル全体を抽象化し、ワークシート、チャート、OLE オブジェクトへのアクセスを提供します。

```csharp
using Aspose.Cells;

try
{
    // Load the Excel file that contains the chart and OLE object.
    // Adjust the path to point to your own workbook.
    Workbook workbook = new Workbook(@"C:\MyProjects\ChartAndOle.xlsx");
}
catch (Exception ex)
{
    Console.WriteLine($"Failed to load workbook: {ex.Message}");
    return;
}
```

**重要なポイント:** ワークブックの読み込みは全工程の基盤です。パスが間違っている、またはファイルが破損していると、以降のパイプラインは実行されません。`try…catch` ブロックにより、クラッシュではなくフレンドリーなエラーメッセージが表示されます。

---

## Step 2: Set the Print Area in Excel  

エクスポート前に、出力範囲を特定の領域に限定したいことが多いです。ここで **set print area excel** が活躍します。印刷領域を設定することで、Aspose.Cells に対し、どのセル（および関連オブジェクト）をスライドに表示すべきかを正確に指示できます。

```csharp
// Assuming we want to export only the range A1:H30 on the first worksheet.
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:H30";
```

> **プロのコツ:** 複数のワークシートがある場合は、エクスポート対象の各シートに対して `PrintArea` の割り当てを繰り返してください。印刷領域を設定しないとシート全体がエクスポートされ、PowerPoint ファイルが肥大化します。

---

## Step 3: Configure Export Options – Keep Charts & OLE Editable  

Aspose.Cells には豊富な `ImageOrPrintOptions` オブジェクトがあります。`ExportChartObjects` と `ExportOleObjects` を切り替えることで、チャートのベクタ特性と OLE オブジェクトのライブ編集性を保持します（埋め込み Word 文書や PDF など）。

```csharp
ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,   // We want a PPTX, not a PNG or PDF.
    ExportChartObjects = true,      // Charts stay editable in PowerPoint.
    ExportOleObjects = true         // OLE objects remain live (you can double‑click to edit).
};
```

**内部で何が起きているか？**  
`ExportChartObjects` が `true` の場合、Aspose はチャートを PowerPoint のネイティブチャート形状に変換し、系列、軸、書式設定を保持します。`ExportOleObjects` を有効にすると、埋め込みオブジェクトは OLE フレームとして挿入され、PowerPoint でダブルクリックすると元のアプリケーション（Word、Excel など）が開き、直接編集できます。

---

## Step 4: Save the Worksheet as an Editable PowerPoint File  

ここまでの設定をまとめて実行します。`Save` メソッドは、構成したオプションを使用して `.pptx` ファイルを書き出します。結果として、各ワークシートが 1 枚のスライド（印刷領域が複数ページに跨る場合は複数スライド）になります。

```csharp
// Save the first worksheet as an editable PowerPoint presentation.
workbook.Save(@"C:\MyProjects\EditableChartOle.pptx", pptExportOptions);
Console.WriteLine("Export completed! Check EditableChartOle.pptx.");
```

### 期待される結果

- **ファイルの場所:** `C:\MyProjects\EditableChartOle.pptx`
- **内容:**  
  - Excel で表示されている範囲 `A1:H30` がそのままスライドに表示されます。  
  - すべてのチャートは PowerPoint のチャートオブジェクトとして保持され、棒グラフをクリックしてデータを編集できます。  
  - OLE オブジェクト（例: 埋め込み Word 文書）はスライド上から直接開いて編集可能です。

PowerPoint で PPTX を開くと、ラスタ画像ではなく完全に編集可能なコンポーネントだけが表示されたクリーンなスライドが確認できるはずです。

---

## Edge Cases & Variations  

### Multiple Worksheets → Multiple Slides  
各ワークシートを個別のスライドにしたい場合は、`workbook.Worksheets` をループし、特定のシートインデックスを対象とした `SheetToImageOptions` を指定して `Save` を呼び出します。Aspose が自動的にイテレーションごとに新しいスライドを生成します。

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    ImageOrPrintOptions opts = new ImageOrPrintOptions
    {
        SaveFormat = SaveFormat.Pptx,
        ExportChartObjects = true,
        ExportOleObjects = true,
        OnePagePerSheet = true   // Ensures each sheet starts on a new slide.
    };
    workbook.Save($"Sheet{i + 1}.pptx", opts);
}
```

### Large Ranges & Performance  
非常に大きな印刷領域（例: `A1:Z1000`）をエクスポートするとメモリ使用量が増加します。対策としては以下を検討してください。  
- 範囲を小さなチャンクに分割し、別々のスライドとしてエクスポートする。  
- `OutOfMemoryException` が発生した場合は、`WorkbookSettings` の `MemorySetting` を増やす。

### Compatibility Concerns  
生成された PPTX は PowerPoint 2016 以降で動作します。古いバージョンでも開くことは可能ですが、一部高度なチャート機能が失われる可能性があります。広く配布する場合は、対象となる Office バージョンで必ずテストしてください。

---

## Full Working Example (Copy‑Paste Ready)

```csharp
// ---------------------------------------------------------------
// Export Excel to PowerPoint – Complete C# Example
// ---------------------------------------------------------------

using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook.
            string excelPath = @"C:\MyProjects\ChartAndOle.xlsx";
            Workbook workbook;
            try
            {
                workbook = new Workbook(excelPath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error loading Excel file: {ex.Message}");
                return;
            }

            // 2️⃣ Set the print area (set print area excel).
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:H30";

            // 3️⃣ Configure export options – keep charts & OLE objects editable.
            ImageOrPrintOptions pptExportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartObjects = true,
                ExportOleObjects = true
            };

            // 4️⃣ Save as PPTX (save excel as pptx).
            string pptxPath = @"C:\MyProjects\EditableChartOle.pptx";
            try
            {
                workbook.Save(pptxPath, pptExportOptions);
                Console.WriteLine($"Success! PPTX created at: {pptxPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to save PPTX: {ex.Message}");
            }
        }
    }
}
```

> **ヒント:** ハードコードされたパスは設定値やコマンドライン引数に置き換えると、より柔軟なツールになります。

---

## Frequently Asked Questions  

**Q: 周囲のセルを除いてチャートだけをエクスポートできますか？**  
A: はい。`ExportChartObjects` のみを使用し、印刷領域をチャートの境界範囲に設定すれば、チャートだけがスライドの中心に表示されます。

**Q: ワークブックにマクロが含まれている場合はどうなりますか？**  
A: Aspose.Cells はエクスポート時に VBA マクロを無視します。PowerPoint でマクロ機能が必要な場合は、PowerPoint VBA やアドインで再実装する必要があります。

**Q: Linux/macOS でも動作しますか？**  
A: 完全に対応しています。Aspose.Cells は純粋な .NET ライブラリなので、.NET ランタイムさえあればクロスプラットフォームで実行可能です。

---

## Conclusion  

これで **export Excel to PowerPoint** と同時に **set print area excel** と **save excel as pptx** を行い、チャートや OLE オブジェクトを完全に編集可能な状態で保持する方法を習得しました。重要な手順は、ワークブックの読み込み、印刷領域の設定、`ImageOrPrintOptions` の構成、そして PPTX の保存です。  

ここからさらにできること:  
- 複数のワークシートを 1 つのデッキにエクスポート  
- カスタムスライドタイトルやノートをプログラムで追加  
- PPTX を PDF に変換して配布（`SaveFormat.Pdf` を使用）  

コードを実行して印刷領域を調整すれば、Excel のデータが魔法のように PowerPoint に現れます—手動のコピー＆ペーストは不要です。問題が発生したら Aspose.Cells のドキュメントを確認するか、下のコメント欄に質問を残してください。Happy coding!  

![Diagram showing export excel to powerpoint workflow](/images/export-excel-to-powerpoint.png "export excel to powerpoint workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}