---
category: general
date: 2026-11-22
description: 使用 Aspose.Cells 在 Java 中將 Excel 轉換為 PowerPoint。了解如何從 Excel 檔案建立 PowerPoint、將工作表匯出為
  PPTX 投影片，以及自動化簡報。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- create powerpoint from excel file
- convert excel workbook to pptx slides
- java convert .xlsx to .pptx
language: zh-hant
lastmod: 2026-11-22
og_description: 使用 Aspose.Cells 在 Java 中將 Excel 轉換為 PowerPoint。本教學示範如何從 Excel 檔案建立
  PowerPoint，並將 .xlsx 匯出為 .pptx 投影片。
og_image_alt: Diagram illustrating convert excel to powerpoint workflow
og_title: 在 Java 中將 Excel 轉換為 PowerPoint – 完整程式設計指南
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  headline: Convert Excel to PowerPoint in Java – step‑by‑step guide
  type: TechArticle
- description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  name: Convert Excel to PowerPoint in Java – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: Converting only selected sheets
    text: 'If you want to **convert Excel workbook to PPTX slides** but exclude certain
      worksheets, filter them before saving:'
  - name: Handling large workbooks
    text: 'For workbooks with many sheets, memory consumption can become significant.
      Use `WorkbookSettings` to enable streaming:'
  - name: Preserving formulas
    text: Aspose.Cells evaluates formulas before rendering. If you need the raw formula
      text on the slide, set `opts.setExportFormulas(true)`.
  type: HowTo
tags:
- java
- excel
- powerpoint
- aspose
title: 在 Java 中將 Excel 轉換為 PowerPoint – 步驟教學
url: /zh-hant/java/integration-interoperability/convert-excel-to-powerpoint-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中將 Excel 轉換為 PowerPoint – 步驟說明

如果您需要 **在 Java 中將 Excel 轉換為 PowerPoint**，本指南將示範如何使用 Aspose.Cells 完成。無論您是構建報表引擎還是自動化投影片，都會學會以程式方式 **從 Excel 檔案建立 PowerPoint**，並將每個工作表匯出為可編輯的 PPTX 投影片。

本教學涵蓋從專案設定到儲存最終簡報的全部步驟。完成後，您將擁有一個可執行的 Java 程式，能將 `.xlsx` 活頁簿轉換為可在 Microsoft PowerPoint 中編輯的 `.pptx` 檔案。無需手動複製貼上。

## 前置條件

* 已安裝 Java 17 或更新版本（程式碼使用現代模組系統）。  
* Aspose.Cells for Java 授權或臨時評估金鑰。  
* 用於相依管理的 Maven 或 Gradle（範例使用 Maven）。  
* 放置於已知目錄的範例 Excel 活頁簿（`input.xlsx`）。

> **小技巧：** Aspose.Cells 同時支援 `.xls` 與 `.xlsx`。相同程式碼可用於任一格式，只需更改檔案副檔名。

## 步驟 1：設定 Java 專案以 **convert Excel to PowerPoint**

建立一個新的 Maven 專案（或加入現有專案），並加入 Aspose.Cells 相依性：

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>excel-to-pptx</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <!-- Aspose.Cells for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest version as of 2026 -->
        </dependency>
    </dependencies>
</project>
```

執行 `mvn clean install` 以下載函式庫。若您有授權檔案（`Aspose.Total.lic`），請放置於 `src/main/resources` 資料夾；程式碼會自動載入。

## 步驟 2：載入 Excel 活頁簿

在 **convert excel workbook to pptx slides** 流程中的第一個功能步驟是載入來源檔案。Aspose.Cells 可從檔案系統、串流或甚至位元組陣列開啟檔案。

```java
package com.example;

import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // Load the license (optional for evaluation)
        License license = new License();
        try {
            license.setLicense(ExcelToPowerPoint.class.getResourceAsStream("/Aspose.Total.lic"));
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }

        // Path to the source .xlsx file
        String inputPath = "YOUR_DIRECTORY/input.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);
        System.out.println("Workbook loaded successfully.");
