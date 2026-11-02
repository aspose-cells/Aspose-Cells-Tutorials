---
category: general
date: 2026-10-07
description: 學習如何在 Java 中從範圍建立 PNG 並將資料匯出為 PNG。本指南將示範如何使用 Aspose.Cells 儲存 Excel 範圍圖像。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: zh-hant
lastmod: 2026-10-07
og_description: 在 Java 中從範圍建立 PNG，並使用 Aspose.Cells 匯出資料為 PNG。跟隨此完整教學，即可即時儲存 Excel
  範圍圖像。
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: 在 Java 中從範圍建立 PNG – Aspose.Cells 一步一步指南
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何在 Java 中使用 Aspose.Cells 從範圍產生 PNG
url: /zh-hant/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose.Cells 從範圍建立 PNG

如果您需要在 Excel 活頁簿中 **create PNG from range**，本教學將完整示範如何操作。完成本指南後，您將能夠 **export data as PNG**，儲存 Excel 範圍圖像，並在報告或網頁中重複使用該檔案。

您將看到一個完整且可執行的 Java 程式，該程式會載入活頁簿、選取目標儲存格、將其渲染為 PNG，並將結果儲存至磁碟。無需任何外部工具——Aspose.Cells 內部處理所有工作。

## 本教學涵蓋內容

* Aspose.Cells 的先決條件與 Maven 設定
* 載入包含樞紐分析表或任何資料範圍的活頁簿
* 定義要轉換的精確儲存格範圍
* 設定 PNG 輸出的影像選項
* 渲染範圍並儲存 PNG 檔案
* 常見陷阱與高品質影像的技巧

完成這些步驟後，您將能夠 **convert worksheet to PNG** 任意範圍，無論是簡單表格或複雜的樞紐圖表。

## 先決條件

* Java 17 或更新版本（程式碼可於 JDK 11+ 編譯）
* Maven 3.6+（若偏好亦可使用 Gradle）
* Aspose.Cells for Java 23.12 或更新版本 – 請加入以下相依性
* 現有的 Excel 檔案（`PivotWithStyle.xlsx`），其中包含您想擷取的範圍

> **專業提示：** 若您沒有授權，仍可向 Aspose 申請臨時評估金鑰。此函式庫在評估模式下即可運作，無需額外設定。

### Maven 相依性

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## 步驟 1：載入包含目標範圍的活頁簿

第一步是開啟 Excel 檔案。Aspose.Cells 會將檔案讀入記憶體，無需 Microsoft Office。

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*為什麼這很重要*：載入活頁簿後，您即可取得工作表、儲存格以及渲染所需的頁面設定屬性。

## 步驟 2：存取包含該範圍的工作表

大多數活頁簿的預設工作表位於索引 0，但您也可以使用工作表名稱。

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

若您的資料位於其他工作表，請將 `0` 替換為相應的索引，或使用 `workbook.getWorksheets().get("SheetName")`。

## 步驟 3：定義要轉換的儲存格範圍

您可以使用 A1 標記法指定任意矩形區域。在本例中，我們擷取 `A1:D15`，它可能是樞紐分析表或一般資料區塊。

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*邊緣情況*：若範圍包含合併儲存格，Aspose.Cells 會自動擴展圖像以納入合併區域。

## 步驟 4：準備 PNG 影像選項

`ImageOrPrintOptions` 讓您控制格式、解析度及其他渲染細節。將儲存格式設定為 PNG 可確保無損品質。

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

提升 DPI 在來源儲存格包含小字體或精細圖表時特別有用。

## 步驟 5：將渲染區域限制為選取的範圍

將範圍指定為列印區域後，Aspose.Cells 只會渲染該部份儲存格，忽略工作表的其他部分。

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

若省略此步驟，整個工作表都會被光柵化，可能浪費記憶體且產生較大的圖像。

## 步驟 6：渲染範圍並將圖片加入工作表（可選）

若您想將產生的 PNG 嵌入回活頁簿（供預覽使用），可將其作為圖片加入。此步驟對於純匯出情境而言是可選的。

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*您可能這樣做的原因*：某些工作流程在發佈前需要將圖像納入活頁簿，例如製作混合原生儲存格與圖片的可列印報告。

## 步驟 7：將 PNG 檔案儲存至磁碟

最後，將圖像寫入檔案。`save` 方法會遵循 `imageOptions` 中指定的格式。

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

程式執行完畢後，`PivotImage.png` 將包含儲存格 `A1:D15` 的像素完美快照。

### 預期輸出

* 名為 `PivotImage.png`、位於 `YOUR_DIRECTORY` 的檔案。
* 圖像顯示選取範圍的完整版面配置、字型、顏色與邊框。
* 若來源範圍包含樞紐分析表，渲染出的圖像會保留與 Excel 中相同的樣式與計算結果。

## 處理常見情境

### 匯出非連續範圍

Aspose.Cells 無法在單一圖像中渲染不相連的範圍。若需匯出多個區域，請為每個範圍建立獨立圖像，然後使用影像處理函式庫（例如 ImageIO）在之後合併。

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### 將大型工作表儲存為 PNG

渲染跨越數千列的整張工作表會消耗大量記憶體。可透過以下方式減輕負擔：

* 降低 DPI（`imageOptions.setResolution(72)`）以產生較小的檔案。
* 使用 `setPageCount` 限制渲染的頁數。
* 透過 `worksheet.getPageSetup().setPrintArea(...)` 每次匯出一個可列印頁面。

### 保留儲存格公式

PNG 為點陣圖格式，無法保留公式。若下游使用者需要原始資料，請同時使用 `Range.exportDataTable()` 將範圍匯出為 CSV 或 JSON。

## 完整、可執行範例

以下為完整的 Java 類別，您可直接複製貼上至 IDE。請將 `YOUR_DIRECTORY` 替換為您機器上的絕對或相對路徑。

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

使用 `mvn compile exec:java`（或您偏好的建置工具）執行程式。執行完畢後，開啟 `PivotImage.png` 以驗證結果。

## 結論

您現在已掌握如何在 Java 中使用 Aspose.Cells **create PNG from range**，有效地 **export data as PNG** 並 **save excel range image**，以應對任何報告或分享情境。上述步驟——載入活頁簿、定義範圍、設定影像選項、設定列印區域以及儲存檔案——完整涵蓋 **convert worksheet to PNG** 與 **save cells as PNG** 的工作流程。

### 後續步驟

* 嘗試不同的 `Resolution` 值，以在品質與檔案大小之間取得平衡。
* 若需要透明背景的 PNG，請使用 `ImageOrPrintOptions.setTransparent(true)`。
* 使用 `PdfSaveOptions` 將多個範圍圖像合併為單一 PDF，以製作多頁報告。
* 透過變更 `setSaveFormat`，探索匯出至其他點陣格式（JPEG、BMP）。

歡迎將此模式套用於圖表、表格，甚至整張工作表。祝開發順利！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，並以此為基礎延伸技術。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索其他實作方式。

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Create Union Range in Excel using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}