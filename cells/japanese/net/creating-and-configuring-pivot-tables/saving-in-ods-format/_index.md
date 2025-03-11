---
title: .NET でプログラム的にピボット テーブルを ODS 形式で保存する
linktitle: .NET でプログラム的にピボット テーブルを ODS 形式で保存する
second_title: Aspose.Cells .NET Excel 処理 API
description: このステップバイステップ ガイドでは、Aspose.Cells for .NET を使用してピボット テーブルを ODS 形式で保存する方法を説明します。
weight: 25
url: /ja/net/creating-and-configuring-pivot-tables/saving-in-ods-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET でプログラム的にピボット テーブルを ODS 形式で保存する

## 導入
スプレッドシートでのデータ管理に関して言えば、ピボット テーブルの力に匹敵するものはありません。ピボット テーブルは、複雑なデータセットを要約、分析、および表示するための頼りになるツールです。今日は、Aspose.Cells for .NET を使用してピボット テーブルを ODS 形式で保存する方法について詳しく説明します。経験豊富な開発者でも、.NET を使い始めたばかりの開発者でも、このガイドはわかりやすいでしょう。 
さあ始めましょう！
## 前提条件
コードに進む前に、必要な基本事項がいくつかあります。
### 1. .NETの基礎知識
.NET とそのプログラミング概念について基本的な知識があれば、簡単に理解できるようになります。
### 2. .NET 用 Aspose.Cells
 Aspose.Cells for .NETがインストールされている必要があります。ダウンロードは以下から行えます。[Aspose リリース ページ](https://releases.aspose.com/cells/net/)試用版もございます[ここ](https://releases.aspose.com/).
### 3. 開発環境
.NET コードを記述してテストできる Visual Studio などの IDE があることを確認してください。
### 4. 少しの忍耐
あらゆるコーディング作業と同様に、忍耐が鍵となります。最初は完璧に動作しなくても心配しないでください。デバッグはプロセスの一部です。
## パッケージのインポート
Aspose.Cells を使用するには、必要な名前空間をインポートする必要があります。コード ファイルの先頭に次の using ディレクティブを追加します。
```csharp
using System;
using Aspose.Cells.Pivot;
```
この行を使用すると、Aspose.Cells ライブラリ内のすべての機能にアクセスできるため、コーディング プロセスが簡単になります。
それでは、プロセスを管理しやすいステップに分解してみましょう。
## ステップ1: 出力ディレクトリを設定する
まず、ODS ファイルを保存する場所を定義する必要があります。これは、ディレクトリ パスの単純な割り当てです。
```csharp
string outputDir = "Your Document Directory";
```
この行では、`"Your Document Directory"`ファイルを保存するパスを入力します。
## ステップ2: 新しいワークブックを作成する
次に、ピボット テーブルを含むすべてのデータと構造を保持する新しい Workbook オブジェクトをインスタンス化します。
```csharp
Workbook workbook = new Workbook();
```
ここでは、基本的に一から始めます。傑作を作成するための空白のキャンバスと考えてください。
## ステップ3: ワークシートにアクセスする
ワークブックができたので、次はワークシートで作業を開始する必要があります。Aspose.Cells を使用すると、利用可能な最初のワークシートに簡単にアクセスできます。
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
この行により、データ入力の準備ができた最初のシートに移動します。
## ステップ4: セルにデータを入力する
ワークシートにデータを入力します。スポーツ販売データの簡単な例を使用します。 
さまざまなセルに値を設定する方法は次のとおりです。
```csharp
Cells cells = sheet.Cells;
cells["A1"].PutValue("Sport");
cells["B1"].PutValue("Quarter");
cells["C1"].PutValue("Sales");
cells["A2"].PutValue("Golf");
cells["A3"].PutValue("Golf");
cells["A4"].PutValue("Tennis");
cells["A5"].PutValue("Tennis");
cells["A6"].PutValue("Tennis");
cells["A7"].PutValue("Tennis");
cells["A8"].PutValue("Golf");
cells["B2"].PutValue("Qtr3");
cells["B3"].PutValue("Qtr4");
cells["B4"].PutValue("Qtr3");
cells["B5"].PutValue("Qtr4");
cells["B6"].PutValue("Qtr3");
cells["B7"].PutValue("Qtr4");
cells["B8"].PutValue("Qtr3");
cells["C2"].PutValue(1500);
cells["C3"].PutValue(2000);
cells["C4"].PutValue(600);
cells["C5"].PutValue(1500);
cells["C6"].PutValue(4070);
cells["C7"].PutValue(5000);
cells["C8"].PutValue(6430);
```
これらの行では、見出しを定義し、売上データを入力します。このステップは、食事を作る前に食料庫に食材を補充するようなものだと考えてください。材料 (データ) が良ければ、食事 (分析) も良くなります。
## ステップ5: ピボットテーブルを作成する
次は楽しい部分、ピボット テーブルの作成です。ワークシートにピボット テーブルを追加する方法は次のとおりです。
```csharp
PivotTableCollection pivotTables = sheet.PivotTables;
//ワークシートにピボットテーブルを追加する
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```
このスニペットでは、ピボットテーブルのデータ範囲とワークシート上の配置場所を指定しています。データ範囲`=A1:C8`データが存在する領域をカバーします。
## ステップ6: ピボットテーブルをカスタマイズする
次に、ニーズに合わせてピボット テーブルをカスタマイズします。これには、表示される内容、分類方法、データの計算方法の制御が含まれます。
```csharp
PivotTable pivotTable = pivotTables[index];
//行の合計を非表示にします。
pivotTable.RowGrand = false;
//最初のフィールドを行領域にドラッグします。
pivotTable.AddFieldToArea(PivotFieldType.Row, 0);
// 2 番目のフィールドを列領域にドラッグします。
pivotTable.AddFieldToArea(PivotFieldType.Column, 1);
// 3 番目のフィールドをデータ領域にドラッグします。
pivotTable.AddFieldToArea(PivotFieldType.Data, 2);
pivotTable.CalculateData();
```
ここでは、どのデータ フィールドを要約し、どのように表現するかを決定します。これは、ディナー パーティーのテーブルをセッティングするようなものです。最適なものとその提示方法を決定します。
## ステップ7: ワークブックを保存する
最後に、作業を希望の ODS 形式で保存する準備が整いました。手順は次のとおりです。
```csharp
workbook.Save(outputDir + "PivotTableSaveInODS_out.ods");
```
この手順で、プロジェクトが完了し、選択したディレクトリに保存されます。満足のいく仕上がりです。
## ステップ8: 出力を確認する
最後に、プロセスが正常に完了したかどうかを常に確認することをお勧めします。簡単なコンソール メッセージを追加できます。
```csharp
Console.WriteLine("PivotTableSaveInODS executed successfully.");
```
このメッセージは、すべてが問題なく完了したことを確認するためにコンソールに表示されます。シェフが料理を出す前にすべてが完璧に調理されているかどうかを確認するのと同じです。
## 結論 
これで完了です。Aspose.Cells を使用してピボット テーブルを作成しただけでなく、ODS 形式で保存しました。このガイドでは、すべての手順を説明し、将来同様のタスクに取り組むための知識と自信を身に付けられるようにしました。
## よくある質問
### Aspose.Cells とは何ですか?
Aspose.Cells は、.NET アプリケーションで Excel ファイルを作成および操作できる高度なライブラリです。
### Aspose.Cells を無料で使用できますか?
はい、無料試用版をこちらからダウンロードできます。[Aspose ウェブサイト](https://releases.aspose.com/).
### Aspose.Cells はどのような形式をサポートしていますか?
XLSX、XLS、ODS、PDF など、多数の形式をサポートしています。
### Aspose.Cells のサポートを受けるにはどうすればよいですか?
ヘルプは[Aspose サポート フォーラム](https://forum.aspose.com/c/cells/9).
### 一時ライセンスはありますか?
はい、Asposeサイトから一時ライセンスを申請できます。[ここ](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
