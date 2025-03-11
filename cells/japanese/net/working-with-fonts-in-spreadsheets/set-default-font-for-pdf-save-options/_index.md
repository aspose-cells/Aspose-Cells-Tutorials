---
title: PDF保存オプションのデフォルトフォントを設定する
linktitle: PDF保存オプションのデフォルトフォントを設定する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して PDF 保存オプションの既定のフォントを設定し、ドキュメントが常に完璧に表示されるようにする方法を学習します。
weight: 11
url: /ja/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF保存オプションのデフォルトフォントを設定する

## 導入
レポート、請求書、その他のドキュメントを PDF 形式で生成する場合、コンテンツが適切に表示されることが最も重要です。フォントは、ドキュメントの見た目と読みやすさを維持する上で重要な役割を果たします。ただし、Excel ファイルで使用したフォントが PDF を生成するシステムで使用できない場合はどうなるでしょうか。ここで Aspose.Cells for .NET が役立ちます。この強力なライブラリを使用すると、PDF 保存オプションの既定のフォントを設定できるため、ドキュメントをどこで開いても、プロフェッショナルで一貫した外観を実現できます。
## 前提条件
始める前に、以下のものを用意してください。
1. Visual Studio: コードを記述して実行するには、Visual Studio などの開発環境が必要です。
2.  Aspose.Cells for .NET: 最新バージョンは以下からダウンロードできます。[このリンク](https://releases.aspose.com/cells/net/)または、Visual Studio の NuGet パッケージ マネージャー経由でインストールすることもできます。
3. C# の基礎知識: C# の基礎を理解すると、コード例を理解しやすくなります。
4. サンプル Excel ファイル: テスト用にサンプル Excel ファイルを用意します。さまざまなフォントとスタイルを使用してファイルを作成し、Aspose.Cells が不足しているフォントをどのように処理するかを確認できます。
## パッケージのインポート
プロジェクトで Aspose.Cells を使用する前に、必要なパッケージをインポートする必要があります。手順は次のとおりです。
1. プロジェクトを開く: Visual Studio を起動し、既存のプロジェクトを開くか、新しいプロジェクトを作成します。
2. 参照の追加: ソリューション エクスプローラーでプロジェクトを右クリックし、「NuGet パッケージの管理」を選択します。
3. Aspose.Cells をインストールします。「Aspose.Cells」を検索し、「インストール」ボタンをクリックします。
4. Using ディレクティブを追加します。C# ファイルの先頭に、次の名前空間を含めます。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;
```
## ステップ1: ディレクトリを設定する
ファイルを操作する前に、ソース ディレクトリと出力ディレクトリを定義することが重要です。これにより、入力 Excel ファイルを見つけやすくなり、生成された出力ファイルを保存しやすくなります。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
//出力ディレクトリ
string outputDir = "Your Document Directory";
```
交換する`"Your Document Directory"`ディレクトリへの実際のパスを入力します。
## ステップ2: Excelファイルを開く
ディレクトリの設定が完了したので、作業したいExcelファイルを開いてみましょう。`Workbook` Aspose.Cells のクラスは、Excel ドキュメントを読み込むために使用されます。
```csharp
//Excelファイルを開く
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
ファイル名を実際のファイル名に置き換えてください。
## ステップ3: 画像レンダリングオプションを設定する
次に、Excelシートを画像形式に変換するためのレンダリングオプションを設定する必要があります。`ImageOrPrintOptions`画像の種類とデフォルトのフォントを指定します。
```csharp
// PNGファイル形式へのレンダリング
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
このコードスニペットでは、`CheckWorkbookDefaultFont`財産に`false`つまり、フォントが不足している場合は、代わりに指定されたデフォルト フォント (「Times New Roman」) が使用されます。
## ステップ4: シートを画像としてレンダリングする
さて、ワークブックの最初のシートをPNG画像としてレンダリングしてみましょう。`SheetRender`これを実現するためのクラスです。
```csharp
//最初のワークシートを画像にレンダリングする
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## ステップ5: 画像タイプを変更してTIFFにレンダリングする
同じシートをTIFFなどの異なる画像形式でレンダリングしたい場合は、`ImageType`プロパティを変更し、レンダリング プロセスを繰り返します。
```csharp
// TIFF形式に設定
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## ステップ6: PDF保存オプションを設定する
次に、PDF保存オプションを設定しましょう。`PdfSaveOptions`デフォルトのフォントを設定し、不足しているフォントをチェックすることを指定します。
```csharp
// PDF保存オプションを設定する
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## ステップ7: ワークブックをPDFとして保存する
保存オプションを設定したら、Excel ブックを PDF ファイルとして保存します。 
```csharp
//ワークブックをPDFに保存する
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## ステップ8: 実行を確認する
最後に、プロセスが正常に完了したことをユーザーに知らせることをお勧めします。これは、簡単なコンソール メッセージを使用して実現できます。
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## 結論
Aspose.Cells は、Excel ファイルの操作を処理するための柔軟で堅牢な方法を提供し、開発者が書式設定を維持したまま視覚的に魅力的なドキュメントを簡単に作成できるようにします。レポート、財務ドキュメント、またはその他の形式のデータ プレゼンテーションを作成する場合でも、フォント レンダリングを制御することで出力の品質を大幅に向上できます。
## よくある質問
### Aspose.Cells とは何ですか?
Aspose.Cells は、Microsoft Excel をインストールしなくても開発者が Excel ファイルを操作できるようにする強力な .NET ライブラリです。さまざまなファイル形式をサポートし、スプレッドシートを操作するための豊富な機能を提供します。
### Excel ファイルのデフォルトのフォントを設定するにはどうすればよいですか?
デフォルトのフォントを設定するには、`PdfSaveOptions`クラスを選択し、希望のフォント名を指定します。これにより、フォントが見つからない場合でも、指定したデフォルトのフォントがドキュメントで使用されます。
### Excel ファイルを PDF 以外の形式に変換できますか?
もちろんです! Aspose.Cells を使用すると、Excel ファイルを画像 (PNG、TIFF)、HTML、CSV などのさまざまな形式に変換できます。
### Aspose.Cells は無料で使用できますか?
Aspose.Cells は商用製品ですが、制限付きの試用版を無料でお試しいただけます。完全な機能を使用するには、ライセンスを購入する必要があります。
### Aspose.Cells のサポートはどこで見つかりますか?
 Aspose.Cellsのサポートについては、[Aspose フォーラム](https://forum.aspose.com/c/cells/9)では、他のユーザーや開発者と質問したり、洞察を共有したりできます。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
