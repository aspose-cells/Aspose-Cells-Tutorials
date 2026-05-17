---
category: general
date: 2026-02-21
description: Excel を txt として保存し、有効数字を正確に制御します。C# で Excel を txt にエクスポートし、簡単に有効数字を設定できます。
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: ja
og_description: Excel をすばやく txt に保存。Excel を txt にエクスポートし、有効数字を設定し、C# でテキスト出力を制御する方法を学びましょう。
og_title: Excelをtxtとして保存 – C#で有効数字付きの数値をエクスポート
tags:
- C#
- Aspose.Cells
- Excel automation
title: Excelをtxtとして保存 – 有効数字を含む数値エクスポートの完全C#ガイド
url: /ja/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Save Excel as txt – Complete C# Guide to Export Numbers with Significant Digits

Excel を **txt として保存** したいけど、数値の精度が失われるのが心配…という経験はありませんか？ 同じ悩みを抱える開発者は多いです。Excel を txt にエクスポートすると、小数点以下が多すぎたり、丸められすぎてしまうことがあります。  

このチュートリアルでは、**Excel を txt にエクスポート** しながら **有効数字を設定** するシンプルな方法をご紹介します。最後まで読めば、ワークブックをテキストとして保存し、数値を txt にエクスポートし、数値フォーマットを完全にコントロールできる C# スニペットが手に入ります。

## What You’ll Learn

- 新しいワークブックを作成し、数値データを書き込む方法。
- `TxtSaveOptions` を使って **有効数字を設定** する正しい手順。
- **ワークブックをテキストとして保存** し、結果を確認する方法。
- エッジケースの取り扱い（大きな数、負の値、ロケール問題）。
- 出力をさらに調整するための簡単なヒント（区切り文字の変更、エンコーディング）。

### Prerequisites

- .NET 6.0 以降（コードは .NET Framework 4.6+ でも動作します）。
- **Aspose.Cells** NuGet パッケージ（`Install-Package Aspose.Cells`）。
- C# の基本構文が分かっていれば OK ― Excel の深い Interop 知識は不要です。

> **Pro tip:** Visual Studio を使用している場合は、*nullable reference types*（`<Nullable>enable</Nullable>`）を有効にして、潜在的な null バグを早期に検出しましょう。

---

## Step 1: Initialize the Workbook and Write a Number

まず、ワークブックオブジェクトが必要です。これは Excel ファイルのメモリ上の表現と考えてください。  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Why this matters:**  
プログラムでワークブックを作成すると COM Interop のオーバーヘッドを回避でき、`PutValue` が自動的にデータ型を判別してくれるため、セルは文字列ではなく数値として扱われます。

---

## Step 2: Configure TxtSaveOptions to Control Significant Digits

`TxtSaveOptions` クラスが魔法の場所です。`SignificantDigits` を設定することで、ファイルを書き出す際に保持する有効数字の桁数を Aspose.Cells に指示できます。

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Why you should set this:**  
**数値を txt にエクスポート** する際、多くの場合、一定の精度だけが必要です（例: 特定の精度しか受け付けないレポートシステム向け）。`SignificantDigits` プロパティは、元の数値の長さに関係なく一貫した丸めを保証します。

---

## Step 3: Save the Workbook as a Text File

先ほど定義したオプションを使って、ワークブックをディスクに書き出します。

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**What you’ll see:**  
`Numbers.txt` を開くと、1 行だけが表示されます。

```
12350
```

元の `12345.6789` は **4 桁の有効数字** に丸められ、要求通りの結果になります。

---

## Step 4: Verify the Output (Optional but Recommended)

自動テストは習慣化すると良いでしょう。保存直後に実行できる簡単なチェックを用意しました。

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

このブロックを実行すると、すべてが一致していれば緑のチェックマークが表示され、**Excel を txt として保存** した操作が期待通りに動作したことを確認できます。

---

## Common Variations & Edge Cases

### Exporting Multiple Cells or Ranges

**Excel を txt にエクスポート** したい範囲が複数ある場合は、保存前にセルを追加で埋めれば OK です。

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

同じ `TxtSaveOptions` が各値に対して 4 桁のルールを適用し、次のような出力になります。

```
12350
0.0001235
-98800
```

### Changing the Delimiter

下流システムがタブ区切りを期待している場合は、区切り文字を次のように変更します。

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

これで行内の各セルがタブで区切られます。

### Handling Locale‑Specific Decimal Separators

ユーザーが小数点にカンマを使用する場合は、カルチャを設定します。

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

フランス語などのロケールでは、`12350` が `12 350`（千位区切りにスペース）として出力されます。

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Expected `Numbers.txt` content (default delimiter, 4 significant digits):**

```
12350	0.0001235	-98800
```

タブ文字（`\t`）が出力に含まれるのは、例ではデリミタをデフォルト（タブ）にしたためです。CSV が好みならカンマに変更してください。

---

## Conclusion

これで **Excel を txt として保存** しながら有効数字をコントロールする方法がマスターできました。ワークブックの作成、`TxtSaveOptions.SignificantDigits` の設定、保存の 3 ステップだけで、**Excel を txt にエクスポート** を確実に行えます。  

ここからは次のように活用できます：

- 大規模データセット向けに **数値を txt にエクスポート**。
- 区切り文字、エンコーディング、カルチャ設定を調整して、任意の下流システムに合わせる。
- エクスポート前に Aspose.Cells の他機能（スタイル、数式など）と組み合わせる。

`SignificantDigits` を 2 や 6 に変えて出力がどう変わるか試してみてください。**テキストとしてワークブックを保存** できる柔軟性は、データ交換パイプラインで非常に便利です。

---

### Related Topics You Might Explore Next

- **Export Excel to CSV** with custom column ordering.
- **Read txt files back into a workbook** (`Workbook.Load` with `LoadOptions`).
- **Batch processing** multiple worksheets and consolidating them into one txt file.
- **Performance tuning** for large‑scale exports (streaming vs. in‑memory).

質問やカスタマイズ例があればコメントで教えてください。Happy coding!  

---  

*Image: A screenshot of the generated `Numbers.txt` file showing rounded values.*  
*Alt text: “Numbers.txt file displaying 12350, 0.0001235, and -98800 after saving Excel as txt with 4 significant digits.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}