---
"description": "在本综合教程中了解如何使用 Aspose.Cells for .NET 管理 XLSB 文件中的外部连接。"
"linktitle": "XLSB文件的外部连接读写"
"second_title": "Aspose.Cells for .NET API参考"
"title": "XLSB文件的外部连接读写"
"url": "/zh/net/excel-workbook/read-and-write-external-connection-of-xlsb-file/"
"weight": 130
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# XLSB文件的外部连接读写

## 介绍

嗨，Excel 爱好者们！准备好探索 XLSB 文件和外部连接的奇妙世界了吗？如果您曾经使用过 Excel，您就会知道它功能强大、用途广泛，但有时也会出现一些小问题——尤其是在处理与外部数据库的连接时。这时，Aspose.Cells for .NET 就派上用场了！这个精巧的库可以让您以直观的方式操作 Excel 文件。在本文中，我们将逐步指导您如何在 XLSB 文件中读取和写入外部连接。

## 先决条件

在我们开始之前，您需要准备以下几样东西：

1. C# 基础知识：了解 C# 编程语言将大有裨益。如果你能熟练地编写 C# 代码，那就大功告成了！
2. Aspose.Cells for .NET：您需要在开发环境中安装此库。如果您尚未安装，可以轻松下载。 [这里](https://releases。aspose.com/cells/net/). 
3. IDE：您需要一个代码编辑器或集成开发环境 (IDE)，例如 Visual Studio。 
4. XLSB 示例文件：我们将使用包含外部连接的示例 XLSB 文件。您可以创建自己的示例文件，也可以在线下载示例文件。 

一旦满足了所有这些先决条件，我们就可以开始编写代码了！

## 导入包

首先，让我们在项目中导入必要的包。确保已在项目中添加了对 Aspose.Cells 的引用。以下是在 C# 中执行此操作的方法：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

这些导入使您可以访问操作 Excel 文件及其连接所需的功能。

## 步骤 1：设置目录

在使用 XLSB 文件之前，您需要设置源目录和输出目录。此步骤对于保持文件井然有序至关重要。

```csharp
// 源目录
string sourceDir = "Your Document Directory";
// 输出目录
string outputDir = "Your Output Directory";
```

在此代码片段中， `"Your Document Directory"` 和 `"Your Document Directory"` 假定用于获取输入和输出文件所在的相应路径。如果您愿意，可以用硬编码路径替换这些方法。

## 步骤2：加载XLSB文件

现在是时候将你的 Excel 文件加载到 Workbook 对象中了。这样你就能够操作其中的数据了。

```csharp
// 加载源 Excel Xlsb 文件
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

只需确保您的 XLSB 文件位于指定的 `sourceDir`。如果路径正确，您的工作簿就可以进行操作了！

## 步骤 3：访问外部连接

工作簿加载完成后，您就可以访问其外部连接了。在本例中，我们将检索第一个数据库连接。

```csharp
// 读取第一个外部连接，实际上是一个 DB-Connection
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

这里， `DataConnections[0]` 指的是工作簿中的第一个连接。我们将其转换为 `DBConnection` 类型以进行进一步的操作。

## 步骤4：提取连接信息

现在您可以访问数据库连接了，让我们提取其详细信息并将其打印到控制台。这将帮助我们准确地了解我们正在处理的内容。

```csharp
// 打印 DB 连接的名称、命令和连接信息
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

此步骤允许您验证外部连接的当前状态。您将看到连接名称、使用的命令以及打印到控制台的连接信息。

## 步骤5：修改连接

有时，只需更改名称即可使事情更清晰或符合新的命名约定。让我们将现有的连接名称更改为更相关的名称。

```csharp
// 修改连接名称
dbCon.Name = "NewCust";
```

这行代码有效地将您的连接从原始名称重命名为“NewCust”。这是一个简单但有效的更改！

## 步骤6：保存更改

修改完成后，您需要将更改保存回 XLSB 文件。操作方法如下：

```csharp
// 保存 Excel Xlsb 文件
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

这行代码保存了更新的工作簿，保留了所有更改，包括新的连接名称。

## 步骤7：确认执行

最后，让我们确认一下一切是否顺利。最后的一条简单消息就能说明一切。

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

此消息将向您保证您的代码已成功运行，并且所有更改均已按预期保存。

## 结论

就这样！您已经成功学会了如何使用 Aspose.Cells for .NET 在 XLSB 文件中读写外部连接。按照以下步骤操作，您可以有效地管理 Excel 数据连接，让您的 Excel 工作更加流畅，减少烦恼。请记住，无论您是处理海量数据集还是仅仅组织信息，Aspose.Cells 都能为您提供所需的工具。

## 常见问题解答

### 什么是 XLSB 文件？  
XLSB文件是一种二进制Excel文件格式，以二进制格式存储电子表格数据，使其更紧凑、打开速度更快。

### 如何安装 Aspose.Cells for .NET？  
您可以从 Aspose 网站轻松下载它 [这里](https://releases。aspose.com/cells/net/).

### 我可以免费使用 Aspose.Cells 吗？  
是的！您可以先免费试用， [这里](https://releases。aspose.com/).

### Aspose.Cells 是否支持其他文件格式？  
当然！Aspose.Cells 支持多种文件格式，包括 XLSX、CSV 等。

### 如果我遇到问题，可以去哪里寻求帮助？  
您可以从 Aspose 论坛获得支持 [这里](https://forum。aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}