---
category: general
date: 2026-03-30
description: Aspose.Cells を使用した C# での区切り文字付き数値の書式設定方法を学びます。カスタム数値書式の設定、千位区切りの追加、小数点以下の書式設定、セルの書式設定方法が含まれます。
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: ja
og_description: C#で区切り文字を使用して数値をフォーマットする。このガイドでは、カスタム数値書式の設定、千位区切りの追加、小数点以下の書式設定、そして
  Aspose.Cells を使用したセルの書式設定方法を紹介します。
og_title: C#で区切り文字を使用した数値の書式設定 – Aspose.Cellsチュートリアル
tags:
- C#
- Aspose.Cells
- Number Formatting
title: C#で区切り文字付き数値のフォーマット – 完全な Aspose.Cells ガイド
url: /ja/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で区切り付き数値をフォーマット – 完全 Aspose.Cells ガイド

スプレッドシートで **区切り付き数値をフォーマット** したいと思ったことはありませんか？どの API 呼び出しを使えばいいか分からないことも多いでしょう。開発者はデータをエクスポートする際、千位区切りや小数点以下の桁数、カスタムパターンに常に頭を悩ませています。  

朗報です。Aspose.Cells を使えばとても簡単です。このチュートリアルでは、実際の例を通して **カスタム数値フォーマットを設定**、**千位区切りを追加**、**小数点以下をフォーマット**、そして **セルの出力を文字列としてフォーマットする方法** を解説します。最後まで読めば、任意の .NET プロジェクトにすぐ貼り付けて実行できるコードスニペットが手に入ります。

## What This Guide Covers

* 必要な NuGet パッケージとインストール方法  
* ワークブックを作成し、数値を書き込み、カスタムフォーマットを適用するステップバイステップのコード  
* `ExportTableOptions.ExportAsString` がフォーマット済みの値を取得する推奨手段である理由  
* 一般的な落とし穴 — `ExportAsString` を有効にし忘れたり、誤ったフォーマットマスクを使用したりするケース  
* 小数点以下の桁数や区切り文字のスタイルを変更したい場合のフォーマットマスクの調整方法  

外部ドキュメントへのリンクは不要です。必要な情報はすべてここにあります。さっそく始めましょう。

---

## Prerequisites

| 要件 | 理由 |
|-------------|--------|
| .NET 6.0 以降 | Aspose.Cells 23.10 以降は .NET Standard 2.0+ を対象としているため、.NET 6 が安全かつ最新です。 |
| Visual Studio 2022（または任意の C# IDE） | デバッグやパッケージ管理が簡単になります。 |
| Aspose.Cells for .NET NuGet パッケージ | `Workbook`、`Worksheet`、`ExportTableOptions` クラスを提供します。 |

You can install the package via the Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

That’s it—no extra DLLs, no COM interop, just a single NuGet reference.

---

## Step 1: Initialise a New Workbook (How to Format Cell)

The first thing we do is create a fresh `Workbook` instance. Think of it as an empty Excel file ready to receive data.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **なぜ重要か:** `Workbook` は Aspose.Cells のすべての操作のエントリーポイントです。最初のワークシート (`Worksheets[0]`) を取得することで、シート名を指定せずにクリーンなキャンバスを得られます。

---

## Step 2: Write a Numeric Value into the Target Cell

Next, we put a raw number into cell **A1**. The value itself isn’t formatted yet—it’s just a double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **プロのコツ:** 後で数値フォーマットを適用したい場合は `PutString` ではなく `PutValue` を使用してください。これにより基になるデータ型が保持され、Excel 互換の計算が可能になります。

---

## Step 3: Set Custom Number Format (Add Thousands Separator & Format Decimal Places)

Now comes the heart of the tutorial: defining a format mask that tells Aspose.Cells how to display the number. The mask `#,##0.00` does three things:

1. `#,##0` – 千位区切り（デフォルトはカンマ）を追加します。  
2. `.00` – 小数点以下をちょうど 2 桁に固定します。  

If you need a different number of decimals, just change the number of `0`s after the decimal point.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **`ExportAsString` を使用する理由:** デフォルトでは `ExportString` は生の値を返します。`ExportAsString = true` を設定すると、テキストに変換する前に API が `NumberFormat` マスクを適用します。レポートや JSON ペイロード、UI 表示などで正確な文字列表現が必要な場合に必須です。

---

## Step 4: Export the Formatted Text (How to Format Cell)

With the options ready, we call `ExportString` on the same cell. The method respects the mask we just defined and hands back a nicely formatted string.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Running the program prints **`12,345.68`** to the console—exactly the format we asked for.

> **エッジケース:** 元の数値に小数点以下が 2 桁以上ある場合、マスクは四捨五入します。切り捨てが必要な場合は、`PutValue` を呼び出す前に `Math.Truncate` で事前に処理してください。

---

## Step 5: Tweaking the Format – Common Variations

### 5.1 Change Decimal Precision

Want three decimal places? Just replace the mask:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Use a Different Thousands Separator

Some locales prefer a space or a period. You can embed the character directly:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Or rely on the workbook’s culture settings:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Prefix or Suffix (Currency, Percent)

Add a dollar sign or a percent sign right in the mask:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **注意:** マスクは大文字小文字を区別します。`$` と `%` はリテラルシンボルであり、基になる数値には影響しません。

---

## Step 6: Full Working Example (Copy‑Paste Ready)

Below is the complete program you can copy into a new console app. It includes all the steps, comments, and the final output verification.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Run the program (`dotnet run` from the terminal or press F5 in Visual Studio) and you’ll see the formatted number printed exactly as shown.

---

## Frequently Asked Questions (FAQ)

**Q: 旧バージョンの Excel でも動作しますか？**  
A: はい。フォーマットマスクは Excel のネイティブな数値書式構文に従うため、`#,##0.00` を理解できるすべてのバージョンで同じ文字列が表示されます。

**Q: 複数セルの範囲をフォーマットしたい場合は？**  
A: 対象範囲をループして各セルに同じ `ExportTableOptions` を適用するか、範囲に対して `Style.Custom` プロパティを設定し、最後に単一セルで `ExportString` を呼び出します。

**Q: これらのフォーマットを適用したまま CSV に直接エクスポートできますか？**  
A: もちろん可能です。各セルにフォーマットを設定した後、`Workbook.Save("output.csv", SaveFormat.CSV);` を使用してください。Aspose.Cells は CSV 生成時にセルの `Style` を尊重します。

## Conclusion

ここでは Aspose.Cells を使用して C# で **区切り付き数値をフォーマット** する方法を示しました。**カスタム数値フォーマットの設定**、**千位区切りの追加**、**小数点以下のフォーマット**、そして文字列エクスポートのための **セルのフォーマット方法** まで網羅しています。コードは完全に自己完結しており、.NET 6+ で動作し、任意のロケールや精度要件に合わせて調整可能です。

次に検討できること:

* 日付や時刻にも同様の手法を適用する (`NumberFormat = "dd‑MMM‑yyyy"`)。  
* 列ごとに異なるマスクが必要な大量エクスポートを自動化する。  
* Aspose.Words を使ってフォーマット済み文字列を PDF レポートに統合する。

ぜひ試してみてください。そうすればチーム内でスプレッドシートのフォーマット担当者としてすぐに認められるでしょう。コーディングを楽しんで！   (Image: ![Aspose.Cells で区切り付き数値が表示されたスクリーンショット](image-placeholder.png){alt="Aspose.Cells の出力で区切り付き数値が表示されたスクリーンショット"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}