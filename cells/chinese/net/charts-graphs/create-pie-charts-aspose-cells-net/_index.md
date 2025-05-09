---
"date": "2025-04-05"
"description": "学习如何使用 Aspose.Cells for .NET 创建带有引线的动态饼图。遵循本指南，提升您的数据可视化技能。"
"title": "在 Aspose.Cells .NET 中创建带引线的饼图——综合指南"
"url": "/zh/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells .NET 创建带引线的饼图

## 介绍
使用 Aspose.Cells for .NET 创建信息丰富的饼图，增强数据可视化效果。本分步指南将向您展示如何在饼图各部分添加引线，以便您一目了然地识别相应的数据类别。按照本教程操作，您的可视化效果将兼具美观性和强大的功能。

**您将学到什么：**
- 在您的环境中设置 Aspose.Cells for .NET
- 使用 C# 创建自定义引线饼图
- 将图表保存为图像或保存在 Excel 工作簿中

确保一切准备就绪，以便有效地跟进。

## 先决条件
开始之前，请确保满足以下先决条件：

- **库和版本**：安装 Aspose.Cells for .NET。确保您的项目已安装最新版本。
- **环境设置**：本指南假设 Aspose.Cells 具有兼容的 .NET 环境。
- **知识前提**：熟悉 C# 编程和 Excel 操作基本知识是有益的。

## 设置 Aspose.Cells for .NET
首先，通过以下方式在您的项目中安装 Aspose.Cells：

**.NET CLI**
```bash
dotnet add package Aspose.Cells
```

**包管理器**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

通过选择以下选项来获取完整功能的许可证：
- **免费试用**：开始免费试用 [Aspose下载页面](https://releases。aspose.com/cells/net/).
- **临时执照**：获得临时执照 [这里](https://purchase。aspose.com/temporary-license/).
- **购买**：如需完整功能，请购买许可证 [这里](https://purchase。aspose.com/buy).

通过创建实例来初始化项目中的 Aspose.Cells `Workbook` 班级。

## 实施指南

### 创建工作簿和工作表
1. **初始化工作簿**
   创建 XLSX 格式的新工作簿：
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **访问第一个工作表**
   使用第一个工作表输入数据：
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **为饼图添加数据**
   使用类别和值填充您的工作表：
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // 添加剩余的类别名称...
   worksheet.Cells["B1"].PutValue(10.4);
   // 添加相应的值...
   ```

### 向工作表添加饼图
1. **创建饼图**
   生成饼图并将其添加到工作表的图表集合中：
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **配置系列和类别数据**
   链接系列和类别的数据：
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **自定义数据标签**
   关闭图例显示，设置数据标签显示类别名称和百分比：
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### 实现引导线
1. **打开牵引线**
   启用引导线以获得更清晰的视觉连接：
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **调整数据标签位置**
   通过调整标签位置确保可见性：
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### 保存图表和工作簿
1. **另存为图像**
   将图表渲染为图像文件：
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **保存工作簿**
   保存工作簿以在 Excel 中查看图表：
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## 实际应用
- **财务报告**：清楚地表示预算分配。
- **营销分析**：在演示文稿或报告中有效地将市场份额数据可视化。
- **销售分析**：轻松显示不同地区/产品的销售分布。

集成可能性包括将这些可视化内容导出到 Web 应用程序或将其嵌入到自动报告工具中。

## 性能考虑
使用 Aspose.Cells 时，请考虑以下事项以获得最佳性能：
- 尽量减少一次加载到内存中的大型数据集。
- 使用高效循环并避免循环内不必要的计算。
- 定期清理工作簿对象等资源，以防止内存泄漏。

## 结论
您已经学习了如何使用 Aspose.Cells for .NET 创建带有引线的饼图。此功能可以增强数据可视化的清晰度，使其更易于访问且更具影响力。 

**后续步骤：**
探索图表外观的进一步定制或尝试 Aspose.Cells 中可用的其他图表类型。

## 常见问题解答部分
1. **饼图中的引导线是什么？**
   引线将数据标签与各自的段连接起来，提高了可读性。

2. **我可以免费使用 Aspose.Cells 吗？**
   是的，您可以从免费试用开始，但完整功能需要许可证。

3. **可以将图表导出为图像吗？**
   当然！使用 `ImageOrPrintOptions` 将图表保存为 PNG 或 JPEG 等图像格式。

4. **如何手动调整数据标签位置？**
   修改系列点循环内数据标签的X和Y坐标。

5. **Aspose.Cells 可以与其他系统集成吗？**
   是的，它可以与数据库、Web 服务等结合使用，形成自动报告解决方案。

## 资源
- [Aspose.Cells文档](https://reference.aspose.com/cells/net/)
- [下载 Aspose.Cells](https://releases.aspose.com/cells/net/)
- [购买许可证](https://purchase.aspose.com/buy)
- [免费试用](https://releases.aspose.com/cells/net/)
- [临时执照](https://purchase.aspose.com/temporary-license/)
- [支持论坛](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}