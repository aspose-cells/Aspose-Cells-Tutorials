---
category: general
date: 2026-09-21
description: 使用 Aspose.Cells 在 Java 中將 Excel 轉換為 PowerPoint 簡報 – 學習如何將圖表匯出為 PPTX，並僅用幾行程式碼將活頁簿儲存為
  PPTX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- save workbook as pptx
- how to export chart to pptx
- create powerpoint from excel chart
language: zh-hant
lastmod: 2026-09-21
og_description: 使用 Aspose.Cells（Java）將 Excel 轉換為 PowerPoint。本教學示範如何將圖表匯出為 PPTX，並將活頁簿另存為含可編輯文字方塊的
  PPTX。
og_image_alt: Screenshot of Java code converting an Excel workbook to a PowerPoint
  presentation
og_title: 使用 Aspose.Cells 將 Excel 轉換為 PowerPoint – Java 指南
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Convert Excel to PowerPoint with Aspose.Cells in Java – learn how to
    export chart to PPTX and save workbook as PPTX in just a few lines of code.
  headline: Convert Excel to PowerPoint with Aspose.Cells in Java
  type: TechArticle
- questions:
  - answer: Yes. Loop through each worksheet, export its chart to a new slide using
      `PdfSaveOptions`, and then save the workbook once after processing all sheets.
    question: Can I convert multiple worksheets into separate PowerPoint slides?
  - answer: Only chart and textbox objects are transferred to PowerPoint. Cell formatting
      stays in the Excel file; it does not appear in the PPTX.
    question: Does this method preserve cell formatting?
  - answer: 'Use `SaveFormat.PDF` and the same `PdfSaveOptions`. The `setExportEditableTextBoxes`
      flag works for PDF as well. ## Next steps Now that you know how to **save workbook
      as PPTX** and **export chart to PPTX**, you might explore: * Adding multiple
      charts to different slides (`create powerpoint from exc'
    question: What if I need to export to PDF instead of PPTX?
  type: FAQPage
tags:
- Excel
- PowerPoint
- Aspose.Cells
- Java
title: 使用 Aspose.Cells 在 Java 中將 Excel 轉換為 PowerPoint
url: /zh-hant/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells for Java 將 Excel 轉換為 PowerPoint

如果您需要 **將 Excel 轉換為 PowerPoint**，本指南將向您展示一種簡潔、可投入生產的做法。您將看到如何將圖表匯出為 PPTX、保持文字方塊可編輯，並且只需三行 Java 程式碼即可 **將活頁簿另存為 PPTX**。

許多開發者會將資料匯出為 PDF，但對於需要即時圖表與可編輯元素的簡報而言，PowerPoint 往往更為合適。本教學涵蓋從專案設定到常見問題處理的全部步驟，讓您能在 Java IDE 中直接從 Excel 圖表建立 PowerPoint。

## 前置條件

開始之前，請確保您已具備：

* 已安裝 Java 17 或更新版本。
* 使用 Maven（或 Gradle）管理相依性。
* 取得 Aspose.Cells for Java 授權（免費試用版可用於評估）。
* 一個包含至少一個圖表與文字方塊的 Excel 檔案（`ChartAndTextbox.xlsx`）。

## 步驟 1：將 Aspose.Cells 加入專案

首先需要在專案中加入 Aspose.Cells 程式庫。使用 Maven 時，將以下相依性加入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **專業提示：** 若您使用 Gradle，等效的寫法是：
> ```groovy
> implementation 'com.aspose:aspose-cells:24.9'
> ```

加入程式庫後，即可使用 `Workbook`、`PdfSaveOptions` 以及 `SaveFormat` 列舉等在轉換過程中必需的類別。

## 步驟 2：載入包含圖表與文字方塊的活頁簿

現在載入 Excel 檔案。`Workbook` 類別會將整個活頁簿讀入記憶體，保留圖表、公式與文字方塊等內容。

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust the path to point to your Excel file
        String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(sourcePath);
        
        // Continue with conversion...
    }
}
```

**為什麼這很重要：** 先載入活頁簿可確保所有嵌入的物件（圖表、圖片、文字方塊）在匯出時皆可取得。若檔案找不到，Aspose.Cells 會拋出明確的 `FileNotFoundException`，您可以捕捉此例外以提供更好的使用者體驗。

## 步驟 3：設定匯出選項以保持文字方塊可編輯

Aspose.Cells 透過 `PdfSaveOptions` 來控制目標格式為 PowerPoint 時的物件寫入方式。啟用 `setExportEditableTextBoxes(true)` 後，Excel 工作表中的任何文字方塊在轉換後仍可編輯。

```java
import com.aspose.cells.PdfSaveOptions;

PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.setExportEditableTextBoxes(true); // Text boxes stay editable in the PPTX
```

> **為什麼要在 PPTX 中使用 `PdfSaveOptions`？**  
> 在內部，Aspose.Cells 會重複使用 PDF 渲染管線來產生 PowerPoint 輸出，從而提供對可編輯元素的細緻控制。設定此旗標是保留文字方塊可編輯性的推薦做法。

## 步驟 4：將活頁簿另存為 PowerPoint 簡報

最後，使用 `SaveFormat.PPTX` 呼叫 `workbook.save`。此步驟即完成 **從 Excel 圖表建立 PowerPoint** 的工作流程。

```java
import com.aspose.cells.SaveFormat;

String targetPath = "YOUR_DIRECTORY/Result.pptx";
workbook.save(targetPath, SaveFormat.PPTX, saveOptions);
System.out.println("Conversion successful! PPTX saved to " + targetPath);
```

將上述程式碼組合起來，完整程式如下：

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.PdfSaveOptions;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook containing the chart and textbox
            String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Create PDF save options and enable editable text boxes for PPTX output
            PdfSaveOptions saveOptions = new PdfSaveOptions();
            saveOptions.setExportEditableTextBoxes(true); // text boxes will remain editable in the PPTX

            // 3. Save the workbook as a PowerPoint presentation using the configured options
            String targetPath = "YOUR_DIRECTORY/Result.pptx";
            workbook.save(targetPath, SaveFormat.PPTX, saveOptions);

            System.out.println("Conversion successful! PPTX saved to " + targetPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### 預期輸出

執行程式後會在主控台印出：

```
Conversion successful! PPTX saved to YOUR_DIRECTORY/Result.pptx
```

開啟 `Result.pptx`（Microsoft PowerPoint）時，您會看到：

* 原始 Excel 圖表以原生 PowerPoint 圖表形式呈現（可在 PowerPoint 的圖表編輯器中編輯）。
* Excel 中的文字方塊以可編輯的圖形出現，您可以直接在投影片上修改文字。

## 處理常見邊緣情況

| 情況 | 建議做法 |
|-----------|----------------------|
| **找不到檔案** | 在 `Workbook` 建構子外層加入 `try‑catch`，並顯示清晰的錯誤訊息。 |
| **活頁簿沒有圖表** | 在轉換前先檢查工作表是否包含圖表（`worksheet.getCharts().getCount() > 0`），若無則跳過或加入佔位圖表。 |
| **大型 Excel 檔案** | 增加 JVM 堆積大小（`-Xmx2g`），以避免渲染過程中發生 `OutOfMemoryError`。 |
| **未設定授權** | 在載入活頁簿之前呼叫 `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` 以移除評估水印。 |

## 常見問題

**Q: 我可以將多個工作表分別匯出成不同的 PowerPoint 投影片嗎？**  
A: 可以。遍歷每個工作表，使用 `PdfSaveOptions` 將其圖表匯出至新投影片，最後在處理完所有工作表後一次性儲存活頁簿。

**Q: 此方法會保留儲存格的格式嗎？**  
A: 只會將圖表與文字方塊物件轉移至 PowerPoint。儲存格格式仍保留在 Excel 檔案中，並不會出現在 PPTX 中。

**Q: 若想匯出為 PDF 而非 PPTX，該怎麼做？**  
A: 使用 `SaveFormat.PDF` 並搭配相同的 `PdfSaveOptions`。`setExportEditableTextBoxes` 旗標在 PDF 輸出時同樣有效。

## 後續步驟

了解了如何 **將活頁簿另存為 PPTX** 以及 **將圖表匯出為 PPTX** 後，您可以進一步探索：

* 透過迴圈將多個圖表加入不同投影片（`create powerpoint from excel chart`）。
* 使用 Aspose.Slides for Java 自訂投影片版面，打造更豐富的簡報樣式。
* 使用 `Picture` 類別將 Excel 儲存格中的圖片嵌入 PowerPoint。

這些延伸功能讓您能建構全自動的報表管線，直接從 Excel 資料產出精緻的簡報。

---

**摘要：** 本教學示範了使用 Aspose.Cells for Java **將 Excel 轉換為 PowerPoint** 的可靠方法。透過載入活頁簿、設定 `PdfSaveOptions` 以保持文字方塊可編輯，並以 `SaveFormat.PPTX` 儲存，您即可取得包含即時圖表與可編輯形狀的 PowerPoint 檔案，完美適用於動態商業簡報。歡迎將此程式碼套用於批次處理或整合至更大型的報表解決方案中。

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化您對 API 功能的掌握，並探索在專案中實作的其他方式。

- [如何使用 Aspose.Cells for Java 建立帶趨勢線的 Excel 圖表並匯出為影像](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [如何使用 Aspose.Cells for Java 將 Excel 圖表轉換為 SVG](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 在 Java 中將 Excel 轉換為 PDF：一步步教學](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}