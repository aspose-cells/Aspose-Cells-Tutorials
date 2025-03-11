---
title: 密码保护或取消保护共享工作簿
linktitle: 密码保护或取消保护共享工作簿
second_title: Aspose.Cells for .NET API 参考
description: 通过我们关于密码保护和取消保护技术的简易指南，使用 Aspose.Cells for .NET 保护您共享的 Excel 文件。
weight: 120
url: /zh/net/excel-workbook/password-protect-or-unprotect-shared-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 密码保护或取消保护共享工作簿

## 介绍

在当今的数字工作空间中，共享文档是一种常见的情况，需要仔细考虑安全性。使用 Excel 文件（尤其是共享工作簿）时，保护敏感信息至关重要。在本指南中，我将带您完成使用 Aspose.Cells for .NET 保护和取消保护共享工作簿的密码步骤。最后，您将像专业人士一样自信地管理 Excel 安全性！

## 先决条件

在深入研究代码之前，请确保您已准备好以下内容：

- C# 基础知识：您不需要成为编码专家，但您应该熟悉 C# 语法和概念。
-  Aspose.Cells for .NET：确保您的项目中安装了该库。您可以[点击下载](https://releases.aspose.com/cells/net/).
- .NET SDK：确保您已安装 .NET SDK 以运行该应用程序。
- Visual Studio 或任何 IDE：设置您喜欢的编码环境来编写和执行代码。

## 导入包

首先，您需要导入必要的软件包。在您的 C# 项目中，包含 Aspose.Cells 库。您可以这样做：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

有了正确的软件包，我们可以顺利地创建、保护和取消保护我们的共享工作簿。 

## 步骤 1：设置输出目录

您需要做的第一件事是定义输出文件的保存位置。这就像在创作作品之前设置一个文件夹。操作方法如下：

```csharp
//输出目录
string outputDir = "Your Document Directory";
```

这行代码检索将存储生成的文件的目录路径。 确保此目录存在；否则，您稍后可能会遇到文件未找到错误。

## 步骤 2：创建新工作簿

接下来，我们将创建一个新的 Excel 工作簿实例。将其视为铺设一块空白画布来开始您的杰作。

```csharp
//创建空的 Excel 文件
Workbook wb = new Workbook();
```

此行初始化一个名为的新工作簿对象`wb`。现在我们准备在这块新画布上进行创作。

## 步骤 3：使用密码保护共享工作簿

现在到了最有趣的部分——保护我们的工作簿。通过应用密码，您可以确保只有拥有正确凭据的人才能进行更改。操作方法如下：

```csharp
//使用密码保护共享工作簿
wb.ProtectSharedWorkbook("1234");
```

在这种情况下，“1234”是我们的密码。您可以将其更改为您喜欢的任何密码。此命令锁定工作簿，防止未经授权的编辑。

## 步骤 4：（可选）取消保护工作簿

如果您改变主意或需要稍后编辑工作簿，您可以通过取消注释以下行轻松解锁。这就像拥有一把保险箱的钥匙：

```csharp
//取消注释此行以取消保护共享工作簿
//wb.解除共享工作簿保护(“1234”);
```

当您准备再次进行编辑时，只需使用正确的密码调用此方法。

## 步骤 5：保存输出 Excel 文件

最后一步是保存工作簿。这是您辛苦工作成果的存储地，供将来使用 — 就像在计算机上保存文档一样。

```csharp
//保存输出 Excel 文件
wb.Save(outputDir + "outputProtectSharedWorkbook.xlsx");
```

此行将受保护的工作簿保存在指定的输出目录中，名称为“outputProtectSharedWorkbook.xlsx”。 

## 步骤 6：验证执行

保存工作簿后，最好检查一下一切是否顺利。以下是一条简单的确认消息：

```csharp
Console.WriteLine("PasswordProtectOrUnprotectSharedWorkbook executed successfully.\r\n");
```

这样，您就会知道您的代码按预期执行，并且您的 Excel 文件已全部设置好！

## 结论

在本教程中，我们介绍了如何使用 Aspose.Cells for .NET 保护和取消保护共享工作簿。通过遵循这些步骤，您可以确保您的 Excel 文件保持安全，同时仍允许协作。无论您共享的是敏感的财务数据还是客户信息，在当今的环境中保护您的工作都至关重要。

## 常见问题解答

### 我可以使用更复杂的密码吗？
当然可以！您可以使用任何符合密码策略要求的字符串。

### 如果我忘记了密码该怎么办？
不幸的是，如果您忘记了密码，则如果不借助第三方工具或专家，您将无法取消对工作簿的保护。

### Aspose.Cells 可以免费使用吗？
 Aspose.Cells 是一款商业产品，但您可以通过免费试用版在有限的时间内免费试用：[免费试用](https://releases.aspose.com/).

### 有没有办法在其他编程语言中使用它？
Aspose.Cells 主要支持 .NET，但它们也有 Java 和其他语言的库。查看其网站了解更多信息！

### 如何获得 Aspose.Cells 的支持？
您可以通过他们的支持论坛寻求帮助：[Aspose 支持](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
