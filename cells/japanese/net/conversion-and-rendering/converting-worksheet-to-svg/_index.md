---
title: .NET でワークシートを SVG に変換する
linktitle: .NET でワークシートを SVG に変換する
second_title: Aspose.Cells .NET Excel 処理 API
description: このステップバイステップ ガイドでは、Aspose.Cells for .NET を使用して Excel ワークシートを SVG に変換する方法を説明します。Excel を SVG に変換する .NET 開発者に最適です。
weight: 11
url: /ja/net/conversion-and-rendering/converting-worksheet-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でワークシートを SVG に変換する

## 導入

Excel ワークシートを SVG 形式に変換したい場合、ここは最適な場所です。Aspose.Cells for .NET は、開発者が Excel ファイルを操作し、広くサポートされている SVG (Scalable Vector Graphics) を含むさまざまな形式に変換できるようにする強力なツールです。このチュートリアルでは、.NET でワークシートを SVG に変換するプロセスをステップごとに詳しく説明するので、初心者でも簡単に理解できます。

## 前提条件

コードに進む前に、必要なものがすべて揃っていることを確認しましょう。

1.  .NET 用 Aspose.Cells: Aspose.Cells for .NETの最新バージョンをダウンロードしてインストールします。[Aspose.Cells for .NET](https://releases.aspose.com/cells/net/).
2. .NET 開発環境: Visual Studio またはその他の .NET IDE がインストールされている必要があります。
3. C# の基礎知識: C# に精通している必要がありますが、心配しないでください。すべてを明確に説明します。
4. Excel ファイル: SVG 形式に変換する Excel ファイルを用意します。

## 必要なパッケージのインポート

コーディング部分に進む前に、C# ファイルの先頭に必要な名前空間が含まれていることを確認してください。

```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Rendering;
```

これらのパッケージは、Aspose.Cells を操作し、SVG エクスポートなどのレンダリング オプションを処理するために必要です。

基本的な内容は説明したので、Excel ワークシートを SVG 画像に変換する実際の手順を説明します。

## ステップ1: ドキュメントディレクトリへのパスを設定する

まず最初に、Excel ファイルが保存されているフォルダーへのパスを定義する必要があります。コードでは、ファイルの読み込みと保存にディレクトリを参照するため、これは非常に重要です。

```csharp
//ドキュメントディレクトリへのパス
string dataDir = "Your Document Directory";
```

必ず交換してください`"Your Document Directory"`Excel ファイルが存在する実際のパスを入力します。

## ステップ2: Excelファイルを読み込む`Workbook`

次に、Excelファイルを`Workbook`クラス。`Workbook`クラスは、その中のすべてのワークシートを含む Excel ファイル全体を表します。

```csharp
string filePath = dataDir + "Template.xlsx";
Workbook book = new Workbook(filePath);
```

ここ、`"Template.xlsx"`は、作業中の Excel ファイルの名前です。このファイルが指定されたディレクトリに存在することを確認してください。存在しない場合は、エラーが発生します。

## ステップ3: SVG変換用の画像または印刷オプションを設定する

ワークシートをSVG形式に変換する前に、画像オプションを指定する必要があります。`ImageOrPrintOptions`クラスを使用すると、ワークシートの変換方法を制御できます。具体的には、`SaveFormat`に`SVG`各ワークシートが 1 ページに変換されていることを確認します。

```csharp
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.SaveFormat = SaveFormat.Svg;
imgOptions.OnePagePerSheet = true;
```

の`SaveFormat.Svg`オプションは出力形式がSVGになることを保証しますが、`OnePagePerSheet`各ワークシートが 1 ページにレンダリングされることを保証します。

## ステップ4: ワークブック内の各ワークシートを反復処理する

ここで、Excel ファイル内のすべてのワークシートをループする必要があります。各ワークシートは個別に変換されます。

```csharp
foreach (Worksheet sheet in book.Worksheets)
{
    //各ワークシートを1つずつ処理します
}
```

このループにより、ワークブックにワークシートがいくつあっても、各ワークシートが処理されるようになります。

## ステップ5: 作成する`SheetRender` Object for Rendering

各ワークシートごとに、`SheetRender`オブジェクト。このオブジェクトは、ワークシートを目的の画像形式 (この場合は SVG) に変換する役割を担います。

```csharp
SheetRender sr = new SheetRender(sheet, imgOptions);
```

の`SheetRender`オブジェクトは、変換するワークシートと、以前に定義した画像オプションの 2 つの引数を取ります。

## ステップ6: ワークシートをSVGに変換する

最後に、ループ内で各ワークシートをSVG形式に変換します。ネストされたループを使用してページを反復処理します（ただし、この場合、`OnePagePerSheet`オプション）。

```csharp
for (int i = 0; i < sr.PageCount; i++)
{
    //ワークシートをSVG画像形式で出力します。
    sr.ToImage(i, filePath + sheet.Name + i + ".out.svg");
}
```

このコードは、ワークシートを Excel ファイルと同じディレクトリに SVG ファイルとして保存します。各 SVG ファイルには、名前の競合を避けるために、ワークシート名とインデックス番号に従って名前が付けられます。

## 結論

これで完了です。Aspose.Cells for .NET を使用して、Excel ワークシートを SVG 形式に変換できました。このプロセスにより、ワークシートのレイアウトとデザインを維持しながら、SVG をサポートするあらゆるブラウザーやデバイス (ほぼすべて) で表示できるようになります。複雑な Excel ファイルでも単純なテーブルでも、この方法により、Web に適した形式でデータが美しくレンダリングされます。

## よくある質問

### SVG とは何ですか? また、なぜ使用する必要があるのですか?
SVG (Scalable Vector Graphics) は、品質を損なうことなく無制限に拡大縮小できる Web 対応の形式です。さまざまなサイズで表示する必要があるグラフ、図、画像に最適です。

### Aspose.Cells は大きな Excel ファイルを変換できますか?
はい、Aspose.Cells は大きな Excel ファイルを効率的に処理し、パフォーマンス上の大きな問題を起こすことなく SVG に変換できます。

### SVG に変換できるワークシートの数に制限はありますか?
いいえ、Aspose.Cells には複数のワークシートを変換するための固有の制限はありません。唯一の制約は、システムのメモリとパフォーマンスです。

### Aspose.Cells を使用するにはライセンスが必要ですか?
はい、Aspose.Cellsを本番環境で使用するためにライセンスが必要です。一時ライセンスを取得できます。[ここ](https://purchase.aspose.com/temporary-license/)または探索する[無料トライアル](https://releases.aspose.com/).

### SVG 出力をカスタマイズできますか?
はい、微調整できます`ImageOrPrintOptions`解像度やスケーリングなど、SVG 出力のさまざまな側面をカスタマイズします。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
