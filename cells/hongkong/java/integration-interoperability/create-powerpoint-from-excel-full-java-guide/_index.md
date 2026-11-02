---
category: general
date: 2026-06-21
description: 使用 Java 快速從 Excel 建立 PowerPoint。學習如何在一步一步的教學中使用 Aspose.Cells 將 XLSX 轉換為
  PPTX。
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- how to convert xlsx
- how to export excel
- excel workbook to powerpoint
language: zh-hant
og_description: 使用 Java 從 Excel 建立 PowerPoint。本教學精確示範如何使用 Aspose.Cells 將 XLSX 轉換為
  PPTX，涵蓋程式碼、常見問題與技巧。
og_title: 從 Excel 建立 PowerPoint – Java 轉換指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PowerPoint from Excel quickly using Java. Learn how to convert
    XLSX to PPTX with Aspose.Cells in a step‑by‑step tutorial.
  headline: Create PowerPoint from Excel – Full Java Guide
  type: TechArticle
- description: Create PowerPoint from Excel quickly using Java. Learn how to convert
    XLSX to PPTX with Aspose.Cells in a step‑by‑step tutorial.
  name: Create PowerPoint from Excel – Full Java Guide
  steps:
  - name: Expected Output
    text: '- A file named `shapes.pptx` appears in `YOUR_DIRECTORY`. - Opening the
      PPTX in Microsoft PowerPoint shows one slide per worksheet, with all cell formatting,
      charts, and shapes preserved as raster images. - No manual copy‑pasting required—your
      data is now presentation‑ready.'
  - name: 5.1 Large Workbooks or High‑Resolution Slides
    text: 'If your Excel file contains many rows, charts, or high‑resolution graphics,
      the generated PPTX can become bulky. You can reduce file size by:'
  - name: 5.2 Preserving Vector Graphics
    text: If you need vector‑based charts (so they stay crisp when zoomed), Aspose.Cells
      also supports `SaveFormat.SVG` for each slide, then you can assemble an SVG‑based
      PPTX manually. This is more advanced and beyond the scope of this quick guide,
      but worth exploring for design‑heavy decks.
  - name: 5.3 Multiple Worksheets per Slide
    text: Sometimes you want two related worksheets side‑by‑side on a single slide.
      Set `options.setOnePagePerSheet(false);` and use `WorksheetCollection` to control
      the range you render per slide.
  - name: 5.4 Automating Batch Conversions
    text: If you have a folder full of Excel files, wrap the conversion logic inside
      a loop that iterates over `File[] files = new File("YOUR_DIRECTORY").listFiles((dir,
      name) -> name.endsWith(".xlsx"));`. This way you can **convert excel to powerpoint**
      en masse.
  - name: Expected Result Screenshot
    text: '![create powerpoint from excel example](https://example.com/images/create-powerpoint-from-excel.png
      "create powerpoint from excel")'
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells supports both `.xls` and `.xlsx`. Just point
      `Workbook` at the old file; the rest of the code stays identical.
    question: Can I convert an `.xls` (old Excel) file?
  - answer: No. The conversion rasterizes the sheet, so formulas become static values
      on the slide. If you need editable data in PowerPoint, consider exporting to
      CSV and using PowerPoint’s table insertion APIs instead.
    question: Does this method retain formulas?
  - answer: Load the workbook with `loadOptions.setPassword("yourPassword");` before
      creating the `Workbook` object.
    question: What about password‑protected workbooks?
  - answer: 'Not directly via `ImageOrPrintOptions`. You’d need to post‑process the
      generated PPTX with Aspose.Slides for Java, adding notes to each slide programmatically.
      ## Full Working Example – Paste and Run Below is the complete, ready‑to‑run
      program. Copy it into a file named `ExcelToPowerPoint.java`, adj'
    question: Is there a way to add speaker notes automatically?
  type: FAQPage
tags:
- java
- excel
- powerpoint
- file-conversion
title: 從 Excel 建立 PowerPoint – 完整 Java 教學
url: /zh-hant/java/integration-interoperability/create-powerpoint-from-excel-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 Excel 建立 PowerPoint – 完整 Java 教學

有沒有想過 **從 Excel 建立 PowerPoint** 而不必手動開啟兩個應用程式？你並不是唯一有此需求的人。許多人需要將資料豐富的試算表轉換成可直接用於簡報的投影片，無論是每週的銷售回顧還是快速的利害關係人更新。好消息是，只要寫幾行 Java 程式碼，就能自動完成整個流程——不需要複製貼上，也不需要手動排版。

在本教學中，我們將示範如何使用 Aspose.Cells for Java 將 **Excel 活頁簿轉換為 PowerPoint**。完成後，你將擁有一個可執行的程式，能把 `.xlsx` 檔案輸出為精美的 `.pptx` 檔案，直接用於下一次會議。我們也會提供 **如何有效匯出 Excel** 資料的技巧，讓你能將此解決方案套用到自己的專案中。

