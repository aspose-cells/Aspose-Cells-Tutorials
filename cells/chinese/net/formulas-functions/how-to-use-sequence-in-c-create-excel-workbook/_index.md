---
category: general
date: 2026-07-03
description: 如何在 C# 中使用 SEQUENCE 生成 Excel 中的递增数字。学习使用 C# 创建 Excel 工作簿，以及在 ASP.NET
  中仅用几行代码创建 Excel 文件。
draft: false
keywords:
- how to use sequence
- create excel workbook c#
- asp.net create excel file
- generate incremental numbers excel
language: zh
og_description: 如何在 C# 中使用 SEQUENCE 在 Excel 中生成递增数字。逐步指南，使用 C# 和 ASP.NET 创建 Excel
  工作簿并生成 Excel 文件。
og_title: 如何在 C# 中使用 SEQUENCE – 创建 Excel 工作簿
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  headline: How to Use SEQUENCE in C# – Create Excel Workbook
  type: TechArticle
- description: How to use SEQUENCE in C# to generate incremental numbers in Excel.
    Learn to create Excel workbook C# and ASP.NET create Excel file with a few lines
    of code.
  name: How to Use SEQUENCE in C# – Create Excel Workbook
  steps:
  - name: Why Use SEQUENCE Instead of a Loop?
    text: '- **Performance** – Excel does the math on its own engine, which is highly
      optimized. - **Maintainability** – The formula is self‑documenting; anyone opening
      the sheet instantly knows the intent. - **Dynamic resizing** – Change the `rows`
      argument and the spill range expands automatically.'
  - name: Pro Tip
    text: 'If you need the workbook in memory (e.g., to send it over a web API), use
      a `MemoryStream`:'
  - name: What If the Client Uses an Older Excel Version?
    text: 'Dynamic arrays (including `SEQUENCE`) were introduced in Excel 365/2019.
      If you need backward compatibility, fall back to a manual fill:'
  type: HowTo
- questions:
  - answer: No. `SEQUENCE` is a non‑iterative function; a simple `CalculateFormula()`
      call is enough.
    question: Do I need to enable iterative calculation?
  - answer: 'Change the second argument: `=SEQUENCE(1,5,10,2)` spills across B1:F1.'
    question: What if I want a horizontal spill?
  - answer: Absolutely. For example, `=INDEX(A:A, SEQUENCE(5,1,10,2))` can pull rows
      from another column.
    question: Can I combine SEQUENCE with other functions?
  - answer: The file size impact of a formula is negligible. Only when you start populating
      millions of cells manually does size become an issue.
    question: Is the workbook size a concern?
  type: FAQPage
tags:
- C#
- Excel
- Aspose.Cells
- ASP.NET
title: 如何在 C# 中使用 SEQUENCE – 创建 Excel 工作簿
url: /zh/net/formulas-functions/how-to-use-sequence-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中使用 SEQUENCE – 创建 Excel 工作簿

有没有想过 **how to use SEQUENCE**（如何使用 SEQUENCE）从 C# 在 Excel 表格中输出一系列数字？你并不是唯一的。无论是构建报表仪表盘、为数据网格提供数据，还是仅仅需要快速生成 ID，掌握这个技巧可以让你免去编写循环的麻烦。

在本教程中，我们将 **create an Excel workbook in C#**，在单元格 A1 中插入 `SEQUENCE` 动态数组公式，最终得到一列递增的数字。我们还会展示如何在 ASP.NET 控制器中提供该文件——是的，**ASP.NET create Excel file** 也会涉及。完成后，你将能够用一行代码 **generate incremental numbers Excel**。

## 你需要的条件

- .NET 6+（代码同样适用于 .NET Framework 4.6+）  
- **Aspose.Cells for .NET** NuGet 包（或任何提供 `Workbook`/`Worksheet` 对象的库）  
- 如果想尝试网页下载部分，需要一个基本的 ASP.NET Core 或 MVC 项目  

就这么简单。无需额外的 COM 互操作，也不需要安装 Office。

---

## 如何使用 SEQUENCE 生成递增数字

Excel 的 `SEQUENCE(rows, [columns], [start], [step])` 函数返回一个 **spill**（溢出）范围。我们这里需要 5 行、1 列、起始值 10、步长 2。公式如下：

```excel
=SEQUENCE(5,1,10,2)
```

当 Excel 计算该公式时，单元格 A1:A5 将包含 **10, 12, 14, 16, 18**。妙处在于我们无需编写任何 C# 循环——公式已经完成了繁重的工作。

下面是完整的 C# 代码片段，用于创建工作簿、插入公式、强制计算并保存文件。

```csharp
using Aspose.Cells;
using System.IO;

// 1️⃣ Create a new workbook
Workbook workbook = new Workbook();

// 2️⃣ Grab the first worksheet (Aspose creates one by default)
Worksheet sheet = workbook.Worksheets[0];

// 3️⃣ Insert the SEQUENCE formula – this will spill a 5‑row column starting at 10, step 2
sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";

// 4️⃣ Force calculation so the spilled range is materialized
workbook.CalculateFormula();

// 5️⃣ Save to disk (you can change the path as needed)
workbook.Save("DynamicArray.xlsx");
```

**Expected output** – 打开 *DynamicArray.xlsx*，你会看到：

| A |
|---|
| 10 |
| 12 |
| 14 |
| 16 |
| 18 |

