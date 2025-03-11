---
title: ピボットテーブルでのデータのグループ化
linktitle: ピボットテーブルでのデータのグループ化
second_title: Aspose.Cells Java Excel 処理 API
description: Aspose.Cells for Java を使用して Excel でピボット テーブルを作成する方法を学習します。ソース コードの例を使用して、データのグループ化と分析を自動化します。
weight: 14
url: /ja/java/excel-pivot-tables/grouping-data-in-pivot-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ピボットテーブルでのデータのグループ化


ピボット テーブルは、スプレッドシートのデータを分析および要約するための強力なツールです。データをグループ化および分類して、貴重な洞察を得ることができます。この記事では、Aspose.Cells for Java を使用してピボット テーブルでデータを効果的にグループ化する方法と、ソース コードの例について説明します。

## 導入

ピボット テーブルは、大規模なデータセットのデータを柔軟に整理して要約する方法を提供します。データをカテゴリまたは階層にグループ化することで、データのカスタム ビューを作成できます。これにより、データの傾向、パターン、外れ値をより簡単に特定できます。

## ステップ1: ピボットテーブルを作成する

まず、Aspose.Cells for Java を使用してピボット テーブルを作成しましょう。以下は、サンプル Excel ファイルからピボット テーブルを作成する方法の例です。

```java
// Excelファイルを読み込む
Workbook workbook = new Workbook("sample.xlsx");

//データを含むワークシートにアクセスする
Worksheet worksheet = workbook.getWorksheets().get(0);

//データ範囲を指定する
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; //20行のデータを想定
sourceData.startColumn = 0;
sourceData.endColumn = 3; //4列のデータを想定

//データ範囲に基づいてピボットテーブルを作成する
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

//インデックスでピボットテーブルを取得する
PivotTable pivotTable = worksheet.getPivotTables().get(index);

//行と列にフィールドを追加する
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

//値を追加して集計を適用する
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

//変更したExcelファイルを保存する
workbook.save("output.xlsx");
```

## ステップ2: データのグループ化

Aspose.Cells for Javaでは、ピボットテーブル内のデータをグループ化するために、`PivotField`クラス。ピボット テーブルでフィールドをグループ化する方法の例を次に示します。

```java
//ピボットテーブルの「製品」フィールドにアクセスする
PivotField productField = pivotTable.getPivotFields().get("Product");

//「製品」フィールドを特定の基準（例：先頭文字）でグループ化する
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

//グループ化されたデータを含む変更されたExcelファイルを保存する
workbook.save("output_grouped.xlsx");
```

## ステップ3: グループ化をカスタマイズする

日付に基づくグループ化間隔やカスタム グループ化ルールを指定するなど、グループ化設定をさらにカスタマイズできます。日付に基づくグループ化をカスタマイズする例を次に示します。

```java
//ピボット テーブルの「日付」フィールドにアクセスします (日付フィールドであると仮定)
PivotField dateField = pivotTable.getPivotFields().get("Date");

//月ごとに日付をグループ化する
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

//カスタム日付グループ化で変更したExcelファイルを保存する
workbook.save("output_custom_grouping.xlsx");
```

## 結論

ピボット テーブルでデータをグループ化することは、Excel でデータを分析および要約するための有用な手法であり、Aspose.Cells for Java を使用すると、このプロセスを簡単に自動化できます。提供されているソース コードの例を使用すると、ピボット テーブルを作成し、グループ化をカスタマイズし、データから効率的に洞察を得ることができます。

## よくある質問

### 1. Excel のピボット テーブルの目的は何ですか?

Excel のピボット テーブルは、大規模なデータセットを要約および分析するために使用されます。データのカスタム ビューを作成できるため、パターンや傾向を簡単に特定できます。

### 2. ピボット テーブル内のデータのグループ化をカスタマイズするにはどうすればよいですか?

ピボットテーブル内のデータのグループ化は、`PivotField` Aspose.Cells for Java のクラス。これにより、日付ベースの間隔やカスタム ルールなどのグループ化条件を指定できます。

### 3. Aspose.Cells for Java を使用してピボット テーブルの作成を自動化できますか?

はい、提供されているソース コードの例に示されているように、Aspose.Cells for Java を使用して Excel でのピボット テーブルの作成を自動化できます。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
