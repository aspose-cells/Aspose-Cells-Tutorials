---
title: 将数字签名添加到已签名的 Excel 文件
linktitle: 将数字签名添加到已签名的 Excel 文件
second_title: Aspose.Cells for .NET API 参考
description: 通过详细的分步指南了解如何使用 Aspose.Cells for .NET 将数字签名添加到已签名的 Excel 文件。
weight: 30
url: /zh/net/excel-workbook/add-digital-signature-to-an-already-signed-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 将数字签名添加到已签名的 Excel 文件

## 介绍

在当今的数字世界中，保护文档比以往任何时候都更加重要。数字签名提供了一种确保文件真实性和完整性的方法，尤其是在处理敏感信息时。如果您正在使用 Excel 文件并希望向已签名的工作簿添加新的数字签名，那么您来对地方了！在本指南中，我们将引导您完成使用 Aspose.Cells for .NET 向已签名的 Excel 文件添加数字签名的过程。那么，让我们开始吧！

## 先决条件

在我们深入讨论编码细节之前，您需要做好以下几件事：

1.  Aspose.Cells for .NET：确保您已在 .NET 项目中安装了 Aspose.Cells 库。您可以从[地点](https://releases.aspose.com/cells/net/).
2. 证书文件：您需要一个有效的证书文件（通常是`.pfx`包含数字证书的文件。请确保您知道此文件的密码。
3. 开发环境：使用 Visual Studio 或任何其他支持 .NET 的 IDE 设置您的开发环境。
4. C# 基础知识：熟悉 C# 编程将帮助您顺利跟上。
5. 示例文件：准备一个已经过数字签名的示例 Excel 文件。您将向该文件添加新签名。

现在一切就绪，让我们开始编码吧！

## 导入包

首先，您需要在 C# 文件中导入必要的包。操作方法如下：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

这些命名空间将允许您处理 Excel 文件并无缝处理数字签名。

## 步骤 1：设置源目录和输出目录

在操作 Excel 文件之前，您需要定义源文件的位置以及要保存输出文件的位置。操作方法如下：

```csharp
//源目录
string sourceDir = "Your Document Directory";
//输出目录
string outputDir = "Your Document Directory";
```

在此步骤中，我们使用一种方法来获取源目录和输出目录的路径。确保这些目录存在并包含所需的文件。

## 步骤 2：加载已签名的工作簿

接下来，您需要加载要修改的 Excel 工作簿。这是通过创建`Workbook`类并传递签名文件的路径。

```csharp
//加载已经过数字签名的工作簿
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```

这里，我们正在加载名为`sampleDigitallySignedByCells.xlsx`确保此文件已经签名。

## 步骤 3：创建数字签名集合

现在，让我们创建一个数字签名集合。此集合将保存您要添加到工作簿的所有数字签名。

```csharp
//创建数字签名集合
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```

这一步至关重要，因为它允许您在需要时管理多个签名。

## 步骤 4：创建新证书

您需要加载证书文件来创建新的数字签名。在这里您可以指定`.pfx`文件及其密码。

```csharp
//证书文件及其密码
string certFileName = sourceDir + "AsposeDemo.pfx";
string password = "aspose";

//创建新证书
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```

确保更换`AsposeDemo.pfx`并将密码替换为您的实际的证书文件名和密码。

## 步骤 5：创建数字签名

有了证书，您现在可以创建数字签名了。您还需要提供签名的原因以及当前日期和时间。

```csharp
//创建新的数字签名并将其添加到数字签名集合中
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
```

此步骤将新签名添加到您的收藏中，您稍后可将其应用到工作簿。

## 步骤 6：将数字签名集合添加到工作簿

现在是时候将数字签名集合添加到工作簿了。这就是奇迹发生的地方！

```csharp
//在工作簿中添加数字签名集合
workbook.AddDigitalSignature(dsCollection);
```

通过执行此行，您可以有效地将新的数字签名附加到已签名的工作簿。

## 步骤 7：保存并处理工作簿

最后，您需要将修改后的工作簿保存到输出目录并释放正在使用的任何资源。

```csharp
//保存工作簿并处理。
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```

此步骤确保您的更改被保存，并且工作簿被正确处理以释放资源。

## 步骤8：确认执行

最后，最好确认一下代码是否成功执行。您可以使用一条简单的控制台消息来确认。

```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```

这提供了操作成功的反馈，这总是令人高兴的！

## 结论

就这样！您已成功使用 Aspose.Cells for .NET 向已签名的 Excel 文件添加了新的数字签名。数字签名是确保文档真实性的强大方法，现在您知道如何以编程方式管理它们。无论您处理的是财务文件、合同还是任何敏感信息，实施数字签名都可以增强安全性和信任度。

## 常见问题解答

### 什么是数字签名？
数字签名是一种用于验证消息或文档的真实性和完整性的加密方法。

### 我可以在同一个 Excel 文件中添加多个数字签名吗？
是的，您可以创建数字签名集合并将多个签名添加到同一个工作簿。

### Aspose.Cells 支持哪些格式的数字签名？
 Aspose.Cells 支持多种格式，包括`.pfx`用于证书。

### 我需要特定版本的.NET 才能使用 Aspose.Cells 吗？
检查[Aspose.Cells 文档](https://reference.aspose.com/cells/net/)为了与您的.NET 版本兼容。

### 如何获得 Aspose.Cells 的临时许可证？
您可以从申请临时许可证[Aspose 的购买页面](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
