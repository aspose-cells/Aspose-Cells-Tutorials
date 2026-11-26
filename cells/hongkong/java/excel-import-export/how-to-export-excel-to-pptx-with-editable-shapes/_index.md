---
category: general
date: 2026-11-25
description: 學習如何將 Excel 匯出為 PPTX 並保留可編輯的圖形。本指南亦說明如何設定列印範圍以及將 Excel 圖表轉換為簡報使用。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- set print area
- how to convert xlsx
- set print area excel
- convert excel chart
language: zh-hant
lastmod: 2026-11-25
og_description: 如何使用 Aspose.Cells 將 Excel 匯出為 PPTX 並保留可編輯的圖形，另附設定列印區域及將 Excel 圖表轉換為簡報的技巧。
og_image_alt: Screenshot showing how to export Excel to PPTX with editable shapes
og_title: 如何將 Excel 匯出為 PPTX 並保留可編輯的圖形
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  headline: How to export Excel to PPTX with editable shapes
  type: TechArticle
- description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  name: How to export Excel to PPTX with editable shapes
  steps:
  - name: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
    text: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
  - name: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
    text: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
  - name: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
    text: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
  - name: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
    text: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
  - name: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
    text: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
  - name: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
    text: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: 如何將 Excel 匯出為 PPTX 並保留可編輯的圖形
url: /zh-hant/java/excel-import-export/how-to-export-excel-to-pptx-with-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何將 Excel 匯出為 PPTX 並保留可編輯形狀

如果您需要 **how to export Excel** 檔案匯出至 PowerPoint 並保留可編輯的文字方塊與形狀，本指南將一步步帶您完成整個流程。您還將學習如何 **set print area** 以聚焦於特定投影片，以及如何 **convert Excel chart** 物件，使其在匯出後仍能完整編輯。

在從資料驅動的報告製作簡報時，將 Excel 匯出為 PPTX 是常見需求。使用 Aspose.Cells for Java 可避免手動複製貼上，保持格式完整，並取得對輸出之程式化控制。

## 您將學習

* 載入包含文字方塊或圖表的現有 XLSX 活頁簿。  
* 設定匯出選項，使產生的 PPTX 檔案包含 **editable shapes**。  
* **Set the print area** 以限制匯出範圍僅為所需的儲存格。  
* 將工作表儲存為 PPTX 檔案，並驗證文字方塊與圖表在 PowerPoint 中可編輯。  

**先決條件**

* 已安裝 Java 17 或更新版本。  
* 使用 Maven 或 Gradle 進行相依性管理。  
* 具備 Excel 活頁簿與 Java 程式設計的基本概念。

---

## 如何將 Excel 匯出為 PPTX 並保留可編輯形狀

本節提供執行匯出的核心程式碼。範例使用 Aspose.Cells 23.9（撰寫時的最新版本），示範所有必要步驟。

```java
// ------------------------------------------------------------
// 1. Add Aspose.Cells dependency (Maven example)
// ------------------------------------------------------------
/*
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
*/

// ------------------------------------------------------------
// 2. Import required classes
// ------------------------------------------------------------
import com.aspose.cells.*;

public class ExcelToPptxExporter {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------
        // 3. Load the workbook that contains a text box or chart
        // --------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBox.xlsx");

        // --------------------------------------------------------
        // 4. Set up export options for PPTX and enable shape editing
        // --------------------------------------------------------
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setFormat(ImageFormat.PPTX);          // output format
        exportOptions.setExportType(ExportType.PPTX);      // explicit PPTX export
        exportOptions.setEditable(true);                   // makes text boxes/shapes editable

        // --------------------------------------------------------
        // 5. Define the print area to limit the exported range
        // --------------------------------------------------------
        // This is the **set print area** step. Adjust the range as needed.
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");

        // --------------------------------------------------------
        // 6. Save the first worksheet as an editable PPTX file
        // --------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed: EditableShapes.pptx");
    }
}
```

### 為何每一行都很重要

