---
title: 以编程方式检测 Excel 中的循环引用
linktitle: 以编程方式检测 Excel 中的循环引用
second_title: Aspose.Cells .NET Excel 处理 API
description: 使用 Aspose.Cells for .NET 轻松检测 Excel 中的循环引用。按照我们的分步指南确保电子表格中的计算准确。
weight: 13
url: /zh/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 以编程方式检测 Excel 中的循环引用

## 介绍
在使用 Excel 文件时，您可能遇到的最令人沮丧的问题之一就是循环引用。当公式直接或间接引用其自己的单元格时，就会发生这种情况，从而创建一个可能使 Excel 计算引擎混乱的循环。但不要害怕！使用 Aspose.Cells for .NET，您可以以编程方式检测这些讨厌的循环引用，确保您的电子表格保持功能和准确性。在本指南中，我们将逐步引导您完成该过程，使其变得非常简单。
## 先决条件
在我们深入研究检测循环引用的细节之前，让我们确保您已准备好开始所需的一切：
1. Visual Studio：确保您的机器上安装了 Visual Studio。这将是您的开发环境。
2. .NET Framework：确保您使用的是兼容版本的 .NET Framework（至少是 .NET Framework 4.0）。
3.  Aspose.Cells 库：您需要有 Aspose.Cells 库。您可以从[Aspose 网站](https://releases.aspose.com/cells/net/).
4. C# 基础知识：熟悉 C# 编程将会很有益，因为我们将用这种语言编写代码。
5. Excel 文件：准备一个包含循环引用的 Excel 文件以供测试。您可以创建一个简单的文件或下载一个示例。
现在我们已经满足了先决条件，让我们进入有趣的部分！
## 导入包
在开始编码之前，您需要导入必要的软件包。操作方法如下：
### 创建新项目
- 打开 Visual Studio 并创建一个新的 C# 控制台应用程序项目。
### 添加 Aspose.Cells 引用
- 在解决方案资源管理器中右键单击您的项目。
- 选择“管理 NuGet 包”。
- 搜索“Aspose.Cells”并安装最新版本。
### 导入所需的命名空间
在你的顶部`Program.cs`文件，导入必要的命名空间：
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

现在我们已经完成所有设置，让我们深入研究代码以检测 Excel 文件中的循环引用。
## 步骤 1：定义输入目录
首先，您需要指定 Excel 文件所在的目录。这是您将加载 Excel 文件的位置。
```csharp
//输入目录
string sourceDir = "Your Document Directory";
```
代替`"Your Document Directory"`使用您的 Excel 文件的实际路径。
## 步骤 2：使用 LoadOptions 加载工作簿
接下来，您将加载 Excel 工作簿。这就是奇迹的开始！
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
在这里，我们创建一个新的实例`LoadOptions`并从指定路径加载工作簿。请确保您的 Excel 文件名匹配！
## 步骤 3：启用迭代设置
为了允许循环引用，您需要在工作簿中启用迭代设置。
```csharp
objWB.Settings.Iteration = true;
```
这告诉 Aspose.Cells 在计算期间允许循环引用。
## 步骤 4：创建计算选项和圆形监视器
现在，让我们创建计算选项和自定义圆形监视器。
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
在这里，我们创建一个实例`CalculationOptions`以及一个习俗`CircularMonitor`该监视器将有助于追踪计算过程中发现的任何循环引用。
## 步骤 5：计算公式
现在，是时候计算工作簿中的公式了。
```csharp
objWB.CalculateFormula(copts);
```
此行执行计算并检查循环引用。
## 步骤 6：计算循环引用
计算完毕之后，你就可以统计出发现了多少个循环引用。
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
这将输出在 Excel 文件中检测到的循环引用的数量。
## 步骤 7：显示结果
最后，让我们显示结果并确认我们的方法执行成功。
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## 步骤 8：实现 CircularMonitor 类
要完成此过程，您需要实施`CircularMonitor`类。此类将继承自`AbstractCalculationMonitor`并处理循环引用的检测。
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
此类捕获发现的每个循环引用的详细信息，包括工作表名称和单元格索引。
## 结论
使用 Aspose.Cells for .NET 检测 Excel 中的循环引用是一个简单的过程，只要将其分解为可管理的步骤即可。按照本指南，您可以轻松识别和处理电子表格中的循环引用，确保您的计算保持准确可靠。无论您是经验丰富的开发人员还是刚刚起步，Aspose.Cells 都能提供强大的工具来增强您的 Excel 操作能力。 
## 常见问题解答
### Excel 中的循环引用是什么？
当公式引用其自己的单元格时，就会发生循环引用，从而导致计算无限循环。
### 如何以编程方式检测循环引用？
您可以使用.NET 中的 Aspose.Cells 库通过实现自定义计算监视器以编程方式检测循环引用。
### 使用 Aspose.Cells 的先决条件是什么？
您需要安装 Visual Studio、.NET Framework 和 Aspose.Cells 库。
### 我可以免费使用 Aspose.Cells 吗？
是的，Aspose.Cells 提供免费试用，您可以使用它来探索其功能。
### 在哪里可以找到有关 Aspose.Cells 的更多信息？
您可以访问[Aspose.Cells 文档](https://reference.aspose.com/cells/net/)了解详细信息和示例。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
