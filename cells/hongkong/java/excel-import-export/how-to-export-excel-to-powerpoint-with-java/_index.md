---
category: general
date: 2026-09-08
description: 學習如何使用 Java 與 Aspose.Cells 將 Excel 匯出至 PowerPoint，並在 PPTX 輸出中保留可編輯的文字方塊。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- Aspose.Cells Java
- editable text boxes
- ImageOrPrintOptions
- Workbook save
- PowerPoint PPTX export
language: zh-hant
lastmod: 2026-09-08
og_description: 使用 Aspose.Cells 以 Java 將 Excel 匯出至 PowerPoint。本指南將示範如何保持圖表文字可編輯，並在數分鐘內產生
  PPTX 檔案。
og_image_alt: Screenshot of Java code exporting an Excel worksheet to a PowerPoint
  slide
og_title: 使用 Java 將 Excel 匯出至 PowerPoint – 一步一步教學
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to export Excel to PowerPoint using Java and Aspose.Cells,
    preserving editable text boxes in the PPTX output.
  headline: How to export Excel to PowerPoint with Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
title: 如何使用 Java 將 Excel 匯出至 PowerPoint
url: /zh-hant/java/excel-import-export/how-to-export-excel-to-powerpoint-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Java 將 Excel 匯出至 PowerPoint

如果您需要 **export Excel to PowerPoint**，本教學將向您展示一個簡潔的 Java 解決方案。使用 **Aspose.Cells Java**，您可以保留圖表格式，並在產生的 PPTX 檔案中啟用 **editable text boxes**。

將試算表匯出為簡報是常見需求，特別是當您想在投影片中重複使用資料驅動的圖表時。在本指南中，您將學習如何：

* 載入包含圖表的現有 Excel 活頁簿。
* 設定 **ImageOrPrintOptions**，使匯出的投影片保持文字方塊可編輯。
* 以單一方法呼叫將工作表儲存為 **PowerPoint PPTX** 檔案。
* 執行完整、獨立的範例，您可以將其複製到自己的專案中。

唯一的先決條件是 Java 8（或更新版本）執行環境以及有效的 Aspose.Cells for Java 授權。若您使用免費評估版，輸出檔案會包含浮水印，但程式碼仍可正常運作。

---

## 匯出 Excel 至 PowerPoint – 建置開發環境

在撰寫程式碼之前，請確保您已具備以下項目：

| 項目 | 原因 |
|------|--------|
| **Java Development Kit (JDK) 8+** | 需要編譯與執行範例。 |
| **Aspose.Cells for Java** library | 提供用於轉換的 `Workbook`、`ImageOrPrintOptions` 與 `SaveFormat` 類別。 |
| **A valid Aspose.Cells license** (optional) | 移除評估浮水印並解鎖完整功能。 |
| **An Excel file (`chartSheet.xlsx`)** with at least one chart | 您將匯出的來源活頁簿。 |

將 Aspose.Cells JAR 加入專案的 classpath。若使用 Maven，請加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest version -->
</dependency>
```

---

## 為可編輯文字方塊設定 ImageOrPrintOptions

`ImageOrPrintOptions` 類別控制匯出時工作表的呈現方式。將 `setExportEditableTextBox(true)` 設為 true，會告訴 Aspose.Cells 在 PowerPoint 中將圖表內的文字元素保留為 **editable text boxes**，而非將其平鋪為靜態影像。

```java
// Create export options for PowerPoint
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);          // Target format is PPTX
exportOptions.setExportEditableTextBox(true);        // Keep chart text editable
```

此設定的重要性：當您稍後在 PowerPoint 中開啟 PPTX 檔案時，能直接點擊圖表標籤並編輯其內容，這對需要即時調整的簡報而言相當關鍵。

---

## 載入活頁簿並匯出為 PPTX 檔案

現在載入 Excel 檔案，套用前一步的選項，然後呼叫 `save`。`Workbook.save` 方法接受輸出路徑與 `ImageOrPrintOptions` 實例，內部完成轉換。

```java
// Load the workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/chartSheet.xlsx");

