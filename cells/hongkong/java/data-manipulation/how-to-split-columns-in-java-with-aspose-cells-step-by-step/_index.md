---
category: general
date: 2026-10-07
description: 如何使用 Aspose.Cells for Java 分割欄位。學習將字串分割成欄位、自動化 Excel 公式，並以簡短程式碼將公式寫入儲存格。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: zh-hant
lastmod: 2026-10-07
og_description: 如何在 Java 中使用 Aspose.Cells 分割欄位。 本教學示範如何將字串分割成欄位、自動執行 Excel 公式計算，以及將公式寫入儲存格。
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: 使用 Aspose.Cells 在 Java 中拆分欄位 – 快速教學
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何在 Java 中使用 Aspose.Cells 拆分欄位 – 逐步指南
url: /zh-hant/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose.Cells 分割欄位 – 步驟指南

如果您需要以程式方式在 Excel 工作表中 **how to split columns**，本指南將向您展示使用 Aspose.Cells for Java 的完整流程。您還將學習如何 **split string into columns**、**automate Excel formula** 評估，以及 **write formula to a cell**，使用簡潔、可投入生產的程式碼。

程式化的欄位分割可消除手動複製貼上、減少錯誤，並支援大規模資料轉換。完成本教學後，您即可即時產生、修改與評估公式，讓 Excel 成為 Java 後端的真正一部份。

## 前置條件

* 已安裝 Java 17 或更新版本。
* 已安裝 Maven 3.8+（或 Gradle）以管理相依性。
* 擁有 Aspose.Cells for Java 授權（免費評估版可用於學習）。
* 具備 Java 語法與 Excel 概念的基本熟悉度。

如果缺少上述任何項目，請先安裝；程式碼範例假設使用標準的 Maven 專案。

## 步驟 1：將 Aspose.Cells 加入您的專案

在您的 `pom.xml` 中加入以下相依性。此操作會下載最新的穩定版 Aspose.Cells 程式庫。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**此步驟的重要性：** 此程式庫提供 `Workbook`、`Worksheet` 與 `Cell` 類別，讓您在沒有 Microsoft Office 的情況下操作 Excel 檔案。若未加入相依性，程式碼將無法編譯。

## 步驟 2：建立工作簿並選取第一個工作表

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

`Workbook` 物件代表整個 Excel 檔案。存取第一個工作表可確保公式寫入時有可預測的起始點。

## 步驟 3：將 WRAPCOLS 公式寫入目標儲存格

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**為何使用 `WRAPCOLS`：** 內建的 Excel 函數 `WRAPCOLS` 會自動將單一文字值依指定的欄位數分割，並智慧地處理單字邊界。這是 **split string into columns** 的最可靠方法，無需自行撰寫解析邏輯。

## 步驟 4：強制工作簿評估公式

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

呼叫 `calculateFormula()` **automates Excel formula** 於伺服器端的評估。若未呼叫此方法，儲存格仍只會顯示公式文字，而非計算結果。

## 步驟 5：取得並顯示分割結果

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

執行程式時，主控台會輸出：

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

產生的 `SplitColumnsResult.xlsx` 檔案會顯示三個欄位已填入分割後的文字。

## 了解 WRAPCOLS 函數

* **語法：** `WRAPCOLS(text, columns, [delimiter])`
* **參數：**
  * `text` – 您想要分割的字串。
  * `columns` – 要將文字分配到的欄位數。
  * `delimiter`（可選）– 用於斷開字串的字元；預設為空格。
* **返回值：** 會向相鄰儲存格溢出的陣列，每個元素包含原始文字的一部分。

由於此函數會水平溢出，您只需將公式寫入最左側的儲存格（範例中的 A1），Excel 會自動填入 B1、C1… 等儲存格。

## 常見變形與邊緣情況

| Situation | Recommended adjustment |
|-----------|------------------------|
| **可變欄位數** | 將硬編碼的 `3` 改為變數：`targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **自訂分隔符號** | 使用第三個參數，例如 `=WRAPCOLS(A2,4,",")` 以逗號作為分割。 |
| **來源字串為空** | 此函數會返回空儲存格；在設定公式前請先檢查 `null` 或空字串。 |
| **大型資料集** | 在每一列的迴圈中套用公式，然後在迴圈結束後僅呼叫一次 `calculateFormula()` 以提升效能。 |
| **非 ASCII 字元** | WRAPCOLS 支援 Unicode；請確保您的 Java 原始檔案以 UTF‑8 編碼儲存。 |

**專業提示：** 處理大量列時，將公式儲存於字串變數並重複使用，可避免重複字串串接的開銷。

## 完整、可執行範例

以下是完整的程式碼，可直接複製貼上。它包含匯入語句、例外處理，以及可選的儲存操作。

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

執行此程式會產生與前述相同的主控台輸出，並寫入一個清楚示範 **how to split columns** 的 Excel 檔案。

## 疑難排解清單

* **Formula not evaluating** – 確認在設定公式後已呼叫 `workbook.calculateFormula()`。
* **Empty cells after split** – 確認來源字串不是 `null` 或空，且欄位數大於零。
* **License exception** – 在建立工作簿之前提供有效的 Aspose.Cells 授權檔案 (`License license = new License(); license.setLicense("Aspose.Total.lic");`) 以移除評估水印。
* **Performance lag on large sheets** – 在所有公式寫入完成後僅呼叫一次 `calculateFormula()`，而非每個儲存格都呼叫。

## 結論

您現在已了解如何在 Java 中使用 Aspose.Cells **how to split columns**，以及如何使用 `WRAPCOLS` 函數 **split string into columns**，如何 **automate Excel formula** 評估，並以程式方式 **write formula to a cell**。此技巧可省去手動資料前處理步驟，將 Excel 強大的文字處理功能直接整合至您的 Java 應用程式中。

### 後續步驟

* 探索其他文字函數，如 `TEXTSPLIT` 與 `FILTERXML`，以應對更複雜的解析情境。
* 將 `WRAPCOLS` 與 `IFERROR` 結合，以優雅地處理意外的輸入。
* 將此解決方案整合至 Spring Boot 服務，該服務透過 REST 接收 CSV 資料並回傳已填充的 Excel 檔案。

掌握這些模式後，您即可構建穩健且自動化的 Excel 工作流程，隨業務需求擴展。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南技術緊密相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [aspose cells java – 將姓名分割至欄位](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [使用 Aspose.Cells 在 Java 中自動調整 Excel 欄寬](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [如何使用 Aspose.Cells Java&#58; 刪除 Excel 空白欄位&#58; 完整指南](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}