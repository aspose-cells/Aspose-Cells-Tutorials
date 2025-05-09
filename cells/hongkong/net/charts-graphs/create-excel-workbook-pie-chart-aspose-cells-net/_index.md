---
"date": "2025-04-05"
"description": "了解如何使用 Aspose.Cells for .NET 建立和自訂帶有圓餅圖的 Excel 工作簿。按照本逐步指南可以有效地增強您的資料視覺化任務。"
"title": "使用 Aspose.Cells .NET 建立包含圓餅圖的 Excel 工作簿 - 綜合指南"
"url": "/zh-hant/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells .NET 建立帶有圓餅圖的 Excel 工作簿

## 介紹

在當今數據驅動的世界中，有效的資訊視覺化至關重要。無論您是管理銷售數據還是分析區域績效指標，Excel 中精心製作的圓餅圖都可以讓您的見解更易於理解且更具影響力。手動建立這些圖表可能非常耗時。輸入 Aspose.Cells for .NET－一個功能強大的函式庫，可以簡化以程式設計方式產生動態 Excel 報表的過程。

本教學將引導您從頭開始建立 Excel 工作簿、填充資料以及添加引人注目的餅圖的過程 - 所有這些都使用 C# 完成。本指南專為希望利用 Aspose.Cells for .NET 的人量身定制，使您的資料視覺化任務變得無縫且高效。

**您將學到什麼：**
- 如何在您的 .NET 專案中設定 Aspose.Cells。
- 建立新的 Excel 工作簿並用範例銷售資料填入它的步驟。
- 使用 Aspose.Cells 新增和自訂餅圖的技術。
- 處理大型資料集時優化效能的最佳實務。

首先讓我們介紹一下您開始此旅程之前所需的先決條件。

## 先決條件

在開始之前，請確保您具備以下條件：

### 所需庫
- **Aspose.Cells for .NET**：該程式庫允許在 .NET 應用程式中無縫建立和操作 Excel 檔案。
- **Visual Studio 或任何 C# IDE**：確保您的環境設定為支援 .NET 開發。

### 環境設定要求
- .NET Framework 4.6.1 或更高版本，或 .NET Core/5+/6+，以實現跨平台相容性。

### 知識前提
- 對 C# 程式設計有基本的了解。
- 熟悉 Excel 操作（可選但有幫助）。

## 設定 Aspose.Cells for .NET

首先，您需要在專案中安裝 Aspose.Cells 函式庫。您可以按照以下步驟操作：

**使用 .NET CLI：**
```bash
dotnet add package Aspose.Cells
```

**使用套件管理器：**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### 許可證獲取

Aspose 提供不同的授權選項：
- **免費試用**：在某些限制條件下測試該程式庫。
- **臨時執照**：獲得臨時許可證以進行廣泛測試。
- **購買**：獲得商業使用的完整許可。

要初始化和設置，只需添加：
```csharp
using Aspose.Cells;
```

## 實施指南

我們將根據特點將流程分解為邏輯部分。每個部分將提供概述，然後提供帶有程式碼片段的逐步說明。

### 建立並填入工作簿

**概述**：此功能示範如何建立新工作簿、存取其第一個工作表、設定工作表名稱以及用資料填充它。

1. **建立新工作簿**
   
   ```csharp
   string SourceDir = "YOUR_SOURCE_DIRECTORY";
   string outputDir = "YOUR_OUTPUT_DIRECTORY";

   Workbook workbook = new Workbook();
   ```

2. **訪問第一個工作表並設定名稱**
   
   ```csharp
   Worksheet sheet = workbook.Worksheets[0];
   sheet.Name = "Data";
   ```

3. **用資料填入工作表**
   
   ```csharp
   Cells cells = sheet.Cells;
   cells["A1"].PutValue("Region");
   // 填充區域數據
   cells["A2"].PutValue("France");
   // 繼續其他地區...

   cells["B1"].PutValue("Sale");
   // 填充銷售數據
   cells["B2"].PutValue(70000);
   ```

### 新增圖表表並建立圓餅圖

**概述**：了解如何新增新的圖表表、建立餅圖以及設定其基本屬性。

1. **新增圖表**
   
   ```csharp
   int sheetIndex = workbook.Worksheets.Add(SheetType.Chart);
   Worksheet chartSheet = workbook.Worksheets[sheetIndex];
   chartSheet.Name = "Chart";
   ```

