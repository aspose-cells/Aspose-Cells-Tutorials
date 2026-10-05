---
category: general
date: 2026-03-22
description: 学习如何在从 Excel 提取日期时将日期时间格式化为 ISO，并使用 Aspose.Cells 在 C# 中显示 ISO 日期。
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: zh
og_description: 轻松将日期时间格式化为 ISO。本指南展示如何从 Excel 提取日期并使用 Aspose.Cells 显示 ISO 日期。
og_title: 在 C# 中将日期时间格式化为 ISO – 步骤教程
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: 在 C# 中将日期时间格式化为 ISO – 完整指南
url: /zh/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 C# 中将 datetime 格式化为 ISO – 完整指南

是否曾经需要**将 datetime 格式化为 iso**，但数据源位于 Excel 工作簿中？也许单元格中包含类似“令和3年5月1日”的日本纪元，你正为如何将其转换为 `2021‑05‑01` 这种干净的字符串而苦恼。你并不孤单。在本教程中，我们将**从 excel 中提取日期**，解析日本纪元，然后在控制台**显示 iso 日期**——全部只需几行 C# 代码和 Aspose.Cells。

我们将逐步讲解你需要的所有内容：必备的 NuGet 包、可以直接复制粘贴的完整代码、每行代码的意义以及一些边缘案例的技巧。完成后，你将拥有一个可复用的代码片段，无论原始 Excel 值多么古怪，都能将 datetime 格式化为 iso。

## 您需要的环境

- .NET 6.0 或更高（代码同样可以在 .NET Framework 4.6+ 上编译）
- Visual Studio 2022（或您喜欢的任何编辑器）
- **Aspose.Cells for .NET** NuGet 包 – `Install-Package Aspose.Cells`
- 一个包含日本纪元格式日期的 Excel 文件（或新建工作簿）

就是这么简单。无需额外库、无需 COM 互操作，只需一个单一且文档完善的方法。

## 步骤 1：创建工作簿并写入日本纪元日期  

首先，我们需要一个工作簿来操作。如果你已经有 Excel 文件，可以使用 `new Workbook("path")` 加载。此示例我们将在内存中创建一个新工作簿，并将日本纪元字符串写入单元格 **A1**。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **我们这样做的原因：** Aspose.Cells 默认将单元格值视为字符串。通过插入原始纪元文本，我们模拟了日本客户使用本土历法输入日期的真实场景。

## 步骤 2：启用日本纪元解析并提取日期  

Aspose.Cells 可以自动将日本纪元字符串转换为 .NET `DateTime` 对象——前提是你告诉它这么做。`DateTimeParseOptions.EnableJapaneseEra` 标志负责完成这项工作。

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **专业提示：** 如果忘记使用 `EnableJapaneseEra` 选项，库会返回原始字符串，后续转换将失败。处理混合内容时，请始终检查 `parsed.Type`。

## 步骤 3：将解析后的 DateTime 转换为 ISO 8601  

现在我们已经拥有正确的 `DateTime`，将其转换为 ISO 格式的字符串轻而易举。`"yyyy-MM-dd"` 模式符合 ISO 8601 日期部分的要求，这也是大多数 API 所期望的格式。

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

运行程序后会输出：

```
ISO date: 2021-05-01
```

这就是你想要的**显示 iso 日期**。

## 完整、可运行的示例  

下面是可以直接复制到控制台项目中的完整代码块。没有隐藏的依赖，也无需额外配置。

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **预期输出：** `ISO date: 2021-05-01`

## 步骤拆解（每一步的重要性）

| 步骤 | 发生了什么 | 为什么重要 |
|------|------------|------------|
| **Create workbook** | 初始化一个内存中的 Excel 容器。 | 为你提供一个沙盒，能够在不触及文件系统的情况下进行测试。 |
| **PutValue** | 将原始日本纪元字符串存入 **A1**。 | 模拟真实数据录入，确保解析器看到的正是文本本身。 |
| **GetValue with `EnableJapaneseEra`** | 将纪元字符串转换为 .NET `DateTime`。 | 自动完成日历转换，无需手动查表。 |
| **`ToString("yyyy-MM-dd")`** | 将 `DateTime` 格式化为 ISO 8601。 | 保证得到文化无关、可排序的日期字符串，符合 REST API、数据库等的要求。 |
| **Console.WriteLine** | 显示最终的 ISO 日期。 | 验证整个流水线端到端工作正常。 |

## 处理常见变体  

### 1. 不同的单元格位置  

如果你的日期位于 **B2** 或命名范围，只需将 `"A1"` 替换为相应的地址：

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. 列中多个日期  

当需要为多行 **从 excel 中提取日期** 时，遍历已使用的范围即可：

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. 非纪元日期的回退方案  

如果单元格已经包含标准日期字符串，解析器仍然可以工作，但你可能需要一个安全网：

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

`TryParse` 标志可以防止异常，并在转换失败时返回原始值。

### 4. 时间组件  

如果还需要时间部分，可使用 `"yyyy-MM-ddTHH:mm:ss"`：

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

这将生成完整的 ISO 8601 时间戳（`2021-05-01T00:00:00`）。

## 可视化示例  

![datetime 格式化为 iso 示例](image.png "在 C# 中将 datetime 格式化为 iso 的示例")

*Alt 文本:* *显示控制台输出的 datetime 格式化为 iso 示例*

## 常见问题  

- **我可以在 .xls 文件中使用吗？**  
  可以。Aspose.Cells 开箱即支持 `.xls`、`.xlsx`、`.csv` 以及许多其他格式。

- **如果工作簿受密码保护怎么办？**  
  使用 `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })` 加载。

- **ISO 格式是否依赖于地区设置？**  
  不。`"yyyy-MM-dd"` 模式是与区域无关的，确保在任何机器上得到相同的字符串。

- **这在 .NET Core 上能工作吗？**  
  当然可以——Aspose.Cells 符合 .NET Standard 2.0。

## 总结  

我们已经介绍了如何通过**从 excel 中提取日期**、解析日本纪元字符串，最终在控制台**显示 iso 日期**来**将 datetime 格式化为 iso**。核心步骤——创建工作簿、写入或加载纪元文本、启用日本纪元解析、使用 `ToString("yyyy-MM-dd")` 格式化——几乎可以应对所有场景。

接下来，你可能想要：

- 将 ISO 日期写回另一列，以便后续处理。
- 将转换后的工作簿导出为 CSV，以便批量导入。
- 将此逻辑与接受 Excel 上传并返回 JSON 编码 ISO 日期的 Web API 结合。

欢迎尝试不同的日期格式、时区，甚至自定义日历。Aspose.Cells 的灵活性意味着你很少会遇到瓶颈。

祝编码愉快，愿你的所有日期都完美符合 ISO 标准！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}