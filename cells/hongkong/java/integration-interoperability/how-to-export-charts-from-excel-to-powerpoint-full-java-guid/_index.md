---
category: general
date: 2026-06-27
description: 如何使用 Java 將 Excel 圖表匯出至 PowerPoint。學習將試算表轉換為 PowerPoint、儲存 PPTX 檔案，並輕鬆匯出
  Excel 資料至 PPT。
draft: false
keywords:
- how to export charts
- convert spreadsheet to powerpoint
- how to save pptx
- excel to powerpoint slide
- export excel data ppt
language: zh-hant
og_description: 如何在 Java 中將 Excel 圖表匯出至 PowerPoint。此一步一步的指南會示範如何將試算表轉換為 PowerPoint、儲存
  PPTX 檔案，以及匯出 Excel 資料至 PPT。
og_title: 如何將 Excel 圖表匯出至 PowerPoint – Java 教學
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to export charts from Excel to PowerPoint using Java. Learn to
    convert spreadsheet to PowerPoint, save PPTX files, and export Excel data PPT
    effortlessly.
  headline: How to Export Charts from Excel to PowerPoint – Full Java Guide
  type: TechArticle
- description: How to export charts from Excel to PowerPoint using Java. Learn to
    convert spreadsheet to PowerPoint, save PPTX files, and export Excel data PPT
    effortlessly.
  name: How to Export Charts from Excel to PowerPoint – Full Java Guide
  steps:
  - name: '**Load** the workbook you want to transform.'
    text: '**Load** the workbook you want to transform.'
  - name: '**Configure** a `PresentationOptions` instance to tell Aspose which elements
      (charts, OLE objects, etc.) should make it into the slide deck.'
    text: '**Configure** a `PresentationOptions` instance to tell Aspose which elements
      (charts, OLE objects, etc.) should make it into the slide deck.'
  - name: '**Save** the workbook using the `PPTX` format and the options you configured.'
    text: '**Save** the workbook using the `PPTX` format and the options you configured.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- PowerPoint
title: 如何將 Excel 圖表匯出至 PowerPoint – 完整 Java 指南
url: /zh-hant/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何從 Excel 匯出圖表至 PowerPoint – 完整 Java 教學

有沒有想過 **如何直接將 Excel 工作簿中的圖表匯出** 到 PowerPoint 投影片？你並不是唯一有此需求的人——開發者常常需要把以資料為驅動的試算表轉換成可直接使用的簡報，而不必手動複製貼上。本文將一步步示範一個乾淨、程式化的解決方案，讓你 **將試算表轉換為 PowerPoint**、將結果儲存為 PPTX，甚至在執行時微調圖表的處理方式。

完成後，你將得到一段可直接執行的 Java 程式碼，能夠讀取任意工作簿、擷取其中的圖表（如需亦可擷取 OLE 物件），並輸出一個精緻的 **excel to powerpoint slide** 檔案。無需額外 UI、無需繁雜的 VBA，只有純粹的 Java 程式碼，今天就能放入你的專案中使用。

## 前置條件

在開始之前，請確保你已具備：

- **Java 17** 或更新版本（此 API 在任何近期 JDK 上皆可運作）
- **Aspose.Cells for Java** 套件（程式碼會使用 `PresentationOptions` 與 `SaveFormat.PPTX`）
- 基本的 Java 專案設定知識（Maven / Gradle）
- 一個包含至少一個圖表的 Excel 檔案（`.xlsx`）

如果缺少 Aspose.Cells 的 JAR，請透過 Maven 加入：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

或直接從 Aspose 官方網站下載 JAR，並放置於 classpath 中。

## 匯出圖表概觀

整體流程如下：

1. **載入** 需要轉換的工作簿。
2. **設定** `PresentationOptions` 以告訴 Aspose 哪些元素（圖表、OLE 物件等）需要納入投影片。
3. **儲存** 工作簿為 `PPTX` 格式，並套用先前設定的選項。

就這樣。函式庫會負責繁重的工作——將每個圖表渲染為向量圖形、保留版面配置，並產生 PowerPoint 檔案，讓 PowerPoint 本身可以順利開啟且不會出現異常。

以下將逐步說明每個步驟、解釋 *為什麼* 這麼做，以及提供完整程式碼範例。

## 步驟 1：載入工作簿並設定匯出選項

