---
"date": "2025-04-05"
"description": "Aspose.Cells for .NET でカスタムフォントを使用しながら、Excel ファイルを PNG、TIFF、PDF 形式に変換する方法を学びます。すべてのドキュメント変換で一貫したタイポグラフィを実現します。"
"title": "Aspose.Cells を使用して .NET でカスタム フォントを使用して Excel を PNG、TIFF、PDF にレンダリングする"
"url": "/ja/net/workbook-operations/render-excel-custom-fonts-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells for .NET を使用して Excel ファイルをカスタム フォントで PNG、TIFF、PDF にレンダリングする

## 導入

Excelファイルを画像やPDFに変換する際、フォントの整合性を維持することは、ブランドの一貫性を保つ上で非常に重要です。Aspose.Cells for .NETは、ドキュメント変換時にカスタムデフォルトフォントを指定できる堅牢なソリューションを提供します。

このチュートリアルでは、Aspose.Cells for .NET を使用して、カスタムデフォルトフォントを指定し、Excel ファイルを PNG、TIFF、PDF 形式に変換する方法を説明します。このチュートリアルは、以下の場合に最適です。
- レンダリングされたドキュメントでは一貫したタイポグラフィを目指します。
- 変換中にフォント設定をカスタマイズする必要があります。
- Aspose.Cells for .NET 内の構成オプションを調べたい。

環境を設定してこれらの機能をシームレスに実装しましょう。

### 前提条件

始める前に、次のものがあることを確認してください。
- **.NET環境**マシンにセットアップします (.NET Core または .NET Framework が推奨)。
- **Aspose.Cells for .NET ライブラリ**プロジェクトにインストールされました。
- **Excelファイル**変換するデータを含む Excel ブック。

### Aspose.Cells for .NET のセットアップ

まず、Aspose.Cells ライブラリをプロジェクトに追加します。

**.NET CLI の使用:**
```bash
dotnet add package Aspose.Cells
```

**パッケージマネージャーの使用:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

