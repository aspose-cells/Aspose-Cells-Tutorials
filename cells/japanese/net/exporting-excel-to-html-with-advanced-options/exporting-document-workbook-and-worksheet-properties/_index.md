---
title: ドキュメントのワークブックとワークシートのプロパティを HTML 形式でエクスポートする
linktitle: ドキュメントのワークブックとワークシートのプロパティを HTML 形式でエクスポートする
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、Excel ドキュメント、ワークブック、ワークシートのプロパティを HTML にエクスポートする方法を学びます。簡単なステップバイステップ ガイドが含まれています。
weight: 11
url: /ja/net/exporting-excel-to-html-with-advanced-options/exporting-document-workbook-and-worksheet-properties/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ドキュメントのワークブックとワークシートのプロパティを HTML 形式でエクスポートする

## 導入

スプレッドシートを扱う場合、共有、保存、またはプレゼンテーションのために Excel ファイルをさまざまな形式に変換する必要があることがよくあります。一般的なタスクの 1 つは、ワークブックとワークシートのプロパティを HTML 形式にエクスポートすることです。この記事では、Aspose.Cells for .NET を使用してこれを実現する方法について説明します。コーディングや Aspose ライブラリを初めて使用する場合でも心配はいりません。わかりやすいように、手順ごとに説明します。

## 前提条件

コードに進む前に、開始するために必要なものがすべて揃っていることを確認しましょう。

1. .NET Framework: 開発環境が .NET Framework で設定されていることを確認してください。Aspose.Cells は、.NET Framework バージョン 4.8 までと互換性があります。
   
2.  Aspose.Cells for .NET: Aspose.Cellsがインストールされている必要があります。ライブラリは以下からダウンロードできます。[ダウンロードページ](https://releases.aspose.com/cells/net/). 

3. IDE: Visual Studio のような適切な統合開発環境 (IDE) を使用すると、コーディング作業が簡素化されます。

4. サンプルExcelファイル: テスト用に、次の名前のExcelファイルを用意してください。`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx`作業ディレクトリ内。

## パッケージのインポート

前提条件を説明したので、まずは C# プロジェクトに必要なパッケージをインポートしてみましょう。手順は次のとおりです。

### 新しいプロジェクトを作成する

- IDE を開いて、新しい C# プロジェクトを作成します。このタイプのタスクを実行するのに最適なコンソール アプリケーションを選択できます。

### Aspose.Cells NuGet パッケージを追加する

Aspose.Cells パッケージを追加するには、次の手順に従います。

- ソリューション エクスプローラーでプロジェクトを右クリックし、[NuGet パッケージの管理] を選択します。
- NuGet パッケージ マネージャーで、「Aspose.Cells」を検索してインストールします。
- このパッケージは、Excel ファイルの操作に必要なクラスとメソッドを提供します。

### 名前空間のインポート

メイン プログラム ファイルの先頭に、次の名前空間が含まれていることを確認します。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

これにより、`Workbook`そして`HtmlSaveOptions`例で使用するクラスです。

これで準備はすべて完了です。プロセスを簡単なステップに分解してみましょう。

## ステップ1: ファイルディレクトリを設定する

まず、入力ファイルと出力ファイルの配置場所を指定する必要があります。コードでは、次のようにディレクトリを初期化します。

```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory/";  //実際のパスを更新

//出力ディレクトリ
string outputDir = "Your Document Directory/";  //実際のパスを更新
```

- ソースディレクトリ: 入力Excelファイル(`sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx`）が格納されます。
- 出力ディレクトリ: 出力 HTML ファイルを保存するパスです。

## ステップ2: Excelファイルを読み込む

次に、Excelファイルをロードします。`Workbook`クラス：

```csharp
//サンプルExcelファイルを読み込む
Workbook workbook = new Workbook(sourceDir + "sampleExportDocumentWorkbookAndWorksheetPropertiesInHTML.xlsx");
```

- ワークブックインスタンス:`Workbook`コンストラクターは Excel ファイルへのファイル パスを受け取り、操作可能な新しいインスタンスを作成します。

## ステップ3: HTML保存オプションを設定する

次に、Excel データを HTML に保存する方法を指定します。

```csharp
// HTML保存オプションを指定する
HtmlSaveOptions options = new HtmlSaveOptions();

//ドキュメント、ワークブック、ワークシートのプロパティのエクスポートを禁止する
options.ExportDocumentProperties = false;
options.ExportWorkbookProperties = false;
options.ExportWorksheetProperties = false;
```

- HtmlSaveOptions: このクラスは、Excel ファイルを HTML に変換する方法を管理するのに役立ちます。
- いくつかのオプションを設定しました`false`HTML 出力にワークブックとワークシートのプロパティを含めたくないためです。

## ステップ4: すべてをHTMLにエクスポートする

これで、ワークブックを HTML 形式で保存する準備が整いました。

```csharp
// HTML保存オプションを使用してExcelファイルをHTMLにエクスポートします。
workbook.Save(outputDir + "outputExportDocumentWorkbookAndWorksheetPropertiesInHTML.html", options);
```

- の`Save`このメソッドは、出力 HTML ファイルのファイル パスと設定したオプションの 2 つのパラメータを取ります。これを実行すると、指定された出力ディレクトリに HTML ファイルが作成されます。

## ステップ5: コンソールフィードバック

最後に、プロセスが正常に完了したことを確認するために、コンソールにフィードバックを提供しましょう。

```csharp
Console.WriteLine("ExportDocumentWorkbookAndWorksheetPropertiesInHTML executed successfully.");
```

## 結論

これで、Aspose.Cells for .NET を使用してワークブックとワークシートのプロパティを HTML にエクスポートできました。環境の設定から Excel データのエクスポートまで、簡単なプロセスを実行できました。Aspose.Cells などのライブラリを使用する利点は、複雑なタスクを効率化して、開発者の作業を容易にできることです。これで、ブック全体を公開することなく、世界中の人々にワークブックを覗き見させるのと同じように、スプレッドシートを HTML でより広く共有できるようになりました。

## よくある質問

### Aspose.Cells for .NET をインストールするにはどうすればよいですか?  
NuGet パッケージ マネージャーを使用して、Visual Studio プロジェクトに NuGet 経由で Aspose.Cells ライブラリをインストールできます。

### HTML 出力をカスタマイズできますか?  
はい、Aspose.Cellsはさまざまなオプションを提供します。`HtmlSaveOptions` Excel ファイルを HTML に変換する方法をカスタマイズします。

### HTML エクスポートにドキュメントのプロパティを含める方法はありますか?  
設定できます`ExportDocumentProperties`, `ExportWorkbookProperties`、 そして`ExportWorksheetProperties`に`true`で`HtmlSaveOptions`それらを含めたい場合は。

### Excel ファイルを HTML 以外にどのような形式でエクスポートできますか?  
Aspose.Cells は、PDF、CSV、XML などさまざまな形式をサポートしています。

### 試用版はありますか？  
はい、Aspose.Cellsの無料試用版は以下から入手できます。[Webサイト](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
