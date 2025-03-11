---
title: 为已签名的 Excel 文件添加数字签名
linktitle: 为已签名的 Excel 文件添加数字签名
second_title: Aspose.Cells .NET Excel 处理 API
description: 在本分步指南中了解如何使用 Aspose.Cells for .NET 将数字签名添加到已签名的 Excel 文件。保护您的文档。
weight: 12
url: /zh/net/workbook-operations/add-digital-signature-to-signed-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 为已签名的 Excel 文件添加数字签名

## 介绍
在当今的数字世界中，确保文件的真实性和完整性至关重要。数字签名是一种可靠的方法，可以验证文档未被更改且来自合法来源。如果您在 .NET 中使用 Excel 文件并希望向已签名的文件添加数字签名，那么您来对地方了！在本指南中，我们将引导您完成使用 Aspose.Cells for .NET 向现有签名的 Excel 文件添加新数字签名的过程。 
## 先决条件
在我们深入讨论细节之前，让我们确保您已准备好开始所需的一切：
1.  Aspose.Cells for .NET：首先，您需要在 .NET 环境中安装 Aspose.Cells。您可以从[发布页面](https://releases.aspose.com/cells/net/).
2. .NET Framework：确保您的机器上已安装 .NET Framework。本指南假定您熟悉基本的 .NET 编程概念。
3. 数字证书：您需要有效的数字证书（.pfx 格式）来创建数字签名。如果您没有，可以创建自签名证书用于测试目的。
4. 开发环境：代码编辑器或 IDE（如 Visual Studio），您可以在其中编写和执行 C# 代码。
5. 示例 Excel 文件：您应该有一个已进行数字签名的现有 Excel 文件。我们将向该文件添加另一个签名。
满足了这些先决条件后，我们就可以开始编写代码了！
## 导入包
在开始编码之前，请确保导入必要的命名空间。以下是您需要在 C# 文件顶部包含的内容：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
这些命名空间将使您能够访问操作 Excel 文件和处理数字签名所需的类和方法。
现在，让我们将这个过程分解成几个可管理的步骤。我们将逐一介绍每个步骤，以确保您了解如何向已签名的 Excel 文件添加数字签名。
## 步骤 1：定义目录
首先，你需要指定源文件的位置以及保存输出文件的位置。这很简单，但至关重要：
```csharp
//源目录
string sourceDir = "Your Document Directory"; //替换为您的实际目录
//输出目录
string outputDir = "Your Document Directory"; //替换为您的实际目录
```
代替`"Your Document Directory"`替换为文件存储的实际路径。这将为文件操作奠定基础。
## 步骤 2：加载现有的签名工作簿
接下来，您将加载已签名的现有 Excel 工作簿。这就是魔法开始的地方：
```csharp
//加载已经数字签名的工作簿以添加新的数字签名
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```
这行初始化一个新的`Workbook`对象与指定文件。请确保文件名与您现有的已签名 Excel 文件匹配。
## 步骤 3：创建数字签名集合
要管理您的数字签名，您需要创建一个集合。这样您就可以在需要时保存多个签名：
```csharp
//创建数字签名集合
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```
在将新的数字签名应用到工作簿之前，您可以在此集合中添加它。
## 步骤 4：加载证书
现在，是时候加载您的数字证书了。此证书将用于创建新的签名：
```csharp
//证书文件及其密码
string certFileName = sourceDir + "AsposeDemo.pfx"; //您的证书文件
string password = "aspose"; //您的证书密码
//创建新证书
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```
确保更换`AsposeDemo.pfx`替换为证书文件的名称并相应地更新密码。此步骤至关重要，因为如果没有正确的证书，您将无法创建有效的签名。
## 步骤 5：创建新的数字签名
加载证书后，您现在可以创建新的数字签名。此签名将添加到您的收藏中：
```csharp
//创建新的数字签名并将其添加到数字签名集合中
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
dsCollection.Add(signature);
```
在这里，您提供了一条描述签名的消息，这有助于记录保存。时间戳可确保签名与正确的时间点相关联。
## 步骤 6：将签名集合添加到工作簿
创建签名后，就可以将整个集合添加到工作簿了：
```csharp
//在工作簿中添加数字签名集合
workbook.AddDigitalSignature(dsCollection);
```
此步骤可有效地将您的新数字签名应用到工作簿，并标记其增加的真实性。
## 步骤 7：保存工作簿
最后，保存包含新数字签名的工作簿。这是您所有辛勤工作得到回报的时刻：
```csharp
//保存工作簿并处理。
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```
确保为输出文件指定一个名称。这将是您的 Excel 文件的新版本，并带有附加的数字签名。
## 步骤8：确认成功
总而言之，操作成功完成后提供反馈是个好主意：
```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```
此行将向控制台打印一条确认消息，让您知道一切顺利。
## 结论
就这样！您已成功使用 Aspose.Cells for .NET 向已签名的 Excel 文件添加了新的数字签名。此过程不仅增强了文档的安全性，还确保了文档的可信度和可验证性。 
在当今的数字环境中，数字签名至关重要，尤其是对于需要维护文档完整性的企业和专业人士而言。按照本指南，您可以轻松管理 Excel 文件中的数字签名，确保您的数据保持安全和真实。
## 常见问题解答
### 什么是数字签名？
数字签名是一种用于验证数字信息或文档的真实性和完整性的数学方案。它确保文档未被更改并确认签名者的身份。
### 我是否需要特殊证书来创建数字签名？
是的，您需要由受信任的证书颁发机构 (CA) 颁发的数字证书来创建有效的数字签名。
### 我可以使用自签名证书进行测试吗？
当然可以！您可以创建自签名证书用于开发和测试目的，但对于生产，最好使用来自受信任 CA 的证书。
### 如果我尝试在未签名的文档中添加签名会发生什么？
如果您尝试将数字签名添加到尚未签名的文档中，它将正常工作，但原始签名将不存在。
### 在哪里可以找到有关 Aspose.Cells 的更多信息？
您可以检查[Aspose.Cells 文档](https://reference.aspose.com/cells/net/)以获取详细指南和 API 参考。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
