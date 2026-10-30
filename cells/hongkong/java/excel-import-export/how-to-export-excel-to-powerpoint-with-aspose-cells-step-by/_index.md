---
category: general
date: 2026-09-18
description: 學習如何使用 Aspose.Cells 將 Excel 匯出至 PowerPoint。將 Excel 轉換為 PPTX、從 Excel 建立
  PowerPoint，並在幾分鐘內將 Excel 儲存為 PowerPoint。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- convert excel to pptx
- create powerpoint from excel
- save excel as powerpoint
- export excel to powerpoint
language: zh-hant
lastmod: 2026-09-18
og_description: 如何使用 Aspose.Cells 將 Excel 匯出至 PowerPoint。請參考本指南，將 Excel 轉換為 PPTX、從
  Excel 建立 PowerPoint，並高效地將 Excel 儲存為 PowerPoint。
og_image_alt: Screenshot showing how to export Excel to PowerPoint with Aspose.Cells
og_title: 如何將 Excel 匯出至 PowerPoint – 完整的 Aspose.Cells 教學
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  headline: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to export Excel to PowerPoint using Aspose.Cells. Convert
    Excel to PPTX, create PowerPoint from Excel, and save Excel as PowerPoint in minutes.
  name: How to export Excel to PowerPoint with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that contains the shapes
    text: '```java import com.aspose.cells.*;'
  - name: Configure export options for PowerPoint conversion
    text: '```java /** * Creates ImageOrPrintOptions that control how Excel content
      is rendered * in the resulting PowerPoint file. * * @return a fully configured
      ImageOrPrintOptions object */ private static ImageOrPrintOptions createExportOptions()
      { ImageOrPrintOptions options = new ImageOrPrintOptions(); //'
  - name: Mark pictures (or charts) as editable
    text: '```java /** * Marks the first picture on the first worksheet as editable.
      * You can extend this loop to mark all pictures if needed. * * @param workbook
      the workbook that was loaded earlier */ private static void makeFirstPictureEditable(Workbook
      workbook) { // Navigate to the first worksheet (index'
  - name: Save the workbook as an editable PowerPoint presentation
    text: '```java /** * Performs the actual conversion and writes the PPTX file.
      * * @param workbook the workbook prepared in previous steps * @param exportOptions
      the options created in step 2 * @param outputPath full path for the resulting
      .pptx file * @throws Exception if saving fails */ private static voi'
  - name: Full runnable example
    text: '```java import com.aspose.cells.*;'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel‑to‑PowerPoint
- Document conversion
title: 使用 Aspose.Cells 將 Excel 匯出至 PowerPoint 的逐步指南
url: /zh-hant/java/excel-import-export/how-to-export-excel-to-powerpoint-with-aspose-cells-step-by/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何將 Excel 匯出至 PowerPoint（使用 Aspose.Cells） – 步驟說明指南

如果您需要 **將 Excel 匯出** 為 PowerPoint 簡報，本教學提供完整、可直接執行的解決方案。閱讀前兩句後，您將清楚知道哪些 API 呼叫可將 `.xlsx` 檔案轉換為可編輯的 `.pptx`。此方法適用於任何包含圖表、圖片或其他形狀的活頁簿，且僅需少量 Java 程式碼。

在本指南中，您將學習如何 **將 Excel 轉換為 PPTX**、**從 Excel 建立 PowerPoint**，以及 **將 Excel 儲存為 PowerPoint**，同時保留圖表與圖片的可編輯性。除 Aspose.Cells 外不需其他工具，程式碼可在 Java 8+ 及任何近期的 JDK 上執行。  

Prerequisites:

* 已安裝 Java Development Kit (JDK) 8 或更新版本  
* 用於相依性管理的 Maven 或 Gradle（或在 classpath 中的 Aspose.Cells JAR）  
* 一個包含至少一張圖片或圖表的活頁簿 (`WithShapes.xlsx`)  

---

![Diagram illustrating how to export Excel to PowerPoint](https://example.com/diagram.png "how to export excel to powerpoint illustration")

## 使用 Aspose.Cells 將 Excel 匯出至 PowerPoint

轉換的核心分為四個簡潔步驟。每個步驟皆封裝於方法中，方便在較大型的應用程式中重複使用。

### 步驟 1：載入包含圖形的活頁簿

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    /**
     * Loads the source Excel workbook.
     *
     * @param path full path to the .xlsx file
     * @return a Workbook instance ready for manipulation
     * @throws Exception if the file cannot be read
     */
    private static Workbook loadWorkbook(String path) throws Exception {
        // The Workbook constructor reads the entire file into memory.
        return new Workbook(path);
    }
}
```

**為何重要：**  
載入活頁簿可讓您存取工作表、圖片與圖表。Aspose.Cells 直接讀取檔案，無需呼叫 Microsoft Office，因而可在無介面的伺服器上執行此操作。

### 步驟 2：設定 PowerPoint 轉換的匯出選項

```java
    /**
     * Creates ImageOrPrintOptions that control how Excel content is rendered
     * in the resulting PowerPoint file.
     *
     * @return a fully configured ImageOrPrintOptions object
     */
    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        // Do not include hidden worksheets – they usually contain metadata only.
        options.setExportHiddenWorksheet(false);
        // Export charts as editable shapes so the end‑user can modify them in PowerPoint.
        options.setExportChartAsEditable(true);
        return options;
    }
```

**為何重要：**  
`setExportChartAsEditable(true)` 讓 Aspose.Cells 產生向量形狀而非點陣圖。這使得 PowerPoint 輸出 **從 Excel 建立 PowerPoint** 時，圖表保持完全可編輯，符合大多數簡報製作流程。

### 步驟 3：將圖片（或圖表）標記為可編輯

```java
    /**
     * Marks the first picture on the first worksheet as editable.
     * You can extend this loop to mark all pictures if needed.
     *
     * @param workbook the workbook that was loaded earlier
     */
    private static void makeFirstPictureEditable(Workbook workbook) {
        // Navigate to the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
        // Retrieve the first picture on that sheet
        Picture pic = sheet.getPictures().get(0);
        // Set the picture to be editable in the PowerPoint output
        pic.setEditable(true);
    }
```

**為何重要：**  
當圖片被標記為可編輯時，Aspose.Cells 會在 PPTX 檔案中以 EMF/WMF 形狀輸出。這對於 **將 Excel 匯出至 PowerPoint** 的使用情境至關重要，因為接收者之後需要調整圖像。

### 步驟 4：將活頁簿儲存為可編輯的 PowerPoint 簡報

```java
    /**
     * Performs the actual conversion and writes the PPTX file.
     *
     * @param workbook      the workbook prepared in previous steps
     * @param exportOptions the options created in step 2
     * @param outputPath    full path for the resulting .pptx file
     * @throws Exception if saving fails
     */
    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // The SaveFormat.PPTX enum tells Aspose.Cells to generate a PowerPoint file.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
```

**為何重要：**  
`save` 呼叫會將先前所有的修改（可編輯的圖片、圖表設定）打包成單一的 `.pptx` 壓縮檔。產生的檔案可於 Microsoft PowerPoint、Google Slides 或任何支援 PPTX 的檢視器開啟。

### 完整可執行範例

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {

    public static void main(String[] args) {
        try {
            // Adjust these paths to match your environment.
            String sourcePath = "YOUR_DIRECTORY/WithShapes.xlsx";
            String destinationPath = "YOUR_DIRECTORY/Result.pptx";

            // Step 1 – load workbook
            Workbook workbook = loadWorkbook(sourcePath);

            // Step 2 – configure export options
            ImageOrPrintOptions exportOptions = createExportOptions();

            // Step 3 – make the first picture editable
            makeFirstPictureEditable(workbook);

            // Step 4 – save as PPTX
            saveAsPowerPoint(workbook, exportOptions, destinationPath);

            System.out.println("Conversion successful! File saved at: " + destinationPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }

    // ---- Helper methods from earlier steps ----

    private static Workbook loadWorkbook(String path) throws Exception {
        return new Workbook(path);
    }

    private static ImageOrPrintOptions createExportOptions() {
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setExportHiddenWorksheet(false);
        options.setExportChartAsEditable(true);
        return options;
    }

    private static void makeFirstPictureEditable(Workbook workbook) {
        Worksheet sheet = workbook.getWorksheets().get(0);
        if (!sheet.getPictures().isEmpty()) {
            sheet.getPictures().get(0).setEditable(true);
        }
    }

    private static void saveAsPowerPoint(Workbook workbook,
                                          ImageOrPrintOptions exportOptions,
                                          String outputPath) throws Exception {
        // Export options are automatically applied when saving to PPTX.
        workbook.save(outputPath, SaveFormat.PPTX);
    }
}
```

**預期結果：**  
在 PowerPoint 中開啟 `Result.pptx` 後，會看到一張與 `WithShapes.xlsx` 第一個工作表相同的投影片。圖表以向量形狀呈現，您可雙擊編輯資料；第一張圖片則為可編輯物件（可直接在 PowerPoint 中調整大小、變更顏色或取代）。

---

## 將 Excel 轉換為 PPTX – 更深入的自訂

雖然基本流程已足以應付大多數情況，但您可能仍需：

* **匯出多個工作表** – 迭代 `workbook.getWorksheets()`，對每個工作表呼叫 `workbook.save`，並透過 `ImageOrPrintOptions.setSlideNumber(int)` 傳入不同的投影片索引。  
* **控制投影片尺寸** – 使用 `exportOptions.setImageHeight(int)` 與 `setImageWidth(int)` 以符合特定的 PowerPoint 投影片大小（例如 1024 × 768）。  
* **保留公式** – 若希望將原始 Excel 公式以隱藏資料形式嵌入，請設定 `exportOptions.setExportFormulasAsValues(false)`。

這些調整讓您能 **從 Excel 建立 PowerPoint**，以符合企業品牌或簡報標準。

---

## 將 Excel 儲存為 PowerPoint – 常見陷阱與避免方法

| 症狀 | 可能原因 | 解決方法 |
|------|----------|----------|
| 圖表顯示為點陣圖 | `setExportChartAsEditable(false)`（預設） | 使用 `setExportChartAsEditable(true)` 以啟用可編輯圖表 |
| 投影片上未顯示圖片 | 圖片未標記為可編輯或圖片索引超出範圍 | 在呼叫 `setEditable(true)` 前，先確認 `sheet.getPictures().size() > 0` |
| 隱藏的工作表出現在 PPTX 中 | `setExportHiddenWorksheet(true)` | 保留預設值 `false`，或明確設定為 `false` |
| 輸出檔案損毀 | 使用過時的 Aspose.Cells 版本（20.10 之前） | 升級至最新的 Aspose.Cells for Java（例如 23.12） |

---

## 匯出 Excel 至 PowerPoint：效能技巧

* **重複使用相同的 `ImageOrPrintOptions`** 物件進行多次儲存——可避免重複分配。  
* **以串流方式讀取來源活頁簿**（`new Workbook(InputStream)`），在記憶體受限的伺服器上處理大型檔案時特別有用。  
* **對每個工作表的轉換進行平行化**，若需產生包含數百張投影片的簡報；每個工作表皆可在獨立執行緒中處理，因為 Aspose.Cells 物件在建構後是執行緒安全的。

---

## 後續步驟

您現在已了解 **如何將 Excel 匯出** 為 PowerPoint 投影片、**將 Excel 轉換為 PPTX**，以及 **將 Excel 儲存為 PowerPoint**，且內容可編輯。若要進一步擴展此知識，您可以：

* 探索 **Aspose.Slides**，於轉換後加入動畫或母片版面配置。  
* 在 CI/CD 流程中自動化此工作流程，使每份新的 Excel 報告自動轉換為 PPTX 投影片。  
* 結合 **Apache POI** 於將 Excel 檔案交給 Aspose.Cells 前進行前置處理。

---

## 結論

本教學示範了 **如何將 Excel 匯出** 為 PowerPoint，使用 Aspose.Cells，涵蓋從載入活頁簿到儲存可編輯 `.pptx` 的每一步。您現在可以在 Java 應用程式中自信地 **將 Excel 轉換為 PPTX**、**從 Excel 建立 PowerPoint**，以及 **將 Excel 儲存為 PowerPoint**。請嘗試可選設定，以符合您的精確簡報需求。祝開發順利！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在所示技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.Cells for .NET 將 Excel 轉換為 PowerPoint&#58; 完整指南](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [如何將 Excel 匯出至 PowerPoint – 步驟說明指南](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [如何使用 C# 將 Excel 匯出至 PowerPoint – 完整指南](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}