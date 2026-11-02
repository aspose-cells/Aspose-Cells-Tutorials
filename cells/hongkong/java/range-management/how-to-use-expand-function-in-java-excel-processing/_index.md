---
category: general
date: 2026-10-10
description: 學習如何在 Java 中讀寫 Excel 檔案時使用 expand 函數。一步一步的指南，提供完整程式碼與說明。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use expand function
- read and write excel file java
- Java Excel formula
- Aspose.Cells expand
- Excel dynamic range Java
language: zh-hant
lastmod: 2026-10-10
og_description: 如何在 Java 中讀寫 Excel 檔案時使用 Expand 函數。請參考本完整教學，使用 Aspose.Cells 添加動態範圍。
og_image_alt: Screenshot of Java code using the EXPAND function on an Excel worksheet
og_title: 在 Java Excel 處理中如何使用 expand 函數 – 完整指南
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to use expand function while reading and writing Excel files
    in Java. Step‑by‑step guide with complete code and explanations.
  headline: How to use expand function in Java Excel processing
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Formula
title: 如何在 Java Excel 處理中使用 expand 函數
url: /zh-hant/java/range-management/how-to-use-expand-function-in-java-excel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java Excel 處理中使用 EXPAND 函數

如果您在 Java 中處理 Excel 檔案時需要 **如何使用 EXPAND 函數**，本教學將一步步示範。完成本教學後，您將能在 Java 專案中讀寫 Excel 檔案，並使用 `EXPAND` 公式動態展開儲存格範圍。

在處理 Excel 工作表時，常會遇到需要根據資料大小自動調整的公式。`EXPAND` 函數是 Excel 近期版本加入的功能，可依指定的列數與欄數擴大參照範圍。結合功能強大的 Java 函式庫，您可以在程式碼中自動化此行為，無需離開開發環境。

在本教學中，您將會：

* 載入既有活頁簿（`read and write excel file java` 情境）  
* 將 `EXPAND` 公式套用至儲存格  
* 重新計算公式，使新值顯示  
* 儲存更新後的活頁簿  

先備條件：

* 已安裝 Java 17 或更新版本  
* 使用 Maven 或 Gradle 管理相依性  
* Aspose.Cells for Java（提供 `Workbook`、`Worksheet` 等類別）  

> **專業提示：** Aspose.Cells 同時支援 `.xlsx` 與 `.xls` 格式，且不需要在主機上安裝 Microsoft Office。

## 您需要的工具

| 項目 | 理由 |
|------|------|
| JDK 17+ | 現代語言功能與更佳效能 |
| Maven/Gradle | 輕鬆加入函式庫 |
| Aspose.Cells for Java | 提供 `Workbook`、`Worksheet` 與公式引擎 |
| Excel 檔案（`input.xlsx`） | 用於示範 `EXPAND` 函數的來源活頁簿 |

使用 Maven 將 Aspose.Cells 加入專案：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

或使用 Gradle：

```groovy
implementation 'com.aspose:aspose-cells:23.12'
```

## 步驟 1：載入活頁簿（how to use expand function – 初始化）

第一步是開啟要修改的 Excel 檔案。`Workbook` 代表記憶體中的整個檔案。

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

**為什麼重要：** 載入活頁簿後即可存取所有工作表、儲存格與內部公式引擎。未載入活頁簿就無法讀寫 Excel file java 資料。

## 步驟 2：取得目標工作表

大多數活頁簿包含多張工作表；範例使用第一張工作表（索引 0）。您也可以依名稱取得工作表。

```java
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**說明：** `Worksheet` 物件會公開 `Cells` 集合，您在此設定公式。若需操作其他工作表，只要將索引改成對應的數字或呼叫 `get("SheetName")` 即可。

## 步驟 3：設定 EXPAND 公式（how to use expand function in practice）

現在將 `EXPAND` 公式寫入 **B1** 儲存格。此公式會將參照 `A1` 向下 **5 列**、向右 **1 欄** 展開，產生範圍 `A1:A6`，但向右平移一欄。

```java
        // Apply the EXPAND formula to B1
        // =EXPAND(A1,5,1) expands A1 by 5 rows and 1 column
        worksheet.getCells().get("B1").setFormula("=EXPAND(A1,5,1)");
