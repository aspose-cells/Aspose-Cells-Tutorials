---
"description": "学习使用 Aspose.Cells for .NET 在 Excel 工作表中创建可编辑范围，允许特定单元格可编辑，同时使用工作表保护确保其余单元格的安全。"
"linktitle": "允许用户使用 Aspose.Cells 编辑工作表中的范围"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "允许用户使用 Aspose.Cells 编辑工作表中的范围"
"url": "/zh/net/worksheet-security/allow-edit-ranges/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 允许用户使用 Aspose.Cells 编辑工作表中的范围

## 介绍
Excel 文档通常包含敏感数据或结构化内容，您希望保护它们免受不必要的编辑。但是，您可能希望将某些单元格或区域设置为仅供特定用户编辑。这时，Aspose.Cells for .NET 便应运而生，它是一款强大的工具，可让您保护整个工作表，同时仍授予指定区域的编辑权限。想象一下，共享一个预算电子表格，其中只有某些单元格可编辑，而其他单元格保持安全——Aspose.Cells 让这一切变得简单高效。
## 先决条件
在深入编码部分之前，让我们确保您拥有所需的一切：
- Aspose.Cells for .NET：确保您已安装 Aspose.Cells for .NET 库。您可以下载 [这里](https://releases。aspose.com/cells/net/).
- 开发环境：Visual Studio 或任何与 C# 兼容的 IDE。
- .NET Framework：4.0 或更高版本。
- 许可证：考虑获取许可证以避免试用限制。您可以获取 [此处为临时驾照](https://purchase。aspose.com/temporary-license/).
## 导入包
确保在代码开始时包含必要的 Aspose.Cells 命名空间：
```csharp
using System.IO;
using Aspose.Cells;
```
这将确保您可以访问在 Excel 文件中设置受保护范围所需的所有类和方法。
现在基础工作已经就绪，让我们一步一步详细地介绍代码。
## 步骤 1：设置目录
在处理文件之前，您需要设置保存 Excel 文件的目录。这可以确保您的文件井然有序且安全存储。
```csharp
// 定义文档目录的路径
string dataDir = "Your Document Directory";
// 检查目录是否存在，如果不存在则创建
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
这部分代码确保你的目录已准备好进行文件操作。你可以把它看作是为接下来的一切奠定基础。
## 步骤 2：初始化工作簿和工作表
现在，让我们继续创建一个新的工作簿并访问其默认工作表。
```csharp
// 初始化新的工作簿
Workbook book = new Workbook();
// 访问工作簿中的第一个工作表
Worksheet sheet = book.Worksheets[0];
```
这里，我们初始化一个 Excel 工作簿并选择其中的第一个工作表。此工作表将作为我们应用保护设置和定义可编辑范围的画布。
## 步骤 3：访问允许编辑范围集合
Aspose.Cells 有一个功能叫做 `AllowEditRanges`，它是可编辑的范围的集合，即使工作表受到保护也是如此。
```csharp
// 访问“允许编辑范围”集合
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
此行设置了对可编辑的特殊范围集合的访问权限。您可以将其视为工作表中的“VIP”区域，只有特定范围才能绕过保护。
## 步骤 4：定义并创建受保护范围
现在，让我们在工作表中定义并创建一个受保护的范围。我们将指定此范围的起始单元格和结束单元格。
```csharp
// 定义 ProtectedRange 变量
ProtectedRange protectedRange;
// 向集合中添加具有特定名称和单元格位置的新范围
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
在此代码块中：
- `EditableRange` 是分配给范围的名称。
- 数字 (1, 1, 3, 3) 定义范围坐标，表示它从单元格 B2（第 1 行，第 1 列）开始到单元格 D4（第 3 行，第 3 列）。
## 步骤 5：为受保护范围设置密码
为了增强安全性，您可以为受保护的范围设置密码。此步骤增加了一层额外的保护，确保只有授权用户才能编辑该范围。
```csharp
// 为可编辑范围设置密码
protectedRange.Password = "123";
```
在这里，我们添加了密码（`"123"`) 到受保护的范围。此密码要求为谁可以进行更改提供了额外的控制级别。
## 步骤 6：保护工作表
确定可编辑范围后，下一步就是保护整个工作表。此保护设置将确保定义范围之外的所有单元格均被锁定且不可编辑。
```csharp
// 对工作表应用保护，使所有其他单元格不可编辑
sheet.Protect(ProtectionType.All);
```
这 `Protect` 方法会锁定整个工作表，除了我们定义为可编辑的区域。此步骤本质上创建了一个安全的“只读”环境，用户可以根据需要访问特定的单元格。
## 步骤 7：保存工作簿
最后一步是保存工作簿，以便应用和存储您的设置。
```csharp
// 将Excel文件保存到指定目录
book.Save(dataDir + "protectedrange.out.xls");
```
在此步骤中，我们将工作簿保存为步骤 1 中设置的目录中的“protectedrange.out.xls”。现在，您拥有一个功能齐全、安全的 Excel 文件，其中只有特定范围可编辑！
## 结论
Aspose.Cells for .NET 提供了一种出色的方式来管理 Excel 文件中的保护和权限。通过创建可编辑区域，您可以保护工作表的安全，同时仍允许特定区域保持可访问。此功能对于协作文档尤其有用，因为协作文档中只有少数单元格可以打开进行编辑，而其他单元格则保持锁定状态。
## 常见问题解答
### 我可以向工作表添加多个可编辑范围吗？
是的，您可以通过重复以下操作添加多个范围 `allowRanges.Add()` 方法适用于每个新范围。
### 如果我稍后想删除受保护的范围怎么办？
使用 `allowRanges.RemoveAt()` 方法与您想要删除的范围的索引。
### 我可以为每个范围设置不同的密码吗？
绝对如此。每个 `ProtectedRange` 可以拥有自己独特的密码，让您进行精细控制。
### 如果我保护工作表而没有任何可编辑范围会发生什么？
如果您不定义可编辑范围，则整个工作表一旦受到保护将不可编辑。
### 受保护的范围对其他用户可见吗？
不会，保护是内部的。只有当用户尝试编辑受保护区域时，才会提示输入密码。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}