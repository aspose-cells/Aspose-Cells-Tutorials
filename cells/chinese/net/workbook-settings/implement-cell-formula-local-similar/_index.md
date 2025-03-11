---
title: 实现类似于本地范围公式的本地单元格公式
linktitle: 实现类似于本地范围公式的本地单元格公式
second_title: Aspose.Cells .NET Excel 处理 API
description: 了解如何实现类似于 Aspose.Cells for .NET 中的范围公式本地功能的单元格公式。学习自定义内置 Excel 函数名称等。
weight: 13
url: /zh/net/workbook-settings/implement-cell-formula-local-similar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 实现类似于本地范围公式的本地单元格公式

## 介绍
Aspose.Cells for .NET 是一个功能强大且灵活的电子表格操作 API，允许您以编程方式创建、操作和转换 Excel 文件。Aspose.Cells 提供的众多功能之一是能够自定义内置 Excel 函数的行为，包括创建自己的本地函数名称。在本教程中，我们将引导您完成实现类似于 Aspose.Cells for .NET 中的范围公式本地功能的单元格公式的步骤。
## 先决条件
开始之前，请确保您已准备好以下物品：
1. 您的系统上安装了 Microsoft Visual Studio 2010 或更高版本。
2. 您的项目中安装了最新版本的 Aspose.Cells for .NET 库。您可以从[Aspose.Cells for .NET 下载页面](https://releases.aspose.com/cells/net/).
## 导入包
首先，您需要在 C# 项目中导入必要的包。在代码文件顶部添加以下 using 语句：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## 步骤 1：创建自定义全球化设置类
第一步是创建自定义`GlobalizationSettings`类，允许您覆盖 Excel 函数的默认行为。在此示例中，我们将更改`SUM`和`AVERAGE`功能`UserFormulaLocal_SUM`和`UserFormulaLocal_AVERAGE`， 分别。
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //根据您的需要更改 SUM 函数名称。
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //根据您的需要更改 AVERAGE 函数名称。
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## 步骤 2：创建新工作簿并分配自定义全球化设置
接下来，创建一个新的 Workbook 实例并分配自定义`GlobalizationSettings`工作簿的实现类`Settings.GlobalizationSettings`财产。
```csharp
//创建工作簿
Workbook wb = new Workbook();
//分配 GlobalizationSettings 实现类
wb.Settings.GlobalizationSettings = new GS();
```
## 步骤 3：访问第一个工作表和单元格
现在，让我们访问工作簿中的第一个工作表和该工作表中的特定单元格。
```csharp
//访问第一个工作表
Worksheet ws = wb.Worksheets[0];
//访问一些单元格
Cell cell = ws.Cells["C4"];
```
## 步骤 4：分配公式并打印 FormulaLocal
最后，让我们分配`SUM`和`AVERAGE`公式到单元格并打印结果`FormulaLocal`值。
```csharp
//分配 SUM 公式并打印其 FormulaLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//分配 AVERAGE 公式并打印其 FormulaLocal
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## 结论
在本教程中，您学习了如何实现类似于 Aspose.Cells for .NET 中的范围公式本地功能的单元格公式。通过创建自定义`GlobalizationSettings`类，您可以覆盖 Excel 函数的默认行为并自定义本地函数名称以满足您的需求。这在处理本地化或国际化的 Excel 文档时特别有用。
## 常见问题解答
### 的目的是什么`GlobalizationSettings` class in Aspose.Cells?
这`GlobalizationSettings` Aspose.Cells 中的类允许您自定义内置 Excel 函数的行为，包括更改本地函数名称的能力。
### 我可以覆盖除`SUM` and `AVERAGE`?
是的，你可以通过修改`GetLocalFunctionName`您的自定义方法`GlobalizationSettings`班级。
### 有没有办法将函数名称重置回其默认值？
是的，您可以通过删除自定义`GlobalizationSettings`类或通过从`GetLocalFunctionName`方法。
### 我可以使用此功能在 Aspose.Cells 中创建自定义函数吗？
不，`GlobalizationSettings`类旨在覆盖内置 Excel 函数的行为，而不是创建自定义函数。如果需要创建自定义函数，可以使用`UserDefinedFunction`Aspose.Cells 中的类。
### 所有版本的 Aspose.Cells for .NET 都提供此功能吗？
是的，`GlobalizationSettings`类和自定义函数名称的能力在所有版本的 Aspose.Cells for .NET 中均可用。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
