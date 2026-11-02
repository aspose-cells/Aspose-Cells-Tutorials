---
category: general
date: 2026-09-27
description: 如何使用 Aspose.Cells 在 Java 中將 Excel 工作表匯出至 PowerPoint ─ 步驟說明指南，同時示範如何將
  Excel 活頁簿轉換為 PowerPoint 簡報。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel sheet to powerpoint
- convert excel workbook to powerpoint presentation
language: zh-hant
lastmod: 2026-09-27
og_description: 如何使用 Aspose.Cells 在 Java 中將 Excel 工作表匯出至 PowerPoint。學習完整程式碼將 Excel
  活頁簿轉換為 PowerPoint 簡報。
og_image_alt: Java code snippet that exports an Excel sheet to a PowerPoint file using
  Aspose.Cells
og_title: 如何將 Excel 工作表匯出至 PowerPoint – Aspose.Cells Java 教學
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: How to export Excel sheet to PowerPoint with Aspose.Cells in Java –
    a step‑by‑step guide that also shows how to convert Excel workbook to PowerPoint
    presentation.
  headline: How to export Excel sheet to PowerPoint with Aspose.Cells in Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- Document conversion
title: 如何在 Java 中使用 Aspose.Cells 將 Excel 工作表匯出至 PowerPoint
url: /zh-hant/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 在 Java 中將 Excel 工作表匯出至 PowerPoint

如果您需要 **how to export Excel sheet to PowerPoint**，本教學提供完整、可直接執行的解決方案。您將會看到如何 **convert Excel workbook to PowerPoint presentation**，同時保留可編輯的文字方塊與基本格式。

本指南假設您已具備可運作的 Java 開發環境以及有效的 Aspose.Cells for Java 授權。完成本文後，您將擁有一個 Java 程式，可載入 Excel 活頁簿、匯出第一個工作表，並產生可於 Microsoft PowerPoint 開啟與編輯的 `.pptx` 檔案。

## 前置條件

| 需求 | 為什麼重要 |
|------|------------|
| Java 17 或更新版本 | Aspose.Cells 支援現代 Java 執行環境，並提供更佳效能。 |
| Aspose.Cells for Java（版本 23.10 或更新） | 此函式庫包含用於轉換的 `Workbook.save(..., SaveFormat.PPTX)` 方法。 |
| 已授權的 Aspose.Cells 版本 | 未授權時函式庫會以評估模式執行，並加上浮水印。 |
| 包含至少一個可編輯文字方塊的 Excel 檔案 | 轉換時會將文字方塊保留為 PowerPoint 中的可編輯圖形。 |
| IDE 或建置工具（例如 Maven、Gradle） | 用於編譯與執行範例程式碼。 |

## 步驟 1：將 Aspose.Cells 加入專案

如果您使用 Maven，請在 `pom.xml` 中加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

對於 Gradle，請將下列程式碼片段放入 `build.gradle`：

```gradle
implementation 'com.aspose:aspose-cells:23.10:jdk17'
```

> **小技巧：** 若只在伺服器執行時需要此函式庫，請將相依性宣告為 `provided` 範圍。

## 步驟 2：準備 Excel 活頁簿

建立一個 Excel 檔案（`WorkbookWithTextbox.xlsx`），於第一個工作表上插入可編輯的文字方塊。可於 Excel 透過 **Insert → Text Box** 插入。將檔案儲存於可供 Java 參照的目錄，例如 `src/main/resources`。

## 步驟 3：撰寫轉換程式碼

建立一個名為 `ExportEditableTextbox` 的 Java 類別。以下程式碼包含完整的匯入、錯誤處理與說明註解。

```java
package com.example.excel2ppt;

import com.aspose.cells.SaveFormat;
import com.aspose.cells.Workbook;

/**
 * Demonstrates how to export an Excel sheet to PowerPoint while preserving
 * editable text boxes. The example uses Aspose.Cells for Java.
 */
public class ExportEditableTextbox {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------------------
        // Step 1: Load the Excel workbook that contains the editable textbox.
        // --------------------------------------------------------------------
        String workbookPath = "src/main/resources/WorkbookWithTextbox.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // --------------------------------------------------------------------
        // Step 2: Export the first worksheet to a PowerPoint presentation.
        //         The SaveFormat.PPTX option writes a .pptx file that PowerPoint
        //         can open and edit. The textbox remains editable.
        // --------------------------------------------------------------------
        String outputPath = "src/main/resources/Worksheet.pptx";
        workbook.save(outputPath, SaveFormat.PPTX);

        System.out.println("Conversion successful. PowerPoint saved to: " + outputPath);
    }
}
```