首先，我們需要告訴 Aspose 在建立 PowerPoint 時要包含哪些內容。`PresentationOptions` 類別提供了細緻的控制。設定 `setExportCharts(true)` 可確保每個圖表都會成為投影片元素；而 `setExportOleObjects(true)` 則會將任何內嵌物件（例如 Excel 表格）一併帶入。

```java
import com.aspose.cells.*;

public class ExcelToPowerPointExporter {

    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source Excel workbook
        // -------------------------------------------------
        String srcPath = "C:/data/sourceWorkbook.xlsx";
        Workbook workbook = new Workbook(srcPath);

        // -------------------------------------------------
        // 2️⃣ Configure presentation export options
        // -------------------------------------------------
        PresentationOptions presentationOptions = new PresentationOptions();
        presentationOptions.setExportCharts(true);          // <-- how to export charts
        presentationOptions.setExportOleObjects(true);     // include embedded OLE objects

        // The next lines are optional but often useful:
        presentationOptions.setExportFormulas(false);      // skip raw formulas if you only need visuals
        presentationOptions.setExportImages(true);         // grab any pictures as well
```

**此步驟的重要性：**  
若未呼叫 `setExportCharts(true)`，Aspose 會把圖表當作普通儲存格處理，將資料直接寫入投影片，而非以視覺圖表呈現，這樣就失去了簡報的意義。同樣地，開關 OLE 匯出可讓你保留複雜物件（如樞紐分析表）而不必額外撰寫程式碼。

> **小技巧：** 處理大型工作簿時，考慮關閉 `setExportFormulas` 以加快轉換速度。視覺輸出不會受影響，但記憶體佔用會較低。

## 步驟 2：將工作簿儲存為 PowerPoint 檔案

選項設定完成後，實際的轉換只需要一行程式碼：使用 `SaveFormat.PPTX` 呼叫 `workbook.save(...)`。這正是我們在 Java 中回答 **如何儲存 pptx** 的關鍵。

```java
        // -------------------------------------------------
        // 3️⃣ Save the workbook as a PowerPoint file
        // -------------------------------------------------
        String outPath = "C:/output/slide.pptx";
        workbook.save(outPath, SaveFormat.PPTX, presentationOptions);

        System.out.println("✅ Conversion complete! Check " + outPath);
    }
}
```

**底層發生了什麼？**  
Aspose 會遍歷每個工作表，擷取所有圖表，將其轉換為 PowerPoint 形狀（通常為 EMF 向量），並放置於新投影片上。若有多個工作表，預設會為每個工作表產生一張投影片。之後你可以使用 Apache POI 或 PowerPoint 本身重新排列投影片順序。

### 預期結果

在 Microsoft PowerPoint 中開啟 `slide.pptx`，應看到：

- 每個工作表（或每個圖表）對應一張投影片
- 圖表以銳利的方式呈現，保留顏色與資料標籤
- 任何 OLE 物件（如內嵌的 Excel 表格）以可編輯的形式出現

若未看到圖表，請再次確認來源工作簿確實包含圖表物件，且 `setExportCharts(true)` 未在其他地方被覆寫。

## 變形方案：將單一圖表匯出為獨立 PPTX

有時只需要 **excel to powerpoint slide** 的特定圖表，而非整本工作簿。這時可以先建立一個只包含目標圖表的暫存工作簿，再進行匯出。

```java
        // -------------------------------------------------
        // 4️⃣ Export a single chart (optional)
        // -------------------------------------------------
        // Assume the chart is on the first worksheet, first chart
        Worksheet sheet = workbook.getWorksheets().get(0);
        int chartIndex = 0; // change if you have multiple charts
        Chart chart = sheet.getCharts().get(chartIndex);

        // Clone the chart into a new workbook
        Workbook singleChartWb = new Workbook();
        Worksheet newSheet = singleChartWb.getWorksheets().get(0);
        newSheet.getCharts().addCopy(chart);

        // Use the same PresentationOptions
        singleChartWb.save("C:/output/singleChart.pptx", SaveFormat.PPTX, presentationOptions);
```

**為什麼會需要這樣做：**  
如果你在即時產生投影片（例如報表服務每封郵件只附送一張圖表），建立最小化的工作簿可以減少記憶體使用量並加快處理速度。

## 常見問題與避免方式

