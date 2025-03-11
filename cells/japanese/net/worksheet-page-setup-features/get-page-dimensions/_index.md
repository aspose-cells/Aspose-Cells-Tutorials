---
title: ワークシートのページサイズを取得する
linktitle: ワークシートのページサイズを取得する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して Excel ワークシートのページ サイズを取得する方法を学びます。A2、A3、A4、レターの用紙サイズをカスタマイズするためのステップ バイ ステップ ガイドです。
weight: 13
url: /ja/net/worksheet-page-setup-features/get-page-dimensions/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ワークシートのページサイズを取得する

## 導入
Aspose.Cells for .NET を使用してプログラムで Excel ファイルを操作している場合、ワークシートのページ サイズにアクセスして設定する必要がある場合があります。サイズを知っておくと、特定の目的に合わせて Excel シートをレイアウト、印刷、カスタマイズするのに役立ちます。この記事では、Aspose.Cells for .NET を使用して Excel でさまざまなページ サイズを取得して表示する方法について説明します。自信を持って開始できるように、詳細をすべて把握できるように、ステップ バイ ステップのチュートリアルを進めていきます。
## 前提条件
始める前に、このチュートリアルに従うために必要なものがすべて揃っていることを確認しましょう。
1.  Aspose.Cells for .NET: Aspose.Cells for .NETがインストールされていることを確認してください。[ライブラリをここからダウンロード](https://releases.aspose.com/cells/net/)または、NuGet 経由で .NET プロジェクトにインストールします。
2. .NET 環境: 互換性のある .NET 開発環境 (Visual Studio など)。
3. ライセンス設定: Aspose.Cellsの全機能を使用するには、ライセンスを適用してください。[無料の一時ライセンスをリクエストする](https://purchase.aspose.com/temporary-license/)評価目的のため。
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
最初のステップは、`Workbook`クラス。このオブジェクトは、操作可能なワークシートを含むメインのワークブックとして機能します。
```csharp
Workbook book = new Workbook();
```
考えてみてください`Workbook` Excel ファイルのメイン コンテナーとして使用します。個々のワークシートにアクセスして制御するために必要です。
## ステップ2: 最初のワークシートにアクセスする
次に、ワークブックの最初のワークシートにアクセスしてみましょう。デフォルトでは、新しいワークブックには1つのシートが付属しているので、次のインデックスを使用して直接参照することができます。`0`.
```csharp
Worksheet sheet = book.Worksheets[0];
```
の`Worksheets`コレクション`Workbook`インデックスによって各ワークシートにアクセスできます。ここでは、最初のシートを取得してページ サイズの設定を開始します。
## ステップ3: 用紙サイズをA2に設定し、寸法を表示する
ワークシートにアクセスできるようになりましたので、用紙サイズを A2 に設定しましょう。用紙サイズを設定すると、印刷またはエクスポートする前にページをフォーマットするのに役立ちます。用紙サイズを設定したら、ページ寸法をインチ単位で印刷します。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA2;
Console.WriteLine("PaperA2: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
ここでは、`PaperSize`財産に`PaperA2`サイズを設定したら、`PageSetup.PaperWidth`そして`PageSetup.PaperHeight`シートの幅と高さをインチ単位で取得します。これにより、ページのサイズの概要を簡単に把握できます。
## ステップ4: 用紙サイズをA3に設定し、寸法を表示する
上記と同じ手順に従って、ページのサイズを A3 サイズに調整しましょう。この変更は、少し大きめに印刷する場合や、1 ページに多くのコンテンツを収める場合に便利です。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA3;
Console.WriteLine("PaperA3: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
A3 サイズは A4 の 2 倍のサイズなので、大きな表や詳細なグラフに適しています。用紙サイズを変更すると、ワークシートのレイアウトをそれに応じて調整できます。
## ステップ5: 用紙サイズをA4に設定し、寸法を表示する
ここで、用紙サイズを A4 に設定しましょう。これは、ドキュメントの印刷に最もよく使用されるページ サイズです。後で更新された寸法を表示します。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperA4;
Console.WriteLine("PaperA4: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
ターゲットが標準のドキュメント形式である場合、通常は A4 が最も適したサイズです。寸法を知っておくと、コンテンツのレイアウトを調整して印刷の問題を回避するのに役立ちます。
## ステップ6: 用紙サイズをレターに設定し、寸法を表示する
最後に、用紙サイズを北米で一般的に使用されているレター形式に設定します。最後にもう一度寸法を印刷してみましょう。
```csharp
sheet.PageSetup.PaperSize = PaperSizeType.PaperLetter;
Console.WriteLine("PaperLetter: " + sheet.PageSetup.PaperWidth + "x" + sheet.PageSetup.PaperHeight);
```
レター サイズは北米のドキュメントで広く使用されているため、このサイズを設定すると、北米に拠点を置くチームやクライアントと共同作業するときに役立ちます。
## 結論
このチュートリアルでは、Aspose.Cells for .NET を使用して、さまざまな用紙サイズのページ寸法を設定および取得する方法について説明しました。A2、A3、A4、レターなどのページ サイズを構成することで、Excel ワークシートを特定の印刷およびレイアウトのニーズに合わせてフォーマットできます。ページ寸法のこの制御は、コンテンツが各ページ サイズに完全に収まるようにするため、専門的なレポート作成やプレゼンテーションに特に役立ちます。
## よくある質問
### Aspose.Cells でページの向きを変更するにはどうすればよいですか?  
方向を変えるには`PageSetup.Orientation`プロパティを、`PageOrientationType.Portrait`または`PageOrientationType.Landscape`.
### Aspose.Cells でカスタム ページ サイズを設定できますか?  
はい、余白と拡大縮小オプションを調整することで、カスタムページサイズを設定できます。`PageSetup`より詳細な制御が可能になります。
### Aspose.Cells のデフォルトの用紙サイズは何ですか?  
デフォルトの用紙サイズは通常 A4 です。ただし、これは地域設定によって異なる場合があり、必要に応じて調整できます。
### Aspose.Cells でページ レイアウトをプレビューすることは可能ですか?  
Aspose.Cells ではグラフィカルなプレビューは提供されませんが、プログラムでレイアウトを設定し、Excel で印刷プレビューを使用することができます。
### Aspose.Cells for .NET をインストールするにはどうすればよいですか?  
 Aspose.CellsはVisual StudioのNuGetパッケージマネージャーを使用してインストールするか、[Aspose.Cells ダウンロード ページ](https://releases.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