// Export the first worksheet to PowerPoint using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", exportOptions);
```

**重點說明**

* `Workbook` 代表整個 Excel 檔案。若只想匯出單一工作表，可使用 `workbook.getWorksheets().get(0)` 取得特定工作表。
* `save` 方法預設會產生每個工作表對應一張投影片的 PPTX 檔案。
* 若活頁簿包含多個工作表且只需要圖表工作表，可在儲存前刪除不需要的工作表，或使用 `ExportOptions.setOnePagePerSheet(false)` 來控制分頁。

---

## 完整可執行範例

以下是一個最小且可完整執行的 Java 程式，示範整個流程。請將 `YOUR_DIRECTORY` 替換為指向您檔案的絕對或相對路徑。

```java
import com.aspose.cells.*;

public class ExcelToPowerPointDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the Excel workbook that holds the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chartSheet.xlsx");

            // 2. Prepare export options for PowerPoint and enable editable text boxes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);          // Export as PPTX
            exportOptions.setExportEditableTextBox(true);        // Keep text boxes editable

            // 3. Export the worksheet(s) to a PPTX file
            workbook.save("YOUR_DIRECTORY/output.pptx", exportOptions);

            System.out.println("Export completed successfully. Check output.pptx.");
        } catch (Exception e) {
            System.err.println("Error during export: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

**預期輸出**

執行程式會印出：

```
Export completed successfully. Check output.pptx.
```

當您在 Microsoft PowerPoint 中開啟 `output.pptx` 時，會看到與 Excel 圖表相同的投影片。雙擊任意圖表標籤即可直接編輯文字，證實 **editable text boxes** 已啟用。

---

## 處理常見變化與邊緣情況

| 情況 | 建議做法 |
|-----------|----------------------|
| **Multiple worksheets** 但只需匯出一個圖表工作表 | 在呼叫 `save` 前使用 `workbook.getWorksheets().removeAt(index)` 刪除不需要的工作表，或設定 `exportOptions.setOnePagePerSheet(false)`，再手動選取要渲染的工作表。 |
| **Large Excel files** 造成記憶體壓力 | 在建立 `Workbook` 時使用 `loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` 開啟串流模式。 |
| **License not set**（評估版） | 產生的 PPTX 會包含浮水印。於 `main` 開頭加入 `License license = new License(); license.setLicense("Aspose.Cells.lic");` 以移除浮水印。 |
| **Need to export only a specific range** | 建立暫存工作表，使用 `worksheet.getCells().copyRange(...)` 複製所需範圍，然後匯出該暫存工作表。 |
| **PowerPoint version compatibility** | Aspose.Cells 總是產生 Office Open XML（PPTX），相容於 PowerPoint 2007 及之後版本。若需舊版 PPT 格式，將 `SaveFormat.PPT` 改為相應設定（但 editable text boxes 僅支援 PPTX）。 |

---

## 生產環境的專業提示

* **Batch conversion** – 迴圈處理目錄中的 Excel 檔案，重複使用單一 `ImageOrPrintOptions` 實例以減少物件建立開銷。
* **Performance profiling** – 量測 `workbook.save` 處理大型檔案所需時間；若遭遇 `OutOfMemoryError`，可考慮增大 JVM 堆積 (`-Xmx2g`)。
* **Custom slide layout** – 匯出後，可使用 Aspose.Slides for Java 進一步操作 PPTX，加入標題、頁腳或套用母片投影片。

---

## 結論

現在您已了解如何使用 Java **export Excel to PowerPoint**，透過 `ImageOrPrintOptions` 保留圖表品質並啟用 **editable text boxes**。完整範例示範了載入活頁簿、設定匯出選項，以及以三個簡潔步驟儲存 PPTX 檔案。

接下來您可以探索相關主題，例如 **Aspose.Cells Java chart manipulation**、使用自訂範本的 **PowerPoint PPTX export**，或 **batch processing multiple spreadsheets**。嘗試不同的 `SaveFormat` 值，將此方法與 Aspose.Slides 結合，並將工作流程整合至您的報表管線中。

![Java code exporting Excel to PowerPoint](/images/export-excel-to-powerpoint.png){: .responsive-img alt="將 Excel 工作表匯出至 PowerPoint 投影片的 Java 程式碼螢幕截圖"}

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立於此處示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 Aspose.Cells Java 在 Excel 中建立與設定文字方塊以增強資料呈現](/cells/english/java/images-shapes/create-text-boxes-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells Java 將 Excel 圖表匯出為 SVG（可縮放向量圖形）](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [如何使用 Aspose.Cells Java 將 Excel 工作表匯出為 PNG](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}