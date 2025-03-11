---
title: Excel での小数点データの検証
linktitle: Excel での小数点データの検証
second_title: Aspose.Cells .NET Excel 処理 API
description: わかりやすいガイドで、Aspose.Cells for .NET を使用して Excel で小数点データの検証を実装する方法を学びます。データの整合性を簡単に強化できます。
weight: 11
url: /ja/net/excel-autofilter-validation/decimal-data-validation-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel での小数点データの検証

## 導入

正確なデータを含むスプレッドシートを作成することは、あらゆるビジネスで明確なコミュニケーションを行うために不可欠です。データの正確性を確保する方法の 1 つは、Excel でデータ検証を使用することです。このチュートリアルでは、Aspose.Cells for .NET のパワーを活用して、データの信頼性とクリーンさを維持する 10 進データ検証メカニズムを作成します。Excel のスキルを向上させたいと考えているなら、ここが最適な場所です。

## 前提条件

コードに進む前に、スムーズに作業が進むようにすべて設定されていることを確認してください。

1. Visual Studio: まだインストールしていない場合は、Visual Studio をダウンロードしてインストールしてください。これは、.NET アプリケーションを開発するのに最適な環境です。
2.  Aspose.Cells for .NET: プロジェクトにAspose.Cellsライブラリを追加する必要があります。ダウンロードするには、[このリンク](https://releases.aspose.com/cells/net/).
3. C# の基礎知識: すべてを段階的に説明しますが、C# プログラミングの基礎を理解しておくと、概念をより深く理解できるようになります。
4. .NET Framework: Aspose.Cells と互換性のある必要な .NET Framework がインストールされていることを確認します。
5. ライブラリ: コンパイル エラーを回避するには、プロジェクトで Aspose.Cells ライブラリを参照します。

基本を説明したので、次は楽しい部分であるコーディングに進みましょう。

## パッケージのインポート

まず、C# ファイルに必要なパッケージをインポートする必要があります。これにより、Aspose.Cells の機能にアクセスできるようになります。

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

この行をファイルの先頭に含めることで、Excel ファイルを操作できる Aspose.Cells 機能を探すように C# に指示します。

準備ができたので、Excel ワークシートで小数点データの検証を作成するために必要な手順を見ていきましょう。

## ステップ1: ドキュメントディレクトリを設定する

ファイルを保存する前に、ドキュメント ディレクトリが正しく設定されていることを確認する必要があります。

```csharp
string dataDir = "Your Document Directory";
```

交換する`"Your Document Directory"` Excel ファイルを保存するパスを入力します。

## ステップ2: ディレクトリの存在を確認する

このスニペットは、ディレクトリが存在するかどうかを確認し、存在しない場合は作成します。

```csharp
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

このステップは、新しいプロジェクトを開始する前に作業スペースの準備ができていることを確認するようなものです。混乱もストレスもありません!

## ステップ3: ワークブックオブジェクトを作成する

次に、基本的に Excel ファイルである新しいワークブック オブジェクトを作成しましょう。

```csharp
Workbook workbook = new Workbook();
```

ワークブックは、データ用の空白のキャンバスと考えてください。この時点では、コンテンツはありませんが、ペイントする準備は整っています。

## ステップ4: ワークシートを作成してアクセスする


次に、ワークシートを作成し、ワークブックの最初のシートにアクセスします。

```csharp
Worksheet ExcelWorkSheet = workbook.Worksheets[0];
```

本に複数のページがあるように、ワークブックには複数のワークシートを含めることができます。現在は最初のワークシートに焦点を当てています。

## ステップ5: 検証コレクションを取得する

ここで、データ検証ルールを管理するため、ワークシートから検証コレクションを取得しましょう。

```csharp
ValidationCollection validations = ExcelWorkSheet.Validations;
```

このステップは、プロジェクトを開始する前にツールボックスを確認することに似ています。

## ステップ6: 検証するセル領域を定義する

検証を適用する領域を定義する必要があります。

```csharp
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 0;
ca.StartColumn = 0;
ca.EndColumn = 0;
```

ここでは、データ検証が単一のセル、具体的にはワークシートの最初のセル (A1) に適用されることを規定しています。

## ステップ7: 検証を作成して追加する

検証オブジェクトを作成し、検証コレクションに追加しましょう。

```csharp
Validation validation = validations[validations.Add(ca)];
```

これで、小数点条件を適用するように構成する検証オブジェクトができました。

## ステップ8: 検証タイプを設定する

次に、必要な検証の種類を指定します。

```csharp
validation.Type = ValidationType.Decimal;
```

タイプを Decimal に設定することで、検証されたセルに小数値が含まれることを Excel に指示します。

## ステップ9: 演算子を指定する

ここで、許容値の条件を指定します。入力されたデータが次の 2 つの範囲内にあることを確認します。

```csharp
validation.Operator = OperatorType.Between;
```

境界線を引くようなものと考えてください。この範囲外の数値は拒否され、データがクリーンな状態を保ちます。

## ステップ10: 検証の制限を設定する

次に、検証の下限と上限を設定します。

```csharp
validation.Formula1 = Decimal.MinValue.ToString();
validation.Formula2 = Decimal.MaxValue.ToString();
```

これらの制限により、有効である限り、大小を問わずすべての小数が受け入れられます。

## ステップ11: エラーメッセージのカスタマイズ

エラー メッセージを追加して、入力が拒否された理由をユーザーが理解できるようにします。

```csharp
validation.ErrorMessage = "Please enter a valid integer or decimal number";
```

これにより、何を入力すればよいかのガイダンスが提供され、ユーザーフレンドリーなエクスペリエンスが実現します。

## ステップ12: 検証領域を定義する

ここで、この検証を実行するセルを指定しましょう。

```csharp
CellArea area;
area.StartRow = 0;
area.EndRow = 9;
area.StartColumn = 0;
area.EndColumn = 0;
```

この構成では、検証はセル A1 から A10 まで適用されます。

## ステップ13: 検証領域を追加する

検証領域を定義したので、それを適用してみましょう。

```csharp
validation.AddArea(area);
```

検証が確実に実行され、不適切な入力を検出する準備が整いました。

## ステップ14: ワークブックを保存する

最後に、小数点データの検証を適用したワークブックを保存します。

```csharp
workbook.Save(dataDir + "output.out.xls");
```

これで完了です。Aspose.Cells for .NET を使用して、小数点データの検証を含むワークブックを正常に作成できました。

## 結論

Aspose.Cells for .NET を使用して Excel に小数点データの検証を実装するのは、これらの簡単な手順に従うと簡単です。データがクリーンかつ構造化された状態を保てるだけでなく、スプレッドシート全体のデータの整合性も向上し、信頼性が高く使いやすいものになります。
財務、プロジェクト管理、またはデータ レポートを利用するあらゆる分野に携わっている場合、これらのスキルを習得すると生産性が大幅に向上します。ぜひ試してみてください。スプレッドシートが喜ぶはずです。

## よくある質問

### Excel のデータ検証とは何ですか?
Excel のデータ検証は、特定のセルまたは範囲に入力できるデータの種類を制限し、データの整合性を確保する機能です。

### データ検証のエラー メッセージをカスタマイズできますか?
はい。誤ったデータ入力があった場合にユーザーを誘導するカスタム エラー メッセージを提供できます。

### Aspose.Cells は無料で使用できますか?
 Aspose.Cellsは無料トライアルを提供していますが、長期使用にはライセンスが必要です。一時ライセンスの取得に関する詳細情報をご覧ください。[ここ](https://purchase.aspose.com/temporary-license/).

### Excel で検証できるデータの種類は何ですか?
Aspose.Cells を使用すると、整数、小数、日付、リスト、カスタム数式など、さまざまなデータ型を検証できます。

### Aspose.Cells の詳細なドキュメントはどこで入手できますか?
詳細なドキュメントを閲覧することができます[ここ](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
