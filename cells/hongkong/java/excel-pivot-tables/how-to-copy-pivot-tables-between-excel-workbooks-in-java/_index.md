---
category: general
date: 2026-10-01
description: 學習如何使用 Java 在 Excel 活頁簿之間複製樞紐分析表。本分步指南亦說明如何在活頁簿之間複製範圍以及安全地複製 Excel 範圍。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- copy range between workbooks
- how to copy excel
- duplicate excel range
- copy range to workbook
language: zh-hant
lastmod: 2026-10-01
og_description: 使用 Java 在 Excel 活頁簿之間複製樞紐分析表。請參考本指南，將範圍複製至活頁簿、複製 Excel 範圍，並保留樞紐資料。
og_image_alt: Screenshot of Java code that copies a pivot table from one Excel workbook
  to another
og_title: 如何在 Java 中於 Excel 活頁簿之間複製樞紐分析表 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  headline: How to copy pivot tables between Excel workbooks in Java
  type: TechArticle
- description: Learn how to copy pivot tables between Excel workbooks using Java.
    This step‑by‑step guide also shows how to copy range between workbooks and duplicate
    Excel ranges safely.
  name: How to copy pivot tables between Excel workbooks in Java
  steps:
  - name: Expected output
    text: '* Console: `Pivot table copied successfully.` * `destination.xlsx` opens
      in Excel with a pivot table identical to the one in `source.xlsx`. Refreshing
      the pivot shows the same data source, proving that **how to copy pivot** works
      as intended.'
  - name: Copying multiple worksheets
    text: If your project requires copying several sheets, loop through the workbook’s
      worksheets and repeat steps 2‑4 for each sheet. The pivot in each sheet will
      be preserved independently.
  - name: Preserving external data connections
    text: Pivot tables that rely on external data sources keep the connection string
      after copying. However, the destination file must have access to the same data
      source. Verify the connection by opening the pivot and checking the **Data**
      tab.
  - name: Dealing with merged cells
    text: If the source range contains merged cells, Aspose.Cells copies the merge
      layout automatically. Still, validate the result if the destination workbook
      uses a different default column width.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Pivot table
- Data manipulation
title: 如何在 Java 中於 Excel 活頁簿之間複製樞紐分析表
url: /zh-hant/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中於 Excel 活頁簿之間複製樞紐分析表

如果你需要 **how to copy pivot** 從一個 Excel 檔案複製到另一個檔案，本指南提供即時可執行的解決方案。閱讀完前兩句後，你將確切了解哪些 API 呼叫在複製資料範圍時會保留樞紐分析表的定義。

你還會學習如何 **copy range between workbooks**、**duplicate Excel range** 物件，以及安全地 **copy range to workbook** 而不遺失公式或格式。無需外部腳本——只需一個使用 Aspose.Cells for Java 的單一 Java 專案。

## 前置條件

* Java Development Kit 17 或更新版本。
* Maven 或 Gradle 以管理相依性。
* 有效的 Aspose.Cells for Java 授權（免費評估版可用於測試）。
* 兩個 Excel 檔案：`source.xlsx`（包含樞紐分析表）以及空的 `destination.xlsx`（或讓程式碼自行建立）。

## 步驟 1：設定 Maven 專案

建立包含 Aspose.Cells 的 `pom.xml`。此相依性提供範例中使用的 `Workbook`、`Worksheet` 與 `Range` 類別。

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>excel-pivot-copy</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest at time of writing -->
        </dependency>
    </dependencies>
</project>
```

> **專業提示：** 保持 Aspose.Cells 版本為最新；較新版本會提供對複雜樞紐快取結構的更佳支援。

## 步驟 2：載入包含樞紐分析表的來源活頁簿

第一段程式碼示範 **how to copy excel** 資料的方式，透過載入來源檔案。`Workbook` 建構子會將整個檔案讀入記憶體，保留所有工作表物件，包括樞紐分析表。

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook containing the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Access the first worksheet (index 0) where the pivot resides
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

*為何這很重要：* Aspose.Cells 將樞紐分析表儲存為工作表內部模型的一部份。載入活頁簿可確保樞紐快取在之後的複製中可用。

## 步驟 3：定義包含樞紐分析表的範圍

樞紐分析表可能跨越多列多欄。大多情況下，你可以複製工作表的整個已使用範圍。`createRange` 方法會建立一個 `Range` 物件，由複製操作處理。

```java
        // Define the range to copy – includes the pivot table and its source data
        // Adjust the address if your pivot occupies a different block
        Range srcRange = srcWs.getCells().createRange("A1:H20");
