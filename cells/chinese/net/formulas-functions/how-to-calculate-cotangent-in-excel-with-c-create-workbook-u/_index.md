---
category: general
date: 2026-05-04
description: 如何在 C# 中创建 Excel 工作簿时计算余切。学习如何使用 EXPAND 函数、保存工作簿以及自动化计算。
draft: false
keywords:
- how to calculate cotangent
- create excel workbook
- how to use expand
- how to save workbook
- use expand function
language: zh
og_description: 如何在 Excel 中使用 C# 计算余切。本教程展示了如何创建 Excel 工作簿、使用 EXPAND 并保存文件。
og_title: 如何在Excel中计算余切 – 完整的C#工作簿指南
tags:
- C#
- Aspose.Cells
- Excel Automation
title: 如何使用 C# 在 Excel 中计算余切 – 创建工作簿、使用 EXPAND 并保存
url: /zh/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中使用 C# 计算余切 – 完整指南

是否曾想过 **如何直接在 C# 生成的 Excel 文件中计算余切**？也许你在构建金融模型、科学报告，或只是想自动化一项枯燥的电子表格任务。好消息是——只需几行代码即可实现，无需手动公式，也不必复制粘贴。

在本教程中，我们将逐步演示如何创建 Excel 工作簿、使用 **EXPAND** 函数展开数组、插入 **COT** 公式计算 45° 的余切，最后保存文件，以便在 Excel 中打开查看结果。过程中我们还会涉及 **如何使用 expand**、**如何保存工作簿**，以及一些常被忽视的实用技巧。

> **快速答案：** 使用 Aspose.Cells（或 Microsoft Interop）创建工作簿，设置 `ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"`，设置 `ws.Cells["B1"].Formula = "=COT(PI()/4)"`，然后调用 `workbook.Save("output.xlsx")`。

---

## 你需要准备的东西

- **.NET 6+**（或任意近期的 .NET 运行时）。  
- **Aspose.Cells for .NET**（免费试用版或正式授权版）。  
- 基本的 C# 语法了解。  
- Visual Studio、Rider，或你喜欢的任何编辑器。

不需要额外的 Excel 插件；所有操作均在服务器端完成，生成的文件可在任何近期版本的 Excel 中使用。

---

## 第一步：从 C# 创建 Excel 工作簿  

创建工作簿是基础。可以把它想象成在开始写作前打开一本全新的笔记本。

```csharp
using Aspose.Cells;

// Step 1: Initialize a new workbook object
Workbook workbook = new Workbook();               // Empty workbook
Worksheet ws = workbook.Worksheets[0];            // Grab the first sheet
```

**为什么这很重要：**  
`Workbook` 代表整个 `.xlsx` 包。默认情况下它包含一个工作表，我们通过 `Worksheets[0]` 访问。如果以后需要更多工作表，可以使用 `workbook.Worksheets.Add()` 添加。

> **专业提示：** 如果你面向 .NET Core，确保 Aspose.Cells NuGet 包与运行时匹配，以免缺少本机依赖。

---

## 第二步：使用 EXPAND 函数填充列  

**EXPAND** 函数是 Excel 将静态数组转换为动态范围的方式。当你想生成一列数值而不手动为每个单元格编写时，它非常适用。

```csharp
// Step 2: Write an EXPAND formula in cell A1
ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // Expands to a 5‑row column
```

### 工作原理  

- `{1,2,3}` 是源数组（三个数字）。  
- `5` 告诉 Excel 生成 **5 行**。  
- `1` 告诉 Excel 生成 **1 列**。  

打开保存后的文件时，单元格 A1 到 A5 将依次显示 `1, 2, 3, 0, 0`（多余的行会用零填充）。

**边界情况：** 如果 `rows` 参数小于源数组长度，Excel 会截断数组。因此 `=EXPAND({1,2,3},2,1)` 只会显示 `1` 和 `2`。

---

## 第三步：插入 COT 公式计算余切  

现在进入重点：**如何在 Excel 中计算余切**。`COT` 函数接受弧度制的角度值，所以我们传入 `PI()/4`（相当于 45°）。

```csharp
// Step 3: Write a COT formula in cell B1
ws.Cells["B1"].Formula = "=COT(PI()/4)"; // Returns 1
```

