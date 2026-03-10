---
category: general
date: 2026-02-15
description: C#でブックを作成し、DataTableを行の書式設定付きでExcelにエクスポート、行の背景色を設定し、数分でExcelのタスクを自動化します。
draft: false
keywords:
- create workbook c#
- excel export formatting
- export datatable excel
- set row background
- excel automation c#
language: ja
og_description: C#でワークブックを素早く作成し、行スタイルを適用し、完全なコード例とベストプラクティスのヒントを用いてExcelエクスポートを自動化する。
og_title: C#でワークブックを作成 – 書式付きでDataTableをExcelにエクスポート
tags:
- C#
- Excel
- DataExport
title: C#でワークブックを作成 – DataTableを書式付きでExcelにエクスポート
url: /ja/net/excel-data-export-retrieval/create-workbook-c-export-datatable-to-excel-with-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Workbook を作成 C# – DataTable を Excel にエクスポート（書式設定付き）

カスタムスタイルで `DataTable` を Excel に書き出すために **create workbook C#** が必要だったことはありませんか？ あなただけではありません。多くの業務アプリケーションでは、非技術者でもすぐに開いて理解できる、見栄えの良いスプレッドシートを出力する必要があります。  

このガイドでは、**how to create workbook C#** の完全な実装例を順を追って解説し、**excel export formatting** を適用し、**row background** を設定し、**excel automation c#** を活用して洗練されたファイルを生成する方法を示します。曖昧な「ドキュメント参照」ではなく、全コードと各行が重要な理由の説明、そして明日すぐに使えるヒントを提供します。

---

## 前提条件

- .NET 6（または .NET Framework 4.6 以上）。  
- Visual Studio 2022 または任意の C# 対応 IDE。  
- **Aspose.Cells for .NET** NuGet パッケージ（または `Workbook`、`Worksheet`、`Style` を提供する任意のライブラリ）。  
- `DataTable` の基本的な知識。  

Aspose.Cells がまだインストールされていない場合は、以下を実行してください：

```bash
dotnet add package Aspose.Cells
```

> **プロのコツ:** 無料トライアルはほとんどの開発シナリオで利用可能です。出荷前に必ずライセンスキーを差し替えてください。

![スタイル付き行を示す Workbook C# の例（Excel）]( "行の背景色付き Workbook C# の例")

---

## 手順 1: Workbook と Worksheet を初期化する（Create Workbook C#）

最初に行うべきことは `Workbook` のインスタンス化です。メモリ上で新しい Excel ファイルを開くイメージです。

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // Create a new workbook – this is the core of create workbook C#
        var workbook = new Workbook();

        // Grab the first worksheet (index 0) – it's already there by default
        var worksheet = workbook.Worksheets[0];

        // The rest of the steps will fill this worksheet with data and styling
        ExportDataTableWithStyling(workbook, worksheet);
    }
}
```

**Why?**  
`Workbook` は Excel ドキュメント全体を保持し、`Worksheet` は単一のタブを表します。クリーンなブックから始めることで、出力のすべての側面を制御でき、デフォルトの隠れたスタイルが混入することを防げます。

---

## 手順 2: サンプル DataTable を作成する（Export DataTable Excel）

実際のプロジェクトではデータベースから取得しますが、ここでは簡易的に `DataTable` をその場で作成します。

```csharp
private static DataTable GetSampleData()
{
    var dt = new DataTable("Employees");
    dt.Columns.Add("Id", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
    dt.Rows.Add(2, "Bob Smith", "IT", 68000);
    dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
    dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);

    return dt;
}
```

**Why this matters:**  
`DataTable` のエクスポートは、アプリケーションから Excel へ表形式データを移す最も一般的な方法です。上記のメソッドは完全に自己完結しているため、任意のプロジェクトにコピーペーストすればそのまま動作します。

---

## 手順 3: 行ごとに Style を作成する（Excel Export Formatting）

各行に個別の背景色を付けるため、`DataTable` の行数だけ `Style` オブジェクトを生成します。ここで **excel export formatting** の威力が発揮されます。

```csharp
private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
{
    var styles = new Style[rowCount];

    // Define a palette of background colors – feel free to extend
    var colors = new[] { System.Drawing.Color.LightYellow,
                         System.Drawing.Color.LightCyan,
                         System.Drawing.Color.LightGreen,
                         System.Drawing.Color.LightPink };

    for (int i = 0; i < rowCount; i++)
    {
        // Create a fresh style instance
        var style = workbook.CreateStyle();

        // Cycle through our color array so rows get alternating shades
        style.ForegroundColor = colors[i % colors.Length];
        style.Pattern = BackgroundType.Solid;

        // Optional: make the font a little bolder for readability
        style.Font.IsBold = true;

        styles[i] = style;
    }

    return styles;
}
```

**Why per‑row styling?**  
特定のレコード（例: 支払期限超過の請求書）を強調したい場合は、単純な色サイクルを条件ロジックに置き換えて `style.ForegroundColor` を行データに基づいて設定すれば実現できます。

---

## 手順 4: 行スタイル付きで DataTable をインポートする（Set Row Background）

ここまで準備したデータ、ブック、スタイルをすべて結合します。

```csharp
private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
{
    // 1️⃣ Get the data
    DataTable dt = GetSampleData();

    // 2️⃣ Build a style for each row
    Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

    // 3️⃣ Import the DataTable starting at cell A1.
    //    The `true` flag tells Aspose.Cells to include column headers.
    worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

    // 4️⃣ Save the workbook to disk
    string outputPath = "EmployeesReport.xlsx";
    workbook.Save(outputPath);
    Console.WriteLine($"Workbook saved to {outputPath}");
}
```

**What you’ll see:**  
`EmployeesReport.xlsx` を開くと、ヘッダー行はデフォルトの書式、続く 4 行のデータはそれぞれ淡い背景色が付いています。結果は手作業で作成したレポートのように見え、単なるデータダンプとは異なります。

---

## 手順 5: 高度な Excel Automation C# ヒント（Excel Automation C#）

基本例に加えて活用できる簡単なテクニックをいくつか紹介します：

| Tip | Code Snippet | When to Use |
|-----|--------------|-------------|
| **Auto‑Fit Columns** | `worksheet.AutoFitColumns();` | データをインポートした後、文字が切れないようにします。 |
| **Freeze Header Row** | `worksheet.WindowPane.SplitRows = 1;` | テーブルが画面を超えてスクロールする可能性がある場合。 |
| **Conditional Formatting** | <details><summary>Show</summary>```csharp\nvar cf = worksheet.ConditionalFormattings[0];\ncf.AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");\ncf.Style.ForegroundColor = System.Drawing.Color.LightSalmon;\ncf.Style.Pattern = BackgroundType.Solid;\n```</details> | 閾値を超える給与をハイライトします。 |
| **Protect Sheet** | `worksheet.Protect(ProtectionType.All, "myPassword");` | 読み取り専用レポートが必要な場合。 |

