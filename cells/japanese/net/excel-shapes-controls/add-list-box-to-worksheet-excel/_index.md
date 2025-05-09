---
"description": "Aspose.Cells for .NET を使用して、Excel ワークシートにリストボックスを追加する方法を学びましょう。簡単なステップバイステップガイドに従って、Excel シートをインタラクティブなものにしましょう。"
"linktitle": "Excelのワークシートにリストボックスを追加する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "Excelのワークシートにリストボックスを追加する"
"url": "/ja/net/excel-shapes-controls/add-list-box-to-worksheet-excel/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excelのワークシートにリストボックスを追加する

## 導入
リストボックスなどのインタラクティブな要素をExcelワークシートに追加すると、データ管理とプレゼンテーションが大幅に向上します。インタラクティブなフォームを作成する場合でも、カスタムデータ入力ツールを作成する場合でも、リストボックスでユーザー入力を制御できることは非常に重要です。Aspose.Cells for .NETは、Excelファイルにこれらのコントロールを効率的に追加および管理する方法を提供します。このガイドでは、Aspose.Cells for .NETを使用してワークシートにリストボックスを追加する手順を詳しく説明します。
## 前提条件
コーディングを始める前に、次のツールとリソースが揃っていることを確認してください。
- Aspose.Cells for .NET ライブラリ: ダウンロードはこちらから [Aspose.Cells for .NET のダウンロード ページ](https://releases。aspose.com/cells/net/).
- 開発環境: Visual Studio など、.NET 開発をサポートする任意の IDE。
- .NET Framework: プロジェクトがサポートされているバージョンの .NET Framework をターゲットにしていることを確認します。
また、 [一時ライセンス](https://purchase.aspose.com/temporary-license/) すべての機能を制限なく試してみたい場合。
## パッケージのインポート
始める前に、必要なAspose.Cells名前空間がインポートされていることを確認してください。手順は以下のとおりです。
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
このチュートリアルでは、リストボックスを追加するプロセスを複数の簡単なステップに分解して説明します。各ステップを注意深く実行し、すべてが期待どおりに動作することを確認してください。
## ステップ1: ドキュメントディレクトリの設定
Excelファイルを作成する前に、保存場所を指定する必要があります。ディレクトリの設定方法は次のとおりです。
```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
// ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
このステップでは、ファイルの保存場所を定義します。コードはディレクトリが存在するかどうかを確認し、存在しない場合はディレクトリを作成します。これにより、後で「ファイルが見つかりません」というエラーが発生するのを防ぎます。
## ステップ2: 新しいワークブックを作成し、最初のワークシートにアクセスする
次に、新しいブックを作成し、リスト ボックスを追加する最初のワークシートにアクセスします。
```csharp
// 新しいワークブックを作成します。
Workbook workbook = new Workbook();
// 最初のワークシートを取得します。
Worksheet sheet = workbook.Worksheets[0];
```
ワークブックとは、基本的にはExcelファイルのことです。ここでは、新しいワークブックを作成し、最初のワークシートにアクセスします。ここにリストボックスを配置します。これは、コントロールを描画するための空白のキャンバスを作成するようなものです。
## ステップ3: リストボックスにデータを入力する
リスト ボックスを追加する前に、リスト ボックスが参照するデータを入力する必要があります。
```csharp
// ワークシート セルのコレクションを取得します。
Cells cells = sheet.Cells;
// ラベルの値を入力します。
cells["B3"].PutValue("Choose Dept:");
// ラベルを太字に設定します。
cells["B3"].GetStyle().Font.IsBold = true;
// リスト ボックスに値を入力します。
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
ここでは、ワークシートにテキストを追加しています。「部門を選択:」というラベルをセルB3に配置し、フォントを太字に設定しています。列Aには、リストボックスの入力範囲となる値を挿入しています。これは、各部門を表すものです。この入力範囲は、ユーザーがリストボックスを操作する際に選択するものです。
## ステップ4: リストボックスをワークシートに追加する
データの設定が完了したので、リスト ボックス コントロール自体を追加しましょう。
```csharp
// 新しいリスト ボックスを追加します。
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
このコードは、ワークシートにリストボックスを追加します。パラメータはリストボックスの位置とサイズを定義します。リストボックスは行2、列0に配置され、幅は122、高さは100です。これらの座標とサイズによって、ワークシート内のリストボックスの表示位置が決まります。
## ステップ5: リストボックスのプロパティを設定する
次に、リスト ボックスが完全に機能するようにさまざまなプロパティを設定します。
```csharp
// 配置タイプを設定します。
listBox.Placement = PlacementType.FreeFloating;
// リンクセルを設定します。
listBox.LinkedCell = "A1";
// 入力範囲を設定します。
listBox.InputRange = "A2:A7";
// 選択タイプを設定します。
listBox.SelectionType = SelectionType.Single;
// リスト ボックスを 3D シェーディングで設定します。
listBox.Shadow = true;
```
- PlacementType.FreeFloating: このプロパティは、ワークシートがどのように変更されたかに関係なく、リスト ボックスがその位置に留まるようにします。
- LinkedCell: リスト ボックスから選択した値が表示されるセル (この場合は A1) を設定します。
- InputRange: これは、リスト ボックスにオプションのリストを検索する場所 (前に設定した A2 から A7) を指示します。
- SelectionType.Single: ユーザーはリスト ボックスから 1 つの項目のみ選択できるように制限されます。
- 影: 影の効果により、リスト ボックスの外観がより立体的になり、視覚的に魅力的になります。
## ステップ6: Excelファイルを保存する
最後に、リスト ボックスが含まれたワークブックを保存しましょう。
```csharp
// ワークブックを保存します。
workbook.Save(dataDir + "book1.out.xls");
```
このコード行は、先ほど設定したディレクトリにワークブックを保存します。ファイル名は「book1.out.xls」ですが、プロジェクトに合った任意の名前にすることができます。
## 結論
これで完了です！Aspose.Cells for .NET を使って、Excel ワークシートにリストボックスを追加できました。わずか数行のコードで、完全に機能するリストボックスを作成でき、ワークシートをよりインタラクティブでダイナミックなものにすることができます。このチュートリアルでは、Aspose.Cells for .NET の他のコントロールや機能を試すための確かな基礎を身に付けることができます。ぜひいろいろ試してみてください。そうすれば、すぐにライブラリの豊富な機能をマスターできるでしょう。
## よくある質問
### リスト ボックスで複数選択を許可できますか?  
はい、変更できます `SelectionType` に `SelectionType.Multi` 複数選択を可能にします。
### リスト ボックスの外観を変更できますか?  
もちろんです！Aspose.Cells を使用すると、リスト ボックスのサイズ、フォント、色など、リスト ボックスの外観をカスタマイズできます。
### 後でリスト ボックスを削除する必要がある場合はどうすればよいですか?  
リストボックスにアクセスして削除するには、 `Shapes` コレクションを使用して `sheet。Shapes.RemoveAt(index)`.
### リスト ボックスを別のセルにリンクできますか?  
はい、変更するだけです `LinkedCell` 選択した値を表示する他のセルにプロパティを適用します。
### リスト ボックスに項目を追加するにはどうすればよいですか?  
指定したセルにさらに値を挿入して入力範囲を更新するだけで、リスト ボックスが自動的に更新されます。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}