### 為什麼這樣可行

* `Workbook` 代表整個 Excel 檔案。載入時會解析所有工作表、圖表與圖形。
* `workbook.save(..., SaveFormat.PPTX)` 會啟動 Aspose.Cells 內建的轉換引擎。此引擎會將 Excel 的儲存格、列與圖形映射至 PowerPoint 投影片，並保留可編輯的文字方塊為 PowerPoint 圖形。
* 此方法會為每個工作表產生一張投影片。範例中僅將第一個工作表轉換為唯一的投影片。

## 步驟 4：執行程式

使用您的建置工具編譯並執行此類別：

```bash
mvn compile exec:java -Dexec.mainClass=com.example.excel2ppt.ExportEditableTextbox
```

或是使用 Gradle：

```bash
gradle run --args='com.example.excel2ppt.ExportEditableTextbox'
```

程式執行完畢後，於 Microsoft PowerPoint 開啟 `Worksheet.pptx`。您應該會看到一張與 Excel 工作表外觀相同的投影片，且在 Excel 中建立的文字方塊會以可編輯圖形的形式出現，您可以雙擊進行修改。

## 步驟 5：處理多個工作表（可選）

若需匯出 **all** 工作表，請將單一工作表的呼叫改為迴圈：

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.save("Worksheet_" + i + ".pptx", SaveFormat.PPTX);
}
```

每次迭代會產生一個獨立的 PowerPoint 檔案（`Worksheet_0.pptx`、`Worksheet_1.pptx`…）。若希望在同一個簡報中包含多張投影片，只要一次呼叫 `save`，Aspose.Cells 會自動為每個工作表新增投影片，無需額外程式碼。

## 邊緣案例與最佳實踐

| 情況 | 推薦做法 |
|------|----------|
| 大型活頁簿（數百 MB） | 增加 JVM 記憶體上限（`-Xmx4g`），並考慮逐一匯出工作表以避免記憶體不足。 |
| 受密碼保護的活頁簿 | 使用 `LoadOptions` 在載入前提供密碼：`new LoadOptions(LoadFormat.XLSX, "pwd")`。 |
| 需要保留 Excel 公式 | PowerPoint 不支援公式，轉換時會以靜態值呈現。 |
| 需要自訂投影片版面配置 | 轉換後，可使用 Aspose.Slides for Java 操作產生的 `.pptx`，調整投影片母片或加入動畫。 |
| 在 Web 服務中執行 | 直接將輸出串流至 HTTP 回應，而非寫入檔案：`workbook.save(response.getOutputStream(), SaveFormat.PPTX);` |

## 預期輸出

執行範例後會產生名為 `Worksheet.pptx` 的檔案。於 PowerPoint 開啟時會看到：

* 一張與第一個 Excel 工作表視覺上相符的投影片。
* 文字方塊位於 Excel 中的相同位置，且可直接編輯。
* 基本的儲存格格式（字型大小、顏色、邊框）皆被保留。

主控台會印出：

```
Conversion successful. PowerPoint saved to: src/main/resources/Worksheet.pptx
```

## 結論

您現在已掌握使用 Aspose.Cells for Java **how to export Excel sheet to PowerPoint** 的方法，同時也了解在實務情境中 **convert Excel workbook to PowerPoint presentation** 的步驟。此解決方案支援單工作表匯出、多工作表活頁簿，且可結合 Aspose.Slides 進一步自訂投影片。

---

### 後續步驟

* 探索 **Aspose.Slides for Java**，於轉換後加入動畫、圖表或自訂投影片母片。  
* 嘗試轉換包含圖表的活頁簿；Aspose.Cells 會將圖表呈現為原生 PowerPoint 圖表物件。  
* 研究批次處理：讀取資料夾內的多個 Excel 檔案，為每個檔案產生對應的 PowerPoint。

歡迎自行實驗程式碼、調整檔案路徑，並將轉換功能整合至更大型的 Java 應用程式，例如報表服務或自動化文件流程。祝開發順利！

## 接下來該學什麼？

以下教學與本指南緊密相關，能進一步深化您的技巧。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能與替代實作方式。

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}