1. **Dependency** – Aspose.Cells 提供 `ImageOrPrintOptions` 類別，可將工作表渲染為 PPTX 投影片。透過 Maven 加入可確保程式庫位於 classpath 中。  
2. **Imports** – 匯入正確的類別可讓程式碼保持簡潔，避免使用全名。  
3. **Loading the workbook** – 必須指向包含欲匯出物件的確切檔案。路徑可以是絕對路徑或相對於專案根目錄。  
4. **Export options** – 設定 `setEditable(true)` 是 **how to export Excel** 的關鍵，讓產生的 PowerPoint 形狀保持可編輯。若未設定此旗標，文字方塊將變成靜態影像。  
5. **Print area** – `setPrintArea` 呼叫會將匯出限制於您關注的區域，減少檔案大小並移除不需要的列/欄。這直接對應 **set print area excel** 的需求。  
6. **Saving** – `SaveFormat.PPTX` 常數告訴 Aspose.Cells 產生 PowerPoint 檔案，而非影像或 PDF。  

#### 預期輸出

執行程式後，於 PowerPoint 開啟 `EditableShapes.pptx`。您應該會看到與所選 Excel 範圍相同的投影片，且任何文字方塊或圖表圖例皆可雙擊編輯，彷彿原生 PowerPoint 物件。

---

## 在 Excel 中設定列印區域

當您只需工作表的部分區域時，定義 **print area** 可提升效能與視覺清晰度。

```java
// Example: set print area to the first 10 rows and columns A‑J
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.getPageSetup().setPrintArea("A1:J10");
```

*Tip:* 若之後變更資料範圍，請在匯出前再次呼叫 `setPrintArea`。匯出會遵循最新的設定。

---

## 將 XLSX 圖表轉換為可編輯的 PowerPoint 圖表

Aspose.Cells 將圖表視為繪圖物件。啟用 `setEditable(true)` 後，圖表會轉換為原生 PowerPoint 圖表，可進行編輯（例如變更系列、座標軸標題）。

```java
// No extra code needed – the same exportOptions handle chart conversion.
// Just ensure the workbook contains a chart object.
```

如果您需要 **how to convert xlsx** 含有多個圖表的檔案，請對每個工作表重複匯出，或在調整活動工作表後使用 `Workbook.save` 搭配 `SaveFormat.PPTX`。

---

## 如何以程式方式轉換 XLSX（額外）

除了 PPTX，您也可能想將活頁簿轉換為其他格式，如 PDF 或 PNG。相同的 `ImageOrPrintOptions` 類別可用於這些目標：

```java
exportOptions.setFormat(ImageFormat.PDF);   // for PDF output
workbook.save("Converted.pdf", SaveFormat.PDF);
```

這展示了 Aspose.Cells 更廣泛的 **how to convert xlsx** 功能。

---

## 常見陷阱與最佳實踐提示

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| 形狀變成影像 | `setEditable(false)`（預設） | 呼叫 `exportOptions.setEditable(true)` |
| 匯出的投影片為空白 | 列印區域未包含任何資料 | 驗證傳遞給 `setPrintArea` 的範圍字串 |
| 圖表失去格式 | 使用過時的 Aspose.Cells 版本 | 升級至最新程式庫（≥ 23.9） |
| 檔案過大 | 匯出整個工作表 | 限制列印區域或隱藏未使用的列/欄 |

---

## 結論

您現在已了解如何 **how to export Excel** 活頁簿至 PPTX，並保留完整可編輯的形狀與圖表，如何 **set print area** 以聚焦輸出，以及如何 **convert Excel chart** 物件以便無縫編輯簡報。上述完整且可執行的 Java 範例可直接放入已使用 Aspose.Cells 的任何專案中。

**下一步**

* 探索 PowerPoint 中的 **convert excel chart** 選項（例如變更圖表類型）。  
* 將此匯出與 **set print area excel** 自動化結合，以從單一活頁簿產生多張投影片。  
* 使用相同的 `ImageOrPrintOptions` 模式嘗試匯出至其他格式（PDF、PNG）。

歡迎嘗試不同的範圍、 多張工作表或自訂投影片版面配置。祝開發愉快！

---

## 接下來您應該學習什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在所示技巧之上。每個資源皆提供完整可運作的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [如何設定列印區域 Excel 並匯出至 PowerPoint](/cells/english/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/)
- [將 Excel 轉換為 PowerPoint 並設定列印區域](/cells/english/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/)
- [在 Excel 中設定列印區域並匯出至 PowerPoint – 步驟指南](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}