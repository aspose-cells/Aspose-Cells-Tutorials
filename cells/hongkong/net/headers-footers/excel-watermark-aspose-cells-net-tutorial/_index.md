---
"date": "2025-04-05"
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 表中新增和自訂浮水印。本指南涵蓋設定、實作和安全功能。"
"title": "如何使用 Aspose.Cells .NET 在 Excel 中新增浮水印綜合指南"
"url": "/zh-hant/net/headers-footers/excel-watermark-aspose-cells-net-tutorial/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 如何使用 Aspose.Cells .NET 在 Excel 中新增浮水印

在當今的數位世界中，共享電子表格等文件時保護敏感資料至關重要。添加水印（一種微妙而有力的視覺提示）可以表明機密性或所有權。本綜合指南將指導您使用 Aspose.Cells for .NET 在 Excel 表中新增和自訂浮水印文字效果。

## 您將學到什麼
- 在您的開發環境中設定 Aspose.Cells for .NET。
- 使用 C# 在 Excel 表格中新增浮水印。
- 自訂浮水印的外觀，包括顏色和透明度設定。
- 鎖定 Excel 中的形狀以防止未經授權的修改。
- 增強文件安全性的實際應用。

讓我們探索如何在您的專案中實現這些功能。

## 先決條件
在開始之前，請確保您已：
- **Visual Studio** 安裝在您的機器上（2017 年及以後的任何版本）。
- C# 和 .NET 開發的基本知識。
- 對使用 API 操作 Excel 檔案有大致的了解。

此外，透過 NuGet 套件管理器控制台或 .NET CLI 安裝 Aspose.Cells for .NET：

**NuGet 套件管理器**
```bash
PM> Install-Package Aspose.Cells
```

**.NET CLI**
```bash
dotnet add package Aspose.Cells
```

### 許可證獲取
要使用 Aspose.Cells for .NET，您可以先免費試用授權來探索其功能：
1. **免費試用：** 訪問 [Aspose 臨時許可證頁面](https://purchase.aspose.com/temporary-license/) 並申請臨時執照。
2. **購買：** 如需長期使用，請透過以下方式購買許可證 [Aspose 購買頁面](https://purchase。aspose.com/buy).

### 基本設定
透過 NuGet 或 CLI 取得 Aspose.Cells 後，請在 C# 專案中對其進行初始化：
```csharp
using Aspose.Cells;
```

## 設定 Aspose.Cells for .NET
以下是設定和初始化 Aspose.Cells 的簡要概述：
1. **安裝** Aspose.Cells 使用套件管理器控制台或 .NET CLI，如上所示。
2. **初始化：** 首先創建一個 `Workbook` 對象，代表一個 Excel 檔案。

```csharp
Workbook workbook = new Workbook();
```
3. **申請許可證：** 如果您有許可證，請申請以解鎖全部功能。

## 實施指南

### 功能 1：向 Excel 工作表新增浮水印
#### 概述
新增浮水印涉及建立巧妙地覆蓋資料的文字效果，以表示文件狀態，例如「機密」。

#### 逐步實施
##### 建立工作簿和工作表
```csharp
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

##### 添加文字效果作為浮水印
建立具有特定屬性（例如字體樣式、大小、位置和外觀）的文字效果形狀。

```csharp
Shape wordart = sheet.Shapes.AddTextEffect(
    MsoPresetTextEffect.TextEffect1,
    "CONFIDENTIAL", 
    "Arial Black",
    50,   // 字體大小
    false, // 斜體
    true, // 是粗體
    18,   // 左側位置
    8,    // 頂部位置
    1,    // 寬度
    1,    // 高度
    130,  // 旋轉角度
    800   // 比例因子
);
```

##### 自訂外觀
設定漸層顏色和透明度以獲得精緻的外觀。
```csharp
FillFormat wordArtFormat = wordart.Fill;
wordArtFormat.SetOneColorGradient(Color.Red, 0.2, GradientStyleType.Horizontal, 2); 
wordArtFormat.Transparency = 0.9; // 使其稍微透明

wordart.HasLine = false; // 去除邊框線，使外觀更整潔
```

##### 儲存您的工作簿
```csharp
workbook.Save("YOUR_OUTPUT_DIRECTORY\output_out.xlsx");
```

### 功能 2：鎖定 Excel 工作表中的形狀
#### 概述
鎖定形狀可防止未經授權的使用者變更浮水印或其他形狀，從而確保文件的完整性。

#### 逐步實施
##### 鎖定浮水印的各種屬性
透過鎖定浮水印的各個方面來保護浮水印。
```csharp
wordart.IsLocked = true;
wordart.SetLockedProperty(ShapeLockType.Selection, true);
wordart.SetLockedProperty(ShapeLockType.ShapeType, true);
wordart.SetLockedProperty(ShapeLockType.Move, true);
wordart.SetLockedProperty(ShapeLockType.Resize, true);
wordart.SetLockedProperty(ShapeLockType.Text, true);
```

##### 儲存變更
確保變更已儲存到您的工作簿。
```csharp
workbook.Save("YOUR_OUTPUT_DIRECTORY\output_out.xlsx");
```

## 實際應用
1. **機密報告：** 對包含敏感資訊的內部報告使用浮水印。
2. **版權聲明：** 在分發給客戶的範本中嵌入版權聲明。
3. **版本控制：** 以相關浮水印文字標示文件的草稿或最終版本。

## 性能考慮
- **優化資源：** 僅載入必要的工作表和形狀，以最大限度地減少資源使用。
- **記憶體管理：** 使用以下方式妥善處理物品 `Dispose()` 方法適用，確保.NET 應用程式中的高效記憶體管理。

## 結論
透過掌握使用 Aspose.Cells for .NET 在 Excel 表中新增浮水印和鎖定形狀，您可以增強文件安全性並一目了然地傳達關鍵訊息。本指南為您提供了有效實現這些功能所需的技能。

### 後續步驟
探索更多自訂選項 [Aspose.Cells 文檔](https://reference.aspose.com/cells/net/) 或嘗試將這些功能整合到需要強大文件管理的大型系統中。

## 常見問題部分
1. **如何更改水印文字？**
   - 修改第二個參數 `AddTextEffect()` 方法與您想要的文字。
2. **我可以使用不同的字體作為浮水印嗎？**
   - 是的，透過更改第三個參數來指定任何字體 `AddTextEffect()`。
3. **如果我的 Excel 文件很大並且加載很慢怎麼辦？**
   - 考慮優化您的程式碼以僅載入工作簿的必要部分或使用 Aspose.Cells 中可用的效能調整選項。
4. **以後可以去除浮水印嗎？**
   - 是的，您可以從形狀所在的工作表集合中刪除它們。
5. **如何在批次中應用此解決方案？**
   - 遍歷多個工作簿，在循環或非同步任務中應用類似的邏輯以提高效率。

## 資源
- [Aspose.Cells文檔](https://reference.aspose.com/cells/net/)
- [下載 Aspose.Cells](https://releases.aspose.com/cells/net/)
- [購買許可證](https://purchase.aspose.com/buy)
- [取得免費試用](https://releases.aspose.com/cells/net/)
- [申請臨時許可證](https://purchase.aspose.com/temporary-license/)
- [Aspose 支援論壇](https://forum.aspose.com/c/cells/9)

現在您已經掌握了知識，是時候將這些技術付諸實踐並有效地保護您的 Excel 文件了！


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}