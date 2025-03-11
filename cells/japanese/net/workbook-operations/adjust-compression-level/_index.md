---
title: ワークブックの圧縮レベルを調整する
linktitle: ワークブックの圧縮レベルを調整する
second_title: Aspose.Cells .NET Excel 処理 API
description: このステップバイステップ ガイドでは、Aspose.Cells for .NET を使用して Excel ブックの圧縮レベルを調整する方法を説明します。ファイル管理を最適化します。
weight: 14
url: /ja/net/workbook-operations/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ワークブックの圧縮レベルを調整する

## 導入
大きな Excel ファイルの管理に関しては、圧縮が大きな効果を発揮します。ストレージ スペースを節約できるだけでなく、ファイル転送も高速かつ効率的になります。Aspose.Cells for .NET を使用している場合は、ワークブックの圧縮レベルを簡単に調整できます。このガイドでは、コードの各部分とその仕組みを理解できるように、プロセスを段階的に説明します。
## 前提条件
コードに進む前に、いくつかの前提条件を満たす必要があります。
1. C# の基礎知識: C# プログラミングに精通していると、コード スニペットをよりよく理解できるようになります。
2.  Aspose.Cellsライブラリ: Aspose.Cellsライブラリがインストールされている必要があります。ここからダウンロードできます。[ここ](https://releases.aspose.com/cells/net/).
3. Visual Studio: コードを実行するには、Visual Studio のような開発環境が必要になります。
4. .NET Framework: プロジェクトが互換性のあるバージョンの .NET Framework を使用して設定されていることを確認します。
## パッケージのインポート
まず、C# プロジェクトに必要なパッケージをインポートする必要があります。手順は次のとおりです。
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
これらのパッケージは、Aspose.Cellsライブラリを使用してExcelファイルを操作するために不可欠です。`Aspose.Cells`名前空間にはExcelファイルを操作するために必要なすべてのクラスが含まれていますが、`Aspose.Cells.Xlsb` XLSB 形式でファイルを保存するためのオプションを提供します。
ここで、ワークブックの圧縮レベルを調整するプロセスを、管理しやすい手順に分解してみましょう。
## ステップ1: ソースディレクトリと出力ディレクトリを定義する
まず、ソース ファイルの場所と出力ファイルを保存する場所を指定する必要があります。これは、プログラムが作業に必要なファイルの場所を確実に認識するために重要です。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
交換する`"Your Document Directory"`ディレクトリへの実際のパスを入力します。これにより、プログラムは圧縮するファイルを見つけやすくなります。
## ステップ2: ワークブックを読み込む
次に、圧縮するワークブックを読み込みます。ここから魔法が始まります。
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
この行では、`Workbook`クラスを作成し、既存の Excel ファイルをロードします。ファイル名がソース ディレクトリにあるファイル名と一致していることを確認します。
## ステップ3: 保存オプションを設定する
次に、保存オプションを設定します。出力ファイルの圧縮タイプを設定します。 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
の`XlsbSaveOptions`クラスを使用すると、ワークブックを XLSB 形式で保存するときに、圧縮レベルなどのさまざまなオプションを指定できます。
## ステップ4: レベル1の圧縮時間を測定する
最初の圧縮レベルから始めましょう。この圧縮レベルでワークブックを保存するのにかかる時間を測定します。
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
ここでは、圧縮タイプをレベル 1 に設定し、ワークブックを保存して、経過時間を測定します。これにより、プロセスにかかる時間がわかります。
## ステップ5: レベル6の圧縮時間を測定する
次に、レベル 6 の圧縮がどのように機能するかを見てみましょう。
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
この手順は前の手順と似ていますが、圧縮レベルをレベル 6 に変更します。所要時間はワークブックの複雑さに応じて異なる場合があることに注意してください。
## ステップ6: レベル9の圧縮時間を測定する
最後に、最高の圧縮レベルでのパフォーマンスを確認してみましょう。
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
この手順では、圧縮レベルをレベル 9 に設定します。通常、このレベルではファイル サイズが最も大幅に削減されますが、処理に時間がかかる場合があります。
## ステップ7: 最終出力
すべての圧縮レベルを実行した後、プロセスが正常に完了したことを示すメッセージを出力できます。
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
この単純なコード行は、プログラムが問題なく実行を完了したことを確認します。
## 結論
Aspose.Cells for .NET を使用してワークブックの圧縮レベルを調整することは、ファイル サイズとパフォーマンスの面で大きなメリットをもたらす簡単なプロセスです。このガイドで説明されている手順に従うことで、アプリケーションに簡単に圧縮を実装し、Excel ファイル管理の効率を向上させることができます。
## よくある質問
### Aspose.Cells とは何ですか?  
Aspose.Cells は、開発者が Microsoft Excel を必要とせずに Excel ファイルを作成、操作、変換できるようにする .NET 用の強力なライブラリです。
### Aspose.Cells をインストールするにはどうすればよいですか?  
 Aspose.Cellsは以下からダウンロードしてインストールできます。[Aspose ウェブサイト](https://releases.aspose.com/cells/net/).
### どのような圧縮レベルが利用可能ですか?  
Aspose.Cells は、レベル 1 (最低圧縮) からレベル 9 (最高圧縮) までの複数の圧縮レベルをサポートします。
### Aspose.Cells を無料でテストできますか?  
はい！Aspose.Cellsの無料トライアルを入手できます[ここ](https://releases.aspose.com/).
### Aspose.Cells のサポートはどこで見つかりますか?  
ご質問やサポートについては、Aspose サポートフォーラムをご覧ください。[ここ](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
