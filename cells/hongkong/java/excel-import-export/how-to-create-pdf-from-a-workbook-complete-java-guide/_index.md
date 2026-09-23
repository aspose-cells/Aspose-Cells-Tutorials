---
category: general
date: 2026-03-01
description: 如何使用 Aspose.Cells for Java 建立 PDF 並將工作簿另存為 PDF、將 Excel 匯出為 HTML，以及使用
  Expand 功能。附有逐步程式碼示例。
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: zh-hant
og_description: 如何使用 Aspose.Cells for Java 從工作簿建立 PDF。學習將工作簿另存為 PDF、將 Excel 匯出為 HTML，以及使用
  EXPAND 函數。
og_title: 如何從工作簿產生 PDF – Java 教學
tags:
- Aspose.Cells
- Java
- PDF generation
title: 如何從工作簿建立 PDF – 完整 Java 指南
url: /zh-hant/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何從活頁簿建立 PDF – 完整 Java 指南

是否曾經想過 **如何直接從 Excel 活頁簿建立 PDF**，而不必使用第三方轉換工具？你並不孤單。許多開發人員在需要快速 PDF 匯出、HTML 預覽或炫酷的陣列公式時，常常卡住——一次就想搞定。  

在本教學中，我們將逐步說明一個完整且獨立的 Java 程式，正好能達成上述需求。我們會 **將活頁簿儲存為 PDF**，示範如何 **將 Excel 匯出為 HTML** 並保留凍結列，並展示在工作表中 **使用 EXPAND 函數**。完成後，你將擁有一個可直接放入任何 Maven 或 Gradle 專案的可執行範例。

> **小技巧：** 以下所有程式碼皆適用於 Aspose.Cells 23.10（或更新版本）。若你使用較舊的版本，部分方法名稱可能會略有不同。

---

## 前置條件

- **Java 17**（或任何 LTS 版本）已安裝並設定。
- **Aspose.Cells for Java** 函式庫。將以下 Maven 依賴加入你的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- 你喜歡的 IDE 或文字編輯器（IntelliJ IDEA、VS Code、Eclipse…）。

不需外部 API、也不需 Web 服務——僅使用純 Java 以及 Aspose.Cells SDK。

---

## 解決方案概觀

我們將把實作分為 **七個邏輯步驟**：

1. 建立活頁簿並示範 **EXPAND** 函數。  
2. 啟用字型變體選擇器，並 **將活頁簿儲存為 PDF**。  
3. 將同一活頁簿匯出為 HTML，同時保留凍結列。  
4. 使用帶有 `IF` 參數的 Smart Marker 以注入條件文字。  
5. 套用主‑從 Smart Marker 以處理階層資料。  
6. 載入包含 Base‑64 編碼圖片的 Markdown 檔案。  
7. 設定 GridJs 選項以調整對齊與邊框，然後插入資料。

每個步驟皆封裝於獨立的方法中，以保持 `main` 方法簡潔，並說明 **為何** 要這樣做，而不只是 **做了什麼**。

---

## 步驟 1 – 建立活頁簿並使用 EXPAND 函數

**EXPAND** 函數是 Office 365 中推出的全新動態陣列公式。它允許你將範圍自動展開至更大的區域，而無需手動複製儲存格。

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**為何重要：**  
- `EXPAND` 會自動在結果中填入空白，這對於之後 **將活頁簿儲存為 PDF** 極為理想——PDF 會呈現整齊的矩形表格。  
- 呼叫 `calculateFormula()` 可確保公式引擎在匯出前已執行。

---

## 步驟 2 – 啟用字型變體選擇器並 **將活頁簿儲存為 PDF**

若需支援進階排版（例如 emoji 或中日韓變體選擇器），必須在儲存之前 **開啟** 此功能。

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**重點：** 這裡解答了主要關鍵字 **how to create pdf**——在設定完畢後呼叫 `workbook.save(..., SaveFormat.PDF)` 即可。

---

## 步驟 3 – **將 Excel 匯出為 HTML** 同時保留凍結列

常常有利害關係人需要快速的網頁預覽。Aspose.Cells 能匯出為 HTML，且透過 `setPreserveFrozenRows(true)` 可保留與 Excel 相同的捲動體驗。

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**為何在乎：** 凍結列是一項使用便利性；若未保留，使用者在捲動頁面時，標題列會消失。

---

## 步驟 4 – 帶 IF 參數的 Smart Marker

Smart Marker 讓你在不撰寫迴圈的情況下將資料合併至模板。`if` 參數直接在標記內加入條件邏輯。

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

輸出的 PDF 會顯示 **「VIP Customer: Acme Corp」**，因為 `IsVIP` 為 `true`。將旗標改為 `false` 後，則會得到 **「Regular Customer: Acme Corp」**——不需要額外程式碼。

---

## 步驟 5 – 使用階層範圍的主‑從 Smart Marker

當你有父子資料（例如訂單與明細項目）時，主‑從標記可免除手動插入列的工作。

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**你能得到的好處：** 引擎會為每筆訂單展開主列，並自動在其下方嵌入明細列——非常適合發票或採購報表。

---

## 步驟 6 – 載入含嵌入式 Base‑64 圖片的 Markdown 文件

如果你的來源資料以 Markdown 形式存在（在文件流程中很常見），Aspose.Cells 能直接將其渲染至活頁簿。

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**邊緣情況說明：** 若 Base‑64 字串格式錯誤，Aspose 會跳過該圖片，繼續處理文件的其他部分——不會當機。

---

## 步驟 7 – 設定 GridJs 選項並插入資料

GridJs 是一個輕量級的 JavaScript 表格，Aspose 可將其渲染為 HTML。對齊數字並套用邊框可提升可讀性。

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**為何在乎：** 正確的對齊與邊框讓產生的 HTML 看起來像精緻的試算表——對於儀表板非常有用。

---

## 完整整合 – `main` 方法

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}