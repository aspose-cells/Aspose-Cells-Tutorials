---
title: Adjust Compression Level in Workbook
linktitle: Adjust Compression Level in Workbook
second_title: Aspose.Cells .NET Excel Processing API
description: Learn how to adjust the compression level of Excel workbooks using Aspose.Cells for .NET with this step-by-step guide. Optimize your file management.
weight: 14
url: /net/workbook-operations/adjust-compression-level/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Adjust Compression Level in Workbook

## Introduction
When it comes to managing large Excel files, compression is a game changer. Not only does it save storage space, but it also makes file transfers faster and more efficient. If you're working with Aspose.Cells for .NET, you can easily adjust the compression level of your workbooks. In this guide, we’ll walk you through the process step-by-step, ensuring that you understand each part of the code and how it works.
## Prerequisites
Before diving into the code, there are a few prerequisites you need to have in place:
1. Basic Knowledge of C#: Familiarity with C# programming will help you understand the code snippets better.
2. Aspose.Cells Library: You need to have the Aspose.Cells library installed. You can download it from [here](https://releases.aspose.com/cells/net/).
3. Visual Studio: A development environment like Visual Studio will be necessary to run the code.
4. .NET Framework: Ensure that your project is set up with a compatible version of the .NET Framework.
## Import Packages
To get started, you need to import the necessary packages in your C# project. Here’s how you can do it:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
```
These packages are essential for working with Excel files using the Aspose.Cells library. The `Aspose.Cells` namespace contains all the classes you need to manipulate Excel files, while `Aspose.Cells.Xlsb` provides the options for saving files in the XLSB format.
Now, let’s break down the process of adjusting the compression level in a workbook into manageable steps.
## Step 1: Define Source and Output Directories
First, you need to specify where your source files are located and where you want to save the output files. This is crucial for ensuring that your program knows where to find the files it needs to work with.
```csharp
// Source directory
string sourceDir = "Your Document Directory";
string outDir = "Your Document Directory";
```
Replace `"Your Document Directory"` with the actual path to your directories. This will help the program locate the files you want to compress.
## Step 2: Load the Workbook
Next, you’ll load the workbook that you want to compress. This is where the magic begins!
```csharp
Workbook workbook = new Workbook(sourceDir + "LargeSampleFile.xlsx");
```
In this line, we create a new instance of the `Workbook` class and load an existing Excel file. Make sure that the file name matches the one you have in your source directory.
## Step 3: Set Up Save Options
Now it’s time to configure the save options. We will set the compression type for the output file. 
```csharp
XlsbSaveOptions options = new XlsbSaveOptions();
```
The `XlsbSaveOptions` class allows you to specify various options when saving your workbook in the XLSB format, including compression levels.
## Step 4: Measure Compression Time for Level 1
Let’s start with the first compression level. We will measure how long it takes to save the workbook with this level of compression.
```csharp
options.CompressionType = OoxmlCompressionType.Level1;
var watch = Stopwatch.StartNew();
workbook.Save(outDir + "LargeSampleFile_level_1_out.xlsb", options);
watch.Stop();
var elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 1 Elapsed Time: " + elapsedMs);
```
Here, we set the compression type to Level 1, save the workbook, and then measure the elapsed time. This gives us an idea of how long the process takes.
## Step 5: Measure Compression Time for Level 6
Next, let’s see how Level 6 compression performs.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level6;
workbook.Save(outDir + "LargeSampleFile_level_6_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 6 Elapsed Time: " + elapsedMs);
```
This step is similar to the previous one, but we change the compression level to Level 6. You’ll notice that the time taken might vary based on the complexity of the workbook.
## Step 6: Measure Compression Time for Level 9
Finally, let’s check out the performance with the highest compression level.
```csharp
watch = Stopwatch.StartNew();
options.CompressionType = OoxmlCompressionType.Level9;
workbook.Save(outDir + "LargeSampleFile_level_9_out.xlsb", options);
watch.Stop();
elapsedMs = watch.ElapsedMilliseconds;
Console.WriteLine("Level 9 Elapsed Time: " + elapsedMs);
```
In this step, we set the compression level to Level 9. This is where you’ll typically see the most significant reduction in file size, but it may take longer to process.
## Step 7: Final Output
After running all the compression levels, you can output a message indicating that the process has completed successfully.
```csharp
Console.WriteLine("AdjustCompressionLevel executed successfully.");
```
This simple line of code confirms that your program has finished executing without any hitches.
## Conclusion
Adjusting the compression level of your workbooks using Aspose.Cells for .NET is a straightforward process that can lead to significant benefits in terms of file size and performance. By following the steps outlined in this guide, you can easily implement compression in your applications and improve the efficiency of your Excel file management.
## FAQ's
### What is Aspose.Cells?  
Aspose.Cells is a powerful library for .NET that allows developers to create, manipulate, and convert Excel files without the need for Microsoft Excel.
### How do I install Aspose.Cells?  
You can download and install Aspose.Cells from the [Aspose website](https://releases.aspose.com/cells/net/).
### What compression levels are available?  
Aspose.Cells supports multiple compression levels ranging from Level 1 (lowest compression) to Level 9 (highest compression).
### Can I test Aspose.Cells for free?  
Yes! You can get a free trial of Aspose.Cells [here](https://releases.aspose.com/).
### Where can I find support for Aspose.Cells?  
For any queries or support, you can visit the Aspose support forum [here](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
