---
category: general
date: 2026-08-11
description: C#でExcelをTXTにエクスポートするステップバイステップガイド。Aspose.Cellsを使用してxlsxをプレーンテキストに変換する方法を学びましょう。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: ja
lastmod: 2026-08-11
og_description: C#でExcelを素早くTXTにエクスポート。このチュートリアルでは、xlsxをプレーンテキストに変換する方法、フォーマットの設定、そして大規模なワークシートの処理方法を紹介します。
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: C#でExcelをTXTにエクスポート – 開発者向けステップバイステップガイド
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: C#でExcelをテキストファイルにエクスポートする – 完全プログラミングガイド
url: /ja/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で Excel を txt にエクスポート – 完全プログラミングガイド

**Excel を txt にエクスポート** したい場合、数行の C# コードで実現できます。このガイドでは、`.xlsx` ワークブックをプレーンテキストファイルに変換し、任意のデータ形式を保持する方法を示します。

ワークシートをテキストファイルとしてエクスポートするのは、下流システムが区切りデータのみを受け付ける場合や、生セル値を監査したい場合に一般的な要件です。以下のセクションでは、日付や数値の書式設定、巨大シートの取り扱い、典型的な落とし穴の回避方法を学びます。

## xlsx をプレーンテキストに変換するための前提条件

開始する前に、以下が揃っていることを確認してください。

* .NET 6.0（またはそれ以降） – コードは .NET Standard 2.0 を対象としているため、.NET Framework 4.6+ でも動作します。
* **Aspose.Cells** のライセンス（評価版でもテストは可能）。
* Visual Studio 2022 または Visual Studio Code などの IDE。
* プロジェクトから参照できるフォルダーに配置した `input.xlsx` という名前の Excel ファイル。

これらが唯一の外部要件であり、チュートリアルは追加の NuGet パッケージに依存しません。

## Aspose.Cells を使って excel を txt にエクスポートする方法

Aspose.Cells は `ExportTableOptions` クラスを提供し、セル値を文字列としてどのようにレンダリングするかを制御できます。`ExportAsString` を `true` に設定すると、すべてのセルがテキストとして書き込まれ、決定的なプレーンテキスト出力が得られます。

### 手順 1 – ワークブックをロード

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*`Workbook` コンストラクタは Excel ファイルをメモリに読み込みます。ファイルが存在しない場合は例外がスローされるため、本番コードでは try‑catch でラップすることを推奨します。*

### 手順 2 – 最初のワークシートを取得

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*ワークシートはゼロベースなので、インデックス 0 は最初のタブを指します。特定のタブを対象にしたい場合は、インデックスの代わりにシート名（`workbook.Worksheets["Sheet1"]`）を使用できます。*

### 手順 3 – テキスト変換用のエクスポートオプションを定義

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` は元の型に関係なくすべてのセルを文字列に変換することを保証します。`DateTimeFormat` と `NumberFormat` プロパティで日付や数値の表示方法を制御でき、**xlsx をプレーンテキストに変換** する際に特定のパターンが必要なシステム向けに重要です。*

### 手順 4 – ワークシートをテキストファイルとしてエクスポート

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` は指定したオプションを使用してワークシートの内容をプレーンテキストファイルに書き込みます。デフォルトの区切り文字はタブ文字（`\t`）です。別の区切り文字が必要な場合は、`ExportTableOptions` インスタンスを受け取るオーバーロードを使用し、`ExportTableOptions.Separator` を指定してください。生成されたファイルは任意のテキストエディタで開くか、データベースにインポートできます。*

#### 期待される出力

`input.xlsx` の内容が次のとおりであると仮定します。

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Sample text|

上記オプションを使用すると、`Exported.txt` ファイルは次のようになります。

```
2023-05-01	1,234.50	Sample text
```

各列はタブで区切られ、日付は `yyyy‑MM‑dd` 形式、数値は千位区切りにカンマを使用し小数点以下2桁が表示されます。

## ワークシートをテキストファイルとしてエクスポートする際の一般的な落とし穴

| 問題 | 発生理由 | 回避策 |
|------|----------|--------|
| ロケール依存の数値書式 | デフォルト書式は OS のカルチャに従うため、カンマやピリオドが不規則になることがあります。 | `ExportTableOptions` の `NumberFormat` を明示的に設定する。 |
| 非表示行・列が出力に含まれる | Aspose.Cells は使用範囲全体をエクスポートするため、非表示行も含まれます。 | `ExportTableOptions.ExportHiddenRows = false` および `ExportHiddenColumns = false` を設定して除外する。 |
| 大規模ワークシートでメモリ圧迫 | エクスポート前にワークブック全体がメモリにロードされます。 | `Workbook.LoadOptions` の `LoadDataOnly = true` を使用してメモリ使用量を削減するか、チャンク単位で処理する。 |
| ソースファイルで日付セルがテキストとして保存されている | 既に文字列としてフォーマットされたセルは、エクスポーターがテキストとして扱い `DateTimeFormat` が無視されます。 | ソースワークブックで日付を正しい Excel の日付型として保存する。 |

これらの問題に対処すれば、**ワークシートをテキストとしてエクスポートする方法** がさまざまな環境でも信頼できるものになります。

## ソリューションの拡張 – カスタム区切り文字とストリーミングエクスポート

タブ区切りではなくカンマ区切り（CSV）ファイルが必要な場合は、オプションを次のように変更します。

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

500 MB を超える大容量ファイルの場合、ストリーミングで出力すると RAM の枯渇を防げます。

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

`Stream` を受け取るオーバーロードは行を逐次書き込むため、バッチジョブやテキストファイルを直接クライアントに返す Web サービスに最適です。

## プログラムで結果を検証する

エクスポート完了後、最初の行をメモリに読み戻して書式を確認できます。

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

このスニペットを実行すると、*期待される出力* セクションに示した行と同じ内容が表示され、変換が成功したことを確認できます。

## 完全コードのまとめ

すべての要素を組み合わせると、コンソールアプリケーションにコピペできる自己完結型プログラムが完成します。

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

コンパイルして実行すると、`Exported.txt` ファイルがソースワークブックと同じディレクトリに作成されます。

## 次のステップと関連トピック

* **ワークシートをテキストファイルとしてエクスポート** – 区切り文字、エンコーディング（UTF‑8 vs. ASCII）、改行スタイルを変えてクロスプラットフォーム互換性を検証してください。  
* **一括変換** – `workbook.Worksheets` をループして、各タブごとに別々のテキストファイルを生成します。  
* **データベースとの統合** – 生成したテキストを直接 SQL Server や PostgreSQL のバルクインサートにパイプします。  
* **  

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示したテクニックを基にした密接に関連するテーマを取り上げています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、追加の API 機能を習得したり、独自プロジェクトで代替実装アプローチを探求したりするのに役立ちます。

- [How to Export Excel Files in .NET Using Aspose.Cells&#58; A Comprehensive Guide](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [How to Export Visible Excel Rows Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}