---
title: Xades 署名サポート
linktitle: Xades 署名サポート
second_title: Aspose.Cells for .NET API リファレンス
description: このステップバイステップ ガイドでは、Aspose.Cells for .NET を使用して Excel ファイルに Xades 署名を追加する方法を説明します。ドキュメントを保護します。
weight: 190
url: /ja/net/excel-workbook/xades-signature-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xades 署名サポート

## 導入

今日のデジタル世界では、ドキュメントのセキュリティ保護がこれまで以上に重要になっています。機密性の高いビジネス情報を扱う場合でも、個人データを扱う場合でも、ファイルの整合性と信頼性を確保することが最も重要です。これを実現する方法の 1 つは、デジタル署名、具体的には Xades 署名を使用することです。アプリケーションに Xades 署名サポートを実装しようとしている .NET 開発者であれば、このガイドはまさにうってつけです。このガイドでは、Aspose.Cells for .NET を使用して Excel ファイルに Xades 署名を追加する手順を説明します。それでは、早速始めましょう。

## 前提条件

始める前に、いくつか準備しておく必要があります。

1.  Aspose.Cells for .NET: Aspose.Cellsライブラリがインストールされていることを確認してください。[Aspose ウェブサイト](https://releases.aspose.com/cells/net/).
2. 開発環境: コードを記述して実行できる、実用的な .NET 開発環境 (Visual Studio など)。
3. デジタル証明書: パスワード付きの有効なデジタル証明書 (PFX ファイル) が必要です。この証明書は、デジタル署名を作成するために不可欠です。
4. C# の基礎知識: C# プログラミングに精通していると、例をよりよく理解するのに役立ちます。

これらの前提条件を整理したら、Excel ファイルに Xades 署名を実装する準備が整います。

## パッケージのインポート

Aspose.Cells for .NET を使用するには、必要な名前空間をインポートする必要があります。その方法は次のとおりです。

```csharp
using Aspose.Cells.DigitalSignatures;
using System;
using System.IO;
```

これらの名前空間は、Excel ファイルの操作やデジタル署名の管理に必要なクラスとメソッドへのアクセスを提供します。

これですべての設定が完了したので、Xades 署名を Excel ファイルに追加するプロセスを明確で管理しやすい手順に分解してみましょう。

## ステップ1: ソースディレクトリと出力ディレクトリを設定する

まず、ソース Excel ファイルの場所と、署名された出力ファイルを保存する場所を定義する必要があります。これは、ファイルを効率的に整理するのに役立つため、重要なステップです。

```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
//出力ディレクトリ
string outputDir = "Your Output Directory";
```

## ステップ2: ワークブックを読み込む

次に、署名する Excel ブックを読み込みます。ここで、既存の Excel ファイルを読み込みます。

```csharp
Workbook workbook = new Workbook(sourceDir + "sourceFile.xlsx");
```

ここで、新しいインスタンスを作成します。`Workbook`クラスに、ソース Excel ファイルのパスを渡します。ファイル名がソース ディレクトリにあるファイル名と一致していることを確認します。

## ステップ3: デジタル証明書を準備する

デジタル署名を作成するには、デジタル証明書を読み込む必要があります。これには、PFX ファイルの読み取りとパスワードの提供が含まれます。

```csharp
string password = "pfxPassword"; // PFXパスワードに置き換えます
string pfx = "pfxFile"; //PFXファイルへのパスに置き換えます
```

このステップでは、`pfxPassword`実際のパスワードと`pfxFile`PFX ファイルへのパスを入力します。これがドキュメントに署名するための鍵となります。

## ステップ4: デジタル署名を作成する

それでは、デジタル署名を作成しましょう。`DigitalSignature`クラス。ここで魔法が起きます！

```csharp
DigitalSignature signature = new DigitalSignature(File.ReadAllBytes(pfx), password, "testXAdES", DateTime.Now);
signature.XAdESType = XAdESType.XAdES;
```

このスニペットでは、PFXファイルをバイト配列に読み込み、新しい`DigitalSignature`オブジェクトを設定します。`XAdESType`に`XAdES`これは私たちの署名にとって不可欠です。

## ステップ5: ワークブックに署名を追加する

デジタル署名を作成したら、次の手順ではそれをワークブックに追加します。

```csharp
DigitalSignatureCollection dsCollection = new DigitalSignatureCollection();
dsCollection.Add(signature);
workbook.SetDigitalSignature(dsCollection);
```

ここでは、`DigitalSignatureCollection`署名を追加し、このコレクションをブックに設定します。このようにして、Excel ファイルに署名を添付します。

## ステップ6: 署名されたワークブックを保存する

最後に、署名されたワークブックを出力ディレクトリに保存します。この手順でプロセスが完了します。

```csharp
workbook.Save(outputDir + "XAdESSignatureSupport_out.xlsx");
Console.WriteLine("XAdESSignatureSupport executed successfully.");
```

このコードでは、ワークブックを新しい名前で保存します。`XAdESSignatureSupport_out.xlsx`、出力ディレクトリに保存されます。この手順が完了すると、コンソールに成功メッセージが表示されます。

## 結論

これで完了です。Aspose.Cells for .NET を使用して、Excel ファイルに Xades 署名を正常に追加できました。このプロセスにより、ドキュメントのセキュリティが強化されるだけでなく、ファイルの信頼性が確保され、ユーザーとの信頼関係も構築されます。 
デジタル署名は現代のドキュメント管理に不可欠な要素であり、Aspose.Cells の力により、アプリケーションに簡単に実装できます。

## よくある質問

### Xades の署名とは何ですか?
Xades (XML Advanced Electronic Signatures) は、電子文書の整合性と信頼性を確保するための追加機能を提供するデジタル署名の標準です。

### Xades 署名を作成するにはデジタル証明書が必要ですか?
はい、Xades 署名を作成するには有効なデジタル証明書 (PFX ファイル) が必要です。

### 購入前に Aspose.Cells for .NET をテストできますか?
もちろんです！無料トライアルは[Aspose ウェブサイト](https://releases.aspose.com/).

### Aspose.Cells はすべてのバージョンの .NET と互換性がありますか?
Aspose.Cellsは.NETフレームワークのさまざまなバージョンをサポートしています。[ドキュメント](https://reference.aspose.com/cells/net/)互換性の詳細については、こちらをご覧ください。

### 問題が発生した場合、どこでサポートを受けることができますか?
訪問することができます[Aspose フォーラム](https://forum.aspose.com/c/cells/9)コミュニティのサポートと支援のため。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
