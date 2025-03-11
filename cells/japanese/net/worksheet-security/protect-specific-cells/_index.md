---
title: Aspose.Cells を使用してワークシート内の特定のセルを保護する
linktitle: Aspose.Cells を使用してワークシート内の特定のセルを保護する
second_title: Aspose.Cells .NET Excel 処理 API
description: Aspose.Cells for .NET を使用して Excel ワークシート内の特定のセルを保護する方法を学びます。わずか数ステップで機密データを保護し、誤った変更を防止します。
weight: 14
url: /ja/net/worksheet-security/protect-specific-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用してワークシート内の特定のセルを保護する

## 導入
このチュートリアルでは、Excel ワークシート内の特定のセルを保護する手順を説明します。最後には、プロのように自信を持ってセルをロックし、不正な変更を防ぎながら、必要に応じてワークシートの柔軟性を維持できるようになります。
## 前提条件
詳細に入る前に、このチュートリアルをスムーズに実行するために必要なものがすべて揃っていることを確認しましょう。
1. Visual Studio – まだインストールしていない場合は、Visual Studio をダウンロードしてインストールしてください。これは、.NET アプリケーションを実行する主な環境になります。
2.  Aspose.Cells for .NET – .NETアプリケーションでExcelファイルを操作するには、Aspose.Cellsライブラリが必要です。まだインストールしていない場合は、最新バージョンを以下から入手できます。[Aspose ウェブサイト](https://releases.aspose.com/cells/net/).
3. .NET Framework または .NET Core – このチュートリアルは、.NET Framework と .NET Core の両方で動作します。プロジェクトが Aspose.Cells と互換性があることを確認してください。
これらを準備したら、開始する準備は完了です。
## パッケージのインポート
ステップバイステップ ガイドに進む前に、Aspose.Cells を操作するために必要な名前空間をインポートしていることを確認する必要があります。プロジェクトで、ファイルの先頭に次のインポート ステートメントを含めます。
```csharp
using System.IO;
using Aspose.Cells;
```
これらの名前空間を使用すると、Excel ファイルや、ワークシート セルのスタイル設定と保護に必要なクラスを操作できるようになります。
ここで、Aspose.Cells for .NET を使用してワークシート内の特定のセルを保護するための簡単な手順を説明します。セル A1、B1、C1 を保護し、ワークシートの残りの部分は編集できるように開いたままにします。
## ステップ1: 新しいワークブックとワークシートを作成する
まず最初に、新しいワークブック (Excel ファイル) とその中にワークシートを作成する必要があります。ここでセル保護を適用します。
```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "Your Document Directory";
//ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
//新しいワークブックを作成します。
Workbook wb = new Workbook();
//ワークシート オブジェクトを作成し、最初のシートを取得します。
Worksheet sheet = wb.Worksheets[0];
```
このステップでは、まだ存在しない場合は、結果のExcelファイルを保存するディレクトリも作成します。`Workbook`クラスは新しいExcelファイルを初期化し、`Worksheets[0]`ワークブックの最初のシートを操作できるようになります。
## ステップ2: すべての列のロックを解除する
次に、ワークシート内のすべての列のロックを解除します。これにより、デフォルトでワークシート内のすべてのセルが編集可能になります。後で、保護するセルのみをロックします。
```csharp
//スタイル オブジェクトを定義します。
Style style;
//スタイルフラグオブジェクトを定義する
StyleFlag styleflag;
//ワークシート内のすべての列をループしてロックを解除します。
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    styleflag = new StyleFlag();
    styleflag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, styleflag);
}
```
このコードブロックでは、すべての列（最大255）を反復処理し、`IsLocked`財産に`false`これにより、基本的にこれらの列のすべてのセルがロック解除され、デフォルトで編集可能になります。次に、`ApplyStyle()`方法。
## ステップ 3: 特定のセルをロックする (A1、B1、C1)
すべての列のロックが解除されたので、特定のセル、つまりA1、B1、C1をロックすることに焦点を当てます。セルスタイルを変更し、`IsLocked`財産に`true`.
```csharp
// 3 つのセル (A1、B1、C1) をロックします。
style = sheet.Cells["A1"].GetStyle();
style.IsLocked = true;
sheet.Cells["A1"].SetStyle(style);
style = sheet.Cells["B1"].GetStyle();
style.IsLocked = true;
sheet.Cells["B1"].SetStyle(style);
style = sheet.Cells["C1"].GetStyle();
style.IsLocked = true;
sheet.Cells["C1"].SetStyle(style);
```
この手順により、セル A1、B1、C1 がロックされます。これらは保護されるセルであり、ワークシート保護が適用されると編集できなくなります。
## ステップ4: ワークシートを保護する
必要なセルをロックしたら、次のステップはワークシート全体を保護します。このステップにより、ロックされたセル (A1、B1、C1) は編集できなくなりますが、他のセルは編集可能なままになります。
```csharp
//最後に、シートを保護します。
sheet.Protect(ProtectionType.All);
```
の`Protect`メソッドがワークシート上で呼び出され、シートのすべての側面を保護するように指定します。これにより、マークされた特定のセルがロックされます。`IsLocked = true`ユーザーによる変更が不可能であることを保証します。
## ステップ5: ワークブックを保存する
セルがロックされ、シートが保護されたら、ワークブックを目的の場所に保存できます。
```csharp
// Excel ファイルを保存します。
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
この手順では、ワークブックを`dataDir`ファイル名のフォルダ`output.out.xls`ファイル名とディレクトリは必要に応じて変更できます。ファイルは Excel 97-2003 形式で保存されますが、必要に応じて調整できます。
## 結論
Aspose.Cells for .NET を使用して Excel ワークシート内の特定のセルを保護するのは簡単なプロセスです。上記の手順に従うことで、特定のセルをロックしながら、他のセルは編集可能なままにすることができます。この機能は、どのデータを変更可能にし、どのデータを保護したままにするか制御できるため、他のユーザーとワークブックを共有するときに非常に便利です。機密データを扱う場合でも、単に誤って変更されないようにする場合でも、Aspose.Cells は柔軟で強力なソリューションを提供します。
## よくある質問
### いくつかのセルではなく、特定の範囲のセルだけを保護するにはどうすればよいでしょうか?
個々のセルを手動でロックする代わりに、特定の範囲のセルまたは列をループしてロックするようにコードを変更することができます。
### ワークシートを保護するためにパスワードを追加できますか?
はい、電話をかける際にパスワードを指定できます。`Protect()`正しいパスワードなしでユーザーがシートの保護を解除できないように制限する方法。
### セルではなく特定の行や列を保護することはできますか?
はい、Aspose.Cellsでは、行または列全体をロックすることができます。`IsLocked`セルをロックしたのと同じように、行または列のプロパティを設定します。
### ワークシートの保護を解除するにはどうすればよいですか?
ワークシートの保護を解除するには、`Unprotect()`保護中にパスワードが設定されている場合は、オプションでパスワードを指定します。
### 数式やグラフの追加など、他の Excel 操作に Aspose.Cells を使用できますか?
もちろんです! Aspose.Cells は、数式の追加、グラフの作成など、さまざまな Excel 操作を実行できる強力なライブラリです。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