```

**為什麼會生效：** `setFormula` 只會儲存公式字串，Aspose.Cells 不會立即求值。`EXPAND` 會在稍後觸發計算時才被評估。

## 步驟 4：重新計算公式（finalizing the expand function）

插入公式後，要求活頁簿重新計算所有相依儲存格。此步驟可確保新值出現在工作表上。

```java
        // Recalculate all formulas so the EXPAND result is evaluated
        workbook.calculateFormula();
```

**背後發生的事：** 計算引擎會解析 `EXPAND` 表達式，決定新的範圍，並將產生的陣列值寫回工作表。若 `A1` 為數字，展開後的儲存格會重複該數字。

## 步驟 5：儲存更新後的活頁簿

最後，將修改過的活頁簿寫回磁碟（或輸出串流）。這樣就完成 **read and write excel file java** 的完整流程。

```java
        // Save the workbook with the new formula evaluated
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

執行程式後會產生 `output.xlsx`，其中 **B1** 會呈現一個溢位範圍，將 `A1` 的值在五列一欄內複製。開啟檔案即可看到動態陣列的效果。

### 預期輸出

假設 `A1` 原本的數值為 `42`，則結果儲存格會是：

| B1 | B2 | B3 | B4 | B5 | B6 |
|----|----|----|----|----|----|
| 42 | 42 | 42 | 42 | 42 | 42 |

若 `A1` 為文字字串，則相同文字會在展開的範圍內溢出。

## 常見變化與例外情況

| 情境 | 調整方式 |
|----------|------------|
| **不同的起始儲存格** | 將 `"B1"` 改成任意地址，例如 `"C3"` |
| **僅向欄位展開** | 使用 `=EXPAND(A1,0,3)` 以向右展開三欄 |
| **動態列數** | 將靜態的 `5` 換成儲存格參照，如 `D1`，其內含欲展開的列數 |
| **使用命名範圍** | 將 `A1` 換成已定義的名稱，例如 `=EXPAND(MyRange,5,1)` |
| **公式錯誤** | 確保活頁簿儲存為支援動態陣列的格式（`.xlsx`）。舊版 `.xls` 會截斷溢位結果 |

### 處理大型工作表

面對極大活頁簿時，可使用自訂的 `CalcOptions` 物件呼叫 `workbook.calculateFormula(CalcOptions)`，以限制記憶體使用或啟用多執行緒計算。

```java
CalcOptions options = new CalcOptions();
options.setCalculateOnOpen(true); // Faster if you only need the result later
workbook.calculateFormula(options);
```

## 完整原始碼（可直接複製貼上）

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Set a formula that expands the range of A1 by 5 rows and 1 column
        worksheet.getCells().get("B1").setFormula("=EXPAND(A1,5,1)");

        // Step 4: Recalculate all formulas so the new value is evaluated
        workbook.calculateFormula();

        // Step 5: Save the workbook with the updated data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

> **注意：** 請將 `YOUR_DIRECTORY` 替換為 Excel 檔案的絕對或相對路徑。此程式碼可在任何 Java 支援的平台（Windows、macOS、Linux）上執行。

## 結論

現在您已掌握 **如何在 Java 環境中使用 EXPAND 函數** 以動態擴大儲存格參照，並了解完整的 **read and write excel file java** 工作流程。從載入活頁簿、套用 `EXPAND` 公式、重新計算到儲存，涵蓋了 Excel 自動化的全生命週期。

**接下來** 您可以探索：

* 結合 `EXPAND` 與其他動態陣列函數，如 `FILTER` 或 `SORT`。  
* 使用相同模式從資料庫或 REST API **read and write excel file java**。  
* 針對展開範圍套用條件格式化。  

歡迎將此範例套用到自己的專案，讓 `EXPAND` 函數協助您處理資料量隨時間變化的情境。

--- 

*祝開發順利！*


## 接下來該學什麼？

以下教學與本指南的技巧密切相關，提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能並探索其他實作方式。

- [How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide](/cells/english/java/formulas-functions/how-to-use-sequence-in-java-excel-workbook-step-by-step-guid/)
- [How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [How to Use Reduce in Excel with Java – Lambda Formula Guide](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}