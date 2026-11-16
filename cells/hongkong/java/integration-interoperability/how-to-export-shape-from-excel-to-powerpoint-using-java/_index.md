---
category: general
date: 2026-11-16
description: 學習如何在 Java 中將 Excel 圖形匯出至 PowerPoint、將 Excel 圖表轉換為 PPTX 檔案，並使用 Aspose.Cells
  儲存圖形為 PPTX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shape
- convert excel chart
- shape to powerpoint
- save shape pptx
- export shape from excel
language: zh-hant
lastmod: 2026-11-16
og_description: 如何在 Java 中將 Excel 的形狀匯出至 PowerPoint。跟隨本完整教學，將 Excel 圖表轉換、儲存形狀為 PPTX，並將形狀嵌入
  PowerPoint 檔案。
og_image_alt: Diagram illustrating how to export shape from Excel to PowerPoint using
  Java
og_title: 如何在 Java 中將 Excel 圖形匯出至 PowerPoint – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  headline: How to export shape from Excel to PowerPoint using Java
  type: TechArticle
- description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  name: How to export shape from Excel to PowerPoint using Java
  steps:
  - name: '**Load the workbook** that contains the shape.'
    text: '**Load the workbook** that contains the shape.'
  - name: '**Locate the shape** on the first worksheet.'
    text: '**Locate the shape** on the first worksheet.'
  - name: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
    text: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
  - name: '**Save the shape as a PPTX file**.'
    text: '**Save the shape as a PPTX file**.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
- PowerPoint integration
title: 如何使用 Java 從 Excel 匯出形狀至 PowerPoint
url: /zh-hant/java/integration-interoperability/how-to-export-shape-from-excel-to-powerpoint-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Java 從 Excel 匯出形狀至 PowerPoint

如果您需要 **how to export shape** 從 Excel 工作簿匯入至 PowerPoint 投影片，本指南將為您示範完整步驟。您將會看到如何 **convert Excel chart** 物件，將它們轉換為 **shape to PowerPoint**，最後以正確的匯出選項 **save shape PPTX**。

在程式化產生報告時，匯出形狀是一項常見需求。完成本教學後，您將擁有一個獨立的 Java 程式，可建立 `shape.pptx` 檔案以供簡報使用。無需外部腳本，且程式碼相容於 Aspose.Cells 2024‑R2 或更新版本。

## 前置條件

* Java 17 或更新版本（程式碼可在任何 JDK 8+ 上編譯）
* Aspose.Cells for Java 函式庫（從 Aspose 官方網站下載或加入 Maven 依賴）
* 包含至少一個形狀（圖表、文字方塊或 SmartArt）的 Excel 檔案（`chart.xls`）
* 具備基本的 Java 例外處理知識

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

## 如何從 Excel 匯出形狀至 PowerPoint（整體流程）

此流程包含四個邏輯段落：

1. **Load the workbook** 包含該形狀的工作簿。  
2. **Locate the shape** 在第一個工作表上。  
3. **Configure export options** 使形狀成為可編輯的 PowerPoint 物件。  
4. **Save the shape as a PPTX file**。

以下將逐一詳細說明每個段落，完整可執行的程式碼緊隨說明之後。

## 步驟 1：載入包含形狀的工作簿

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // Load the Excel workbook. Adjust the path to your environment.
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");
```

*Why this step?*  
`Workbook` 是所有 Aspose.Cells 操作的入口點。載入檔案後即可存取工作表、儲存格與形狀集合。若找不到檔案，Aspose.Cells 會拋出 `FileNotFoundException`，我們稍後會捕捉此例外。

## 步驟 2：存取第一個工作表並取得目標形狀

```java
            // Access the first worksheet (index 0)
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // Retrieve the first shape. In most examples the chart is the first shape.
            Shape shape = worksheet.getShapes().get(0);
```

*Why this step?*  
工作表以零基索引集合儲存，`get(0)` 會回傳第一張工作表。形狀亦以索引方式存取；`get(0)` 取得第一個形狀，通常就是您想匯出的圖表。若工作簿內有多個形狀，您可以遍歷集合或使用 `shape.getName()` 來挑選特定形狀。

## 步驟 3：準備匯出選項 – 我們希望形狀成為可編輯的 PPTX 物件

```java
            // Create export options. Setting the save format to PPTX tells Aspose.Cells
            // to generate a PowerPoint file rather than an image.
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);
```

*Why this step?*  
`ImageOrPrintOptions` 控制形狀的呈現方式。選擇 `SaveFormat.PPTX` 後，函式庫會將 Excel 圖形轉換為向量式 PowerPoint 形狀，匯入後仍可編輯。這對真正的 **shape to PowerPoint** 轉換至關重要；若使用 PNG 或 JPEG 會將圖形鎖定為圖片。

## 步驟 4：將形狀匯出為 PowerPoint 檔案

```java
            // Export the shape. The output file will contain a single slide with the shape.
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

