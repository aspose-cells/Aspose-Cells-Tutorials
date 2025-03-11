---
title: 圧縮レベルを調整する
linktitle: 圧縮レベルを調整する
second_title: Aspose.Cells for .NET API リファレンス
description: Aspose.Cells for .NET を使用して Excel ファイルの圧縮レベルを調整する方法を学びます。このステップ バイ ステップ ガイドを使用して、ファイル サイズを効率的に最適化します。
weight: 50
url: /ja/net/excel-workbook/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 圧縮レベルを調整する

## 導入

大きな Excel ファイルを扱う場合、効率的なストレージが鍵となります。ファイル サイズの最適化を目指す開発者でも、ファイル転送の高速化を目指すデータ アナリストでも、Aspose.Cells for .NET で圧縮レベルを調整する方法を理解することは大きな変化をもたらします。このガイドでは、Excel ファイルを保存するときに圧縮レベルを調整し、品質を犠牲にすることなくパフォーマンスを維持する手順を説明します。

## 前提条件

圧縮レベルの詳細に入る前に、始めるのに必要なものがすべて揃っていることを確認しましょう。

1. C# の基礎知識: C# プログラミングの基礎的な理解が必須です。変数、ループ、基本的なファイル操作に慣れていれば、問題ありません。
2. Aspose.Cells for .NET ライブラリ: Aspose.Cells ライブラリがインストールされていることを確認してください。[Webサイト](https://releases.aspose.com/cells/net/)始めたばかりの方は、無料トライアルをお試しください[ここ](https://releases.aspose.com/).
3. 開発環境: C# コードを記述して実行するための開発環境 (理想的には Visual Studio) をセットアップします。 
4. サンプル Excel ファイル: テスト用に、大きな Excel ファイルを用意します。ファイルを作成することも、既存のファイルを使用することもできますが、圧縮の効果を確認できる大きさであることを確認してください。

これらの前提条件が整ったら、始めましょう。

## パッケージのインポート

Excel ファイルを操作する前に、必要な名前空間をインポートする必要があります。これは、Aspose.Cells によって提供されるクラスとメソッドにアクセスできるようにするための重要なステップです。

### Aspose.Cells 名前空間をインポートする

```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```

このコードスニペットは、`Aspose.Cells` Excelファイルを操作するのに必要なすべてのクラスを含む名前空間。`Aspose.Cells.Xlsb`名前空間は、XLSB ファイル形式を処理するために特別に設計されています。

これですべての設定が完了したので、圧縮レベルを調整するプロセスを管理しやすいステップに分解してみましょう。異なる圧縮レベルでワークブックを保存し、各操作にかかる時間を測定します。 

## ステップ1: ディレクトリを設定する

まず最初に、ファイルを保存する場所を定義する必要があります。これには、入力ファイルのソース ディレクトリと圧縮ファイルの出力ディレクトリの指定が含まれます。

```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```

## ステップ2: ワークブックを読み込む

次に、圧縮する Excel ブックを読み込みます。ここで、大きな Excel ファイルを指定します。

```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```

この行は新しい`Workbook`オブジェクトを指定されたファイルに関連付けます。ファイル パスが正しいことを確認してください。そうでない場合、エラーが発生します。

## ステップ3: XLSBの保存オプションを作成する

さて、インスタンスを作成します`XlsbSaveOptions`これにより、圧縮レベルなど、ワークブックの保存方法を指定できます。

```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```

この行は、ワークブックを XLSB 形式で保存するために使用するオプションを準備します。

## ステップ4: 圧縮レベルの設定と測定

次は楽しい部分です。さまざまな圧縮レベルを使用してワークブックを保存し、各操作にかかる時間を測定します。 

### レベル 1 圧縮

最も低い圧縮レベルから始めましょう:

```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```

このスニペットでは、圧縮タイプをレベル 1 に設定し、ワークブックを保存して、かかった時間をログに記録します。 

### レベル6圧縮

次に、中程度の圧縮レベルを試してみます。

```csharp
options.CompressionType = OoxmlCompressionType.Level6;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```

今回は圧縮タイプをレベル6に設定して保存操作を繰り返します。

### レベル9圧縮

最後に、最高の圧縮レベルを使用して保存しましょう。

```csharp
options.CompressionType = OoxmlCompressionType.Level9;
watch = System.Diagnostics.Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```

この手順では、圧縮タイプをレベル 9 に設定します。これにより、ファイル サイズは最小になりますが、保存に時間がかかる可能性があります。

## ステップ5: 最終出力

上記の手順をすべて実行すると、各圧縮レベルの経過時間がコンソールに表示されます。 

```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```

この行は、プロセス全体が問題なく完了したことを確認します。

## 結論

Aspose.Cells for .NET を使用して Excel ファイルを保存するときに圧縮レベルを調整することは、簡単でありながら強力なテクニックです。このガイドで説明されている手順に従うことで、ファイル サイズを簡単に操作し、保存や転送をより管理しやすくすることができます。データにすばやくアクセスする必要がある場合でも、アプリケーションのパフォーマンスを最適化したい場合でも、これらのテクニックを習得すると、開発者としてのスキルが確実に向上します。

## よくある質問

### Aspose.Cells とは何ですか?
Aspose.Cells は、開発者がプログラムによって Excel ファイルを作成、操作、変換できるようにする .NET ライブラリです。

### Aspose.Cells をダウンロードするにはどうすればいいですか?
 Aspose.Cellsライブラリは以下からダウンロードできます。[Webサイト](https://releases.aspose.com/cells/net/).

### Aspose.Cells を無料で使用できますか?
はい、Asposeは無料で試用できるバージョンを提供しています。[ここ](https://releases.aspose.com/).

### 利用できるさまざまな圧縮レベルは何ですか?
Aspose.Cells は、レベル 1 (最小圧縮) からレベル 9 (最大圧縮) までの複数の圧縮レベルをサポートします。

### Aspose.Cells のサポートはどこで見つかりますか?
サポートを受けたり質問したりできます[Aspose フォーラム](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
