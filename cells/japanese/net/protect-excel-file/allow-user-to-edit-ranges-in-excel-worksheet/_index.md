---
title: ユーザーが Excel ワークシートの範囲を編集できるようにする
linktitle: ユーザーが Excel ワークシートの範囲を編集できるようにする
second_title: Aspose.Cells for .NET API リファレンス
description: Aspose.Cells for .NET を使用して、ユーザーが Excel スプレッドシート内の特定の範囲を編集できるようにします。C# のソース コードを使用したステップ バイ ステップ ガイド。
weight: 10
url: /ja/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ユーザーが Excel ワークシートの範囲を編集できるようにする

## 導入

Excel ワークシートの操作では、柔軟性が鍵となることがよくあります。特に、シート全体のデータの整合性を損なうことなく、複数のユーザーが特定の領域を編集できるようにする必要がある場合はそうです。ここで Aspose.Cells for .NET が活躍します。このチュートリアルでは、ドキュメントの残りの部分を保護しながら、ユーザーが Excel ワークシート内の特定の範囲を編集できるようにする方法について詳しく説明します。この記事を読み終える頃には、概念を理解できるだけでなく、具体的な例も理解できるようになります。 

## 前提条件

細かい点に入る前に、始めるのに必要なものがすべて揃っていることを確認しましょう。

1. .NET 開発環境: 機能する .NET 開発環境 (Visual Studio または任意の他の IDE) をセットアップしておく必要があります。
2.  Aspose.Cells for .NETライブラリ: Aspose.Cellsライブラリをダウンロードしてインストールします。[ここ](https://releases.aspose.com/cells/net/).
3. C# の基礎知識: C# プログラミングに精通していると、コード例を簡単に理解できるようになります。
4. Excel の基本を理解する: Excel の仕組みを理解することで、これから説明する機能の基礎を身に付けることができます。

これらの前提条件が整えば、準備は完了です。

## パッケージのインポート

コーディングを始める前に、プロジェクトが Aspose.Cells 名前空間を認識していることを確認する必要があります。必要なパッケージをインポートする方法は次のとおりです。

```csharp
using System.IO;
using Aspose.Cells;
```

必要なものをインポートしたので、チュートリアルを段階的に進めていきましょう。

## ステップ1: ドキュメントディレクトリを設定する

どのようなファイル操作でも、ドキュメントを保存する場所を定義することが重要です。Excel ファイルを保存するための作業ディレクトリを設定しましょう。

```csharp
//ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";

//ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

まず、`"YOUR DOCUMENT DIRECTORY"`ファイルを保存するパスを指定します。このコードはディレクトリが存在するかどうかを確認し、存在しない場合は作成します。

## ステップ 2: 新しいワークブックをインスタンス化する

作業ディレクトリの準備ができたら、Excel ワークブックを作成します。 

```csharp
//新しいワークブックをインスタンス化する
Workbook book = new Workbook();
```

ここでは、`Workbook` Aspose.Cells によって提供されるクラス。これを使用すると、Excel ファイルを操作できます。

## ステップ3: デフォルトのワークシートにアクセスする

新しく作成されたすべてのワークブックには、少なくとも 1 つのワークシートが付属しています。それにアクセスしてみましょう。

```csharp
//最初の（デフォルトの）ワークシートを取得する
Worksheet sheet = book.Worksheets[0];
```

このコード スニペットでは、ワークブックの最初のワークシートにアクセスし、後続の手順で操作します。

## ステップ4: 編集範囲を許可する

ワークシートの特定の範囲を編集できるようにするには、`AllowEditRanges`財産。

```csharp
//編集範囲の許可を取得する
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

このコレクションを使用すると、ワークシート内で編集可能な範囲を管理できます。

## ステップ5: 保護範囲を定義する

次に、指定した範囲の編集を許可しながら、ワークシートのどの部分を保護するかを定義します。

```csharp
// ProtectedRange を定義する
ProtectedRange proteced_range;

//範囲を作成する
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

//パスワードを指定してください
proteced_range.Password = "123";
```

この手順では、行 1 列 1 から行 3 列 3 までのセルの編集を許可する「r2」という新しい編集可能範囲を追加します。さらに、この範囲を保護するためにパスワードを設定し、承認されたユーザーのみが変更できるようにします。

## ステップ6: ワークシートを保護する

編集可能な範囲を設定したので、ワークシートを保護する必要があります。

```csharp
//シートを保護する
sheet.Protect(ProtectionType.All);
```

このコードは、指定した範囲を除いて、ワークシート全体を不要な変更から保護します。

## ステップ7: Excelファイルを保存する

変更が Excel ファイルに反映されていることを確認するために、ワークブックを保存しましょう。

```csharp
//Excelファイルを保存する
book.Save(dataDir + "protectedrange.out.xls");
```

必要に応じてファイル名を調整してください。これにより、指定したディレクトリに、設定した内容で Excel ファイルが作成されます。

## 結論

これで完了です。指定した範囲の編集を制限し、シートの残りの部分を保護する Excel ワークシートの作成に成功しました。Aspose.Cells for .NET を使用すると、このようなタスクの管理がはるかに簡単かつ効率的になります。複雑なアプリケーションを開発する場合でも、データを安全に管理する必要がある場合でも、これらの機能によりワークフローが大幅に強化されます。

## よくある質問

### Aspose.Cells とは何ですか?
Aspose.Cells は、Excel ファイルを処理するための強力な .NET ライブラリであり、プログラムによるスプレッドシートの作成、編集、変換などの機能を提供します。

### 複数の編集範囲を適用できますか?
もちろんです！`Add`方法`allowRanges`コレクションを複数回使用して、複数の編集可能な範囲を指定します。

### パスワードを忘れた場合はどうなりますか?
残念ながら、編集可能な範囲のパスワードを忘れた場合は、保護を解除するか、資格情報を必要とする可能性のある定義済みの方法でファイルにアクセスする必要があります。

### Aspose.Cells の無料版はありますか?
はい、Aspose では、購入前に機能を試すことができる無料トライアルを提供しています。

### Aspose.Cells の詳細情報はどこで入手できますか?
確認するには[ドキュメント](https://reference.aspose.com/cells/net/)詳細なガイドとリファレンスについては、こちらをご覧ください。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
