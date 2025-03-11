---
title: チャートにテキストボックスコントロールを追加する
linktitle: チャートにテキストボックスコントロールを追加する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して Excel のグラフに TextBox を追加する方法を学びます。データの視覚化を簡単に強化できます。
weight: 12
url: /ja/net/inserting-controls-in-charts/add-textbox-control-to-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# チャートにテキストボックスコントロールを追加する

## 導入

Excel で動的で視覚的に魅力的なグラフを作成することは、データを効果的に表現する素晴らしい方法です。グラフに TextBox を追加するという便利な機能を使用できます。Aspose.Cells for .NET を使用すると、この作業が簡単かつ楽しくなります。このガイドでは、グラフに TextBox を統合するプロセスを段階的に説明します。熟練した開発者でも、初心者でも、このチュートリアルでは Excel グラフを強化するために必要なすべてのツールが提供されます。さあ、始める準備はできていますか?

## 前提条件

コーディングを始める前に、準備しておくべきことがいくつかあります。

- C# の基本的な理解: C# プログラミングの基礎を理解していると役立ちます。心配しないでください。専門家である必要はなく、構文を操作できるだけで十分です。
-  Aspose.Cellsライブラリのインストール: Aspose.Cells for .NETライブラリがインストールされていることを確認してください。ダウンロードはこちらから行えます。[ここ](https://releases.aspose.com/cells/net/)まだお持ちでない場合は、ぜひご覧ください。
- Visual Studio: Visual Studio または .NET フレームワークに使用する IDE に精通していることが必須です。
- 既存の Excel ファイル: この例では、「sampleAddingTextBoxControlInChart.xls」という名前の既存の Excel ファイルを使用します。ファイルを作成することも、サンプルをダウンロードすることもできます。

準備がすべて整ったので、コーディングの部分に進みましょう。

## パッケージのインポート

まず最初に、必要な Aspose.Cells 名前空間を C# プロジェクトにインポートする必要があります。これは、コード ファイルの先頭に次の行を含めることで簡単に実行できます。

```csharp
using System;
using System.IO;

using Aspose.Cells;
using System.Drawing;
```

## ステップ1: ソースディレクトリと出力ディレクトリを定義する

Excel ファイルで作業を始める前に、入力ファイルの場所と出力ファイルの保存場所を定義することが重要です。これにより、プロジェクトを整理しやすくなります。

```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";

//出力ディレクトリ
string outputDir = "Your Output Directory";
```
交換する`"Your Document Directory"`そして`"Your Output Directory"`システム上の実際のパスを使用します。

## ステップ2: 既存のExcelファイルを開く

次に、変更したいグラフが含まれている Excel ファイルを開く必要があります。これにより、グラフを取得して変更できるようになります。

```csharp
//既存のファイルを開きます。
Workbook workbook = new Workbook(sourceDir + "sampleAddingTextBoxControlInChart.xls");
```
この行は、指定されたファイルを使用して新しい Workbook オブジェクトを初期化します。

## ステップ3: ワークシートのグラフにアクセスする

Excel のグラフはワークシート内に保存されるため、まずワークシートにアクセスして、目的のグラフを取得する必要があります。この例では、最初のワークシートの最初のグラフにアクセスします。

```csharp
//最初のシートでデザイナーチャートを取得します。
Worksheet sheet = workbook.Worksheets[0];
Aspose.Cells.Charts.Chart chart = sheet.Charts[0];
```
インデックス値を変更することで、ファイルに複数のワークシートやグラフがある場合に、異なるワークシートやグラフを選択できます。

## ステップ4: チャートに新しいテキストボックスを追加する

これで、TextBox を追加する準備ができました。作成時に位置とサイズを指定します。

```csharp
//グラフに新しいテキストボックスを追加します。
Aspose.Cells.Drawing.TextBox textbox0 = chart.Shapes.AddTextBoxInChart(400, 1100, 350, 2550);
```
このコマンドでは、パラメータによってチャート内の TextBox の位置 (x、y) とサイズ (幅、高さ) が定義されます。特定のレイアウトのニーズに応じてこれらの値を調整します。

## ステップ5: テキストボックスのテキストを設定する

TextBox を配置したら、コンテンツを入力します。チャートに必要と思われるテキストを追加できます。

```csharp
//テキストを入力してください。
textbox0.Text = "Sales By Region";
```
「地域別売上」を、データに関連する任意のテキストに置き換えてください。

## ステップ6: テキストボックスのプロパティを調整する

それでは、TextBox の見栄えを良くしてみましょう。フォントの色、サイズ、スタイルなど、さまざまなプロパティをカスタマイズできます。

```csharp
//フォントの色を設定します。
textbox0.Font.Color = Color.Maroon; //希望の色に変更

//フォントを太字に設定します。
textbox0.Font.IsBold = true;

//フォントサイズを設定します。
textbox0.Font.Size = 14;

//フォント属性を斜体に設定します。
textbox0.Font.IsItalic = true;
```

これらの各行は TextBox 内のテキストの外観を変更し、視認性と魅力を高めます。

## ステップ7: テキストボックスの外観をフォーマットする

また、テキスト ボックスの背景と境界線をフォーマットすることも重要です。これにより、チャート上でテキスト ボックスが目立つようになります。

```csharp
//テキストボックスの塗りつぶし形式を取得します。
Aspose.Cells.Drawing.FillFormat fillformat = textbox0.Fill;

//テキスト ボックスの線の書式タイプを取得します。
Aspose.Cells.Drawing.LineFormat lineformat = textbox0.Line;

//線の太さを設定します。
lineformat.Weight = 2;

//ダッシュスタイルを実線に設定します。
lineformat.DashStyle = Aspose.Cells.Drawing.MsoLineDashStyle.Solid;
```

これらのオプションを使用すると、TextBox の背景の塗りつぶしを設定し、その境界をカスタマイズできます。

## ステップ8: 変更したExcelファイルを保存する

最後のステップは、新しい Excel ファイルに加えた変更を保存することです。これにより、元のファイルはそのまま残ります。

```csharp
// Excel ファイルを保存します。
workbook.Save(outputDir + "outputAddingTextBoxControlInChart.xls");
```
交換する`"outputAddingTextBoxControlInChart.xls"`好きなファイル名で保存してください。

## 結論

おめでとうございます! Aspose.Cells for .NET を使用して、グラフに TextBox コントロールを正常に追加しました。このシンプルですが効果的な変更により、グラフの情報量が増え、視覚的に魅力的になります。データ表現は効果的なコミュニケーションの鍵であり、Aspose などのツールを使用すると、最小限の労力でプレゼンテーションを強化できます。

## よくある質問

### Aspose.Cells for .NET とは何ですか?
Aspose.Cells for .NET は、Microsoft Excel に依存せずに Excel ファイルを作成、操作、変換するための強力なライブラリです。

### 1 つのグラフに複数のテキスト ボックスを追加できますか?
はい。異なる位置で TextBox の作成手順を繰り返すことで、必要な数の TextBox を追加できます。

### Aspose.Cells は無料で使用できますか?
Aspose.Cellsは有料のライブラリですが、無料試用版を以下からダウンロードできます。[ここ](https://releases.aspose.com/).

### Aspose.Cells に関する詳細なドキュメントはどこで見つかりますか?
包括的なドキュメントにアクセスできます[ここ](https://reference.aspose.com/cells/net/).

### 問題が発生した場合、どうすればサポートを受けることができますか?
 Asposeサポートフォーラムを通じてサポートを受けることができます[ここ](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
