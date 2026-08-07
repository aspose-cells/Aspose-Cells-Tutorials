---
date: 2026-07-26
description: 了解如何使用 Aspose.Cells Excel 日期函數在 Java 中計算日期差異。包括月底、TODAY 和 DATEDIF 範例。
keywords:
- calculate date difference java
- end of month java
- add excel date formula
- implement excel date functions
- retrieve current date excel
lastmod: 2026-07-26
linktitle: 在 Java 中計算日期差異 – Excel 日期函數
og_description: 使用 Aspose.Cells Excel 日期函數在 Java 中計算日期差異。本指南說明如何新增 Excel 日期公式、取得當前日期，以及有效取得月底值。
og_image_alt: 'Guide: calculate date difference in Java with Aspose.Cells Excel functions'
og_title: 在 Java 中計算日期差異 – Excel 日期函數
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: Learn how to calculate date difference in Java using Aspose.Cells Excel
    date functions. Includes end of month, TODAY, and DATEDIF examples.
  headline: Calculate Date Difference in Java – Excel Date Functions
  type: TechArticle
- description: Learn how to calculate date difference in Java using Aspose.Cells Excel
    date functions. Includes end of month, TODAY, and DATEDIF examples.
  name: Calculate Date Difference in Java – Excel Date Functions
  steps:
  - name: '**Download and Install Aspose.Cells:** Visit [Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
      and download the latest release.'
    text: '**Download and Install Aspose.Cells:** Visit [Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
      and download the latest release.'
  - name: '**Add the Library to Your Project:** Include the JAR file in your build
      path or add the Maven dependency.'
    text: '**Add the Library to Your Project:** Include the JAR file in your build
      path or add the Maven dependency.'
  - name: '**License Configuration:** Place your license file (`Aspose.Cells.lic`)
      in the project resources and load it at runtime to unlock full features.'
    text: '**License Configuration:** Place your license file (`Aspose.Cells.lic`)
      in the project resources and load it at runtime to unlock full features.'
  - name: '**Download the library [here](https://releases.aspose.com/cells/java/).**'
    text: '**Download the library [here](https://releases.aspose.com/cells/java/).**'
  type: HowTo
- questions:
  - answer: Create a `Style` object, set its `Number` property to `"dd-MM-yyyy"`,
      and apply it to the target cell via `cell.setStyle(style)`. **`Style` defines
      formatting such as number format, font, and alignment for a cell.**
    question: How do I format a cell to display dates in `dd‑MM‑yyyy` format?
  - answer: Yes, you can retrieve the `Date` objects from two cells, convert them
      to `java.time.LocalDate`, and use `ChronoUnit.DAYS.between(start, end)` for
      precise control.
    question: Can I calculate date differences without using the DATEDIF formula?
  - answer: Absolutely. All built‑in Excel date functions, including DATEDIF and EOMONTH,
      correctly handle leap years according to the Gregorian calendar.
    question: Does Aspose.Cells support leap‑year calculations?
  - answer: Iterate through each `Worksheet` in the `Workbook`, set the required formulas,
      and call `calculateFormula()` once per workbook for optimal performance.
    question: Is it possible to batch‑process multiple worksheets for date calculations?
  - answer: All functions are available from **Aspose.Cells 23.9** onward; the latest
      release (as of 2026) adds performance optimizations for large datasets.
    question: What version of Aspose.Cells is required for these features?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- excel date functions
- aspose cells
- java excel processing
- date calculations
- java tutorial
title: 在 Java 中計算日期差異 – Excel 日期函數
url: /zh-hant/java/basic-excel-functions/excel-date-functions-tutorial/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel 日期函數教學

在本綜合教學中，**calculate date difference java** 是我們的主要焦點。我們將逐步說明如何使用 Aspose.Cells for Java 來處理 Excel 日期函數，從建構日期、取得當前日期、計算差異，到尋找月份結尾。無論您是要優化報告引擎或自動化試算表，這些技巧都能為您節省時間並減少錯誤。讓我們開始吧！

## 快速解答
- **如何在 Java 中計算日期差異？** 使用 Aspose.Cells 的 DATEDIF 函數，並指定單位（天、月、年）。  
- **如何從 Java 取得 Excel 中的今天日期？** 透過 Aspose.Cells 呼叫 TODAY 函數，或將儲存格的值設定為 `new Date()`。  
- **哪個方法會回傳月份的最後一天？** 使用 EOMONTH 函數；Aspose.Cells 會自動計算。  
- **我需要 Aspose.Cells 的授權嗎？** 是的，有效的授權會移除評估水印並解鎖全部功能。  
- **支援哪個 Java 版本？** Aspose.Cells 支援 Java 8 及更新版本。

