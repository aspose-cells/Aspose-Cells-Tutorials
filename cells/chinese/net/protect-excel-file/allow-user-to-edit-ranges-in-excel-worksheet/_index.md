---
"description": "允许用户使用 Aspose.Cells for .NET 编辑 Excel 电子表格中的特定范围。提供 C# 源代码的分步指南。"
"linktitle": "允许用户编辑 Excel 工作表中的范围"
"second_title": "Aspose.Cells for .NET API参考"
"title": "允许用户编辑 Excel 工作表中的范围"
"url": "/zh/net/protect-excel-file/allow-user-to-edit-ranges-in-excel-worksheet/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 允许用户编辑 Excel 工作表中的范围

## 介绍

在使用 Excel 工作表时，灵活性通常至关重要——尤其是在多个用户需要访问编辑特定区域且不损害整个工作表数据完整性的情况下。这正是 Aspose.Cells for .NET 的优势所在！在本教程中，我们将深入探讨如何允许用户编辑 Excel 工作表中的特定区域，同时保护文档的其余部分。读完本文后，您不仅能掌握相关概念，还能获得一个实际的示例来操作。 

## 先决条件

在我们讨论细节之前，让我们确保您已准备好开始所需的一切：

1. .NET 开发环境：您应该设置一个可运行的 .NET 开发环境（可以是 Visual Studio 或您选择的任何其他 IDE）。
2. Aspose.Cells for .NET Library：下载并安装 Aspose.Cells 库。您可以找到它 [这里](https://releases。aspose.com/cells/net/).
3. C# 基础知识：熟悉 C# 编程将帮助您轻松浏览代码示例。
4. 了解 Excel 基础知识：了解 Excel 的工作原理将为我们将要讨论的功能奠定基础。

一旦满足了这些先决条件，您就可以开始了！

## 导入包

在开始编码之前，我们需要确保我们的项目能够识别 Aspose.Cells 命名空间。导入必要的包的方法如下：

```csharp
using System.IO;
using Aspose.Cells;
```

现在我们已经导入了我们需要的内容，让我们逐步深入了解我们的教程。

## 步骤 1：设置文档目录

对于任何文件操作，定义一个保存文档的位置至关重要。让我们设置工作目录来存储 Excel 文件。

```csharp
// 文档目录的路径。
string dataDir = "YOUR DOCUMENT DIRECTORY";

// 如果目录尚不存在，则创建该目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

首先，更换 `"YOUR DOCUMENT DIRECTORY"` 替换为您想要保存文件的路径。此代码检查该目录是否存在；如果不存在，则创建一个。

## 步骤 2：实例化新工作簿

工作目录准备好后，就可以创建 Excel 工作簿了。 

```csharp
// 实例化新的工作簿
Workbook book = new Workbook();
```

在这里，我们正在创建一个新的实例 `Workbook` Aspose.Cells 提供的类，它允许我们操作 Excel 文件。

## 步骤 3：访问默认工作表

每个新创建的工作簿都至少包含一个工作表。让我们来访问它。

```csharp
// 获取第一个（默认）工作表
Worksheet sheet = book.Worksheets[0];
```

在此代码片段中，我们访问工作簿的第一个工作表，我们将在后续步骤中对其进行操作。

## 步骤 4：获取允许编辑范围

为了能够编辑工作表的特定范围，我们需要访问 `AllowEditRanges` 财产。

```csharp
// 获取允许编辑范围
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

该集合将允许我们管理工作表中哪些范围是可编辑的。

## 步骤5：定义保护范围

接下来，让我们定义想要保护工作表的哪一部分，同时允许对指定范围进行编辑。

```csharp
// 定义 ProtectedRange
ProtectedRange proteced_range;

// 创建范围
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];

// 指定密码
proteced_range.Password = "123";
```

在此步骤中，我们添加一个名为“r2”的新可编辑范围，允许编辑从第 1 行第 1 列到第 3 行第 3 列的单元格。此外，我们设置密码来保护此范围，确保只有授权用户才能修改它。

## 步骤 6：保护工作表

现在我们已经设置了可编辑范围，我们需要保护工作表。

```csharp
// 保护工作表
sheet.Protect(ProtectionType.All);
```

此代码将保护整个工作表免受任何不必要的更改，除了我们刚刚指定的范围之外。

## 步骤 7：保存 Excel 文件

让我们保存工作簿，以便我们可以在 Excel 文件中看到我们的更改。

```csharp
// 保存 Excel 文件
book.Save(dataDir + "protectedrange.out.xls");
```

请务必根据需要调整文件名。这将使用我们配置的设置在指定的目录中创建一个 Excel 文件。

## 结论

就是这样！您已成功创建了一个 Excel 工作表，该工作表将编辑限制在指定范围内，同时保护工作表的其余部分。使用 Aspose.Cells for .NET 可以使管理此类任务更加简单高效。无论您是开发复杂的应用程序，还是只需要安全地管理数据，这些功能都可以显著增强您的工作流程。

## 常见问题解答

### 什么是 Aspose.Cells？
Aspose.Cells 是一个功能强大的 .NET 库，用于处理 Excel 文件，提供以编程方式创建、编辑和转换电子表格等功能。

### 我可以应用多个可编辑范围吗？
当然！你可以致电 `Add` 方法 `allowRanges` 多次收集以指定多个可编辑范围。

### 如果我忘记了密码怎么办？
不幸的是，如果您忘记了可编辑范围的密码，则需要删除保护或以可能涉及凭据的预定义方式访问文件。

### Aspose.Cells 有免费版本吗？
是的，Aspose 提供免费试用，您可以在购买前利用它探索其功能。

### 在哪里可以找到有关 Aspose.Cells 的更多信息？
您可以检查 [文档](https://reference.aspose.com/cells/net/) 以获得详细的指南和参考。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}