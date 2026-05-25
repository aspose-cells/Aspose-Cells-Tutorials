---
category: general
date: 2026-03-22
description: 書式付きでExcelをエクスポートし、数値形式を保持する方法。Excelの範囲を変換し、数式の結果を取得し、Aspose.Cells を使用して書式付きでExcelをエクスポートする方法を学びます。
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: ja
og_description: 書式付きでExcelをエクスポートし、数値形式を保持する方法。Excelの範囲を変換し、数式結果を取得し、C#で書式付きExcelをエクスポートするステップバイステップガイド。
og_title: Excelを書式付きでエクスポートする方法 – 数値形式を保持する
tags:
- C#
- Aspose.Cells
- Excel automation
title: Excelを書式付きでエクスポートする方法 – 数値書式を保持
url: /ja/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excelを書式付きでエクスポートする方法 – 数値書式を保持する

Excelデータをエクスポートする際に、ワークブックで見える通りにすべてのセルの見た目をそのまま保ちたいと思ったことはありませんか？ クライアントにレポートを送付したり、グリッドコントロールにデータを供給したり、単にデータベースに値を保存したりする必要があるかもしれません。 主な問題は、数値の書式が失われたり、数式が生の文字列に変換されてしまうことです。

このチュートリアルでは、**数値書式を保持**し、**Excelの範囲を** `DataTable` に **変換**し、**数式の結果を取得**し、最後に Aspose.Cells を使用して **書式付きでExcelをエクスポート**する、完全に実行可能な C# のサンプルを順を追って解説します。 最後まで読むと、任意のプロジェクトに貼り付けてワークシート参照で呼び出せる単一メソッドが手に入ります。

> **クイックプレビュー:** コードはブックを作成し、値と数式を書き込み、Aspose.Cells にセルを書式付き文字列としてエクスポートするよう指示し、`123.456 | 246.912` を出力します – まさに Excel で見える通りです。

---

## 必要なもの

- **Aspose.Cells for .NET**（無料トライアルで学習は問題ありません）
- .NET 6.0 以降（API は .NET Framework でも同じです）
- 基本的な C# 開発環境（Visual Studio、VS Code、Rider… お好きなもの）

追加の NuGet パッケージは Aspose.Cells 以外不要です。まだインストールしていない場合は、以下を実行してください：

```bash
dotnet add package Aspose.Cells
```

---

## ステップ 1 – ワークブックを作成し、値（数式含む）を書き込む

まず新しいブックを作成し、数値を **A1** に入力します。次に **B1** に、最初のセルを 2 倍するシンプルな数式を追加します。これにより、後で **数式の結果を取得** するデモの土台ができます。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**なぜ重要か:**  
- `PutValue` は生の数値を格納し、`PutFormula` は計算式を格納します。  
- Aspose.Cells は数式を **生きたまま** 保持するため、後でセルの値を取得すると `246.912` が得られ、文字列 `"=A1*2"` ではありません。

---

## ステップ 2 – Aspose.Cells に書式付き文字列として値をエクスポートさせる

`ExportDataTable` をデフォルト設定で呼び出すだけだと、数値セルは基になる `double` 値として返されます。これにより、千区切りや通貨記号、カスタム小数点など、設定した書式がすべて失われます。`ExportTableOptions` クラスを使うと、**数値書式を保持**し、**文字列としてエクスポート**できます。

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**重要ポイント:** `ExportNumberFormat = true` が **数値書式を保持** するフラグです。これが無いと、`"123.456"` や `"246.912"` が生の数値として出力され、コード上は問題なくても、Excel と同じ書式を期待する UI に貼り付けたときに見た目が変わってしまいます。

---

## ステップ 3 – エクスポートされたデータを出力（検証）

`DataTable` に書式付き文字列が入ったので、コンソールに内容をダンプしましょう。これにより、数式を自分で評価せずに **数式の結果を取得** できていることも確認できます。

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

プログラムを実行すると次のように出力されます：

```
123.456 | 246.912
```

2 列目が **数式の結果** を示しており、数式そのもののテキストではないことに注目してください。これが **書式付きで Excel をエクスポート** して下流処理に渡す際に必要な動作です。

---

## ステップ 4 – 大きな Excel 範囲の変換（オプション）

上記の例は小さな `A1:B1` のスライスだけを扱っていますが、実務ではテーブル全体をエクスポートする必要があることが多いです。同じメソッドは任意の矩形ブロックで機能します – `firstRow`、`firstColumn`、`totalRows`、`totalColumns` の引数を調整するだけです。

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**プロのコツ:** シートにすでにヘッダー行がある場合は、`includeColumnNames` を `true` に設定してください。Aspose.Cells は範囲の最初の行を列名として使用し、後で `DataTable` を UI グリッドにバインドする際に便利です。

---

## ステップ 5 – よくある落とし穴と回避方法

| 問題 | 発生原因 | 対策 |
|-------|----------------|-----|
| **数値からカンマや通貨記号が失われる** | `ExportAsString` が `false` になっている、または `ExportNumberFormat` が省略されている | `ExportAsString = true` と `ExportNumberFormat = true` の両方を設定する。 |
| **数式セルが数式テキストを返す** | エクスポート前に `CalculateFormula` を呼び出していない（ワークブックが自動計算設定でない場合に必要） | `workbook.CalculateFormula()` で自動計算を有効にするか、`ExportAsString` を使用して評価を強制する。 |
| **ヘッダーがデータ行として表示される** | 範囲にヘッダー行が含まれているのに `includeColumnNames` が `false` に設定されている | `includeColumnNames = true` に設定し、最初の行を列名として扱う。 |
| **大きな範囲でメモリ使用量が増える** | シート全体を一度にエクスポートすると、すべてがメモリにロードされるため | 500 行ずつなどのチャンクに分けてエクスポートし、必要に応じて `DataTable` を結合する。 |

---

## ステップ 6 – 完全動作サンプル（コピー＆ペースト可能）

以下は `using` 文から `Main` までの全プログラムです。コンソールアプリに貼り付けて **F5** キーを押すだけで、書式付きの出力がすぐに確認できます。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**期待される出力**

```
123.456 | 246.912

Press any key to exit...
```

これが **Excel をエクスポートする方法** の全工程です。書式はそのまま保持され、数式結果が評価され、.NET で利用できるクリーンな `DataTable` が得られます。

---

## 結論

ここでは、**Excel をエクスポートする方法** として、**数値書式を保持**し、**Excel の範囲を** `DataTable` に **変換**し、**数式結果を取得**するために必要なすべてを解説しました。ポイントは `ExportTableOptions` の設定で、`ExportAsString` と `ExportNumberFormat` を `true` にすれば、Aspose.Cells が重い処理をすべて引き受けてくれます。

ここからできること:

- `DataTable` を WPF の `DataGrid` や ASP.NET MVC のビューにバインドする。
- テーブルを CSV ファイルに書き出し、見た目を完全に保持する。
- この手法を複数シートや動的範囲に拡張する。

さまざまな書式（通貨、パーセンテージなど）や大きなデータブロックで試してみてください。問題が発生した場合は、**よくある落とし穴** の表を参照してください – **書式付きで Excel をエクスポート** する際に最も頻繁に起こるトラブルがまとめられています。

コーディングを楽しんで、エクスポートしたスプレッドシートが常にオリジナルと同じく美しく整っていることを願っています！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}