---
title: Excel のワークシートにリスト ボックスを追加する
linktitle: Excel のワークシートにリスト ボックスを追加する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、Excel ワークシートにリスト ボックスを追加する方法を学びます。簡単なステップ バイ ステップ ガイドに従って、Excel シートをインタラクティブにしましょう。
weight: 20
url: /ja/net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel のワークシートにリスト ボックスを追加する

## 導入
リスト ボックスなどのインタラクティブな要素を Excel ワークシートに追加すると、データ管理とプレゼンテーションが大幅に改善されます。インタラクティブなフォームを作成する場合でも、カスタム データ入力ツールを作成する場合でも、リスト ボックスを使用してユーザー入力を制御する機能は非常に重要です。Aspose.Cells for .NET は、Excel ファイルにこれらのコントロールを追加および管理するための効率的な方法を提供します。このガイドでは、Aspose.Cells for .NET を使用してワークシートにリスト ボックスを追加する手順について説明します。
## 前提条件
コーディングに取り掛かる前に、次のツールとリソースが揃っていることを確認してください。
-  Aspose.Cells for .NETライブラリ:以下からダウンロードできます。[Aspose.Cells for .NET のダウンロード ページ](https://releases.aspose.com/cells/net/).
- 開発環境: Visual Studio など、.NET 開発をサポートする任意の IDE。
- .NET Framework: プロジェクトがサポートされているバージョンの .NET Framework をターゲットにしていることを確認します。
また、[一時ライセンス](https://purchase.aspose.com/temporary-license/)制限なくすべての機能を探索したい場合。
## パッケージのインポート
始める前に、必要な Aspose.Cells 名前空間がインポートされていることを確認してください。手順は次のとおりです。
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
このチュートリアルでは、リスト ボックスを追加するプロセスを複数の簡単な手順に分解します。各手順を厳密に実行して、すべてが期待どおりに動作することを確認してください。
## ステップ1: ドキュメントディレクトリの設定
Excel ファイルを作成する前に、ファイルを保存する場所が必要です。ディレクトリを設定する方法は次のとおりです。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
//ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
このステップでは、ファイルを保存する場所を定義します。コードはディレクトリが存在するかどうかを確認し、存在しない場合はディレクトリを作成します。これにより、後で「ファイルが見つかりません」というエラーが発生しなくなります。
## ステップ 2: 新しいワークブックを作成し、最初のワークシートにアクセスする
次に、新しいワークブックを作成し、リスト ボックスを追加する最初のワークシートにアクセスします。
```csharp
//新しいワークブックを作成します。
Workbook workbook = new Workbook();
//最初のワークシートを入手します。
Worksheet sheet = workbook.Worksheets[0];
```
ワークブックは、基本的には Excel ファイルです。ここでは、新しいワークブックを作成し、リスト ボックスを配置する最初のワークシートにアクセスします。これは、コントロールを描画する空白のキャンバスを作成するものと考えてください。
## ステップ3: リストボックスにデータを入力する
リスト ボックスを追加する前に、リスト ボックスが参照するデータを入力する必要があります。
```csharp
//ワークシートのセルのコレクションを取得します。
Cells cells = sheet.Cells;
//ラベルの値を入力します。
cells["B3"].PutValue("Choose Dept:");
//ラベルを太字に設定します。
cells["B3"].GetStyle().Font.IsBold = true;
//リスト ボックスに値を入力します。
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
ここでは、ワークシートにテキストを追加しています。ラベル「部門を選択:」はセル B3 に配置され、フォントは太字に設定されています。列 A には、リスト ボックスの入力範囲として機能する、さまざまな部門を表す値を挿入しています。この入力範囲は、ユーザーがリスト ボックスを操作するときに選択する範囲です。
## ステップ4: リストボックスをワークシートに追加する
データを設定したので、リスト ボックス コントロール自体を追加しましょう。
```csharp
//新しいリスト ボックスを追加します。
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
このコードは、リスト ボックスをワークシートに追加します。パラメータは、リスト ボックスの位置とサイズを定義します。リスト ボックスは、幅 122、高さ 100 で行 2、列 0 に配置されます。これらは、ワークシート内でリスト ボックスが表示される場所を決定する座標とサイズです。
## ステップ5: リストボックスのプロパティを設定する
次に、リスト ボックスが完全に機能するように、さまざまなプロパティを設定します。
```csharp
//配置タイプを設定します。
listBox.Placement = PlacementType.FreeFloating;
//リンクセルを設定します。
listBox.LinkedCell = "A1";
//入力範囲を設定します。
listBox.InputRange = "A2:A7";
//選択タイプを設定します。
listBox.SelectionType = SelectionType.Single;
//リスト ボックスを 3D シェーディングで設定します。
listBox.Shadow = true;
```
- PlacementType.FreeFloating: このプロパティは、ワークシートがどのように変更されたかに関係なく、リスト ボックスがその位置に留まるようにします。
- LinkedCell: リスト ボックスから選択した値が表示されるセル (この場合は A1) を設定します。
- InputRange: これは、リスト ボックスにオプションのリストを検索する場所 (前に設定した A2 から A7) を指示します。
- SelectionType.Single: これにより、ユーザーはリスト ボックスから 1 つの項目のみを選択できるようになります。
- 影: 影の効果により、リスト ボックスの外観がより立体的になり、視覚的に魅力的になります。
## ステップ6: Excelファイルを保存する
最後に、リスト ボックスが含まれたワークブックを保存しましょう。
```csharp
//ワークブックを保存します。
workbook.Save(dataDir + "book1.out.xls");
```
このコード行は、前に設定したディレクトリにワークブックを保存します。ファイル名は「book1.out.xls」ですが、プロジェクトに適した任意の名前を選択できます。
## 結論
これで完了です。Aspose.Cells for .NET を使用して、Excel ワークシートにリスト ボックスを正常に追加できました。わずか数行のコードで、完全に機能するリスト ボックスを作成し、ワークシートをよりインタラクティブでダイナミックなものにしました。このチュートリアルでは、Aspose.Cells for .NET の他のコントロールや機能を調べるための強固な基盤を提供します。実験を続ければ、すぐにライブラリの幅広い機能をマスターできます。
## よくある質問
### リスト ボックスで複数の選択を許可できますか?  
はい、変更できます`SelectionType`に`SelectionType.Multi`複数選択を可能にします。
### リスト ボックスの外観を変更できますか?  
もちろんです! Aspose.Cells を使用すると、リスト ボックスのサイズ、フォント、色など、リスト ボックスの外観をカスタマイズできます。
### 後でリスト ボックスを削除する必要がある場合はどうすればよいですか?  
リストボックスにアクセスして削除することができます。`Shapes`コレクションの使用`sheet.Shapes.RemoveAt(index)`.
### リスト ボックスを別のセルにリンクできますか?  
はい、変更するだけです`LinkedCell`選択した値を表示する他のセルにプロパティを適用します。
### リスト ボックスに項目を追加するにはどうすればよいですか?  
指定したセルにさらに値を挿入して入力範囲を更新するだけで、リスト ボックスが自動的に更新されます。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
