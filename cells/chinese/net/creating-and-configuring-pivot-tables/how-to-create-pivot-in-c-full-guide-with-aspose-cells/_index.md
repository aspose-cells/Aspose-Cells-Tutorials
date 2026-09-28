---
category: general
date: 2026-03-27
description: 如何在 C# 中使用 Aspose.Cells 创建数据透视表——学习添加数据、启用刷新，并在单个教程中将工作簿保存为 xlsx。
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: zh
og_description: 如何在 C# 中使用 Aspose.Cells 创建数据透视表。本指南展示了如何添加数据、启用刷新以及将工作簿保存为 xlsx。
og_title: 如何在 C# 中创建透视表 – 完整的 Aspose.Cells 教程
tags:
- Aspose.Cells
- C#
- Excel automation
title: 如何在 C# 中创建数据透视表 – 使用 Aspose.Cells 的完整指南
url: /zh/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 C# 中创建数据透视表 – 完整 Aspose.Cells 教程

是否曾想过在 C# 中 **如何创建数据透视表** 而不必与 COM 互操作纠缠？你并非唯一有此需求的人。在许多数据驱动的应用中，我们需要一种快速方式将原始销售数据转化为整洁的汇总，而 Aspose.Cells 让这变得轻而易举。  

在本教程中，我们将逐步演示：添加数据、构建数据透视表、启用自动刷新，最后 **将工作簿保存为 xlsx**，让用户能够立即在 Excel 中打开。完成后，你将拥有一个可直接使用的 `PivotRefresh.xlsx` 文件，并对每行代码的意义有深入了解。

## 前置条件

- .NET 6+（或 .NET Framework 4.7.2 及更高版本）– 任意近期运行时均可。  
- Aspose.Cells for .NET – 可通过 NuGet 获取 (`Install-Package Aspose.Cells`)。  
- 对 C# 语法有基本了解 – 不需要深入的 Excel 知识。  

> **专业提示：** 如果你使用的是公司机器，请确保已应用 Aspose 许可证；否则生成的文件会出现水印。

## 第 1 步 – 如何向新工作簿添加数据

在创建数据透视表之前，需要有源表。我们将创建一个全新的工作簿，将第一个工作表命名为 *SalesData*，并添加几行数据，模拟真实的销售记录。

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**为什么这很重要：**  
- 使用 `PutValue` 会自动设置单元格类型，后续无需担心字符串与数值类型不匹配。  
- 在第 1 行定义标题，可为数据透视引擎提供映射字段的依据。  

## 第 2 步 – 创建用于放置数据透视表的工作表

数据透视表位于独立的工作表上，保持源数据整洁，报表有序。

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **如果已经有工作表怎么办？** 只需通过索引引用它（`workbook.Worksheets["MySheet"]`），而不是新增工作表。

## 第 3 步 – 定义源范围（如何添加数据 → 定义范围）

Aspose.Cells 需要一个包含标题和数据的 `CellArea` 或范围字符串。这里假设最多 100 行；可根据实际情况调整。

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**边缘情况：** 如果数据集是动态的，可以使用 `salesDataSheet.Cells.MaxDataRow` 计算最后使用的行号，并相应构建范围。

## 第 4 步 – 如何创建数据透视表 – 插入数据透视表

现在进入有趣的部分：我们让 Aspose.Cells 创建一个关联到刚才定义范围的数据透视表。

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

请注意公式式引用（`=SalesData!A1:D100`），这与在 Excel 中输入的语法相同，使 API 更直观。

## 第 5 步 – 配置行、列和数据字段（如何添加数据 → 字段）

我们将在行上放置 *Region*，列上放置 *Product*，并对 *Units* 与 *Revenue* 进行求和。

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**为什么使用这些索引？**  
Aspose.Cells 的列索引从 0 开始，因此 `0` 对应 *Region*。`DataFields.Add` 方法允许你重命名字段（例如 “Sum of Units”）并选择聚合类型——`Sum` 是数值数据最常用的聚合方式。

## 第 6 步 – 如何启用刷新 – 让数据透视表在打开时自动更新

如果源数据随后发生变化，你可能希望数据透视表自动反映这些更改。这时 `RefreshDataOnOpen` 就派上用场了。

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **注意：** 此标志仅在工作簿使用 Excel 打开时生效；在 Aspose.Cells 内部不会重新计算，除非手动调用 `pivotTable.RefreshData()`。

## 第 7 步 – 将工作簿保存为 XLSX（如何将工作簿保存为 XLSX）

最后，我们将文件保存到磁盘。`.xlsx` 格式是现代的基于 zip 的 Excel 文件类型，兼容性极好。

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

运行程序后会在执行文件夹生成名为 **PivotRefresh.xlsx** 的文件。用 Excel 打开后，你会看到一个布局整齐的数据透视表，行是 *Region*，列是 *Product*，并对 *Units* 与 *Revenue* 进行求和。由于我们已启用刷新，对 *SalesData* 工作表的任何编辑都会在下次打开工作簿时自动更新数据透视表。

### 预期输出

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*（数字会根据你添加的行而变化。）*

---

## 常见问题与变体

### 如果需要多个数据透视表怎么办？

你可以使用不同的名称和位置重复 **第 4 步**。每次调用 `PivotTables.Add` 都会返回一个新的索引，可用于获取相应的表对象。

### 如何将聚合方式改为 *Average*（平均）而不是 *Sum*（求和）？

在 `DataFields.Add` 调用中，将 `PivotTableDataAggregationType.Sum` 替换为 `PivotTableDataAggregationType.Average`。

### 能否为数据透视表设置样式（字体、颜色）？

可以。创建数据透视表后，你可以访问其 `Style` 属性，或对包含数据透视表的范围应用单元格格式。例如：

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### 保存工作簿后还能添加更多行吗？

完全可以。使用 `new Workbook("PivotRefresh.xlsx")` 加载文件，在 *SalesData* 工作表中追加行，然后在再次保存前调用 `pivotTable.RefreshData()`。

---

## 完整可运行示例（复制粘贴即用）

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

保存文件，运行程序，然后打开生成的 **PivotRefresh.xlsx** —— 你已经掌握了在 C# 中 **如何创建数据透视表**。

---

## 总结

我们已经介绍了使用 Aspose.Cells 以编程方式 **创建数据透视表**、**添加数据**、**启用刷新**，以及最终 **将工作簿保存为 xlsx** 的方法。代码

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}