---
category: general
date: 2026-09-24
description: 使用 Aspose.Cells 在 C# 中解析带有日本天皇年号的 DateTime。启用日本纪元历，写入年号字符串，并获取准确的 DateTime
  值。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: zh
lastmod: 2026-09-24
og_description: 使用 Aspose.Cells 在 C# 中解析带有日本天皇年号的 DateTime。本教程展示如何启用日本纪元日历、写入纪元字符串，并读取正确的
  DateTime。
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: 使用 Aspose.Cells 解析带有日本天皇在位时期的日期时间 – C# 指南
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: 使用 Aspose.Cells 解析带有日本天皇年号的日期时间
url: /zh/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 解析带有日本天皇年号的 DateTime

如果您需要在 .NET 应用程序中 **解析带有日本天皇年号的 DateTime**，本指南将向您展示如何使用 Aspose.Cells 完成此操作。通过启用日本年号日历、写入基于年号的字符串并读取生成的 `DateTime` 值，您可以获得可靠的、符合文化的日期，而无需手动字符串处理。

在金融、政府以及仍然以 “令和3年5月10日” 形式存储日期的遗留系统中，使用日本年号日期非常常见。本教程涵盖完整的工作流程，从项目设置到获取可用于计算、日志记录或 UI 显示的 `DateTime` 对象。

## 您将学习的内容

- 如何将 Aspose.Cells NuGet 包添加到 C# 项目中。  
- 如何通过 `Workbook.Settings` 启用 **Japanese era calendar**（日本年号日历）。  
- 如何将日本年号日期字符串写入单元格并让 Aspose.Cells 自动解析。  
- 如何使用 `DateTimeValue` 属性读取解析后的 `DateTime`。  

**先决条件**  
- .NET 6.0 或更高（代码同样适用于 .NET Framework 4.7+）。  
- 对 C# 和 Visual Studio（或任意 IDE）有基本了解。  
- 有互联网连接以下载 Aspose.Cells 包。

---

## 第一步：安装 Aspose.Cells

在终端或 NuGet 包管理器控制台中打开项目文件夹并运行：

```bash
dotnet add package Aspose.Cells
```

或者，在 Visual Studio 中，右键单击项目 → **Manage NuGet Packages** → 搜索 **Aspose.Cells** 并点击 **Install**。  
这将添加 `Aspose.Cells` 程序集，提供我们所需的 `Workbook`、`Worksheet` 和解析功能。

## 第二步：启用日本年号日历

Aspose.Cells 默认禁用日本年号解析。您必须通过 `Workbook.Settings.UseJapaneseEraCalendar` 标志将其打开。

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

将 `UseJapaneseEraCalendar` 设置为 `true`，库会根据官方日本日历规则解释包含年号（`令和`、`平成`、`昭和` 等）的字符串。

## 第三步：将日本年号日期字符串写入单元格

接下来，获取第一个工作表并将日本年号日期字符串写入单元格 **A1**。

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**为什么这样有效：**  
当 `UseJapaneseEraCalendar` 处于激活状态时，`PutValue` 会检查字符串，检测到年号前缀（`令和`），并在内部转换为对应的公历年份（2021）。库随后将该值存储为真正的 `DateTime` 对象，而不是纯文本。

## 第四步：获取解析后的 `DateTime` 值

现在读取单元格的 `DateTimeValue`。Aspose.Cells 会自动返回公历日期。

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

运行程序后输出：

```
Parsed Gregorian date: 2021-05-10
```

输出确认 **Parse DateTime with Japanese Emperor Reign** 正确地将 “令和3年5月10日” 转换为 2021 年 5 月 10 日。

## 第五步：处理边缘情况和常见变体

### 多种年号格式
Aspose.Cells 能识别多种年号表示方式：

| 年号（Japanese） | 公历年份范围 |
|----------------|----------------------|
| 明治 (Meiji)   | 1868‑1912            |
| 大正 (Taishō)  | 1912‑1926            |
| 昭和 (Shōwa)   | 1926‑1989            |
| 平成 (Heisei)  | 1989‑2019            |
| 令和 (Reiwa)   | 2019‑present         |

如果您的源数据混合全角字符、空格，或使用汉字 “年”、 “月”、 “日”，解析器仍能成功。例如，`"平成31年4月30日"` 将转换为 `2019-04-30`。

### 无效字符串
当字符串无法解析时（例如，`"令和99年13月40日"`），`DateTimeValue` 返回 `DateTime.MinValue`。您可以检查此情况：

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### 禁用此功能
如果以后需要存储未转换的原始年号字符串，可将该标志重新设为 `false`：

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### 性能提示
启用年号日历会给每个涉及字符串的 `PutValue` 调用带来少量开销。如果只解析少量单元格，建议在操作前打开标志，操作后关闭，以将影响降至最低。

## 完整、可运行的示例

下面是完整的程序代码，您可以直接复制、粘贴并立即运行。

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**预期输出**

```
Parsed Gregorian date: 2021-05-10
```

该程序演示了使用 Aspose.Cells 完成 **Parse DateTime with Japanese Emperor Reign** 的端到端流程，从工作簿创建到获取可用的 `DateTime` 对象。

---

## 结论

现在，您已经了解如何在 C# 中通过以下步骤 **Parse DateTime with Japanese Emperor Reign**：

1. 安装 **Aspose.Cells**。  
2. 通过 `Workbook.Settings` 启用 **Japanese era calendar**（日本年号日历）。  
3. 将基于年号的字符串写入单元格。  
4. 读取生成的 `DateTimeValue`。  

此方法消除了手动解析逻辑，遵循官方年号边界，并能无缝集成到现有的 .NET 日期处理代码中。

**下一步**  
- 探索 Aspose.Cells 的其他文化特定功能，例如针对伊斯兰历或泰国佛教历的 **C# date parsing**。  
- 将此技术与 `CalcEngine` 等 **Workbook Settings** 结合，以评估引用年号日期的公式。  
- 在报表、数据库存储或需要公历日期的 UI 组件中使用解析后的 `DateTime`。  

欢迎尝试不同的年号字符串，处理无效输入，并将该解决方案集成到更大的数据导入流水线中。祝编码愉快！

## 接下来您应该学习什么？

以下教程涵盖与本指南技术密切相关的主题。每个资源都包含完整的可运行代码示例和逐步说明，帮助您掌握更多 API 功能并在项目中探索替代实现方案。

- [在 Excel 中解析日本年号日期 – C# 开发者完整指南](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [如何在 C# 中解析日本日期 – 完整指南](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [如何使用 Aspose.Cells 在 .NET 中实现日期验证：综合指南](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}