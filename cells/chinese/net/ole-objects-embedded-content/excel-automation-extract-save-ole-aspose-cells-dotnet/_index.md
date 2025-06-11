---
"date": "2025-04-05"
"description": "学习使用 Aspose.Cells for .NET 自动从 Excel 文件中提取和保存 OLE 对象，增强您的数据处理工作流程。"
"title": "使用 Aspose.Cells for .NET 自动提取和保存 Excel OLE 对象"
"url": "/zh/net/ole-objects-embedded-content/excel-automation-extract-save-ole-aspose-cells-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells for .NET 自动提取和保存 Excel OLE 对象

## 介绍

您是否希望通过自动提取 Excel 文件中嵌入的对象来简化工作流程？无论您是开发人员还是数据分析师，都可以利用 **Aspose.Cells for .NET** 可以显著减少手动工作量和错误。本教程将指导您根据 Excel 工作簿的文件格式提取并保存对象链接与嵌入 (OLE) 对象。

### 您将学到什么：
- 使用 Aspose.Cells 打开并加载 Excel 工作簿。
- 访问工作表中的 OLE 对象集合。
- 根据特定格式提取并保存 OLE 对象。

让我们设置您的环境并实现这一高效的功能！

## 先决条件

在开始之前，请确保您已满足以下先决条件：

### 所需库：
- **Aspose.Cells for .NET** - 在 .NET 环境中处理 Excel 文件必不可少。

### 环境设置：
- 类似 Visual Studio 或任何兼容 IDE 的开发环境，支持 C# 和 .NET。

### 知识前提：
- 对 C# 编程有基本的了解。
- 熟悉.NET框架，尤其是文件I/O操作。

## 设置 Aspose.Cells for .NET

要使用 Aspose.Cells for .NET，您需要将其安装到您的项目中。操作步骤如下：

### 安装说明：

**使用 .NET CLI：**
```bash
dotnet add package Aspose.Cells
```

**使用包管理器：**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### 许可证获取：
- **免费试用：** 从 30 天免费试用开始探索所有功能。
- **临时执照：** 申请临时许可证以延长访问权限。
- **购买：** 如果此工具满足您的需求，请购买完整许可证。

安装后，在项目中初始化 Aspose.Cells，如下所示：

```csharp
using Aspose.Cells;

// 初始化库
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Path to License File");
```

## 实施指南

### 功能 1：打开并加载工作簿

让我们从指定目录加载一个 Excel 工作簿。

#### 逐步实施：

**定义源目录：**
```csharp
string sourceDir = "YOUR_SOURCE_DIRECTORY";
```

**创建工作簿实例：**
```csharp
Workbook workbook = new Workbook(sourceDir + "sampleExtractOLEObjects.xlsx");
```
此步骤将您的 Excel 文件加载到 `Workbook` 对象，允许您以编程方式操作其内容。

### 功能2：在工作表中访问OleObject集合

现在，访问工作簿第一个工作表中嵌入的 OLE 对象。

#### 逐步实施：

**访问第一个工作表：**
```csharp
OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
此代码片段从指定的工作表中检索所有 OLE 对象以供进一步处理。

### 功能3：根据格式提取并保存OLE对象

接下来，遍历每个 OLE 对象以提取其数据并根据其格式保存。

#### 逐步实施：

**迭代 OLE 对象：**
```csharp
using System.IO;

