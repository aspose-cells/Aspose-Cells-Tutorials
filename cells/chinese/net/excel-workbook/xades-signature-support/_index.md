---
title: Xades 签名支持
linktitle: Xades 签名支持
second_title: Aspose.Cells for .NET API 参考
description: 通过本分步指南了解如何使用 Aspose.Cells for .NET 将 Xades 签名添加到 Excel 文件。保护您的文档。
weight: 190
url: /zh/net/excel-workbook/xades-signature-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xades 签名支持

## 介绍

在当今的数字世界中，保护文档比以往任何时候都更加重要。无论您处理的是敏感的商业信息还是个人数据，确保文件的完整性和真实性都是至关重要的。实现这一点的一种方法是通过数字签名，特别是 Xades 签名。如果您是一名 .NET 开发人员，希望在您的应用程序中实现 Xades 签名支持，那么您来对地方了！在本指南中，我们将引导您完成使用 Aspose.Cells for .NET 将 Xades 签名添加到 Excel 文件的过程。那么，让我们开始吧！

## 先决条件

在开始之前，您需要准备好以下几件事：

1.  Aspose.Cells for .NET：确保已安装 Aspose.Cells 库。您可以从[Aspose 网站](https://releases.aspose.com/cells/net/).
2. 开发环境：一个可用的 .NET 开发环境（如 Visual Studio），您可以在其中编写和执行代码。
3. 数字证书：您需要一个有效的数字证书（PFX 文件）及其密码。此证书对于创建数字签名至关重要。
4. C# 基础知识：熟悉 C# 编程将帮助您更好地理解示例。

一旦您满足了这些先决条件，您就可以开始在 Excel 文件中实现 Xades 签名了！

## 导入包

要使用 Aspose.Cells for .NET，您需要导入必要的命名空间。具体操作如下：

```csharp
using Aspose.Cells.DigitalSignatures;
using System;
using System.IO;
```

这些命名空间提供处理 Excel 文件和管理数字签名所需的类和方法的访问。

现在我们已经完成所有设置，让我们将向 Excel 文件添加 Xades 签名的过程分解为清晰、易于管理的步骤。

## 步骤 1：设置源目录和输出目录

首先，我们需要确定源 Excel 文件的位置以及我们要保存签名输出文件的位置。这是一个至关重要的步骤，因为它有助于有效地组织文件。

```csharp
//源目录
string sourceDir = "Your Document Directory";
//输出目录
string outputDir = "Your Output Directory";
```

## 步骤 2：加载工作簿

接下来，让我们加载要签名的 Excel 工作簿。这是您将加载现有 Excel 文件的地方。

```csharp
Workbook workbook = new Workbook(sourceDir + "sourceFile.xlsx");
```

在这里，我们创建一个新的实例`Workbook`类，传递源 Excel 文件的路径。确保文件名与源目录中的文件名匹配。

## 步骤 3：准备您的数字证书

要创建数字签名，您需要加载数字证书。这涉及读取 PFX 文件并提供其密码。

```csharp
string password = "pfxPassword"; //替换为您的 PFX 密码
string pfx = "pfxFile"; //替换为 PFX 文件的路径
```

在此步骤中，替换`pfxPassword`使用您的实际密码`pfxFile`以及 PFX 文件的路径。这是签署文档的关键！

## 步骤 4：创建数字签名

现在，让我们使用`DigitalSignature`课堂上。这就是奇迹发生的地方！

```csharp
DigitalSignature signature = new DigitalSignature(File.ReadAllBytes(pfx), password, "testXAdES", DateTime.Now);
signature.XAdESType = XAdESType.XAdES;
```

在此代码片段中，我们将 PFX 文件读入字节数组并创建一个新的`DigitalSignature`对象。我们还设置了`XAdESType`到`XAdES`，这对于我们的签名至关重要。

## 步骤 5：将签名添加到工作簿

创建数字签名后，下一步是将其添加到工作簿。

```csharp
DigitalSignatureCollection dsCollection = new DigitalSignatureCollection();
dsCollection.Add(signature);
workbook.SetDigitalSignature(dsCollection);
```

在这里，我们创建一个`DigitalSignatureCollection`，在其中添加我们的签名，然后将此集合设置为工作簿。这就是我们将签名附加到 Excel 文件的方式。

## 步骤 6：保存已签名的工作簿

最后，是时候将签名的工作簿保存到输出目录了。此步骤完成了整个过程。

```csharp
workbook.Save(outputDir + "XAdESSignatureSupport_out.xlsx");
Console.WriteLine("XAdESSignatureSupport executed successfully.");
```

在此代码中，我们用新名称保存工作簿，`XAdESSignatureSupport_out.xlsx`，在输出目录中。完成此步骤后，您将在控制台中看到一条成功消息。

## 结论

就这样！您已成功使用 Aspose.Cells for .NET 将 Xades 签名添加到 Excel 文件中。此过程不仅可以增强文档的安全性，还可以通过确保文件的真实性来与用户建立信任。 
数字签名是现代文档管理的重要组成部分，借助 Aspose.Cells 的强大功能，您可以轻松地在应用程序中实现它们。

## 常见问题解答

### Xades 签名是什么？
Xades（XML 高级电子签名）是一种数字签名标准，它提供了用于确保电子文档的完整性和真实性的附加功能。

### 我需要数字证书来创建 Xades 签名吗？
是的，您需要一个有效的数字证书（PFX 文件）来创建 Xades 签名。

### 我可以在购买之前测试 Aspose.Cells for .NET 吗？
当然！你可以从[Aspose 网站](https://releases.aspose.com/).

### Aspose.Cells 是否与所有版本的.NET 兼容？
Aspose.Cells 支持 .NET 框架的各种版本。检查[文档](https://reference.aspose.com/cells/net/)了解兼容性详细信息。

### 如果我遇到问题，可以在哪里获得支持？
您可以访问[Aspose 论坛](https://forum.aspose.com/c/cells/9)寻求社区的支持和援助。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
