---
"description": "Aspose.Cells for .NET を使用して、Excel ワークシートのセルと範囲を保護する方法を学びましょう。このステップバイステップガイドに従って、スプレッドシートを保護しましょう。"
"linktitle": "Aspose.Cells を使用してワークシート内のセルと範囲を保護する"
"second_title": "Aspose.Cells .NET Excel 処理 API"
"title": "Aspose.Cells を使用してワークシート内のセルと範囲を保護する"
"url": "/ja/net/worksheet-security/protect-cells-and-ranges/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells を使用してワークシート内のセルと範囲を保護する

## 導入
スプレッドシートの作業では、特に共同作業環境では、シートの特定の部分を不正な変更から保護することがしばしば必要になります。このチュートリアルでは、Aspose.Cells for .NET を使用して、ワークシート内の特定のセルと範囲を保護する方法を説明します。保護されたシートの設定、編集可能な範囲の指定、そしてファイルの保存手順を順を追って説明します。これは、機密データへのアクセスを制限しながら、特定のセクションを他のユーザーによる変更を許可したい場合に非常に便利な機能です。
## 前提条件
チュートリアルに進む前に、次の前提条件が満たされていることを確認してください。
1. Aspose.Cells for .NET: プロジェクトにAspose.Cellsライブラリがインストールされている必要があります。まだインストールされていない場合は、以下のリンクからダウンロードできます。 [Aspose ウェブサイト](https://releases。aspose.com/cells/net/).
2. Visual Studio: このガイドでは、Visual Studio または C# 開発をサポートする同様の IDE を使用していることを前提としています。
3. C# の基礎知識: C# プログラミングの基礎と Visual Studio でプロジェクトを設定する方法に精通している必要があります。
4. Aspose.Cellsライセンス：Asposeは無料トライアルを提供していますが、有効なライセンスをお持ちであれば、ライブラリの全機能をご利用いただけます。ライセンスをお持ちでない場合は、 [仮免許証はこちら](https://purchase。aspose.com/temporary-license/).
上記のすべての準備が整ったことを確認したら、コーディング部分に進むことができます。
## パッケージのインポート
Aspose.Cells を使用するには、まず必要な名前空間を C# ファイルにインポートする必要があります。インポート方法は次のとおりです。
```csharp
using System.IO;
using Aspose.Cells;
```
その `Aspose.Cells` 名前空間を使用すると、Excelファイルを操作するためのコア機能にアクセスできます。 `System.IO` ワークブックの保存などのファイル操作に使用されます。
ここで、Aspose.Cells を使用してワークシート内のセルと範囲を保護する手順を詳しく説明します。
## ステップ1: 環境を設定する
まず、Excelファイルを保存するディレクトリを作成してください。ディレクトリがまだ存在しない場合は、自動的に作成されます。これにより、出力ファイルを保存するための場所が確保されます。
```csharp
// ドキュメントディレクトリへのパスを定義する
string dataDir = "Your Document Directory";
// ディレクトリが存在するかどうかを確認し、存在しない場合は作成します
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
    Directory.CreateDirectory(dataDir);
```
ここでは、 `System.IO.Directory.Exists()` フォルダが存在するかどうかを確認し、存在しない場合は、 `Directory。CreateDirectory()`.
## ステップ2: 新しいワークブックを作成する
それでは、新しい Workbook オブジェクトをインスタンス化しましょう。これは、セルと範囲を定義する Excel ファイルとして機能します。
```csharp
// 新しいワークブックオブジェクトをインスタンス化する
Workbook book = new Workbook();
```
その `Workbook` クラスは、Aspose.Cells で Excel ファイルを操作する際のエントリポイントです。Excel ドキュメントを表します。
## ステップ3: デフォルトのワークシートにアクセスする
新しく作成されたワークブックには必ずデフォルトのワークシートがあります。これを取得して、その内容を操作します。
```csharp
// ワークブックの最初の（デフォルトの）ワークシートを取得する
Worksheet sheet = book.Worksheets[0];
```
ここ、 `Worksheets[0]` ワークブックの最初のシートを取得します (インデックスは 0 から始まります)。
## ステップ4: 編集可能な範囲を定義する
ワークシートの特定の部分を保護し、ユーザーが特定のセルを編集できるようにするには、編集可能な範囲を定義する必要があります。編集可能な範囲を作成し、ワークシートのAllowEditRangesコレクションに追加します。
```csharp
// AllowEditRangesコレクションを取得する
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
// ProtectedRangeを定義してコレクションに追加する
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
ProtectedRange protectedRange = allowRanges[idx];
```
上記のコードでは:
- `"r2"` 編集可能な範囲の名前です。
- 数字 `1, 1, 3, 3` 範囲の開始行インデックスと終了行インデックス、列インデックスを表します (つまり、セル B2 から D4 まで)。
## ステップ5: 保護された範囲にパスワードを設定する
編集可能な範囲を定義したので、パスワードを設定して保護しましょう。つまり、ユーザーはこの範囲を編集する際にパスワードが必要になります。
```csharp
// 編集可能な範囲のパスワードを指定します
protectedRange.Password = "123";
```
ここではパスワードを次のように設定しました `"123"`ただし、安全なパスワードを設定することもできます。この手順は、編集領域へのアクセスを制御するために不可欠です。
## ステップ6：シート全体を保護する
この段階では、ワークシート全体を保護します。ワークシートを保護すると、許可された範囲を除くシートの他の部分は編集できなくなります。
```csharp
// 指定された保護タイプ（すべて）でシートを保護します
sheet.Protect(ProtectionType.All);
```
これにより、編集可能な範囲内のセルを除き、シート内のすべてのセルがロックされます。
## ステップ7: ワークブックを保存する
最後に、ワークブックをファイルに保存します。保護されたシートは、指定した名前で保存されます。
```csharp
// Excelファイルを指定されたディレクトリに保存します
book.Save(dataDir + "protectedrange.out.xls");
```
ここで、Excelファイルは次のように保存されます。 `protectedrange.out.xls` 先ほど定義したディレクトリに保存します。別の名前や形式で保存したい場合は、ファイル名と拡張子を変更できます。
## 結論
このチュートリアルでは、Aspose.Cells for .NET を使用して Excel ワークシートのセルと範囲を保護する方法を学習しました。このアプローチにより、スプレッドシートの編集可能な領域と編集不可能な領域を柔軟に制御できます。これらのスキルを実際のプロジェクトに適用することで、機密データのセキュリティを確保しながら、ユーザーが編集可能な領域を確保できます。
覚えておいてください、Aspose.Cells は Excel ファイルの操作のための強力なツール セットを提供しており、これは Aspose.Cells で実行できる多くの機能の 1 つにすぎません。 
## よくある質問
### ワークシート内の特定のセルのみを保護することはできますか?
はい、 `AllowEditRanges` プロパティを使用すると、ワークシートの残りの部分を保護したまま、編集可能なセルまたは範囲を指定できます。
### 後で保護を解除できますか?
はい、ワークシートの保護を解除するには、 `Unprotect()` 方法があり、パスワードが設定されている場合は、それを入力する必要があります。
### シート全体をパスワードで保護するにはどうすればよいですか?
シート全体を保護するには、 `Protect()` パスワードの有無にかかわらず、以下の方法で実行できます。例えば、 `sheet。Protect("password")`.
### 編集可能な範囲を複数追加できますか?
もちろんです！編集可能な範囲を必要なだけ追加するには、 `allowRanges.Add()` 複数回。
### Aspose.Cells には他にどのようなセキュリティ機能がありますか?
Aspose.Cells は、ワークブックの暗号化、ファイル パスワードの設定、セルとシートの保護など、さまざまなセキュリティ機能をサポートしています。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}