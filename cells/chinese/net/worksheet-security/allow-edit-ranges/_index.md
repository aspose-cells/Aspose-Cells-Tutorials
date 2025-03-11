---
title: 允许用户使用 Aspose.Cells 编辑工作表中的范围
linktitle: 允许用户使用 Aspose.Cells 编辑工作表中的范围
second_title: Aspose.Cells .NET Excel 处理 API
description: 学习使用 Aspose.Cells for .NET 在 Excel 工作表中创建可编辑范围，允许特定单元格可编辑，同时使用工作表保护确保其余单元格的安全。
weight: 10
url: /zh/net/worksheet-security/allow-edit-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 允许用户使用 Aspose.Cells 编辑工作表中的范围

## 介绍
Excel 文档通常包含敏感数据或结构化内容，您希望保护它们免受不必要的编辑。但是，您可能希望某些单元格或范围可供某些用户编辑。这就是 Aspose.Cells for .NET 发挥作用的地方，它是一款强大的工具，可让您保护整个工作表，同时仍授予指定范围的编辑权限。想象一下共享一个预算电子表格，其中只有某些单元格可编辑，而其他单元格保持安全 - Aspose.Cells 使这变得简单而高效。
## 先决条件
在深入编码部分之前，让我们确保您已准备好所需的一切：
-  Aspose.Cells for .NET：确保您已安装 Aspose.Cells for .NET 库。您可以下载它[这里](https://releases.aspose.com/cells/net/).
- 开发环境：Visual Studio 或任何与 C# 兼容的 IDE。
- .NET Framework：版本 4.0 或更高版本。
- 许可证：考虑获取许可证以避免试用限制。您可以获取[此处为临时执照](https://purchase.aspose.com/temporary-license/).
## 导入包
确保在代码开始处包含必要的 Aspose.Cells 命名空间：
```csharp
using System.IO;
using Aspose.Cells;
```
这将确保您可以访问在 Excel 文件中设置受保护范围所需的所有类和方法。
现在基础工作已经就绪，让我们一步一步地详细了解代码。
## 步骤 1：设置目录
在处理文件之前，您需要设置保存 Excel 文件的目录。这可确保您的文件井然有序且存储安全。
```csharp
//定义文档目录的路径
string dataDir = "Your Document Directory";
//检查目录是否存在，如果不存在则创建
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
这部分代码可确保您的目录已准备好进行文件操作。可以将其视为为后续所有内容奠定基础。
## 步骤 2：初始化工作簿和工作表
现在，让我们继续创建一个新的工作簿并访问其默认工作表。
```csharp
//初始化新工作簿
Workbook book = new Workbook();
//访问工作簿中的第一个工作表
Worksheet sheet = book.Worksheets[0];
```
这里，我们初始化一个 Excel 工作簿并选择其中的第一个工作表。此工作表将成为我们应用保护设置和定义可编辑范围的画布。
## 步骤 3：访问允许编辑范围集合
Aspose.Cells 有一项功能叫做`AllowEditRanges`，它是可编辑的范围的集合，即使工作表受到保护也是如此。
```csharp
//访问“允许编辑区域”集合
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
此行设置对可编辑的特殊范围集合的访问权限。可以将其视为工作表中的“VIP”区域，其中只有特定范围才允许绕过保护。
## 步骤 4：定义并创建保护范围
现在，让我们在工作表中定义并创建一个受保护的范围。我们将指定此范围的起始和结束单元格。
```csharp
//定义 ProtectedRange 变量
ProtectedRange protectedRange;
//向集合中添加具有特定名称和单元格位置的新范围
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
在此代码块中：
- `EditableRange`是分配给该范围的名称。
- 数字 (1, 1, 3, 3) 定义范围坐标，表示它从单元格 B2（第 1 行，第 1 列）开始到单元格 D4（第 3 行，第 3 列）。
## 步骤 5：为受保护范围设置密码
为了增加安全性，您可以为受保护的范围设置密码。此步骤增加了一层额外的保护，以确保只有授权用户才能编辑该范围。
```csharp
//为可编辑范围设置密码
protectedRange.Password = "123";
```
在这里，我们添加了密码（`"123"`) 到受保护的范围。此密码要求为谁可以进行更改提供了额外的控制级别。
## 步骤 6：保护工作表
建立可编辑范围后，下一步是保护整个工作表。此保护设置将确保定义范围之外的所有单元格都被锁定且不可编辑。
```csharp
//对工作表应用保护，使所有其他单元格不可编辑
sheet.Protect(ProtectionType.All);
```
这`Protect`方法锁定整个工作表，除了我们定义为可编辑的范围。此步骤实质上创建了一个安全的“只读”环境，可以根据需要访问特定单元格。
## 步骤 7：保存工作簿
最后一步是保存工作簿，这样您的设置就会被应用和存储。
```csharp
//保存Excel文件到指定目录
book.Save(dataDir + "protectedrange.out.xls");
```
在此步骤中，我们将工作簿保存为步骤 1 中设置的目录中的“protectedrange.out.xls”。现在，您拥有一个功能齐全、安全的 Excel 文件，其中只有特定范围可编辑！
## 结论
Aspose.Cells for .NET 提供了一种管理 Excel 文件中的保护和权限的绝佳方法。通过创建可编辑范围，您可以保护工作表，同时仍允许特定区域保持可访问。此功能对于协作文档特别有用，因为协作文档中只有少数单元格应打开进行编辑，而其他单元格保持锁定状态。
## 常见问题解答
### 我可以向工作表添加多个可编辑范围吗？
是的，你可以添加多个范围，只需重复`allowRanges.Add()`方法适用于每个新范围。
### 如果我稍后想删除受保护的范围该怎么办？
使用`allowRanges.RemoveAt()`方法与您想要删除的范围的索引。
### 我可以为每个范围设置不同的密码吗？
当然。每个`ProtectedRange`可以拥有自己独特的密码，从而为您提供精细的控制。
### 如果我保护工作表而没有任何可编辑范围会发生什么？
如果您不定义可编辑范围，则整个工作表一旦受到保护将不可编辑。
### 受保护的范围对其他用户可见吗？
否，保护是内部的。只有当用户尝试编辑受保护区域时，才会提示输入密码。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
