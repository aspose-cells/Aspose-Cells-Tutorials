---
category: general
date: 2026-08-20
description: 學習如何設定 Excel 列印範圍，然後使用 Aspose.Cells 將 Excel 匯出為 PPTX。本指南將一步步帶您將工作表轉換為
  PowerPoint 並儲存為 PPTX 檔案。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- export excel to pptx
- convert worksheet to powerpoint
- save worksheet as powerpoint
language: zh-hant
lastmod: 2026-08-20
og_description: 設定 Excel 列印區，然後使用 Aspose.Cells 將 Excel 匯出為 PPTX。請跟隨此一步一步的教學，將工作表轉換為
  PowerPoint 並儲存為 PPTX 檔案。
og_image_alt: Screenshot showing Excel print area set and PPTX export using Aspose.Cells
og_title: 設定 Excel 列印範圍並匯出至 PowerPoint – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to set print area excel, then export excel to pptx with Aspose.Cells.
    This guide walks you through converting a worksheet to PowerPoint and saving it
    as a PPTX.
  headline: How to set print area excel and export to PowerPoint
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint generation
title: 如何設定 Excel 列印區域並匯出至 PowerPoint
url: /zh-hant/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何設定 Excel 列印區域並匯出至 PowerPoint

如果您需要在分享投影片資料前 **設定 Excel 列印區域**，本教學將完整說明操作步驟。您將會看到如何設定列印區域，然後 **將 Excel 匯出為 pptx** 並保留文字方塊可編輯，讓產生的 PowerPoint 可直接進一步編輯。

我們將使用 Aspose.Cells for Java 來 **將工作表轉換為 PowerPoint**，最後 **將工作表儲存為 PowerPoint**（PPTX 格式）。除了 Aspose.Cells JAR 之外不需要其他函式庫。完成本指南後，您即可在任何相容 Java 的環境執行程式碼，產生與所選 Excel 範圍相同的簡報。

## 前置條件

- Java Development Kit 17 或更新版本  
- Aspose.Cells for Java（從官方 Aspose 網站下載）  
- 含有您想保留可編輯形狀的 Excel 活頁簿（例如 `BookWithShapes.xlsx`）  

確保 Aspose.Cells JAR 已加入 classpath：

```bash
javac -cp "aspose-cells-23.12.jar" ExportEditableShapesToPptx.java
java -cp ".:aspose-cells-23.12.jar" ExportEditableShapesToPptx
```

## 步驟 1：使用 Aspose.Cells 設定 Excel 列印區域

第一步是定義要匯出的範圍。設定列印區域可將轉換限制在您關心的儲存格，並提升效能。

```java
// Load the workbook that contains shapes
Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

// Define the print area for the first worksheet (A1:G30)
workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");
```

**為什麼這很重要** – `setPrintArea` 方法告訴 Aspose.Cells 哪些儲存格屬於可列印頁面。當您稍後 **將 Excel 匯出為 pptx** 時，僅會呈現此區域，避免多餘資料出現在投影片上。

### 專業提示
如果需要動態範圍，您可以以程式方式計算地址：

```java
int lastRow = workbook.getWorksheets().get(0).getCells().getMaxDataRow() + 1;
int lastCol = workbook.getWorksheets().get(0).getCells().getMaxDataColumn() + 1;
String range = String.format("A1:%s%d", CellsHelper.columnIndexToName(lastCol - 1), lastRow);
workbook.getWorksheets().get(0).getPageSetup().setPrintArea(range);
```

## 步驟 2：將 Excel 匯出為 pptx 並保留可編輯文字方塊

在定義列印區域後，設定匯出選項。啟用 `setExportEditableTextBoxes` 可將形狀文字保留為 PowerPoint 中的可編輯欄位。

```java
// Create export options and enable editable text boxes in the PPTX
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);
exportOptions.setExportEditableTextBoxes(true);   // keeps text boxes editable
```

**為什麼這很重要** – 預設情況下 Aspose.Cells 會將文字方塊光柵化，變成影像的一部份。將 `ExportEditableTextBoxes` 設為 `true` 可保留原始形狀物件，讓使用者可直接在 PowerPoint 中修改文字。

## 步驟 3：將工作表轉換為 PowerPoint 並儲存檔案

現在執行實際的轉換。`Workbook.save` 方法接受目標檔名以及先前設定好的選項。

```java
// Export the first worksheet to PPTX using the configured options
workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
```

程式執行完畢後，`SheetWithEditableShapes.pptx` 會包含一張與已定義列印區域（`A1:G30`）相同的投影片。所有形狀，包括文字方塊，皆保持可編輯。

### 預期輸出
在 Microsoft PowerPoint 中開啟產生的 PPTX：

- 投影片顯示 **A1 到 G30** 的儲存格，與 Excel 中的顯示完全相同。  
- 原始工作表中存在的任何形狀皆會以 PowerPoint 形狀呈現。  
- 這些形狀內的文字可直接在 PowerPoint 中編輯（不會被光柵化）。

## 步驟 4：完整、可執行範例

以下為完整程式碼。請將 `YOUR_DIRECTORY` 替換為您機器上的實際資料夾路徑。

```java
import com.aspose.cells.*;

public class ExportEditableShapesToPptx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

        // Step 2: Create export options and enable editable text boxes in the PPTX
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setSaveFormat(SaveFormat.PPTX);
        exportOptions.setExportEditableTextBoxes(true); // keeps text boxes editable

        // Step 3: Define the print area to limit the exported range
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");

        // Step 4: Export the first worksheet to PPTX using the configured options
        workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
    }
}
```

依照 *前置條件* 章節說明執行程式。產生的 PowerPoint 檔案會放在您指定的同一目錄下。

## 常見問題與邊緣案例

| Question | Answer |
|----------|--------|
| **我可以匯出多個工作表嗎？** | 可以。使用 `workbook.getWorksheets()` 迴圈，對每個工作表呼叫 `save`，必要時可更改輸出檔名。 |
| **如果我的工作簿包含圖表怎麼辦？** | 圖表預設會以影像方式呈現。若要保留可編輯，必須手動將其轉換為 PowerPoint 形狀，這超出本指南範圍。 |
| **列印區域是必須的嗎？** | 不需要。若省略 `setPrintArea`，Aspose.Cells 會匯出工作表的整個使用範圍。設定列印區域可讓您精確控制。 |
| **這能適用於其他工具產生的 .xlsx 檔案嗎？** | 絕對可以。Aspose.Cells 支援任何符合規範的 Office Open XML 活頁簿，無論其來源為何。 |

## 後續步驟

- **將工作表儲存為 PowerPoint** 並使用自訂投影片版面配置：探索 Aspose.Slides 的 `Presentation` 類別，將匯出的投影片合併至更大的簡報。  
- **將 Excel 匯出為 pptx** 並使用不同影像解析度：調整 `exportOptions.setResolution(300)` 以取得高 DPI 輸出。  
- **自動化批次轉換**：將此程式碼與檔案監視器結合，處理資料夾中的多個 Excel 檔案。

透過精通 **set print area excel**、**export excel to pptx**、**convert worksheet to powerpoint** 與 **save worksheet as powerpoint**，您可以以程式方式將 Excel 資料整合至投影片，簡化報表流程，減少手動複製貼上的工作。

---

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，並以此為基礎。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.Cells for .NET 在 Excel 中設定列印區域](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [設定列印區域 Excel Aspose Cells .NET](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [設定列印區域 Excel Aspose Cells .NET](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}