```

**為什麼這很重要：** 載入活頁簿會驗證檔案格式，並準備內部結構，供 Aspose.Cells 稍後轉換為 PowerPoint 物件。

## 步驟 3：設定儲存選項以 **create PowerPoint from Excel file**

Aspose.Cells 使用 `ImageOrPrintOptions` 來定義轉換為簡報檔案時的輸出格式。將 `SaveFormat` 設為 `SaveFormat.PPTX` 即可產生可編輯的投影片。

```java
        // Step 3: Set up conversion options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PPTX);          // Export as PPTX
        opts.setOnePagePerSheet(false);               // Each sheet becomes a separate slide
        opts.setRenderToSize(1024, 768);               // Optional: control slide resolution
        System.out.println("Conversion options configured.");
```

**為什麼這很重要：** `setOnePagePerSheet(false)` 旗標告訴 Aspose.Cells 將每個工作表視為單獨的投影片，這是您在 **convert Excel to PowerPoint** 用於簡報時最常見的情況。

## 步驟 4：將活頁簿儲存為 PPTX 投影片

現在您可以將簡報寫入磁碟。`Workbook.save` 方法接受輸出路徑以及先前設定的選項。

```java
        // Step 4: Export the workbook to a PowerPoint file
        String outputPath = "YOUR_DIRECTORY/editable.pptx";
        wb.save(outputPath, opts);
        System.out.println("Conversion complete. PowerPoint saved to: " + outputPath);
    }
}
```

當您在 Microsoft PowerPoint 中開啟 `editable.pptx` 時，會看到每個工作表對應一張投影片，所有儲存格皆以可編輯的文字方塊和圖形呈現。您還可以直接在 PowerPoint 中進一步編輯字型、顏色或加入動畫。

### 預期輸出

執行程式會輸出：

```
Workbook loaded successfully.
Conversion options configured.
Conversion complete. PowerPoint saved to: YOUR_DIRECTORY/editable.pptx
```

而檔案 `editable.pptx` 會出現在指定目錄中，已可供手動微調或進一步自動化使用。

## 步驟 5：常見變形與邊緣案例

### 僅轉換選取的工作表

如果您想 **convert Excel workbook to PPTX slides** 但排除特定工作表，請在儲存前先過濾它們：

```java
        // Example: Export only the first two worksheets
        int[] sheetIndices = {0, 1};
        wb.save(outputPath, opts, sheetIndices);
```

### 處理大型活頁簿

對於包含大量工作表的活頁簿，記憶體使用量可能會顯著增加。請使用 `WorkbookSettings` 以啟用串流：

```java
        wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

### 保留公式

Aspose.Cells 會在呈現前評估公式。若您需要在投影片上保留原始公式文字，請設定 `opts.setExportFormulas(true)`。

## 步驟 6：以程式方式驗證結果（可選）

您可以使用 Aspose.Slides 載入產生的 PPTX，以確認投影片數量與工作表數量相符：

```java
import com.aspose.slides.*;

        Presentation pres = new Presentation(outputPath);
        int slideCount = pres.getSlides().size();
        System.out.println("Generated PPTX contains " + slideCount + " slides.");
```

此額外檢查在 CI 流程中很有用，可用於斷言轉換是否成功。

## 結論

您現在擁有一套完整、可投入生產的 **convert Excel to PowerPoint in Java** 解決方案。程式會載入 `.xlsx` 活頁簿，設定 `ImageOrPrintOptions` 以 **create PowerPoint from Excel file**，並將結果儲存為可編輯的 PPTX 投影片。透過調整選項，您可以微調解析度、選取特定工作表，或串流大型檔案，使此方法在各種自動化情境下皆具彈性。

**下一步**

* 進一步探索 **java convert .xlsx to .pptx**，透過 Aspose.Slides 加入自訂投影片版面配置。  
* 使用簡易目錄監視器自動批次處理多個活頁簿。  
* 將此轉換與資料驅動的圖表產生結合，製作動態簡報。

歡迎自行嘗試各項設定並分享成果。祝程式開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在所示技術之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [Convert Excel to PowerPoint with Aspose.Cells in Java](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}