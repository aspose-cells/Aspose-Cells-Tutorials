---
title: 创建自定义数据验证
linktitle: 创建自定义数据验证
second_title: Aspose.Cells Java Excel 处理 API
description: 了解如何使用 Aspose.Cells for Java 创建自定义数据验证。带有源代码的分步指南。
weight: 10
url: /zh/java/data-validation-rules/creating-custom-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建自定义数据验证


## 介绍

数据验证可防止用户在 Excel 电子表格中输入不正确或无效的数据，从而帮助维护数据完整性。虽然 Excel 提供了内置数据验证选项，但在某些情况下您需要定义自定义验证规则。Aspose.Cells for Java 可让您高效地实现此目的。

## 先决条件

在深入研究代码之前，请确保您满足以下先决条件：

-  Aspose.Cells for Java：从以下网址下载并安装该库[这里](https://releases.aspose.com/cells/java/).

## 步骤 1：设置 Java 项目

首先，在您首选的集成开发环境 (IDE) 中创建一个新的 Java 项目。将 Aspose.Cells for Java 库添加到项目的类路径中。

## 步骤 2：创建 Excel 工作簿

让我们首先使用 Aspose.Cells for Java 创建一个新的 Excel 工作簿。

```java
// Java 代码用于创建新的 Excel 工作簿
Workbook workbook = new Workbook();
```

## 步骤 3：添加工作表

现在，让我们向工作簿添加一个工作表，我们将在其中应用自定义数据验证。

```java
//添加工作表的 Java 代码
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 步骤 4：定义自定义验证标准

在此步骤中，我们将定义数据必须遵守的自定义验证标准。假设我们想将单元格中输入的年龄限制在 18 至 60 岁之间。

```java
//定义自定义验证标准的 Java 代码
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

## 步骤 5：将数据验证应用于范围

现在我们已经定义了自定义验证标准，让我们将其应用到特定范围的单元格。

```java
// Java 代码将数据验证应用于某一范围
CellArea area = new CellArea();
area.startRow = 0;
area.startColumn = 0;
area.endRow = 9; //对前十行应用验证
area.endColumn = 0;

validation.addArea(area);
```

## 步骤6：保存Excel文件

最后，保存应用了自定义数据验证规则的 Excel 文件。

```java
//保存 Excel 文件的 Java 代码
workbook.save("CustomDataValidation.xlsx");
```

## 结论

在本教程中，我们探讨了如何使用 Aspose.Cells for Java 创建自定义数据验证规则。通过遵循这些步骤，您可以确保您的 Excel 数据符合特定标准，从而提高数据完整性和准确性。

## 常见问题解答

### 如何下载 Aspose.Cells for Java？

您可以从以下网站下载 Aspose.Cells for Java：[这里](https://releases.aspose.com/cells/java/).

### 我可以将自定义数据验证应用于同一张工作表中的多个范围吗？

是的，您可以通过对每个所需范围重复步骤 5，将自定义数据验证应用于同一工作表内的多个范围。

### Aspose.Cells for Java 是否支持其他类型的数据验证？

是的，Aspose.Cells for Java 支持各种类型的数据验证，包括整数、小数、日期、时间、文本长度等。

### 如何自定义数据验证失败时显示的错误信息？

您可以通过修改`setErrorMessage`方法，在步骤 4 中定义验证标准。

### Aspose.Cells for Java 能处理不同格式的 Excel 文件吗？

是的，Aspose.Cells for Java 支持多种 Excel 文件格式，包括 XLS、XLSX、XLSM 等。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
