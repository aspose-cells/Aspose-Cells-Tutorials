---
title: 使用 Aspose.Cells 将 VBAMacro 用户表单设计器存储复制到工作簿
linktitle: 使用 Aspose.Cells 将 VBAMacro 用户表单设计器存储复制到工作簿
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过我们全面的分步教程学习如何在 Aspose.Cells for .NET 中高效复制 VBA 宏用户表单设计器！释放 Excel 的潜力。
weight: 11
url: /zh/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 将 VBAMacro 用户表单设计器存储复制到工作簿

## 介绍
欢迎！如果您希望通过 VBA 宏和用户表单增强您的 Excel 体验，那么您来对地方了！在本指南中，我们将深入介绍如何使用 Aspose.Cells for .NET 将 VBA 宏用户表单设计器从一个工作簿无缝复制到另一个工作簿。无论您是经验丰富的开发人员还是刚刚入门，我们都会引导您完成每个关键步骤。将其视为您掌握以编程方式处理 Excel 文件的技巧的剧本。准备好了吗？我们走吧！
## 先决条件
在我们深入编码细节之前，让我们确保您已准备好所需的一切：
1. C# 开发环境：您应该有一个可用于 C# 开发的工作环境。强烈推荐使用 Visual Studio。
2.  Aspose.Cells for .NET 库：确保已将 Aspose.Cells 库集成到项目中。您可以轻松[点击下载](https://releases.aspose.com/cells/net/).
3. VBA 和 Excel 宏的基本知识：充分了解 VBA 以及 Excel 宏的工作原理将帮助您轻松完成本教程。
4. 带有用户表单的 Excel 文件：为了进行实验，请创建或获取包含用户表单的 Excel 工作簿，最好启用宏（例如`.xlsm`文件）。
## 导入包
在您的 C# 项目中，您需要在文件顶部导入某些命名空间以利用 Aspose.Cells 功能。操作方法如下：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
包括这些命名空间允许您访问 Aspose.Cells 库中嵌入的所有强大的工具。 
现在我们已经了解了先决条件和软件包，是时候进入有趣的部分了：编码！让我们一步一步地分解。
## 步骤 1：定义源和输出目录
首先，您需要确定文件所在的位置：
```csharp
//源目录
string sourceDir = "Your Document Directory";
//输出目录
string outputDir = "Your Document Directory";
```
在这里，替换`"Your Document Directory"`替换为文件存储的实际路径。这是我们获取源工作簿（包含用户窗体）的位置，也是保存新工作簿的位置。
## 步骤 2：创建空目标工作簿
接下来，让我们创建目标工作簿，在其中复制用户表单和宏：
```csharp
//创建空的目标工作簿
Workbook target = new Workbook();
```
这行代码初始化了一个新的空工作簿，供我们填充数据。可以把它想象成您杰作的空白画布！
## 步骤 3：加载模板工作簿
我们需要加载包含您的用户表单和宏的工作簿：
```csharp
//加载包含 VBA-Macro Designer 用户表单的 Excel 文件
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
确保改变`"sampleDesignerForm.xlsm"`到您的实际文件的名称。此工作簿就像您的食谱书 - 我们会从中获取食材！
## 步骤 4：将工作表复制到目标工作簿
现在，让我们开始将工作表从模板复制到目标工作簿：
```csharp
//将所有模板工作表复制到目标工作簿
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        //将消息放入目标工作表的 A2 单元格中
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
在此步骤中，我们将循环遍历模板中的每个工作表并将其复制到目标工作簿中。如果您仔细想想，这就像将您最好的食谱从一本食谱转移到另一本食谱中一样！
## 步骤 5：从模板复制 VBA 宏
接下来，我们将 VBA 宏（包括 UserForm Designer 模块）复制到我们的新工作簿中：
```csharp
//将 VBA 宏设计器用户窗体从模板复制到目标
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        //复制 ThisWorkbook 模块代码
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        //复制其他模块的代码和数据
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            //获取用户表单即设计器存储的数据
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            //将设计器存储添加到目标 Vba 项目
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
这大段代码负责检查模板文件中的每个 VBA 模块。我们正在复制 UserForm 设计及其相关代码。这就像确保您不仅能获得奶奶著名的馅饼食谱，还能获得她确切的烘焙技巧！
## 步骤 6：保存目标工作簿
完成所有副本后，就该保存我们的辛苦工作成果了：
```csharp
//保存目标工作簿
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
确保根据需要修改输出文件名。保存后，您就可以有效地创建自己的定制版本的工作簿，其中包含宏和用户表单。这有多令人兴奋？
## 步骤 7：确认成功
最后，让我们向控制台打印一条成功消息：
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
这行字让你确信你的过程进展顺利。这是你编码圣代上的点睛之笔！
## 结论
恭喜！您已完成使用 Aspose.Cells for .NET 将 VBA 宏用户表单设计器从一个工作簿复制到另一个工作簿的分步指南。一开始可能看起来有点不知所措，但通过练习，您将像专业人士一样处理工作簿操作。请记住，编码完全取决于练习，因此不要害怕在 Excel 文件中尝试不同的东西。如果您有任何疑问或遇到任何问题，请随时查看 Aspose 论坛或文档以获取支持！
## 常见问题解答
### Aspose.Cells 支持哪些版本的 Excel？
Aspose.Cells 支持多种 Excel 格式，包括 XLSX、XLSM、CSV 等。
### 我可以免费使用 Aspose.Cells 吗？
是的！您可以先免费试用，以便评估该库：[免费试用](https://releases.aspose.com/).
### 我需要 Visual Studio 来运行此代码吗？
虽然它由于用户友好的功能而受到强烈推荐，但只要它支持.NET 开发，任何 C# IDE 都可以。
### 在哪里可以找到更多示例和文档？
您可以探索[Aspose.Cells 文档](https://reference.aspose.com/cells/net/)以获取更多示例和深入解释。
### 如何解决使用 Aspose.Cells 时出现的问题？
你应该访问[Aspose 支持论坛](https://forum.aspose.com/c/cells/9)寻求社区和 Aspose 支持人员的帮助。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
