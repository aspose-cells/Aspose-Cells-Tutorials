---
category: general
date: 2026-07-23
description: 在 Java 中建立新工作簿，並在數分鐘內學會如何複製樞紐分析表、複製 Excel 範圍，以及使用 Aspose.Cells 匯出樞紐分析表。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook
- copy pivot table
- how to copy pivot
- copy excel range
- export pivot table
language: zh-hant
lastmod: 2026-07-23
og_description: 在 Java 中建立新工作簿，即時複製樞紐分析表、複製 Excel 範圍，然後使用 Aspose.Cells 匯出樞紐分析表。跟隨此完整教學。
og_image_alt: Screenshot of Java code copying a pivot table from one workbook to another
og_title: 在 Java 中建立新工作簿 – 逐步複製樞紐分析表
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Create new workbook in Java and learn how to copy pivot table, copy
    excel range, and export pivot table with Aspose.Cells in minutes.
  headline: Create New Workbook in Java – Full Guide to Copy Pivot Table
  type: TechArticle
- questions:
  - answer: You’ll need to copy each relevant range separately, then recreate the
      pivot on the destination sheet using `PivotTable` APIs.
    question: What if the source pivot spans more than one worksheet?
  - answer: Set `sourceRange.setCopyDataOnly(false)` before the copy. This tells Aspose
      to keep the cache but not the underlying source data.
    question: Can I copy only the pivot layout without the data?
  - answer: CSV doesn’t support pivots, but you can export the pivot’s *result* by
      calling `pivotTable.calculate()` and then saving the sheet as CSV.
    question: Is there a way to copy the pivot to a CSV file?
  - answer: Formatting lives in the style collection. After copying, you can call
      `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())`
      to transfer styles.
    question: Why does the copied pivot lose its formatting?
  type: FAQPage
tags:
- Java
- Aspose.Cells
- Excel Automation
title: 在 Java 中建立新工作簿 – 完整的樞紐分析表複製指南
url: /zh-hant/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中建立新工作簿 – 完整的樞紐分析表複製指南

有沒有想過如何在 Java 中 **create new workbook** 同時保留複雜的樞紐分析表？你並不是唯一為此抓頭的人。在許多報表應用程式中，你需要將樞紐分析表從來源檔案移到全新的工作簿，可能是要交給客戶或進一步計算。好消息是，只要幾行程式碼就能完成——不需要手動複製貼上。

在本教學中，我們將逐步說明整個流程：載入來源檔案、定義包含樞紐分析表的範圍、**copying the Excel range**、建立 **new workbook**，最後 **exporting the pivot table** 到新檔案。完成後，你將擁有一個獨立且可執行的 Java 程式，直接回答「**how to copy pivot**」的問題，免除任何猜測。

## 前置條件

- Java 17 或更新版本（此程式碼適用於任何近期的 JDK）
- Aspose.Cells for Java 函式庫（免費試用或授權版）
- 一個包含樞紐分析表於 `A1:G20` 範圍的範例 `source.xlsx`
- 一個 IDE 或建置工具（Maven/Gradle）以管理 Aspose.Cells JAR

都有了嗎？太好了——讓我們開始吧。

## 步驟 1：設定專案並匯入 Aspose.Cells

首先，你需要將 Aspose.Cells 加入專案。如果使用 Maven，請將以下相依性加入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.8</version> <!-- check for the latest version -->
</dependency>
```

如果你偏好 Gradle，等效的寫法如下：

```groovy
implementation 'com.aspose:aspose-cells:24.8'
```

將函式庫加入 classpath 後，匯入你需要的類別：

```java
import com.aspose.cells.*;
import java.io.IOException;
```

> **專業提示：** Aspose.Cells 為商業函式庫，但提供功能完整的 30 天評估版，會在輸出上加上浮水印——非常適合試用。

## 步驟 2：載入來源工作簿

現在我們將 **create new workbook** 物件，但首先需要載入包含樞紐分析表的來源。此步驟是任何 **copy excel range** 操作的基礎，因為範圍物件精確知道要傳輸哪些儲存格（包括樞紐快取）。

```java
// Load the source workbook that contains the pivot table
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Grab the first worksheet (index 0) – adjust if your pivot lives elsewhere
Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

為什麼不直接讀取範圍？因為樞紐分析表的中繼資料存放在工作表的樞紐快取中，Aspose.Cells 在複製範圍時會自動一起打包。

## 步驟 3：定義包含樞紐分析表的範圍

在許多實務檔案中，樞紐分析表佔據一個矩形區塊。此範例假設它位於 `A1:G20`。當然，你可以依實際版面調整地址。

```java
// Define the exact area that includes the pivot table
Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

如果不確定確切地址，可使用 `sourceSheet.getCells().getMaxDataRow()` 與 `getMaxDataColumn()` 動態計算範圍。當樞紐大小隨時間變化時，這個技巧相當實用。

## 步驟 4：**Create New Workbook** 與目標工作表

現在就是實際 **create new workbook**，用來接收複製內容的時刻。把它想像成你將貼上樞紐的空白畫布。

```java
// Create an empty workbook – this is our destination
Workbook destinationWorkbook = new Workbook();

