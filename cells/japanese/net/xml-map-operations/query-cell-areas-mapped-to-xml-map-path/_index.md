---
"description": "Aspose.Cells for .NET を使用して、Excel の XML マッピングされたセル領域をクエリする方法を学びます。このステップバイステップガイドは、構造化された XML データをシームレスに抽出するのに役立ちます。"
"linktitle": "Aspose.Cells を使用して XML マップ パスにマップされたセル領域をクエリする"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "Aspose.Cells を使用して XML マップ パスにマップされたセル領域をクエリする"
"url": "/ja/net/xml-map-operations/query-cell-areas-mapped-to-xml-map-path/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用して XML マップ パスにマップされたセル領域をクエリする

## 導入
.NETを使ってExcelでXMLデータを扱う方法を考えたことはありませんか？スプレッドシート操作のための強力なライブラリであるAspose.Cells for .NETを使えば、Excelファイル内のXMLマップを簡単に操作できます。構造化データで満たされたExcelファイルがあり、XMLパスにマッピングされた特定の領域をクエリする必要がある場合を想像してみてください。Aspose.Cellsがまさにその真価を発揮します。このチュートリアルでは、Aspose.Cells for .NETを使って、Excelファイル内のXMLマップパスにマッピングされたセル領域をクエリする方法を詳しく解説します。動的なレポートの作成やデータ抽出の自動化など、どのような目的にも対応できる、ステップバイステップの手順が満載です。
## 前提条件
コーディングを始める前に、必要なものがいくつかあります。
1. Aspose.Cells for .NET: このライブラリがインストールされていることを確認してください。ダウンロードできます。 [ここ](https://releases.aspose.com/cells/net/) または NuGet 経由で入手します。
2. XML マップされた Excel ファイル: このチュートリアルでは、XML マップを含む Excel ファイル (.xlsx) が必要です。
3. 開発環境: このガイドでは Visual Studio を使用していることを前提としていますが、どの C# エディターでも問題なく動作するはずです。
4. Asposeライセンス: 必要に応じて一時ライセンスを使用することができます。 [ここ](https://purchase。aspose.com/temporary-license/).
## パッケージのインポート
開始するには、コード ファイルに必要な名前空間をインポートしてください。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Diagnostics;
using System.Collections;
```
これらのパッケージを使用すると、ワークブックにアクセスし、ワークシートを操作し、スプレッドシート内で XML マップをクエリできるようになります。
## ステップ1: XMLマップを含むExcelファイルを読み込む
まず、XMLマッピングが既に含まれたExcelファイルを読み込む必要があります。このファイルがデータソースとして機能します。
```csharp
// ソースと出力のディレクトリパスを定義する
string sourceDir = "Your Document Directory";
// Excelファイルを読み込む
Workbook wb = new Workbook(sourceDir + "sampleXmlMapQuery.xlsx");
```
ここ、 `Workbook` はExcelファイル全体を表すクラスで、ファイルパスを使用して読み込みます。 `"Your Document Directory"` ファイルが配置されている実際のディレクトリ パスを入力します。
## ステップ2: ワークブック内のXMLマップにアクセスする
ファイルが読み込まれたら、次のステップはワークブック内のXMLマップにアクセスすることです。このマップは、スプレッドシートとXMLデータをつなぐ橋渡しとして機能します。
```csharp
// ワークブックの最初のXMLマップにアクセスする
XmlMap xmap = wb.Worksheets.XmlMaps[0];
```
ここでは、ワークブックの最初のXMLマップを取得するために、 `XmlMaps[0]` から `Worksheets` コレクション。ブックには複数の XML マップを含めることができますが、このチュートリアルでは最初の XML マップに焦点を当てます。
## ステップ3: クエリを実行するワークシートにアクセスする
XMLマップの準備ができたら、マップされたデータが格納されている特定のワークシートを選択します。通常は最初のワークシートですが、ファイルの設定によって異なります。
```csharp
// ワークブックの最初のワークシートにアクセスする
Worksheet ws = wb.Worksheets[0];
```
XMLマッピングされたデータが存在するワークシートにアクセスすることで、特定のセルをターゲットにすることができます。ここでは最初のワークシートを使用していますが、インデックスを変更するか名前を指定することで、他のワークシートを選択することもできます。
## ステップ4: パスを使用してXMLマップをクエリする
いよいよ核心部分、XMLマップのクエリです。ここではXMLパスを指定し、ワークシート内でそのパスにマッピングされたデータを取得します。
```csharp
Console.WriteLine("Query Xml Map from Path - /MiscData");
ArrayList ret = ws.XmlMapQuery("/MiscData", xmap);
```
その `XmlMapQuery` メソッドは2つのパラメータ、つまりXMLパスと先ほど取得したXMLマップを受け取ります。この例では、パスをクエリしています。 `/MiscData`これはXML構造の最上位パスです。結果は `ArrayList`反復処理が容易になります。
## ステップ5: クエリ結果を表示する
クエリされたデータを使って、次のステップは結果を表示することです。各項目を出力してみましょう。 `ArrayList` 抽出されたデータを明確に確認できるようにコンソールに表示されます。
```csharp
// クエリの結果を印刷する
for (int i = 0; i < ret.Count; i++)
{
    Console.WriteLine(ret[i]);
}
```
このループは、 `ArrayList` コンソールに出力します。XMLマップパスから抽出されたデータが表示されます。 `/MiscData`。
## ステップ6: ネストされたXMLパスをクエリする
クエリを絞り込むために、XML構造内のネストされたパスを掘り下げてみましょう。 `/MiscData/row/Color`。
```csharp
Console.WriteLine("Query Xml Map from Path - /MiscData/row/Color");
ret = ws.XmlMapQuery("/MiscData/row/Color", xmap);
```
ここでは、XMLデータ内のより具体的なパスをクエリしています。 `/MiscData/row/Color`、下の色の情報のみをターゲットにします `row` XML 構造内のノード。
## ステップ7: ネストされたパスクエリの結果を表示する
最後に、この絞り込んだクエリの結果を印刷して、マッピングされた特定の値を確認します。 `/MiscData/row/Color`。
```csharp
// ネストされたパスクエリの結果を印刷する
for (int i = 0; i < ret.Count; i++)
{
    Console.WriteLine(ret[i]);
}
```
前と同様に、このループはクエリ結果をコンソールに出力し、ネストされた XML パスから取得された特定のデータを確認できます。
## 結論
これで完了です！Aspose.Cells for .NET を使えば、XML マップパスにマッピングされたセル領域へのクエリが簡単かつ効率的に実行できます。この強力な機能は、スプレッドシートから特定のXMLデータを抽出する必要がある開発者にとって画期的なものです。より複雑なXMLクエリを実装したり、Excel ワークフロー内で複数のXMLマッピングを組み合わせたりするための基盤が整いました。さらに高度な機能をお探しですか？Aspose.Cells のドキュメントで、アプリケーションを強化するための追加のXMLマップ機能をご確認ください。
## よくある質問
### つの Excel ブックに複数の XML ファイルをマップできますか?  
はい、Aspose.Cells を使用すると、ワークブック内の複数の XML マップを管理し、複雑なデータのやり取りが可能になります。
### マップ内に XML パスが存在しない場合はどうなりますか?  
パスが無効または存在しない場合、 `XmlMapQuery` メソッドは空の `ArrayList`。
### Aspose.Cells for .NET を使用するにはライセンスが必要ですか?  
はい、すべての機能を使用するにはライセンスが必要です。 [無料トライアル](https://releases.aspose.com/) または [一時ライセンス](https://purchase。aspose.com/temporary-license/).
### クエリしたデータを新しい Excel ファイルに保存できますか?  
もちろんです！クエリされたデータを抽出し、別の Excel ファイルや Aspose.Cells でサポートされている他の形式に書き込むことができます。
### Excel (.xlsx) 以外の形式で XML マップをクエリすることは可能ですか?  
XMLマッピングは.xlsxファイルでサポートされています。他の形式では、機能が制限されるか、サポートされない場合があります。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}