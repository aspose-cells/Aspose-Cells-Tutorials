---
category: general
date: 2026-10-01
description: C#でExcelブックを作成し、カスタム数値書式を適用、セルの小数点以下桁数を設定、XLSXとして保存する方法を、ステップバイステップの完全ガイドで学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: ja
lastmod: 2026-10-01
og_description: C#でカスタム数値書式を使用してExcelブックを作成し、セルの小数点以下の桁数を設定し、XLSXとして保存します。正確な数値出力のためにこの完全ガイドに従ってください。
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: C#でExcelブックを作成 – カスタム数値形式とXLSXエクスポート
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: C#でカスタム数値書式を使用してExcelブックを作成する方法
url: /ja/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Excel ワークブックを作成し、カスタム数値書式を設定する方法

**C# で Excel ワークブックを作成**し、数値を希望通りに表示したい場合は、このガイドに従って数ステップで実装できます。カスタム数値書式の適用、セルの小数点桁数設定、そして最終的に **xlsx としてワークブックを保存** する方法を学びます。

数値データを扱う際は、精度と可読性のバランスを取ることが重要です。このチュートリアルを終える頃には、表示桁数を特定の有効数字に制限しつつ、ファイル内の元の値は保持する再利用可能なパターンが手に入ります。外部スクリプトは不要で、C# と Aspose.Cells ライブラリだけで完結します。

## 前提条件

開始する前に、以下がインストールされていることを確認してください。

* .NET 6.0 SDK 以降  
* Visual Studio 2022（または任意の C# IDE）  
* **Aspose.Cells for .NET** NuGet パッケージ (`Install-Package Aspose.Cells`) – 本チュートリアルの例で使用する `Workbook`、`Worksheet`、`ExportTableOptions` クラスを提供します。  

これらの要件は最小限です。同じコードは .NET Core、.NET Framework、さらには Azure Functions でも動作します。

## 手順 1: Excel ワークブック C# – ファイルの初期化

最初の操作は新しい `Workbook` オブジェクトをインスタンス化することです。このオブジェクトはメモリ上の Excel ファイル全体を表し、デフォルトのワークシートが自動的に含まれます。

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**重要ポイント:**  
ワークブックを最初に作成しておくと、クリーンなキャンバスが得られます。デフォルトのワークシート (`Worksheets[0]`) はデータ入力の準備ができているため、シナリオで複数タブが必要でない限り新しいシートを追加する必要はありません。

## 手順 2: 数値をセルに書き込む

サンプル数値をセル **A1** に入力します。使用する値 (`123.456789`) は、最終的に表示したい小数点以下の桁数より多く含んでいるため、後で丸め処理をデモできます。

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**ヒント:** `PutValue` はデータ型を自動検出するので、数値を文字列に変換する必要はありません。

## 手順 3: カスタム数値書式を適用 – 表示小数点数の制限

Excel が数値をどのように表示するかを制御するために、**カスタム数値書式** を持つ `Style` を作成します。パターン `"0.######"` は最大で小数点以下 6 桁まで表示し、末尾のゼロは省略します。

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**仕組み:**  
書式文字列は Excel のカスタム書式構文に従います。`0` は必ず桁を表示し、`#` は有効な桁がある場合にのみ表示します。これらを組み合わせることで、元の精度を保持しつつ柔軟な表示が可能になります。

## 手順 4: セルの小数点桁数を設定 – ExportTableOptions を使用

エクスポート時に **セルの小数点桁数を設定** したい場合（例: DataTable へ変換する際）、Aspose.Cells では **有効数字** の数を指定できます。この手順により、エクスポートされた CSV や DataTable がワークブックで適用した丸めルールを尊重します。

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**`SignificantDigits` を使う理由:**  
固定小数点数とは異なり、有効数字は数値の桁数全体を保ちつつ精度だけを制限します。これは分析者がデータを要約する際に期待する挙動です。

