---
"description": "わかりやすいガイドで、Aspose.Cells for .NET を使用して Excel から PDF への変換時に外部リソースを制御する方法を学びます。"
"linktitle": "Aspose.Cells で Excel の外部リソースを PDF に制御する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "Aspose.Cells で Excel の外部リソースを PDF に制御する"
"url": "/ja/net/rendering-and-export/control-loading-of-external-resources/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells で Excel の外部リソースを PDF に制御する

## 導入
今日のデジタル時代において、ExcelスプレッドシートをPDFドキュメントに変換することは日常的なタスクです。レポート、財務データ、プレゼンテーション資料など、どのようなファイルを作成する場合でも、PDFが意図した通りの仕上がりになることは重要です。Aspose.Cells for .NETは、この変換プロセスを細部に至るまで制御できる強力なライブラリです。特に、Excelファイルに付随する画像などの外部リソースを扱う際に役立ちます。このガイドでは、Aspose.Cellsを使用してExcelからPDFへの変換プロセス中に外部リソースを制御する方法について詳しく説明します。さあ、お気に入りの飲み物を用意して、早速始めましょう！
## 前提条件
具体的な内容に入る前に、始めるのに必要なものがすべて揃っているか確認しましょう。簡単なチェックリストはこちらです。
1. Visual Studio または任意の .NET 互換 IDE: コードを記述してテストするための環境が必要になります。
2. Aspose.Cells for .NET: まだインストールしていない場合は、 [Aspose ダウンロード](https://releases.aspose.com/cells/net/) ページにアクセスして最新バージョンを入手してください。
3. C#の基礎知識：C#プログラミング言語の知識があると役立ちます。不明な概念があれば、遠慮なく調べてください。
4. サンプルExcelファイル：変換したい外部リソースを含むExcelファイルを用意してください。提供されているサンプルファイル「samplePdfSaveOptions_StreamProvider.xlsx」を使用できます。
5. テスト用の画像ファイル：これは変換中に外部リソースとして使用されます。画像ファイル「newPdfSaveOptions_StreamProvider.png」は適切なプレースホルダーです。
## パッケージのインポート
まず、Aspose.Cellsライブラリから必要な名前空間をインポートする必要があります。これは、Aspose.Cellsの機能にアクセスするために不可欠です。ファイルの先頭に以下のusingディレクティブを追加してください。
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
最初の仕事は、次のものを実装するストリームプロバイダクラスを作成することです。 `IStreamProvider` インターフェース。このクラスを使用すると、外部リソースの読み込み方法を制御できます。
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
        // メモリストリーム内の新しい画像を読み取り、Streamプロパティに割り当てます。
        byte[] bts = File.ReadAllBytes(sourceDir + "newPdfSaveOptions_StreamProvider.png");
        MemoryStream ms = new MemoryStream(bts);
        options.Stream = ms;
    }
}
```
このクラスでは:
- CloseStream: このメソッドはストリームが閉じられたときに呼び出されます。今のところは、追跡用のデバッグメッセージを書き込むだけです。
- InitStream: ここから魔法が始まります。ここでは外部画像をバイト配列として読み込み、メモリストリームに変換し、 `options.Stream` 財産。
## ステップ2: ソースディレクトリと出力ディレクトリを設定する
ストリーム プロバイダーの準備ができたので、Excel ファイルの場所と PDF を保存する場所を決定します。
```csharp
// ソースディレクトリ
string sourceDir = "Your Document Directory";
// 出力ディレクトリ
string outputDir = "Your Document Directory";
```
単に置き換える `"Your Document Directory"` ファイルが保存されているコンピュータ上の実際のパスを入力してください。ファイルを整理整頓しておくことが重要です。
## ステップ3: Excelファイルを読み込む
次に、PDF を作成する Excel ファイルを読み込みます。
```csharp
// 外部画像を含むソースExcelファイルを読み込む
Workbook wb = new Workbook(sourceDir + "samplePdfSaveOptions_StreamProvider.xlsx");
```
私たちは `Workbook` Aspose.CellsのクラスはExcelファイルを表します。ファイルには、変換中に制御したい画像などのさまざまな外部リソースを含めることができます。
## ステップ4: PDF保存オプションを設定する
ワークブックをPDFとして保存する前に、保存方法を指定しましょう。これらのオプションは、必要に応じて調整できます。
```csharp
// PDF保存オプションの指定 - ストリームプロバイダー
PdfSaveOptions opts = new PdfSaveOptions();
opts.OnePagePerSheet = true; // 各シートを新しいページに保存します
```
ここでは、新しいインスタンスを作成します `PdfSaveOptions`では、PDFのフォーマットをカスタマイズできます。 `OnePagePerSheet` このオプションは、最終的な PDF で各 Excel シートが独自のページになるようにするのに便利です。
## ステップ5: ストリームプロバイダーを割り当てる
PDF オプションを設定したら、外部リソースにカスタム ストリーム プロバイダーを使用するように Aspose に指示する必要があります。
```csharp
wb.Settings.StreamProvider = new MyStreamProvider();
```
この線はあなたの `Workbook` インスタンス `MyStreamProvider` 先ほど作成したクラスです。つまり、変換中に外部リソースが検出されると、プロバイダーは指定どおりに処理します。
## ステップ6: ワークブックをPDFとして保存する
すべての準備が完了したら、いよいよ Excel ブックを PDF として保存します。
```csharp
// ワークブックをPDFに保存する
wb.Save(outputDir + "outputPdfSaveOptions_StreamProvider.pdf", opts);
```
電話をかけることで `Save` メソッドを使用してワークブック オブジェクトを作成し、出力ディレクトリと PDF オプションを渡すと、Excel ファイルが美しくフォーマットされた PDF に変換されます。
## ステップ7: 実行が成功したことを確認する
最後に、プロセスが成功したことを確認するのは常に良いことです。
```csharp
Console.WriteLine("ControlLoadingOfExternalResourcesInExcelToPDF executed successfully.\r\n");
```
コンソールに成功メッセージを出力すると、操作のステータスを把握しやすくなります。コードにこのような小さな確認メッセージを含めるのは良い習慣です。
## 結論
これで完了です！これらの簡単な手順に従うだけで、Aspose.Cells を使用して Excel から PDF への変換時に外部リソースをどのように処理するかを巧みに制御できます。これにより、ドキュメントに画像やその他の外部要素を正確に組み込むことができるようになり、常に洗練された最終製品が完成します。
## よくある質問
### Aspose.Cells とは何ですか?  
Aspose.Cells は、さまざまな形式で Excel ファイルを作成、操作、変換、レンダリングできる .NET 開発者向けの強力なライブラリです。
### Aspose.Cells をダウンロードするにはどうすればいいですか?  
Aspose.Cellsの最新バージョンは、以下からダウンロードできます。 [ダウンロードリンク](https://releases。aspose.com/cells/net/).
### Aspose.Cells を無料で試すことはできますか?  
はい！無料トライアルは [無料トライアルページ](https://releases。aspose.com/).
### Aspose.Cells のサポートはどこで見つかりますか?  
サポートに関するお問い合わせは、 [Aspose サポートフォーラム](https://forum。aspose.com/c/cells/9).
### Aspose.Cells の一時ライセンスを取得するにはどうすればよいですか?  
一時ライセンスを申請できます [ここ](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}