---
category: general
date: 2026-03-30
description: 学习如何在 C# 中使用 WRAPCOLS 创建 Excel 工作簿、向 Excel 添加数据，并强制公式计算，同时使用 WRAPROWS。
draft: false
keywords:
- how to use wrapcols
- create excel workbook c#
- add data to excel
- force formula calculation
- how to use wraprows
language: zh
og_description: 了解如何在 C# 中使用 WRAPCOLS 构建 Excel 工作簿、添加数据、强制公式计算，并利用 WRAPROWS 实现数组公式。
og_title: 如何在 C# 中使用 WRAPCOLS – 完整指南
tags:
- Aspose.Cells
- C#
- Excel Automation
title: 如何在 C# 中使用 WRAPCOLS – 使用换行函数创建 Excel 工作簿
url: /zh/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 WRAPCOLS – 使用包装函数创建 Excel 工作簿

是否曾经想过在使用 C# 自动化 Excel 时 **如何使用 WRAPCOLS**？你并不孤单——许多开发者在需要将水平范围转换为垂直数组而不想编写大量代码时会遇到瓶颈。好消息是 Aspose.Cells 让这变得轻而易举。

在本教程中，我们将逐步演示一个完整且可运行的示例，展示 **如何使用 WRAPCOLS**、如何 **以 C# 方式创建 Excel 工作簿**、如何 **向 Excel 添加数据**，甚至如何 **强制公式计算** 以便结果立即显示。我们还会顺带介绍 **如何使用 WRAPROWS** 进行相反的转换。完成后，你将拥有一个可直接运行的程序，并清晰了解每一步的意义。

