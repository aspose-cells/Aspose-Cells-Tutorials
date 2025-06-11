---
"description": ".NET 開発者向けに設計されたこの包括的なステップバイステップのチュートリアルでは、Aspose.Cells を使用して Excel ブックを CSV 形式に簡単に変換する方法を学びます。"
"linktitle": "ワークブックをテキストCSV形式で保存"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "ワークブックをテキストCSV形式で保存"
"url": "/ja/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ワークブックをテキストCSV形式で保存

## 導入
データを扱う際、選択するフォーマットによって、データの扱いやすさは大きく左右されます。表形式データの処理に最もよく使われるフォーマットの一つがCSV（カンマ区切り値）です。Excelファイルを扱う開発者で、ワークブックをCSV形式に変換する必要がある場合、Aspose.Cells for .NETは、この作業を簡素化する優れたライブラリです。このチュートリアルでは、Excelワークブックをテキスト形式のCSV形式にシームレスに変換する手順を詳しく説明します。
## 前提条件
始める前に、始めるために必要なものがすべて揃っていることを確認しましょう。
1. C# と .NET の基礎知識: C# でコードを記述するため、この言語と .NET フレームワークに精通していることが必須です。
2. Aspose.Cellsライブラリ：開発環境にAspose.Cells for .NETライブラリがインストールされていることを確認してください。ダウンロードできます。 [ここ](https://releases。aspose.com/cells/net/).
3. Visual Studio または任意の C# IDE: コードを記述して実行するには、統合開発環境 (IDE) が必要です。Visual Studio は人気のある選択肢です。
4. Excel ワークブック: 変換をテストするためのデータを含むサンプルの Excel ワークブック (例: 「book1.xls」) を準備します。
## パッケージのインポート
前提条件が満たされたので、プロセスの最初のステップは必要なパッケージをインポートすることです。C#プロジェクトでは、コードファイルの先頭に次の名前空間を含める必要があります。
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
これらの名前空間により、Excel ファイルの操作やメモリ ストリームの管理に必要なクラスとメソッドにアクセスできるようになります。
## ステップ1: ドキュメントディレクトリへのパスを定義する
プロセスの最初のステップは、ドキュメント（Excelワークブック）の保存場所を定義することです。これは、プログラムが処理に必要なファイルの場所を認識できるようにするために不可欠です。 
```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
```
必ず交換してください `"Your Document Directory"` 「book1.xls」ファイルが保存されている実際のパスを入力します。これは、コンピュータ上のディレクトリ、またはサーバーへのパスになります。
## ステップ2: ソースブックを読み込む
次に、CSV 形式に変換する Excel ブックを読み込む必要があります。
```csharp
// ソースブックを読み込む
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
その `Workbook` Aspose.Cellsライブラリのクラスを使用すると、Excelブックの操作とアクセスが可能になります。ファイルパスを渡すことで、指定されたブックを読み込んで処理します。
## ステップ3: ワークブックデータのバイト配列を初期化する
ワークブックを CSV に変換する前に、最終的にすべてのワークシート データを保持する空のバイト配列を初期化する必要があります。
```csharp
// 0バイト配列
byte[] workbookData = new byte[0];
```
このバイト配列は、各ワークシートのデータを単一の構造に結合し、後でファイルに書き込むことができます。
## ステップ4: テキスト保存オプションを設定する
それでは、テキストの保存形式に関するオプションを設定しましょう。カスタム区切り文字を選択するか、タブをそのまま使用することもできます。
```csharp
// テキスト保存オプション。任意の区切り文字を使用できます。
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // タブを区切りとして設定する
```
この例では、区切り文字としてタブ文字を使用しています。 `'\t'` 任意の文字（カンマなど）で区切ることができます（`,`) を選択します。
## ステップ5: 各ワークシートを反復処理する
次に、ワークブック内のすべてのワークシートを反復処理し、各ワークシートを `workbookData` 配列ですが、最初に作業するワークシートを選択する必要があります。
```csharp
// 各ワークシートデータをテキスト形式でワークブックデータ配列内にコピーします。
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // アクティブなワークシートをテキスト形式で保存する
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
ループはワークブック内の各ワークシートに対して実行されます。 `ActiveSheetIndex` ループを実行するたびに現在のワークシートを保存するように設定されています。結果は、 `MemoryStream`。
## ステップ6: ワークシートデータを取得する
ワークシートをメモリストリームに保存した後、次のステップはこのデータを取得して `workbookData` 配列。
```csharp
    // ワークシートのデータをシートデータ配列に保存する
    ms.Position = 0; // メモリストリームの位置をリセット
    byte[] sheetData = ms.ToArray(); // バイト配列を取得する
```
`ms.Position = 0;` 書き込み後に読み取り位置をリセットします。その後、 `ToArray()` メモリ ストリームを、ワークシート データを保持するバイト配列に変換します。
## ステップ7: ワークシートのデータを結合する
ここで、各ワークシートのデータを1つの `workbookData` 配列は以前に初期化されました。
```csharp
    // このワークシートデータをワークブックデータ配列に結合する
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
既存のワークブックデータと新しいワークシートデータの両方を格納できる十分な大きさの新しい配列を作成します。そして、既存のデータと新しいデータをこの結合された配列にコピーし、後で使用します。
## ステップ8: ワークブックデータ全体をファイルに保存する
最後に、私たちのすべてのデータを統合して `workbookData` 配列の場合、この配列を指定されたファイル パスに保存できます。
```csharp
// ワークブックデータ全体をファイルに保存する
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` 結合されたバイト配列を受け取り、指定されたディレクトリ内の「out.txt」という名前のテキスト ファイルに書き込みます。
## 結論
これで完了です！Aspose.Cells for .NET を使用して、Excel ブックを CSV 形式に変換できました。このプロセスは効率的であるだけでなく、Excel データを簡単に操作して、さらに分析やレポート作成を行うこともできます。これで、データ処理タスクを自動化したり、この機能を大規模なアプリケーションに統合したりすることも可能です。
## よくある質問
### CSV ファイルに異なる区切り文字を使用できますか?
はい、変更できます `opts.Separator` カンマやパイプなど、任意の文字に変更できます。
### Aspose.Cells は無料で使用できますか?
Aspose.Cellsは無料ではありませんが、無料トライアルを利用できます。 [ここ](https://releases。aspose.com/).
### CSV 以外にどのような形式で保存できますか?
Aspose.Cells を使用すると、XLSX、PDF など、複数の形式で保存できます。
### Aspose.Cells を使用して大きな Excel ファイルを処理できますか?
はい、Aspose.Cells は大きなファイルを効率的に処理するように設計されていますが、パフォーマンスはシステム リソースに依存する場合があります。
### より詳細なドキュメントはどこで見つかりますか?
包括的なドキュメントと例については、 [参考サイト](https://reference。aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}