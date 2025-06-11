---
"description": "Aspose.Cells for .NET を使って表示形式をカスタマイズする方法を学びましょう。このステップバイステップガイドに従って、日付、パーセンテージ、通貨の書式を設定します。"
"linktitle": "ユーザー定義の数値による表示形式のカスタマイズ"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "ユーザー定義の数値による表示形式のカスタマイズ"
"url": "/ja/net/number-and-display-formats-in-excel/customizing-display-formats-with-user-defined-numbers/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ユーザー定義の数値による表示形式のカスタマイズ

## 導入
Excelファイルを扱う際には、データをより分かりやすくユーザーフレンドリーな方法で表示するために、セルの書式をカスタマイズする必要があることがよくあります。レポート用のExcelファイルを作成していると想像してみてください。単に数値を表示するだけでなく、日付、パーセンテージ、通貨などを洗練されたプロフェッショナルな形式で表示したいですよね？そこでカスタム表示形式が役立ちます。このチュートリアルでは、Aspose.Cells for .NETを詳しく解説し、ユーザー定義の設定を使用して数値の表示形式をカスタマイズする方法を説明します。
## 前提条件
始める前に、このチュートリアルに必要なものがすべて揃っていることを確認してください。必要なものは以下のとおりです。
- Aspose.Cells for .NET がインストールされています。 [ここからダウンロード](https://releases。aspose.com/cells/net/).
- C# および .NET フレームワークに関する基本的な知識。
- Aspose.Cellsの有効なライセンス。お持ちでない場合は、 [無料トライアル](https://releases.aspose.com/) またはリクエスト [一時ライセンス](https://purchase。aspose.com/temporary-license/).
- Visual Studio のような IDE。
- .NET Framework 4.0 以上。
何か足りないものがあってもご心配なく。いつでもこれらのリンクにアクセスして必要なファイルをダウンロードしたり、サポートに問い合わせたりすることができます。 [Aspose サポートフォーラム](https://forum。aspose.com/c/cells/9).
## 名前空間のインポート
コードに進む前に、必要なすべての Aspose.Cells 機能にアクセスするために必要な名前空間をインポートする必要があります。
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
この2つの名前空間が、このチュートリアルの核となるツールとなります。それでは、楽しい部分に移りましょう。
## ステップ1: プロジェクトディレクトリの設定
まず、ファイルを保存する場所が必要ですよね？出力Excelファイルを保存するディレクトリを作成しましょう。このステップでは、保存する前にディレクトリが存在することを確認します。
```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
// ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- 私たちは定義しています `dataDir` 出力される Excel ファイルが保存されるパスを格納する変数。
- 次に、ディレクトリが存在するかどうかを確認します。 `System。IO.Directory.Exists()`.
- ディレクトリが存在しない場合は、以下を使用して作成されます。 `System。IO.Directory.CreateDirectory()`.
## ステップ2: 新しいワークブックを作成し、ワークシートを追加する
ディレクトリが作成されたので、新しい Excel ブックを作成し、そこにワークシートを追加しましょう。
```csharp
// Workbookオブジェクトのインスタンス化
Workbook workbook = new Workbook();
// Excelオブジェクトに新しいワークシートを追加する
int i = workbook.Worksheets.Add();
// 新しく追加されたワークシートの参照をシートインデックスを渡して取得する
Worksheet worksheet = workbook.Worksheets[i];
```
- まず、新しい `Workbook` オブジェクトです。これは Excel ファイルと考えてください。
- このワークブックに新しいワークシートを追加するには、 `Add()` メソッドを実行し、インデックスを変数に格納する `i`。
- このワークシートは、 `workbook。Worksheets[i]`.
## ステップ3: セルに日付を追加して書式をカスタマイズする
さて、セルに現在の日付を挿入し、カスタム形式で表示してみましょう。デフォルトの日付形式の代わりに、次のようなカスタム形式を設定します。 `d-mmm-yy`。
```csharp
// 現在のシステム日付を「A1」セルに追加する
worksheet.Cells["A1"].PutValue(DateTime.Now);
// A1セルのスタイルを取得する
Style style = worksheet.Cells["A1"].GetStyle();
// 日付を「d-mmm-yy」として表示するようにカスタム表示形式を設定する
style.Custom = "d-mmm-yy";
// A1セルにスタイルを適用する
worksheet.Cells["A1"].SetStyle(style);
```
- 現在のシステム日付をセルに追加します `A1` 使用して `PutValue(DateTime。Now)`.
- セルの現在のスタイルを取得します `A1` 使用して `GetStyle()`。
- セルのスタイルを変更するには、 `style.Custom = "d-mmm-yy"`は、日付を日、月（省略形）、年を表示するようにフォーマットします。
- 最後に、新しいスタイルをセルに適用します。 `SetStyle()`。
## ステップ4: セルをパーセンテージで書式設定する
次に、数値を操作してみましょう。別のセルに数値を追加します。 `A2`をクリックし、パーセンテージとしてフォーマットします。
```csharp
// 「A2」セルに数値を追加する
worksheet.Cells["A2"].PutValue(20);
// A2セルのスタイルを取得する
style = worksheet.Cells["A2"].GetStyle();
// 値をパーセンテージで表示するためのカスタム表示形式を設定する
style.Custom = "0.0%";
// A2セルにスタイルを適用する
worksheet.Cells["A2"].SetStyle(style);
```
- 価値を付加します `20` セルへ `A2`。
- セルのスタイルを取得します `A2` カスタムフォーマットを次のように設定します `0.0%` 値をパーセンテージ（例：20%）で表示します。
- 最後に、セルにスタイルを適用します。 `SetStyle()`。
## ステップ5: セルを通貨として書式設定する
セルに別の値を追加してみましょう `A3`を選択し、通貨として表示するように書式設定します。より興味深い表示にするために、正の値はポンド、負の値はドルで通貨として表示する書式を使用します。
```csharp
// 「A3」セルに数値を追加する
worksheet.Cells["A3"].PutValue(2546);
// A3セルのスタイルを取得する
style = worksheet.Cells["A3"].GetStyle();
// 値を通貨として表示するためのカスタム表示形式を設定する
style.Custom = "£#,##0;[Red]$-#,##0";
// A3セルにスタイルを適用する
worksheet.Cells["A3"].SetStyle(style);
```
- 価値を付加します `2546` セルへ `A3`。
- カスタムフォーマットを設定します `£#,##0;[Red]$-#,##0`正の値はポンド記号で表示され、負の値はドル記号で赤く表示されます。
- セルにスタイルを適用するには、 `SetStyle()`。
## ステップ6: ワークブックを保存する
最後のステップは、ワークブックをExcelファイルとして保存することです。このチュートリアルでは、Excel 97-2003形式を使用します。
```csharp
// Excelファイルを保存する
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
- その `Save()` メソッドは、指定されたディレクトリにブックを保存します。
- 私たちは選ぶ `SaveFormat.Excel97To2003` 古いバージョンの Excel との互換性を確保するためです。
## 結論
これで完了です！Excelファイルを作成し、Aspose.Cells for .NETを使って特定のセルにカスタムの日付、パーセンテージ、通貨書式を追加し、ファイルを保存しました。カスタム書式設定により、Excelファイルの読みやすさとプロフェッショナルさが格段に向上します。Aspose.Cellsの他の書式設定オプション、例えば条件付き書式設定などもぜひお試しください。データの表示をさらに細かく制御できます。
## よくある質問
### Aspose.Cells でより複雑な書式設定オプションを適用するにはどうすればよいですか?
フォント色、境界線、背景色などのさまざまな書式設定スタイルをカスタム数値書式と組み合わせることができます。
### セル範囲にカスタム数値形式を適用できますか?
はい、Aspose.Cellsでは、 `Range.SetStyle()` 方法。
### 他にどのようなファイル形式でワークブックを保存できますか?
Aspose.CellsはXLSX、CSV、PDFなど、多くの形式をサポートしています。 `SaveFormat` の中で `Save()` 方法。
### 負の数を別の形式でフォーマットすることはできますか?
もちろんです！カスタム数値形式を使用すると、負の数値を異なる色や記号で表示できます。
### Aspose.Cells for .NET は無料ですか?
Aspose.Cellsは無料トライアルを提供していますが、すべての機能を使用するには有効なライセンスが必要です。 [仮免許証はこちら](https://purchase。aspose.com/temporary-license/).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}