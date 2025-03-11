---
title: Excel ワークシートの範囲を編集する
linktitle: Excel ワークシートの範囲を編集する
second_title: Aspose.Cells for .NET API リファレンス
description: この包括的なガイドでは、ステップバイステップの手順を取り上げ、Aspose.Cells for .NET を使用して Excel ワークシートの範囲を編集する方法を学習します。
weight: 20
url: /ja/net/protect-excel-file/edit-ranges-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel ワークシートの範囲を編集する

## 導入

Excel スプレッドシートの編集に関して言えば、最も便利な機能の 1 つは、特定の領域を保護しながら他の領域を編集できるようにする機能です。これは、複数のユーザーがアクセスする必要があるものの、指定されたセルのみを変更しなければならない共同作業環境で非常に役立ちます。今日は、Aspose.Cells for .NET を利用して Excel ワークシート内の編集可能な範囲を管理する方法について詳しく説明します。では、お気に入りのコーディング ドリンクを手に取って、始めましょう。

## 前提条件

コーディングを始める前に、準備が整っていることを確認しましょう。必要なものは次のとおりです。

1. Visual Studio: Visual Studio がインストールされていることを確認してください。コミュニティ エディションは問題なく動作します。
2.  Aspose.Cellsライブラリ: Aspose.Cells for .NETライブラリが必要です。[ここからダウンロード](https://releases.aspose.com/cells/net/).
3. 基本的な C# の知識: C# の基礎的な理解は大いに役立ちます。
4. プロジェクトのセットアップ: Visual Studio で新しい C# コンソール アプリケーションを作成します。

完璧です。準備完了です。では、コードの細部を見ていきましょう。

## パッケージのインポート

プロジェクトをセットアップしたら、最初のステップとして必要な Aspose.Cells 名前空間をインポートします。これを行うには、コード ファイルの先頭に次の行を追加するだけです。

```csharp
using Aspose.Cells;
```

これにより、プロジェクトで Aspose.Cells によって提供されるすべての機能にアクセスできるようになります。

## ステップ1: ディレクトリを設定する

Excel ファイルの操作を開始する前に、ファイルを保存するディレクトリを確立することをお勧めします。この手順により、アプリケーションがデータの読み取りと書き込みを行う場所を認識できるようになります。

ディレクトリを作成するためのコードをレイアウトしてみましょう (まだ存在しない場合)。

```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";
//ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

交換する`"YOUR DOCUMENT DIRECTORY"`ファイルを保管したいパスを入力します。たとえば、`@"C:\ExcelFiles\"`.

## ステップ 2: 新しいワークブックをインスタンス化する

ディレクトリの設定が完了したら、新しい Excel ブックを作成しましょう。これは、絵を描き始める前に空白のキャンバスを起動するようなものです。

```csharp
//新しいワークブックをインスタンス化する
Workbook book = new Workbook();
```

これで、空のワークブックの準備ができました。

## ステップ3: 最初のワークシートを入手する

各ワークブックには、デフォルトで少なくとも 1 つのワークシートが含まれています。ワークシートに対して操作を実行するには、そのワークシートを取得する必要があります。

```csharp
//最初の（デフォルトの）ワークシートを取得する
Worksheet sheet = book.Worksheets[0];
```

ここで、最初のワークシートにアクセスします。これは、ノートブックの新しい紙を開くのと似ています。

## ステップ4: 編集範囲を許可する

編集可能な範囲を設定する前に、ワークシートから保護された範囲のコレクションを取得する必要があります。

```csharp
//編集範囲の許可を取得する
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

この行は、保護された範囲を管理するコレクションを取得します。内部で何が利用できるかを知っておくと便利です。

## ステップ5: 保護範囲の定義と作成

この時点で、編集を許可する範囲を定義する準備が整いました。この範囲を作成しましょう。

```csharp
// ProtectedRange を定義する
ProtectedRange proteced_range;

//範囲を作成する
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];
```

上記のコードでは、行 1、列 1 から行 3、列 3 までのセル (Excel 用語では A1 から C3 のブロックに相当) を編集できる「r2」という保護された範囲を作成しています。必要に応じてこれらのインデックスを調整できます。

## ステップ6: パスワードを設定する 

保護された範囲にパスワードを設定すると、パスワードを持つユーザーだけが定義された領域を変更できるようになります。この手順により、スプレッドシートのセキュリティが強化されます。

```csharp
//パスワードを指定してください
proteced_range.Password = "YOUR_PASSWORD";
```

交換する`"YOUR_PASSWORD"`パスワードは自由に設定できます。ただし、あまり単純なパスワードにはしないでください。宝箱に鍵をかけるようなものだと思ってください。

## ステップ7: シートを保護する

編集可能な範囲を定義し、パスワードで保護したので、次はワークシート全体を保護します。

```csharp
//シートを保護する
sheet.Protect(ProtectionType.All);
```

このメソッドを呼び出すと、基本的にワークシート全体がロックされます。編集用に定義された範囲のみを変更できます。

## ステップ8: Excelファイルを保存する

ついにチュートリアルの最後のステップ、つまり定義したディレクトリにワークブックを保存するところまで来ました。

```csharp
//Excelファイルを保存する
book.Save(dataDir + "protectedrange.out.xls");
```

これにより、保護されたワークブックが次のように保存されます。`protectedrange.out.xls`指定したディレクトリに。

## 結論

これで完了です。Aspose.Cells for .NET を使用して Excel ワークシートを作成し、編集可能な範囲を定義し、パスワードを設定し、シートを保護しました。すべて簡単な手順で完了です。これで、ワークブックを同僚と共有して、重要なデータを安全に保ちながら共同作業を強化できます。

## よくある質問

### Aspose.Cells とは何ですか?  
Aspose.Cells は、開発者がプログラムによって Excel ファイルを作成、操作、変換できるようにする強力な .NET ライブラリです。

### Excel ワークシート内の特定のセルを保護することはできますか?  
はい、Aspose.Cells を使用すると、特定の編集可能な範囲を定義し、ワークシートの残りの部分を保護できます。

### Aspose.Cells の試用版はありますか?  
もちろんです！無料トライアルをダウンロードできます[ここ](https://releases.aspose.com/).

### Aspose.Cells を他のプログラミング言語で使用できますか?  
このチュートリアルでは .NET に焦点を当てていますが、Aspose.Cells は Java や Cloud API を含む複数のプログラミング言語で利用できます。

### Aspose.Cells の詳細情報はどこで入手できますか?  
完全なドキュメントを閲覧することができます[ここ](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
