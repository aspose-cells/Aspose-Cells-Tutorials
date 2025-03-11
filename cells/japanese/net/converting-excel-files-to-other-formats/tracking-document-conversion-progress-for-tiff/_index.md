---
title: .NET でプログラム的に TIFF のドキュメント変換の進行状況を追跡する
linktitle: .NET でプログラム的に TIFF のドキュメント変換の進行状況を追跡する
second_title: Aspose.Cells .NET Excel 処理 API
description: ステップバイステップ ガイドを使用して、Aspose.Cells for .NET を使用して TIFF 変換の進行状況をプログラムで追跡する方法を学びます。ドキュメント管理スキルを強化します。
weight: 21
url: /ja/net/converting-excel-files-to-other-formats/tracking-document-conversion-progress-for-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的に TIFF のドキュメント変換の進行状況を追跡する

## 導入
ドキュメント変換の世界に飛び込んでみませんか? Aspose.Cells for .NET を使用している場合は、素晴らしい体験が待っています。この強力なライブラリを使用すると、Excel ファイルを驚くほど簡単に処理でき、スプレッドシートを TIFF などのさまざまな形式に変換できます。このチュートリアルでは、ドキュメントが TIFF 画像にレンダリングされるときに、その変換の進行状況を追跡する方法を説明します。傑作を描いているときに、ブラシの各ストロークが最終的な画像にどのように影響するかを知りたいと想像してください。それが、変換の進行状況を追跡する感覚です。
この記事では、プロセスを段階的に説明し、各要素を完全に理解できるようにします。熟練した開発者でも、初心者でも、ドキュメント処理スキルを向上させるのに役立つ洞察と実用的なコード スニペットが見つかります。さあ、袖をまくって Aspose.Cells の世界に飛び込みましょう。
## 前提条件
コーディングの楽しさに飛び込む前に、すべてが整っていることを確認しましょう。始めるために必要なものは次のとおりです。
1. Visual Studio: マシンに Visual Studio がインストールされていることを確認します。ここでコードを記述してテストします。
2.  Aspose.Cells for .NET: Aspose.Cellsライブラリをダウンロードしてインストールする必要があります。最新バージョンは以下から入手できます。[ここ](https://releases.aspose.com/cells/net/).
3. C# の基礎知識: C# プログラミングの基礎を理解すると、コードをスムーズに操作できるようになります。
これらの前提条件が整ったら、ドキュメント変換の世界に飛び込む準備が整います。
## パッケージのインポート
コーディングを始める前に、必要なパッケージをインポートする必要があります。手順は次のとおりです。
1. Visual Studio を開き、新しいコンソール アプリケーション プロジェクトを作成します。
2. Aspose.Cells は NuGet パッケージ マネージャーからインストールします。ソリューション エクスプローラーでプロジェクトを右クリックし、[NuGet パッケージの管理] を選択して Aspose.Cells を検索することでインストールできます。[インストール] をクリックすると、プロジェクトに追加されます。
ライブラリをインストールしたら、C# ファイルの先頭に適切な using ディレクティブを追加する必要があります。
```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.Rendering;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
さて、ここからは、ドキュメント変換の進行状況を追跡するためのステップバイステップ ガイドという、興味深い部分に進みましょう。
## ステップ1: ソースディレクトリと出力ディレクトリを設定する
まず、ソース ドキュメントが配置されている場所と、出力 TIFF ファイルを保存する場所を定義する必要があります。設定方法は次のとおりです。
```csharp
//ソースディレクトリ
string sourceDir = "Your Document Directory";
//出力ディレクトリ
string outputDir = "Your Document Directory";
```
必ず交換してください`"Your Document Directory"` Excel ファイルが保存されている実際のパスと、TIFF ファイルを保存する場所を入力します。
## ステップ2: ワークブックを読み込む
それでは、変換したい Excel ブックを読み込んでみましょう。Aspose.Cells を使用すると、これが非常に簡単になります。手順は次のとおりです。
```csharp
Workbook workbook = new Workbook(sourceDir + "sampleUseWorkbookRenderForImageConversion.xlsx");
```
この行では、`"sampleUseWorkbookRenderForImageConversion.xlsx"` Excelファイルの名前を入力します。この行は`Workbook`オブジェクトは、メモリ内のスプレッドシートを表します。
## ステップ3: 画像または印刷オプションを作成する
次に、ワークブックを TIFF 形式でレンダリングするためのオプションを設定する必要があります。ここでは、カスタム ページ保存コールバックを含むさまざまな設定を指定できます。
```csharp
ImageOrPrintOptions opts = new ImageOrPrintOptions();
opts.PageSavingCallback = new TestTiffPageSavingCallback();
opts.ImageType = ImageType.Tiff;
```
ここでは、インスタンスを作成しています`ImageOrPrintOptions`そして、カスタムコールバッククラスを使用するように指示します。`TestTiffPageSavingCallback`、進捗状況を追跡します。また、出力画像の種類を TIFF に指定します。
## ステップ4: ページ保存コールバックを実装する
コンバージョンの進捗を追跡する上で重要なのは、`IPageSavingCallback`インターフェース。ここで、各ページの保存の開始時と終了時に何が起こるかを定義します。設定方法は次のとおりです。
```csharp
public class TestTiffPageSavingCallback : IPageSavingCallback
{
    public void PageStartSaving(PageStartSavingArgs args)
    {
        Console.WriteLine("Start saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        //ページインデックス 2 より前のページは出力しません。
        if (args.PageIndex < 2)
        {
            args.IsToOutput = false;
        }
    }
    public void PageEndSaving(PageEndSavingArgs args)
    {
        Console.WriteLine("End saving page index {0} of pages {1}", args.PageIndex, args.PageCount);
        //ページインデックス 8 以降のページは出力しません。
        if (args.PageIndex >= 8)
        {
            args.HasMorePages = false;
        }
    }
}
```
では`PageStartSaving`この方法では、保存を開始する前にページインデックスと合計ページ数をログに記録します。さらに、出力するページを制御することもできます。この場合、インデックス2より前のページをスキップします。同様に、`PageEndSaving`この方法を使用すると、ページの保存が完了したときにログに記録し、インデックス 8 以降のページが保存されないようにすることもできます。
## ステップ5: ワークブックを画像にレンダリングする
オプションの設定とコールバックの実装が完了したので、ワークブックをレンダリングする準備ができました。手順は次のとおりです。
```csharp
WorkbookRender wr = new WorkbookRender(workbook, opts);
wr.ToImage(outputDir + "DocumentConversionProgressForTiff_out.tiff");
```
この行はインスタンスを作成します`WorkbookRender`、私たちの`workbook`そして先ほど設定したオプションを呼び出します`ToImage`TIFF ファイルの出力パスを指定します。
## ステップ6: 成功メッセージ
最後に、変換が成功したというフィードバックを提供しましょう。確認をもらえるのはいつでも嬉しいですよね?
```csharp
Console.WriteLine("DocumentConversionProgressForTiff executed successfully.");
```
これにより、すべてが計画どおりに進んだことを知らせる成功メッセージがコンソールに表示されます。
## 結論
おめでとうございます。Aspose.Cells for .NET を使用して TIFF イメージのドキュメント変換の進行状況を追跡する方法を学習しました。これらの手順に従うことで、Excel ドキュメントの変換を簡単に管理し、プロセスの各段階を把握することができます。この機能は、進行状況を監視したり、特定のページの出力を制御したりする必要がある大規模なドキュメントに特に役立ちます。
自由にコードを試して、ニーズに合わせてさらにカスタマイズしてください。コーディングを楽しんでください!
## よくある質問
### Aspose.Cells とは何ですか?  
Aspose.Cells は、幅広い形式と機能をサポートし、Excel ファイルをプログラムで操作できる .NET ライブラリです。
### 他の形式の変換の進行状況を追跡できますか?  
はい。コールバック メカニズムは、PDF や JPEG などの他の形式にも適応できます。
### Aspose.Cells を使用するにはライセンスが必要ですか?  
無料でお試しいただけますが、本番環境でフル機能を使用するにはライセンスが必要です。詳細については[ここ](https://purchase.aspose.com/buy).
### 問題が発生した場合、どこでサポートを受けることができますか?  
訪問することができます[Aspose サポート フォーラム](https://forum.aspose.com/c/cells/9)コミュニティと Aspose チームからのサポートに感謝します。
### Aspose.Cells を使い始めるにはどうすればよいですか?  
ライブラリをダウンロードして、[ドキュメント](https://reference.aspose.com/cells/net/)チュートリアルと例については、こちらをご覧ください。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
