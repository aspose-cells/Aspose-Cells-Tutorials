---
title: .NET でプログラム的に出力 HTML に HTML CrossType を指定する
linktitle: .NET でプログラム的に出力 HTML に HTML CrossType を指定する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET で HTML CrossType を指定する方法を学びます。ステップバイステップのチュートリアルに従って、Excel ファイルを正確に HTML に変換します。
weight: 17
url: /ja/net/converting-excel-files-to-other-formats/specifying-html-crosstype-in-output-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的に出力 HTML に HTML CrossType を指定する

## 導入
.NET アプリケーションで Excel ファイルを HTML に変換する場合、出力で相互参照を処理する方法を指定する必要がある場合があります。Aspose.Cells for .NET の HtmlSaveOptions クラスには、変換プロセスを制御するためのさまざまな設定が用意されており、そのオプションの 1 つが HtmlCrossType です。このチュートリアルでは、Excel ファイルを HTML 形式にエクスポートするときに、プログラムで HTML 相互参照を指定する方法について説明します。 
## 前提条件
コードに進む前に、次のものを用意してください。
-  Aspose.Cells for .NET: プロジェクトにAspose.Cellsライブラリがインストールされていることを確認してください。[Aspose ウェブサイト](https://releases.aspose.com/cells/net/).
- Visual Studio: Visual Studio またはその他の .NET 開発環境の動作するインストール。
- C# の基礎知識: C# プログラミングに精通していると、例をよりよく理解するのに役立ちます。
- サンプルExcelファイル: サンプルExcelファイルを用意します。この例では、`sampleHtmlCrossStringType.xlsx`.
## パッケージのインポート
まず、必要な Aspose.Cells 名前空間をインポートする必要があります。手順は次のとおりです。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
これをステップごとに分解して、簡単に理解して、自分のプロジェクトにこの機能を実装できるようにしましょう。
## ステップ1: ソースディレクトリと出力ディレクトリを定義する
まず、ソース Excel ファイルのディレクトリと、出力 HTML ファイルを保存する場所を設定する必要があります。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
//出力ディレクトリ
string outputDir = "Your Document Directory";
```
## ステップ2: サンプルExcelファイルを読み込む
次に、サンプルExcelファイルを`Workbook`オブジェクト。ここからすべての魔法が始まります。
```csharp
//サンプルExcelファイルを読み込む
Workbook wb = new Workbook(sourceDir + "sampleHtmlCrossStringType.xlsx");
```
ここで、`"Your Document Directory"`Excel ファイルが配置されている実際のパスを入力します。この行は Excel ファイルをメモリに読み込み、操作できるようにします。
## ステップ3: HTML保存オプションを指定する
さて、インスタンスを作成します`HtmlSaveOptions`これにより、Excel ファイルを HTML に変換する方法を設定できます。
```csharp
// HTMLクロスタイプを指定する
HtmlSaveOptions opts = new HtmlSaveOptions();
opts.HtmlCrossStringType = HtmlCrossType.Default;
```
このステップでは、`HtmlCrossStringType`に`HtmlCrossType.Default`これは、出力 HTML で相互参照を処理するために使用できるオプションの 1 つです。
## ステップ4: 必要に応じてクロスタイプを変更する
異なるタイプを指定できます`HtmlCrossStringType`要件に応じて、使用できるさまざまなオプションを以下に示します。
- `HtmlCrossType.Default`: デフォルトのクロスタイプ。
- `HtmlCrossType.MSExport`: MS Excel のような動作で HTML をエクスポートします。
- `HtmlCrossType.Cross`: 相互参照を作成します。
- `HtmlCrossType.FitToCell`: 相互参照をセルの寸法に適合させます。
変更することができます`HtmlCrossStringType`このような：
```csharp
opts.HtmlCrossStringType = HtmlCrossType.MSExport;
//または
opts.HtmlCrossStringType = HtmlCrossType.Cross;
//または
opts.HtmlCrossStringType = HtmlCrossType.FitToCell;
```
## ステップ5: 出力HTMLファイルを保存する
オプションを設定したら、変換したHTMLファイルを保存します。`Save`あなたの`Workbook`物体：
```csharp
//出力HTML
wb.Save(outputDir + "out" + opts.HtmlCrossStringType + ".htm", opts);
```
ここでは、出力ファイルに次の名前を付けています。`HtmlCrossStringType`設定しました。これにより、変換にどのクロスタイプが使用されたかを簡単に識別できます。
## ステップ6: 実行が成功したことを確認する
最後に、操作が成功したことを確認するのは常に良い習慣です。コンソールにメッセージを出力できます。
```csharp
Console.WriteLine("SpecifyHtmlCrossTypeInOutputHTML executed successfully.\r\n");
```
これにより、プロセスがエラーなしで完了したことが通知されます。
## 結論
これで完了です。Aspose.Cells を使用して、.NET での Excel エクスポートの HTML クロス タイプを正常に指定できました。この機能は、HTML 出力で特定の書式設定や参照を維持し、変換されたドキュメントが要件を満たすようにする必要がある場合に特に便利です。
## よくある質問
### Aspose.Cells の HtmlCrossType とは何ですか?  
HtmlCrossType は、HTML 変換中に Excel ファイル内の相互参照を処理する方法を定義します。Default、MSExport、Cross、FitToCell などのオプションを選択できます。
### Aspose.Cells を無料で使用できますか?  
 Aspose.Cellsは無料試用版を提供しています。こちらからダウンロードできます。[Webサイト](https://releases.aspose.com/).
### .NET プロジェクトに Aspose.Cells をインストールするにはどうすればよいですか?  
次のコマンドを実行すると、Visual Studio の NuGet パッケージ マネージャー経由で Aspose.Cells をインストールできます。`Install-Package Aspose.Cells`.
### Aspose.Cells のドキュメントはどこにありますか?  
 Aspose.Cellsに関する包括的なドキュメントが見つかります[ここ](https://reference.aspose.com/cells/net/).
### HTML ファイルの保存中にエラーが発生した場合はどうすればよいですか?  
ディレクトリ パスが正しいこと、および出力ディレクトリへの書き込み権限があることを確認してください。問題が解決しない場合は、Aspose サポート フォーラムでヘルプを確認してください。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
