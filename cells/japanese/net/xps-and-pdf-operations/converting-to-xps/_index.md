---
title: .NET で XPS に変換する
linktitle: .NET で XPS に変換する
second_title: Aspose.Cells .NET Excel 処理 API
description: 実用的なコード例を参考に、Aspose.Cells for .NET を使用して Excel ファイルを XPS 形式に変換する方法を簡単な手順で学習します。
weight: 10
url: /ja/net/xps-and-pdf-operations/converting-to-xps/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET で XPS に変換する

## 導入
Excel ファイルを XPS 形式に変換するとなると、特にプログラミングの世界に不慣れな場合や、.NET 開発を始めたばかりの場合は、少し手に負えないと感じるかもしれません。でも、心配はいりません。このガイドでは、Aspose.Cells for .NET をプロのように使用してプロセスを詳しく説明します。読み終える頃には、これを行う方法を明確に理解できるだけでなく、コーディング スキルを高めるための実用的な洞察も得られます。それでは、始めましょう。
## 前提条件
変換の細部に入る前に、必要なものがすべて揃っていることを確認しましょう。必要なものは次のとおりです。
1. Visual Studio: これはコードを記述する IDE です。インストールされていることを確認してください。
2.  Aspose.Cellsライブラリ: Excelファイルを効率的に処理するにはこのライブラリが必要です。ダウンロードするには、[ここ](https://releases.aspose.com/cells/net/).
3. .NET の基礎知識: C# または VB.NET に精通していると、例をよりよく理解できるようになります。
4. Excel ファイル: 作業ディレクトリにサンプルの Excel ファイル (このチュートリアルでは、「Book1.xls」を使用します) を用意しておきます。

## パッケージのインポート
前提条件を説明したので、必要なパッケージのインポートに進みましょう。適切な名前空間をインポートすることは、使用するクラスとメソッドがどこにあるかをコンパイラーに伝えるため、非常に重要です。
### プロジェクトを設定する
まず最初に！Visual Studio を開いて、新しいプロジェクトを作成します。コンソール アプリケーションを選択します。これは簡単で、この種のタスクに最適です。
### プロジェクトに Aspose.Cells を追加する
Aspose.Cells を使い始めるには、ライブラリを追加する必要があります。これを行うには、次の手順を実行します。
1. ソリューション エクスプローラーでプロジェクトを右クリックします。
2. 「NuGet パッケージの管理」をクリックします。
3. 「Aspose.Cells」を検索し、「インストール」をクリックします。
### 必要な名前空間をインポートする
C# ファイルの先頭で、Aspose.Cells をインポートする必要があります。これには、次の using ディレクティブの追加が含まれます。
```csharp
using System.IO;
using Aspose.Cells;
```
Excel ファイルを XPS 形式に変換するプロセスを、シンプルで管理しやすい手順に分解してみましょう。 
## ステップ1: ドキュメントディレクトリを定義する
ここで、Excel ファイルが保存されているパスを指定します。コードがファイルの場所を知る必要があるため、これは非常に重要です。
```csharp
string dataDir = "Your Document Directory"; //実際のパスに置き換えてください
```
## ステップ2: Excelファイルを開く
次に、Excel ファイルを Aspose Workbook オブジェクトに読み込みます。このアクションにより、プログラムは Excel ファイル内のデータにアクセスできるようになります。
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
ここでは、`Workbook`クラスを作成し、そこに「Book1.xls」を読み込みます。
## ステップ3: 最初のワークシートにアクセスする
次に、作業するワークシートを取得する必要があります。最初のワークシートを使用しているため、コードは次のようになります。
```csharp
Worksheet sheet = workbook.Worksheets[0]; //最初のワークシートにアクセスする
```
このコード行を使用すると、最初のワークシートにアクセスしてさらにコマンドを実行できます。
## ステップ4: 画像と印刷オプションを設定する
次に、出力をどのようにレンダリングするかを定義する必要があります。これには、インスタンスの作成が含まれます。`ImageOrPrintOptions`希望する出力形式を設定します。
```csharp
Aspose.Cells.Rendering.ImageOrPrintOptions options = new Aspose.Cells.Rendering.ImageOrPrintOptions();
options.SaveFormat = SaveFormat.Xps; //出力形式をXPSに設定する
```
このステップでは、Excel コンテンツを XPS 形式に変換することを Aspose に伝えます。
## ステップ5: シートをレンダリングする
オプションを設定したら、特定のシートをレンダリングします。
```csharp
Aspose.Cells.Rendering.SheetRender sr = new Aspose.Cells.Rendering.SheetRender(sheet, options);
sr.ToImage(0, dataDir + "out_printingxps.out.xps");
```
ここでは、`SheetRender`オブジェクトはレンダリング処理を担当します。メソッド`ToImage`実際の変換を処理し、レンダリングされた出力を「out_printingxps.out.xps」として保存します。
## ステップ 6: ワークブック全体を XPS にエクスポートする
つのシートだけではなくワークブック全体を変換する場合は、次の追加手順に従います。
```csharp
WorkbookRender wr = new WorkbookRender(workbook, options);
wr.ToImage(dataDir + "out_whole_printingxps.out.xps");
```
このコード スニペットを使用すると、ワークブック全体を一度にエクスポートできるため、複数のワークシートを変換する必要がある場合に効率的です。
## 結論
おめでとうございます。.NET の Aspose.Cells ライブラリを使用して、Excel ファイルを XPS 形式に正常に変換できました。手順が多いように思えるかもしれませんが、各手順はプロセスで重要な役割を果たします。この知識があれば、アプリケーションで Excel ファイルを処理し、さまざまな形式に最適化する準備が整います。次に誰かが厄介なスプレッドシートの変換方法を尋ねてきたら、何をすべきか正確にわかるでしょう。
## よくある質問
### XPS 形式とは何ですか?
XPS (XML Paper Specific) は、ドキュメントのレイアウトと外観を保持する固定ドキュメント形式です。
### 使用するには Aspose.Cells を購入する必要がありますか?
 Aspose.Cellsの無料トライアルをお試しください[ここ](https://releases.aspose.com/)その後、完全な機能を使用するにはライセンスを購入する必要がある場合があります。
### 複数の Excel ファイルを一度に変換できますか?
はい、ディレクトリ内の複数のファイルをループし、各ファイルに同じ変換ロジックを適用するようにコードを適応させることができます。
### 特定のシートだけを変換する必要がある場合はどうすればよいですか?
必要なシートのインデックスを`SheetRender`手順に示されているオブジェクト。
### Aspose.Cells の詳細情報はどこで入手できますか?
探索することができます[ドキュメント](https://reference.aspose.com/cells/net/)ライブラリで利用できるより高度な機能とオプションについては、こちらをご覧ください。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
