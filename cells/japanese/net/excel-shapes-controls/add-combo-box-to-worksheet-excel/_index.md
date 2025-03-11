---
title: Excel のワークシートにコンボ ボックスを追加する
linktitle: Excel のワークシートにコンボ ボックスを追加する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して、プログラムによって Excel ワークシートにコンボ ボックスを追加する方法を学習します。このステップ バイ ステップ ガイドでは、詳細を順を追って説明します。
weight: 21
url: /ja/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel のワークシートにコンボ ボックスを追加する

## 導入
インタラクティブな Excel スプレッドシートを作成すると、特にコンボ ボックスなどのフォーム要素を追加すると、ユーザー エクスペリエンスが大幅に向上します。コンボ ボックスを使用すると、ユーザーは定義済みのリストからオプションを選択できるため、データ入力が簡単かつ効率的になります。Aspose.Cells for .NET を使用すると、Excel を直接使用せずに、Excel シートにプログラムでコンボ ボックスを作成できます。この強力なライブラリにより、開発者はフォーム コントロールを自動化する機能など、さまざまな方法で Excel ファイルを操作できます。
このチュートリアルでは、Aspose.Cells for .NET を使用して Excel のワークシートにコンボ ボックスを追加する手順を説明します。動的でユーザー フレンドリなスプレッドシートを作成したい場合は、このガイドが役立ちます。
## 前提条件
コードに進む前に、必要なものがすべて揃っていることを確認しましょう。
- Aspose.Cells for .NET: Aspose.Cells for .NETライブラリを以下のサイトからダウンロードしてインストールします。[ダウンロードページ](https://releases.aspose.com/cells/net/).
- .NET Framework: マシンに .NET Framework がインストールされていることを確認してください。Aspose.Cells でサポートされているバージョンであればどれでも動作します。
- 開発環境: Visual Studio などの IDE を使用してプロジェクトを管理し、コードを記述します。
-  Asposeライセンス: 評価モードではライセンスなしでも使用できますが、フルバージョンの場合はライセンスを適用する必要があります。[一時ライセンス](https://purchase.aspose.com/temporary-license/)必要であれば。
## パッケージのインポート
開始するには、必要な名前空間をプロジェクトにインポートする必要があります。必要なものは次のとおりです。
```csharp
using System.IO;
using Aspose.Cells;
```
これらは、Excel ファイルを操作したり、ワークブック内のコンボ ボックスなどのフォーム要素を操作するために不可欠です。
簡単に理解できるように、コンボ ボックスを追加するプロセスを複数の簡単な手順に分解してみましょう。
## ステップ1: ドキュメントディレクトリを設定する
最初のステップは、Excel ファイルを保存するディレクトリを作成することです。まだ存在しない場合は、新しいフォルダーを作成できます。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
//ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: 出力ファイルが保存される場所を指定します。
- System.IO.Directory.Exists: ディレクトリが既に存在するかどうかを確認します。
- System.IO.Directory.CreateDirectory: ディレクトリが存在しない場合は作成します。
## ステップ2: 新しいワークブックを作成する
次に、コンボ ボックスを追加する新しい Excel ブックを作成します。

```csharp
//新しいワークブックを作成します。
Workbook workbook = new Workbook();
```

- Workbook ワークブック: Excel ファイルを表す Workbook クラスの新しいインスタンスを初期化します。
## ステップ3: ワークシートとセルを取得する
次に、ワークブックから最初のワークシートにアクセスし、データを入力するセル コレクションを取得します。

```csharp
//最初のワークシートを入手します。
Worksheet sheet = workbook.Worksheets[0];
//ワークシートのセルのコレクションを取得します。
Cells cells = sheet.Cells;
```

- ワークシート シート: ワークブックから最初のワークシートを取得します。
- セル セル: ワークシートからセルのコレクションを取得します。
## ステップ4: コンボボックスに値を入力する
ここで、セルにいくつかの値を入力する必要があります。これらの値はコンボ ボックスのオプションとして機能します。

```csharp
//値を入力してください。
cells["B3"].PutValue("Employee:");
//太字に設定します。
cells["B3"].GetStyle().Font.IsBold = true;
//コンボ ボックスの入力範囲を示す値を入力します。
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- 細胞["B3"].PutValue: セル B3 にラベル "Employee" を配置します。
- Font.IsBold = true: テキストを太字にして目立たせます。
- 入力範囲: セル A2 から A7 に複数の従業員 ID を入力します。これらはコンボ ボックスのドロップダウンに表示されます。
## ステップ5: ワークシートにコンボボックスを追加する
次の手順では、ワークシートにコンボ ボックス コントロールを追加します。このコンボ ボックスを使用すると、ユーザーは先ほど入力した従業員 ID の 1 つを選択できます。

```csharp
//新しいコンボ ボックスを追加します。
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: ワークシートに新しいコンボ ボックスを追加します。数字 (2、0、2、0、22、100) は、コンボ ボックスの位置と寸法を表します。
## ステップ6: コンボボックスをセルにリンクし、入力範囲を設定する
コンボ ボックスを機能させるには、特定のセルにリンクし、オプションを取得するセルの範囲を定義する必要があります。

```csharp
//リンクセルを設定します。
comboBox.LinkedCell = "A1";
//入力範囲を設定します。
comboBox.InputRange = "A2:A7";
```

- LinkedCell: コンボ ボックスの選択をセル A1 にリンクします。コンボ ボックスから選択された値がこのセルに表示されます。
- InputRange: コンボ ボックスのオプションに入力される値を含むセル範囲 (A2:A7) を定義します。
## ステップ7: コンボボックスの外観をカスタマイズする
ドロップダウン行の数を指定し、3D シェーディングを有効にして見た目を良くすることで、コンボ ボックスをさらにカスタマイズできます。

```csharp
//コンボボックスのリスト部分に表示されるリスト行の数を設定します。
comboBox.DropDownLines = 5;
//コンボ ボックスを 3D シェーディングで設定します。
comboBox.Shadow = true;
```

- DropDownLines: コンボ ボックスのドロップダウンに一度に表示されるオプションの数を制御します。
- シャドウ: コンボ ボックスに 3D シェーディング効果を追加します。
## ステップ 8: 列を自動調整してワークブックを保存する
最後に、列を自動調整してレイアウトをきれいにし、ワークブックを保存します。

```csharp
//列の自動調整
sheet.AutoFitColumns();
//ファイルを保存します。
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: コンテンツに合わせて列の幅を自動的に調整します。
- 保存: ワークブックを指定されたディレクトリに Excel ファイルとして保存します。

## 結論
Aspose.Cells for .NET を使用して Excel ワークシートにコンボ ボックスを追加するのは簡単なプロセスであり、データ入力の柔軟性が大幅に向上します。プログラムでフォーム コントロールを作成することにより、対話型のスプレッドシートを簡単に作成できます。このチュートリアルでは、Aspose.Cells を使用してコンボ ボックスを追加し、セルにリンクし、入力範囲を構成する方法を説明しました。
 Aspose.CellsはExcelファイル操作のための幅広い機能を提供しており、スプレッドシートのタスクを自動化したい開発者にとって理想的な選択肢です。[無料トライアル](https://releases.aspose.com/).
## よくある質問
### Excel をインストールせずに Aspose.Cells を使用できますか?
はい、Aspose.Cells は Excel とは独立して動作し、Excel をインストールする必要はありません。
### Aspose.Cells でライセンスを適用するにはどうすればよいですか?
ライセンスは以下から取得して申請できます。[ここ](https://purchase.aspose.com/buy)そして呼びかける`License.SetLicense()`コード内で。
### Aspose.Cells はどのような形式のファイルを保存できますか?
Aspose.Cells は、XLSX、XLS、CSV、PDF などの複数の形式でのファイルの保存をサポートしています。
### 追加できるコンボ ボックスの数に制限はありますか?
いいえ、厳密な制限はありません。プロジェクトの必要に応じて、コンボ ボックスをいくつでも追加できます。
### Aspose.Cells のサポートを受けるにはどうすればよいですか?
サポートを受けるには[Aspose フォーラム](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