2. **創建圓餅圖**
   
   ```csharp
   int chartIndex = chartSheet.Charts.Add(ChartType.Pie, 5, 0, 25, 10);
   Chart chart = chartSheet.Charts[chartIndex];
   ```

### 配置圖表屬性

**概述**：自訂餅圖的繪圖區域、標題和系列屬性。

1. **配置繪圖區域和標題**
   
   ```csharp
   chart.PlotArea.Area.ForegroundColor = Color.Coral;
   chart.Title.Text = "Sales By Region";
   chart.Title.Font.Color = Color.Blue;
   ```

2. **設定係列屬性**
   
   ```csharp
   chart.NSeries.Add("Data!B2:B8", true);
   chart.NSeries.CategoryData = "Data!A2:A8";
   chart.NSeries.IsColorVaried = true;
   ```

### 設定圖表系列的資料標籤

**概述**：透過為每個系列添加資料標籤來增強餅圖。

1. **新增數據標籤**
   
   ```csharp
   for (int i = 0; i < chart.NSeries.Count; i++) {
       DataLabels datalabels = chart.NSeries[i].DataLabels;
       datalabels.Position = LabelPositionType.InsideBase;
       datalabels.ShowCategoryName = true;
       datalabels.ShowValue = true;
   }
   ```

### 自訂圖表區和圖例

**概述**：透過調整圖表區域和圖例屬性進一步個性化您的圓餅圖。

1. **自訂圖表區**
   
   ```csharp
   ChartArea chartarea = chart.ChartArea;
   chartarea.Area.Formatting = FormattingType.Custom;
   chartarea.Area.FillFormat.Texture = TextureType.BlueTissuePaper;
   ```

2. **修改圖例屬性**
   
   ```csharp
   Legend legend = chart.Legend;
   legend.Position = LegendPositionType.Left;
   legend.Font.IsBold = true;
   legend.Border.Color = Color.Blue;
   ```

### 儲存工作簿

**概述**：儲存您的工作簿以及您配置的所有圖表和資料。

```csharp
workbook.Save(outputDir + "outputHowToCreatePieChart.xlsx");
```

## 實際應用

以下是一些實際用例，其中建立帶有餅圖的 Excel 工作簿特別有用：

1. **銷售業績分析**：可視化區域銷售數據以確定表現最佳的區域。
2. **預算分配**：顯示不同部門或項目的預算分配狀況。
3. **客戶人口統計**：根據年齡、位置或偏好分析客戶群。
4. **庫存管理**：追蹤產品類別及其對整體庫存價值的貢獻。

## 性能考慮

使用 Aspose.Cells for .NET 時，請考慮以下提示：
- **優化大型資料集**：使用批次方法有效處理大型資料集。
- **記憶體管理**：妥善處理物品以釋放資源。
- **利用多執行緒**：對於密集操作，請使用 .NET 中提供的多執行緒功能。

## 結論

使用 Aspose.Cells for .NET 建立具有圓餅圖的 Excel 工作簿是一種以視覺和有效方式呈現資料的有效方法。透過遵循本指南，您已經了解如何設定環境、填充 Excel 工作簿、建立圖表以及自訂它們以滿足您的需求。

**後續步驟**：嘗試不同的圖表類型並探索 Aspose.Cells 的附加功能以進一步增強您的應用程式。

## 常見問題部分

1. **如何安裝 Aspose.Cells for .NET？**
   - 請依照設定部分中的說明使用 .NET CLI 或套件管理器。

2. **我可以免費使用 Aspose.Cells 嗎？**
   - 可以免費試用，但擴充功能和商業用途需要許可證。

3. **我可以使用 Aspose.Cells 建立哪些圖表類型？**
   - 除了圓餅圖，您還可以使用 Aspose.Cells 建立長條圖、折線圖、散點圖、面積圖等。

4. **如何使用 Aspose.Cells 處理 Excel 中的大型資料集？**
   - 使用庫的高效資料處理功能來有效地管理和處理大型資料集。

5. **Aspose.Cells 是否與所有版本的 .NET 相容？**
   - 是的，它與各種 .NET Framework 和 .NET Core 版本相容。

## 關鍵字推薦
- “Aspose.Cells for .NET”
- “建立 Excel 工作簿”
- “Excel 圓餅圖”

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}