これらのスニペットは **excel automation c#** の幅広さを示しており、コアのインポートロジックを書き換えることなくワークブックを拡張し続けられます。

---

## よくある質問とエッジケース

**DataTable に数千行ある場合はどうすればいいですか？**  
Aspose.Cells はデータを効率的にストリーミングしますが、メモリ節約のために各行ごとのスタイル作成を無効にしたい場合があります。その代わりに範囲全体に単一のスタイルを適用します：

```csharp
var range = worksheet.Cells.CreateRange(1, dt.Rows.Count, 0, dt.Columns.Count);
range.SetStyle(rowStyles[0]); // reuse one style for the whole block
```

**.xlsx ではなく .csv にエクスポートできますか？**  
もちろんです。保存形式を変更するだけです：

```csharp
workbook.Save("EmployeesReport.csv", SaveFormat.Csv);
```

スタイルは失われます（CSV には書式情報がありません）が、データのエクスポートは同じです。

**.NET Core でも動作しますか？**  
はい。Aspose.Cells は .NET Standard 2.0 以降をサポートしているため、同じコードが .NET 6、.NET 7、または .NET Framework でも動作します。

---

## 完全動作サンプル（コピー＆ペースト可能）

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExcelExporter
{
    static void Main()
    {
        // 1️⃣ Create a new workbook – core of create workbook C#
        var workbook = new Workbook();
        var worksheet = workbook.Worksheets[0];

        // 2️⃣ Export DataTable with styling
        ExportDataTableWithStyling(workbook, worksheet);
    }

    private static DataTable GetSampleData()
    {
        var dt = new DataTable("Employees");
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Department", typeof(string));
        dt.Columns.Add("Salary", typeof(decimal));

        dt.Rows.Add(1, "Alice Johnson", "Finance", 72000);
        dt.Rows.Add(2, "Bob Smith", "IT", 68000);
        dt.Rows.Add(3, "Charlie Lee", "HR", 59000);
        dt.Rows.Add(4, "Diana Prince", "Marketing", 75000);
        return dt;
    }

    private static Style[] BuildRowStyles(Workbook workbook, int rowCount)
    {
        var styles = new Style[rowCount];
        var colors = new[]
        {
            System.Drawing.Color.LightYellow,
            System.Drawing.Color.LightCyan,
            System.Drawing.Color.LightGreen,
            System.Drawing.Color.LightPink
        };

        for (int i = 0; i < rowCount; i++)
        {
            var style = workbook.CreateStyle();
            style.ForegroundColor = colors[i % colors.Length];
            style.Pattern = BackgroundType.Solid;
            style.Font.IsBold = true;
            styles[i] = style;
        }

        return styles;
    }

    private static void ExportDataTableWithStyling(Workbook workbook, Worksheet worksheet)
    {
        DataTable dt = GetSampleData();
        Style[] rowStyles = BuildRowStyles(workbook, dt.Rows.Count);

        // Import with row styles – sets row background (set row background)
        worksheet.Cells.ImportDataTable(dt, true, "A1", rowStyles);

        // Optional polish
        worksheet.AutoFitColumns();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}