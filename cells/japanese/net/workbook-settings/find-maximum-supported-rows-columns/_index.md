---
"description": "Aspose.Cells for .NET を使用して、XLS および XLSX 形式でサポートされる行数と列数の最大数をご確認ください。この包括的なチュートリアルで、Excel のデータ管理を最大限に活用しましょう。"
"linktitle": "XLS および XLSX 形式でサポートされる最大行数と最大列数を確認する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "XLS および XLSX 形式でサポートされる最大行数と最大列数を確認する"
"url": "/ja/net/workbook-settings/find-maximum-supported-rows-columns/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# XLS および XLSX 形式でサポートされる最大行数と最大列数を確認する

## 導入
Excelの世界では、大規模なデータセットの管理は困難な作業になることがあります。特に、様々なファイル形式でサポートされる行数と列数の最大数を扱うとなるとなおさらです。このチュートリアルでは、Aspose.Cells for .NETライブラリを用いて、XLS形式とXLSX形式でサポートされる行数と列数の最大値を調べる手順を説明します。この記事を読み終える頃には、この強力なツールを活用してExcel関連のタスクを効率的に処理する方法を包括的に理解できるでしょう。
## 前提条件
チュートリアルに進む前に、次の前提条件が満たされていることを確認してください。
1. [.NET フレームワーク](https://dotnet.microsoft.com/en-us/download) または [.NET コア](https://dotnet.microsoft.com/en-us/download) システムにインストールされています。
2. [Aspose.Cells .NET 版](https://releases.aspose.com/cells/net/) ライブラリがダウンロードされ、プロジェクトで参照されます。
まだダウンロードしていない場合は、Aspose.Cells for .NETライブラリを以下のサイトからダウンロードできます。 [Webサイト](https://releases.aspose.com/cells/net/) またはインストールするには [ヌゲット](https://www。nuget.org/packages/Aspose.Cells/).
## パッケージのインポート
まず、Aspose.Cells for .NETライブラリから必要なパッケージをインポートする必要があります。C#ファイルの先頭に以下のusingステートメントを追加してください。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## ステップ1: XLS形式でサポートされる最大行数と最大列数を確認する
まず、XLS (Excel 97-2003) 形式でサポートされている最大行数と最大列数を調べてみましょう。
```csharp
// XLS 形式に関するメッセージを印刷します。
Console.WriteLine("Maximum Rows and Columns supported by XLS format.");
// XLS 形式でワークブックを作成します。
Workbook wb = new Workbook(FileFormatType.Excel97To2003);
// XLS 形式でサポートされる最大行数と最大列数を印刷します。
int maxRows = wb.Settings.MaxRow + 1;
int maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
Console.WriteLine();
```
このステップでは、次の作業を行います。
1. XLS 形式で作業していることを示すメッセージを出力します。
2. 新規作成 `Workbook` インスタンスを使用して `FileFormatType.Excel97To2003` XLS 形式を表す列挙型。
3. XLS形式でサポートされている最大行数と最大列数を取得するには、 `Workbook.Settings.MaxRow` そして `Workbook.Settings.MaxColumn` それぞれプロパティです。これらの値に1を加算することで、実際の最大行数と最大列数が得られます（行番号と列番号は0から始まるため）。
4. 最大行数と最大列数をコンソールに出力します。
## ステップ2: XLSX形式でサポートされている最大行数と最大列数を確認する
次に、XLSX (Excel 2007 以降) 形式でサポートされている最大行数と最大列数を調べてみましょう。
```csharp
// XLSX 形式に関するメッセージを印刷します。
Console.WriteLine("Maximum Rows and Columns supported by XLSX format.");
// XLSX 形式でワークブックを作成します。
wb = new Workbook(FileFormatType.Xlsx);
// XLSX 形式でサポートされる最大行数と最大列数を印刷します。
maxRows = wb.Settings.MaxRow + 1;
maxCols = wb.Settings.MaxColumn + 1;
Console.WriteLine("Maximum Rows: " + maxRows);
Console.WriteLine("Maximum Columns: " + maxCols);
```
このステップでは、次の作業を行います。
1. XLSX 形式で作業していることを示すメッセージを出力します。
2. 新規作成 `Workbook` インスタンスを使用して `FileFormatType.Xlsx` XLSX 形式を表す列挙型。
3. XLSX形式でサポートされている最大行数と最大列数を取得するには、 `Workbook.Settings.MaxRow` そして `Workbook.Settings.MaxColumn` それぞれプロパティです。これらの値に1を加算することで、実際の最大行数と最大列数が得られます（行番号と列番号は0から始まるため）。
4. 最大行数と最大列数をコンソールに出力します。
## ステップ3: 成功メッセージを表示する
最後に、「FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats」の例が正常に実行されたことを示す成功メッセージを表示しましょう。
```csharp
Console.WriteLine("FindMaximumRowsAndColumnsSupportedByXLSAndXLSXFormats executed successfully.");
```
このステップでは、コンソールに成功メッセージを出力するだけです。
## 結論
このチュートリアルでは、Aspose.Cells for .NETライブラリを使用して、XLSおよびXLSXファイル形式でサポートされる最大行数と最大列数を確認する方法を学習しました。これらの形式の制限を理解することで、Excelベースのプロジェクトをより適切に計画・管理し、データがサポート範囲内に収まるようにすることができます。
## よくある質問
### XLS 形式でサポートされる行の最大数はいくつですか?
XLS (Excel 97-2003) 形式でサポートされる行の最大数は 65,536 です。
### XLS 形式でサポートされる列の最大数はいくつですか?
XLS (Excel 97-2003) 形式でサポートされる列の最大数は 256 です。
### XLSX 形式でサポートされる行の最大数はいくつですか?
XLSX (Excel 2007 以降) 形式でサポートされる行の最大数は 1,048,576 です。
### XLSX 形式でサポートされる列の最大数はいくつですか?
XLSX (Excel 2007 以降) 形式でサポートされる列の最大数は 16,384 です。
### Aspose.Cells for .NET ライブラリを使用して他の Excel ファイル形式で作業できますか?
はい、Aspose.Cells for .NETライブラリは、XLS、XLSX、ODSなど、幅広いExcelファイル形式をサポートしています。 [ドキュメント](https://reference.aspose.com/cells/net/) 利用可能な機能について学習します。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}