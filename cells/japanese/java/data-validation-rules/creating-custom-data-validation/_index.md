---
title: カスタムデータ検証の作成
linktitle: カスタムデータ検証の作成
second_title: Aspose.Cells Java Excel 処理 API
description: Aspose.Cells for Java を使用してカスタム データ検証を作成する方法を学習します。ソース コード付きのステップ バイ ステップ ガイド。
weight: 10
url: /ja/java/data-validation-rules/creating-custom-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# カスタムデータ検証の作成


## 導入

データ検証は、ユーザーが Excel スプレッドシートに不正確なデータや無効なデータを入力するのを防ぐことで、データの整合性を維持するのに役立ちます。Excel には組み込みのデータ検証オプションが用意されていますが、カスタム検証ルールを定義する必要があるシナリオもあります。Aspose.Cells for Java を使用すると、これを効率的に実現できます。

## 前提条件

コードに進む前に、次の前提条件を満たしていることを確認してください。

-  Aspose.Cells for Java: ライブラリをダウンロードしてインストールします。[ここ](https://releases.aspose.com/cells/java/).

## ステップ1: Javaプロジェクトの設定

まず、お好みの統合開発環境 (IDE) で新しい Java プロジェクトを作成します。プロジェクトのクラスパスに Aspose.Cells for Java ライブラリを追加します。

## ステップ2: Excelブックを作成する

まず、Aspose.Cells for Java を使用して新しい Excel ブックを作成しましょう。

```java
//新しい Excel ワークブックを作成するための Java コード
Workbook workbook = new Workbook();
```

## ステップ3: ワークシートの追加

ここで、カスタム データ検証を適用するワークシートをワークブックに追加します。

```java
//ワークシートを追加するJavaコード
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## ステップ4: カスタム検証基準の定義

このステップでは、データが準拠する必要があるカスタム検証基準を定義します。セルに入力される年齢を 18 ～ 60 歳に制限するとします。

```java
//カスタム検証基準を定義するJavaコード
Validation validation = worksheet.getValidations().add();
validation.setType(ValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("18");
validation.setFormula2("60");
validation.setShowError(true);
validation.setAlertStyle(ValidationAlertType.STOP);
validation.setErrorTitle("Invalid Age");
validation.setErrorMessage("Age must be between 18 and 60.");
```

## ステップ 5: 範囲にデータ検証を適用する

カスタム検証基準を定義したので、それを特定のセル範囲に適用してみましょう。

```java
//範囲にデータ検証を適用するJavaコード
CellArea area = new CellArea();
area.startRow = 0;
area.startColumn = 0;
area.endRow = 9; //最初の10行に検証を適用する
area.endColumn = 0;

validation.addArea(area);
```

## ステップ6: Excelファイルを保存する

最後に、カスタム データ検証ルールを適用した Excel ファイルを保存します。

```java
// Excel ファイルを保存するための Java コード
workbook.save("CustomDataValidation.xlsx");
```

## 結論

このチュートリアルでは、Aspose.Cells for Java を使用してカスタム データ検証ルールを作成する方法について説明しました。これらの手順に従うことで、Excel データが特定の基準に準拠していることを保証し、データの整合性と正確性を高めることができます。

## よくある質問

### Aspose.Cells for Java をダウンロードするにはどうすればいいですか?

 Aspose.Cells for Javaは次のウェブサイトからダウンロードできます。[ここ](https://releases.aspose.com/cells/java/).

### 同じワークシート内の複数の範囲にカスタム データ検証を適用できますか?

はい、必要な範囲ごとに手順 5 を繰り返すことで、同じワークシート内の複数の範囲にカスタム データ検証を適用できます。

### Aspose.Cells for Java でサポートされている他の種類のデータ検証はありますか?

はい、Aspose.Cells for Java は、整数、小数、日付、時刻、テキストの長さなど、さまざまな種類のデータ検証をサポートしています。

### データ検証が失敗したときに表示されるエラー メッセージをカスタマイズするにはどうすればよいですか?

エラーメッセージをカスタマイズするには、`setErrorMessage`手順 4 で検証基準を定義する方法。

### Aspose.Cells for Java は、さまざまな形式の Excel ファイルでも動作しますか?

はい、Aspose.Cells for Java は、XLS、XLSX、XLSM など、幅広い Excel ファイル形式をサポートしています。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
