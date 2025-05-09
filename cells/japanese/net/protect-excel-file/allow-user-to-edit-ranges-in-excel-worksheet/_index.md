---
"description": "Aspose.Cells for .NET を使用して、Excel スプレッドシート内の特定の範囲を編集できるようにします。C# のソースコードを使用したステップバイステップガイドです。"
"linktitle": "ユーザーが Excel ワークシートの範囲を編集できるようにする"
"second_title": "Aspose.Cells for .NET API リファレンス"
"title": "ユーザーが Excel ワークシートの範囲を編集できるようにする"
"url": "/ja/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# ユーザーが Excel ワークシートの範囲を編集できるようにする

## 導入

Excelワークシートの操作では、柔軟性が鍵となることがよくあります。特に、シート全体のデータの整合性を損なうことなく、複数のユーザーが特定の領域を編集する必要がある場合はなおさらです。Aspose.Cells for .NETが真価を発揮するのはまさにこの点です。このチュートリアルでは、Excelワークシート内の特定の範囲のみを編集できるようにしながら、ドキュメントの残りの部分は保護する方法について詳しく説明します。この記事を読み終える頃には、概念を理解するだけでなく、具体的な例を使って作業を進めることができるようになります。 

## 前提条件

具体的な内容に入る前に、始めるのに必要なものがすべて揃っていることを確認しましょう。

1. .NET 開発環境: 機能する .NET 開発環境 (Visual Studio または任意の他の IDE) がセットアップされている必要があります。
2. Aspose.Cells for .NET ライブラリ: Aspose.Cells ライブラリをダウンロードしてインストールします。 [ここ](https://releases。aspose.com/cells/net/).
3. C# の基本知識: C# プログラミングに精通していると、コード例を簡単に理解できるようになります。
4. Excel の基本を理解する: Excel の仕組みを理解することで、これから説明する機能の基礎を身に付けることができます。

これらの前提条件が満たされれば、準備は完了です。

## パッケージのインポート

コーディングを始める前に、プロジェクトがAspose.Cells名前空間を認識していることを確認する必要があります。必要なパッケージをインポートする方法は次のとおりです。

```csharp
using System.IO;
using Aspose.Cells;
```

必要なものをインポートしたので、チュートリアルを段階的に進めていきましょう。

## ステップ1: ドキュメントディレクトリを設定する

ファイル操作を行う際には、ドキュメントを保存する場所を明確にしておくことが重要です。Excelファイルを保存する作業ディレクトリを設定しましょう。

```csharp
// ドキュメント ディレクトリへのパス。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// ディレクトリがまだ存在しない場合は作成します。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

まず、 `"YOUR DOCUMENT DIRECTORY"` ファイルを保存したいパスを指定します。このコードはディレクトリが存在するかどうかを確認し、存在しない場合はディレクトリを作成します。

## ステップ2: 新しいワークブックをインスタンス化する

作業ディレクトリの準備ができたら、Excel ブックを作成します。 

```csharp
// 新しいワークブックをインスタンス化する
Workbook book = new Workbook();
```

ここでは、 `Workbook` Aspose.Cells によって提供されるクラス。これを使用して Excel ファイルを操作できます。

## ステップ3: デフォルトのワークシートにアクセスする

新しく作成されたワークブックには、少なくとも 1 つのワークシートが含まれています。それにアクセスしてみましょう。

```csharp
// 最初の（デフォルトの）ワークシートを取得する
Worksheet sheet = book.Worksheets[0];
```

このコード スニペットでは、ワークブックの最初のワークシートにアクセスし、後続の手順で操作します。

## ステップ4: 編集範囲の許可を取得する

ワークシートの特定の範囲を編集できるようにするには、 `AllowEditRanges` 財産。

```csharp
// 編集範囲の許可を取得する
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

このコレクションを使用すると、ワークシート内で編集可能な範囲を管理できます。

## ステップ5: 保護範囲を定義する

次に、指定した範囲の編集を許可しながら、ワークシートのどの部分を保護するかを定義します。

```csharp
// ProtectedRangeを定義する
ProtectedRange proteced_range;

// 範囲を作成する
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

// パスワードを指定してください
proteced_range.Password = "123";
```

この手順では、「r2」という新しい編集可能な範囲を追加し、行 1 列 1 から行 3 列 3 までのセルを編集できるようにします。さらに、この範囲を保護するためにパスワードを設定し、承認されたユーザーのみが変更できるようにします。

## ステップ6: ワークシートを保護する

編集可能な範囲を設定したので、ワークシートを保護する必要があります。

```csharp
// シートを保護する
sheet.Protect(ProtectionType.All);
```

このコードは、指定した範囲を除いて、ワークシート全体を不要な変更から保護します。

## ステップ7: Excelファイルを保存する

変更が Excel ファイルに反映されるのを確認できるように、ワークブックを保存しましょう。

```csharp
// Excelファイルを保存する
book.Save(dataDir + "protectedrange.out.xls");
```

必要に応じてファイル名を調整してください。これにより、指定したディレクトリに、設定した内容でExcelファイルが作成されます。

## 結論

これで完了です！指定した範囲のみの編集を制限し、シートの残りの部分は保護するExcelワークシートの作成に成功しました。Aspose.Cells for .NETを使用すると、このようなタスクの管理がはるかに簡単かつ効率的になります。複雑なアプリケーションを開発する場合でも、単にデータを安全に管理する必要がある場合でも、これらの機能はワークフローを大幅に強化します。

## よくある質問

### Aspose.Cells とは何ですか?
Aspose.Cells は、Excel ファイルを処理するための強力な .NET ライブラリであり、プログラムによるスプレッドシートの作成、編集、変換などの機能を提供します。

### 複数の編集範囲を適用できますか?
もちろんです！ `Add` 方法 `allowRanges` 複数の編集可能な範囲を指定するには、コレクションを複数回実行します。

### パスワードを忘れた場合はどうなりますか?
残念ながら、編集可能な範囲のパスワードを忘れた場合は、保護を解除するか、資格情報を必要とする事前定義された方法でファイルにアクセスする必要があります。

### Aspose.Cells の無料版はありますか?
はい、Aspose では、購入前に機能を試すことができる無料トライアルを提供しています。

### Aspose.Cells の詳細情報はどこで入手できますか?
確認するには [ドキュメント](https://reference.aspose.com/cells/net/) 詳細なガイドとリファレンスについては、こちらをご覧ください。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}