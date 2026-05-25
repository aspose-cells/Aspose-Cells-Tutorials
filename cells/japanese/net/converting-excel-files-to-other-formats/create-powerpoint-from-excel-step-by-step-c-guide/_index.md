---
category: general
date: 2026-05-04
description: Aspose.Cells for .NET を使用して Excel から PowerPoint を素早く作成 – Excel を PPTX
  に変換し、数分で Excel を PowerPoint にエクスポートする方法を学びましょう。
draft: false
keywords:
- create powerpoint from excel
- convert excel to pptx
- export excel to powerpoint
- how to convert excel
- excel sheet to ppt
language: ja
og_description: Aspose.Cells を使用して Excel から PowerPoint を作成します。このガイドでは、Excel を PPTX
  に変換する方法、Excel を PowerPoint にエクスポートする方法、そして一般的なエッジケースの処理方法を示します。
og_title: ExcelからPowerPointを作成 – 完全C#チュートリアル
tags:
- C#
- Aspose.Cells
- Office Automation
title: Excel から PowerPoint を作成する – ステップバイステップ C# ガイド
url: /ja/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create PowerPoint from Excel – Complete C# Tutorial

Excel から **PowerPoint を作成** したいけど、どこから始めればいいか分からないことはありませんか？ 同じ壁にぶつかる開発者は多いです。データが豊富なスプレッドシートを洗練されたスライドデッキに変換したいとき、悩むのは当然です。

朗報です！数行の C# と Aspose.Cells for .NET ライブラリさえあれば、**Excel を PPTX に変換** でき、チャート、テーブル、書式設定を保持したまま **Excel を PowerPoint にエクスポート** できます。

このチュートリアルでは、前提条件、インストール手順、完全なコード、エッジケースの対処法まで順を追って解説します。最後にはプレゼンテーション用の PowerPoint ファイルが手に入ります。

---

## What You’ll Need

始める前に以下を用意してください：

- **.NET 6.0**（またはそれ以降）— ライブラリは .NET Framework、.NET Core、.NET 5+ でも動作します。
- **Aspose.Cells for .NET** NuGet パッケージ — 唯一の外部依存関係です。
- C# と Visual Studio（またはお好みの IDE）の基本的な知識。
- PPTX に変換したい Excel ワークブック（`input.xlsx`）。

以上です。COM 相互運用や Office のインストールは不要です。

---

## Step 1: Install Aspose.Cells via NuGet

まず、プロジェクトに Aspose.Cells パッケージを追加します。Package Manager Console を開き、次のコマンドを実行してください。

```powershell
Install-Package Aspose.Cells
```

*Why this step?* Aspose.Cells は Excel ファイルの読み取りと画像やスライドへのレンダリングを自動化します。完全にオフラインで動作するため、Office がインストールされていないサーバーでも高速かつ信頼性の高い変換が可能です。

---

## Step 2: Load the Excel Workbook You Want to Convert

次に、ワークブックを開きます。ファイルパスが実際のファイルを指していることを確認してください。そうでないと `FileNotFoundException` が発生します。

```csharp
using Aspose.Cells;

// Load the workbook from disk
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

*Pro tip:* ストリーム（例：アップロードされたファイル）から読み込む場合は、ファイルパスの代わりに `MemoryStream` を `Workbook` コンストラクタに渡すことができます。

---

## Step 3: Configure the Conversion Options

Aspose.Cells では `ImageOrPrintOptions` を使って出力形式を指定します。`SaveFormat` を `SaveFormat.Pptx` に設定すると、PowerPoint ファイルが生成されます。

```csharp
// Prepare conversion options – tell Aspose we need a PPTX
ImageOrPrintOptions saveOptions = new ImageOrPrintOptions
{
    // The format we’re targeting
    SaveFormat = SaveFormat.Pptx,

    // Optional: control slide dimensions (default is 1024x768)
    // Width = 1280,
    // Height = 720,

    // Optional: include only the first sheet
    // OnePagePerSheet = true
};
```

*Why this matters:* `ImageOrPrintOptions` を調整することで、スライドサイズ、DPI、各ワークシートを別々のスライドにするかどうかなどを制御できます。企業のテンプレートに合わせたレイアウトが必要なときに便利です。

---

## Step 4: Save the Workbook as a PPTX Presentation

最後に、PowerPoint ファイルをディスクに書き出します。

```csharp
// Export the workbook as a PowerPoint presentation
workbook.Save(@"C:\MyProjects\ExcelToPpt\output.pptx", saveOptions);
```

問題なく実行できれば、元の Excel ファイルと同じフォルダーに `output.pptx` が作成されます。

---

## Step 5: Verify the Result (Optional but Recommended)

生成された PPTX をプログラム上または手動で開き、チャート、テーブル、書式が正しく保持されているか確認する習慣をつけましょう。

```csharp
using System.Diagnostics;

