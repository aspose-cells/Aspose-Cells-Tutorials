---
category: general
date: 2026-10-07
description: 了解如何在 Java 中使用 Aspose.Cells 從儲存格讀取 Excel 日期，並且高效地將值寫回 Excel。
draft: false
keywords:
- how to read excel
- write value to excel
- get datetime from excel
- extract datetime from cell
- Aspose.Cells Java date parsing
lastmod: 2026-10-07
og_description: 如何在 Java 中使用 Aspose.Cells 從儲存格讀取 Excel 日期。本指南亦示範如何高效地將值寫入 Excel 儲存格。
og_image_alt: 'Developer guide: reading and writing Excel dates with Aspose.Cells
  Java'
og_title: 如何在 Java 中使用 Aspose.Cells 從儲存格讀取 Excel 日期
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to read Excel dates from cells in Java using Aspose.Cells
    and write values back.
  headline: How to read Excel dates from cells in Java using Aspose.Cells
  type: TechArticle
- description: Learn how to read Excel dates from cells in Java using Aspose.Cells
    and write values back.
  name: How to read Excel dates from cells in Java using Aspose.Cells
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
- date parsing
- Excel automation
title: 如何在 Java 中使用 Aspose.Cells 從儲存格讀取 Excel 日期
url: /zh-hant/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose.Cells 讀取 Excel 儲存格的日期

如果您需要 **how to read Excel** 以日本元號字串儲存的值，您來對地方了。許多舊版活頁簿包含類似「Reiwa 3/04/01」的日期，將其正確轉換為 `java.time.LocalDateTime` 可能感覺像在破譯密碼。Aspose.Cells for Java 能理解這些元號表示，且也允許您 **write value to excel** 儲存格而不失去格式。在本指南中，您將獲得完整的逐步說明，今天即可貼入任何 Maven 專案使用。

## 快速回答
- **Aspose.Cells 能解析日本元號日期嗎？** 是 – 啟用日本元號日曆旗標並重新計算公式。  
- **我需要手動重新計算公式嗎？** 絕對需要；如果不進行計算，元號字串會保持為文字。  
- **Aspose.Cells 支援多少種 Excel 格式？** 超過 50 種輸入與輸出格式，包括 XLSX、XLS、CSV 與 ODS。  
- **此函式庫相容於 Java 8+ 嗎？** 是的，它可在 Java 8 及更新的執行環境上運作。  
- **我可以將公曆日期寫回同一個儲存格嗎？** 使用 `putValue` 搭配 `LocalDateTime`，並設定數字格式為 ISO‑8601 顯示。

## 什麼是 **如何讀取 Excel** 日期從儲存格？
**如何讀取 Excel** 指的是將儲存格內容——尤其是日期——抽取為原生程式類型，例如 `java.time.LocalDateTime`。Aspose.Cells 抽象化了低階解析，讓您專注於業務邏輯，而不必處理 Excel 序號的怪異行為。此方式簡化了程式碼維護，降低了在處理舊版試算表時的轉換錯誤機率。

## 為何使用 Aspose.Cells 進行日本元號轉換？
Aspose.Cells 支援 **50+** 檔案格式，且可在不將整個檔案載入記憶體的情況下處理 **數百頁** 的活頁簿。啟用日本元號日曆僅會產生極小的效能開銷，適合大量處理舊版試算表。函式庫亦在轉換過程中保留儲存格樣式與公式，確保輸出與原始活頁簿外觀一致。

## 前置條件

* **Java 8+** – 範例使用現代的 `java.time` API。  
* **Aspose.Cells for Java ≥ 23.9.0** – 從官方儲存庫加入 Maven/Gradle 依賴。  
* 基本的 Excel 概念（工作表、儲存格、公式）認知。  

如果您尚未取得函式庫，請從官方 Aspose 儲存庫下載：

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

## 如何建立活頁簿並存取第一個工作表？
`Workbook` 代表載入記憶體中的 Excel 檔案。`Worksheet` 代表該活頁簿中的單一工作表。  
建立一個 `Workbook` 物件，然後取得第一個 `Worksheet`。這讓您在任何資料寫入磁碟前就能完整控制。先初始化活頁簿即可在讀寫儲存格前設定（例如日曆處理）等設定。

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

## 如何將日本元號日期字串寫入儲存格 A1？
`Cell` 是保存單一 Excel 儲存格值的物件。  
將舊版元號字串「Reiwa 3/04/01」寫入儲存格 A1。這模擬使用者輸入的值，稍後您會將其轉換。先寫入字串可示範從文字到正確日期物件的完整工作流程。

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

## 如何啟用日本元號日曆以進行日期解析？
`WorkbookSettings.setUseJapaneseEraCalendar(boolean)` 會切換元號轉換功能。  
開啟此旗標讓 Aspose.Cells 知道如何將元號名稱轉換為公曆年份。啟用後，計算引擎會把「Reiwa」等字串解讀為對應的公曆年份，這對正確的日期解析至關重要。

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

## 如何重新計算公式，使元號字串轉換為公曆日期？
`Workbook.calculateFormula()` 會強制計算引擎評估活頁簿中的所有公式。  
執行一次計算引擎後，它會識別元號模式、完成轉換，並在內部儲存公曆結果。之後，`getDateTime()` 會回傳 `java.util.Date`，您可再轉換為 `java.time`。此步驟必要，因為元號字串在公式未計算前會被視為純文字。

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