## 手順 5: ワークシートデータをエクスポートし、**xlsx としてワークブックを保存**

最後にデータをエクスポート（DataTable が必要な場合）し、ワークブックをディスクに保存します。`ExportDataTable` 呼び出しは設定した `ExportTableOptions` を考慮し、`workbook.Save` が標準的な XLSX ファイルを書き出します。

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**期待結果:**  
Excel で *SigDigits.xlsx* を開くと、セル **A1** に `123.5` と表示されます。内部値は `123.456789` のままですが、表示は 4 桁の有効数字ルールに従います。シートを DataTable にエクスポートした場合も、テーブル内の値は `123.5` に丸められます。

---

## 追加セルへのカスタム数値書式の適用

単一セルではなく範囲全体に書式を適用したい場合は、`Style` オブジェクトを再利用します。

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**プロのコツ:** スタイルオブジェクトを再利用するとメモリ使用量が削減され、シート全体で一貫した書式が保証されます。

## C# で Excel の数値書式を設定する一般的なバリエーション

| シナリオ | 書式文字列 | 結果 |
|----------|---------------|--------|
| 小数点以下 2 桁固定 | `"0.00"` | `123.46` |
| 通貨（米国） | `"$#,##0.00"` | `$123.46` |
| 小数点以下 1 桁のパーセンテージ | `"0.0%"` | `12,346.0%` |
| 科学技術表記 | `"0.00E+00"` | `1.23E+02` |

報告要件に合ったパターンを選択してください。すべてのパターンは前述の `Style.Custom` プロパティと互換性があります。

## ユーザー入力に基づくセル小数点桁数の動的設定

コンパイル時に精度が決まっていないケースがあります。実行時に書式文字列を組み立てることができます。

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**エッジケース:** `decimals` が 0 の場合、書式は `"0"`（整数表示）になります。書式文字列が不正にならないよう、必ずユーザー入力を検証してください。

## XLSX としてワークブックを保存するベストプラクティス

* **絶対パス** を使用して既知のディレクトリに書き込む（例: `Path.Combine(Environment.CurrentDirectory, "output.xlsx")`）。  
* `Workbook` を `using` 文でラップして **Dispose** し、アンマネージドリソースを速やかに解放する：

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **バージョン互換性:** Aspose.Cells が生成するファイルは Excel 2010‑2023 と互換性があるため、下流ユーザーが形式の問題に直面することはありません。

---

## 完全動作サンプル

以下はすぐにコピー＆ペーストして実行できる完全プログラムです。必要な `using` ディレクティブ、コメント、エラーハンドリングをすべて含んでいます。

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**検証手順**

1. プログラムを実行 (`dotnet run`)。  
2. `SigDigits.xlsx` を開く。  
3. **A1** が `123.5` と表示されていることを確認。  
4. ファイルの XML（`.xlsx` は zip アーカイブ）を展開し、`<c>` 要素の `s` 属性にカスタム書式 `"0.######"` が格納されていることを確認。

---

## まとめ

このチュートリアルでは、**C# で Excel ワークブックを作成**し、**カスタム数値書式を適用**、**セルの小数点桁数を設定**、そして **xlsx としてワークブックを保存** する方法を Aspose.Cells を使って学びました。解決策は、Excel 内での視覚的書式設定と `ExportTableOptions` を通したデータエクスポート時の丸め処理の両方を示しています。

ここからさらにできること:

* 範囲やテーブル全体への適用へ拡張  
* `StyleFlag` を使ってフォントや罫線など複数のスタイルを組み合わせ  
* データソースをループしながら同一の書式ロジックでレポート自動生成  

さまざまな書式文字列や小数点数、エクスポートオプションを試して、特定の報告ニーズに合わせてカスタマイズしてください。コーディングを楽しんでください！

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを基にした関連トピックを扱っています。各リソースには、ステップバイステップの解説と完全なコード例が含まれているので、API の追加機能を習得したり、別の実装アプローチを探求したりするのに役立ちます。

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}