---
title: 將資料透視表中的資料分組
linktitle: 將資料透視表中的資料分組
second_title: Aspose.Cells Java Excel 處理 API
description: 了解如何使用 Aspose.Cells for Java 在 Excel 中建立資料透視表。使用原始碼範例自動進行資料分組和分析。
weight: 14
url: /zh-hant/java/excel-pivot-tables/grouping-data-in-pivot-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將資料透視表中的資料分組


資料透視表是用於分析和匯總電子表格中的資料的強大工具。它們允許您對資料進行分組和分類以獲得有價值的見解。在本文中，我們將探討如何使用 Aspose.Cells for Java 以及原始程式碼範例有效地將資料透視表中的資料分組。

## 介紹

資料透視表提供了一種靈活的方式來組織和匯總大型資料集中的資料。它們允許您透過將資料分組為類別或層次結構來建立資料的自訂視圖。這可以幫助您更輕鬆地識別資料中的趨勢、模式和異常值。

## 第 1 步：建立資料透視表

讓我們先使用 Aspose.Cells for Java 建立資料透視表。以下是如何從範例 Excel 檔案建立資料透視表的範例。

```java
//載入 Excel 文件
Workbook workbook = new Workbook("sample.xlsx");

//存取包含資料的工作表
Worksheet worksheet = workbook.getWorksheets().get(0);

//指定資料範圍
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; //假設有20行數據
sourceData.startColumn = 0;
sourceData.endColumn = 3; //假設有4列數據

//根據資料範圍建立資料透視表
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

//透過索引取得資料透視表
PivotTable pivotTable = worksheet.getPivotTables().get(index);

//將欄位新增至行和列
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

//添加值並應用聚合
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

//儲存修改後的Excel文件
workbook.save("output.xlsx");
```

## 第 2 步：將資料分組

在 Aspose.Cells for Java 中，您可以使用下列方法將資料透視表中的資料分組：`PivotField`班級。以下是如何對資料透視表中的欄位進行分組的範例：

```java
//存取資料透視表中的「產品」字段
PivotField productField = pivotTable.getPivotFields().get("Product");

//按特定標準對「產品」欄位進行分組，例如按起始字母
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

//將修改後的 Excel 檔案與分組資料一起儲存
workbook.save("output_grouped.xlsx");
```

## 第 3 步：自訂分組

您可以進一步自訂分組設置，例如指定基於日期的分組間隔或自訂分組規則。以下是自訂基於日期的分組的範例：

```java
//存取資料透視表中的「日期」欄位（假設它是日期欄位）
PivotField dateField = pivotTable.getPivotFields().get("Date");

//按月份對日期進行分組
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

//使用自訂日期分組儲存修改後的 Excel 文件
workbook.save("output_custom_grouping.xlsx");
```

## 結論

在資料透視表中將資料分組是在 Excel 中分析和匯總資料的寶貴技術，而 Aspose.Cells for Java 可以輕鬆實現此過程的自動化。透過提供的原始程式碼範例，您可以建立資料透視表、自訂分組並有效率地從資料中取得見解。

## 常見問題解答

### 1. Excel 中資料透視表的用途是什麼？

Excel 中的資料透視表用於匯總和分析大型資料集。它們允許您建立資料的自訂視圖，從而更輕鬆地識別模式和趨勢。

### 2. 如何自訂資料透視表中的資料分組？

您可以使用以下命令自訂資料透視表中的資料分組`PivotField`Aspose.Cells for Java 中的類別。這允許您指定分組標準，例如基於日期的間隔或自訂規則。

### 3. 我可以使用 Aspose.Cells for Java 自動建立資料透視表嗎？

是的，您可以使用 Aspose.Cells for Java 在 Excel 中自動建立資料透視表，如提供的原始程式碼範例所示。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
