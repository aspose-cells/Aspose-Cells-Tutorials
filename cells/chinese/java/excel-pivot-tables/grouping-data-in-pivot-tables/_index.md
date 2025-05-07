---
"description": "学习如何使用 Aspose.Cells for Java 在 Excel 中创建数据透视表。使用源代码示例自动进行数据分组和分析。"
"linktitle": "在数据透视表中分组数据"
"second_title": "Aspose.Cells Java Excel 处理 API"
"title": "在数据透视表中分组数据"
"url": "/zh/java/excel-pivot-tables/grouping-data-in-pivot-tables/"
"weight": 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在数据透视表中分组数据


数据透视表是分析和汇总电子表格中数据的强大工具。它允许您对数据进行分组和分类，从而获得有价值的见解。在本文中，我们将探讨如何使用 Aspose.Cells for Java 在数据透视表中有效地分组数据，并提供源代码示例。

## 介绍

数据透视表提供了一种灵活的方式来组织和汇总大型数据集中的数据。它允许您通过将数据分组为类别或层次结构来创建自定义数据视图。这可以帮助您更轻松地识别数据中的趋势、模式和异常值。

## 步骤 1：创建数据透视表

让我们首先使用 Aspose.Cells for Java 创建数据透视表。以下是如何从示例 Excel 文件创建数据透视表的示例。

```java
// 加载 Excel 文件
Workbook workbook = new Workbook("sample.xlsx");

// 访问包含数据的工作表
Worksheet worksheet = workbook.getWorksheets().get(0);

// 指定数据范围
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // 假设有 20 行数据
sourceData.startColumn = 0;
sourceData.endColumn = 3; // 假设有 4 列数据

// 根据数据范围创建数据透视表
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// 通过索引获取数据透视表
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// 向行和列添加字段
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// 添加值并应用聚合
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// 保存修改后的Excel文件
workbook.save("output.xlsx");
```

## 第 2 步：分组数据

在 Aspose.Cells for Java 中，您可以使用 `PivotField` 类。下面是如何对数据透视表中的字段进行分组的示例：

```java
// 访问数据透视表中的“产品”字段
PivotField productField = pivotTable.getPivotFields().get("Product");

// 按特定标准对“产品”字段进行分组，例如按首字母
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// 保存修改后的包含分组数据的 Excel 文件
workbook.save("output_grouped.xlsx");
```

## 步骤 3：自定义分组

您可以进一步自定义分组设置，例如指定基于日期的分组间隔或自定义分组规则。以下是自定义基于日期的分组的示例：

```java
// 访问数据透视表中的“日期”字段（假设它是一个日期字段）
PivotField dateField = pivotTable.getPivotFields().get("Date");

// 按月份对日期进行分组
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// 使用自定义日期分组保存修改后的 Excel 文件
workbook.save("output_custom_grouping.xlsx");
```

## 结论

在数据透视表中分组数据是分析和汇总 Excel 数据的有效方法，而 Aspose.Cells for Java 可以轻松实现此过程的自动化。借助提供的源代码示例，您可以创建数据透视表、自定义分组并高效地从数据中获取洞察。

## 常见问题解答

### 1. Excel 中的数据透视表有什么用途？

Excel 中的数据透视表用于汇总和分析大型数据集。它们允许您创建数据的自定义视图，从而更轻松地识别模式和趋势。

### 2. 如何自定义数据透视表中数据的分组？

您可以使用 `PivotField` Aspose.Cells for Java 中的类。这允许您指定分组条件，例如基于日期的间隔或自定义规则。

### 3. 我可以使用 Aspose.Cells for Java 自动创建数据透视表吗？

是的，您可以使用 Aspose.Cells for Java 自动在 Excel 中创建数据透视表，如提供的源代码示例所示。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}