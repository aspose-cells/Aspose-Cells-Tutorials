---
title: Excel で名前付き範囲内のセルを結合する
linktitle: Excel で名前付き範囲内のセルを結合する
second_title: Aspose.Cells .NET Excel 処理 API
description: このステップバイステップのチュートリアルでは、Aspose.Cells for .NET を使用して名前付き範囲内のセルを結合する方法を学びます。Excel レポートの書式設定、スタイル設定、自動化の方法を学びます。
weight: 11
url: /ja/net/excel-advanced-named-ranges/merge-cells-in-named-range/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel で名前付き範囲内のセルを結合する

## 導入

Excel ファイルをプログラムで操作する場合、よく発生するタスクの 1 つに、名前付き範囲内のセルの結合があります。レポート生成の自動化、ダッシュボードの構築、または大規模なデータセットの管理など、どのような場合でも、セルの結合は不可欠な手法です。このチュートリアルでは、Microsoft Excel をインストールしなくても開発者が Excel ファイルを操作できる強力なライブラリである Aspose.Cells for .NET を使用して、名前付き範囲内のセルを結合する方法を説明します。

## 前提条件

始める前に、以下のものを準備しておいてください。

-  Aspose.Cells for .NET: ダウンロードはこちらから[Aspose.Cells リリース ページ](https://releases.aspose.com/cells/net/).
- .NET Framework がマシンにインストールされています。
- C# の基本的な理解: クラス、メソッド、オブジェクトなどの概念を理解していると役立ちます。

## パッケージのインポート

コーディングを始める前に、必要な名前空間をインポートする必要があります。これらの名前空間により、Aspose.Cells ライブラリの機能にアクセスできるようになります。

```csharp
using System;
using System.IO;
using Aspose.Cells;
```

前提条件とパッケージの準備が整ったので、楽しい部分であるコーディングに移りましょう。

ここでは、Aspose.Cells for .NET を使用して Excel シート内の名前付き範囲内のセルを結合する方法を説明します。

## ステップ1: 新しいワークブックを作成する

まず最初に必要なのはワークブックです。Excel 用語では、ワークブックは Excel ファイルに相当します。ワークブックを作成しましょう。

```csharp
//新しいワークブックをインスタンス化します。
Workbook wb1 = new Workbook();
```

新しいワークブックを初期化すると、操作できる空の Excel ファイルが作成されます。これは、空白のキャンバスから始めるようなものです。

## ステップ2: 最初のワークシートにアクセスする

すべてのワークブックにはワークシートが含まれており、この場合は最初のワークシートを操作します。それを取得しましょう。

```csharp
//ワークブックの最初のワークシートを取得します。
Worksheet worksheet1 = wb1.Worksheets[0];
```

ワークシートは、実際のデータが存在する Excel ファイル内の個々のタブと考えてください。デフォルトでは、最初のタブにアクセスします。

## ステップ3: セル範囲を作成する

ワークシートが完成したら、範囲を作成します。範囲とは、複数の行と列にまたがるセルのブロックを指します。

```csharp
//範囲を作成します。
Range mrange = worksheet1.Cells.CreateRange("D6", "I12");
```

ここでは、D6 から I12 までのセルを選択しています。これは、複数の行と列をカバーするブロックです。すぐにこの範囲を結合します。

## ステップ4: 範囲に名前を付ける

範囲に名前を付けると、特に大規模なデータセットを扱う場合に、後で参照しやすくなります。

```csharp
//範囲に名前を付けます。
mrange.Name = "TestRange";
```

この範囲に「TestRange」という名前を付けると、セルの座標を再度指定しなくても、コード内で後ですぐに取得できるようになります。

## ステップ5: セル範囲を結合する

次は魔法です。先ほど作成した範囲内のセルを結合します。

```csharp
//範囲内のセルを結合します。
mrange.Merge();
```

この手順では、D6 から I12 までのすべてのセルを 1 つのセルに結合します。タイトルや概要などに最適です。

## ステップ6: 名前付き範囲を取得する

セルを結合したら、書式設定を適用する必要があります。まず、名前付き範囲を取得しましょう。

```csharp
//範囲を取得します。
Range range1 = wb1.Worksheets.GetRangeByName("TestRange");
```

名前で範囲を取得すると、スタイルの追加やデータの入力などの追加の操作を実行できます。

## ステップ7: 結合セルのスタイルを定義する

結合したセルが洗練されていなければ意味がありません。テキストを揃えて背景色を適用するスタイル オブジェクトを作成しましょう。

```csharp
//スタイル オブジェクトを定義します。
Style style = wb1.CreateStyle();

//配置を設定します。
style.HorizontalAlignment = TextAlignmentType.Center;
style.VerticalAlignment = TextAlignmentType.Center;
style.Pattern = BackgroundType.Solid;
style.ForegroundColor = System.Drawing.Color.Aqua;
```

ここでは、テキストを水平方向と垂直方向の両方で中央に配置し、背景色を水色 (アクア) に設定しています。スタイリッシュですよね?

## ステップ8: 範囲にスタイルを適用する

スタイルを定義したら、それを結合範囲に適用します。

```csharp
// StyleFlag オブジェクトを作成します。
StyleFlag flag = new StyleFlag();

//相対スタイル属性をオンにします。
flag.HorizontalAlignment = true;
flag.VerticalAlignment = true;
flag.CellShading = true;

//範囲にスタイルを適用します。
range1.ApplyStyle(style, flag);
```

の`StyleFlag` Aspose.Cells に、配置や網掛けなどの適用するスタイル プロパティを指示します。これにより、スタイルの適用方法を細かく制御できます。

## ステップ9: 結合範囲にデータを入力する

コンテンツのないフォーマットされた範囲とは何でしょうか? テキストを追加してみましょう。

```csharp
//範囲内にデータを入力します。
range1[0, 0].PutValue("Welcome to Aspose APIs.");
```

これにより、結合範囲の最初のセルに「Welcome to Aspose APIs」というテキストが配置されます。セルが結合されると、このテキストは D6 から I12 までのすべてのセルにまたがります。

## ステップ10: Excelファイルを保存する

最後に、ワークブックを Excel ファイルとして保存します。

```csharp
// Excel ファイルを保存します。
wb1.Save(dataDir + "outputMergeCellsInNamedRange.xlsx");
```

ここで、ワークブックは指定したディレクトリに「outputMergeCellsInNamedRange.xlsx」という名前で保存されます。

## 結論

これで完了です。名前付き範囲内のセルを結合し、美しい書式を適用し、さらにデータを入力できました。これらはすべて Aspose.Cells for .NET で実行できます。レポートの自動化、Excel ファイルの操作、または単に新しいテクニックの学習に取り組む場合でも、このステップ バイ ステップ ガイドは必要な基礎を提供します。

## よくある質問

### Aspose.Cells で複数の非連続範囲を結合できますか?  
いいえ、Aspose.Cells では連続するセルのみを結合できます。

### プログラムでマージ操作を元に戻すことはできますか?  
セルを結合したら、`UnMerge()` Aspose.Cells のメソッド。

### セルを結合すると、その中のデータは削除されますか?  
結合前にセルにデータがある場合は、範囲の最初のセルのデータが保持されます。

### 結合範囲内の個々のセルに異なるスタイルを適用できますか?  
いいえ、結合された範囲は単一のセルとして機能するため、その中の個々のセルに異なるスタイルを適用することはできません。

### 結合後に結合されたセルにアクセスするにはどうすればよいですか?  
結合後も、左上隅の座標を使用して結合されたセルにアクセスできます。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
