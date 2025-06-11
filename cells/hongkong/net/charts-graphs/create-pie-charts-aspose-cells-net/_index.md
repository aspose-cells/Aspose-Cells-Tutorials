---
"date": "2025-04-05"
"description": "了解如何使用 Aspose.Cells for .NET 建立帶有引線的動態圓餅圖。請按照本指南來增強您的資料視覺化技能。"
"title": "在 Aspose.Cells .NET 中建立帶有引線的圓餅圖&#58;綜合指南"
"url": "/zh-hant/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells .NET 建立引線的圓餅圖

## 介紹
使用 Aspose.Cells for .NET 創建更具資訊量的圓餅圖，增強資料視覺化。本逐步指南向您展示如何為圓餅圖部分新增引線，以便更輕鬆地一目了然地識別對應的資料類別。透過遵循本教程，您的視覺化效果將既具有視覺吸引力，又具有強大的功能。

**您將學到什麼：**
- 在您的環境中設定 Aspose.Cells for .NET
- 使用 C# 建立自訂引線餅圖
- 將圖表儲存為圖像或儲存在 Excel 工作簿中

確保一切準備就緒，以便有效地跟進。

## 先決條件
在開始之前，請確保滿足以下先決條件：

- **庫和版本**：安裝 Aspose.Cells for .NET。確保您的專案設定了最新版本。
- **環境設定**：本指引假設 Aspose.Cells 具有相容的 .NET 環境。
- **知識前提**：熟悉 C# 程式設計和 Excel 操作基本知識是有益的。

## 設定 Aspose.Cells for .NET
首先，透過以下方式在您的專案中安裝 Aspose.Cells：

**.NET CLI**
```bash
dotnet add package Aspose.Cells
```

**套件管理器**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

透過選擇以下選項來取得完整功能的許可證：
- **免費試用**：開始免費試用 [Aspose下載頁面](https://releases。aspose.com/cells/net/).
- **臨時執照**：取得臨時執照 [這裡](https://purchase。aspose.com/temporary-license/).
- **購買**：如需完整功能，請購買許可證 [這裡](https://purchase。aspose.com/buy).

透過建立實例來初始化專案中的 Aspose.Cells `Workbook` 班級。

## 實施指南

### 建立工作簿和工作表
1. **初始化工作簿**
   建立 XLSX 格式的新工作簿：
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **訪問第一個工作表**
   使用第一個工作表輸入資料：
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **為圓餅圖新增數據**
   使用類別和值填入您的工作表：
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // 新增剩餘的類別名稱...
   worksheet.Cells["B1"].PutValue(10.4);
   // 新增對應的值...
   ```

### 在工作表中加入圓餅圖
1. **創建圓餅圖**
   產生餅圖並將其新增至工作表的圖表集合中：
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **配置系列和類別數據**
   連結系列和類別的資料：
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **自訂資料標籤**
   關閉圖例顯示，設定資料標籤顯示類別名稱和百分比：
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### 實現引導線
1. **打開牽引線**
   啟用引導線以獲得更清晰的視覺連結：
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **調整資料標籤位置**
   透過調整標籤位置確保可見性：
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

### 儲存圖表和工作簿
1. **另存為影像**
   將圖表渲染為圖像檔案：
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **儲存工作簿**
   儲存工作簿以在 Excel 中檢視圖表：
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## 實際應用
- **財務報告**：清楚表示預算分配。
- **行銷分析**：在簡報或報告中有效地將市場佔有率資料視覺化。
- **銷售分析**：輕鬆顯示不同地區/產品的銷售分佈。

整合可能性包括將這些視覺化內容匯出到 Web 應用程式或將其嵌入到自動報告工具中。

## 性能考慮
使用 Aspose.Cells 時，請考慮以下事項以獲得最佳性能：
- 盡量減少一次載入到記憶體中的大型資料集。
- 使用高效循環並避免循環內不必要的計算。
- 定期清理工作簿物件等資源，以防止記憶體洩漏。

## 結論
您已經學習如何使用 Aspose.Cells for .NET 建立帶有引線的圓餅圖。此功能增強了資料視覺化的清晰度，使其更易於存取和更具影響力。 

**後續步驟：**
探索圖表外觀的進一步定製或嘗試 Aspose.Cells 中可用的其他圖表類型。

## 常見問題部分
1. **餅圖中的引導線是什麼？**
   引線將資料標籤與各自的段連接起來，提高了可讀性。

2. **我可以免費使用 Aspose.Cells 嗎？**
   是的，您可以從免費試用開始，但完整功能需要許可證。

3. **可以將圖表匯出為圖像嗎？**
   絕對地！使用 `ImageOrPrintOptions` 將圖表儲存為 PNG 或 JPEG 等影像格式。

4. **如何手動調整資料標籤位置？**
   修改系列點循環內資料標籤的X和Y座標。

5. **Aspose.Cells 可以與其他系統整合嗎？**
   是的，它可以與資料庫、Web 服務等結合使用，形成自動報告解決方案。

## 資源
- [Aspose.Cells文檔](https://reference.aspose.com/cells/net/)
- [下載 Aspose.Cells](https://releases.aspose.com/cells/net/)
- [購買許可證](https://purchase.aspose.com/buy)
- [免費試用](https://releases.aspose.com/cells/net/)
- [臨時執照](https://purchase.aspose.com/temporary-license/)
- [支援論壇](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}