**預期輸出**

```
2021-04-01T00:00:00.000+00:00
```

## 如何將新值寫回同一個儲存格（或其他儲存格）？
`Cell.putValue(Object)` 會將值寫入儲存格，並自動處理型別轉換。  
使用 `putValue` 用乾淨的 ISO‑8601 日期覆寫原始元號字串，同時保留儲存格樣式。`putValue` 會偵測 `LocalDateTime` 型別並轉換為 Excel 的序號表示。設定數字格式可確保在 Excel 中開啟時顯示您期望的日期格式。

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

## 完整範例

以下程式碼將上述所有步驟合併成一個可編譯執行的 Java 類別。它會建立活頁簿、寫入元號字串、執行轉換，最後儲存檔案。

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

使用 `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` 執行類別，並開啟 **output.xlsx**。儲存格 A1 會顯示已轉換的公曆日期，主控台會列印出值「2021‑04‑01」。

## 如果儲存格已經包含真正的 Excel 日期該怎麼辦？
若儲存格已存儲原生 Excel 日期，您可以直接讀取而不需額外處理。這樣可節省時間，因為計算引擎不必重新解讀值。只要檢查儲存格類型並取得日期即可。

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

## 如何處理整欄元號字串？
當大量儲存格包含元號字串時，遍歷已使用的範圍並對每個儲存格套用相同的轉換邏輯。此批次方式較逐一處理效能更佳。記得在迴圈前啟用日本元號日曆，處理完畢後一次重新計算。

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

## 後續可以關閉日本元號處理嗎？
在完成相關儲存格的處理後，您可以關閉元號轉換旗標。關閉後會恢復預設的解析行為，適用於同一本活頁簿中稍後需要處理標準日期的情況。

```java
settings.setUseJapaneseEraCalendar(false);
```

若在寫入資料後變更設定，請再次重新計算。

## 專業技巧與常見陷阱

* **效能：** 啟用日本元號日曆只會產生極小的額外開銷。僅對需要轉換的儲存格開啟，完成後再關閉。  
* **語系意識：** 元號字串必須完全符合「EraName yy/MM/dd」模式。拼寫錯誤（例如「Rewa」）會使儲存格保持為文字。  
* **儲存格式：** `Workbook.save("output.xlsx")` 會寫入 XLSX 檔案。若使用 `"output.xls"` 會產生舊版二進位格式，但某些進階功能（如元號解析）可能受限。

## 常見問與答

**問：此方法適用於其他文化曆法（泰曆、伊斯蘭曆）嗎？**  
答：可以——Aspose.Cells 提供泰國佛教曆與伊斯蘭曆的類似旗標；啟用相應設定並重新計算即可。

**問：我可以從受密碼保護的活頁簿讀取日期嗎？**  
答：使用帶有密碼參數的方式載入活頁簿，然後照常執行步驟；日曆旗標仍然有效。

**問：處理的列數有上限嗎？**  
答：Aspose.Cells 能處理數百萬列；它會以串流方式處理資料以降低記憶體使用，特別是每批次切換 `setUseJapaneseEraCalendar` 時。

**問：覆寫日期時如何保留原有儲存格樣式？**  
答：在呼叫 `putValue` 前先取得儲存格的 `Style` 物件，寫入後再重新套用該樣式。

**問：商業使用是否需要授權？**  
答：是的，正式上線必須擁有有效的 Aspose.Cells 授權；亦提供免費試用版供評估使用。

## 結論

您現在已掌握 **如何讀取 Excel** 中使用日本元號表示的日期，並了解如何 **write value to excel** 儲存格以正確格式呈現。只要啟用 `setUseJapaneseEraCalendar(true)` 並強制公式重新計算，Aspose.Cells 即可在幾行 Java 程式碼內將舊版元號字串橋接至現代公曆日期。試著將此模式延伸至其他文化曆法或大量活頁簿的批次處理——相同的啟用‑重新計算‑讀寫工作流程普遍適用。

有無法破解的奇怪日期格式嗎？在下方留言，我們一起排除問題。祝程式開發愉快！

![從儲存格取得日期時間範例](https://example.com/images/get-datetime-from-cell.png "從儲存格取得日期時間範例")
[從儲存格取得日期時間範例](https://example.com/images/get-datetime-from-cell.png "從儲存格取得日期時間範例")

## 接下來該學什麼？

以下教學與本指南主題密切相關，能進一步深化您對 API 功能的掌握，並探索在專案中實作的其他方式。

- [精通 Aspose.Cells Java 在 Excel 中設定 1904 日期系統以提升儲存格操作效能](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [在 Aspose.Cells Java 中實作遞迴儲存格計算以加強 Excel 自動化](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [使用 Aspose.Cells for Java 將 Excel 儲存格名稱轉換為索引的逐步指南](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

---

**最後更新：** 2026-10-07  
**測試版本：** Aspose.Cells 23.9.0  
**作者：** Aspose

## 相關教學

- [aspose cells performance: 使用 Java 取得 Excel 儲存格資料](/cells/java/cell-operations/aspose-cells-java-data-retrieval-excel/)
- [使用 Aspose.Cells for Java 變更 Excel 1904 日期系統](/cells/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [精通 Aspose.Cells Java 檔案處理：高效讀寫與資料處理](/cells/java/workbook-operations/java-file-handling-aspose-cells-read-write-process/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}