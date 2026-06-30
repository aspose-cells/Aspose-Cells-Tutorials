---
category: general
date: 2026-06-30
description: 使用 Aspose.Cells 在 Excel 工作簿中创建条件格式。了解如何设置单元格背景、对单元格进行排名以及以编程方式生成文件。
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: zh
og_description: 使用 Aspose.Cells 在 Excel 工作簿中创建条件格式。通过本完整教程设置单元格背景、对单元格进行排名并实现 Excel
  自动化。
og_title: 使用 Aspose.Cells 在 Excel 中创建条件格式
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: 使用 Aspose.Cells 在 Excel 中创建条件格式 – 步骤指南
url: /zh/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中使用 Aspose.Cells 创建条件格式 – 步骤指南

是否曾想过在不打开 UI 的情况下 **创建条件格式**？你并不孤单。许多开发者需要 **创建 excel workbook** 文件并且以编程方式完成可以节省大量手动工作时间。在本教程中，我们将展示如何 **创建条件格式**、为单元格设置样式，甚至对最高值进行排名——全部使用功能强大的 Aspose.Cells .NET 库。

我们将通过一个真实案例：生成成绩表、用浅绿色高亮高分、并为前三名的成绩加上金色背景。完成后，你将了解 **如何设置单元格背景**、**如何对单元格排名**，以及 **如何使用 Aspose** 实现高级 Excel 自动化。没有冗余，只提供完整、可直接运行的代码，随时可以放入任何 C# 项目。

## 你将学到

- 使用 Aspose.Cells **创建 excel workbook**  
- 为范围填充随机数据（成绩）  
- 使用纯色 **设置单元格背景**  
- 应用基于公式的规则 **对单元格排名** 并高亮前三名  
- 将结果保存为 .xlsx 文件  

前置条件：.NET 6+（或 .NET Framework 4.6+）、Visual Studio（或任意 C# IDE），以及对 Aspose.Cells NuGet 包的引用。如果你从未使用过 Aspose，也无需担心——我们会从零开始讲解 **如何使用 Aspose**。

---

![创建条件格式示例](https://example.com/images/create-conditional-formatting.png "显示生成的 Excel 文件中条件格式的截图")

*图片 alt 文本：使用 Aspose.Cells 生成的 Excel 工作簿中的创建条件格式示例。*

## 使用 Aspose.Cells 创建 Excel Workbook 的方法

首先，你需要一个 workbook 对象来操作。Aspose.Cells 只需一行代码即可完成。

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

为什么要重命名工作表？一个清晰的名称（如 **Scores**）便于后续引用，尤其是在将文件分享给非技术用户时。

Workbook 创建完毕后，我们来为 A 列填充随机成绩。

## 填充数据 – 创建随机成绩

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

小提示：`PutValue` 会自动检测数据类型，无需手动转换为 `int`。循环从 `i = 0` 开始，但写入的是第 `i + 1` 行，因为 Excel 行号是从 1 开始，而 `Cells` 集合是从 0 开始。

## 为高分设置单元格背景

现在我们 **创建条件格式**，将所有 ≥ 80 的成绩填充为浅绿色。

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

`ForegroundColor` 属性控制填充颜色，而 `Pattern = BackgroundType.Solid` 表示使用纯色填充，而非渐变或图案。这就是基于数值阈值 **设置单元格背景** 的核心。

## 对单元格进行排名并高亮前 3 名

排名稍微复杂一些，因为需要一个公式来将每个单元格与整个范围进行比较。Aspose.Cells 允许你使用与在 UI 中输入的完全相同的 Excel 公式语法。

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

为什么公式里使用 `A2`？Aspose 会相对于范围内的每个单元格评估公式，所以 `A2` 会自动在应用规则时变为 `A3`、`A4` 等。`RANK` 函数返回指定范围内值的位置，`<=3` 部分确保只有排名前三的成绩会得到金色填充。

## 保存 Workbook

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

将 `YOUR_DIRECTORY` 替换为你的应用程序可写入的绝对或相对路径。运行该方法后，用 Excel 打开文件，你会看到：

- 任意 ≥ 80 的成绩显示浅绿色单元格  
- 前三名的成绩（即使低于 80）显示金色单元格  

这就是完整的 **创建条件格式** 流程。

---

## 完整可运行示例

下面是完整的方法代码，直接复制粘贴到控制台应用或任意 C# 类中即可使用：

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### 预期结果

打开 `Scores_ConditionalFormatting.xlsx` 时：

- 值为 **80** 或更高的单元格呈现浅绿色。  
- 三个最高的数字（即使低于 80）显示 **金色** 背景。  
- 其他单元格保持默认的白色背景。

这种视觉提示能够让管理者一眼看出顶尖表现者，无需手动排序。

---

## 常见问题与边缘情况

**如果需要显示超过三名的最高分怎么办？**  
只需将公式中的 `<=3` 改为 `<=5`（或任意你想要的数字），规则会自动适配。

**可以对多个范围应用格式吗？**  
完全可以。再次调用 `sheet.ConditionalFormattings.Add` 并传入不同的范围，然后为该新 `ConditionalFormatting` 对象添加条件即可。

**旧版 Excel 如何兼容？**  
Aspose.Cells 默认保存为现代的 `.xlsx` 格式，兼容 Excel 2007 及以上。如果需要 `.xls`，在 `Save` 方法中传入 `SaveFormat.Excel97To2003` 即可。

**大表格会有性能影响吗？**  
条件格式作为元数据存储，对文件大小影响不大。但生成数十万行数据可能会增加内存占用——建议分批处理。

---

## 后续步骤

掌握了 **如何创建条件格式** 后，你可能想进一步探索：

- **如何以编程方式创建 Excel 图表**（另一个 Aspose.Cells 的亮点）  
- **如何基于文本值（如 “Pass/Fail”）设置单元格背景**  
- **如何使用 Aspose.Cells 实现数据验证和下拉列表**  

这些主题都基于你刚学到的基础，能够帮助你快速上手更多高级功能。

---

## 小结

我们完整演示了如何使用 Aspose.Cells 在 Excel 工作簿中 **创建条件格式**：从初始化 workbook、填充数据、**设置单元格背景**、对顶尖表现者进行**排名**，直至最终保存文件，每一步都兼顾了 **如何对单元格排名** 与 **如何使用 Aspose** 的要点。  

试着运行代码，调整阈值，感受一下几乎瞬间即可生成精美报表的快感。有什么创新的思路想分享？欢迎在下方留言——祝编码愉快！

## 接下来该学习什么？

以下教程与本指南紧密相关，帮助你进一步掌握 API 功能并在项目中探索替代实现方式。

- [使用 Aspose.Cells for Java 自动化 Excel 条件格式化：完整指南](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [使用 Aspose.Cells for Java 创建并格式化 Excel 单元格：一步步指南](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [使用 Aspose.Cells for Java 创建 Excel Workbook：一步步指南](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}