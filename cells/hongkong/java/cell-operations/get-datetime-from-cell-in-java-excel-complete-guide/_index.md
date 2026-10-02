---
category: general
date: 2026-06-08
description: 使用 Aspose.Cells Java 取得儲存格的日期時間，並學習如何在幾個步驟內寫入值到 Excel 儲存格。
draft: false
keywords:
- get datetime from cell
- write value to excel cell
- Aspose.Cells Java date parsing
- Japanese era calendar Excel
- Excel formula recalculation Java
language: zh-hant
og_description: 使用 Aspose.Cells Java 從儲存格取得日期時間。本教學亦示範如何高效寫入值至 Excel 儲存格。
og_title: 在 Java Excel 中從儲存格取得日期時間 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  headline: Get datetime from cell in Java Excel – Complete Guide
  type: TechArticle
- description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  name: Get datetime from cell in Java Excel – Complete Guide
  steps:
  - name: What if the cell already contains a true Excel date?
    text: 'If `cell.getType()` returns `CellValueType.IS_DATE_TIME`, you can skip
      the recalculation step and read the value directly:'
  - name: How to process a whole column of era strings?
    text: 'Loop through the used range and apply the same settings once:'
  - name: Can I disable the Japanese era handling later?
    text: 'Yes—just flip the flag back:'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
title: 在 Java Excel 中從儲存格取得日期時間 – 完整指南
url: /zh-hant/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 Java Excel 中的儲存格取得日期時間 – 完整指南

是否曾需要 **從儲存格取得日期時間**，但值卻是日文元號字串？你並非唯一遇到此問題的人。在許多舊版試算表中，日期會以「Reiwa 3/04/01」的形式儲存，而要把它轉換成正確的 `java.time.LocalDateTime` 常常感覺像在破解密碼。  

幸好 Aspose.Cells for Java 能為你處理這個轉換，同時我們也會示範如何 **寫入值到 Excel 儲存格**，讓你在不破壞工作表邏輯的前提下完成資料的來回傳遞。

在本教學中，你將學會：

* 如何建立工作簿並鎖定特定工作表。  
* 啟用日文元號曆的精確步驟，以便解析。  
* 為什麼在讀取日期前必須重新計算公式。  
* 如何將新值寫回儲存格而不失去格式。  

不需要外部工具，也不需要魔法——只要純粹的 Java 程式碼，今天就能放入任何 Maven 專案使用。

---

## 前置條件

* **Java 8+**（範例使用現代的 `java.time` API）。  
* **Aspose.Cells for Java** ≥ 23.9.0 – 透過 Maven 或 Gradle 加入相依性。  
* 基本的 Excel 概念（工作表、儲存格、公式）熟悉度。  

如果缺少此函式庫，請從官方 Aspose 倉庫取得：

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## 第一步：建立新工作簿並存取第一個工作表

首先，我們需要一個全新的 `Workbook` 物件。把它想像成在記憶體中開啟一個新的 Excel 檔案。

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

*為什麼這很重要：*  
以程式方式建立工作簿可讓你在任何資料寫入檔案系統之前，完整掌控設定。第一個工作表（`index 0`）將用來示範讀寫操作。

---

## 第二步：將日文元號日期字串寫入儲存格 A1

現在我們要 **寫入值到 Excel 儲存格** A1。這模擬了使用者手動輸入「Reiwa 3/04/01」的真實情境。

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

*小技巧：* `putValue` 功能多元——它接受字串、數字、日期，甚至公式。當你傳入純文字時，Aspose 會原樣儲存，非常適合本示範。

---

## 第三步：啟用日文元號曆以供日期解析

預設情況下 Aspose.Cells 使用公曆。為了讓「Reiwa」有意義，我們需要切換設定。

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

*為什麼要啟用？*  
日文元號曆會把元號名稱（Reiwa、Heisei、Showa）映射到對應的公曆日期。若未開啟此旗標，函式庫會把字串視為純文字，永遠不會得到正確的 `DateTime` 物件。

---

## 第四步：重新計算公式，使元號字串轉換為公曆日期

Aspose 不會自動將字串解析為日期。相反地，它會在一次計算過程後，將儲存格視為公式結果。

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

當 `calculateFormula()` 執行時，引擎會辨識元號模式、套用日文曆，並在內部儲存轉換後的公曆日期。之後呼叫 `getDateTime()` 會回傳 `java.util.Date`（或自行轉換為 `java.time`）。

