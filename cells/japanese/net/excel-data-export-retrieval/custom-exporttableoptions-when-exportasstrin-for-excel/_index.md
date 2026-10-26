---
category: general
date: 2026-10-26
description: ExportAsStrin のカスタム ExportTableOptions を使用すると、C# で Excel データを文字列としてエクスポートできます。エクスポートの設定と実行手順をステップバイステップでご案内します。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: ja
lastmod: 2026-10-26
og_description: ExportAsStrin が有効な場合のカスタム ExportTableOptions は、文字列のみの Excel エクスポートを可能にします。C#
  でエクスポートを設定し実行する正確な手順を学びましょう。
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: ExportAsString時のカスタムExportTableOptions – C#でExcelを文字列としてエクスポート
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Excel の ExportAsStrin 時のカスタム ExportTableOptions
url: /ja/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – C#でExcelを文字列としてエクスポート

もし **Custom ExportTableOptions when ExportAsStrin** が必要で、すべてのセルの値をプレーンな文字列として取得したい場合、このガイドではその手順を正確に示します。データインポートパイプラインを構築している場合や、クリーンなCSV用ダンプが必要な場合でも、オプションをこのように設定すると型変換の予期せぬ問題を回避できることが分かります。

このチュートリアルでは、Aspose.Cells ライブラリを使用して **how to export excel as string** を学び、完全な実行可能コードを確認し、各設定の背後にある理由を理解します。外部ドキュメントは不要です – 必要なものはすべてここにあります。

## 前提条件

* .NET 6.0 SDK またはそれ以降がインストールされている  
* Visual Studio 2022（または .NET をサポートする任意の IDE）  
* Aspose.Cells for .NET パッケージ（NuGet でインストール: `Install-Package Aspose.Cells`）  
* プロジェクトのルートフォルダーに配置した Excel ワークブック（`sample.xlsx`）

これらが唯一の依存項目です。コードは Windows、Linux、macOS のいずれでも追加のライブラリなしで実行できます。

## 手順 1: エクスポートしたいブックをロードする

**Custom ExportTableOptions when ExportAsStrin** を使用する際に最初に行うことは、ロードしたブックから `Worksheet` オブジェクトを取得することです。このオブジェクトを使って行や列、エクスポート API にアクセスできます。

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*なぜ重要か:*  
`Workbook` はファイルを一度だけ読み込み、すべての書式情報をメモリに保持します。特定の `Worksheet` を選択することで、エクスポート対象を限定し、非表示シートの不要な処理を回避できます。

## 手順 2: ExportAsString = true で ExportTableOptions を設定する

**Custom ExportTableOptions when ExportAsStrin** の核心は `ExportTableOptions` オブジェクトです。`ExportAsString` を設定すると、元のデータ型（日付、数値、ブール値など）に関係なく、すべてのセルを文字列として扱うようエクスポーターが強制されます。`PreserveFormatting` を有効にすると、結果の文字列に視覚的スタイル（例: 通貨記号）が保持されます。

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*なぜ重要か:*  
その後 `ExportDataTable` を呼び出すと、ライブラリは通常各列の .NET 型を推測しようとします。`ExportAsString = true` にすると、この推測ステップがスキップされ、下流の CSV パーサーを壊す可能性のある予期せぬ `DateTime` や `double` への変換が防止されます。

## 手順 3: カスタムオプションを使用して範囲を DataTable にエクスポートする

これでワークシートから矩形範囲（行 0‑9、列 0‑4）をエクスポートできます。このメソッドは、すべてのフィールドが `string` である `DataTable` を返します。

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*なぜ重要か:*  
`ExportDataTable` は、Excel データを多くの .NET API（例: Entity Framework、Dapper）がすでに理解できるリレーショナル構造に移す最も便利な方法です。**Custom ExportTableOptions when ExportAsStrin** を渡すことで、各 `DataColumn.DataType` が `typeof(string)` になることが保証されます。

## 手順 4: 結果を検証する – すべての値が文字列であることを確認

エクスポートが期待通りに動作したことを確認するのは良い習慣です。以下のループは各セルとその実行時型を出力します。

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**期待される出力**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

すべてのセルが型として `String` を示し、**Custom ExportTableOptions when ExportAsStrin** が正しく機能したことが確認できます。

## 手順 5: オプション – DataTable を CSV に書き出す

最終的な目的がプレーンテキストファイルである場合、`DataTable` を簡単に CSV にシリアライズできます。



## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法を基にした、密接に関連するトピックを取り上げています。各リソースには、ステップバイステップの解説とともに完全な動作コード例が含まれており、追加の API 機能を習得し、独自プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [Aspose.Cells for .NET を使用した Excel から DataTable への HTML 文字列エクスポート: ステップバイステップガイド](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Excel のカスタムプロパティを PDF にエクスポート (Aspose Cells .NET)](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java カスタムロードフィルタによる Excel エクスポート](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}