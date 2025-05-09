---
"description": "この詳細なステップバイステップ ガイドでは、Aspose.Cells for .NET を使用して、既に署名されている Excel ファイルにデジタル署名を追加する方法を学習します。"
"linktitle": "すでに署名された Excel ファイルにデジタル署名を追加する"
"second_title": "Aspose.Cells for .NET API リファレンス"
"title": "すでに署名された Excel ファイルにデジタル署名を追加する"
"url": "/ja/net/excel-workbook/add-digital-signature-to-an-already-signed-excel-file/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# すでに署名された Excel ファイルにデジタル署名を追加する

## 導入

今日のデジタル世界において、ドキュメントのセキュリティ保護はこれまで以上に重要になっています。デジタル署名は、特に機密情報を扱う際に、ファイルの真正性と整合性を保証する手段となります。Excelファイルを扱っていて、既に署名済みのワークブックに新しいデジタル署名を追加したいとお考えなら、まさにうってつけです！このガイドでは、Aspose.Cells for .NETを使用して、既に署名済みのExcelファイルにデジタル署名を追加する手順を詳しく説明します。それでは、早速始めましょう！

## 前提条件

コーディングの細部に入る前に、準備しておく必要のあるものがいくつかあります。

1. Aspose.Cells for .NET: .NETプロジェクトにAspose.Cellsライブラリがインストールされていることを確認してください。ダウンロードは以下から行えます。 [サイト](https://releases。aspose.com/cells/net/).
2. 証明書ファイル: 有効な証明書ファイル（通常は `.pfx` デジタル証明書を含むファイル（.dtc）が作成されます。このファイルのパスワードを必ず確認してください。
3. 開発環境: Visual Studio または .NET をサポートするその他の IDE を使用して開発環境をセットアップします。
4. C# の基礎知識: C# プログラミングに精通していると、スムーズに理解できるようになります。
5. サンプルファイル：既にデジタル署名されているサンプルのExcelファイルを用意してください。このファイルに新しい署名を追加します。

準備が整ったので、コーディングを始めましょう。

## パッケージのインポート

まず、C#ファイルに必要なパッケージをインポートする必要があります。手順は以下のとおりです。

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

これらの名前空間を使用すると、Excel ファイルを操作し、デジタル署名をシームレスに処理できるようになります。

## ステップ1: ソースディレクトリと出力ディレクトリを設定する

Excelファイルを操作するには、まずソースファイルの保存場所と出力ファイルの保存場所を定義する必要があります。手順は以下のとおりです。

```csharp
// ソースディレクトリ
string sourceDir = "Your Document Directory";
// 出力ディレクトリ
string outputDir = "Your Document Directory";
```

このステップでは、ソースディレクトリと出力ディレクトリのパスを取得するメソッドを使用します。これらのディレクトリが存在し、必要なファイルが含まれていることを確認してください。

## ステップ2: すでに署名されたワークブックを読み込む

次に、変更したいExcelブックを読み込む必要があります。これは、 `Workbook` クラスを作成し、署名されたファイルのパスを渡します。

```csharp
// すでにデジタル署名されているワークブックをロードします
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```

ここでは、次のワークブックを読み込んでいます。 `sampleDigitallySignedByCells.xlsx`このファイルがすでに署名されていることを確認してください。

## ステップ3: デジタル署名コレクションを作成する

それでは、デジタル署名コレクションを作成しましょう。このコレクションには、ワークブックに追加したいすべてのデジタル署名が格納されます。

```csharp
// デジタル署名コレクションを作成する
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```

この手順は、必要に応じて複数の署名を管理できるため、非常に重要です。

## ステップ4: 新しい証明書を作成する

新しいデジタル署名を作成するには、証明書ファイルを読み込む必要があります。ここで証明書ファイルへのパスを指定します。 `.pfx` ファイルとそのパスワード。

```csharp
// 証明書ファイルとそのパスワード
string certFileName = sourceDir + "AsposeDemo.pfx";
string password = "aspose";

// 新しい証明書を作成する
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```

必ず交換してください `AsposeDemo.pfx` 実際の証明書ファイル名とパスワードを入力します。

## ステップ5：デジタル署名を作成する

証明書を入手したら、デジタル署名を作成できます。署名の理由と現在の日時も入力してください。

```csharp
// 新しいデジタル署名を作成し、デジタル署名コレクションに追加します
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
```

この手順により、新しい署名がコレクションに追加され、後でワークブックに適用されます。

## ステップ6: デジタル署名コレクションをワークブックに追加する

いよいよ、デジタル署名コレクションをワークブックに追加します。ここで魔法が起こります！

```csharp
// ワークブック内にデジタル署名コレクションを追加する
workbook.AddDigitalSignature(dsCollection);
```

この行を実行すると、既に署名されているワークブックに新しいデジタル署名が効果的に添付されます。

## ステップ7: ワークブックを保存して破棄する

最後に、変更したワークブックを出力ディレクトリに保存し、使用されているリソースを解放します。

```csharp
// ワークブックを保存して破棄します。
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```

この手順により、変更が保存され、ワークブックが適切に破棄されてリソースが解放されます。

## ステップ8: 実行の確認

最後に、コードが正常に実行されたことを確認することをお勧めします。これは、簡単なコンソールメッセージで確認できます。

```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```

これにより、操作が成功したというフィードバックが提供され、常に嬉しいものになります。

## 結論

これで完了です！Aspose.Cells for .NET を使用して、既に署名済みの Excel ファイルに新しいデジタル署名を追加できました。デジタル署名は文書の真正性を保証する強力な手段であり、プログラムで管理する方法も習得できました。財務文書、契約書、その他の機密情報を扱う場合でも、デジタル署名を実装することでセキュリティと信頼性を強化できます。

## よくある質問

### デジタル署名とは何ですか?
デジタル署名は、メッセージまたはドキュメントの信頼性と整合性を検証するために使用される暗号化方法です。

### 同じ Excel ファイルに複数のデジタル署名を追加できますか?
はい、デジタル署名コレクションを作成し、同じブックに複数の署名を追加できます。

### Aspose.Cells はデジタル署名にどのような形式をサポートしていますか?
Aspose.Cellsは、次のようなさまざまな形式をサポートしています。 `.pfx` 証明書用。

### Aspose.Cells を使用するには、特定のバージョンの .NET が必要ですか?
チェックしてください [Aspose.Cells ドキュメント](https://reference.aspose.com/cells/net/) .NET バージョンとの互換性のためです。

### Aspose.Cells の一時ライセンスを取得するにはどうすればよいですか?
一時ライセンスの申請は [Asposeの購入ページ](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}