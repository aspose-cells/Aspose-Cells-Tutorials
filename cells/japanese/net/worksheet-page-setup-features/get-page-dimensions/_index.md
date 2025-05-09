---
"description": "Aspose.Cells for .NET を使用して Excel ワークシートのページサイズを取得する方法を学びます。A2、A3、A4、レターの用紙サイズをカスタマイズするためのステップバイステップガイドです。"
"linktitle": "ワークシートのページサイズを取得する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "ワークシートのページサイズを取得する"
"url": "/ja/net/worksheet-page-setup-features/get-page-dimensions/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ワークシートのページサイズを取得する

## 導入
Aspose.Cells for .NET を使用して Excel ファイルをプログラムで操作している場合、ワークシートのページサイズにアクセスして設定する必要があることがあります。ページサイズを把握しておくと、Excel シートのレイアウト、印刷、カスタマイズなど、特定の用途に合わせて作業を進めるのに役立ちます。この記事では、Aspose.Cells for .NET を使用して Excel でさまざまなページサイズを取得および表示する方法について説明します。ステップバイステップのチュートリアルで詳細を解説し、自信を持って使い始めることができるようにします。
## 前提条件
始める前に、このチュートリアルに従うために必要なものがすべて揃っていることを確認しましょう。
1. Aspose.Cells for .NET: Aspose.Cells for .NETがインストールされていることを確認してください。 [ライブラリはこちらからダウンロードできます](https://releases.aspose.com/cells/net/) または、.NET プロジェクトで NuGet 経由でインストールします。
2. .NET 環境: 互換性のある .NET 開発環境 (Visual Studio など)。
3. ライセンス設定：Aspose.Cellsの全機能を使用するには、ライセンスを適用してください。 [無料の一時ライセンスをリクエストする](https://purchase.aspose.com/temporary-license/) 評価目的のため。
初めて評価する場合は、Aspose.Cells の無料試用版から始めてください。
## パッケージのインポート
コードに進む前に、必要なすべてのクラスとメソッドにアクセスするために、Aspose.Cells 名前空間をプロジェクトにインポートする必要があります。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
プロセスを簡単なステップに分解してみましょう。ここでは、さまざまな用紙サイズにアクセスし、それらをワークシートに適用し、それぞれの寸法を印刷します。
## ステップ1: ワークブックインスタンスを作成する
最初のステップは、 `Workbook` クラスです。このオブジェクトは、操作可能なワークシートを含むメインのワークブックとして機能します。
```csharp
Workbook book = new Workbook();
```
考えてみてください `Workbook` Excelファイルのメインコンテナとして。個々のワークシートにアクセスして制御するために必要です。
## ステップ2: 最初のワークシートにアクセスする
次に、ワークブックの最初のワークシートにアクセスしてみましょう。デフォルトでは、新しいワークブックには1つのシートが含まれているので、インデックスを使って直接参照することができます。 `0`。
```csharp
Worksheet sheet = book.Worksheets[0];
```
その `Worksheets` コレクション `Workbook` インデックスを使って各ワークシートにアクセスできます。ここでは、最初のシートを取得してページサイズの設定を開始します。
## ステップ3: 用紙サイズをA2に設定し、寸法を表示します。
ワークシートにアクセスできるようになりましたので、用紙サイズをA2に設定しましょう。用紙サイズの設定は、印刷またはエクスポート前にページの書式を設定するのに役立ちます。用紙サイズを設定すると、ページのサイズがインチ単位で印刷されます。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
ここでは、 `PaperSize` 財産に `PaperA2`サイズを設定したら、 `PageSetup.PaperWidth` そして `PageSetup.PaperHeight` シートの幅と高さをインチ単位で取得します。これにより、ページのサイズを簡単に把握できます。
## ステップ4: 用紙サイズをA3に設定し、寸法を表示する
上記と同じ手順に従って、ページサイズをA3サイズに調整しましょう。この変更は、少し大きめに印刷する場合や、1ページに多くのコンテンツを収めたい場合に便利です。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
A3サイズはA4の2倍の大きさなので、大きな表や詳細なグラフを作成するのに適しています。用紙サイズを変更すると、ワークシートのレイアウトもそれに応じて調整できます。
## ステップ5: 用紙サイズをA4に設定し、寸法を表示する
それでは、用紙サイズをA4に設定しましょう。これは文書の印刷で最も一般的に使用されるページサイズです。変更後の寸法は後ほど表示されます。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
標準的な文書形式をターゲットとする場合、通常はA4サイズが最適です。寸法を知っておくと、印刷上の問題を回避するためにコンテンツのレイアウトを調整するのに役立ちます。
## ステップ6: 用紙サイズをレターに設定し、寸法を表示する
最後に、用紙サイズを北米で一般的に使用されているレター形式に設定します。最後にもう一度寸法を印刷してみましょう。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
レター サイズは北米のドキュメントで広く使用されているため、このサイズを設定すると、北米に拠点を置くチームやクライアントと共同作業を行うときに役立ちます。
## 結論
このチュートリアルでは、Aspose.Cells for .NET を使用して、様々な用紙サイズのページサイズを設定および取得する方法を解説しました。A2、A3、A4、レターなどのページサイズを設定することで、Excelワークシートを特定の印刷およびレイアウトのニーズに合わせてフォーマットできます。ページサイズを細かく制御できる機能は、コンテンツが各ページサイズに完璧に収まるため、特にプロフェッショナルなレポート作成やプレゼンテーションに有効です。
## よくある質問
### Aspose.Cells でページの向きを変更するにはどうすればよいですか?  
方向を変えるには `PageSetup.Orientation` プロパティを、 `PageOrientationType.Pまたはtrait` or `PageOrientationType。Landscape`.
### Aspose.Cells でカスタム ページ サイズを設定できますか?  
はい、余白と拡大縮小オプションを調整することで、カスタムページサイズを設定できます。 `PageSetup` より詳細な制御が可能になります。
### Aspose.Cells のデフォルトの用紙サイズは何ですか?  
デフォルトの用紙サイズは通常A4です。ただし、地域設定によって異なる場合があり、必要に応じて調整できます。
### Aspose.Cells でページレイアウトをプレビューすることは可能ですか?  
Aspose.Cells ではグラフィカルなプレビューは提供されませんが、プログラムでレイアウトを設定し、Excel で印刷プレビューを使用することができます。
### Aspose.Cells for .NET をインストールするにはどうすればよいですか?  
Aspose.CellsはVisual StudioのNuGetパッケージマネージャーを使用してインストールするか、DLLを [Aspose.Cells のダウンロードページ](https://releases。aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}