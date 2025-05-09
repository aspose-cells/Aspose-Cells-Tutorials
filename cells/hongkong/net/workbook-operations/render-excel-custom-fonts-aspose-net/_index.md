---
"date": "2025-04-05"
"description": "了解如何使用 Aspose.Cells for .NET 的自訂字體將 Excel 檔案呈現為 PNG、TIFF 和 PDF 格式。確保所有文件轉換過程中的排版一致。"
"title": "使用 Aspose.Cells 在 .NET 中將 Excel 渲染為具有自訂字體的 PNG、TIFF、PDF"
"url": "/zh-hant/net/workbook-operations/render-excel-custom-fonts-aspose-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells for .NET 將 Excel 檔案渲染為具有自訂字體的 PNG、TIFF 和 PDF

## 介紹

在將 Excel 檔案轉換為圖像或 PDF 時保持字體完整性對於品牌一致性至關重要。 Aspose.Cells for .NET 可讓您在文件轉換中指定自訂預設字體，從而提供了一個強大的解決方案。

在本教程中，我們將指導您使用指定自訂預設字體的 Aspose.Cells for .NET 將 Excel 檔案渲染為 PNG、TIFF 和 PDF 格式。如果您符合以下情況，這是理想的選擇：
- 力求在呈現的文檔中實現一致的排版。
- 轉換時需要自訂字體設定。
- 想要探索 Aspose.Cells for .NET 中的設定選項。

讓我們設定您的環境並無縫實現這些功能。

### 先決條件

在開始之前，請確保您已準備好以下內容：
- **.NET 環境**：在您的機器上設定（最好是.NET Core 或 .NET Framework）。
- **Aspose.Cells for .NET函式庫**：安裝在您的專案中。
- **Excel 檔案**：包含要轉換的資料的 Excel 工作簿。

### 設定 Aspose.Cells for .NET

首先，將 Aspose.Cells 庫新增到您的專案中：

**使用 .NET CLI：**
```bash
dotnet add package Aspose.Cells
```

**使用套件管理器：**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

