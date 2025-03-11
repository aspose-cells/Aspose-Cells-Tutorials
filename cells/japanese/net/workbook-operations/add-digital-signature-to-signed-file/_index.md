---
title: 署名された Excel ファイルにデジタル署名を追加する
linktitle: 署名された Excel ファイルにデジタル署名を追加する
second_title: Aspose.Cells .NET Excel 処理 API
description: このステップバイステップ ガイドでは、Aspose.Cells for .NET を使用して、既に署名されている Excel ファイルにデジタル署名を追加する方法を説明します。ドキュメントを保護します。
weight: 12
url: /ja/net/workbook-operations/add-digital-signature-to-signed-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 署名された Excel ファイルにデジタル署名を追加する

## 導入
今日のデジタル世界では、ドキュメントの信頼性と整合性を確保することが非常に重要です。デジタル署名は、ドキュメントが改ざんされていないこと、および正当なソースから送信されたものであることを確認するための強力な手段として機能します。.NET で Excel ファイルを操作していて、既に署名されているファイルにデジタル署名を追加したい場合は、ここが最適な場所です。このガイドでは、Aspose.Cells for .NET を使用して、既存の署名済み Excel ファイルに新しいデジタル署名を追加するプロセスについて説明します。 
## 前提条件
細かい点に入る前に、始めるのに必要なものがすべて揃っていることを確認しましょう。
1.  Aspose.Cells for .NET: まず最初に、.NET環境にAspose.Cellsをインストールする必要があります。[リリースページ](https://releases.aspose.com/cells/net/).
2. .NET Framework: マシンに .NET Framework が設定されていることを確認してください。このガイドでは、読者が基本的な .NET プログラミングの概念を理解していることを前提としています。
3. デジタル証明書: デジタル署名を作成するには、有効なデジタル証明書 (.pfx 形式) が必要です。デジタル証明書がない場合は、テスト目的で自己署名証明書を作成できます。
4. 開発環境: C# コードを記述して実行できる Visual Studio などのコード エディターまたは IDE。
5. サンプル Excel ファイル: すでにデジタル署名されている既存の Excel ファイルが必要です。これが、別の署名を追加するファイルになります。
これらの前提条件を満たしたら、コードに進みましょう。
## パッケージのインポート
コーディングを始める前に、必要な名前空間をインポートしてください。C# ファイルの先頭に含める必要があるものは次のとおりです。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
これらの名前空間を使用すると、Excel ファイルを操作し、デジタル署名を処理するために必要なクラスとメソッドにアクセスできるようになります。
それでは、プロセスを管理しやすいステップに分解してみましょう。各ステップを説明して、すでに署名されている Excel ファイルにデジタル署名を追加する方法を理解できるようにします。
## ステップ1: ディレクトリを定義する
まず、ソース ファイルの場所と出力ファイルの保存場所を指定する必要があります。これは簡単ですが、非常に重要です。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory"; //実際のディレクトリに置き換えます
//出力ディレクトリ
string outputDir = "Your Document Directory"; //実際のディレクトリに置き換えます
```
交換する`"Your Document Directory"`ファイルが保存されている実際のパスを入力します。これにより、ファイル操作の準備が整います。
## ステップ2: 既存の署名済みワークブックを読み込む
次に、すでに署名されている既存の Excel ブックを読み込みます。ここから魔法が始まります。
```csharp
//すでにデジタル署名されているワークブックをロードして、新しいデジタル署名を追加します。
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```
この行は新しい`Workbook`オブジェクトを指定されたファイルに関連付けます。ファイル名が既存の署名済み Excel ファイルと一致していることを確認します。
## ステップ3: デジタル署名コレクションを作成する
デジタル署名を管理するには、コレクションを作成する必要があります。これにより、必要に応じて複数の署名を保持できます。
```csharp
//デジタル署名コレクションを作成する
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```
このコレクションは、新しいデジタル署名をワークブックに適用する前に追加する場所になります。
## ステップ4: 証明書を読み込む
次に、デジタル証明書をロードします。この証明書は、新しい署名を作成するために使用されます。
```csharp
//証明書ファイルとそのパスワード
string certFileName = sourceDir + "AsposeDemo.pfx"; //証明書ファイル
string password = "aspose"; //証明書のパスワード
//新しい証明書を作成する
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```
必ず交換してください`AsposeDemo.pfx`証明書ファイルの名前に置き換え、それに応じてパスワードを更新します。正しい証明書がないと有効な署名を作成できないため、この手順は非常に重要です。
## ステップ5: 新しいデジタル署名を作成する
証明書が読み込まれたら、新しいデジタル署名を作成できます。この署名はコレクションに追加されます。
```csharp
//新しいデジタル署名を作成し、デジタル署名コレクションに追加します
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
dsCollection.Add(signature);
```
ここでは、署名を説明するメッセージを指定します。これは記録の保存に役立ちます。タイムスタンプにより、署名が正しい時点に関連付けられていることが保証されます。
## ステップ 6: 署名コレクションをワークブックに追加する
署名を作成したら、コレクション全体をワークブックに追加します。
```csharp
//ワークブック内にデジタル署名コレクションを追加する
workbook.AddDigitalSignature(dsCollection);
```
この手順により、新しいデジタル署名がワークブックに効果的に適用され、信頼性が強化されます。
## ステップ7: ワークブックを保存する
最後に、新しいデジタル署名が含まれたワークブックを保存します。これで、これまでの努力が報われる瞬間です。
```csharp
//ワークブックを保存して破棄します。
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```
出力ファイルの名前を必ず指定してください。これは、追加のデジタル署名が追加された Excel ファイルの新しいバージョンになります。
## ステップ8: 成功を確認する
最後に、操作が正常に完了したらフィードバックを提供することをお勧めします。
```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```
この行は、すべてがスムーズに進んだことを知らせる確認メッセージをコンソールに出力します。
## 結論
これで完了です。Aspose.Cells for .NET を使用して、既に署名されている Excel ファイルに新しいデジタル署名を正常に追加できました。このプロセスにより、ドキュメントのセキュリティが強化されるだけでなく、ドキュメントが信頼性が高く検証可能であることも保証されます。 
デジタル署名は、今日のデジタル環境において、特に文書の整合性を維持する必要がある企業や専門家にとって不可欠です。このガイドに従うことで、Excel ファイル内のデジタル署名を簡単に管理し、データの安全性と信頼性を確保できます。
## よくある質問
### デジタル署名とは何ですか?
デジタル署名は、デジタル メッセージまたはドキュメントの信頼性と整合性を検証するための数学的スキームです。これにより、ドキュメントが改ざんされていないことが保証され、署名者の ID が確認されます。
### デジタル署名を作成するには特別な証明書が必要ですか?
はい、有効なデジタル署名を作成するには、信頼できる証明機関 (CA) によって発行されたデジタル証明書が必要です。
### テストに自己署名証明書を使用できますか?
もちろんです! 開発およびテストの目的で自己署名証明書を作成できますが、運用環境では、信頼できる CA からの証明書を使用するのが最適です。
### 署名されていない文書に署名を追加しようとするとどうなりますか?
まだ署名されていないドキュメントにデジタル署名を追加しようとすると、問題なく機能しますが、元の署名は存在しなくなります。
### Aspose.Cells の詳細情報はどこで入手できますか?
確認するには[Aspose.Cells ドキュメント](https://reference.aspose.com/cells/net/)詳細なガイドと API リファレンスについては、こちらをご覧ください。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
