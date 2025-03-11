---
title: Excel ワークシートの行を保護する
linktitle: Excel ワークシートの行を保護する
second_title: Aspose.Cells for .NET API リファレンス
description: このチュートリアルでは、Aspose.Cells for .NET を使用して Excel スプレッドシートの行を保護する方法を説明します。C# でのステップ バイ ステップ チュートリアルです。
weight: 60
url: /ja/net/protect-excel-file/protect-row-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel ワークシートの行を保護する

## 導入

Excel シートで作業する場合、データの整合性を維持するために特定の行を保護する必要があることがよくあります。チーム プロジェクトの管理、財務レポートの監視、ドキュメントの共有など、特定の行へのアクセスを制限することで、不要な変更を防ぐことができます。このチュートリアルでは、Aspose.Cells for .NET を利用して Excel ワークシートの特定の行を保護する方法について説明します。では、コーディングの知識を身につけて、C# による Excel 操作のエキサイティングな世界に飛び込みましょう。

## 前提条件

実際に作業を始める前に、すべてがセットアップされていることを確認しましょう。前提条件は次のとおりです。

1.  Aspose.Cells for .NET: ライブラリを以下からダウンロードしてください。[Aspose ウェブサイト](https://releases.aspose.com/cells/net/)すべての新機能とバグ修正のために最新バージョンを使用していることを確認してください。
2. Visual Studio: Visual Studio (Community、Professional、または Enterprise) などの統合開発環境 (IDE) を使用すると、C# コードを効率的にコンパイルして実行できます。
3. .NET Framework: 互換性のあるバージョンの .NET Framework が必要です。Aspose.Cells は複数のバージョンをサポートしているため、最新バージョンであることを確認してください。 
4. C# の基礎知識: このガイド全体でコードを記述する際には、C# の基礎的な理解が役立ちます。
5. リファレンスドキュメント:[Aspose.Cells for .NET ドキュメント](https://reference.aspose.com/cells/net/)使用されるメソッドとクラスの詳細については、こちらをご覧ください。

## パッケージのインポート

最初のステップは、C# プロジェクトに必要なパッケージをインポートすることです。Aspose.Cells は、含める必要のある一連のクラスを通じて動作します。

```csharp
using System.IO;
using Aspose.Cells;
```

必要なパッケージをインポートしたので、Excel ブックを作成し、特定の行を保護する手順を見ていきましょう。 

## ステップ1: ディレクトリを定義する

この手順では、Excel ファイルを保存する場所を指定します。このディレクトリが存在することを確認することが重要です。存在しない場合は、必要に応じてプログラムで作成します。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; //ドキュメントパスに置き換えます
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
{
    Directory.CreateDirectory(dataDir);
}
```
このコードでは、`YOUR DOCUMENT DIRECTORY`Excel ファイルを保存する実際のパスを入力します。

## ステップ2: 新しいワークブックを作成する

次に、すべての操作が行われる新しいワークブックを作成します。これは、夢の家を建てる前に基礎を築くのと同じように、基本的なステップです。

```csharp
Workbook wb = new Workbook();
```
この行は、`Workbook`クラスで取り組むための新しいワークシートを作成しました。

## ステップ3: ワークシートにアクセスする

ワークブックが作成されたので、最初のワークシートを作成しましょう。Excel ファイルには複数のシートが含まれることがあるため、適切なシートを選択することが重要です。

```csharp
Worksheet sheet = wb.Worksheets[0]; //最初のシートにアクセスする
```

## ステップ4: すべての列のロックを解除する

特定の行をロックする前に、最初にすべての列のロックを解除することをお勧めします。これにより、後で編集可能なデータを残すかどうかを制御できます。

```csharp
Style style;
StyleFlag flag;

//すべての列をループしてロックを解除します
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
このループは最初の 256 列を反復処理し、各列のロックを解除してデフォルトの編集権限を確保します。

## ステップ5: 特定の行をロックする

ここで、ワークシートの最初の行をロックの対象にします。この手順により、ユーザーがこの行に含まれる重要なデータに不正な変更を加えることができなくなります。

```csharp
style = sheet.Cells.Rows[0].Style; //最初の行のスタイルを取得する
style.IsLocked = true; //行をロックする
flag = new StyleFlag();
flag.Locked = true; //ロックフラグを設定する
sheet.Cells.ApplyRowStyle(0, style, flag); //最初の行にスタイルを適用する
```
ここでは、最初の行のスタイルを取得し、それをロック済みとしてマークし、ロック スタイルを適用します。これは、重要な引き出しに鍵をかけるのと似ており、機密情報を保護するために不可欠です。

## ステップ6: シートを保護する

行をロックしたら、もう一歩踏み込んでワークシートを完全に保護しましょう。これにより、`ProtectionType`.

```csharp
sheet.Protect(ProtectionType.All); //すべての機能でシートを保護する
```
この保護を適用すると、ユーザーはロックされた行を編集したり、ロックされた領域に影響を与える可能性のある変更を加えたりできなくなります。

## ステップ7: ワークブックを保存する

最後のステップは、ワークブックを保存することです。ここで、これまでの努力が報われ、美しく保護されたスプレッドシートが完成します。

```csharp
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
保存したファイル名と形式が要件に合っていることを確認してください。この場合は、古い Excel 形式 (Excel 97-2003) で保存します。

## 結論

これで完了です。Aspose.Cells for .NET を使用して Excel ワークシートの特定の行を保護する方法を学習しました。わずか数行のコードで、ワークブックを作成しただけでなく、機密情報を保護して、Excel ファイルがそのままの状態で信頼できる状態を保つことができました。財務レポート、出勤簿、共同プロジェクト計画など、重要なデータを保護することは不可欠です。 

## よくある質問

### Aspose.Cells とは何ですか?
Aspose.Cells は、ユーザーがプログラムによって Excel ファイルを作成、操作、変換できるようにする強力な .NET ライブラリです。

### Aspose.Cells を使用して複数の行を一度に保護できますか?
はい、複数の行を反復処理し、それぞれに同様のスタイルの変更を適用することで、ロック手法を拡張できます。

### 保護後に行のロックを解除する方法はありますか?
はい、まずシートの保護を解除してから調整することができます。`IsLocked`目的の行のプロパティを変更し、その後保護を再適用します。

### Aspose.Cells は Excel 以外の形式もサポートしていますか?
もちろんです! Aspose.Cells は、ワークブックを CSV、PDF、HTML などのさまざまな形式に変換して保存できます。

### Aspose.Cells のサポートはどこで受けられますか?
訪問することができます[Aspose サポート フォーラム](https://forum.aspose.com/c/cells/9)支援とコミュニティのガイダンスのため。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