// By default a new workbook comes with one worksheet
Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);
```

為什麼要從空白工作簿開始？這可確保沒有隱藏樣式或先前的樞紐干擾複製，讓你得到乾淨的結果，隨時可進行 **export pivot table**。

## 步驟 5：複製樞紐分析表（及其底層範圍）

現在進入教學核心：**copy pivot table**。Aspose.Cells 將範圍複製視為深層複製，意味著樞紐快取會隨儲存格一起搬移。這就是為什麼只需一行程式碼即可完成重任。

```java
// Copy the defined range (including the pivot) to the destination sheet at A1
sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

如果你曾想過 **how to copy pivot** 而不失去功能，這就是答案。目標工作表現在已包含完整可運作的樞紐，你可以重新整理、修改，或直接匯出。

### 邊緣情況：保留重新整理設定

有時來源樞紐設定為開啟時自動重新整理。若要保留此行為，可明確複製樞紐的選項：

```java
// Optional: retain the original pivot's refresh settings
PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
PivotTable destPivot = destinationSheet.getPivotTables().get(0);
destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
```

此程式碼片段可確保複製的樞紐行為與原始完全相同。

## 步驟 6：儲存目標工作簿 – **Export Pivot Table**

最後，我們透過將新工作簿儲存至磁碟來 **export pivot table**。你可以選擇 Aspose 支援的任何格式：XLSX、XLS、CSV、PDF 等。本教學將以 XLSX 為例。

```java
// Save the workbook that now contains the copied pivot
destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);
```

若需透過 Web 服務傳送檔案，可將其寫入 `ByteArrayOutputStream` 而非檔案路徑——Aspose 讓此操作變得簡單。

## 完整可執行範例

將上述步驟整合起來，以下是一個完整、可直接執行的程式。歡迎在 IDE 中複製、貼上並執行。

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.getWorksheets().get(0);

        // 3️⃣ Copy the range (pivot table included) to the destination sheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Optional: Preserve refresh settings if needed
        if (!sourceSheet.getPivotTables().isEmpty()) {
            PivotTable srcPivot = sourceSheet.getPivotTables().get(0);
            PivotTable destPivot = destinationSheet.getPivotTables().get(0);
            destPivot.setRefreshOnFileOpen(srcPivot.isRefreshOnFileOpen());
        }

        // 4️⃣ Save the result – this effectively **export pivot table**
        destinationWorkbook.save("YOUR_DIRECTORY/copied_with_pivot.xlsx", SaveFormat.XLSX);

        System.out.println("Pivot table copied successfully!");
    }
}
```

### 預期輸出

執行程式時，主控台會輸出：

```
Pivot table copied successfully!
```

且檔案 `copied_with_pivot.xlsx` 會出現在 `YOUR_DIRECTORY`。在 Excel 中開啟，即可看到完整的樞紐分析表，隨時可重新整理或編輯。

## 常見問題與疑難排解

- **如果來源樞紐跨越多個工作表呢？**  
  需要分別複製每個相關範圍，然後在目標工作表上使用 `PivotTable` API 重新建立樞紐。

- **我可以只複製樞紐的版面配置而不帶資料嗎？**  
  在複製前設定 `sourceRange.setCopyDataOnly(false)`。這會指示 Aspose 保留快取但不複製底層來源資料。

- **有沒有辦法將樞紐複製成 CSV 檔案？**  
  CSV 不支援樞紐，但可透過呼叫 `pivotTable.calculate()` 後將工作表另存為 CSV，匯出樞紐的 *結果*。

- **為什麼複製的樞紐會失去格式？**  
  格式屬於樣式集合。複製後，可呼叫 `destinationSheet.getCells().applyStyle(sourceSheet.getCells().getStyle())` 以轉移樣式。

## 結論

我們剛剛示範了如何在 Java 中 **create new workbook**、**copy pivot table**，以及 **export pivot table**——全部使用乾淨且可重現的程式碼範例。透過明確定義 **copy excel range**、利用 Aspose.Cells 的深層複製語意，並保留可選設定，你即可自動化幾乎所有的樞紐遷移工作。

準備好進一步了嗎？可以嘗試將輸出格式改為 PDF，或是遍歷多個來源檔案批次處理數十個樞紐。使用相同的模式，只需調整檔案路徑與範圍地址即可。

如果遇到問題，歡迎在下方留言或查閱 Aspose.Cells 文件以取得進階的樞紐操作說明。祝程式開發愉快，並享受自動化那些繁瑣複製貼上工作所節省的時間！

## 接下來可以學習什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在本篇示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在專案中探索其他實作方式。

- [如何使用 Aspose.Cells for Java 在 Excel 中建立樞紐分析表：完整指南](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 更新 Excel 樞紐分析表來源：完整指南](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [如何使用 Aspose.Cells Java 建立並匯出 Excel 為 HTML：工作簿操作指南](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}