---
category: general
date: 2026-08-14
description: 在使用 Aspose.Cells 將 Excel 匯出為 SVG 時嵌入字型。了解如何設定列印區域、列印選項，以及使用 WRAPCOLS
  函數。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: zh-hant
lastmod: 2026-08-14
og_description: 在使用 Aspose.Cells 將 Excel 匯出為 SVG 時嵌入字型。此指南說明如何設定列印區域、配置列印選項，以及套用 WRAPCOLS
  函數。
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: 在匯出 Excel 為 SVG 時嵌入字型 – 步驟說明
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: 在將 Excel 匯出為 SVG 時嵌入字型於 SVG
url: /zh-hant/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在匯出 Excel 為 SVG 時嵌入字型於 SVG 中

如果您需要 **在匯出 Excel 為 SVG 時嵌入字型於 SVG**，本教學將向您展示如何使用 Aspose.Cells for Java 完成此操作。我們還會說明如何 **設定列印區域**、**設定列印選項**，以及 **使用 WRAPCOLS 函數** 來格式化資料而不失去版面配置。

您將會一步步執行完整且可執行的範例，載入既有活頁簿、套用 `WRAPCOLS` 公式、設定 SVG 專屬的影像選項、定義列印區域，最後將檔案儲存為嵌入字型的 SVG。無需額外文件說明——只要複製程式碼、執行，即可檢視產生的 SVG。

## 嵌入字型於 SVG – 設定 ImageOrPrintOptions

嵌入字型可確保 SVG 的呈現與 Excel 中完全相同，即使在未安裝原始字型的機器上亦能正確顯示。

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*為什麼這很重要*：當啟用 `setEmbedFonts(true)` 時，Aspose.Cells 會直接將字型資料寫入 SVG 的 `<defs>` 區段。結果是一個自包含的檔案，在各瀏覽器與平台上顯示一致。

## 匯出 Excel 為 SVG – 完整工作流程

以下步驟說明從載入活頁簿到儲存 SVG 檔案的端對端流程。

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**預期輸出**：`output.svg` 會出現在 `YOUR_DIRECTORY`。在瀏覽器中開啟它會顯示工作表，所有字型皆已嵌入，資料因 `WRAPCOLS` 而換行成三欄，且僅渲染 `A1:H30` 內的儲存格。

## 為工作表設定列印區域

定義列印區域可將匯出的 SVG 限制在特定範圍內，減少檔案大小並將觀者焦點集中於相關資料。

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*提示*：範圍遵循 Excel 的 A1 表示法。如果需要動態範圍，可使用 `ws.getCells().getMaxDisplayRange()` 以程式方式計算。

## 為 SVG 輸出設定列印選項

列印選項控制 Aspose.Cells 如何將工作表轉換為影像。除了嵌入字型外，您還可以調整解析度、縮放比例與頁面版面配置。

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*為什麼要設定列印選項*：若未明確設定，Aspose.Cells 會使用預設值，可能會省略字型嵌入或套用不需要的縮放比例，導致 SVG 模糊或樣式不正確。

## 使用 WRAPCOLS 函數換列資料

`WRAPCOLS` 是一個 Excel 公式，可將垂直範圍分配成指定數量的欄位。當您想將長清單以緊湊格線顯示時，非常實用。

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

當活頁簿儲存時，Aspose.Cells 會評估此公式，於已定義的列印區域內產生三欄版面。此技巧適用於任何大小的範圍，只需將第二個參數調整為欲的欄數即可。

## 完整可執行範例

以下為完整的 Java 程式，您可直接貼到任意 IDE 中執行。請確保已將 Aspose.Cells for Java 套件加入 classpath。

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**驗證步驟**

1. 執行程式。  
2. 在網頁瀏覽器中開啟 `output.svg`。  
3. 確認文字使用的字型與原始 Excel 檔案相同（已嵌入字型）。  
4. 驗證僅顯示 `A1:H30` 內的儲存格，且 `A2:A10` 的資料已以三欄方式呈現。

## 常見陷阱與避免方法

| 問題 | 為何會發生 | 解決方法 |
|-------|----------------|-----|
| SVG 中缺少字型 | `setEmbedFonts(false)` 或字型檔案無法存取 | 確保 `setEmbedFonts(true)` 並且字型已安裝於執行程式的機器上 |
| WRAPCOLS 未計算 | 計算引擎被停用 | 在匯出前呼叫 `workbook.calculateFormula()`，或讓 Aspose.Cells 在儲存時自動計算 |
| 匯出的 SVG 為空白 | 列印區域未包含任何資料 | 再次確認傳遞給 `setPrintArea` 的範圍 |
| SVG 檔案過大 | 未套用縮放，影像解析度過高 | 調整 `imgOptions.setResolution(96)` 或類似設定以控制 DPI |

## 專業提示：在多個工作表重複使用 ImageOrPrintOptions

如果您的活頁簿包含多個需要相同 SVG 設定的工作表，請建立單一 `ImageOrPrintOptions` 實例，並將其指派給每個工作表的 `PageSetup`。此作法可減少記憶體使用，並確保所有匯出檔案的字型嵌入一致。

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## 下一步

* **匯出至其他向量格式** – 將 `ImageFormat.SVG` 改為 `ImageFormat.PDF` 可產生高品質 PDF。  
* **批次處理** – 迴圈處理資料夾中的 `.xlsx` 檔案，自動產生 SVG。  
* **自訂字型處理** – 使用 `FontSettings` 從特定目錄載入字型，當系統字型不足時可使用此方式。  

透過精通 **embed fonts in SVG**、**export excel to svg**、**set print area**、**set print options** 與 **use WRAPCOLS function**，您即可自動化產生高保真度的 SVG 報表、儀表板與網頁視覺化，直接從 Excel 資料轉換。祝開發順利！

## 接下來該學什麼？

以下教學涵蓋與本指南技術緊密相關的主題，並提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何在 Excel 中使用 Aspose.Cells for .NET 設定列印區域](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [在 Excel 中設定列印區域 – Aspose Cells .NET](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [在 Excel 中設定列印區域 – Aspose Cells .NET](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}