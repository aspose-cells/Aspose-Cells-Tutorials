---
category: general
date: 2026-06-18
description: 使用 Aspose.Cells 在 Java 中解析日本元號日期。了解如何快速從 Excel 儲存格讀取日期並提取日期時間。
draft: false
keywords:
- parse japanese era date
- read date from excel cell
- extract datetime from excel cell
language: zh-hant
og_description: 解析日本元號日期於 Java 使用 Aspose.Cells。此指南示範如何從 Excel 儲存格讀取日期，並在簡單幾步內提取日期時間。
og_title: 在 Java 中從 Excel 解析日本元號日期 – 完整教學
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  headline: Parse Japanese Era Date from Excel in Java – Full Guide
  type: TechArticle
- description: Parse Japanese era date in Java using Aspose.Cells. Learn how to read
    date from Excel cell and extract datetime from Excel cell quickly.
  name: Parse Japanese Era Date from Excel in Java – Full Guide
  steps:
  - name: Multiple Eras
    text: Japan has had several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa). The `setParseDateUsingJapaneseEra(true)`
      flag covers all of them automatically, but be aware that older dates may fall
      outside the library’s supported range (typically 1868‑present). If you encounter
      a date like “昭和45年12月31日”, the sam
  - name: Blank or Invalid Cells
    text: 'If a cell is empty or contains a malformed string, `cell.getDateTime()`
      throws a `CellsException`. Guard against this with a simple check:'
  - name: Time Component
    text: The example only includes a date, but if your Excel file also stores time
      (e.g., “令和3年5月10日 14:30”), Aspose.Cells will preserve the time portion. The
      `LocalDateTime` you receive will include hours, minutes, and seconds.
  type: HowTo
tags:
- Java
- Excel
- DateTime
title: 從 Excel 解析日本年號日期（Java）— 完整指南
url: /zh-hant/java/cell-operations/parse-japanese-era-date-from-excel-in-java-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從 Excel 解析日文元號日期（Java）完整指南

是否曾需要 **解析日文元號日期**，但不確定如何將其轉換為一般的公曆 `DateTime`？你並不孤單——許多開發者在處理日本舊會計表或政府表格時，都會遇到這個問題。好消息是，只要寫幾行 Java 程式碼並使用正確的函式庫，就能 **從 Excel 讀取日期** 並 **從 Excel 取出日期時間**，無需手動字串處理。

在本教學中，我們將一步步示範完整、可執行的範例，說明如何將「令和3年5月10日」等 **解析日文元號日期** 字串轉換為 Java `java.time.LocalDateTime`。我們會說明所需的 Maven 依賴、為何必須啟用元號感知的解析，並指出常見的陷阱。完成後，你將擁有一段可直接放入任何 Java 專案的生產級程式碼。

## 前置條件

- Java 17 或更新版本（程式碼亦可在 Java 8+ 上執行）
- Maven 或 Gradle 建置系統
- 對 Excel 檔案有基本了解
- **Aspose.Cells for Java** 函式庫（免費試用版可用於測試）

如果上述任一項你不熟悉，別擔心——我會一步步示範如何加入函式庫並開始使用。

## 步驟 1：將 Aspose.Cells 加入專案

首先，你需要能夠理解日文元號日期的函式庫。Aspose.Cells 為你處理繁重的工作。

**Maven**：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for latest version -->
</dependency>
```

**Gradle**：

```groovy
implementation 'com.aspose:aspose-cells:24.9'
```

依賴解決後，你就可以開始撰寫能 *從 Excel 讀取日期* 並 *從 Excel 取出日期時間* 的程式碼了。

## 步驟 2：建立 Workbook 並鎖定第一個工作表

我們先在記憶體中建立一個新的 Workbook，並取得第一張工作表。這對應原始範例的前兩行程式碼。

```java
import com.aspose.cells.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize workbook and worksheet
        Workbook workbook = new Workbook();               // creates a blank workbook
        Worksheet sheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

為何要從全新 Workbook 開始？這樣可以保證環境乾淨，讓我們能控制每一個設定——在之後啟用元號感知解析時尤為關鍵。

## 步驟 3：將日文元號日期字串寫入 A1 儲存格

現在我們模擬一個已經包含日文元號日期的 Excel 檔案。實務上你可能會載入現有的 `.xlsx`，但為了說明，我們會 **寫入**這個值。

```java
        // Step 3: Insert a Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日"); // Reiwa 3rd year = 2021-05-10
```

此字串遵循標準的日文表示法：*元號* + *年* + *月* + *日*。若未額外設定，Aspose.Cells 會把它當作純文字，而非日期。

## 步驟 4：啟用元號感知的日期解析

這是關鍵步驟：告訴 Workbook 在遇到 **解析日文元號日期** 字串時進行解析。這透過 `ParseDateUsingJapaneseEra` 旗標完成。

```java
        // Step 4: Turn on era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);
```

為何需要這樣做？預設情況下 Aspose.Cells 會假設使用公曆，因而把「令和3年5月10日」視為字串。啟用此旗標後，引擎會在底層把它轉換為 `java.util.Date`（或等價的 `java.time` 型別）。

