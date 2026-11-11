---
category: general
date: 2026-10-26
description: C#で元号の日付を解析し、NPOIを使ってExcelワークシートに挿入する際の日本カレンダーCultureInfoの使い方を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: ja
lastmod: 2026-10-26
og_description: C#で日本のカレンダーCultureInfoを使用して令和元号の日付を解析し、Excelワークシートに書き込む。完全な実行可能コードと解説。
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: C#で日本のカレンダーCultureInfoを使用 – 完全なExcel例
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: C#で日本のカレンダーCultureInfoを使用してExcelに日付を書き込む方法
url: /ja/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#で日本のカレンダーCultureInfoを使用して日付をExcelに書き込む方法

C#で日付を扱う際に **日本のカレンダーCultureInfo** を使用する必要がある場合、このガイドで具体的な手順を示します。日本の元号名を含む日付文字列（例: *Reiwa 2/5/1*）を解析し、結果として得られる `DateTime` を NPOI ライブラリを使って Excel ワークシートの最初のセルに書き込む方法を学びます。

正しい `CultureInfo` を使用せずに元号ベースの日付を解析すると、`FormatException` が発生したり、月や日が正しく解釈されなかったりします。`CultureInfo` を日本のカレンダーに設定することで、.NET ランタイムが元号を正しく解釈し、Excel に保存する値が元の日本表記と一致することが保証されます。

このチュートリアルで学べること:

* 日本のカレンダーを使用する `CultureInfo` オブジェクトを作成する。
* `DateTime.Parse` で日本の元号日付文字列を解析する。
* 解析した `DateTime` を NPOI のワークシートセルに挿入する。
* 完全な実行可能プログラムと期待される出力を見る。

> **前提条件** – .NET 6.0+（または .NET Core 3.1+）、**NPOI** NuGet パッケージ、そして C# と Excel ファイル操作の基本的な理解。

---

## 必要なもの

| アイテム | 理由 |
|------|--------|
| **.NET SDK** (6.0 以上) | `CultureInfo` 用のランタイムとライブラリを提供します。 |
| **NPOI** (`NPOI` NuGet パッケージ) | Office がインストールされていなくても Excel ファイルを作成・操作できます。 |
| **Visual Studio Code**、**Visual Studio**、または任意の C# IDE | サンプルをコンパイルして実行するために使用します。 |
| **日本の元号日付文字列**（例: `"Reiwa 2/5/1"`） | 日本のカレンダー使用例を示すために必要です。 |

---

## Step 1: Install NPOI

プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します:

```bash
dotnet add package NPOI --version 2.6.1
```

このパッケージは後で使用する `IWorkbook`、`ISheet`、`ICell` 型を提供します。

---

## Step 2: Create a CultureInfo that uses the Japanese calendar

日本のカレンダーは元号ベースのカレンダーです。`ja-JP` ロケールの *Japanese* バリアントを要求し、カレンダーを明示的に `JapaneseCalendar` に設定する必要があります。

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **なぜ重要か** – デフォルトの `ja-JP` カルチャはグレゴリオ暦を使用します。`Calendar` プロパティを再割り当てすることで、*Reiwa* などの元号名が解析時に認識されるようになります。

---

## Step 3: Parse a Japanese era date string

`CultureInfo` が設定されたので、元号を含む文字列を安全に解析できます。

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**出力**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

`Parse` メソッドは *Reiwa 2* をグレゴリオ暦の 2020 年、5 月、1 日として解釈します。

### エッジケース: 無効な元号の取り扱い

ユーザーがサポート外の元号（例: Heisei が終了した後の `"Heisei 31/4/30"`）を入力した場合、`DateTime.Parse` は `FormatException` をスローします。try‑catch ブロックでラップして、わかりやすいエラーメッセージを提供しましょう:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## Step 4: Write the parsed DateTime into an Excel worksheet

`DateTime` オブジェクトが用意できたら、Excel のセルに格納できます。NPOI は `DateTime` 値を自動的に Excel の日付形式に変換します。

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**結果** – *JapaneseEraDate.xlsx* を開くと、セル A1 に **2020‑05‑01** が表示されます。

### なぜ NPOI を使うのか？

*任意のプラットフォーム*（Windows、Linux、macOS）で動作し、Microsoft Office を **必要としません**。このため CI パイプライン、Docker コンテナ、サーバーサイド処理にも適しています。

---

## Step 5: Full, runnable program

すべてをまとめると、以下の完全なコンソールアプリケーションが全体の流れを示しています:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**実行方法**

```bash
dotnet run
```

実行後、プロジェクトフォルダーに正しく解析された日付が入った `JapaneseEraDate.xlsx` が作成されます。

---

## Common pitfalls and best‑practice tips

| 落とし穴 | 対策 / 推奨 |
|---------|----------------------|
| `japaneseCulture.DateTimeFormat.Calendar` の設定を忘れる | 必ず `JapaneseCalendar` インスタンスを割り当てること。設定しないと元号が認識されません。 |
| カスタム `CultureInfo` を使用せずに `DateTime.TryParse` を呼び出す | `TryParse` にも同じ `japaneseCulture` を渡して、動作を統一しましょう。 |
| Excel が元号を表示すると期待する | Excel の組み込み日付形式はグレゴリオ暦のみです。元号を表示したい場合は、元の文字列を別列に保存するか、カスタムテキスト形式を作成してください。 |
| `FileStream` を破棄しない | 示したように `using` ブロックを使用し、ファイルハンドルを速やかに解放します。 |
| スレッド間で `CultureInfo` オブジェクトを混在させる | `CultureInfo` は読み取り専用操作ではスレッドセーフですが、初期設定後に `Calendar` プロパティを変更しないようにしてください。 |

---

## Conclusion

これで C# で **日本のカレンダーCultureInfo** を使用し、日本の元号日付を正確に解析して NPOI で Excel ワークシートに `DateTime` として書き込む方法が分かりました。設定、解析、エラーハンドリング、Excel 出力を網羅した完全な例は、国際化されたレポートやデータ交換シナリオの堅実な基盤となります。

次に試したいこと:

* **カスタムテキストで日付をフォーマット** し、Excel 内に元号名を保持する。
* **Excel から日付を読み取る** ときに `cell.DateCellValue` を使用し、日本のカレンダーを尊重する。
* **同様の手法を他の元号ベースカレンダー**（例: タイの仏教暦）に適用するには、`JapaneseCalendar` を該当する `Calendar` サブクラスに置き換える。

さまざまな元号文字列や大規模データセットで実験したり、ASP.NET Core API に組み込んでオンデマンドで Excel レポートを生成したりしてみてください。ハッピーコーディング！

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示した手法を応用した関連トピックを扱っています。各リソースには完全な動作コード例とステップバイステップの解説が含まれており、追加の API 機能を習得したり、プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [Create Excel Workbook with Japanese Calendar Dates – Full Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to create Excel workbook and parse Japanese dates in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}