![How to use WRAPCOLS in C# example](alt="Screenshot showing Excel workbook after using WRAPCOLS in C#")

## 本指南涵盖内容

* 使用 Aspose.Cells 设置全新的工作簿。
* 以编程方式填充单元格（**add data to Excel**）。
* 应用 `WRAPCOLS` 函数将行转换为列。
* 使用 `WRAPROWS` 将列翻转回行（**how to use wraprows**）。
* 强制引擎立即评估公式（**force formula calculation**）。
* 保存文件并检查输出。

无需外部文档——所有你需要的内容都在这里。

## 如何在 C# 中使用 WRAPCOLS – 步骤实现

下面是完整的源文件。请随意将其复制粘贴到新的控制台项目中，添加 Aspose.Cells NuGet 包，然后按 **F5** 运行。

```csharp
// ------------------------------------------------------------
// How to Use WRAPCOLS in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.Cells;

namespace WrapFunctionsDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a fresh workbook (this is how we **create excel workbook c#** style)
            Workbook workbook = new Workbook();

            // 2️⃣ Grab the first worksheet – it's created by default
            Worksheet sheet = workbook.Worksheets[0];

            // 3️⃣ **Add data to Excel**: place two numbers side‑by‑side
            sheet.Cells["A1"].PutValue(1);   // first value
            sheet.Cells["B1"].PutValue(2);   // second value

            // 4️⃣ **How to use WRAPCOLS** – turn the horizontal range A1:B1 into a vertical array
            //    The second argument (1) tells WRAPCOLS to create 1 column per element.
            sheet["C1"].Formula = "WRAPCOLS(A1:B1, 1)";

            // 5️⃣ **How to use WRAPROWS** – the opposite; turn the same range into a horizontal array
            //    Here we ask for 2 rows per element, which produces a single row with both values.
            sheet["C2"].Formula = "WRAPROWS(A1:B1, 2)";

            // 6️⃣ **Force formula calculation** so the workbook reflects the results immediately
            workbook.CalculateFormula();

            // 7️⃣ Save the workbook to disk – change the path to a folder you own
            string outputPath = @"WrapFunctions.xlsx";
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
            Console.WriteLine("Check cells C1 and C2 for the WRAPCOLS / WRAPROWS results.");
        }
    }
}
```

### 每行代码的意义

| 步骤 | 说明 |
|------|-------------|
| **1️⃣ 创建全新的工作簿** | 这是基础。Aspose.Cells 将 `Workbook` 对象视为整个 Excel 文件，因此你实际上是在 **以 C# 方式创建 Excel 工作簿**。 |
| **2️⃣ 获取第一个工作表** | 新工作簿始终至少包含一个工作表（`Worksheets[0]`）。提前访问可避免空引用异常。 |
| **3️⃣ 向 Excel 添加数据** | 通过使用 `PutValue`，我们 **add data to Excel** 而无需担心单元格格式。数字 `1` 和 `2` 是我们用于包装函数的测试数据。 |
| **4️⃣ 如何使用 WRAPCOLS** | `WRAPCOLS(A1:B1, 1)` 告诉 Excel 将范围 `A1:B1` 的值垂直展开，每行一个。结果放在 `C1` 并向下展开（`C1`、`C2`、…）。 |
| **5️⃣ 如何使用 WRAPROWS** | `WRAPROWS(A1:B1, 2)` 则相反：它创建水平展开，将两个值放入从 `C2` 开始的单行中。 |
| **6️⃣ 强制公式计算** | 默认情况下，Aspose.Cells 可能会延迟计算，直到在 Excel 中打开文件。调用 `CalculateFormula()` **forces formula calculation**，因此你可以在保存后立即读取结果。 |
| **7️⃣ 保存工作簿** | 最后一步将所有内容写入磁盘。打开生成的 `WrapFunctions.xlsx` 查看结果。 |

## 创建 Excel 工作簿 C# – 环境设置

在运行代码之前，请确保你拥有正确的工具：

1. **.NET 6.0+** – 最新的 LTS 版本效果最佳。
2. **Visual Studio 2022**（或带 C# 扩展的 VS Code）。
3. **Aspose.Cells for .NET** – 通过 NuGet 安装：  
   ```bash
   dotnet add package Aspose.Cells
   ```
4. 用于输出文件的可写文件夹。

这些前置条件很少；不需要 COM 互操作或 Office 安装，这也是 Aspose.Cells 成为服务器端 Excel 生成的热门选择的原因。

## 向 Excel 添加数据 – 最佳实践

在以编程方式 **add data to Excel** 时，请考虑以下提示：

* **使用 `PutValue`** 来写入原始数字或字符串；它会自动检测数据类型。
* **避免在大型项目中硬编码单元格地址**——使用循环或命名范围以实现可扩展性。
* **谨慎设置单元格样式**；每次样式更改都会产生开销。如果需要格式化，请创建单个样式对象并将其应用于多个单元格。

在我们的简短示例中仅插入了两个数字，但相同的模式可以扩展到数千行。

## 如何使用 WRAPROWS – 水平数组示例

如果你需要 `WRAPCOLS` 的相反操作，`WRAPROWS` 是你的首选。语法如下：

```
WRAPROWS(source_range, [rows_per_item])
```

* `source_range` – 你想要转换的范围。
* `rows_per_item` – 可选；告诉 Excel 每个元素占用多少行。在我们的演示中使用 `2` 将两个值强制放在同一行上。

你可以通过更改第二个参数进行实验：

```csharp
// Example: split each value into its own column, three rows per item
sheet["D1"].Formula = "WRAPROWS(A1:B1, 3)";
```

打开工作簿，你会看到值跨越三列展开，每列包含原始数字，按需重复。

## 强制公式计算 – 何时以及为何

你可能会想，‘我真的需要调用 `CalculateFormula()` 吗？’答案是 **是**，如果：

* 你计划在保存后 **programmatically** 读取计算后的值。
* 你希望确保文件在 Excel 中打开时已显示正确的结果。
* 你在 **headless environment**（例如 Web API）中运行，且没有用户手动触发重新计算。

跳过此步骤不会破坏工作簿，但单元格会显示公式文本（`=WRAPCOLS(...)`），而不是计算值，直到 Excel 重新计算。

## 预期输出 – 查看结果

运行程序并打开 `WrapFunctions.xlsx` 后：

| 单元格 | 公式 | 显示值 |
|------|---------|-----------------|
| **C1** | `=WRAPCOLS(A1:B1, 1)` | `1`（在 C1）和 `2`（在 C2）– 垂直列表 |
| **C2** | `=WRAPROWS(A1:B1, 2)` | `1` 在 C2，`2` 在 D2 – 水平列表 |

因此你会看到从 **C1** 开始的一列值，以及从 **C2** 开始的一行值。这确认了两个 wrap 函数均按预期工作。

## 边缘情况与变体

| 场景 | 有什么变化？ | 建议的调整 |
|----------|---------------|-----------------|
| **大范围 (A1:Z1)** | 更多值需要垂直展开 | 如果希望每组有多列，可增加 `WRAPCOLS` 的第二个参数。 |
| **非数值数据** | 字符串以相同方式处理 | 无需代码更改；`PutValue` 接受任何对象。 |
| **动态范围** | 编译时不知道大小 | 使用 `sheet.Cells.MaxDataColumn` 和 `MaxDataRow` 构建地址字符串。 |
| **多个工作表** | 需要在不同工作表上应用 wrap 函数 | 引用正确的工作表（`workbook.Worksheets["Sheet2"]`）。 |

## 实战技巧

* **Pro tip:** 如果你的目标是 .NET Core 3.1+，请在 `using` 块中包装工作簿创建，以确保及时释放所有资源。
* **Watch out for:** 在大范围内设置相同公式而不调用 `CalculateFormula()` 可能导致性能瓶颈。尽可能批量处理公式。
* **Tip:** 如果需要在代码中读取计算后的值，请调用 `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}