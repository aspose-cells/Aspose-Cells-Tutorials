---
title: Excel で循環参照をプログラム的に検出する
linktitle: Excel で循環参照をプログラム的に検出する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用すると、Excel の循環参照を簡単に検出できます。ステップ バイ ステップ ガイドに従って、スプレッドシートで正確な計算を実行してください。
weight: 13
url: /ja/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel で循環参照をプログラム的に検出する

## 導入
Excel ファイルの操作で遭遇する最も厄介な問題の 1 つが循環参照です。これは、数式が直接的または間接的に自身のセルを参照し、ループを作成して Excel の計算エンジンを混乱させる場合に発生します。しかし、心配はいりません。Aspose.Cells for .NET を使用すると、これらの厄介な循環参照をプログラムで検出し、スプレッドシートが機能し、正確であることを確認できます。このガイドでは、プロセスをステップごとに簡単に説明します。
## 前提条件
循環参照の検出の詳細に入る前に、始めるのに必要なものがすべて揃っていることを確認しましょう。
1. Visual Studio: マシンに Visual Studio がインストールされていることを確認してください。これが開発環境になります。
2. .NET Framework: 互換性のあるバージョンの .NET Framework (少なくとも .NET Framework 4.0) を使用していることを確認します。
3.  Aspose.Cellsライブラリ: Aspose.Cellsライブラリが必要です。ダウンロードは以下から行えます。[Aspose ウェブサイト](https://releases.aspose.com/cells/net/).
4. C# の基礎知識: この言語でコードを記述するため、C# プログラミングの知識があると役立ちます。
5. Excel ファイル: テスト用に循環参照を含む Excel ファイルを用意します。簡単なファイルを作成することも、サンプルをダウンロードすることもできます。
前提条件が整ったので、楽しい部分に進みましょう。
## パッケージのインポート
コーディングを始める前に、必要なパッケージをインポートする必要があります。手順は次のとおりです。
### 新しいプロジェクトを作成する
- Visual Studio を開き、新しい C# コンソール アプリケーション プロジェクトを作成します。
### Aspose.Cells 参照を追加する
- ソリューション エクスプローラーでプロジェクトを右クリックします。
- 「NuGet パッケージの管理」を選択します。
- 「Aspose.Cells」を検索し、最新バージョンをインストールします。
### 必要な名前空間をインポートする
あなたの一番上に`Program.cs`ファイルに、必要な名前空間をインポートします。
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

これですべての設定が完了したので、Excel ファイル内の循環参照を検出するコードについて詳しく見ていきましょう。
## ステップ1: 入力ディレクトリを定義する
まず、Excel ファイルが保存されているディレクトリを指定する必要があります。ここで Excel ファイルを読み込みます。
```csharp
//入力ディレクトリ
string sourceDir = "Your Document Directory";
```
交換する`"Your Document Directory"`Excel ファイルへの実際のパスを入力します。
## ステップ 2: LoadOptions を使用してワークブックを読み込む
次に、Excel ブックを読み込みます。ここから魔法が始まります。
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
ここでは、新しいインスタンスを作成します`LoadOptions`指定されたパスからワークブックを読み込みます。Excel ファイル名が一致していることを確認してください。
## ステップ3: 反復設定を有効にする
循環参照を許可するには、ワークブックで反復設定を有効にする必要があります。
```csharp
objWB.Settings.Iteration = true;
```
これにより、Aspose.Cells は計算中に循環参照を許可するようになります。
## ステップ4: 計算オプションと円形モニターを作成する
次に、計算オプションとカスタム円形モニターを作成しましょう。
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
ここでは、インスタンスを作成しています`CalculationOptions`そして習慣`CircularMonitor`このモニターは、計算中に見つかった循環参照を追跡するのに役立ちます。
## ステップ5: 数式を計算する
ここで、ワークブック内の数式を計算します。
```csharp
objWB.CalculateFormula(copts);
```
この行は計算を実行し、循環参照をチェックします。
## ステップ6: 循環参照を数える
計算後、見つかった循環参照の数をカウントできます。
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
これにより、Excel ファイル内で検出された循環参照の数を出力します。
## ステップ7: 結果を表示する
最後に、結果を表示して、メソッドが正常に実行されたことを確認しましょう。
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## ステップ 8: CircularMonitor クラスを実装する
プロセスを完了するには、`CircularMonitor`クラス。このクラスは`AbstractCalculationMonitor`循環参照の検出を処理します。
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
このクラスは、ワークシート名やセル インデックスなど、見つかった各循環参照の詳細を取得します。
## 結論
Aspose.Cells for .NET を使用して Excel の循環参照を検出するのは、管理しやすい手順に分解すれば簡単なプロセスです。このガイドに従うことで、スプレッドシート内の循環参照を簡単に識別して処理し、計算の正確性と信頼性を確保できます。熟練した開発者でも、初心者でも、Aspose.Cells は Excel の操作機能を強化する強力なツールを提供します。 
## よくある質問
### Excel の循環参照とは何ですか?
循環参照は、数式が自身のセルを参照し、計算で無限ループを引き起こす場合に発生します。
### プログラムで循環参照を検出するにはどうすればいいですか?
.NET の Aspose.Cells ライブラリを使用すると、カスタム計算モニターを実装して、循環参照をプログラムで検出できます。
### Aspose.Cells を使用するための前提条件は何ですか?
Visual Studio、.NET Framework、および Aspose.Cells ライブラリがインストールされている必要があります。
### Aspose.Cells を無料で使用できますか?
はい、Aspose.Cells では、その機能を試すために使用できる無料トライアルを提供しています。
### Aspose.Cells の詳細情報はどこで入手できますか?
訪問することができます[Aspose.Cells ドキュメント](https://reference.aspose.com/cells/net/)詳細な情報と例については、こちらをご覧ください。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