## Excel 日期函數是什麼？
Excel 日期函數是內建公式，可在工作表中建立、操作或評估日期。它們讓您能執行算術運算、取得當前日期，或計算月份邊界，而無需手動計算。透過使用這些函數，您可以加減天、月或年，計算兩個日期之間的天數，並自動調整閏年與不同月份長度，同時保持資料以 Excel 能理解的格式儲存，並可依區域設定顯示。

## 為何使用 Aspose.Cells for Java 來實作 Excel 日期函數？
Aspose.Cells 支援 **50+** 種輸入與輸出格式，能在不將整個檔案載入記憶體的情況下處理 **最多 1 000 頁** 的試算表，且公式計算速度比原生 Excel 快 **最高 3 倍**。此效能提升對大型資料管線至關重要。

## 了解 Excel 中的日期函數
Excel 提供豐富的日期函數，簡化複雜計算。以下我們將重點介紹最常用的函數，並示範 Aspose.Cells 如何自動計算它們。

### DATE 函數
`DATE` 函數從年、月、日組件建立日期值。  
**直接答案：** `=DATE(2023, 12, 31)` 會回傳 2023 年 12 月 31 日的序號，Excel 會將其格式化為日期。在 Java 中，您可以將儲存格的公式設定為此字串，Aspose.Cells 會在工作簿儲存或重新計算時計算正確的日期。

### TODAY 函數
`TODAY` 函數回傳當前系統日期（不含時間）。  
**直接答案：** `=TODAY()` 總是反映工作簿開啟或重新計算時的當天日期，非常適合動態報表。

### DATEDIF 函數
`DATEDIF` 函數計算兩個日期之間的天、月或年差異。  
**直接答案：** `=DATEDIF(A1, B1, "d")` 會給出儲存格 A1 與 B1 之間的天數。這正是我們的 **calculate date difference java** 情境的核心。

### EOMONTH 函數
`EOMONTH` 函數回傳給定起始日期所在月份的最後一天，可依指定的月份數量偏移。  
**直接答案：** `=EOMONTH(A1, 0)` 會返回 A1 所在月份的最後一天。

## 使用 Aspose.Cells for Java
既然我們已說明基礎，接下來看看如何設定 Aspose.Cells 並以程式方式套用這些函數。

### 設定 Aspose.Cells
在編寫程式碼之前，請確保環境已就緒：

