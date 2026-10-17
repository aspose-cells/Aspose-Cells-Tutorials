---
category: general
date: 2026-10-16
description: Aspose.Cells 在 Java 中使用 EXPAND 函數設定公式。學習一步一步的範例，了解如何使用 expand 進行動態範圍。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells set formula
- how to use expand
- expand function example
- Java Excel automation
- dynamic range formula
language: zh-hant
lastmod: 2026-10-16
og_description: Aspose.Cells 在 Java 中使用 EXPAND 函數設定公式。透過完整範例了解如何在 Excel 工作簿中動態展開範圍。
og_image_alt: Spreadsheet screenshot showing the EXPAND formula applied to cell B2
  via Aspose.Cells
og_title: Aspose.Cells 使用 EXPAND 設定公式 – Java 教學
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: Aspose.Cells set formula in Java using the EXPAND function. Learn a
    step‑by‑step example and see how to use expand for dynamic ranges.
  headline: Aspose.Cells set formula with EXPAND function – complete Java guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel formulas
- Spreadsheet automation
title: Aspose.Cells 使用 EXPAND 函數設定公式 – 完整 Java 指南
url: /zh-hant/java/formulas-functions/aspose-cells-set-formula-with-expand-function-complete-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells 設定公式與 EXPAND 函數 – 完整 Java 教學

如果您需要以程式方式 **aspose cells set formula**，本教學將完整示範。您將學習如何使用 EXPAND 函數，從起始儲存格向下與向右各擴展五列與五欄，全部透過 Java 程式碼完成。

在 Java 中操作 Excel 公式常常感覺笨重，但 Aspose.Cells 抽象化了這些複雜度。以下各節我們將逐步說明完整可執行的範例，討論每行程式碼的意義，並探討常見的變化，例如不同的起始儲存格或可變的擴展大小。

## 本教學涵蓋內容

* 使用 Aspose.Cells 載入既有活頁簿  
* 取得工作表及其儲存格集合  
* 使用 `EXPAND` 函數 **aspose cells set formula**  
* 重新計算活頁簿以評估公式  
* 儲存結果並驗證輸出  

不需要除 Aspose.Cells 之外的其他函式庫，程式碼可在任何 Java 8 以上的執行環境執行。完成後您即可將此模式套用至其他動態公式。

## 前置條件

* Java Development Kit (JDK) 8 或更新版本  
* Aspose.Cells for Java（從[官方網站](https://downloads.aspose.com/cells/java)下載）  
* 放置於已知目錄的輸入 Excel 檔案（`input.xlsx`）  
* 具備 Java 語法基礎，並熟悉 Maven/Gradle 之相依管理  

## 第一步：設定專案並加入 Aspose.Cells

若使用 Maven，請在 `pom.xml` 中加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest version -->
</dependency>
```

Gradle 的等效寫法如下：

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **專業提示：** 請始終使用最新的穩定版；較新版本包含公式計算效能的改進。

## 第二步：載入活頁簿

我們解決方案的第一行會開啟既有活頁簿。請將 `YOUR_DIRECTORY` 替換為 `input.xlsx` 所在的絕對路徑。

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*為什麼這很重要*：載入活頁簿會在記憶體中建立表示，讓您能在不再次存取檔案系統的情況下操作工作表、儲存格與公式。

## 第三步：取得目標工作表與儲存格集合

我們使用第一張工作表（索引 0）。`Cells` 物件可直接依地址存取單一儲存格。

```java
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
```

若需使用其他工作表，請變更索引或使用 `get("SheetName")`。

## 第四步：**aspose cells set formula** – 套用 EXPAND 函數

現在我們在儲存格 **B2** 設定公式。`EXPAND` 函數接受三個參數：參考儲存格、要向下擴展的列數，以及要向右擴展的欄數。

```java
        // Apply the EXPAND function to B2, expanding 5 rows and 5 columns from A2
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");
```

### 如何使用 EXPAND

* **參考儲存格 (`A2`)** – 動態範圍的起始點。  
* **列數 (`5`)** – 範圍向下要擴展的列數。  
* **欄數 (`5`)** – 範圍向右要擴展的欄數。

若需要彈性解決方案，可將這些值改為變數：

```java
int rows = 10;
int cols = 3;
cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));
```

## 第五步：重新計算活頁簿

設定公式後，必須告訴 Aspose.Cells 執行計算。`calculateFormula()` 方法會處理活頁簿中所有公式。

```java
        // Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();