for (int i = 0; i < oles.Count; i++)
{
    OleObject ole = oles[i];
    byte[] oleData = ole.ObjectData;
    string fileName = outputDir + "outputExtractOLEObjects" + (i+1) + ".";

    switch (ole.FileFormatType)
    {
        case FileFormatType.Doc:
            fileName += "doc";
            break;
        case FileFormatType.Docx:
            fileName += "docx";
            break;
        case FileFormatType.Excel97To2003:
            fileName += "xls";
            break;
        case FileFormatType.Xlsx:
            // XLSX 格式的特殊处理
            using (MemoryStream ms = new MemoryStream())
            {
                ms.Write(ole.ObjectData, 0, ole.ObjectData.Length);
                Workbook oleBook = new Workbook(ms);
                oleBook.Settings.IsHidden = false;

                ms.SetLength(0); // 清除流
                oleBook.Save(ms, SaveFormat.Xlsx);

                ms.Position = 0;
                byte[] bts = new byte[ms.Length];
                ms.Read(bts, 0, (int)ms.Length);
                oleData = bts;
            }
            fileName += "xlsx";
            break;
        case FileFormatType.Ppt:
            fileName += "ppt";
            break;
        case FileFormatType.Pdf:
            fileName += "pdf";
            break;
        case FileFormatType.Unknown:
            Guid g = new Guid(ole.ClassIdentifier);
            if (g.ToString() == "b801ca65-a1fc-11d0-85ad-444553540000")
            {
                fileName += "pdf";
            }
            else
            {
                fileName += "jpg";
            }                      
            break;
        default:
            // 处理其他格式或引发异常
            break;
    }

    File.WriteAllBytes(fileName, oleData);
}
```
本节演示如何动态处理不同的文件格式并适当地保存它们。

## 实际应用

以下是从 Excel 文件中提取 OLE 对象的一些实际用例：
1. **自动数据报告：** 作为数据报告过程的一部分，自动提取嵌入的文档或图像。
2. **数据归档系统：** 出于合规目的，将嵌入的内容存档在电子表格中。
3. **与文档管理系统集成：** 将提取的 OLE 对象无缝集成到其他文档管理平台。

## 性能考虑

为了确保使用 Aspose.Cells 时获得最佳性能：
- **优化内存使用：** 使用 `MemoryStream` 在文件操作期间明智地有效地管理内存。
- **批处理：** 如果处理大型数据集，请批量处理文件以避免过多的资源占用。
- **最佳实践：** 定期更新您的.NET 库并利用 Aspose.Cells 的最新功能以获得更好的性能。

## 结论

通过本指南，您学习了如何使用 Aspose.Cells for .NET 自动从 Excel 工作簿中提取 OLE 对象。此技能可以提高数据处理效率，并减少工作流程中的手动处理错误。

### 后续步骤：
- 尝试不同的文件格式。
- 探索 Aspose.Cells 提供的其他功能，以进一步简化您的任务。

准备好尝试一下了吗？今天就开始在你的项目中运用这些技巧吧！

## 常见问题解答部分

1. **如何处理不受支持的 OLE 对象格式？**
   - 对于未知或不支持的格式，请使用 `FileFormatType.Unknown` 案例并根据需要实现自定义逻辑。

2. **Aspose.Cells 能有效处理大型 Excel 文件吗？**
   - 是的，它针对性能进行了优化。考虑对非常大的数据集进行批处理以保持效率。

3. **如果我提取的文件格式不正确怎么办？**
   - 仔细检查 `FileFormatType` 在您的 switch 语句中并确保格式的正确映射。

4. **Aspose.Cells .NET 可以免费使用吗？**
   - 您可以先进行 30 天免费试用，然后购买许可证以延长使用期限。

5. **如何将提取的 OLE 对象集成到其他系统？**
   - 使用标准文件 I/O 操作或集成工具将文件移动到所需的系统。

## 资源
- **文档：** [Aspose.Cells .NET文档](https://reference.aspose.com/cells/net/)
- **下载：** [最新发布](https://releases.aspose.com/cells/net/)
- **购买许可证：** [立即购买](https://purchase.aspose.com/buy)
- **免费试用：** [开始](https://releases.aspose.com/cells/net/)
- **临时执照：** [在此请求](https://purchase.aspose.com/temporary-license/)
- **支持论坛：** [Aspose 支持](https://forum.aspose.com/c/cells/9)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}