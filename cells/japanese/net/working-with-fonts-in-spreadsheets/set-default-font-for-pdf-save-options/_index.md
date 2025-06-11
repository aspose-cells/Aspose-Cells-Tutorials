---
"description": "Aspose.Cells for .NET を使用して PDF 保存オプションの既定のフォントを設定し、ドキュメントが常に完璧に表示されるようにする方法を学習します。"
"linktitle": "PDF保存オプションのデフォルトフォントを設定する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "PDF保存オプションのデフォルトフォントを設定する"
"url": "/ja/net/working-with-fonts-in-spreadsheets/set-default-font-for-pdf-save-options/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# PDF保存オプションのデフォルトフォントを設定する

## 導入
レポート、請求書、その他のドキュメントをPDF形式で生成する場合、コンテンツの見栄えを完璧にすることが最も重要です。フォントは、ドキュメントの見た目の魅力と読みやすさを維持する上で重要な役割を果たします。しかし、Excelファイルで使用したフォントが、PDFを生成するシステムで利用できない場合はどうすればよいでしょうか？そこでAspose.Cells for .NETが役立ちます。この強力なライブラリを使えば、PDF保存オプションのデフォルトフォントを設定できるため、どこで開いてもドキュメントの見栄えがプロフェッショナルで統一された状態を保つことができます。
## 前提条件
始める前に、次のものを用意してください。
1. Visual Studio: コードを記述して実行するには、Visual Studio などの開発環境が必要です。
2. Aspose.Cells for .NET: 最新バージョンは以下からダウンロードできます。 [このリンク](https://releases.aspose.com/cells/net/)または、Visual Studio の NuGet パッケージ マネージャーを使用してインストールすることもできます。
3. C# の基礎知識: C# の基礎を理解すると、コード例を理解するのに役立ちます。
4. サンプルExcelファイル：テスト用にサンプルExcelファイルを用意してください。様々なフォントとスタイルでサンプルファイルを作成し、Aspose.Cellsが不足しているフォントをどのように処理するかを確認できます。
## パッケージのインポート
プロジェクトでAspose.Cellsを使用する前に、必要なパッケージをインポートする必要があります。手順は以下のとおりです。
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
ファイルを操作する前に、ソースディレクトリと出力ディレクトリを定義することが重要です。これにより、入力Excelファイルの場所を特定し、生成された出力ファイルを保存しやすくなります。
```csharp
// ソースディレクトリ
string sourceDir = "Your Document Directory";
// 出力ディレクトリ
string outputDir = "Your Document Directory";
```
交換する `"Your Document Directory"` ディレクトリへの実際のパスを入力します。
## ステップ2: Excelファイルを開く
ディレクトリの設定が完了したら、作業したいExcelファイルを開いてみましょう。 `Workbook` Aspose.Cells のクラスは、Excel ドキュメントを読み込むために使用されます。
```csharp
// Excelファイルを開く
Workbook workbook = new Workbook(sourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");
```
ファイル名を実際のファイル名に置き換えてください。
## ステップ3: 画像レンダリングオプションを設定する
次に、Excelシートを画像形式に変換するためのレンダリングオプションを設定する必要があります。 `ImageOrPrintOptions`画像の種類とデフォルトのフォントを指定します。
```csharp
// PNGファイル形式へのレンダリング
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false;
imgOpt.DefaultFont = "Times New Roman";
```
このコードスニペットでは、 `CheckWorkbookDefaultFont` 財産に `false`つまり、フォントが不足している場合は、指定されたデフォルトのフォント (「Times New Roman」) が代わりに使用されます。
## ステップ4: シートを画像としてレンダリングする
さて、ワークブックの最初のシートをPNG画像としてレンダリングしてみましょう。 `SheetRender` これを実現するためのクラスです。
```csharp
// 最初のワークシートを画像としてレンダリングする
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```
## ステップ5: 画像の種類を変更してTIFFにレンダリングする
同じシートをTIFFのような別の画像形式でレンダリングしたい場合は、 `ImageType` プロパティを設定し、レンダリング プロセスを繰り返します。
```csharp
// TIFF形式に設定
imgOpt.ImageType = Drawing.ImageType.Tiff;
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```
## ステップ6: PDF保存オプションを設定する
次に、PDF保存オプションを設定しましょう。 `PdfSaveOptions`、デフォルトのフォントを設定し、不足しているフォントを確認することを指定します。
```csharp
// PDF保存オプションを設定する
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false;
```
## ステップ7: ワークブックをPDFとして保存する
保存オプションを設定したら、Excel ブックを PDF ファイルとして保存します。 
```csharp
// ワークブックをPDFに保存する
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```
## ステップ8: 実行の確認
最後に、プロセスが正常に完了したことをユーザーに知らせることをお勧めします。これは、シンプルなコンソールメッセージを使用することで実現できます。
```csharp
Console.WriteLine("SetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions executed successfully.\r\n");
```
## 結論
Aspose.Cellsは、Excelファイルの操作を柔軟かつ堅牢に処理する方法を提供します。これにより、開発者は書式設定を維持しながら、視覚的に魅力的なドキュメントを簡単に作成できます。レポート、財務書類、その他のデータプレゼンテーションを作成する場合でも、フォントレンダリングを制御できれば、出力品質を大幅に向上させることができます。
## よくある質問
### Aspose.Cells とは何ですか?
Aspose.Cellsは、Microsoft ExcelをインストールすることなくExcelファイルを操作できる強力な.NETライブラリです。様々なファイル形式をサポートし、スプレッドシート操作のための豊富な機能を提供します。
### Excel ファイルのデフォルトのフォントを設定するにはどうすればよいですか?
デフォルトのフォントを設定するには、 `PdfSaveOptions` クラスにフォント名を指定してください。これにより、フォントが見つからない場合でも、指定したデフォルトフォントがドキュメントで使用されます。
### Excel ファイルを PDF 以外の形式に変換できますか?
もちろんです！Aspose.Cells を使用すると、Excel ファイルを画像（PNG、TIFF）、HTML、CSV などのさまざまな形式に変換できます。
### Aspose.Cells は無料で使用できますか?
Aspose.Cellsは商用製品ですが、機能制限付きの無料トライアル版をお試しいただけます。全機能をご利用いただくには、ライセンスをご購入いただく必要があります。
### Aspose.Cells のサポートはどこで見つかりますか?
Aspose.Cellsのサポートについては、 [Asposeフォーラム](https://forum.aspose.com/c/cells/9)では、他のユーザーや開発者と質問したり、意見を共有したりすることができます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}