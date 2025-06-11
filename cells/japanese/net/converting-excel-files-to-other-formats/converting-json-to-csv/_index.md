---
"description": "Aspose.Cellsを使用して、.NETでプログラム的にJSONをCSVに変換する方法を学びましょう。ステップバイステップガイドに従って、シームレスなデータ変換を実現しましょう。"
"linktitle": ".NET でプログラム的に JSON を CSV に変換する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": ".NET でプログラム的に JSON を CSV に変換する"
"url": "/ja/net/converting-excel-files-to-other-formats/converting-json-to-csv/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的に JSON を CSV に変換する

## 導入
今日のデジタル世界では、複数の形式でデータを扱うことが当たり前になり、JSON（JavaScript Object Notation）はデータ交換で最も広く使われている形式の一つです。しかし、そのJSONをCSV（カンマ区切り値）のような、分析しやすい形式に変換する必要がある場合はどうでしょうか？このチュートリアルでは、使いやすく強力なスプレッドシート操作APIであるAspose.Cells for .NETを使用して、JSONをCSVにプログラムで変換する手順を解説します。 
## 前提条件
コードの説明に入る前に、必要なコンポーネントがすべて揃っていること、そして使用するツールの基本を理解していることを確認することが重要です。必要なものを概説しましょう。
- Aspose.Cells for .NET: これはJSONからCSVへの変換に使用する主要なライブラリです。 [ここからダウンロード](https://releases。aspose.com/cells/net/).
- Visual Studio: .NET コードを記述して実行するには、Visual Studio のような統合開発環境 (IDE) が必要です。
- .NET Framework: .NET Framework がインストールされていることを確認してください。Aspose.Cells は .NET Core と .NET Framework の両方と互換性があります。
- C# の基本知識: このガイドではコードの各部分を詳しく説明しますが、C# に多少精通していると役立ちます。
## パッケージのインポート
.NETプロジェクトでAspose.Cellsを使用するには、まずライブラリをインストールする必要があります。NuGetパッケージマネージャーからインストールできます。
1. Visual Studio を開きます。
2. [ツール] > [NuGet パッケージ マネージャー] > [ソリューションの NuGet パッケージの管理] に移動します。
3. Aspose.Cells を検索し、最新バージョンをインストールします。
インストールしたら、コードに次の名前空間を含めるようにしてください。
```csharp
using Aspose.Cells.Utility;
using System;
using System.IO;
```
すべての設定が完了したら、コードを段階的に説明して、Aspose.Cells を使用して JSON ファイルを CSV に変換するのがいかに簡単かを確認しましょう。
## ステップ1: JSONファイルを読む
まず最初に、ファイルからJSONデータを読み込む必要があります。JSONファイル（ここではJSONファイルと呼びます）が既にあると仮定します。 `SampleJson.json`) がシステム上のディレクトリに保存されます。
使用することができます `File.ReadAllText()` JSON ファイルの内容を文字列に読み込む C# のメソッド。
```csharp
// ソースディレクトリ
string sourceDir = "Your Document Directory";
// JSONファイルを読む
string str = File.ReadAllText(sourceDir + "SampleJson.json");
```

このステップは非常に重要です。変換プロセスを開始するには生のJSONデータが必要だからです。これを文字列として読み込むことで、Aspose.Cellsで処理できるように準備します。
## ステップ2: 空のワークブックを作成する
Aspose.Cellsは主にワークブック（Excelファイル）上で動作します。JSONデータのインポートを開始するには、まずデータを挿入する空のワークブックを作成する必要があります。
```csharp
// 空のワークブックを作成する
Workbook workbook = new Workbook();
```
ここでは、最終的にCSV形式のデータを格納する空のワークブックを初期化しています。これは、JSONデータですぐに入力される空のExcelスプレッドシートを作成するようなものです。
## ステップ3: ワークブック内のセルにアクセスする
空のワークブックができたので、そのセルにアクセスする必要があります。 `Cells` Aspose.Cells のコレクションは、JSON データを配置するワークシート内のすべてのセルを表します。
```csharp
// セルを取得
Cells cells = workbook.Worksheets[0].Cells;
```
このコードスニペットは最初のワークシート（インデックス0のワークシート）を選択し、その `Cells` コレクション。これらのセルは、データが追加されるスプレッドシートのグリッドのようなものです。
## ステップ4: JsonLayoutOptionsを設定する
Aspose.CellsはJSONデータのインポート方法に関するいくつかのカスタマイズオプションを提供しています。ここでは、 `JsonLayoutOptions` Aspose が配列、数値データ、およびオブジェクト タイトルを処理する方法を指定します。
```csharp
// JsonLayoutOptionsを設定する
JsonLayoutOptions importOptions = new JsonLayoutOptions();
importOptions.ConvertNumericOrDate = true;
importOptions.ArrayAsTable = true;
importOptions.IgnoreArrayTitle = true;
importOptions.IgnoreObjectTitle = true;
```

