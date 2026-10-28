---
date: '2026-10-28'
description: 了解如何在 Java 中使用 Aspose.Cells 複製與貼上選項貼上值，並提供逐步代碼、Maven 依賴設定與授權技巧。
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: 了解如何在 Java 中使用 Aspose.Cells 複製與貼上選項貼上值，並提供逐步代碼、Maven 依賴設定與授權技巧。
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: 如何使用 Aspose.Cells 複製與貼上選項貼上值
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: 如何使用 Aspose.Cells 複製與貼上選項貼上值
url: /zh-hant/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 複製與貼上選項貼上值

在 Java 中自動化 Excel 報告意味著您可以在不手動開啟 Excel 的情況下產生、合併與格式化活頁簿。使用 **Aspose.Cells** 您可以完整控制公式、隱藏列與儲存格值，讓報告保持精確且輕量。於本教學中，您將學習如何使用 **CopyOptions.ReferToDestinationSheet** 以保持公式正確，並使用 **PasteOptions** 只貼上所需的可見值。

## 快速解答
- **What does `CopyOptions.ReferToDestinationSheet` do?** 它會重新寫入公式，使其在複製操作後指向目標工作表。  
- **How can I paste only visible cells?** 呼叫 `PasteOptions.setOnlyVisibleCells(true)` 並搭配 `PasteType.VALUES`。  
- **Which library version is required?** Aspose.Cells 25.3 或更新版本。  
- **Do I need a license for production?** 是 – 永久或暫時授權皆可移除評估限制。  
- **Can I use Maven or Gradle?** 兩者皆受支援；請參閱下方的相依性程式碼片段。

## 什麼是「自動化 Excel 報告」？
自動化 Excel 報告指的是以程式方式產生與更新 Excel 活頁簿，讓您能在不進行手動複製貼上的情況下建立、合併與格式化報告，從而減少錯誤並節省大量重複性的工作時間。此方法特別適用於排程批次工作、資料驅動的儀表板，以及財務合併流程。

## 為何在報告中使用 CopyOptions 與 PasteOptions？
這兩個類別讓您在複製資料 **同時** 保持公式參照不變，並僅提取過濾或隱藏列後可見的儲存格。將它們結合使用可在一般的過濾表格情境中將傳輸資料量減少最高 80 %，且確保公式在目標工作表中仍能正確計算。

## 前置條件
- Java 8 或更高版本。  
- 用於相依性管理的 Maven 或 Gradle。  
- Aspose.Cells 25.3 以上（試用版、暫時授權或永久授權）。  

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
- **Free trial** – 完整功能供評估使用。  
- **Temporary license** – 測試期間移除試用限制。  
- **Permanent license** – 推薦用於正式環境工作負載。

在您的 Java 程式碼中初始化 Aspose.Cells：  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## 步驟說明

### 1. 使用 referToDestinationSheet 的 copyOptions

#### 概觀
`CopyOptions` 是 Aspose.Cells 的設定物件，用於控制在複製操作期間公式與儲存格參照的處理方式。將 `CopyOptions.ReferToDestinationSheet` 設為 `true` 會重新寫入公式參照，使其在複製後指向新工作表。

#### 步驟 1：初始化活頁簿與工作表  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### 步驟 2：設定 copyOptions  
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
*為何重要*：原本參照 `Sheet1` 的公式現在會正確參照 `DestSheet`，確保您的自動化報告可靠。

**故障排除提示**：如果公式仍參照舊工作表，請確保在複製之前呼叫 `setReferToDestinationSheet(true)`。

### 2. 使用 pasteOptions 只貼上可見儲存格的值

#### 概觀
`PasteOptions` 是 Aspose.Cells 的設定物件，用於定義貼上的內容。將 `PasteType.VALUES` 與 `onlyVisibleCells=true` 結合使用，只會複製顯示的值，忽略隱藏的列/欄與格式。

#### 步驟 1：初始化活頁簿與工作表  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### 步驟 2：設定 pasteOptions  
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
*為何重要*：適用於提取過濾資料或產生不含隱藏列與格式雜訊的乾淨報告。

**故障排除提示**：請確認在 Excel 中列/欄已真正隱藏後再進行複製，否則仍會被包含。

## 實務應用
1. **Financial consolidation** – 合併每月工作表至主活頁簿，同時保持所有公式的正確性。  
2. **Filtered data export** – 從過濾表格中僅提取可見列至彙總工作表。  
3. **Scheduled report generation** – 自動化每晚的 Excel 報告產生，確保儲存格值精確且參照正確。

## 效能考量
- **Dispose of workbooks** 完成後 (`wb.dispose();`) 釋放原生資源。  
- **Batch operations** – 將多次複製/貼上呼叫合併以降低開銷。  
- **Monitor memory** – 大型活頁簿可能需要增加堆積大小 (`-Xmx2g`)。  
- Aspose.Cells 支援 **50+ 種輸入與輸出格式**，且可在不將整個檔案載入記憶體的情況下處理最多 **200 萬列** 的活頁簿，為企業工作負載提供高吞吐量效能。

## 常見問題

**Q: What is `CopyOptions.ReferToDestinationSheet` used for?**  
A: 它會重新寫入公式參照，使其在複製後指向目標工作表，確保報告公式保持正確。

**Q: How do I paste only visible cells?**  
A: 設定 `PasteOptions.setOnlyVisibleCells(true)` 並選擇 `PasteType.VALUES`。

**Q: Can I use Aspose.Cells without purchasing a license?**  
A: 可以，提供免費試用或暫時授權供評估使用，但正式環境需購買永久授權。

**Q: Why are some references still wrong after copying?**  
A: 請再次確認在複製之前已啟用 `ReferToDestinationSheet`，且來源公式未包含外部活頁簿連結。

**Q: What memory‑management best practices should I follow?**  
A: 完成後釋放 `Workbook` 物件，將大型檔案分塊處理，並監控 JVM 堆積使用情況。

**Q: Is it possible to combine CopyOptions and PasteOptions in one operation?**  
A: 可以，先使用 `CopyOptions` 進行複製，然後在目標範圍上套用 `PasteOptions` 即可。

## 資源
- **文件說明**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **下載**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **購買**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **免費試用**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **暫時授權**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **支援論壇**: [Aspose support](https://forum.aspose.com/c/cells)

---

**最後更新：** 2026-10-28  
**測試環境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose

## 相關教學

- [閱讀 Excel 檔案（Java） – 使用 Aspose.Cells 操作活頁簿儲存格](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [使用 Aspose.Cells for Java 向 Excel 儲存格新增資料](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [使用 Aspose.Cells Java 轉換 Excel 儲存格列與欄索引](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}