取得完整功能存取許可證：
- **免費試用**： 訪問 [Aspose 免費試用](https://releases.aspose.com/cells/net/) 用於初始訪問。
- **臨時執照**：從 [Aspose臨時許可證](https://purchase。aspose.com/temporary-license/).
- **購買**：如需永久許可證，請訪問 [Aspose 購買](https://purchase。aspose.com/buy).

取得許可證後，在應用程式中初始化 Aspose.Cells：
```csharp
// 設定 Aspose.Cells 的許可證。
License license = new License();
license.SetLicense("path_to_your_license_file");
```

## 實施指南

### 使用自訂預設字體渲染為 PNG

將 Excel 工作表渲染為 PNG 格式，同時設定自訂預設字體，確保視覺一致性。方法如下：

#### 步驟 1：配置影像選項

配置影像輸出的渲染選項。
```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// 指定目錄。
string SourceDir = @"YOUR_SOURCE_DIRECTORY";
string outputDir = @"YOUR_OUTPUT_DIRECTORY";

// 開啟 Excel 檔案。
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// 設定圖像渲染選項。
ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
imgOpt.ImageType = Drawing.ImageType.Png;
imgOpt.CheckWorkbookDefaultFont = false; // 使用自訂字體來彌補工作簿中缺少的字體。
imgOpt.DefaultFont = "Times New Roman";
```

#### 第 2 步：渲染並儲存

使用這些設定將您的工作表渲染為圖像檔案。
```csharp
// 將第一個工作表渲染為 PNG 影像。
SheetRender sr = new SheetRender(workbook.Worksheets[0], imgOpt);
sr.ToImage(0, outputDir + "out1_imagePNG.png");
```

### 使用自訂預設字體渲染為 TIFF

TIFF 格式非常適合高品質影像。以下介紹如何將整個工作簿呈現為 TIFF 檔案：

#### 步驟 3：設定 TIFF 的影像選項

專為 TIFF 輸出配置渲染選項。
```csharp
// 重新使用先前定義的目錄並開啟 Excel 檔案。
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// 配置 TIFF 的影像渲染選項。
imgOpt.ImageType = Drawing.ImageType.Tiff;
```

#### 步驟 4：將整個工作簿渲染為 TIFF

將整個工作簿轉換為單一 TIFF 檔案。
```csharp
// 將工作簿呈現為 TIFF 影像。
WorkbookRender wr = new WorkbookRender(workbook, imgOpt);
wr.ToImage(outputDir + "out1_imageTIFF.tiff");
```

### 使用自訂預設字體渲染為 PDF

將 Excel 工作簿儲存為 PDF 同時確保字體一致性對於專業文件至關重要。

#### 步驟5：配置PDF儲存選項

設定將文件儲存為 PDF 所需的選項。
```csharp
using Aspose.Cells;

// 重新開啟工作簿。
Workbook workbook = new Workbook(SourceDir + "sampleSetDefaultFontPropertyOfPdfSaveOptionsAndImageOrPrintOptions.xlsx");

// 設定 PDF 儲存選項。
PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.DefaultFont = "Times New Roman";
saveOptions.CheckWorkbookDefaultFont = false; // 使用自訂字體來彌補工作簿中缺少的字體。
```

#### 步驟 6：另存為 PDF

將您的工作簿匯出為 PDF 文件。
```csharp
// 將工作簿儲存為 PDF 檔案。
workbook.Save(outputDir + "out1_pdf.pdf", saveOptions);
```

## 實際應用

- **商業報告**：使用自訂字體確保所有匯出的報告中品牌的一致性。
- **文件歸檔**：將舊版 Excel 檔案轉換為 PDF，以便使用統一的排版輕鬆共用和存檔。
- **平面設計**：為演示或設計專案建立 Excel 資料的高解析度 TIFF 影像。

與其他系統（例如 CRM 平台或文件管理解決方案）的整合可以透過根據特定觸發器或事件自動匯出來進一步增強這些用例。

## 性能考慮

優化渲染過程至關重要：
- **記憶體管理**：處理 `Workbook`， `SheetRender`， 和 `WorkbookRender` 對像以釋放資源。
- **批次處理**：如果處理多個文件，請實施批次以實現高效處理。
- **非同步操作**：盡可能利用非同步方法來提高應用程式的回應能力。

## 結論

現在，您已經掌握了將 Excel 工作簿渲染為 PNG、TIFF 和 PDF 格式，同時使用 Aspose.Cells for .NET 設定自訂預設字體。此功能可確保您的文件在各種平台和用途上保持視覺完整性。

探索 Aspose.Cells 提供的其他功能，以進一步增強文件處理能力。如需更多資訊或協助，請訪問 [Aspose 論壇](https://forum。aspose.com/c/cells/9).

## 常見問題部分

**1.什麼是Aspose.Cells for .NET？**
   — Aspose.Cells for .NET 是一個函式庫，它提供強大的功能以程式設計方式管理和轉換 Excel 檔案。

**2. 我可以在網路應用程式中使用Aspose.Cells嗎？**
   — 是的，Aspose.Cells 可以整合到 ASP.NET 或任何其他基於 .NET 的 Web 應用程式中。

**3. 如何處理渲染過程中遺失的字體？**
   — 透過設定 `CheckWorkbookDefaultFont` 為 false 並指定 `DefaultFont`，您可以確保所有文字都使用您選擇的字體，即使原始字體不可用。

**4. 除了 PNG、TIFF 和 PDF 之外，還支援其他格式嗎？**
   — 是的，Aspose.Cells 支援各種影像格式，如 JPEG、BMP 等，並提供廣泛的文件轉換功能。

**5. 在大型應用程式中使用 Aspose.Cells 有哪些最佳實務？**
   — 利用高效的記憶體管理技術、批次處理多個文件，並考慮非同步操作來提高應用程式效能。

## 資源
- **文件**： [Aspose.Cells文檔](https://reference.aspose.com/cells/net/)
- **下載**： [Aspose.Cells 發布](https://releases.aspose.com/cells/net/)
- **購買**： [購買 Aspose.Cells](https://purchase.aspose.com/buy)
- **免費試用**： [免費試用 Aspose.Cells](https://releases.aspose.com/cells/net/)
- **臨時執照**： [獲得臨時許可證](https://purchase.aspose.com/temporary-license/) 


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}