```

> **為什麼要重新計算？**  
> 若未呼叫此方法，公式將不會被評估，輸出檔案會顯示原始的 `=EXPAND(...)` 文字字串，而非展開後的陣列。

## 第六步：儲存更新後的活頁簿

最後，將變更寫入新檔案。此做法保留原始活頁簿以供比較。

```java
        // Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

當您在 Excel 中開啟 `output.xlsx` 時，儲存格 **B2** 會顯示一個 5 × 5 的區塊，值來自起始於 **A2** 的區域。若 **A2** 為數字 `1`，則整個區塊皆顯示 `1`，因為 `EXPAND` 會將來源值複製到整個擴展範圍。

## 完整、可執行的原始碼

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet and its cells collection
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Step 3: Apply the EXPAND function to cell B2, referencing A2 and expanding 5 rows and 5 columns
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");

        // Step 4: Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();

        // Step 5: Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### 預期輸出

| B2 | C2 | D2 | E2 | F2 |
|----|----|----|----|----|
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |

（實際值取決於來源檔案中 `A2` 的內容。）

## 常見變化與邊緣情況

| 情境 | 程式碼變更 | 原因 |
|----------|-------------|--------|
| **不同的起始儲存格** | `cells.get("C3").setFormula("=EXPAND(D3,3,2)");` | 使用任意儲存格作為參考；公式會相對於該儲存格展開。 |
| **變數擴展大小** | `int rows = 8; int cols = 4; cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));` | 允許在執行時決定範圍大小，適用於資料驅動的報表。 |
| **零大小擴展** | `=EXPAND(A2,0,0)` | 僅返回原始儲存格的值；適用於可能稍後擴大尺寸的條件邏輯。 |
| **使用命名範圍** | `cells.get("B2").setFormula("=EXPAND(MyRange,5,5)");` | 當工作簿中已定義 `MyRange` 時可使用；使公式更易讀。 |

> **注意：** Excel 的最大陣列尺寸為 16,384 欄 × 1,048,576 列。若嘗試超過此限制會拋出計算錯誤。

## 除錯技巧

* **公式未評估？** 確認在每次 `setFormula` 後都有呼叫 `workbook.calculateFormula();`。  
* **值不如預期？** 檢查參考儲存格（範例中的 `A2`）是否包含您欲傳播的資料。  
* **效能顧慮** – 大範圍的擴展可能耗時。若只需部分資料，請縮減列/欄參數。

## 結論

您現在已擁有完整的 **aspose cells set formula** 範例，示範了在 Java 中 **如何使用 EXPAND**。透過載入活頁簿、設定 `EXPAND` 公式、重新計算並儲存，您即可在不手動操作 Excel 的情況下產生動態範圍。

接下來您可以探索：

* 使用其他動態函數，如 `FILTER` 或 `SEQUENCE` 搭配 Aspose.Cells。  
* 將此邏輯嵌入於即時產生報表的 Web 服務。  
* 透過 Aspose.Cells API 將 `EXPAND` 與條件格式結合。

歡迎嘗試不同的起始儲存格、變數大小或命名範圍，以符合您的自動化情境。若您覺得此 **expand function example** 有幫助，請與團隊分享或在 GitHub 上貢獻改進。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南密切相關的主題，建立在此處示範的技巧之上。每篇資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [精通 Aspose.Cells Java：如何在 Excel 中中斷公式計算](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [使用 Aspose.Cells Java 將 Excel 表格轉換為範圍&#58; 步驟指南](/cells/english/java/tables-structured-references/convert-excel-tables-ranges-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 設定 Excel 文件版本](/cells/english/java/workbook-operations/set-excel-version-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}