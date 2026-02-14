---
category: general
date: 2026-02-14
description: 快速创建折扣模板，并学习如何在电子表格中应用折扣、将数据注入模板，以及为智能标记定义变量前缀。
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: zh
og_description: 使用 C# 创建折扣模板。学习在电子表格中应用折扣、将数据注入模板，并为智能标记定义变量前缀。
og_title: 创建折扣模板 – 完整 C# 教程
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: 在 C# 中创建折扣模板 – 步骤指南
url: /zh/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 创建折扣模板 – 完整 C# 演练

是否曾经需要为销售报告 **创建折扣模板**，却不确定如何自动将数字填入电子表格？你并不孤单。在本教程中，我们将准确演示如何 **创建折扣模板**，随后 **在电子表格中应用折扣**，**向模板注入数据**，甚至 **为智能标记定义变量前缀**——全部使用简洁的 C# 代码。

我们将先概述问题，然后直接跳到可复制粘贴的可运行方案。完成后，你将拥有一个可复用的模式，无论是生成发票、价目表，还是任何需要动态折扣的电子表格，都能轻松应对。

---

## 你将学到

- 如何设计支持折扣的电子表格模板。
- 如何配置自定义的 `VariablePrefix` / `VariableSuffix`，让标记易于辨识。
- 如何将匿名对象 (`discountData`) 传递给 `SmartMarkerProcessor`。
- 结果公式 (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) 如何自动计算最终价格。
- 处理零折扣行或多层折扣等边缘情况的技巧。

**先决条件** – 最近的 .NET 运行时（≥ .NET 6），以及对提供 `SmartMarkerProcessor` 的 `Aspose.Cells`（或类似）库的引用，且具备基本的 C# 语法了解。没有其他特殊要求。

---

## 步骤 1：在电子表格中创建折扣模板

首先，打开一个新工作簿（或使用已有工作簿），在需要应用折扣的地方放置占位符。把模板想象成一个普通的 Excel 文件，其中包含处理器将要替换的“智能标记”。

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**为什么重要：** 在公式中嵌入 `#Discount#`，我们告诉处理器折扣值应放置的位置。`SmartMarkerProcessor` 会在后续将 `#Discount#` 替换为你提供的数值，而公式的其余部分保持不变。

---

## 步骤 2：为智能标记定义变量前缀

开箱即用时，许多库会寻找 `${Variable}` 或 `{{Variable}}`。在本例中，我们希望使用简洁、易读的标记，因此 **显式定义变量前缀** 和后缀。

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**小技巧：** 使用 `#` 可以让标记在 Excel 公式栏中既短小又显眼。如果需要避免与现有 Excel 函数冲突，可改用其他配对（例如 `[[` 和 `]]`）。

---

## 步骤 3：使用 SmartMarkerProcessor 向模板注入数据

现在我们将实际的折扣值传入。处理器会扫描工作表，找到每个 `#Discount#`，并用匿名对象中提供的值替换它。

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

调用之后，`B2` 单元格中的公式变为：

```
=IF(0.1>0, A2*(1-0.1), A2)
```

当工作簿计算时，`B2` 显示 **90**，即在原价 100 上应用了 10 % 的折扣。

**工作原理：** `StartSmartMarkerProcessing` 会遍历每个单元格，查找 `#Discount#` 标记并替换为数值。由于标记位于 `IF` 语句内部，电子表格仍能处理折扣为零的情况。

---

## 步骤 4：在电子表格中应用折扣 – 验证结果

让我们触发计算并将最终价格输出到控制台。此步骤证明 **在电子表格中应用折扣** 的工作流已成功。

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**预期输出**

```
Original: 100
Discounted (10%): 90
```

如果将 `discountData.Discount` 改为 `0.25` 并重新运行处理器，输出将自动反映 25 % 的折扣——无需额外代码。

---

## 步骤 5：处理边缘情况与多重折扣

### 零折扣行

有时商品并未打折。为了让公式更健壮，之前放置的 `IF` 已经覆盖了这种情形：当 `#Discount#` 为 `0` 时，原价保持不变。

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### 多重折扣列

如果需要为每行提供独立的折扣，可为每行使用不同的标记，例如 `#Discount1#`、`#Discount2#`，并传入集合：

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

处理器按顺序匹配标记，因此每行都会得到对应的数值。

---

## 完整可运行示例

下面是完整的、可直接复制的程序，囊括上述所有步骤。将其保存为 `Program.cs`，添加对 `Aspose.Cells` 的引用后运行。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

运行后会打印出预期的数字，并生成 `DiscountedPricing.xlsx` 文件，你可以在 Excel 中打开，看到公式已经被解析。

---

## 结论

现在你已经掌握了 **创建折扣模板**、**在电子表格中应用折扣**、**向模板注入数据**，以及 **为智能标记定义变量前缀** 的完整流程——全部只需几行简洁的 C# 代码。该模式具备可扩展性——只需更改匿名对象或传入集合进行批量更新，同一模板即可应对任何折扣场景。

准备好进阶了吗？尝试以下方向：

- 在折扣的同时加入税费计算。
- 从数据库读取折扣百分比，而不是硬编码。
- 使用条件格式突出显示高折扣行。

这些扩展保持核心思路不变，同时提升折扣模板的实用价值。

有问题或想分享酷炫用例？在下方留言，祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}