---
title: 编辑 Excel 工作表中的范围
linktitle: 编辑 Excel 工作表中的范围
second_title: Aspose.Cells for .NET API 参考
description: 通过本包含分步说明的综合指南，学习使用 Aspose.Cells for .NET 编辑 Excel 工作表中的范围。
weight: 20
url: /zh/net/protect-excel-file/edit-ranges-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 编辑 Excel 工作表中的范围

## 介绍

在编辑 Excel 电子表格时，最强大的功能之一就是能够保护某些区域，同时允许编辑其他区域。这在协作环境中非常有用，因为多个用户需要访问但只能修改指定的单元格。今天，我们将深入探讨如何利用 Aspose.Cells for .NET 来管理 Excel 工作表中的可编辑范围。所以，拿起你最喜欢的编码饮料，让我们开始吧！

## 先决条件

在开始编码之前，让我们先确保您已做好一切准备。以下是您需要的内容：

1. Visual Studio：确保已安装 Visual Studio。社区版运行良好。
2.  Aspose.Cells 库：您需要 Aspose.Cells for .NET 库。您可以[点击下载](https://releases.aspose.com/cells/net/).
3. 基本 C# 知识：对 C# 的基本了解将大有帮助。
4. 项目设置：在 Visual Studio 中创建一个新的 C# 控制台应用程序。

完美无缺——一切就绪！现在，让我们深入研究代码的细节。

## 导入包

设置好项目后，第一步是导入必要的 Aspose.Cells 命名空间。为此，只需在代码文件顶部包含以下行：

```csharp
using Aspose.Cells;
```

这将允许您访问项目中 Aspose.Cells 提供的所有功能。

## 步骤 1：设置目录

在开始处理 Excel 文件之前，最好先建立一个文件存放目录。此步骤可确保您的应用程序知道在哪里读取和写入数据。

让我们列出创建目录的代码（如果它尚不存在）：

```csharp
//文档目录的路径。
string dataDir = "YOUR DOCUMENT DIRECTORY";
//如果目录尚不存在，则创建目录。
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

代替`"YOUR DOCUMENT DIRECTORY"`替换为要存储文件的路径。这可能是`@"C:\ExcelFiles\"`.

## 步骤 2：实例化新工作簿

现在您的目录已全部设置好，让我们创建一个新的 Excel 工作簿。这类似于在开始绘画之前启动一张空白画布。

```csharp
//实例化新的工作簿
Workbook book = new Workbook();
```

这样，您的空白工作簿就可以准备好了！

## 步骤 3：获取第一个工作表

每个工作簿默认包含至少一个工作表。您需要获取该工作表才能对其进行操作。

```csharp
//获取第一个（默认）工作表
Worksheet sheet = book.Worksheets[0];
```

在这里，我们访问第一个工作表，这类似于在笔记本中打开一张新纸。

## 步骤 4：获取允许编辑范围

在我们设置可编辑范围之前，我们需要从工作表中检索受保护范围的集合。

```csharp
//获取允许编辑范围
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```

此行获取您将管理受保护范围的集合。了解底层可用内容很有用！

## 步骤 5：定义并创建保护范围

此时，我们已准备好定义您想要允许编辑的范围。让我们创建这个范围。

```csharp
//定义保护范围
ProtectedRange proteced_range;

//创建范围
int idx = allowRanges.Add("r2", 1, 1, 3, 3);
proteced_range = allowRanges[idx];
```

在上面的代码中，我们创建了一个名为“r2”的受保护范围，允许编辑从第 1 行第 1 列到第 3 行第 3 列的单元格（在 Excel 术语中，相当于 A1 到 C3 的块）。您可以根据需要调整这些索引。

## 步骤 6：设置密码 

为受保护区域设置密码可确保只有拥有密码的人才能修改定义的区域。此步骤可增强电子表格的安全性。

```csharp
//指定密码
proteced_range.Password = "YOUR_PASSWORD";
```

代替`"YOUR_PASSWORD"`用您选择的密码。请记住，不要把它弄得太简单——把它想象成锁住你的宝箱！

## 步骤 7：保护工作表

现在我们已经定义好可编辑范围并用密码保护，是时候保护整个工作表了。

```csharp
//保护工作表
sheet.Protect(ProtectionType.All);
```

通过调用此方法，您实际上是锁定了整个工作表。只有定义的编辑范围才可以更改。

## 步骤 8：保存 Excel 文件

我们终于到达了教程的最后一步 - 将工作簿保存到您定义的目录中！

```csharp
//保存 Excel 文件
book.Save(dataDir + "protectedrange.out.xls");
```

这会将受保护的工作簿保存为`protectedrange.out.xls`在您指定的目录中。

## 结论

就这样！您已成功使用 Aspose.Cells for .NET 创建了 Excel 工作表，定义了可编辑范围，设置了密码并保护了工作表 — 只需几个简单的步骤即可完成。现在您可以与同事共享工作簿，在增强协作的同时确保重要数据的安全。

## 常见问题解答

### 什么是 Aspose.Cells？  
Aspose.Cells 是一个功能强大的.NET 库，允许开发人员以编程方式创建、操作和转换 Excel 文件。

### 我可以保护 Excel 工作表中的特定单元格吗？  
是的，使用 Aspose.Cells，您可以定义特定的可编辑范围并保护工作表的其余部分。

### Aspose.Cells 有试用版吗？  
当然可以！您可以下载免费试用版[这里](https://releases.aspose.com/).

### 我可以将 Aspose.Cells 与其他编程语言一起使用吗？  
虽然本教程重点介绍.NET，但 Aspose.Cells 适用于多种编程语言，包括 Java 和云 API。

### 在哪里可以找到有关 Aspose.Cells 的更多信息？  
您可以浏览完整文档[这里](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