## 前置條件 – 你需要的環境

在開始之前，請確保你的機器上已具備以下項目：

- **Java Development Kit (JDK) 8 或更新版本** – 程式碼在任何近期的 JDK 上皆可執行。
- **Aspose.Cells for Java** 函式庫（免費試用版已足夠測試）。可從 Maven Central 取得或直接下載 JAR。
- 一個 **Excel 活頁簿**（範例中使用 `shapes.xlsx`），放在可參照的目錄下。
- 一個 **開發環境** – 如 IntelliJ IDEA、Eclipse，或甚至是簡易的文字編輯器搭配命令列編譯皆可。

準備好了嗎？那就開始吧。

## 步驟 1：建立專案並匯入相依性

先建立一個新的 Maven（或 Gradle）專案，並將 Aspose.Cells 加入相依性。如果你偏好手動方式，只要把 `aspose-cells-xx.x.jar` 放到 `libs` 資料夾，並加入 classpath 即可。

```xml
<!-- Maven pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest version -->
</dependency>
```

此步驟的重要性：若沒有此函式庫，Java 本身無法原生 **convert excel to powerpoint**。Aspose.Cells 承擔了繁重的工作，會在背後把每個工作表轉成投影片圖像。

## 步驟 2：載入 Excel 活頁簿

