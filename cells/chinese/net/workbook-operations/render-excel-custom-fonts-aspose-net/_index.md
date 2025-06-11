---
"date": "2025-04-05"
"description": "了解如何使用 Aspose.Cells for .NET 自定义字体将 Excel 文件渲染为 PNG、TIFF 和 PDF 格式。确保所有文档转换过程中的字体排版一致。"
"title": "使用 Aspose.Cells 在 .NET 中将 Excel 渲染为带有自定义字体的 PNG、TIFF、PDF"
"url": "/zh/net/workbook-operations/render-excel-custom-fonts-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells for .NET 将 Excel 文件渲染为带有自定义字体的 PNG、TIFF 和 PDF

## 介绍

在将 Excel 文件转换为图像或 PDF 的过程中，保持字体的完整性对于品牌一致性至关重要。Aspose.Cells for .NET 提供了一个强大的解决方案，允许您在文档转换过程中指定自定义默认字体。

在本教程中，我们将指导您使用 Aspose.Cells for .NET 和指定的自定义默认字体将 Excel 文件渲染为 PNG、TIFF 和 PDF 格式。如果您符合以下条件，这将是理想的选择：
- 力求在呈现的文档中实现一致的排版。
- 转换时需要自定义字体设置。
- 想要探索 Aspose.Cells for .NET 中的配置选项。

让我们设置您的环境并无缝实现这些功能。

### 先决条件

开始之前，请确保您已准备好以下内容：
- **.NET 环境**：在您的机器上进行设置（最好是.NET Core 或 .NET Framework）。
- **Aspose.Cells for .NET库**：安装在您的项目中。
- **Excel 文件**：包含要转换的数据的 Excel 工作簿。

### 设置 Aspose.Cells for .NET

首先，将 Aspose.Cells 库添加到您的项目中：

**使用 .NET CLI：**
```bash
dotnet add package Aspose.Cells
```

**使用包管理器：**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

获取完整功能访问许可证：
- **免费试用**： 访问 [Aspose 免费试用](https://releases.aspose.com/cells/net/) 用于初始访问。
- **临时执照**：从 [Aspose临时许可证](https://purchase。aspose.com/temporary-license/).
- **购买**：如需永久许可证，请访问 [Aspose 购买](https://purchase。aspose.com/buy).

获取许可证后，在应用程序中初始化 Aspose.Cells：
```csharp
// 设置 Aspose.Cells 的许可证。
License license = new License();
license.SetLicense("path_to_your_license_file");
```

## 实施指南

### 使用自定义默认字体渲染为 PNG

将 Excel 工作表渲染为 PNG 格式并设置自定义默认字体，可确保视觉一致性。具体方法如下：

#### 步骤 1：配置图像选项

配置图像输出的渲染选项。
```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// 指定目录。
string SourceDir = @"YOUR_SOURCE_DIRECTORY";
string outputDir = @"YOUR_OUTPUT_DIRECTORY";

// 打开 Excel 文件。
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// 设置图像渲染选项。
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false; // 使用自定义字体来弥补工作簿中缺少的字体。
imgOpt.DefaultFont = "Times New Roman";
```

#### 第 2 步：渲染并保存

使用这些设置将您的工作表渲染为图像文件。
```csharp
// 将第一个工作表渲染为 PNG 图像。
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```

### 使用自定义默认字体渲染为 TIFF

TIFF 格式非常适合高质量图像。以下是将整个工作簿渲染为 TIFF 文件的方法：

#### 步骤 3：设置 TIFF 的图像选项

专门为 TIFF 输出配置渲染选项。
```csharp
// 重新使用以前定义的目录并打开 Excel 文件。
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// 配置 TIFF 的图像渲染选项。
imgOpt.ImageType = Drawing.ImageType.Tiff;
```

#### 步骤 4：将整个工作簿渲染为 TIFF

将整个工作簿转换为单个 TIFF 文件。
```csharp
// 将工作簿呈现为 TIFF 图像。
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```

### 使用自定义默认字体渲染为 PDF

将 Excel 工作簿保存为 PDF 同时确保字体一致性对于专业文档至关重要。

#### 步骤5：配置PDF保存选项

设置将文件保存为 PDF 所需的选项。
```csharp
using Aspose.Cells;

// 重新打开工作簿。
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// 设置 PDF 保存选项。
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false; // 使用自定义字体来弥补工作簿中缺少的字体。
```

#### 步骤 6：另存为 PDF

将您的工作簿导出为 PDF 文档。
```csharp
// 将工作簿保存为 PDF 文件。
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```

## 实际应用

- **商业报告**：使用自定义字体确保所有导出的报告中品牌的一致性。
- **文件归档**：将旧版 Excel 文件转换为 PDF，以便使用统一的排版轻松共享和存档。
- **平面设计**：为演示或设计项目创建 Excel 数据的高分辨率 TIFF 图像。

与其他系统（例如 CRM 平台或文档管理解决方案）的集成可以通过根据特定触发器或事件自动导出来进一步增强这些用例。

## 性能考虑

优化渲染过程至关重要：
- **内存管理**：处理 `Workbook`， `SheetRender`， 和 `WorkbookRender` 对象以释放资源。
- **批处理**：如果处理多个文件，请实施批处理以实现高效处理。
- **异步操作**：尽可能利用异步方法来提高应用程序的响应能力。

## 结论

现在，您已经掌握了如何使用 Aspose.Cells for .NET 将 Excel 工作簿渲染为 PNG、TIFF 和 PDF 格式，并设置自定义默认字体。此功能可确保您的文档在各种平台和用途上保持视觉完整性。

探索 Aspose.Cells 提供的其他功能，进一步增强文档处理能力。如需更多信息或帮助，请访问 [Aspose 论坛](https://forum。aspose.com/c/cells/9).

## 常见问题解答部分

**1.什么是Aspose.Cells for .NET？**
   — Aspose.Cells for .NET 是一个库，它提供强大的功能以编程方式管理和转换 Excel 文件。

**2. 我可以在Web应用程序中使用Aspose.Cells吗？**
   — 是的，Aspose.Cells 可以集成到 ASP.NET 或任何其他基于 .NET 的 Web 应用程序中。

**3. 如何处理渲染过程中丢失的字体？**
   — 通过设置 `CheckWorkbookDefaultFont` 为 false 并指定 `DefaultFont`，您可以确保所有文本都使用您选择的字体，即使原始字体不可用。

**4. 除了 PNG、TIFF 和 PDF 之外，还支持其他格式吗？**
   — 是的，Aspose.Cells 支持各种图像格式，如 JPEG、BMP 等，并提供广泛的文档转换功能。

**5. 在大型应用程序中使用 Aspose.Cells 有哪些最佳实践？**
   — 利用高效的内存管理技术、批处理来处理多个文件，并考虑异步操作来提高应用程序性能。

## 资源
- **文档**： [Aspose.Cells文档](https://reference.aspose.com/cells/net/)
- **下载**： [Aspose.Cells 发布](https://releases.aspose.com/cells/net/)
- **购买**： [购买 Aspose.Cells](https://purchase.aspose.com/buy)
- **免费试用**： [免费试用 Aspose.Cells](https://releases.aspose.com/cells/net/)
- **临时执照**： [获得临时许可证](https://purchase.aspose.com/temporary-license/) 


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}