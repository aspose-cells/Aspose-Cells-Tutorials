---
title: MS Excel で選択された色をプログラムで計算する
linktitle: MS Excel で選択された色をプログラムで計算する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、MS Excel によって選択された色を計算する方法を学びます。このステップ バイ ステップ ガイドに従って、プログラムで Excel の条件付き書式設定の色にアクセスします。
weight: 10
url: /ja/net/color-settings-and-customization-in-excel/compute-color-chosen-by-ms-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# MS Excel で選択された色をプログラムで計算する

## 導入
Excel ファイルで作業していて、特定の色がどのように自動的に書式設定に選択されるのか疑問に思ったことはありませんか? あなただけではありません。Excel の条件付き書式設定は、特に Excel が割り当てた色を正確に抽出しようとすると、少し謎めいたものになります。でも、心配しないでください。私たちがお手伝いします! このチュートリアルでは、Aspose.Cells for .NET を使用して、MS Excel によって選択された色をプログラムで計算する方法について詳しく説明します。手順を 1 つ 1 つ説明していくので、簡単に理解して自分のプロジェクトに適用できます。さあ、始めましょう!
## 前提条件
コードに進む前に、このチュートリアルを実行するために必要なものについて説明しましょう。
-  Aspose.Cells for .NETがインストールされている。まだインストールしていない場合は、[ここからダウンロード](https://releases.aspose.com/cells/net/).
- C# および .NET フレームワークに関する実用的な知識。
- 条件付き書式が適用されたサンプル Excel ファイル (Book1.xlsx)。
ライセンスをお持ちでない場合は、Aspose.Cells for .NETの無料トライアルを試すこともできます。トライアル版を入手してください。[ここ](https://releases.aspose.com/).
## パッケージのインポート
コーディングを始める前に、すべてがスムーズに実行されるように、必要なパッケージをインポートする必要があります。プロジェクトに次の名前空間を含めるようにしてください。
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using System;
```
これらのインポートにより、メインの Aspose.Cells クラスと、色を処理するための .NET のネイティブ システム描画ライブラリにアクセスできるようになります。

準備がすべて整ったので、このタスクをわかりやすいステップに分解してみましょう。
## ステップ1: ワークブックオブジェクトを設定する
まず最初にインスタンス化する必要があるのは`Workbook`オブジェクトを作成し、作業する Excel ファイルを読み込みます。ここから旅が始まります。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
//ワークブックオブジェクトをインスタンス化し、テンプレートファイルを開きます
Workbook workbook = new Workbook(dataDir + "Book1.xlsx");
```
このステップでは、`Workbook` Aspose.Cellsのクラス。`Workbook`クラスは Excel ファイルを表し、ファイルへのパスを指定することで、簡単に読み込んでさらに操作することができます。
## ステップ2: 最初のワークシートにアクセスする
ワークブックが読み込まれたら、色を抽出する特定のワークシートにアクセスする必要があります。この例では、最初のシートを操作します。
```csharp
//最初のワークシートを入手する
Worksheet worksheet = workbook.Worksheets[0];
```
ここでは、ワークブックの最初のワークシートを`Worksheets[0]`インデックス。Aspose.Cells を使用すると、インデックスまたは名前で Excel ファイル内の任意のワークシートにアクセスできます。
## ステップ3: 関心のあるセルを選択する
次に、ワークシート内の特定のセルを選択します。このチュートリアルでは、セル「A1」に焦点を当てますが、条件付き書式が適用された任意のセルを選択できます。
```csharp
// A1セルを取得する
Cell a1 = worksheet.Cells["A1"];
```
私たちは`Cells`プロパティを使用して、特定のセルをそのアドレスで参照します。この場合、このセルに適用された条件付き書式の結果を抽出するため、セル「A1」を選択しています。
## ステップ4: 条件付き書式設定の結果を取得する
ここで魔法が起こります! Aspose.Cells を使用して、選択したセルの条件付き書式設定の結果を取得します。Excel はこのようにして、色を含む書式設定を動的に計算します。
```csharp
//条件付き書式の結果オブジェクトを取得する
ConditionalFormattingResult cfr1 = a1.GetConditionalFormattingResult();
```
の`GetConditionalFormattingResult()`このステップでは、メソッドが重要です。このメソッドは、セルに適用された条件付き書式設定の結果を含むオブジェクトを返します。ここで、Excel が使用する色情報を利用し始めます。
## ステップ5: ColorScaleResultにアクセスする
条件付き書式の結果が得られたら、さらに詳しく調べて、Excel がこの特定のセルに対して使用したカラー スケールにアクセスできます。
```csharp
// ColorScaleの結果カラーオブジェクトを取得する
Color c = cfr1.ColorScaleResult;
```
Excel の条件付き書式設定では、多くの場合、カラー スケールが使用されます。この行を使用すると、条件付き書式設定ルールに基づいて適用された結果の色を抽出できます。
## ステップ6: 色情報を出力する
最後に、Excel で適用された色を確認します。ARGB 値と色名の両方を含む、わかりやすい形式で色の詳細を印刷してみましょう。
```csharp
//色を読む
Console.WriteLine(c.ToArgb().ToString());
Console.WriteLine(c.Name);
```
の`ToArgb()`メソッドはARGB形式（アルファ、赤、緑、青）で色を返しますが、`Name`プロパティは、より人間が読みやすい形式で色の名前を提供します。これらの色の詳細を使用して、他のアプリケーションで色を一致させたり、Excel ファイルをプログラムで変更したりできます。

## 結論
これで完了です。これらの手順に従うことで、Aspose.Cells for .NET を使用して MS Excel で選択された色をプログラムで計算する方法を学習しました。このアプローチは、複雑な条件付き書式を扱う場合など、Excel ベースのタスクを自動化するのに非常に役立ちます。これで、次に Excel で不思議な色に遭遇したときに、その秘密を明らかにする方法が正確にわかるようになります。
## よくある質問
### Aspose.Cells を使用してプログラムで条件付き書式を適用できますか?
はい、Aspose.Cells を使用すると、Excel ファイルの条件付き書式をプログラムで適用、変更、削除することができます。
### Aspose.Cells はすべてのバージョンの Excel をサポートしていますか?
もちろんです! Aspose.Cells は、Excel 97-2003 (XLS)、Excel 2007-2019/365 (XLSX) のほか、PDF、HTML、CSV などの形式もサポートしています。
### Aspose.Cells は .NET 以外のプラットフォームでも使用できますか?
はい、Aspose.CellsはJava、Cなどさまざまなプラットフォームで利用できます。++、Java 経由の Android です。
### Aspose.Cells の無料トライアルを入手するにはどうすればよいですか?
 Aspose.Cells for .NETの無料トライアルは以下からダウンロードできます。[ここ](https://releases.aspose.com/).
### Aspose.Cells を使用して大きな Excel ファイルを処理するにはどうすればよいでしょうか?
Aspose.Cells は、大きなファイルを扱う場合でもパフォーマンスが最適化されています。ストリーミング API を利用して、大きなデータを効率的に処理できます。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