## 步驟 5：取得已解析的 DateTime 值

現在 Workbook 已能正確解讀元號，我們可以向儲存格索取其 `DateTime` 表示。

```java
        // Step 5: Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime(); // returns java.util.Date
        // Convert to java.time.LocalDateTime for modern APIs
        java.time.Instant instant = javaDate.toInstant();
        java.time.ZoneId zone = java.time.ZoneId.systemDefault();
        java.time.LocalDateTime dateTime = java.time.LocalDateTime.ofInstant(instant, zone);
```

請注意，我們 **從 Excel 讀取日期** 時使用 `cell.getDateTime()`。此方法回傳 `java.util.Date`，我們隨即將其轉換為 `LocalDateTime` 以提升型別安全性。這同時滿足 **從 Excel 取出日期時間** 的需求，寫法簡潔且符合慣例。

## 步驟 6：驗證結果

最後，將公曆日期印出，以確認轉換成功。

```java
        // Step 6: Output the Gregorian date
        System.out.println(dateTime); // Expected output: 2021-05-10T00:00
    }
}
```

執行程式後，你應該會看到：

```
2021-05-10T00:00
```

此輸出證明我們成功 **解析日文元號日期**、**從 Excel 讀取日期**，以及 **從 Excel 取出日期時間**，整個流程順利完成。

## 處理實務上的邊緣案例

### 多個元號

日本歷史上曾有多個元號（明治、大正、昭和、平成、令和）。`setParseDateUsingJapaneseEra(true)` 旗標會自動支援全部元號，但需注意較早的日期可能超出函式庫支援範圍（通常為 1868 年至今）。若遇到「昭和45年12月31日」，相同程式碼會將其轉換為 1970‑12‑31。

### 空白或無效儲存格

若儲存格為空或包含格式錯誤的字串，`cell.getDateTime()` 會拋出 `CellsException`。可使用簡單的檢查來防護：

```java
if (cell.getType() == CellValueType.IS_DATE) {
    // safe to call getDateTime()
} else {
    System.out.println("Cell does not contain a parsable date.");
}
```

### 時間部分

範例僅包含日期，但若你的 Excel 同時儲存時間（例如「令和3年5月10日 14:30」），Aspose.Cells 會保留時間資訊。你取得的 `LocalDateTime` 會包含時、分、秒。

## 完整可執行範例

將上述所有步驟整合，以下是完整、可直接複製貼上的程式：

```java
import com.aspose.cells.*;
import java.time.*;

public class JapaneseEraDateParser {
    public static void main(String[] args) throws Exception {
        // Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Insert Japanese era date string into A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue("令和3年5月10日");

        // Enable era‑aware parsing
        workbook.getSettings().setParseDateUsingJapaneseEra(true);

        // Extract the parsed DateTime
        java.util.Date javaDate = cell.getDateTime();
        LocalDateTime dateTime = javaDate.toInstant()
                                         .atZone(ZoneId.systemDefault())
                                         .toLocalDateTime();

        // Output the Gregorian date
        System.out.println(dateTime); // 2021-05-10T00:00
    }
}
```

將檔案另存為 `JapaneseEraDateParser.java`，使用 `javac` 編譯，然後以 `java` 執行。若環境設定正確，控制台會印出對應的公曆日期。

## 專業提示與常見陷阱

- **專業提示：** 在讀取任何儲存格值之前，務必先設定 `setParseDateUsingJapaneseEra(true)`。在讀取儲存格之後再變更旗標，無法遞補已讀取的值。
- **留意語系設定：** 函式庫會根據 Unicode 字元解析元號字串，無需額外設定日文語系。
- **效能說明：** 啟用元號解析會帶來極小的額外開銷。若只需處理少量儲存格，可暫時開啟旗標、讀取完畢後再關閉。
- **測試建議：** 使用 Aspose 的免費試用版，對含有多個元號日期的真實 Excel 檔案進行驗證，確保你的生產程式碼如預期運作。

## 結論

我們剛剛示範了如何使用 Java 與 Aspose.Cells **解析日文元號日期**，並透過啟用元號感知解析，**從 Excel 讀取日期** 以及 **從 Excel 取出日期時間**，以乾淨且型別安全的方式完成。此方法支援所有現代日本元號，能處理時間成分，亦能優雅地面對無效資料。

準備好接受下一個挑戰了嗎？試著載入實際的 `.xlsx`，其中同時包含公曆與日文元號日期，或嘗試將取得的 `LocalDateTime` 格式化為符合本地語系的字串。你也可以探索將轉換後的日期寫回 Excel，供只懂公曆的下游系統使用。

有任何問題或遇到奇怪的邊緣案例嗎？在下方留言，我們一起討論，祝開發順利！

## 接下來該學什麼？

以下教學與本指南的技術緊密相關，能幫助你進一步掌握 API 功能並探索其他實作方式：

- [Master the 1904 Date System in Excel Using Aspose.Cells Java for Effective Cell Operations](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}