### 为什么使用 COT 而不是 TAN？

余切是正切的倒数（`cot = 1 / tan`）。虽然可以写成 `=1/TAN(PI()/4)`，但使用 `COT` 更简洁，并且在角度为 0° 或 180° 时可以避免除以零的错误。

**预期输出：** 打开 `output.xlsx` 时，B1 单元格会显示 `1`，因为 45°（π/4 弧度）的余切等于 1。

**如果需要角度制怎么办？**  
Excel 的三角函数使用弧度。可以使用 `RADIANS(deg)` 将度数转换为弧度。例如：`=COT(RADIANS(60))`。

---

## 第四步：保存工作簿以查看结果  

保存是最后一步。你可以将文件写入任意有写权限的文件夹。

```csharp
// Step 4: Persist the workbook to disk
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "output.xlsx");

// Save the workbook (the default format is .xlsx)
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### 不同格式的保存方式  

- **XLS** – `workbook.Save("output.xls", SaveFormat.Excel97To2003);`  
- **CSV** – `workbook.Save("output.csv", SaveFormat.CSV);`  

如果需要将文件以流的形式返回（例如 Web API），使用 `workbook.Save(stream, SaveFormat.Xlsx)`。

---

## 完整可运行示例  

下面把所有步骤整合在一起，提供一个可以直接复制到控制台应用的完整程序。

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Expand an array {1,2,3} into a 5‑row column starting at A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // 3️⃣ Calculate cotangent of 45° (π/4) in B1
        ws.Cells["B1"].Formula = "=COT(PI()/4)";

        // 4️⃣ Define where to save the file (Desktop for easy access)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        // 5️⃣ Save the workbook
        workbook.Save(outputPath);
        Console.WriteLine($"✅ Workbook saved at: {outputPath}");
    }
}
```

**结果验证：**  
- 打开 `output.xlsx`。  
- A 列应显示 `1, 2, 3, 0, 0`。  
- B1 单元格应显示 `1`。  

如果看到这些数值，说明你已经成功掌握了 **如何以编程方式计算余切**，以及 **如何创建 Excel 工作簿**、**使用 expand 函数**、**保存工作簿**——一次性全部搞定。

---

## 常见问题与坑点  

### `COT` 在旧版 Excel 中可用吗？  
可以，`COT` 自 Excel 2007 起就已存在。如果你面向 Excel 2003（`.xls`），需要改用 `1/TAN(...)`，因为当时没有 `COT` 函数。

### 公式没有自动重新计算怎么办？  
Aspose.Cells 默认惰性计算公式。若需要在保存前将计算结果写入文件，请在保存前调用 `workbook.CalculateFormula()`。

```csharp
workbook.CalculateFormula();
workbook.Save(outputPath);
```

### 能直接写入结果而不使用公式吗？  
可以，在 C# 中计算后赋值，例如 `Math.Cos(Math.PI / 4) / Math.Sin(Math.PI / 4)`，然后 `ws.Cells["B1"].Value = result;`。本教程侧重于 Excel 公式，因为它们保持动态——以后修改角度时会自动更新。

---

## 实战项目的专业技巧  

- **批量操作：** 若要填充数千行，写入时先关闭计算 (`workbook.Settings.CalculateFormulaOnOpen = false`)，写完后再开启。  
- **命名范围：** 使用 `ws.Cells.CreateRange("MyArray", "A1:A5")`，在公式中引用名称，可提升可读性。  
- **错误处理：** 将 `workbook.Save` 包裹在 try/catch 中，以捕获权限异常 (`UnauthorizedAccessException`)。

---

## 结论  

我们已经完整演示了 **如何在 C# 生成的 Excel 表中计算余切**，展示了 **如何使用 expand** 填充列，并说明了 **如何保存工作簿** 以便立即检查。上面的可运行示例为你提供了自动化任何混合静态数据与三角函数计算的电子表格的坚实基础。

下一步可以尝试将 `COT` 公式中的角度改为引用单元格（`=COT(PI()*A1/180)`），让用户自行输入度数。或者探索 `SIN`、`COS`、`ATAN2` 等其他数学函数——它们在生成的工作簿中同样适用。

祝编码愉快，愿你的电子表格永远无错！ 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}