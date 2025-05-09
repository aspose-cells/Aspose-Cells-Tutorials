---
"date": "2025-04-05"
"description": "學習使用 Aspose.Cells for .NET 自動從 Excel 檔案中提取和保存 OLE 對象，增強您的資料處理工作流程。"
"title": "使用 Aspose.Cells for .NET 自動擷取並儲存 Excel OLE 對象"
"url": "/zh-hant/net/ole-objects-embedded-content/excel-automation-extract-save-ole-aspose-cells-dotnet/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells for .NET 自動擷取並儲存 Excel OLE 對象

## 介紹

您是否希望透過自動擷取 Excel 檔案中嵌入的物件來簡化工作流程？無論您是開發人員還是資料分析師，都可以利用 **Aspose.Cells for .NET** 可以顯著減少人工工作量和錯誤。本教學將引導您根據文件格式從 Excel 工作簿中提取和儲存物件連結和嵌入 (OLE) 物件。

### 您將學到什麼：
- 使用 Aspose.Cells 開啟並載入 Excel 工作簿。
- 存取工作表中的 OLE 物件集合。
- 根據特定格式提取並儲存 OLE 物件。

讓我們設定您的環境並實現這項高效的功能！

## 先決條件

在開始之前，請確保您已滿足以下先決條件：

### 所需庫：
- **Aspose.Cells for .NET** - 在 .NET 環境中處理 Excel 檔案必不可少。

### 環境設定：
- 類似 Visual Studio 或任何相容 IDE 的開發環境，支援 C# 和 .NET。

### 知識前提：
- 對 C# 程式設計有基本的了解。
- 熟悉.NET框架，尤其是檔案I/O操作。

## 設定 Aspose.Cells for .NET

要使用 Aspose.Cells for .NET，您需要將其安裝在您的專案中。方法如下：

### 安裝說明：

**使用 .NET CLI：**
```bash
dotnet add package Aspose.Cells
```

**使用套件管理器：**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### 許可證取得：
- **免費試用：** 從 30 天免費試用開始探索所有功能。
- **臨時執照：** 申請臨時許可證以延長存取權限。
- **購買：** 如果此工具滿足您的需求，請購買完整許可證。

安裝後，在專案中初始化 Aspose.Cells，如下所示：

```csharp
using Aspose.Cells;

// 初始化函式庫
Aspose.Cells.License license = new Aspose.Cells.License();
license.SetLicense("Path to License File");
```

## 實施指南

### 功能 1：開啟並載入工作簿

讓我們從指定目錄載入一個 Excel 工作簿。

#### 逐步實施：

**定義來源目錄：**
```csharp
string sourceDir = "YOUR_SOURCE_DIRECTORY";
```

**建立工作簿實例：**
```csharp
Workbook workbook = new Workbook(sourceDir + "sampleExtractOLEObjects.xlsx");
```
此步驟將您的 Excel 檔案載入到 `Workbook` 對象，允許您以程式設計方式操作其內容。

### 功能2：在工作表中存取OleObject集合

現在，存取工作簿第一個工作表中嵌入的 OLE 物件。

#### 逐步實施：

**造訪第一個工作表：**
```csharp
OleObjectCollection oles = workbook.Worksheets[0].OleObjects;
```
此程式碼片段從指定的工作表中檢索所有 OLE 物件以供進一步處理。

### 功能3：根據格式提取並儲存OLE對象

接下來，遍歷每個 OLE 物件以提取其資料並根據其格式儲存。

#### 逐步實施：

**迭代 OLE 物件：**
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
            // XLSX 格式的特殊處理
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
            // 處理其他格式或引發異常
            break;
    }

    File.WriteAllBytes(fileName, oleData);
}
```
本節示範如何動態處理不同的文件格式並適當地保存它們。

## 實際應用

以下是從 Excel 檔案中提取 OLE 物件的一些實際用例：
1. **自動數據報告：** 作為資料報告過程的一部分，自動提取嵌入的文件或影像。
2. **資料歸檔系統：** 出於合規目的，將嵌入的內容存檔在電子表格中。
3. **與文件管理系統整合：** 將提取的 OLE 物件無縫整合到其他文件管理平台。

## 性能考慮

為了確保使用 Aspose.Cells 時獲得最佳性能：
- **優化記憶體使用：** 使用 `MemoryStream` 在文件操作期間明智地有效地管理記憶體。
- **批次：** 如果處理大型資料集，請大量處理文件以避免過多的資源佔用。
- **最佳實踐：** 定期更新您的.NET 程式庫並利用 Aspose.Cells 的最新功能以獲得更好的效能。

## 結論

透過遵循本指南，您已經學習如何使用 Aspose.Cells for .NET 自動從 Excel 工作簿中提取 OLE 物件。此技能可提高資料處理效率並減少工作流程中的手動處理錯誤。

### 後續步驟：
- 嘗試不同的文件格式。
- 探索 Aspose.Cells 提供的其他功能，以進一步簡化您的任務。

準備好嘗試了嗎？今天就開始在您的專案中實施這些技術！

## 常見問題部分

1. **如何處理不支援的 OLE 物件格式？**
   - 對於未知或不支援的格式，請使用 `FileFormatType.Unknown` 案例並根據需要實作自訂邏輯。

2. **Aspose.Cells 能有效處理大型 Excel 檔案嗎？**
   - 是的，它針對效能進行了最佳化。考慮對非常大的資料集進行批次處理以保持效率。

3. **如果我提取的文件格式不正確怎麼辦？**
   - 仔細檢查 `FileFormatType` 在您的 switch 語句中並確保格式的正確對應。

4. **Aspose.Cells .NET 可以免費使用嗎？**
   - 您可以先進行 30 天免費試用，然後購買許可證以延長使用期限。

5. **如何將提取的 OLE 物件整合到其他系統？**
   - 使用標準文件 I/O 操作或整合工具將文件移至所需的系統。

## 資源
- **文件:** [Aspose.Cells .NET文檔](https://reference.aspose.com/cells/net/)
- **下載：** [最新發布](https://releases.aspose.com/cells/net/)
- **購買許可證：** [立即購買](https://purchase.aspose.com/buy)
- **免費試用：** [開始](https://releases.aspose.com/cells/net/)
- **臨時執照：** [在此請求](https://purchase.aspose.com/temporary-license/)
- **支援論壇：** [Aspose 支援](https://forum.aspose.com/c/cells/9)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}