**預期輸出**

```
2021-04-01T00:00:00.000+00:00
```

---

## 第五步：將新值寫回同一儲存格（或其他儲存格）

假設你想把原本的字串覆寫為符合 ISO‑8601 格式的日期。以下示範如何安全地 **寫入值到 Excel 儲存格**，同時保留儲存格樣式。

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

*發生了什麼事？*  
`putValue` 會偵測到 `LocalDateTime` 類型，並將其轉換為 Excel 的序號表示法。設定數字格式可確保在 Excel 中開啟時，儲存格會如你所預期顯示日期。

---

## 完整範例程式

將上述步驟整合起來，以下是一個可直接編譯執行的單一 Java 類別。它會建立工作簿、寫入元號字串、完成轉換，最後儲存檔案。

```java
import com.aspose.cells.*;

public class JapaneseEraDateDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first sheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ Write Japanese era date string to A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue("Reiwa 3/04/01");

        // 3️⃣ Enable Japanese era calendar
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEraCalendar(true);

        // 4️⃣ Recalculate so the string becomes a Gregorian date
        workbook.calculateFormula();
        System.out.println("Converted date: " + cell.getDateTime());

        // 5️⃣ Overwrite with a clean LocalDateTime (optional)
        java.time.LocalDateTime now = java.time.LocalDateTime.now();
        cell.putValue(now);
        Style style = cell.getStyle();
        style.setNumber(14); // m/d/yyyy
        cell.setStyle(style);

        // 6️⃣ Save the workbook
        workbook.save("output.xlsx");
        System.out.println("Workbook saved as output.xlsx");
    }
}
```

使用 `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` 執行，然後開啟 **output.xlsx**。你會看到 A1 儲存格顯示當前日期，且主控台會列印轉換後的「2021‑04‑01」值。

---

## 處理邊緣情況與常見問題

### 若儲存格已經是正規的 Excel 日期，該怎麼辦？

如果 `cell.getType()` 回傳 `CellValueType.IS_DATE_TIME`，你可以直接讀取值，省略重新計算步驟：

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

### 如何一次處理整欄的元號字串？

遍歷已使用的範圍，並在一次設定後套用相同的處理流程：

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

### 之後想關閉日文元號處理，該怎麼做？

可以把旗標關回：

```java
settings.setUseJapaneseEraCalendar(false);
```

記得在變更設定後再次重新計算。

---

## 專業技巧與注意事項

* **效能：** 開啟日文元號曆會帶來微小的額外開銷。如果只需要處理少數儲存格，建議在處理完畢後立即關閉此設定。  
* **語系相容性：** 元號字串必須完全符合「EraName yy/MM/dd」的格式。拼寫錯誤（例如「Rewa」）會導致字串被當作純文字處理。  
* **儲存格式：** `Workbook.save("output.xlsx")` 會產生 XLSX 檔案。若需舊版二進位格式，使用 `"output.xls"`，但需注意某些功能（如元號解析）可能受限。

---

## 結論

現在你已掌握在來源使用日文元號表示法時，如何 **從儲存格取得日期時間**，以及如何以正確格式 **寫入值到 Excel 儲存格**。只要切換 `setUseJapaneseEraCalendar(true)` 並強制公式重新計算，Aspose.Cells 就能在舊有元號字串與現代公曆日期之間架起橋樑——全部只需幾行 Java 程式碼。

接下來可以嘗試將此模式延伸至其他文化曆法（如泰曆、伊斯蘭曆），或使用相同方法批次處理大型工作簿。核心原則——啟用正確的曆法、重新計算、再讀寫——在各種情境下皆適用。

有無法破解的日期格式嗎？在下方留言，我們一起來排除問題。祝程式開發愉快！  

![取得儲存格日期時間範例](https://example.com/images/get-datetime-from-cell.png "取得儲存格日期時間範例")


## 接下來該學什麼？

以下教學與本指南的技巧緊密相關，能進一步深化你對 API 功能的掌握，並提供在專案中實作的不同方式。

- [使用 Aspose.Cells Java 在 Excel 中設定 1904 日期系統，以提升儲存格操作效能](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [在 Aspose.Cells Java 中實作遞迴儲存格計算，以加強 Excel 自動化](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [使用 Aspose.Cells for Java 將 Excel 儲存格名稱轉換為索引的逐步指南](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}