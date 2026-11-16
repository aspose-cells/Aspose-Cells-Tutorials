---
category: general
date: 2026-11-16
description: 如何在 Java 中複製 Excel 工作簿之間的儲存格 – 載入工作簿、在工作簿之間複製範圍（包括樞紐分析表），並儲存工作簿檔案。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: zh-hant
lastmod: 2026-11-16
og_description: 如何在 Java 中於 Excel 工作簿之間複製儲存格。學習載入 Excel 工作簿、在工作簿之間複製範圍（包括樞紐分析表），以及儲存工作簿檔案。
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: 如何在 Java 中於 Excel 工作簿之間複製儲存格 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: 在 Java 中如何在 Excel 工作簿之間複製儲存格
url: /zh-hant/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中於 Excel 活頁簿之間複製儲存格

如果您需要使用 Java 從一個 Excel 活頁簿複製儲存格到另一個活頁簿，本指南將向您展示一種可靠的方法。您將學習如何 **load Excel workbook Java**、複製可能包含樞紐分析表的範圍，最後 **save workbook file** 已複製的資料。

本教學涵蓋：

* 載入來源活頁簿並選取工作表。  
* 定義要搬移的精確範圍（包含樞紐分析表）。  
* 建立目標活頁簿並複製該範圍。  
* 儲存目標檔案。  

範例使用 Aspose.Cells for Java 函式庫，無需 Microsoft Office 即可操作 Excel 檔案。程式碼可在 Java 8+ 以及任何現代 IDE（IntelliJ IDEA、Eclipse、VS Code 等）上執行。

---

## 前置條件

在開始之前，請確保您已具備：

| 需求 | 原因 |
|------|------|
| Java Development Kit (JDK) 8 or newer | 需要編譯及執行程式碼。 |
| Maven or Gradle build tool | 簡化加入 Aspose.Cells 相依性。 |
| Aspose.Cells for Java library (latest version) | 提供範例中使用的 `Workbook`、`Worksheet` 與 `Range` 類別。 |
| Two Excel files (`source.xlsx` and an empty folder for `dest.xlsx`) | 來源檔案必須包含資料，且可選擇性包含您想要複製的樞紐分析表。 |

將 Aspose.Cells 相依性加入您的 `pom.xml`（Maven）或 `build.gradle`（Gradle）。以下為 Maven 範例：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## 如何使用 Aspose.Cells 複製儲存格

以下步驟將完整說明整個流程。每一步皆包含 Java 程式碼、說明 **為什麼** 此步驟重要，以及避免常見陷阱的小技巧。

### 步驟 1：載入來源活頁簿

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**為什麼？**  
`Workbook` 代表整個 Excel 檔案。載入它後即可存取所有工作表、儲存格以及樞紐分析表等物件。使用第一個工作表是常見做法，但您也可以透過名稱選取任意工作表（`srcWb.getWorksheets().get("Sheet2")`）。

**專業提示：**  
如果來源檔案很大，建議以 *memory‑efficient* 模式載入：`new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### 步驟 2：定義包含樞紐分析表的範圍

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**為什麼？**  
`Range` 物件抽象出一個矩形儲存格區塊。透過指定 `"A1:G20"`，您告訴 Aspose.Cells 正確的儲存格範圍——包括任何內嵌的樞紐分析表——要進行複製。函式庫會自動複製底層資料、樣式與樞紐定義。

**邊緣情況：**  
若樞紐分析表超出已定義的範圍，請擴大地址（例如 `"A1:Z100"`）。也可以使用 `srcWs.getCells().getMaxDataColumn()` 與 `getMaxDataRow()` 動態計算已使用的區域。

### 步驟 3：建立目標活頁簿

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**為什麼？**  
全新活頁簿可確保不會有不必要的格式或隱藏工作表干擾複製內容。預設活頁簿已包含一個工作表，我們將使用它作為目標。

### 步驟 4：將範圍複製到目標活頁簿

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**為什麼？**  
`copyRange` 會處理所有儲存格屬性：值、公式、格式，甚至樞紐快取。將其複製到 `"A1"`，即可將範圍放置在目標工作表的左上角，保留原始版面配置。

**常見問題：** *樞紐分析表會保持功能嗎？*  
是的。Aspose.Cells 會複製樞紐分析表的定義與快取，因此樞紐在目標活頁簿中會如同來源活頁簿般正常運作。

### 步驟 5：儲存目標活頁簿

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**為什麼？**  
呼叫 `save` 會將記憶體中的活頁簿寫入實體 `.xlsx` 檔案。您也可以透過變更副檔名或使用 `SaveOptions` 另存為其他格式（`.xls`、`.csv`、`.pdf`）。

**提示：**  
若需將檔案串流至 Web 回應，請使用 `destWb.save(OutputStream, SaveFormat.XLSX);` 取代檔案路徑。

---

## 複製活頁簿之間的範圍 – 完整原始碼

以下為可直接執行的完整 Java 類別。請將 `YOUR_DIRECTORY` 替換為您機器上的實際資料夾路徑。

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**預期結果：**  
`dest.xlsx` 會完整複製 `source.xlsx` 中 `A1:G20` 的範圍。若來源範圍內包含樞紐分析表，目標檔案會顯示相同的樞紐，且資料來源正確連結至已複製的儲存格。

您可以在 Excel、LibreOffice 或任何支援 `.xlsx` 的檢視器中開啟 `dest.xlsx`，驗證值、格式與樞紐功能皆已保留。

---

## 複製樞紐分析表活頁簿 – 您需要知道的事項

* **Pivot cache is copied automatically.** 函式庫會轉移底層快取，樞紐分析表不需要手動重新整理。  
* **External data sources are not transferred.** 若樞紐分析表從外部資料庫取得資料，必須確保目標活頁簿能存取相同來源，或在本機重新建立快取。  
* **Large pivot tables may increase memory usage.** 對於非常大的活頁簿，建議增加 JVM 堆積大小（`-Xmx2g`）以避免 `OutOfMemoryError`。

---

## 以不同格式儲存活頁簿檔案

Aspose.Cells 讓您在不修改程式碼的情況下，將結果儲存為多種格式：

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

選擇符合下游流程的格式即可。相同的 `copyRange` 邏輯在任何最終格式下皆可正常運作。

---

## 載入 Excel 活頁簿 Java – 其他技巧

* **Loading encrypted files:** 使用帶密碼的 `LoadOptions`：  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Reading only specific sheets:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

這些選項可加速 **load excel workbook java** 步驟，特別是面對大型檔案時。

---

## 結論

您現在已了解 **how to copy cells** 在 Java 中於 Excel 活頁簿之間的操作方式，亦掌握 **copy range between workbooks** 包含 **pivot table** 的技巧，並能 **save workbook file** 為所需的格式。依循上述步驟，您可以將 Excel 資料操作整合至任何 Java 應用程式——無論是建構報表引擎、ETL 流程，或是簡易的檔案轉換工具。

**下一步** 您可以探索：

* 使用 **copy range between workbooks** 合併多份報表至

## 您接下來應該學習什麼？

以下教學與本指南所示技術緊密相關，提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [Save New Workbook in Java – Copy Range Between Workbooks Tutorial](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [How to copy pivot tables between Excel workbooks in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}