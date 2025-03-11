---
title: ワークブックから埋め込まれた Mol ファイルを抽出する
linktitle: ワークブックから埋め込まれた Mol ファイルを抽出する
second_title: Aspose.Cells .NET Excel 処理 API
description: この詳細なステップバイステップのチュートリアルでは、Aspose.Cells for .NET を使用して Excel ブックから埋め込まれた MOL ファイルを抽出する方法を学習します。
weight: 18
url: /ja/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ワークブックから埋め込まれた Mol ファイルを抽出する

## 導入
Excel ブック内のデータを管理する場合、標準形式ではないさまざまな埋め込みオブジェクトに遭遇することがあります。そのような形式の 1 つが MOL (分子構造ファイル) です。これは、化学で分子情報を表すためによく使用されます。Aspose.Cells for .NET を使用して Excel ブックからこれらの MOL ファイルを抽出しようとしている場合は、このガイドが役に立ちます。この記事では、各部分をわかりやすく説明しながら、プロセスを段階的に説明します。
## 前提条件
コードに取り組む前に、必要なスキルとツールがあることを確認することが重要です。必要なものは次のとおりです。
1. .NET プログラミングの基本的な理解: C# と .NET フレームワークに精通している必要があります。
2.  Aspose.Cells for .NET: Aspose.Cellsライブラリがあることを確認してください。[ここからダウンロード](https://releases.aspose.com/cells/net/).
3. IDE: Visual Studio またはその他の .NET 互換 IDE を使用できます。
4. 埋め込まれた MOL ファイルを含む Excel ワークブック: このチュートリアルでは、MOL オブジェクトを含む Excel ファイルが必要です。独自のファイルを作成することも、任意のサンプル ファイルを使用することもできます。
## パッケージのインポート
まず、プロジェクトに必要な名前空間をインポートする必要があります。これは、Aspose.Cells 機能にアクセスするために重要です。方法は次のとおりです。

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

これらの名前空間を使用すると、ワークブックを操作したり、ワークシートにアクセスしたり、一般的なファイルを操作したりできるようになります。
前提条件が整理されたので、コードを調べて、Excel ブックから埋め込まれた MOL ファイルを抽出する各手順を理解しましょう。 
## ステップ1: ディレクトリの設定
最初のステップは、ソース ドキュメントが配置されている場所と、抽出された MOL ファイルを保存する場所を定義することです。これらのディレクトリを設定しましょう。
```csharp
string SourceDir = "Your Document Directory"; //ディレクトリパスに置き換えます
string outputDir = "Your Document Directory"; //出力パスに置き換えます
```
ここで、`"Your Document Directory"`実際のディレクトリへのパスに置き換えます。ソース ディレクトリと出力ディレクトリの両方がアプリケーションからアクセス可能であることが重要です。
## ステップ2: ワークブックの読み込み
ディレクトリを設定したら、次のタスクは Excel ブックを読み込むことです。今すぐ実行しましょう。

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

インスタンスを作成しています`Workbook`クラスにExcelファイルへのパスを渡し、`EmbeddedMolSample.xlsx`この手順により、ワークブックが初期化され、その内容にアクセスできるようになります。
## ステップ3: ワークシートの反復処理
ワークブックが読み込まれたら、ワークブック内の各ワークシートをループする必要があります。これにより、各シートに埋め込まれたオブジェクトを調べることができます。

```csharp
var index = 1; //抽出されたMOLファイルの命名に使用されます
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    //さらなる抽出ロジックはここに記述します
}
```

ここでは、`foreach`ループを使用してワークシート間を移動します。各ワークシートでは、`OleObjects`すべての埋め込みオブジェクトを含むコレクション。
## ステップ4: MOLファイルの抽出
ここで重要な部分、つまり OLE オブジェクトから MOL ファイルを抽出する作業が始まります。この作業では、ワークシート ループ内に別のループが必要になります。

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

見つかったOLEオブジェクトごとに、出力ディレクトリに新しいファイルが作成されます。`ObjectData`の財産`OleObject`埋め込みオブジェクトのデータを保持し、それを新しく作成されたファイルに書き込む`FileStream`ファイルは順番に名前が付けられます（`OleObject1.mol`, `OleObject2.mol`など）に基づいて`index`変数。
## ステップ5: プロセス完了の確認
最後に、すべての MOL ファイルが抽出されたら、プロセスが正常に完了したことをユーザーに通知することをお勧めします。

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

この行は、抽出が成功したことを知らせるメッセージをコンソールに出力するだけです。ユーザーからのフィードバックを得るのに便利です。
## 結論
これで完了です。Aspose.Cells for .NET を使用して、Excel ブックから埋め込まれた MOL ファイルを正常に抽出できました。このプロセスでは、いくつかのコア ステップが統合されており、埋め込まれたオブジェクトを処理するための構造化されたアプローチが確保されています。科学研究、化学分析、または単に複雑なデータセットの処理など、どのような作業であっても、これらのファイル タイプを抽出して操作できれば、情報の管理方法に大きな違いが生まれます。 
## よくある質問
### Excel から MOL 以外のファイルタイプを抽出できますか?
はい、同様の手法で他のさまざまな埋め込みファイルタイプを抽出できます。
### Aspose.Cells は無料で使用できますか?
 Aspose.Cellsは商用ライブラリですが、[期間限定で無料でお試しいただけます](https://releases.aspose.com/).
### この方法はすべての Excel バージョンで機能しますか?
はい、ファイル形式が Aspose.Cells でサポートされている限り可能です。
### この抽出プロセスを自動化できますか?
もちろんです! スケジュールされたタスクまたはスクリプトにコードを配置することで、このプロセスを自動化できます。
### Aspose.Cells に関する詳細なドキュメントはどこで見つかりますか?
ぜひチェックしてみてください[Aspose.Cells ドキュメント](https://reference.aspose.com/cells/net/)詳細と例についてはこちらをご覧ください。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
