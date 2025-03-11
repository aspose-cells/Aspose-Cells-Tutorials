---
title: 使用中断监视器停止转换或加载
linktitle: 使用中断监视器停止转换或加载
second_title: Aspose.Cells .NET Excel 处理 API
description: 通过详细的分步教程学习如何使用中断监视器停止 Aspose.Cells for .NET 中的工作簿转换。
weight: 26
url: /zh/net/workbook-operations/stop-conversion-or-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用中断监视器停止转换或加载

## 介绍
处理大型 Excel 文件通常涉及冗长的过程，这会耗费时间和资源。但是，如果您在意识到需要更改某些内容时可以中途停止转换过程，会怎么样？Aspose.Cells for .NET 具有一项称为“中断监视器”的功能，它允许您中断工作簿转换为其他格式（如 PDF）。这可以拯救您的生命，尤其是在处理大量数据文件时。在本指南中，我们将介绍如何使用 Aspose.Cells for .NET 中的“中断监视器”中断转换过程。
## 先决条件
在开始之前，请确保您已做好以下准备：
1.  Aspose.Cells for .NET - 下载[这里](https://releases.aspose.com/cells/net/).
2. .NET 开发环境 - 例如 Visual Studio。
3. C# 编程的基础知识 - 熟悉 C# 语法将帮助您跟上。
## 导入包
首先，让我们导入必要的包。这些导入包括：
- Aspose.Cells：操作Excel文件的主要库。
- System.Threading：用于管理线程，因为本例将运行两个并行进程。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
让我们将这个过程分解成详细的步骤。每个步骤都将帮助您了解设置和使用中断监视器对管理 Excel 工作簿转换的重要性。
## 步骤 1：创建类并设置输出目录
首先，我们需要一个类来封装我们的函数，以及一个保存输出文件的目录。
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
代替`"Your Document Directory"`与您想要保存 PDF 文件的实际路径一致。
## 步骤 2：实例化中断监视器
接下来，创建一个 InterruptMonitor 对象。该监视器将通过设置在任意给定点中断的能力来帮助控制该过程。
```csharp
InterruptMonitor im = new InterruptMonitor();
```
该中断监视器将附加到我们的工作簿，使我们能够管理转换过程。
## 步骤 3：设置转换工作簿
现在，让我们创建一个工作簿对象，将 InterruptMonitor 分配给它，然后访问第一个工作表来插入一些示例文本。
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
上述代码创建了一个工作簿，为其设置了 InterruptMonitor，并将文本放在远处的单元格中 (`J1000000`）。将文本放置在此单元格位置可确保处理工作簿更加耗时，从而为 InterruptMonitor 提供足够的时间进行干预。
## 步骤 4：将工作簿保存为 PDF 并处理中断
现在，让我们尝试将工作簿保存为 PDF。我们将使用`try-catch`块来处理可能发生的任何中断。
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
如果该过程被中断，异常将捕获它并显示适当的消息。否则，工作簿将保存为 PDF。
## 步骤5：中断转换过程
这里的主要功能是能够中断该过程。我们将使用`Thread.Sleep`然后调用`Interrupt()`方法在 10 秒后停止转换。
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
此延迟使工作簿有时间在发送中断信号之前开始转换为 PDF。
## 步骤 6：同时执行线程
为了将所有内容整合在一起，我们需要在单独的线程中启动这两个函数。这样，工作簿转换和中断等待就可以同时进行。
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
上面的代码运行`CreateWorkbookAndConvertItToPdfFormat`和`WaitForWhileAndThenInterrupt`在并行线程中，一旦两个进程都完成，它们就会合并在一起。
## 步骤 7：最终执行
最后，我们添加一个`Run()`方法来执行代码。
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
这`Run`方法是启动和观察中断操作的入口点。
## 结论
在本教程中，我们探讨了如何在 Aspose.Cells for .NET 中中断转换过程。中断监视器在处理大型 Excel 文件时非常有用，它允许您停止进程而无需等待它们完成。这在时间和资源宝贵且需要快速反馈的情况下尤其有用。
## 常见问题解答
### Aspose.Cells for .NET 中的中断监视器是什么？  
中断监视器可让您中途停止工作簿的转换或加载过程。
### 除了 PDF 之外，我可以将中断监视器用于其他格式吗？  
是的，您也可以中断向其他支持格式的转换。
### Thread.Sleep() 如何影响中断时间？  
Thread.Sleep() 在触发中断之前会产生延迟，从而为转换开始提供时间。
### 我可以在10秒之前中断该过程吗？  
是的，修改延迟`WaitForWhileAndThenInterrupt()`更短的时间。
### 中断过程是否会影响性能？  
影响很小，并且对于管理长期运行的流程非常有益。
有关详细信息，请参阅[Aspose.Cells for .NET 文档](https://reference.aspose.com/cells/net/)。如果您需要帮助，请查看[支持论坛](https://forum.aspose.com/c/cells/9)或者得到[免费试用](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