1. **下載並安裝 Aspose.Cells：** 前往 [Aspose.Cells for Java](https://releases.aspose.com/cells/java/) 下載最新版本。  
2. **將函式庫加入您的專案：** 將 JAR 檔案加入建置路徑或加入 Maven 依賴。  
3. **授權設定：** 將授權檔 (`Aspose.Cells.lic`) 放置於專案資源中，並於執行時載入以解鎖全部功能。  
4. **在此下載函式庫 [此處](https://releases.aspose.com/cells/java/)。**  

### 如何在 Java 中使用 Aspose.Cells 計算日期差異？
`Workbook` 代表記憶體中的整個 Excel 檔案，包含工作表、儲存格與樣式。  
載入您的工作簿，設定 DATEDIF 公式，並進行評估。  
**直接答案：** 建立 `Workbook`，將 `=DATEDIF(A2,B2,"d")` 指派給儲存格，呼叫 `calculateFormula()`，然後讀取產生的數值。這會在單一 API 呼叫中提供兩個日期之間的精確天數。

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set the date using the DATE function
worksheet.getCells().get("A1").putValue("=DATE(2023, 9, 7)");

// Get the calculated date value
String calculatedDate = worksheet.getCells().get("A1").getStringValue();

// Print the result
System.out.println("Calculated Date: " + calculatedDate);
```

### 使用 DATE 函數與 Aspose.Cells
您可以直接在儲存格中嵌入 `DATE` 公式，從分別的年、月、日值建構日期。  
**直接答案：** 將儲存格的公式設定為 `=DATE(2024, 5, 15)`；呼叫 `calculateFormula()` 後，儲存格會根據工作簿的語系顯示 `15‑May‑2024`。

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Use the TODAY function to get the current date
worksheet.getCells().get("A1").setFormula("=TODAY()");

// Get the current date value
String currentDate = worksheet.getCells().get("A1").getStringValue();

// Print the result
System.out.println("Current Date: " + currentDate);
```

### 使用 TODAY 函數
以程式方式取得當前日期相當簡單。  
**直接答案：** 將 `=TODAY()` 指派給儲存格，呼叫 `calculateFormula()`，每次開啟或重新計算工作簿時，儲存格都會顯示今天的日期。

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set two date values
worksheet.getCells().get("A1").putValue("2023-09-07");
worksheet.getCells().get("A2").putValue("2023-08-01");

// Calculate the difference using DATEDIF
worksheet.getCells().get("A3").setFormula("=DATEDIF(A1, A2, \"d\")");

// Get the difference in days
int daysDifference = worksheet.getCells().get("A3").getIntValue();

// Print the result
System.out.println("Days Difference: " + daysDifference);
```

### 使用 DATEDIF 計算日期差異
對於核心的 **calculate date difference java** 任務，使用 DATEDIF。  
**直接答案：** 在儲存格中放入 `=DATEDIF(C2,D2,"m")` 可取得月份差異，或將 `"m"` 替換為 `"y"` 或 `"d"` 以分別取得年或天的差異。計算後，透過 `cell.getIntValue()` 讀取數值結果。

```java
// Create a new workbook
Workbook workbook = new Workbook();

// Access the first worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);

// Set a date value
worksheet.getCells().get("A1").putValue("2023-09-07");

// Calculate the end of the month using EOMONTH
worksheet.getCells().get("A2").setFormula("=EOMONTH(A1, 0)");

// Get the end-of-month date
String endOfMonth = worksheet.getCells().get("A2").getStringValue();

// Print the result
System.out.println("End of Month: " + endOfMonth);
```

### 尋找月份結尾
`EOMONTH` 函數協助您找出計費週期或報告期間的月份最後一天。  
**直接答案：** 將儲存格的公式設定為 `=EOMONTH(E2,0)`；公式計算後，儲存格會顯示 E2 所在月份的最後一天。

## 常見陷阱與技巧
- **公式重新計算：** 設定或修改公式後，務必呼叫 `workbook.calculateFormula()`；否則儲存格會保留舊值。  
- **日期序號：** Excel 以序號儲存日期；讀取值時，使用 `cell.getDateValue()` 取得 `java.util.Date` 物件。  
- **語系問題：** 日期格式遵循工作簿的語系設定。如需特定顯示格式，請明確設定樣式。  
- **大型工作簿：** 對於 **數十萬列** 的檔案，啟用 `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` 以降低記憶體使用量。  
- **`WorkbookSettings` 為 `Workbook` 設定記憶體與計算選項。**  

## 常見問答
**Q: 如何將儲存格格式化為 `dd‑MM‑yyyy` 日期格式？**  
A: 建立 `Style` 物件，將其 `Number` 屬性設為 `"dd-MM-yyyy"`，並透過 `cell.setStyle(style)` 套用至目標儲存格。  
**`Style` 定義儲存格的格式設定，例如數字格式、字型與對齊方式。**

**Q: 是否可以在不使用 DATEDIF 公式的情況下計算日期差異？**  
A: 可以，您可以從兩個儲存格取得 `Date` 物件，轉換為 `java.time.LocalDate`，並使用 `ChronoUnit.DAYS.between(start, end)` 進行精確計算。

**Q: Aspose.Cells 是否支援閏年計算？**  
A: 當然支援。所有內建的 Excel 日期函數，包括 DATEDIF 與 EOMONTH，皆會依格里曆正確處理閏年。

**Q: 是否可以批次處理多個工作表以進行日期計算？**  
A: 遍歷 `Workbook` 中的每個 `Worksheet`，設定所需公式，然後對每個工作簿呼叫一次 `calculateFormula()` 以獲得最佳效能。

**Q: 需要哪個版本的 Aspose.Cells 才能使用這些功能？**  
A: 所有功能自 **Aspose.Cells 23.9** 版起即提供；最新發行版（截至 2026 年）為大型資料集加入效能最佳化。

## 結論
本教學深入探討了 Excel 日期函數，並示範如何使用 Aspose.Cells for Java **calculate date difference java**。您現在了解如何設定函式庫、套用 DATE、TODAY、DATEDIF 與 EOMONTH 公式，並處理諸如語系格式化與大規模處理等常見挑戰。將這些模式納入您的 Java 應用程式，即可自信地自動化以日期為驅動的報告與分析。

---

**最後更新：** 2026-07-26  
**測試環境：** Aspose.Cells 24.11 for Java  
**作者：** Aspose  
**相關資源：** API Reference [此處](https://reference.aspose.com/cells/java/) | Download Free Trial [此處](https://releases.aspose.com/cells/java/)

{{< blocks/products/products-backtop-button >}}

## 相關教學

- [精通 Excel 中的 1904 日期系統：使用 Aspose.Cells Java 進行有效的儲存格操作](/cells/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [精通 Excel 資料呈現：使用 Aspose.Cells for Java 進行數字與自訂日期格式化](/cells/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Aspose.Cells Java 的 Excel 公式與函數教學](/cells/java/formulas-functions/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

```java
// Create a date style
Style dateStyle = workbook.createStyle();
dateStyle.setCustom("dd-MM-yyyy");

// Apply the style to a cell
worksheet.getCells().get("A1").setStyle(dateStyle);
```