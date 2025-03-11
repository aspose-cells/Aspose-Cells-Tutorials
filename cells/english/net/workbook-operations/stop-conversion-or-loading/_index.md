---
title: Stop Conversion or Loading using Interrupt Monitor
linktitle: Stop Conversion or Loading using Interrupt Monitor
second_title: Aspose.Cells .NET Excel Processing API
description: Learn to stop workbook conversion in Aspose.Cells for .NET using Interrupt Monitor, with detailed, step-by-step tutorial.
weight: 26
url: /net/workbook-operations/stop-conversion-or-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Stop Conversion or Loading using Interrupt Monitor

## Introduction
Working with large Excel files often involves lengthy processes that can eat up time and resources. But what if you could stop the conversion process mid-way when you realize something needs changing? Aspose.Cells for .NET has a feature called the Interrupt Monitor, which allows you to interrupt a workbook's conversion to another format like PDF. This can be a lifesaver, especially when working with substantial data files. In this guide, we’ll walk through how to interrupt the conversion process using the Interrupt Monitor in Aspose.Cells for .NET.
## Prerequisites
Before diving in, make sure you have the following in place:
1. Aspose.Cells for .NET - Download it [here](https://releases.aspose.com/cells/net/).
2. .NET Development Environment - Such as Visual Studio.
3. Basic Knowledge of C# Programming - Familiarity with C# syntax will help you follow along.
## Import Packages
To start, let’s import the necessary packages. These imports include:
- Aspose.Cells: The main library for manipulating Excel files.
- System.Threading: For managing threads, as this example will run two parallel processes.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
Let's break down the process into detailed steps. Each step will help you understand the importance of setting up and using the Interrupt Monitor for managing Excel workbook conversion.
## Step 1: Create the Class and Set Output Directory
First, we need a class to encapsulate our functions, along with a directory where the output file will be saved.
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
Replace `"Your Document Directory"` with the actual path where you want the PDF file to be saved.
## Step 2: Instantiate the Interrupt Monitor
Next, create an InterruptMonitor object. This monitor will help control the process by setting up the capability to interrupt it at any given point.
```csharp
InterruptMonitor im = new InterruptMonitor();
```
This interrupt monitor will be attached to our workbook, allowing us to manage the conversion process.
## Step 3: Set Up the Workbook for Conversion
Now, let’s create a workbook object, assign the InterruptMonitor to it, and then access the first worksheet to insert some sample text.
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
The code above creates a workbook, sets the InterruptMonitor for it, and places text in a far cell (`J1000000`). Placing text at this cell position ensures that processing the workbook will be more time-consuming, giving the InterruptMonitor enough time to intervene.
## Step 4: Save Workbook as PDF and Handle Interruption
Now, let’s attempt to save the workbook as a PDF. We’ll use a `try-catch` block to handle any interruption that might occur.
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
If the process is interrupted, the exception will catch it and display an appropriate message. Otherwise, the workbook will save as a PDF.
## Step 5: Interrupt the Conversion Process
The main feature here is the ability to interrupt the process. We’ll add a delay using `Thread.Sleep` and then call the `Interrupt()` method to stop the conversion after 10 seconds.
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
This delay gives the workbook time to start converting to PDF before the interrupt signal is sent.
## Step 6: Execute the Threads Simultaneously
To bring everything together, we need to start both functions in separate threads. This way, the workbook conversion and the interrupt wait can occur simultaneously.
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
The code above runs `CreateWorkbookAndConvertItToPdfFormat` and `WaitForWhileAndThenInterrupt` in parallel threads, joining them once both processes have finished.
## Step 7: Final Execution
Finally, we’ll add a `Run()` method to execute the code.
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
This `Run` method is the entry point to start and observe the interruption in action.
## Conclusion
In this tutorial, we explored how to interrupt the conversion process in Aspose.Cells for .NET. The Interrupt Monitor is a helpful tool when working with large Excel files, allowing you to stop processes without waiting for them to complete. This is especially useful in scenarios where time and resources are precious, and quick feedback is needed.
## FAQ's
### What is an Interrupt Monitor in Aspose.Cells for .NET?  
The Interrupt Monitor lets you stop a workbook conversion or load process partway through.
### Can I use Interrupt Monitor for other formats besides PDF?  
Yes, you can interrupt conversions to other supported formats as well.
### How does Thread.Sleep() affect the interrupt timing?  
Thread.Sleep() creates a delay before triggering the interrupt, giving time for the conversion to start.
### Can I interrupt the process before 10 seconds?  
Yes, modify the delay in `WaitForWhileAndThenInterrupt()` to a shorter time.
### Will the interrupt process impact performance?  
The impact is minimal, and it’s highly beneficial for managing long-running processes.
For more information, refer to the [Aspose.Cells for .NET Documentation](https://reference.aspose.com/cells/net/). If you need help, check out the [Support Forum](https://forum.aspose.com/c/cells/9) or get a [Free Trial](https://releases.aspose.com/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
