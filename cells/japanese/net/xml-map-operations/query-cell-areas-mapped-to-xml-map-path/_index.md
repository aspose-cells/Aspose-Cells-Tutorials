---
title: Aspose.Cells を使用して XML マップ パスにマップされたセル領域をクエリする
linktitle: Aspose.Cells を使用して XML マップ パスにマップされたセル領域をクエリする
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、Excel で XML にマップされたセル領域をクエリする方法を学びます。このステップ バイ ステップ ガイドは、構造化された XML データをシームレスに抽出するのに役立ちます。
weight: 12
url: /ja/net/xml-map-operations/query-cell-areas-mapped-to-xml-map-path/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用して XML マップ パスにマップされたセル領域をクエリする

## 導入
.NET を使用して Excel で XML データを操作する方法を考えたことはありませんか? スプレッドシート操作用の強力なライブラリである Aspose.Cells for .NET を使用すると、Excel ファイル内の XML マップを簡単に操作できます。構造化データで満たされた Excel ファイルがあり、XML パスにマップされた特定の領域をクエリする必要がある場合を想像してください。ここで Aspose.Cells が活躍します。このチュートリアルでは、Aspose.Cells for .NET を使用して、Excel ファイル内の XML マップ パスにマップされたセル領域をクエリする方法について説明します。動的なレポートを作成する場合でも、データ抽出を自動化する場合でも、このガイドのステップバイステップの手順が役立ちます。
## 前提条件
コーディングを始める前に、いくつか必要なものがあります。
1.  Aspose.Cells for .NET: このライブラリがインストールされていることを確認してください。ダウンロードできます。[ここ](https://releases.aspose.com/cells/net/)または NuGet 経由で入手します。
2. XML マップされた Excel ファイル: このチュートリアルでは、XML マップを含む Excel ファイル (.xlsx) が必要です。
3. 開発環境: このガイドでは Visual Studio を使用していることを前提としていますが、どの C# エディターでも問題なく動作するはずです。
4.  Asposeライセンス: 必要に応じて一時ライセンスを使用することができます。[ここ](https://purchase.aspose.com/temporary-license/).
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
まず、XML マッピングがすでに含まれている Excel ファイルを読み込む必要があります。このファイルはデータ ソースとして機能します。
```csharp
//ソースと出力のディレクトリパスを定義する
string sourceDir = "Your Document Directory";
// Excelファイルを読み込む
Workbook wb = new Workbook(sourceDir + "sampleXmlMapQuery.xlsx");
```
ここ、`Workbook`は、ファイルパスを使用して読み込むExcelファイル全体を表すクラスです。`"Your Document Directory"`ファイルが配置されている実際のディレクトリ パスを入力します。
## ステップ 2: ワークブック内の XML マップにアクセスする
ファイルが読み込まれたら、次のステップはワークブック内の XML マップにアクセスすることです。このマップは、スプレッドシートと XML データ間の橋渡しとして機能します。
```csharp
//ワークブックの最初のXMLマップにアクセスする
XmlMap xmap = wb.Worksheets.XmlMaps[0];
```
ここでは、ワークブックの最初のXMLマップを取得するために、`XmlMaps[0]`から`Worksheets`コレクション。ワークブックには複数の XML マップを含めることができますが、このチュートリアルでは最初のマップに焦点を当てます。
## ステップ3: クエリを実行するワークシートにアクセスする
XML マップの準備ができたら、マップされたデータが配置されている特定のワークシートを選択します。これは通常最初のワークシートですが、ファイルの設定によって異なります。
```csharp
//ワークブックの最初のワークシートにアクセスする
Worksheet ws = wb.Worksheets[0];
```
XML にマップされたデータが存在するワークシートにアクセスすると、特定のセルをターゲットにすることができます。ここでは最初のワークシートを使用していますが、インデックスを変更するか名前を指定することにより、他のワークシートを選択することもできます。
## ステップ 4: パスを使用して XML マップをクエリする
ここで、核となる部分、つまり XML マップのクエリが行われます。ここでは、XML パスを指定して、ワークシート内でそのパスにマップされたデータを取得します。
```csharp
Console.WriteLine("Query Xml Map from Path - /MiscData");
ArrayList ret = ws.XmlMapQuery("/MiscData", xmap);
```
の`XmlMapQuery`メソッドは、XMLパスと先ほど取得したXMLマップの2つのパラメータを取ります。この例では、パスをクエリしています。`/MiscData`はXML構造の最上位パスです。結果は`ArrayList`繰り返し処理が容易になります。
## ステップ5: クエリ結果を表示する
クエリされたデータを使って、次のステップは結果を表示することです。`ArrayList`抽出されたデータを明確に確認するには、コンソールに表示します。
```csharp
//クエリの結果を印刷する
for (int i = 0; i < ret.Count; i++)
{
    Console.WriteLine(ret[i]);
}
```
このループは、`ArrayList`コンソールに出力します。XMLマップパスから抽出されたデータが表示されます。`/MiscData`.
## ステップ 6: ネストされた XML パスをクエリする
クエリを絞り込むには、XML構造内のネストされたパスを掘り下げてみましょう。`/MiscData/row/Color`.
```csharp
Console.WriteLine("Query Xml Map from Path - /MiscData/row/Color");
ret = ws.XmlMapQuery("/MiscData/row/Color", xmap);
```
ここでは、XMLデータ内のより具体的なパスをクエリしています。`/MiscData/row/Color` 、以下の色情報のみをターゲットにします`row`XML 構造内のノード。
## ステップ7: ネストされたパスクエリの結果を表示する
最後に、この絞り込まれたクエリの結果を印刷して、マッピングされた特定の値を確認します。`/MiscData/row/Color`.
```csharp
//ネストされたパスクエリの結果を印刷する
for (int i = 0; i < ret.Count; i++)
{
    Console.WriteLine(ret[i]);
}
```
前と同様に、このループはクエリ結果をコンソールに出力し、ネストされた XML パスから取得された特定のデータを確認できます。
## 結論
これで完了です。Aspose.Cells for .NET を使用すると、XML マップ パスにマップされたセル領域のクエリが簡単かつ非常に効率的になります。この強力な機能は、スプレッドシートから特定の XML データを抽出する必要がある開発者にとって画期的なものです。これで、より複雑な XML クエリを実装し、Excel ワークフロー内で複数の XML マッピングを組み合わせるための基盤ができました。さらに進めたいですか? アプリケーションを強化するための追加の XML マップ機能については、Aspose.Cells のドキュメントを参照してください。
## よくある質問
### 1 つの Excel ブックに複数の XML ファイルをマップできますか?  
はい、Aspose.Cells を使用すると、ワークブック内の複数の XML マップを管理し、複雑なデータのやり取りが可能になります。
### マップ内に XML パスが存在しない場合はどうなりますか?  
パスが無効または存在しない場合は、`XmlMapQuery`メソッドは空の`ArrayList`.
### Aspose.Cells for .NET を使用するにはライセンスが必要ですか?  
はい、フル機能を使用するにはライセンスが必要です。[無料トライアル](https://releases.aspose.com/)または[一時ライセンス](https://purchase.aspose.com/temporary-license/).
### クエリされたデータを新しい Excel ファイルに保存できますか?  
もちろんです! クエリされたデータを抽出し、別の Excel ファイルや Aspose.Cells でサポートされている他の形式に書き込むことができます。
### Excel (.xlsx) 以外の形式で XML マップをクエリすることは可能ですか?  
XML マッピングは .xlsx ファイルでサポートされます。他の形式では、機能が制限されるか、サポートされない場合があります。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
