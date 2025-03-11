---
title: .NET でのチャートから画像への変換
linktitle: .NET でのチャートから画像への変換
second_title: Aspose.Cells .NET Excel 処理 API
description: このステップバイステップ ガイドでは、Aspose.Cells を使用して .NET でグラフを画像に変換する方法を説明します。Excel グラフを高品質の画像に簡単に変換できます。
weight: 10
url: /ja/net/image-and-chart-operations/chart-to-image-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でのチャートから画像への変換

## 導入
Excel のグラフを画像に変換することは、レポート システムを構築したり、視覚的なデータ表現を共有したりするときに重要な要件になることがあります。幸いなことに、Aspose.Cells for .NET を使用すると、このプロセスは非常に簡単です。レポートを生成する場合でも、単に Excel のグラフを画像に変換して表示を改善する場合でも、このガイドでは、プロセスをステップごとに説明します。
## 前提条件
始める前に、このチュートリアルに従うために必要なものがすべて揃っていることを確認しましょう。
### Aspose.Cells for .NET ライブラリ
まず、Aspose.Cells for .NET ライブラリをダウンロードしてプロジェクトで参照する必要があります。最新バージョンはここから入手できます:
- [Aspose.Cells for .NET をダウンロード](https://releases.aspose.com/cells/net/)
### .NET 環境
システムに .NET フレームワークがインストールされていることを確認してください。この例を実行するには、Visual Studio またはその他の .NET 開発環境を使用できます。
### ライセンス設定（オプション）
 Aspose.Cellsは無料トライアルで使用できますが、制限のない完全な機能をお求めの場合は、[一時ライセンス](https://purchase.aspose.com/temporary-license/)または以下から購入[ここ](https://purchase.aspose.com/buy).

## パッケージのインポート
まず、Aspose.Cells ライブラリを操作するために必要な名前空間をインポートしましょう。これにより、Excel ファイルを操作し、画像を生成できるようになります。
```csharp
using System.IO;
using System.Drawing;
using Aspose.Cells;
```
コーディング部分を開始する前に、これらのパッケージが準備されていることを確認してください。

ここで、チャートを画像に変換するプロセスを簡単な手順に分解してみましょう。
## ステップ1: プロジェクトディレクトリを設定する
生成された画像を保存する場所が必要ですね。まずは出力画像を保存するディレクトリを作成しましょう。

まず、ドキュメント ディレクトリのパスを定義し、フォルダーが存在することを確認します。存在しない場合は、フォルダーを作成します。
```csharp
//画像を保存するディレクトリを定義する
string dataDir = "Your Document Directory";
//ディレクトリが存在するか確認する
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
この手順で、チャート画像を生成してこのディレクトリに保存する準備が整います。
## ステップ2: 新しいワークブックを作成する
ここで、Workbook オブジェクトをインスタンス化します。これは、グラフが埋め込まれる Excel ファイルを表します。

ワークブックは、シートを含む Excel ファイルのようなものです。新しいワークブックを作成することで、空の Excel ファイルから新しく始めることになります。
```csharp
//新しいワークブックオブジェクトを作成する
Workbook workbook = new Workbook();
```
## ステップ3: 新しいワークシートを追加する
すべての Excel ファイルにはワークシート (またはタブ) があります。ワークブックにワークシートを追加してみましょう。

このシートにデータとグラフを挿入するため、新しいワークシートを追加することは不可欠です。シートを追加したら、その参照を取得します。
```csharp
//ワークブックに新しいワークシートを追加する
int sheetIndex = workbook.Worksheets.Add();
//新しく追加されたワークシートを取得する
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
## ステップ4: ワークシートにデータを入力する
意味のあるグラフを作成するには、データが必要です。いくつかのセルにサンプル値を入力してみましょう。

ワークシート上の特定のセルにデータを追加します。このデータは、後でグラフを生成するために使用されます。
```csharp
//セルにサンプルデータを追加する
worksheet.Cells["A1"].PutValue(50);
worksheet.Cells["A2"].PutValue(100);
worksheet.Cells["A3"].PutValue(150);
worksheet.Cells["B1"].PutValue(4);
worksheet.Cells["B2"].PutValue(20);
worksheet.Cells["B3"].PutValue(50);
```
## ステップ5: ワークシートにグラフを追加する
ここで、追加したデータを視覚化する縦棒グラフを作成しましょう。

グラフの種類 (縦棒グラフ) を指定し、ワークシート内でのサイズと位置を定義します。
```csharp
//ワークシートに縦棒グラフを追加する
int chartIndex = worksheet.Charts.Add(Aspose.Cells.Charts.ChartType.Column, 5, 0, 15, 5);
```
## ステップ6: チャートデータソースを定義する
ここで魔法が起こります。グラフをワークシート内のデータにリンクするのです。

グラフを列 A1 から B3 のデータにリンクします。これにより、グラフにデータの取得元が指示されます。
```csharp
//チャートをA1からB3の範囲のデータにリンクします
Aspose.Cells.Charts.Chart chart = worksheet.Charts[chartIndex];
chart.NSeries.Add("A1:B3", true);
```
## ステップ7: チャートを画像に変換する
真実の瞬間: このグラフを画像ファイルに変換します。

ここでは、`ToImage`チャートを任意の画像形式に変換する方法。この場合は、EMF (拡張メタファイル) 形式に変換します。
```csharp
//チャートを画像に変換し、ディレクトリに保存します
chart.ToImage(dataDir + "Chart.emf", ImageFormat.Emf);
```
これで完了です。チャートが画像として保存されました。自分を褒めてあげましょう。
## ステップ8: 成功メッセージを表示する
最後に、画像生成を確認するメッセージを表示しましょう。
```csharp
//成功を示すメッセージを表示する
System.Console.WriteLine("Image generated successfully.");
```
## 結論
すごい! Aspose.Cells for .NET を使用すると、Excel のグラフを画像に変換するのがとても簡単になります。このプロセスにより、データの表示が簡素化されるだけでなく、埋め込みグラフよりも画像が優先されるレポートやダッシュボードの柔軟性も向上します。
このガイドで説明されている手順に従うことで、任意の Excel グラフを画像に変換し、視覚データをさまざまなアプリケーションにシームレスに統合できるようになります。
## よくある質問
### この方法を使用して、異なるタイプのグラフを変換できますか?
はい、円グラフ、棒グラフ、折れ線グラフなど、Aspose.Cells でサポートされているあらゆるグラフ タイプを変換できます。
### 画像フォーマットを変更することは可能ですか?
もちろんです！この例ではEMFを使用しましたが、画像形式をPNG、JPEG、BMPなどに変更できます。`ImageFormat`パラメータ。
### Aspose.Cells は高解像度の画像をサポートしていますか?
はい、Aspose.Cells を使用すると、グラフを画像にエクスポートするときに画像の解像度と品質設定を制御できます。
### 複数のグラフを一度に画像に変換できますか?
はい、ワークブック内の複数のグラフをループし、数行のコードですべてを画像に変換できます。
### 変換できるチャートの数に制限はありますか?
Aspose.Cells によって課される固有の制限はありませんが、大量のデータの処理はシステムのメモリとパフォーマンス能力に依存する場合があります。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
