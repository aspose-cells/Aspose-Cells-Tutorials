---
category: general
date: 2026-07-17
description: 使用 Java 的 lambda 函數建立 Excel 工作簿，示範 EXPAND 與 REDUCE 函數，並使用 Aspose.Cells
  計算 Excel 陣列函數。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use lambda function java
- create excel workbook java
- use reduce function excel
- use expand function excel
- calculate array functions excel
language: zh-hant
lastmod: 2026-07-17
og_description: 使用 Java Lambda 函數建立 Excel 工作簿，套用 EXPAND 與 REDUCE，並計算 Excel 陣列函數 –
  完整的逐步指南。
og_image_alt: Screenshot of use lambda function java creating Excel workbook with
  formulas
og_title: 使用 Java Lambda 表達式 – 使用 Aspose.Cells 建立 Excel 工作簿
schemas:
- author: Aspose
  dateModified: '2026-07-17'
  description: Use lambda function java to create an Excel workbook, demonstrate EXPAND
    and REDUCE functions, and calculate array functions in Excel with Aspose.Cells.
  headline: Use Lambda Function Java to Create Excel Workbook Example
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
- Lambda
title: 使用 Lambda 函式 Java 建立 Excel 工作簿範例
url: /zh-hant/java/workbook-operations/use-lambda-function-java-to-create-excel-workbook-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Lambda Function Java 建立 Excel 活頁簿範例

想要 **use lambda function java** 來建立 Excel 活頁簿嗎？在本教學中，我們將透過使用 Aspose.Cells 的完整範例，說明如何 **use expand function excel**、**use reduce function excel**，以及 **calculate array functions excel**，一次完成且易於跟隨的腳本。

如果你曾盯著試算表想說「一定有程式化的方式可以展開這個陣列或縮減這些數字」，那麼你來對地方了。閱讀完本指南後，你將擁有一個可執行的 Java 程式，能建立 Excel 檔案、注入 EXPAND、REDUCE、COT 與 COTH 公式，並儲存計算結果，同時展示 **lambda function java** 方法的威力。

---

## 前置條件 – 開始前您需要的項目

- **Java Development Kit (JDK) 8+** – 此程式碼使用 lambda 表達式，請確保您使用的至少是 JDK 8。  
- **Aspose.Cells for Java** – 一個商業函式庫，可在未安裝 Office 的情況下操作 Excel 檔案。請從 Aspose 官方網站取得最新的 JAR，並加入專案的 classpath。  
- 一個普通的 IDE（IntelliJ IDEA、Eclipse、VS Code）– 任意皆可，但具備 Maven/Gradle 支援的 IDE 能讓相依性管理更輕鬆。  

不需要額外安裝任何東西；函式庫會在背後處理所有繁重工作。

---

## 步驟 1：設定專案並匯入相依性

建立一個新的 Maven 專案（或 Gradle，如果你偏好），並加入 Aspose.Cells 的相依性：

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

如果你不是使用 Maven，只要把 `aspose-cells-24.10.jar` 放到 `libs` 資料夾，並加入建置路徑即可。

> **Pro tip:** 保持相依性為最新版本。較新的版本常會帶來效能提升與針對 EXPAND、REDUCE 等函式的錯誤修正。

---

## 使用 Lambda Function Java 建立 Excel 活頁簿

現在環境已就緒，讓我們 **use lambda function java**，直接在 Excel 公式中嵌入 LAMBDA 表達式。Excel 的 REDUCE 函式需要一個 lambda，而 Java 的字串處理讓這件事變得相當簡單。

```java
import com.aspose.cells.*;

public class Office365FunctionsDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Create a new workbook and obtain the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 3: Demonstrate the EXPAND function – expands a seed array to a larger size
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3},5,1)");
        // Explanation: EXPAND turns the 3‑element seed into a 5‑row, 1‑column array.

        // Step 4: Demonstrate the REDUCE function – aggregates an array into a single value
        // Here we **use lambda function java** inside the Excel formula.
        sheet.getCells().get("A2").setFormula(
            "=REDUCE(0,{1,2,3,4},LAMBDA(a,b,a+b))"
        );
        // Explanation: Starting at 0, the lambda (a,b) → a+b adds each element together.

        // Step 5: Use the COT function to calculate the cotangent of π/4
        sheet.getCells().get("A3").setFormula("=COT(PI()/4)");

        // Step 6: Use the COTH function to calculate the hyperbolic cotangent of 1
        sheet.getCells().get("A4").setFormula("=COTH(1)");

        // Step 7: Recalculate all formulas so the results are stored in the cells
        workbook.calculateFormula();

        // Step 8: Save the workbook with the evaluated results
        workbook.save("Office365Funcs.xlsx");
    }
}
```

### 為何這樣可行

- `Workbook` 是 **create excel workbook java** 任務的入口點。它在記憶體中代表整個檔案。  
- `Worksheet` 為我們提供可操作的工作表；預設的活頁簿已包含一張工作表。  
- `setFormula` 注入原始的 Excel 公式字串。請注意 REDUCE 那一行包含 `LAMBDA(a,b,a+b)` 片段——這裡我們 **use lambda function java** 告訴 Excel 如何合併數值。  
- `calculateFormula()` 強制 Aspose.Cells 評估所有公式，讓計算結果直接寫入檔案。若未呼叫此方法，儲存格只會保留公式文字。  

---

## 如何使用 Expand Function Excel – 動態展開陣列

**use expand function excel** 範例位於儲存格 `A1`。讓我們拆解公式的運作方式：

```excel
=EXPAND({1,2,3},5,1)
```

- `{1,2,3}` 為種子陣列（三個數字）。  
- `5` 告訴 Excel 將結果展開為五列。  
- `1` 設定欄數（僅一欄）。  

當活頁簿在 Excel 中開啟時，`A1:A5` 會顯示：

| A |
|---|
| 1 |
| 2 |
| 3 |
| 0 |
| 0 |

尾端的 0 為填充值，因為種子陣列不足以填滿要求的大小。

> **Common pitfall:** 忘記呼叫 `workbook.calculateFormula()` 會只留下原始的 `=EXPAND(...)` 文字，而非展開後的數字。

---

## 如何使用 Reduce Function Excel – 使用 Lambda 進行加總

**use reduce function excel** 行位於儲存格 `A2`。它的寫法如下：

```excel
=REDUCE(0,{1,2,3,4},LAMBDA(a,b,a+b))
```

- `0` 為初始累加值。  
- `{1,2,3,4}` 為我們欲縮減的陣列。  
- `LAMBDA(a,b,a+b)` 告訴 Excel 將每個元素 (`b`) 加到累計總和 (`a`)。  

計算完成後，`A2` 會顯示 **10**。如果想要計算乘積，只需將 `a+b` 改成 `a*b`——相同的 **use lambda function java** 模式依然適用。

---

## 計算 Array Functions Excel – COT 與 COTH

雖然不完全屬於陣列函式，COT

## 接下來您應該學習什麼？

以下教學涵蓋與本指南技術緊密相關的主題，並在此基礎上進一步延伸。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你掌握更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 Aspose Cells – Java Excel 引擎教學](/cells/english/java/calculation-engine/)
- [使用 Aspose.Cells Java 自訂 SUM 函式&#58; 強化您的計算](/cells/english/java/formulas-functions/custom-sum-function-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells 於 Java 進行 Excel Slicer 自動化](/cells/english/java/advanced-features/excel-slicer-modifications-java-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}