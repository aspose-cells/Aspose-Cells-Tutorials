---
"description": "このステップバイステップガイドでは、Aspose.Cells for .NET を使用して Excel ブックの圧縮レベルを調整する方法を学びます。ファイル管理を最適化しましょう。"
"linktitle": "ワークブックの圧縮レベルを調整する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "ワークブックの圧縮レベルを調整する"
"url": "/ja/net/workbook-operations/adjust-compression-level/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ワークブックの圧縮レベルを調整する

## 導入
大容量のExcelファイルを管理する上で、圧縮は画期的な効果を発揮します。ストレージ容量を節約できるだけでなく、ファイル転送も高速化・効率化されます。Aspose.Cells for .NETをご利用の場合は、ワークブックの圧縮レベルを簡単に調整できます。このガイドでは、コードの各部分とその仕組みを理解できるよう、手順を追って解説します。
## 前提条件
コードに進む前に、いくつかの前提条件を満たす必要があります。
1. C# の基礎知識: C# プログラミングに精通していると、コード スニペットをよりよく理解できるようになります。
2. Aspose.Cellsライブラリ: Aspose.Cellsライブラリがインストールされている必要があります。ダウンロードはこちらから。 [ここ](https://releases。aspose.com/cells/net/).
3. Visual Studio: コードを実行するには、Visual Studio のような開発環境が必要になります。
4. .NET Framework: プロジェクトが互換性のあるバージョンの .NET Framework を使用して設定されていることを確認します。
## パッケージのインポート
まず、C#プロジェクトに必要なパッケージをインポートする必要があります。手順は以下のとおりです。
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
これらのパッケージは、Aspose.Cellsライブラリを使用してExcelファイルを操作するために不可欠です。 `Aspose.Cells` 名前空間にはExcelファイルを操作するために必要なすべてのクラスが含まれていますが、 `Aspose.Cells.Xlsb` XLSB 形式でファイルを保存するためのオプションを提供します。
ここで、ワークブック内の圧縮レベルを調整するプロセスを、管理しやすい手順に分解してみましょう。
## ステップ1: ソースディレクトリと出力ディレクトリを定義する
まず、ソースファイルの場所と出力ファイルの保存場所を指定する必要があります。これは、プログラムが処理に必要なファイルの場所を確実に認識するために非常に重要です。
```csharp
// ソースディレクトリ
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
交換する `"Your Document Directory"` ディレクトリへの実際のパスを入力してください。これにより、プログラムは圧縮したいファイルを見つけやすくなります。
## ステップ2: ワークブックを読み込む
次に、圧縮したいワークブックを読み込みます。ここから魔法が始まります！
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
この行では、 `Workbook` クラスを作成し、既存のExcelファイルを読み込みます。ファイル名がソースディレクトリにあるファイル名と一致していることを確認してください。
## ステップ3: 保存オプションを設定する
次は保存オプションの設定です。出力ファイルの圧縮形式を設定します。 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
その `XlsbSaveOptions` クラスを使用すると、ワークブックを XLSB 形式で保存するときに、圧縮レベルなどのさまざまなオプションを指定できます。
## ステップ4: レベル1の圧縮時間を測定する
まずは最初の圧縮レベルから始めましょう。この圧縮レベルでワークブックを保存するのにかかる時間を測定します。
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
ここでは、圧縮タイプをレベル1に設定し、ワークブックを保存して経過時間を測定します。これにより、処理にかかる時間がわかります。
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
この手順は前の手順と似ていますが、圧縮レベルをレベル 6 に変更します。ワークブックの複雑さに応じて、かかる時間が異なる場合があることに注意してください。
## ステップ6：レベル9の圧縮時間を測定する
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
## ステップ7：最終出力
すべての圧縮レベルを実行した後、プロセスが正常に完了したことを示すメッセージを出力できます。
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
この単純なコード行は、プログラムの実行が問題なく完了したことを確認します。
## 結論
Aspose.Cells for .NET を使用してワークブックの圧縮レベルを調整するのは簡単なプロセスであり、ファイルサイズとパフォーマンスの面で大きなメリットをもたらします。このガイドで概説されている手順に従うことで、アプリケーションに簡単に圧縮を実装し、Excelファイル管理の効率を向上させることができます。
## よくある質問
### Aspose.Cells とは何ですか?  
Aspose.Cells は、開発者が Microsoft Excel を必要とせずに Excel ファイルを作成、操作、変換できるようにする強力な .NET ライブラリです。
### Aspose.Cells をインストールするにはどうすればよいですか?  
Aspose.Cellsは以下からダウンロードしてインストールできます。 [Aspose ウェブサイト](https://releases。aspose.com/cells/net/).
### どのような圧縮レベルが利用可能ですか?  
Aspose.Cells は、レベル 1 (最低圧縮) からレベル 9 (最高圧縮) までの複数の圧縮レベルをサポートします。
### Aspose.Cells を無料でテストできますか?  
はい！Aspose.Cellsの無料トライアルをご利用いただけます [ここ](https://releases。aspose.com/).
### Aspose.Cells のサポートはどこで見つかりますか?  
ご質問やサポートについては、Aspose サポートフォーラムをご覧ください。 [ここ](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}