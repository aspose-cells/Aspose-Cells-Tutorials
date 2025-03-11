---
title: 優先パーサーで CSV ファイルを開く
linktitle: 優先パーサーで CSV ファイルを開く
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET のカスタム パーサーを使用して CSV ファイルを開いて解析する方法を学びます。テキストと日付を簡単に処理できます。開発者に最適です。
weight: 11
url: /ja/net/csv-file-handling/csv-file-opening-csv-files-with-preferred-parser/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 優先パーサーで CSV ファイルを開く

## 導入
CSV ファイルを扱う場合、カスタム パーサーを使用してさまざまなデータ型を処理したい場合があります。このチュートリアルでは、Aspose.Cells for .NET を使用して、好みのパーサーで CSV ファイルを開く方法について説明します。テキスト、日付、その他のカスタム形式を処理する場合でも、このガイドではわかりやすい説明とともに各手順を説明します。
## 前提条件
コードに進む前に、始めるために必要な重要な項目について説明しましょう。
1.  Aspose.Cells for .NETライブラリ: Aspose.Cellsライブラリがインストールされていることを確認してください。ダウンロードできます。[ここ](https://releases.aspose.com/cells/net/)無料トライアルもご利用いただけます[ここ](https://releases.aspose.com/).
2. .NET 開発環境: Visual Studio が推奨されますが、.NET と互換性のある IDE であればどれでも動作します。
3. C# の基礎知識: このチュートリアルでは、C# とオブジェクト指向プログラミングに精通していることを前提としています。
## パッケージのインポート
Aspose.Cells を使用するには、C# ファイルの先頭に必要な名前空間をインポートする必要があります。
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
準備ができたので、テキストや日付などのさまざまなデータ形式を処理しながら、好みのパーサーで CSV ファイルを開く方法を説明しましょう。
## ステップ1: カスタムパーサーを定義する
テキストや特定の日付形式などのさまざまなデータ型を処理するには、カスタムパーサーを定義する必要があります。Aspose.Cellsでは、カスタムパーサーは`ICustomParser`インタフェース。
### 1.1 テキストパーサーを作成する
このパーサーは通常のテキスト値を処理します。形式は変更されないので、値はそのまま返されます。
```csharp
class TextParser : ICustomParser
{
    public object ParseObject(string value)
    {
        return value;
    }
    public string GetFormat()
    {
        return "";
    }
}
```
の`ParseObject`メソッドは単に入力値を返します。これは、「何も変更しないで、テキストだけを渡してください」と言っているようなものです。
### 1.2 日付パーサーを作成する
日付については、CSVデータが正しく解析されていることを確認する必要があります。`DateTime`オブジェクト。日付パーサーを作成する方法は次のとおりです。
```csharp
class DateParser : ICustomParser
{
    public object ParseObject(string value)
    {
        DateTime myDate = DateTime.ParseExact(value, "dd/MM/yyyy", 
            System.Globalization.CultureInfo.InvariantCulture);
        return myDate;
    }
    public string GetFormat()
    {
        return "dd/MM/yyyy";
    }
}
```
このパーサーでは、`ParseExact`日付が定義済みの形式に基づいて正しく解釈されるようにするため（`"dd/MM/yyyy"`)。この方法では、この形式に従う CSV 内のすべての日付が問題なく処理されます。
## ステップ2: ロードオプションを構成する
次に、CSVファイルの読み込み方法を設定する必要があります。これは、`TxtLoadOptions`クラスでは、エンコードやカスタム パーサーなどの解析オプションを指定できます。
### 2.1 ロードオプションの設定
まず初期化から始めます`TxtLoadOptions`セパレータやエンコーディングなどの重要なパラメータを定義します。
```csharp
TxtLoadOptions oTxtLoadOptions = new TxtLoadOptions(LoadFormat.Csv);
oTxtLoadOptions.Separator = Convert.ToChar(",");
oTxtLoadOptions.Encoding = Encoding.UTF8;
oTxtLoadOptions.ConvertDateTimeData = true;
```
- 区切り文字: CSV ファイル内の値を区切るために使用される文字 (この場合はカンマ) を定義します。
- エンコーディング: 幅広い文字を処理するために UTF-8 エンコーディングを使用します。
-  ConvertDateTimeData: これをtrueに設定すると、日付値が自動的に`DateTime`可能な場合はオブジェクトを使用します。
### 2.2 カスタムパーサーを適用する
次に、先ほど作成したパーサーを割り当てて、CSV 内の値を処理します。
```csharp
oTxtLoadOptions.PreferredParsers = new ICustomParser[] 
{ 
    new TextParser(), 
    new DateParser() 
};
```
これはAspose.Cellsに`TextParser`一般的なテキスト値と`DateParser`CSV ファイル内で検出された日付フィールドに対して。
## ステップ3: CSVファイルを読み込んで読み込む
ロードオプションが設定されたので、CSVファイルを`Aspose.Cells.Workbook`物体。
### 3.1 CSVファイルを読み込む
CSVファイルをファイルパスと設定されたパスを渡して読み込みます。`TxtLoadOptions`に`Workbook`コンストラクタ：
```csharp
string sourceDir = "Your Document Directory";
Workbook oExcelWorkBook = new Aspose.Cells.Workbook(sourceDir + "samplePreferredParser.csv", oTxtLoadOptions);
```
この手順では、CSV データが完全に機能する Excel ワークブックに変換され、各値は指定されたルールに従って解析されます。
## ステップ4: セルデータにアクセスして表示する
CSV がワークブックに読み込まれたら、データの操作を開始できます。たとえば、特定のセルの種類と値を印刷したい場合があります。
### 4.1 セルA1を取得して表示する
最初のセル (A1) を取得して、その値と型を表示してみましょう。
```csharp
Cell oCell = oExcelWorkBook.Worksheets[0].Cells["A1"];
Console.WriteLine("A1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
ここでは、`Type`プロパティはデータ型（`String`または`DateTime` ）、 そして`DisplayStringValue`フォーマットされた値を返します。
### 4.2 セルB1を取得して表示する
同様に、B1 などの別のセルを取得して表示することもできます。
```csharp
oCell = oExcelWorkBook.Worksheets[0].Cells["B1"];
Console.WriteLine("B1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
このプロセスは、検査する必要があるセルの数だけ繰り返すことができます。
## ステップ5: ワークブックを保存する
データを操作した後、ワークブックを新しいファイルに保存したい場合があります。Aspose.Cellsでは、簡単な操作で簡単に保存できます。`Save`方法：
```csharp
string outputDir = "Your Document Directory";
oExcelWorkBook.Save(outputDir + "outputsamplePreferredParser.xlsx");
```
これにより、ワークブックが Excel ファイルとして保存され、適用したすべての書式設定とデータ解析が保持されます。
## 結論
Aspose.Cells for .NET で好みのパーサーを使用して CSV ファイルを開くことは、さまざまなデータ型を処理するための柔軟で強力な方法です。カスタム パーサーを作成し、読み込みオプションを構成することで、テキスト、日付、その他のカスタム形式を扱う場合でも、CSV ファイルが正確に必要な方法で解析されることを保証できます。このチュートリアルでは、プロジェクトでより複雑なデータ解析シナリオを処理できるようになりました。
## よくある質問
### Aspose.Cells for .NET のカスタム パーサーの目的は何ですか?
カスタム パーサーを使用すると、CSV ファイルを読み込むときに、テキストや日付などの特定のデータ型をどのように解析するかを定義できます。
### CSV ファイルで別の区切り文字を使用できますか?
はい、任意の文字を区切り文字として指定できます。`TxtLoadOptions.Separator`財産。
### CSV を読み込むときに Aspose.Cells でエンコードをどのように処理すればよいですか?
設定できるのは`Encoding`の所有物`TxtLoadOptions`UTF-8、ASCII などの任意のエンコード方式に変換します。
### CSV 内の日付形式が異なる場合はどうなりますか?
カスタム パーサーを使用して特定の日付形式を定義し、日付値が正しく解析されるようにすることができます。
### ワークブックを他の形式で保存できますか?
はい、Aspose.Cells を使用すると、XLSX、CSV、PDF などのさまざまな形式でワークブックを保存できます。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