// Launch the newly created PowerPoint file (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\MyProjects\ExcelToPpt\output.pptx",
    UseShellExecute = true
});
```

*Edge case note:* Excel ワークブックにマクロ（`.xlsm`）が含まれていても、PPTX には転送されません。マクロ対応が必要な場合は、まず画像としてエクスポートしてから PowerPoint に埋め込むなど別の手法が必要です。

---

## Full Working Example

以下は完成した実行可能プログラムです。新しいコンソールアプリに貼り付け、パスを調整して **F5** キーで実行してください。

```csharp
// ---------------------------------------------------------------
// Complete C# program: Convert Excel to PowerPoint (PPTX)
// ---------------------------------------------------------------
using System;
using System.Diagnostics;
using Aspose.Cells;

namespace ExcelToPowerPoint
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the Excel workbook you want to convert
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // 2️⃣ Set up the conversion options – specify PPTX output
            ImageOrPrintOptions saveOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                // Uncomment to customize slide size
                // Width = 1280,
                // Height = 720,
                // OnePagePerSheet = true   // each sheet → one slide
            };

            // 3️⃣ Save the workbook as a PPTX presentation
            string outputPath = @"C:\MyProjects\ExcelToPpt\output.pptx";
            workbook.Save(outputPath, saveOptions);

            Console.WriteLine($"✅ Successfully created PowerPoint from Excel at: {outputPath}");

            // 4️⃣ (Optional) Open the generated PPTX to verify
            try
            {
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Could not open the file automatically: {ex.Message}");
            }
        }
    }
}
```

**Expected output:**  
プログラムを実行すると成功メッセージが表示され、PowerPoint がインストールされていれば `output.pptx` が自動的に開きます。各ワークシートは別々のスライドとして（`OnePagePerSheet = true` に設定した場合はシートごとに 1 スライド）表示され、チャートや条件付き書式、セルスタイルは元の Excel と同様に保持されます。

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *Can I convert only a specific sheet?* | Yes. Before calling `Save`, set `workbook.Worksheets.ActiveSheetIndex` to the sheet you need, or use `workbook.Worksheets["SheetName"]` and export that sheet only. |
| *What about large workbooks?* | Aspose.Cells streams data, so memory usage stays reasonable. For extremely large files, consider increasing the `MemorySetting` to `MemorySetting.MemoryPreference`. |
| *Do formulas stay live?* | No. The conversion renders the **current** values, not the formulas. If you need live data, export the sheet as an image first, then embed it in PowerPoint. |
| *Is the library free?* | Aspose.Cells offers a free trial with a watermark. For production use you’ll need a license—once applied, the watermark disappears and performance improves. |
| *Can I add a custom PowerPoint template?* | Absolutely. After saving the PPTX, you can open it with `Aspose.Slides` and apply a master slide or theme. |

---

## Pro Tips & Best Practices

- **License early:** Apply your Aspose.Cells license **before** loading the workbook to avoid the evaluation watermark.
- **Batch processing:** Wrap the conversion inside a `foreach` loop if you need to process multiple Excel files in one run.
- **Performance tuning:** Set `saveOptions.Dpi = 200` (default is 96) for sharper images on high‑resolution slides, but beware of larger file sizes.
- **Error handling:** Catch `FileFormatException` for corrupted Excel files and `InvalidOperationException` for unsupported features.

---

## Conclusion

You now have a solid, end‑to‑end solution to **create PowerPoint from Excel** using C#. By loading the workbook, configuring `ImageOrPrintOptions`, and calling `workbook.Save`, you can reliably **convert Excel to PPTX** and **export Excel to PowerPoint** with minimal code.  

From here you might explore adding a corporate slide master, automating batch conversions, or even merging the generated slides with other content using Aspose.Slides. The sky’s the limit when you combine Aspose’s Office APIs.

Got more questions about converting Excel files, handling macros, or integrating with SharePoint? Drop a comment below, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}