全機能にアクセスするためのライセンスを取得します。
- **無料トライアル**： 訪問 [Aspose 無料トライアル](https://releases.aspose.com/cells/net/) 最初のアクセス用。
- **一時ライセンス**入手先 [Aspose 一時ライセンス](https://purchase。aspose.com/temporary-license/).
- **購入**永久ライセンスについては、 [Aspose 購入](https://purchase。aspose.com/buy).

ライセンスを取得したら、アプリケーションで Aspose.Cells を初期化します。
```csharp
// Aspose.Cells のライセンスを設定します。
License license = new License();
license.SetLicense("path_to_your_license_file");
```

## 実装ガイド

### カスタムデフォルトフォントを使用したPNGへのレンダリング

ExcelワークシートをPNG形式でレンダリングし、カスタムデフォルトフォントを設定することで、見た目の一貫性を保つことができます。手順は以下のとおりです。

#### ステップ1: 画像オプションを設定する

画像出力のレンダリング オプションを構成します。
```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// ディレクトリを指定します。
string SourceDir = @"YOUR_SOURCE_DIRECTORY";
string outputDir = @"YOUR_OUTPUT_DIRECTORY";

// Excel ファイルを開きます。
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// 画像のレンダリング オプションを設定します。
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false; // ワークブック内の不足しているフォントにはカスタム フォントを使用します。
imgOpt.DefaultFont = "Times New Roman";
```

#### ステップ2: レンダリングして保存する

これらの設定を使用して、ワークシートを画像ファイルにレンダリングします。
```csharp
// 最初のワークシートを PNG 画像としてレンダリングします。
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```

### カスタムデフォルトフォントを使用したTIFFへのレンダリング

TIFF形式は高画質画像に最適です。ワークブック全体をTIFFファイルとしてレンダリングする方法は次のとおりです。

#### ステップ3: TIFFの画像オプションを設定する

TIFF 出力専用のレンダリング オプションを構成します。
```csharp
// 以前に定義したディレクトリを再利用して、Excel ファイルを開きます。
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// TIFF の画像レンダリング オプションを構成します。
imgOpt.ImageType = Drawing.ImageType.Tiff;
```

#### ステップ4: ワークブック全体をTIFFにレンダリングする

ワークブック全体を 1 つの TIFF ファイルに変換します。
```csharp
// ワークブックを TIFF 画像としてレンダリングします。
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```

### カスタムデフォルトフォントを使用したPDFへのレンダリング

フォントの一貫性を保ちながら Excel ブックを PDF として保存することは、プロフェッショナルなドキュメントを作成するために重要です。

#### ステップ5: PDF保存オプションを設定する

ファイルを PDF として保存するために必要なオプションを設定します。
```csharp
using Aspose.Cells;

// ワークブックを再度開きます。
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// PDF 保存オプションを設定します。
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false; // ワークブック内の不足しているフォントにはカスタム フォントを使用します。
```

#### ステップ6: PDFとして保存

ワークブックを PDF ドキュメントにエクスポートします。
```csharp
// ワークブックを PDF ファイルとして保存します。
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```

## 実用的なアプリケーション

- **ビジネスレポート**カスタム フォントを使用して、エクスポートされたすべてのレポートで一貫したブランド化を確保します。
- **文書アーカイブ**従来の Excel ファイルを PDF に変換し、統一された書体で簡単に共有およびアーカイブできるようにします。
- **グラフィックデザイン**プレゼンテーションやデザイン プロジェクト用に、Excel データの高解像度 TIFF イメージを作成します。

CRM プラットフォームやドキュメント管理ソリューションなどの他のシステムと統合すると、特定のトリガーまたはイベントに基づいてエクスポートを自動化することで、これらのユースケースをさらに強化できます。

## パフォーマンスに関する考慮事項

レンダリング プロセスを最適化することは非常に重要です。
- **メモリ管理**：処分する `Workbook`、 `SheetRender`、 そして `WorkbookRender` オブジェクトをすぐに削除してリソースを解放します。
- **バッチ処理**複数のファイルを扱う場合は、効率的な処理のためにバッチ処理を実装します。
- **非同期操作**可能な場合は非同期メソッドを利用して、アプリケーションの応答性を向上させます。

## 結論

Aspose.Cells for .NET を使用して、Excel ブックを PNG、TIFF、PDF 形式に変換し、カスタムデフォルトフォントを設定する方法を習得しました。この機能により、さまざまなプラットフォームや用途において、ドキュメントの視覚的な整合性が維持されます。

Aspose.Cellsが提供する追加機能を活用して、ドキュメント処理能力をさらに強化しましょう。詳細情報やサポートについては、 [Asposeフォーラム](https://forum。aspose.com/c/cells/9).

## FAQセクション

**1. Aspose.Cells for .NET とは何ですか?**
   — Aspose.Cells for .NET は、Excel ファイルをプログラムで管理および変換するための強力な機能を提供するライブラリです。

**2. Aspose.Cells を Web アプリケーションで使用できますか?**
   — はい、Aspose.Cells は ASP.NET またはその他の .NET ベースの Web アプリケーションに統合できます。

**3. レンダリング中に見つからないフォントをどのように処理しますか?**
   — 設定することで `CheckWorkbookDefaultFont` 偽に設定し、 `DefaultFont`を使用すると、元のフォントが利用できない場合でも、すべてのテキストで選択したフォントが使用されるようになります。

**4. PNG、TIFF、PDF 以外の形式もサポートされていますか?**
   — はい、Aspose.Cells は JPEG、BMP などのさまざまな画像形式をサポートし、広範なドキュメント変換機能を提供します。

**5. 大規模アプリケーションで Aspose.Cells を使用するためのベスト プラクティスは何ですか?**
   — 効率的なメモリ管理技術、複数のファイルを扱うためのバッチ処理を活用し、非同期操作を考慮してアプリケーションのパフォーマンスを向上させます。

## リソース
- **ドキュメント**： [Aspose.Cells ドキュメント](https://reference.aspose.com/cells/net/)
- **ダウンロード**： [Aspose.Cells リリース](https://releases.aspose.com/cells/net/)
- **購入**： [Aspose.Cellsを購入する](https://purchase.aspose.com/buy)
- **無料トライアル**： [Aspose.Cellsを無料でお試しください](https://releases.aspose.com/cells/net/)
- **一時ライセンス**： [一時ライセンスを取得する](https://purchase.aspose.com/temporary-license/) 


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}