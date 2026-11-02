---
category: general
date: 2026-08-17
description: 使用 C# 將 Excel 另存為 PowerPoint – 逐步指南，將 XLSX 檔案轉換、使文字方塊可編輯，並產生 PPTX 輸出。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: zh-hant
lastmod: 2026-08-17
og_description: 在 C# 中將 Excel 儲存為 PowerPoint，附完整程式碼範例。學習如何轉換 XLSX、使文字方塊可編輯，並匯出為 PPTX。
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: 在 C# 中將 Excel 另存為 PowerPoint – 完整轉換指南
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: 如何使用 C# 與 Aspose.Cells 將 Excel 另存為 PowerPoint
url: /zh-hant/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 C# 和 Aspose.Cells 將 Excel 儲存為 PowerPoint

如果您需要在 .NET 專案中 **將 Excel 儲存為 PowerPoint**，本指南將為您展示一個完整、可直接執行的解決方案。您將看到如何載入 XLSX 工作簿、將工作表上的所有文字方塊設為可編輯，並將結果匯出為 PPTX 檔案——只需幾行 C# 程式碼。

將 Excel 轉換為 PowerPoint 是報表儀表板、簡報投影片或自動化簡報產生的常見需求。本教學亦說明 **如何以程式方式編輯文字方塊**，讓您在儲存前自訂投影片內容。

## 前置條件

* .NET 6.0（或更新）SDK 已安裝  
* 開發環境，例如 Visual Studio 2022 或 VS Code  
* Aspose.Cells for .NET 授權（或免費評估金鑰）——可從 [Aspose website](https://products.aspose.com/cells/net/) 下載  
* `input.xlsx` 檔案（您要轉換的檔案）  

> **專業提示：** 若使用免費評估版，輸出的 PPTX 會包含浮水印。取得授權版即可移除浮水印。

## 步驟 1：安裝 Aspose.Cells NuGet 套件

在專案資料夾中開啟終端機，執行以下指令：

```bash
dotnet add package Aspose.Cells
```

此指令會加入 `Aspose.Cells` 程式集，提供轉換所需的 `Workbook`、`Worksheet` 與 `Shape` 類別。

## 步驟 2：建立主控台應用程式骨架

建立一個新的主控台專案（如果尚未有的話）：

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

將產生的 `Program.cs` 替換為下一步所示的程式碼。

## 步驟 3：載入工作簿並選取第一個工作表

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**為什麼這很重要：**  
`Workbook` 會將 Excel 檔案讀入記憶體，而 `Worksheet` 讓您存取工作表的儲存格、圖表與圖形。第一個工作表通常是您想要呈現的預設報表。

## 步驟 4：將工作表上的所有文字方塊設為可編輯

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**為什麼需要這麼做：**  
預設情況下，從 Excel 匯入的文字方塊在 PowerPoint 中為唯讀。將 `IsEditable = true` 設為可編輯，即可讓您（或之後的 PowerPoint 使用者）直接在投影片上修改文字。

## 步驟 5：將工作簿儲存為 PowerPoint 簡報

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**背後的運作原理：**  
`Workbook.Save` 會偵測到 `SaveFormat.Pptx` 列舉值，將 Excel 工作表的版面配置（包括列、欄、圖表以及已設為可編輯的文字方塊）轉換為 PowerPoint 投影片物件。

## 完整可執行原始碼

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### 預期輸出

執行程式 (`dotnet run`) 後，您應該會看到：

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

在 Microsoft PowerPoint 中開啟 `output.pptx`，會顯示與原始 Excel 工作表相同的投影片。所有文字方塊皆可透過雙擊直接編輯。

## 常見問題與邊緣情況

| Question | Answer |
|----------|--------|
| **我可以轉換特定工作表而不是第一個嗎？** | 可以。將 `workbook.Worksheets[0]` 改為 `workbook.Worksheets["SheetName"]` 或您需要的任意索引。 |
| **如果工作簿包含多個工作表該怎麼辦？** | 對每個工作表分別呼叫 `workbook.Save`，為每個檔案提供不同的 PPTX 檔名；或使用 Aspose.Slides 的 `Presentation` 物件將它們合併為單一簡報。 |
| **圖表會被保留嗎？** | Aspose.Cells 會自動將 Excel 圖表轉換為 PowerPoint 圖表物件，無需額外程式碼。 |
| **如何變更投影片尺寸？** | 在 `workbook.Save` 之後，您可以使用 Aspose.Slides 載入產生的 PPTX，並調整 `Presentation.SlideSize`。 |
| **如果需要在儲存前編輯文字方塊內容該怎麼辦？** | 在迴圈中存取 `shapeItem.TextBox.Text`，修改後再設定 `IsEditable = true`。例如：`shapeItem.TextBox.Text = "New title";` |

## 疑難排解技巧

* **「ShapeType.TextBox」未找到** – 請確認您使用的 Aspose.Cells 版本為 25.11 或更新版本；較舊版本不具備 `IsEditable` 屬性。  
* **檔案找不到錯誤** – 請確認 `YOUR_DIRECTORY` 為絕對路徑，或相對路徑指向正確位置。  
* **授權未套用** – 在載入工作簿之前呼叫 `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` 以移除評估浮水印。

## 結論

現在您已了解如何使用 C# **將 Excel 儲存為 PowerPoint**：載入 XLSX 工作簿、將所有文字方塊設為可編輯，並匯出為 PPTX。此方法會自動處理圖表、影像與儲存格格式，為您提供即時可用的簡報投影片。

接下來，您可以探索相關主題，例如 **使用 Aspose.Slides 將 Excel 轉換為 PowerPoint**、**轉換後以程式方式編輯文字方塊**，或 **批次處理多個工作簿**。這些主題皆以本指南的核心步驟為基礎，進一步自動化您的報表工作流程。

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.Cells for .NET 將 Excel 轉換為 PowerPoint：完整指南](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [如何在 C# 中複製樞紐分析表 – 轉換 Excel 為 PPTX、複製範圍並製作文字方塊](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [如何使用 Aspose.Cells .NET 將 Excel 檔案儲存為多種格式（2023 指南）](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}