*Why this step?*  
`save` 方法會依先前定義的選項寫入形狀。產生的 `shape.pptx` 包含單一投影片，形狀呈現與 Excel 中完全相同，但現在您可以在 PowerPoint 中編輯（變更顏色、調整大小、加入動畫等）。這符合 **save shape PPTX** 的需求。

## 完整、可執行範例

將整個類別複製到名為 `ExportShapeDemo.java` 的檔案中，將 `YOUR_DIRECTORY` 替換為絕對或相對路徑，然後執行 `javac ExportShapeDemo.java && java ExportShapeDemo`。執行完成後，您會在目標資料夾中找到 `shape.pptx`。

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook that contains the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");

            // 2. Access the first worksheet
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Retrieve the first shape (assumed to be a chart or textbox)
            Shape shape = worksheet.getShapes().get(0);

            // 4. Prepare export options – we want the shape as an editable PPTX object
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);

            // 5. Export the shape to a PowerPoint file
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            System.err.println("An error occurred while exporting the shape:");
            e.printStackTrace();
        }
    }
}
```

### 預期輸出

```
Export completed. File saved as shape.pptx
```

在 Microsoft PowerPoint 中開啟 `shape.pptx`。您會看到單一投影片，內含原始 Excel 圖表（或文字方塊），且為完整可編輯的 PowerPoint 形狀。

## 常見變體與邊緣情況

| 情況 | 建議調整 |
|-----------|------------------------|
| **Multiple shapes** | 遍歷 `worksheet.getShapes()` 並對每個形狀呼叫 `save`，或使用 `shape.getName()` 進行選取。 |
| **Shape is a chart with data series** | 使用 `exportOptions.setExportChartAsEditable(true)` 以保持資料系列可編輯。 |
| **Need a specific slide layout** | 儲存後，使用 Aspose.Slides 開啟 PPTX，將形狀插入自訂投影片版面配置。 |
| **Large workbook** | 僅使用 `Workbook(String, LoadOptions)` 載入所需工作表，以降低記憶體使用量。 |
| **Different output format (PDF, PNG)** | 將 `exportOptions.setSaveFormat(SaveFormat.PDF)` 或 `SaveFormat.PNG` 變更為其他輸出格式。當您 **convert Excel chart** 為靜態影像而非 PowerPoint 形狀時，此方式相當有用。 |

**Pro tip:** 請務必確認形狀索引 (`get(0)`) 與您欲匯出的視覺元素相符。形狀集合的順序與 Excel 中的插入順序相同，可能與視覺堆疊順序不同。

## 如何從 Excel 匯出形狀至 PowerPoint – 疑難排解清單

* **File not found** – 確認 `new Workbook()` 中的路徑指向現有的 `.xls` 或 `.xlsx` 檔案。  
* **No shapes returned** – 確認工作表確實包含形狀；您可以呼叫 `worksheet.getShapes().getCount()` 進行除錯。  
* **Exported file is empty** – 檢查是否已設定 `exportOptions.setSaveFormat(SaveFormat.PPTX)`；若使用影像格式會產生圖片而非形狀。  
* **Compatibility issues** – Aspose.Cells 24.9 以上版本支援在所有主要平台上匯出 PPTX。如遇到 `UnsupportedOperationException`，請升級。

## 結論

您現在已了解如何 **how to export shape** 從 Excel 工作簿並使用 Java 嵌入至 PowerPoint 簡報。教學涵蓋載入工作簿、定位形狀、設定 **export shape from Excel** 選項，最後 **save shape PPTX**。有了這個基礎，您可以自動化報告產生、建立儀表板，或將 Excel 視覺化內容整合至投影片中，無需手動複製貼上。

### 後續步驟

* 探索 **convert Excel chart** 至其他 Office 格式，例如 PDF 或 DOCX。  
* 將此技巧與 Aspose.Slides 結合，以在單一投影片上放置多個形狀。  
* 嘗試 `ImageOrPrintOptions` 屬性（例如 `setResolution`、`setTransparent`）以微調匯出形狀的視覺品質。

歡迎自行調整程式碼以支援批次處理，或整合至更大型的報告服務中。祝開發順利！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立於本教學所示技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [如何在 Java 中使用 ShapeExportOptions 匯出形狀](/cells/english/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/)
- [如何在 Java 中使用 Aspose.Cells 將 Excel 工作表匯出至 PowerPoint](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [如何將 Excel 圖表匯出至 PowerPoint – 完整 Java 指南](/cells/english/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}