| 問題 | 症狀 | 解決方案 |
|------|------|----------|
| 圖表消失 | 投影片為空白或只顯示資料表格 | 確保在 `workbook.save` 之前呼叫 `presentationOptions.setExportCharts(true)`。 |
| 檔案過大 | PPTX 超過 30 MB（即使只有少量圖表） | 關閉影像匯出 (`setExportImages(false)`) 或在 PowerPoint 中壓縮影像。 |
| OLE 物件遺失 | 內嵌的 Excel 表格變成靜態影像 | 設定 `setExportOleObjects(true)`；同時確認來源 OLE 物件未被保護。 |
| 相容性錯誤 | PowerPoint 顯示檔案損毀 | 使用最新版本的 Aspose.Cells；舊版可能在 PPTX 產生上有 bug。 |

## 在 CI/CD 流程中匯出圖表

若你在建置過程中自動產生報表，可將上述程式碼嵌入 Maven 外掛或 Gradle 任務。務必確保 JVM 有足夠的堆疊記憶體（例如 `-Xmx2g`），以處理大型工作簿。

```groovy
task exportCharts(type: JavaExec) {
    classpath = sourceSets.main.runtimeClasspath
    main = 'com.example.ExcelToPowerPointExporter'
    args = []
    jvmArgs = ['-Xmx2g']
}
```

執行 `./gradlew exportCharts` 後即可自動產生 PPTX，無需任何人工介入——非常適合夜間報表工作。

## 完整範例（可直接複製貼上）

以下提供一個完整、獨立的 Java 類別，你可以直接放入任何 IDE。程式碼已包含所有匯入、錯誤處理與說明註解。

```java
// FullExample.java
import com.aspose.cells.*;

public class FullExample {
    public static void main(String[] args) {
        try {
            // 👉 1️⃣ Load the Excel workbook you want to convert
            String srcFile = "C:/data/analysis.xlsx";
            Workbook wb = new Workbook(srcFile);

            // 👉 2️⃣ Set up export options – this is the core of how to export charts
            PresentationOptions opts = new PresentationOptions();
            opts.setExportCharts(true);          // include every chart
            opts.setExportOleObjects(true);     // keep OLE objects (tables, etc.)
            opts.setExportImages(true);         // optionally keep pictures
            opts.setExportFormulas(false);      // skip formulas for speed

            // 👉 3️⃣ Choose where the PPTX will be saved – answer to how to save pptx
            String outFile = "C:/output/analysis.pptx";

            // 👉 4️⃣ Perform the conversion
            wb.save(outFile, SaveFormat.PPTX, opts);

            System.out.println("✅ Excel file converted to PowerPoint successfully!");
        } catch (Exception e) {
            System.err.println("❌ Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

執行此類別，開啟 `analysis.pptx`，即可看到原始試算表中的每張圖表都已順利轉換至 PowerPoint。這就是 **export excel data ppt** 的核心——全程自動、無手動複製貼上。

## 視覺摘要

![說明如何使用 Aspose.Cells 從 Excel 匯出圖表至 PowerPoint 的流程圖](/images/export-charts-diagram.png "如何從 Excel 匯出圖表至 PowerPoint")

*上圖說明了從 Excel 工作簿 → PresentationOptions → PPTX 檔案的整體流程。*

## 結論

我們已完整說明 **如何從 Excel 匯出圖表** 至 PowerPoint（使用 Java），示範了將 **spreadsheet 轉換為 PowerPoint** 所需的精確程式碼，並解釋了 **如何可靠地儲存 pptx**。透過調整 `PresentationOptions`，你可以掌控圖表、OLE 物件等所有細節，為資料分析與簡報層之間架起彈性橋樑。

接下來的建議？試著結合 **Apache POI** 以程式方式重新排列投影片，或將此轉換流程嵌入 Spring Boot 微服務，讓 PPTX 報表即時提供。你也可以探索使用相同函式庫匯出至 **PDF** 或 **HTML**——Aspose.Cells 讓這些需求變得相當簡單。

有任何關於特殊情境的問題，歡迎提出，

## 接下來該學什麼？

以下教學與本篇內容緊密相關，能幫助你進一步掌握 API 功能，並探索其他實作方式：

- [How to Create and Export Charts in Java Using Aspose.Cells&#58; A Complete Guide](/cells/english/java/charts-graphs/aspose-cells-java-create-export-charts/)
- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Export Excel Charts to PDF Using Aspose.Cells for Java&#58; Custom Page Sizes Guide](/cells/english/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}