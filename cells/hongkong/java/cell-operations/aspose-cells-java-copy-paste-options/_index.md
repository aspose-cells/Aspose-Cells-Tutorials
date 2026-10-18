---
date: '2026-02-22'
description: 學習如何使用 Aspose.Cells 在 Java 中自動化 Excel 報表，透過 CopyOptions 與 PasteOptions
  保持公式正確，僅貼上可見的值。
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: 自動化 Excel 報表 – 精通 Java 中的 CopyOptions 與 PasteOptions（使用 Aspose.Cells）
url: /zh-hant/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 於 Java 自動化 Excel 報表：CopyOptions 與 PasteOptions

您是否想使用 Java **自動化 Excel 報表**？透過 Aspose.Cells，您可以以程式方式複製、貼上及調整公式，確保報表保持正確，且僅傳輸所需的資料。在本教學中，我們將逐步說明兩個重要功能——**CopyOptions.ReferToDestinationSheet** 與 **PasteOptions**——讓您保留公式參照，且僅貼上可見儲存格的值。

## 快速解答
- **`CopyOptions.ReferToDestinationSheet` 的作用是什麼？** 複製資料時會將公式調整為指向目標工作表。  
- **如何只貼上可見儲存格？** 使用 `PasteOptions.setOnlyVisibleCells(true)` 搭配 `PasteType.VALUES`。  
- **需要哪個版本的函式庫？** Aspose.Cells 25.3 或更新版本。  
- **生產環境是否需要授權？** 需要，永久或臨時授權可移除評估限制。  
- **可以使用 Maven 或 Gradle 嗎？** 兩者皆受支援；請參考以下相依性程式碼片段。

## 什麼是「自動化 Excel 報表」？
自動化 Excel 報表是指以程式方式產生、彙總與格式化 Excel 活頁簿，省去手動複製貼上的步驟，降低錯誤。Aspose.Cells 提供完整的 API，讓 Java 開發者能大規模操作試算表。

## 為何在報表中使用 CopyOptions 與 PasteOptions？
- **在工作表之間移動資料時，維持公式完整性**。  
- **排除隱藏的列/行**，使報表保持整潔且聚焦。  
- **提升效能**，僅複製必要的資料，而非整個範圍。

## 前置條件
- Java 8 或更高版本。  
- 用於相依性管理的 Maven 或 Gradle。  
- Aspose.Cells 25.3 以上（試用版、臨時授權或永久授權）。

## 為 Java 設定 Aspose.Cells

使用以下任一方式將函式庫加入您的專案：

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### 授權取得
- **免費試用** – 完整功能供評估使用。  
- **臨時授權** – 測試期間移除試用限制。  
- **永久授權** – 建議於正式環境使用。

在 Java 程式碼中初始化 Aspose.Cells：

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## 步驟說明

### 1. 使用 ReferToDestinationSheet 的 CopyOptions

#### 概觀
將 `CopyOptions.ReferToDestinationSheet` 設為 `true`，會重新寫入公式參照，使其在複製操作後指向新的工作表。

#### 步驟 1：初始化 Workbook 與 Worksheet  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### 步驟 2：設定 CopyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### 步驟 3：執行複製操作  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```

*為何重要*：原本參照 `Sheet1` 的公式現在會正確參照 `DestSheet`，確保自動化報表的可靠性。

**除錯提示**：若公式仍參照舊工作表，請確認在複製之前已呼叫 `setReferToDestinationSheet(true)`。

### 2. 只貼上可見儲存格值的 PasteOptions

#### 概觀
`PasteOptions` 讓您定義貼上的內容。結合 `PasteType.VALUES` 與 `onlyVisibleCells=true`，即可僅複製顯示的值，忽略隱藏的列/行及格式。

#### 步驟 1：初始化 Workbook 與 Worksheet  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### 步驟 2：設定 PasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### 步驟 3：執行貼上操作  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```

*為何重要*：適用於擷取已篩選的資料或產生不含隱藏列與格式雜訊的乾淨報表。

**除錯提示**：在複製前請確認 Excel 中的列/行確實已隱藏；否則仍會被包含。

## 實務應用
1. **財務合併** – 將每月工作表合併至主活頁簿，同時保持所有公式的正確性。  
2. **篩選資料匯出** – 從已篩選的表格中僅提取可見列，匯入摘要工作表。  
3. **排程報表產生** – 自動化每晚的 Excel 報表產生，確保儲存格值精確且參照正確。

## 效能考量
- **釋放 Workbook**（使用 `wb.dispose();`）以釋放原生資源。  
- **批次操作** – 將多個複製/貼上呼叫合併，以降低開銷。  
- **監控記憶體** – 大型活頁簿可能需要增加 JVM 堆積大小（例如 `-Xmx2g`）。

## 常見問題

**Q1：`CopyOptions.ReferToDestinationSheet` 的用途是什麼？**  
A：它會重新寫入公式參照，使其在複製後指向目標工作表，確保報表公式保持正確。

**Q2：如何只貼上可見儲存格？**  
A：設定 `PasteOptions.setOnlyVisibleCells(true)` 並選擇 `PasteType.VALUES`。

**Q3：可以在未購買授權的情況下使用 Aspose.Cells 嗎？**  
A：可以，提供免費試用或臨時授權供評估使用，但正式環境需購買永久授權。

**Q4：為何複製後仍有部分參照錯誤？**  
A：請再次確認在複製之前已啟用 `ReferToDestinationSheet`，且來源公式不含外部活頁簿連結。

**Q5：應遵循哪些記憶體管理最佳實踐？**  
A：完成後釋放 `Workbook` 物件，將大型檔案分塊處理，並監控 JVM 堆積使用情況。

**Q6：能否在一次操作中同時使用 CopyOptions 與 PasteOptions？**  
A：可以，先使用 `CopyOptions` 進行複製，然後在目標範圍上套用 `PasteOptions`。

## 資源
- **文件**： [Aspose.Cells Java 參考](https://reference.aspose.com/cells/java/)  
- **下載**： [Aspose.Cells Java 版本下載](https://releases.aspose.com/cells/java/)  
- **購買**： [購買 Aspose.Cells](https://purchase.aspose.com/buy)  
- **免費試用**： [Aspose.Cells 免費試用](https://releases.aspose.com/cells/java/)  
- **臨時授權**： [申請臨時授權](https://purchase.aspose.com/temporary-license/)  
- **支援論壇**： [Aspose 支援](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**最後更新：** 2026-02-22  
**測試環境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose