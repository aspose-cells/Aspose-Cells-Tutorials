---
title: Aspose.Cells で Excel の外部リソースを PDF に制御する
linktitle: Aspose.Cells で Excel の外部リソースを PDF に制御する
second_title: Aspose.Cells .NET Excel 処理 API
description: わかりやすいガイドで、Aspose.Cells for .NET を使用して Excel から PDF への変換で外部リソースを制御する方法を学びます。
weight: 12
url: /ja/net/rendering-and-export/control-loading-of-external-resources/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells で Excel の外部リソースを PDF に制御する

## 導入
今日のデジタル時代では、Excel スプレッドシートを PDF ドキュメントに変換することは一般的な作業です。レポート、財務データ、プレゼンテーション資料などを作成する場合でも、PDF が意図したとおりに表示されるようにする必要があります。Aspose.Cells for .NET は、特に Excel ファイルに付随する画像などの外部リソースを処理する場合に、この変換プロセスを細部に至るまで制御できる強力なライブラリです。このガイドでは、Aspose.Cells を使用して Excel から PDF への変換プロセス中に外部リソースを制御する方法について詳しく説明します。では、お気に入りの飲み物を手に取って、始めましょう。
## 前提条件
細かい点に入る前に、始めるのに必要なものがすべて揃っているかどうか確認しましょう。簡単なチェックリストを以下に示します。
1. Visual Studio または .NET 互換の IDE: コードを記述してテストするための環境が必要になります。
2.  Aspose.Cells for .NET: まだインストールしていない場合は、[Aspose ダウンロード](https://releases.aspose.com/cells/net/)ページにアクセスして最新バージョンを入手してください。
3. C# の基礎知識: C# プログラミング言語の知識があると役立ちます。概念について不明な点がある場合は、遠慮なく調べてください。
4. サンプル Excel ファイル: 変換する外部リソースを含む Excel ファイルを準備します。提供されているサンプル ファイル「samplePdfSaveOptions_StreamProvider.xlsx」を使用できます。
5. テスト用のイメージ ファイル: これは、変換中に外部リソースとして使用されます。イメージ ファイル「newPdfSaveOptions_StreamProvider.png」は適切なプレースホルダーです。
## パッケージのインポート
まず、Aspose.Cells ライブラリから必要な名前空間をインポートする必要があります。これは、その機能にアクセスするために重要です。ファイルの先頭に次の using ディレクティブを追加してください。
```csharp
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
```
これらのパッケージは、タスクを実行するために必要なすべての重要なクラスとメソッドを提供します。
## ステップ1: ストリームプロバイダークラスを作成する
最初の仕事は、ストリームプロバイダクラスを作成し、`IStreamProvider`インターフェース。このクラスを使用すると、外部リソースの読み込み方法を制御できます。
```csharp
class MyStreamProvider : IStreamProvider
{
    public void CloseStream(StreamProviderOptions options)
    {
        Debug.WriteLine("-----Close Stream-----");
    }
    public void InitStream(StreamProviderOptions options)
    {
        string sourceDir = "Your Document Directory";
        Debug.WriteLine("-----Init Stream-----");
        //メモリストリーム内の新しい画像を読み取り、Streamプロパティに割り当てます。
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
このクラスでは:
- CloseStream: このメソッドは、ストリームが閉じられたときに呼び出されます。現時点では、追跡用のデバッグ メッセージを書き込むだけです。
-  InitStream: ここから魔法が始まります。ここでは、外部画像をバイト配列として読み込み、メモリストリームに変換し、`options.Stream`財産。
## ステップ2: ソースディレクトリと出力ディレクトリを設定する
ストリーム プロバイダーの準備ができたので、Excel ファイルの場所と PDF を保存する場所を決定します。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
//出力ディレクトリ
string outputDir = "Your Document Directory";
```
単に置き換える`"Your Document Directory"`ファイルが保存されているコンピュータ上の実際のパスを入力します。ファイルを整理しておくことが重要です。
## ステップ3: Excelファイルを読み込む
次に、PDF を作成する Excel ファイルを読み込みます。
```csharp
//外部画像を含むソースExcelファイルを読み込む
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
私たちは`Workbook`Aspose.Cells のクラスで、Excel ファイルを表します。ファイルには、変換中に制御する画像などのさまざまな外部リソースを含めることができます。
## ステップ4: PDF保存オプションを設定する
ワークブックを PDF として保存する前に、保存方法を指定しましょう。これらのオプションは、必要に応じて調整できます。
```csharp
// PDF 保存オプションの指定 - ストリーム プロバイダー
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; //各シートを新しいページに保存する
```
ここでは、新しいインスタンスを作成します`PdfSaveOptions`では、PDFのフォーマットをカスタマイズできます。`OnePagePerSheet`このオプションは、最終的な PDF で各 Excel シートが独自のページになるようにするのに便利です。
## ステップ5: ストリームプロバイダーを割り当てる
PDF オプションを設定したら、外部リソースにカスタム ストリーム プロバイダーを使用するように Aspose に指示する必要があります。
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
この線はあなたの`Workbook`インスタンス`MyStreamProvider`以前に作成したクラスです。つまり、変換中に外部リソースが検出されると、プロバイダーはそれを指定どおりに処理します。
## ステップ6: ワークブックをPDFとして保存する
すべての準備が完了したら、Excel ブックを PDF として保存します。
```csharp
//ワークブックをPDFに保存する
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
電話をかけることで`Save`メソッドをワークブック オブジェクトに適用し、出力ディレクトリと PDF オプションを渡すと、Excel ファイルが美しくフォーマットされた PDF に変換されます。
## ステップ7: 実行が成功したことを確認する
最後に、プロセスが成功したことを確認するのは常に良いことです。
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
コンソールに成功メッセージを出力すると、操作のステータスを把握しやすくなります。コードにこのような小さな確認を含めるのは良い習慣です。
## 結論
これで完了です。これらの簡単な手順に従うことで、Aspose.Cells を使用して Excel から PDF への変換中に外部リソースがどのように処理されるかを巧みに制御できます。つまり、ドキュメントに画像やその他の外部要素を正確に含めることができるようになり、毎回洗練された最終製品が保証されます。
## よくある質問
### Aspose.Cells とは何ですか?  
Aspose.Cells は、さまざまな形式で Excel ファイルを作成、操作、変換、レンダリングできる、.NET 開発者向けの強力なライブラリです。
### Aspose.Cells をダウンロードするにはどうすればいいですか?  
 Aspose.Cellsの最新バージョンは、以下からダウンロードできます。[ダウンロードリンク](https://releases.aspose.com/cells/net/).
### Aspose.Cells を無料で試すことはできますか?  
はい！無料トライアルは、[無料トライアルページ](https://releases.aspose.com/).
### Aspose.Cells のサポートはどこで見つかりますか?  
サポート関連のお問い合わせについては、[Aspose サポートフォーラム](https://forum.aspose.com/c/cells/9).
### Aspose.Cells の一時ライセンスを取得するにはどうすればよいですか?  
一時ライセンスを申請することができます[ここ](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