接下來載入來源活頁簿。這與原始程式碼的第一行相同，但我們會將它包在 try‑catch 區塊中，以提升穩定性。

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Define paths – adjust as needed
        String inputPath = "YOUR_DIRECTORY/shapes.xlsx";
        String outputPath = "YOUR_DIRECTORY/shapes.pptx";

        try {
            // Step 1: Load the Excel workbook
            Workbook workbook = new Workbook(inputPath);
            System.out.println("Workbook loaded successfully.");
```

請注意我們使用 `Workbook workbook = new Workbook(inputPath);`。這一行正是 **how to convert xlsx** 的核心——它會把整個試算表載入記憶體，準備後續處理。

## 步驟 3：設定 ImageOrPrintOptions 以產出 PowerPoint

Aspose.Cells 將 PowerPoint 轉換視為影像或列印操作。我們會建立 `ImageOrPrintOptions` 物件，將目標格式設為 PPTX，並視需要調整解析度或投影片尺寸。

```java
            // Step 2: Create options for image/print conversion and set the target format to PPTX
            ImageOrPrintOptions options = new ImageOrPrintOptions();
            options.setSaveFormat(SaveFormat.PPTX);      // PPTX is the modern PowerPoint format
            options.setOnePagePerSheet(true);           // Each worksheet becomes a separate slide
            options.setImageFormat(ImageFormat.Png);    // Use PNG for crisp slide graphics
            options.setQuality(100);                    // Max quality for clearer images
```

為什麼要設定 `OnePagePerSheet`？因為大多數簡報都希望 **每個工作表對應一張投影片**，以保留在 Excel 中設計的版面配置。如果需要每張工作表產生多張投影片，可稍後切換此旗標。

## 步驟 4：將活頁簿儲存為 PowerPoint 簡報

在設定完成後，最後一行程式會把 PPTX 檔寫入磁碟。

```java
            // Step 3: Save the workbook as a PowerPoint presentation
            workbook.save(outputPath, options);
            System.out.println("Conversion complete! PowerPoint saved at: " + outputPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

就這樣——**excel workbook to powerpoint** 只需三個簡潔步驟。執行程式後，Aspose.Cells 會將每張工作表渲染成投影片圖像，嵌入新的 PPTX 檔，並儲存至你指定的位置。

### 預期輸出

- 會在 `YOUR_DIRECTORY` 中產生名為 `shapes.pptx` 的檔案。
- 用 Microsoft PowerPoint 開啟該 PPTX，會看到 **每個工作表對應一張投影片**，且所有儲存格格式、圖表與圖形皆以點陣圖方式保留。
- 不需要 **手動複製貼上**——你的 **資料** 已經變成 **簡報就緒**。

## 步驟 5：處理常見情境與例外情況

雖然核心轉換相當 **straightforward**，但實務專案常會碰到一些小問題。以下提供實用技巧，幫助你避免頭痛。

### 5.1 大型活頁簿或高解析度投影片

如果 Excel 檔案包含大量列、圖表或高解析度圖形，產生的 PPTX 可能會變得相當龐大。可透過以下方式縮減檔案大小：

- 降低 `options.setResolution(150);`（預設為 220 DPI）。
- 改用 `options.setImageFormat(ImageFormat.Jpeg);` 並調整壓縮品質。
- 在轉換前先將活頁簿切割成較小的檔案。

```java
options.setResolution(150);          // Reduce DPI to shrink image size
options.setImageFormat(ImageFormat.Jpeg);
options.setQuality(80);              // JPEG quality (0‑100)
```

### 5.2 保留向量圖形

若需要向量圖表（在放大時仍保持銳利），Aspose.Cells 也支援每張投影片使用 `SaveFormat.SVG`，之後可自行組合成 SVG 為基礎的 PPTX。此方式較進階，超出本快速指南範圍，但對於設計密集型的簡報值得探索。

### 5.3 每張投影片顯示多個工作表

有時你希望在同一張投影片上並排顯示兩個相關工作表。將 `options.setOnePagePerSheet(false);`，再使用 `WorksheetCollection` 來控制每張投影片要渲染的範圍。

```java
options.setOnePagePerSheet(false);
Worksheet sheet1 = workbook.getWorksheets().get(0);
Worksheet sheet2 = workbook.getWorksheets().get(1);
// Render both sheets onto a single slide using custom positioning logic.
```

### 5.4 批次自動轉換

若資料夾內有大量 Excel 檔案，可將轉換邏輯包在迴圈中，遍歷 `File[] files = new File("YOUR_DIRECTORY").listFiles((dir, name) -> name.endsWith(".xlsx"));`。如此即可 **convert excel to powerpoint** 大量執行。

```java
File dir = new File("YOUR_DIRECTORY");
File[] excelFiles = dir.listFiles((d, n) -> n.toLowerCase().endsWith(".xlsx"));
for (File excel : excelFiles) {
    String pptxPath = excel.getAbsolutePath().replace(".xlsx", ".pptx");
    Workbook wb = new Workbook(excel.getAbsolutePath());
    wb.save(pptxPath, options);
    System.out.println("Converted: " + excel.getName());
}
```

## 常見問題 (FAQ)

**Q: 能否轉換 `.xls`（舊版 Excel）檔案？**  
A: 當然可以。Aspose.Cells 同時支援 `.xls` 與 `.xlsx`。只要把 `Workbook` 指向舊檔，其他程式碼保持不變。

**Q: 這個方法會保留公式嗎？**  
A: 不會。轉換會將工作表光柵化，公式會變成投影片上的靜態值。若需要在 PowerPoint 中編輯資料，可考慮先匯出為 CSV，然後使用 PowerPoint 的表格插入 API。

**Q: 密碼保護的活頁簿該怎麼處理？**  
A: 在建立 `Workbook` 物件前，先使用 `loadOptions.setPassword("yourPassword");` 來載入受保護的檔案。

**Q: 有辦法自動加入講者備註嗎？**  
A: `ImageOrPrintOptions` 本身無法直接加入備註。你需要使用 Aspose.Slides for Java 於產生的 PPTX 之上進行後處理，程式化地為每張投影片加入備註。

## 完整範例 – 複製後執行

以下提供完整、可直接執行的程式碼。將它貼到名為 `ExcelToPowerPoint.java` 的檔案中，調整路徑後執行 `javac` + `java`，或在 IDE 中執行。

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust these paths to match your environment
        String inputPath = "YOUR_DIRECTORY/shapes.xlsx";
        String outputPath = "YOUR_DIRECTORY/shapes.pptx";

        try {
            // Load the workbook (how to export excel)
            Workbook workbook = new Workbook(inputPath);
            System.out.println("Workbook loaded.");

            // Configure conversion options (convert excel to powerpoint)
            ImageOrPrintOptions options = new ImageOrPrintOptions();
            options.setSaveFormat(SaveFormat.PPTX);
            options.setOnePagePerSheet(true);
            options.setImageFormat(ImageFormat.Png);
            options.setQuality(100);
            options.setResolution(220); // default DPI

            // Perform the conversion
            workbook.save(outputPath, options);
            System.out.println("PowerPoint created at: " + outputPath);
        } catch (Exception e) {
            System.err.println("Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### 預期結果截圖

![create powerpoint from excel example](https://example.com/images/create-powerpoint-from-excel.png "create powerpoint from excel")

*（圖示顯示由 Excel 工作表產生的 PowerPoint 投影片，保留了儲存格邊框與圖表。）*

## 結論

以上即是使用 Java **create PowerPoint from Excel** 的完整端對端解決方案。我們說明了關鍵程式碼，闡述了 **how to export excel** 資料為 PPTX 投影片，並討論了大型檔案與批次處理等常見問題。

現在，你可以自動化每週的簡報更新、即時產生客戶可用的簡報，或將此轉換流程整合到更大的報表管線中。想更進一步？可以嘗試加入自訂投影片標題、嵌入超連結，或使用 Aspose.Slides 進一步合併輸出結果。

## 接下來該學什麼？

以下教學與本篇內容密切相關，能幫助你延伸技巧與探索其他 API 功能。每篇資源皆提供完整程式範例與逐步說明，方便你在自己的專案中實作。

- [How to Convert Excel to PDF in Java Using Aspose.Cells: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [How to Convert Excel Sheets to XPS Format Using Aspose.Cells Java](/cells/english/java/workbook-operations/render-excel-to-xps-aspose-cells-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}