- ConvertNumericOrDate: 数値または日付値である文字列値を自動的に変換します。
- ArrayAsTable: JSON 内の配列をワークブック内のテーブルとして扱います。
- IgnoreArrayTitle および IgnoreObjectTitle: これらのオプションは、配列とオブジェクトのタイトルを無視し、生のデータのみがインポートされるようにします。
## ステップ5: JSONデータをインポートする
レイアウトオプションを設定したら、JSONデータを取り込む必要があります。 `JsonUtility.ImportData()` メソッドはここで大変な作業を実行し、JSON データをワークブックのセルに挿入します。
```csharp
JsonUtility.ImportData(str, cells, 0, 0, importOptions);
```
このメソッドはいくつかのパラメータを取ります。
- `str`: ステップ 1 で読み取った JSON 文字列。
- `cells`: データが配置されるセルのコレクション。
- `0, 0`: これらは、データの開始位置 (つまり、左上隅) を示す行と列のインデックスです。
- `importOptions`: 手順 4 で設定したレイアウト オプション。
## ステップ6: ワークブックをCSVとして保存する
JSONデータがワークブックに取り込まれたので、ワークブックをCSVファイルとして簡単に保存できます。CSVは表形式のデータを保存するためのシンプルで軽量な形式であり、データ分析に最適です。
```csharp
// 出力ディレクトリ
string outputDir = "Your Document Directory";
// ワークブックを保存
workbook.Save(outputDir + @"SampleJson_out.csv");
```
このステップでは、ワークブックをCSVファイルとして保存します。パスとファイル名（`SampleJson_out.csv`) に CSV が保存されます。
## ステップ7: プロセスを確認する
すべてが期待どおりに機能したことを確認するために、コンソールに確認メッセージを出力できます。
```csharp
Console.WriteLine("ConvertJsonToCsv executed successfully.");
```
シンプルな成功メッセージは、プロセスがスムーズに実行されたことの確認に役立ちます。
## 結論
Aspose.Cells for .NET を使った JSON から CSV への変換は、シンプルながらも強力なプロセスです。わずか数行のコードで、複雑な JSON データをよりアクセスしやすい CSV 形式に変換できます。配列、オブジェクト、数値データなど、どんなデータを扱う場合でも、Aspose.Cells を使えば、ニーズに合わせて変換プロセスを簡単に設定できます。
## よくある質問
### Aspose.Cells は大きな JSON ファイルを処理できますか?
はい、Aspose.Cells は大規模なデータセットを効率的に処理するように設計されており、パフォーマンスの問題なしに大規模な JSON ファイルを処理するのに適しています。
### CSV 出力をカスタマイズするにはどうすればよいですか?
CSV出力をカスタマイズするには、 `JsonLayoutOptions` または、CSV として保存する前にブックの書式を操作します。
### 変換中に JSON から特定のデータを除外する方法はありますか?
はい、インポート前に JSON を微調整するか、カスタム コード ロジックを使用することで、特定のデータ フィールドを除外またはフィルター処理できます。
### Aspose.Cells は CSV 以外のファイル形式もサポートしていますか?
もちろんです! Aspose.Cells は、Excel (XLS、XLSX)、PDF、HTML など、幅広い形式をサポートしています。
### Aspose.Cells を無料で試すにはどうすればいいですか?
あなたはできる [無料トライアルはこちらからダウンロードできます](https://releases.aspose.com/) 購入前にすべての機能をテストします。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}