这就是在 C# 中 **how to use sequence**（如何使用 sequence）的全部内容。很简单，对吧？但我们再深入一点。

### 为什么使用 SEQUENCE 而不是循环？

- **Performance** – Excel 在其自身引擎上进行计算，性能高度优化。  
- **Maintainability** – 该公式自解释；任何打开工作表的人都能立刻了解意图。  
- **Dynamic resizing** – 更改 `rows` 参数后，溢出范围会自动扩展。

---

## 创建 Excel 工作簿 C# – 步骤详解

如果你是 **create excel workbook c#**（创建 Excel 工作簿 C#）的新手，下面的检查清单可以帮助你避免常见的陷阱。

1. **Add the Aspose.Cells package**  
   ```bash
   dotnet add package Aspose.Cells
   ```
   （你也可以使用 ClosedXML 或 EPPlus，但这里展示的 API 与上面的代码相匹配。）
2. **Set a license**（可选，仅用于试用）。  
   ```csharp
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Total.NET.lic");
   ```
3. **Instantiate `Workbook`** – 这将为你提供一个全新的空工作簿。
4. **Reference the worksheet** – `workbook.Worksheets[0]` 是默认的名为 *Sheet1* 的工作表。
5. **Apply the SEQUENCE formula** – 如前所示。
6. **Calculate** – `workbook.CalculateFormula()` 强制计算溢出；否则文件中只会包含公式。
7. **Save** – 你可以保存到磁盘、`MemoryStream`，或直接写入 HTTP 响应。

### 小技巧

如果需要在内存中处理工作簿（例如，通过 Web API 发送），可以使用 `MemoryStream`：

```csharp
using var ms = new MemoryStream();
workbook.Save(ms, SaveFormat.Xlsx);
byte[] excelBytes = ms.ToArray(); // ready to return or attach
```

---

## ASP.NET 创建 Excel 文件 – 流式传输到浏览器

既然我们已经了解 **create excel workbook c#**，现在把它集成到 ASP.NET Core 控制器中，让用户能够即时下载文件。

```csharp
using Aspose.Cells;
using Microsoft.AspNetCore.Mvc;
using System.IO;

[Route("api/[controller]")]
public class ExcelController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        // 1️⃣ Build the workbook (same steps as before)
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=SEQUENCE(5,1,10,2)";
        workbook.CalculateFormula();

        // 2️⃣ Save to a memory stream
        using var ms = new MemoryStream();
        workbook.Save(ms, SaveFormat.Xlsx);
        ms.Position = 0; // reset stream position

        // 3️⃣ Return the file as a download
        const string fileName = "DynamicArray.xlsx";
        return File(ms, 
                    "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", 
                    fileName);
    }
}
```

当用户访问 `/api/excel/download` 时，浏览器会提示下载 *DynamicArray.xlsx*。该文件已经通过 `SEQUENCE` 公式包含了 **generated incremental numbers excel** 列。

### 如果客户端使用较旧的 Excel 版本怎么办？

动态数组（包括 `SEQUENCE`）在 Excel 365/2019 中引入。如果需要向后兼容，请回退到手动填充：

```csharp
// Alternative for older Excel: write numbers directly
for (int i = 0; i < 5; i++)
{
    sheet.Cells[i, 0].PutValue(10 + i * 2); // column 0 = A
}
```

该代码片段展示了经典的 **generate incremental numbers excel**（生成递增数字 Excel）方法，无需依赖新函数。

---

## 常见问题与边缘情况

- **Do I need to enable iterative calculation?**  
  不需要。`SEQUENCE` 是非迭代函数，只需一次 `CalculateFormula()` 调用即可。
- **What if I want a horizontal spill?**  
  更改第二个参数：`=SEQUENCE(1,5,10,2)` 会在 B1:F1 横向溢出。
- **Can I combine SEQUENCE with other functions?**  
  当然可以。例如，`=INDEX(A:A, SEQUENCE(5,1,10,2))` 可以从另一列提取行。
- **Is the workbook size a concern?**  
  公式对文件大小的影响可以忽略不计。只有在手动填充数百万单元格时，文件大小才会成为问题。

---

## 结论

我们已经演示了在 C# 中 **how to use sequence**（如何使用 sequence）来 **create excel workbook c#**（创建 Excel 工作簿 C#），并通过 **ASP.NET create excel file**（ASP.NET 创建 Excel 文件）提供该工作簿，展示了无需编写循环即可 **generate incremental numbers excel**（生成递增数字 Excel）的简洁方法。关键点是：让 Excel 自己的动态数组引擎完成计数，让你的 .NET 代码专注于编排。

欢迎自行实验——更改 `rows`、`start` 或 `step` 参数，横向溢出，或将公式与 `IF`、`FILTER` 结合以生成更复杂的报表。当你准备好时，可以尝试将多个工作表串联，或将工作簿导出为 CSV 供下游系统使用。

有想分享的技巧吗？在下方留言，或在 GitHub 上联系我。祝编码愉快！

## 接下来你应该学习什么？

以下教程涵盖与本指南紧密相关的主题，基于所示技术进行扩展。每篇资源都包含完整的可运行代码示例和逐步解释，帮助你掌握更多 API 功能并在项目中探索替代实现方式。

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)
- [How to Create and Style Excel Workbooks Using Aspose.Cells for .NET (2023 Guide)](/cells/english/net/formatting/create-style-excel-workbooks-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}