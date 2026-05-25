---
category: general
date: 2026-03-18
description: 学习如何使用 C# 在工作表中实现交替行颜色。包括设置行背景颜色、添加淡黄色背景以及交替着色行。
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: zh
og_description: 在 C# 中使用交替行颜色以提高可读性。本指南展示如何设置行背景颜色、添加淡黄色背景以及交替为行着色。
og_title: 在 C# 中应用交替行颜色 – 完整教程
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: 在 C# 中应用交替行颜色 – 步骤指南
url: /zh/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中应用交替行颜色 – 完整教程

是否曾经需要**应用交替行颜色**到数据驱动的工作表，但不确定从何入手？你并不是唯一遇到这种情况的人——大多数开发者在首次尝试让表格看起来更友好时都会卡住。好消息是，只需几行 C# 代码，你就可以**设置行背景颜色**，再**添加浅黄色背景**，从而得到一个即刻提升可读性的精致网格。

在本教程中，我们将完整演示整个过程，从将 `DataTable` 拉入内存到为每行添加细腻的黄白相间条纹。完成后，你将能够自信地**交替着色行**，并且还能看到一些实用的变体，以便在需要不同色调或动态主题时使用。

## 所需条件

- 一个目标为 .NET 6 或更高版本的 .NET 项目（代码同样适用于 .NET Framework 4.7+）。  
- 一个支持样式对象的电子表格库——示例使用了一个通用的 `Workbook`/`Worksheet` API，类似于 **Aspose.Cells**、**GemBox.Spreadsheet** 或 **ClosedXML**。  
- 一个 `DataTable` 数据源——可以来自数据库查询、CSV 导入或任何内存集合。  

不需要除电子表格库之外的额外 NuGet 包。如果使用 Aspose.Cells，命名空间为 `Aspose.Cells`；使用 ClosedXML 时为 `ClosedXML.Excel`。相应地替换 `CreateStyle` 和 `ImportDataTable` 调用即可。

## 步骤 1：将源数据检索为 DataTable

首先——获取你想要显示的数据。在实际应用中这通常意味着访问数据库，但为便于说明，我们将使用一个名为 `GetData()` 的辅助方法来返回已填充的 `DataTable`。

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **为什么这很重要：** `DataTable` 定义了随后会被交替着色的行和列。如果表为空，则没有任何内容可供样式化，因此在继续之前务必确认 `Rows.Count` > 0。

### 专业提示
如果你从 Entity Framework 拉取数据，可以在执行 `SqlCommand` 后使用 `DataTable.Load(reader)`。这样可以保持代码整洁，避免手动定义列。

## 步骤 2：分配一个数组以保存每行的样式

接下来，我们需要一个与行数匹配的容器。大多数电子表格 API 允许你向导入方法传递样式数组，因此我们将创建一个大小恰好等于行数的 `Style[]`。

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **解释：** 通过预先分配数组，我们避免在每次迭代时重新创建新的样式对象，这在处理成千上万行时可以提升性能。

## 步骤 3：应用交替行颜色（浅黄色 / 白色）

现在进入关键步骤：**应用交替行颜色**。我们将遍历每一行，从工作簿创建一个新的样式实例，并根据行索引设置其背景。偶数行使用浅黄色填充，奇数行保持白色。

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### 为什么这样有效
- **`rowIndex % 2 == 0`** 检查行是否为偶数。  
- **`Color.LightYellow`** 提供一种柔和、不突兀的色调，非常适合数据表。  
- **`BackgroundType.Solid`** 确保填充覆盖整个单元格，实现**设置行背景颜色**的效果。  

如果你想要不同的外观，可以将 `Color.LightYellow` 替换为其他任何色调（例如 `Color.LightCyan`）。相同的逻辑也可以让你基于其他条件（如状态标志）**交替着色行**。

## 步骤 4：使用准备好的样式将 DataTable 导入工作表

最后，我们将所有内容写入工作表。大多数库提供接受样式数组的 `ImportDataTable` 重载。`true` 标志指示 API 写入列标题，`0, 0` 坐标则从左上角单元格开始。

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **结果：** 工作表现在以清晰的**交替行阴影**模式显示数据——偶数行为浅黄色，奇数行为白色。用户可以更顺畅地浏览网格，而无需眼睛来回跳动。

### 预期输出
如果打开生成的电子表格，你会看到类似以下内容：

| ID | Name      | Quantity |
|----|-----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

第 1、3、5… 行具有**浅黄色背景**，而第 2、4、6… 行保持**白色**。标题行（第 0 行）继承默认样式，除非你单独自定义。

## 可选变体与边缘情况

### 1. 使用不同的配色方案
如果浅黄色与品牌冲突，只需将 `Color.LightYellow` 替换为其他 `System.Drawing.Color`。例如蓝灰主题可以使用：

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. 基于数据的动态着色
有时你想突出满足特定条件的行（例如库存不足）。将取模检查与自定义测试结合：

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. 仅对特定列应用样式
如果只需要在特定列上**设置行背景颜色**，可以为每列创建单独的样式，并在导入后使用工作表的单元格范围 API 进行分配。

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. 大表性能提示
在处理超过 10,000 行时，考虑为每种颜色复用单一的样式对象，而不是为每行创建新对象。数组随后只保存对这两种共享样式的引用，从而显著降低内存使用。

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## 完整工作示例

下面是一个可直接粘贴到控制台应用的完整示例程序。它使用了一个虚构的 `Workbook`/`Worksheet` API；请将类型替换为你所选库中的对应类型。

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**输出：** 一个名为 `AlternatingRows.xlsx` 的文件，其中每行交替使用浅黄色填充和白色，使表格更易于阅读。

## 常见问题

**Q: 这种方法是否适用于 Excel 样式的条件格式化？**  
A: 是的。如果你的库支持条件规则，你可以将相同的逻辑转换为检查 `MOD(ROW(),2)=0` 的规则。这里展示的基于代码的方法在缺少内置条件格式化的库中更具可移植性。

**Q: 如果我需要在 PDF 表格而不是 Excel 表格中**交替着色行**怎么办？**  
A: 大多数 PDF 表格生成器（例如 iTextSharp、PdfSharp）都允许为每行设置 `BackgroundColor`。相同的取模计算同样适用——

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}