```

如果樞紐分析表超出 `H20`，只需變更地址字串。此步驟是 **duplicate excel range** 處理的核心；範圍物件會包含公式、樣式與隱藏列的資訊。

## 步驟 4：建立將接收複製範圍的新活頁簿

你可以從空白活頁簿開始，或載入現有的目的檔案。此處我們建立全新的活頁簿，這是 **copy range to workbook** 最乾淨的方式。

```java
        // Create a new workbook for the destination
        Workbook destWb = new Workbook(); // starts with one default sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

> **注意：** 若需將樞紐分析表複製至特定工作表名稱，請在貼上前使用 `destWs.setName("Report")` 重新命名 `destWs`。

## 步驟 5：複製範圍 – Aspose.Cells 會自動保留樞紐分析表

`copy` 方法會傳輸來源範圍內的所有內容，包括樞紐分析表的定義、快取與格式。無需額外程式碼即可保持樞紐分析表的功能。

```java
        // Copy the range to the destination worksheet; pivot tables are preserved automatically
        srcRange.copy(destWs.getCells().createRange("A1"));
```

*為何它能運作：* Aspose.Cells 將樞紐分析表視為隱藏儲存格與附屬於範圍的中繼資料集合。呼叫 `copy` 時，函式庫會在目標活頁簿中複製該中繼資料。

## 步驟 6：儲存目的活頁簿

最後，將結果寫入磁碟。儲存的檔案會包含與原始檔案相同的樞紐分析表，你可以像原本一樣重新整理或修改它。

```java
        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");

        System.out.println("Pivot table copied successfully.");
    }
}
```

執行程式會印出確認訊息，並產生具有完整功能樞紐分析表的 `destination.xlsx`。

## 完整、可執行的範例

將所有步驟結合起來，完整的 Java 類別如下所示：

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load source workbook with pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // 2️⃣ Define the range that contains the pivot and its source data
        Range srcRange = srcWs.getCells().createRange("A1:H20");

        // 3️⃣ Prepare destination workbook (blank by default)
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // 4️⃣ Copy range – pivot table is kept intact
        srcRange.copy(destWs.getCells().createRange("A1"));

        // 5️⃣ Save the new file
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

### 預期輸出

* 主控台：`Pivot table copied successfully.`
* `destination.xlsx` 在 Excel 中開啟時，會顯示與 `source.xlsx` 中相同的樞紐分析表。重新整理樞紐分析表會顯示相同的資料來源，證明 **how to copy pivot** 如預期運作。

## 處理常見變化

### 複製多個工作表

如果你的專案需要複製多個工作表，請遍歷活頁簿的工作表，並對每個工作表重複步驟 2‑4。每個工作表中的樞紐分析表都會獨立保留。

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet src = srcWb.getWorksheets().get(i);
    Worksheet dest = destWb.getWorksheets().add();
    src.getCells().copy(dest.getCells());
}
```

### 保留外部資料連線

依賴外部資料來源的樞紐分析表在複製後會保留連線字串。然而，目的檔案必須能存取相同的資料來源。請開啟樞紐分析表並檢查 **Data** 索引標籤以驗證連線。

### 處理合併儲存格

如果來源範圍包含合併儲存格，Aspose.Cells 會自動複製合併佈局。但若目的活頁簿使用不同的預設欄寬，仍需驗證結果。

## 可靠複製的最佳實踐

| 做法 | 原因 |
|----------|--------|
| 使用精確的已使用範圍 (`srcWs.getCells().getMaxDisplayRange()`) 而非硬編碼地址 | 確保整個樞紐分析表及其來源資料皆被包含。 |
| 在執行大量操作前套用授權 | 避免評估水印並提升效能。 |
| 若來源資料變更，於複製後重新整理樞紐分析表 (`pivotTable.refresh()`) | 確保目的檔案反映最新值。 |
| 撰寫單元測試，開啟目的活頁簿並斷言 `pivotTable.getPivotFields().size()` 與來源相符 | 在未來程式變更時偵測欄位意外遺失。 |

## 結論

現在你已了解如何在 Java 中於 Excel 活頁簿之間 **how to copy pivot** 樞紐分析表，同時也掌握 **copy range between workbooks**、**duplicate excel range** 以及 **copy range to workbook**，且能保留所有格式與公式。此範例使用 Aspose.Cells，將 OpenXML SDK 所需的低階 XML 處理抽象化。

接下來，可探索相關主題，如 **updating pivot cache programmatically**、**exporting pivot data to CSV**，或 **creating pivot tables from scratch**。這些皆建立在此處示範的相同概念之上。

祝程式開發順利，歡迎嘗試更大的範圍、多個樞紐分析表或自訂樣式——相同的模式適用於所有情境。

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通其他 API 功能，並在專案中探索替代實作方式。

- [如何使用 Aspose.Cells for Java 在 Excel 中建立樞紐分析表：完整指南](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells Java 複製 Excel 中的多欄位：完整指南](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 在 Excel 工作表之間複製圖片：完整指南](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}