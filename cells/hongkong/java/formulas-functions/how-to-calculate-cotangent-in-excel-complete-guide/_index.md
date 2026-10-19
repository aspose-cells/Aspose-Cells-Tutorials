---
category: general
date: 2026-06-27
description: 如何在 Excel 中使用公式計算餘切。學習如何設定公式、如何使用 EXPAND，並精通 Excel 動態陣列公式。
draft: false
keywords:
- how to calculate cotangent
- how to set formula
- how to use expand
- excel dynamic array formula
- add expand function
language: zh-hant
og_description: 如何在 Excel 中計算餘切並提供清晰範例。本教學示範如何設定公式、使用 EXPAND 以及運用 Excel 動態陣列公式。
og_title: 如何在 Excel 中計算餘切 – 逐步指南
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: How to calculate cotangent in Excel using formulas. Learn how to set
    formula, how to use EXPAND, and master the excel dynamic array formula.
  headline: How to Calculate Cotangent in Excel – Complete Guide
  type: TechArticle
- description: How to calculate cotangent in Excel using formulas. Learn how to set
    formula, how to use EXPAND, and master the excel dynamic array formula.
  name: How to Calculate Cotangent in Excel – Complete Guide
  steps:
  - name: '**Workbook creation** – `new Workbook()` gives us a fresh Excel file in
      memory.'
    text: '**Workbook creation** – `new Workbook()` gives us a fresh Excel file in
      memory.'
  - name: '**Source data** – We fill `A2:A5` with numbers 1‑4; these values will be
      expanded later.'
    text: '**Source data** – We fill `A2:A5` with numbers 1‑4; these values will be
      expanded later.'
  - name: '**How to set formula** – `setFormula` attaches the `EXPAND` expression
      to `A1`. The function tells Excel to spill a 5‑row‑by‑2‑column block based on
      the source range.'
    text: '**How to set formula** – `setFormula` attaches the `EXPAND` expression
      to `A1`. The function tells Excel to spill a 5‑row‑by‑2‑column block based on
      the source range.'
  - name: '**How to calculate cotangent** – The `COT` call uses `PI()/4` (45°). This
      is the core answer to *how to calculate cotangent* in Excel.'
    text: '**How to calculate cotangent** – The `COT` call uses `PI()/4` (45°). This
      is the core answer to *how to calculate cotangent* in Excel.'
  - name: '**Recalculation** – `wb.calculateFormula()` forces Aspose.Cells to evaluate
      all formulas, just like pressing **F9** in the UI.'
    text: '**Recalculation** – `wb.calculateFormula()` forces Aspose.Cells to evaluate
      all formulas, just like pressing **F9** in the UI.'
  - name: '**Result output** – We loop through the spill range to prove that `EXPAND`
      actually created a dynamic array.'
    text: '**Result output** – We loop through the spill range to prove that `EXPAND`
      actually created a dynamic array.'
  - name: '**Saving** – The final workbook, `CotangentDemo.xlsx`, can be opened in
      Excel to see the formulas live.'
    text: '**Saving** – The final workbook, `CotangentDemo.xlsx`, can be opened in
      Excel to see the formulas live.'
  type: HowTo
tags:
- Excel
- Formulas
- Java
- Aspose.Cells
title: Excel 中如何計算餘切 – 完整指南
url: /zh-hant/java/formulas-functions/how-to-calculate-cotangent-in-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 中計算餘切 – 完整指南

有沒有想過 **如何在 Excel 中計算餘切** 而不必拿出科學計算機？你並不是唯一有此疑問的人。無論你是在建立財務模型、物理工作表，或只是熱衷於三角函數的玩弄，精通 Excel 中的餘切函數都能為你節省大量時間。

在本教程中，我們還將展示如何使用 Java 的 Aspose.Cells 庫以程式方式 **設定公式**，深入探討 **如何使用 EXPAND**，並說明 **excel dynamic array formula** 功能為何重要。完成後，你將擁有一個完整可執行的範例，加入 EXPAND 函數、計算餘切，並輸出結果——全部不到十行程式碼。

## 你將學到什麼

- Excel 的 `COT` 函數語法，以及它為何是取得餘切值最快的方法。  
- 如何透過 Java 程式碼在工作表儲存格上 **設定公式**。  
- 使用 **EXPAND** 處理動態陣列的運作機制。  
- 何時以及如何 **加入 expand function** 到你的活頁簿，以進行溢位範圍計算。  
- 針對 **excel dynamic array formula** 行為的常見陷阱排除技巧。  

> **先決條件：**  
> - Java 8+ 已安裝。  
> - Aspose.Cells for Java（免費試用或授權版）。  
> - 對 Excel 函數有基本了解。  

如果你已具備上述條件，讓我們開始吧。

---

## 如何在 Excel 中計算餘切

`COT` 函數會回傳以弧度提供的角度的餘切值。其語法非常簡單：

```excel
=COT(number)
```

其中 *number* 為弧度制的角度。對於經典的 45° 角（π/4 弧度），結果為 `1`，因為 `cot(π/4) = 1`。

### 為什麼使用 `COT` 而不是手動計算？

你可以寫 `=1/TAN(angle)`，但這會迫使 Excel 評估兩個函數，且當角度是 π 的倍數時會產生除以零的錯誤。`COT` 為內建函數，能處理邊緣情況，且更易讀——尤其在與團隊成員共享工作表時。

---

## 步驟說明：使用 Java 設定公式（How to Set Formula）

以下是一個 **完整、可執行的 Java 程式**，它會建立活頁簿、在儲存格 `B1` 加入 `COT` 公式，並對其求值。我們也會加入 `EXPAND` 函數以示範動態陣列。

```java
import com.aspose.cells.*;

public class CotangentDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.getWorksheets().get(0);
        Cells cells = ws.getCells();

        // 2️⃣ Populate source data for EXPAND (A2:A5)
        for (int i = 0; i < 4; i++) {
            cells.get(i + 1, 0).putValue(i + 1); // A2=1, A3=2, A4=3, A5=4
        }

        // 3️⃣ **How to set formula** – Apply EXPAND to cell A1
        //    EXPAND(source, rows, columns) creates a spill range.
        cells.get("A1").setFormula("=EXPAND(A2:A5,5,2)");

        // 4️⃣ **How to calculate cotangent** – Apply COT to cell B1
        //    COT(PI()/4) = 1 because cot(45°) = 1
        cells.get("B1").setFormula("=COT(PI()/4)");

        // 5️⃣ Recalculate the workbook so formulas resolve
        wb.calculateFormula();

        // 6️⃣ Retrieve and print results
        System.out.println("EXPAND result (A1 spill range):");
        for (int r = 0; r < 5; r++) {
            for (int c = 0; c < 2; c++) {
                System.out.print(cells.get(r, c).getStringValue() + "\t");
            }
            System.out.println();
        }

        System.out.println("\nCotangent of π/4 (B1): " + cells.get("B1").getStringValue());

        // 7️⃣ Save the workbook (optional)
        wb.save("CotangentDemo.xlsx");
    }
}
```

#### 程式碼說明

1. **Workbook creation** – `new Workbook()` 為我們在記憶體中建立一個全新的 Excel 檔案。  
2. **Source data** – 我們在 `A2:A5` 填入 1‑4 的數字；這些值稍後會被展開。  
3. **How to set formula** – `setFormula` 將 `EXPAND` 表達式附加到 `A1`。此函數告訴 Excel 依據來源範圍溢位成一個 5 列 2 欄的區塊。  
4. **How to calculate cotangent** – `COT` 呼叫使用 `PI()/4`（45°）。這就是在 Excel 中 *如何計算餘切* 的核心答案。  
5. **Recalculation** – `wb.calculateFormula()` 強制 Aspose.Cells 評估所有公式，就像在介面上按下 **F9** 一樣。  
6. **Result output** – 我們遍歷溢位範圍，以證明 `EXPAND` 確實建立了動態陣列。  
7. **Saving** – 最終的活頁簿 `CotangentDemo.xlsx` 可在 Excel 中開啟，查看即時公式。  

> **專業提示：** 如果你使用支援動態陣列的 Excel 版本（Office 365 或 Excel 2021+），`EXPAND` 函數會自動「溢位」到相鄰儲存格。舊版會回傳 `#NAME?` 錯誤——因此在 **add expand function** 時務必檢查你的 Excel 版本。

## 如何使用 EXPAND – 了解 Excel 動態陣列公式

`EXPAND` 是 Excel **dynamic array** 系列的一部分，旨在取代繁瑣的手動範圍定義。其語法如下：

```excel
=EXPAND(array, rows, columns, [pad_with])
```

- **array** – 你想要展開的來源範圍。  
- **rows** – 溢位範圍的列數（使用 `0` 保持原始高度）。  
- **columns** – 溢位範圍的欄數（使用 `0` 保持原始寬度）。  
- **pad_with** – 用於填充空白儲存格的可選值。  

當你寫 `=EXPAND(A2:A5,5,2)` 時，Excel 會讀取四列的欄位，並將其展開成 5×2 的矩陣，預設以 `0` 填充額外的儲存格。結果會「溢位」到相鄰儲存格，行為類似 **excel dynamic array formula**。

### 何時加入 EXPAND 函數

- **Data normalization** – 你只有單一欄位，但需要矩陣來製作圖表。  
- **Pre‑processing for other array functions** – 如 `FILTER` 或 `SORT` 等函數可直接接受溢位範圍。  
- **Avoiding manual copy‑down** – 動態陣列會在來源資料變更時自動調整。  

## 常見陷阱與解決方法

| 問題 | 為何會發生 | 解決方式 |
|-------|----------------|-----|
| `#SPILL!` 錯誤 | 目標儲存格已包含資料 | 清除該區域或將公式移至空白儲存格。 |
| `#NAME?` 在 `EXPAND` 上 | Excel 版本不支援動態陣列 | 升級至 Office 365/Excel 2021，或使用如 `INDEX` 的備用方案。 |
| `#DIV/0!` 來自 `COT` | 角度等於 `0` 或 `π`（餘切未定義） | 將公式包裹起來：`=IF(MOD(angle,PI())=0,NA(),COT(angle))`。 |
| Java 中公式未更新 | `Workbook.calculateFormula()` 未被呼叫 | 確保在設定所有公式後呼叫 `calculateFormula()`。 |

## 擴充範例 – 更多計算餘切的方法

如果你需要 *度數* 的餘切值，請先將其轉換：

```java
cells.get("C1").setFormula("=COT(RADIANS(30))"); // cot(30°) ≈ 1.732
```

或者，將 `COT` 與其他陣列函數結合：

```excel
=MAP(A2:A5, LAMBDA(x, COT(RADIANS(x))))
```

`MAP` 函數（在較新版本的 Excel 中可用）會將 `COT` 套用至範圍的每個元素，回傳餘切值的動態陣列——非常適合批次計算。

## 完整範例回顧

以下是你可以直接複製貼上到 IDE 的 **完整原始檔案**。沒有隱藏的相依性，所有需要的內容都在此。



## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在本篇示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何使用 Excel IF 函數](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)
- [如何使用 Aspose.Cells for Java 設定 Excel 文件版本](/cells/english/java/workbook-operations/set-excel-version-aspose-cells-java/)
- [如何使用 Aspose.Cells .NET 為 Excel 檔案設定語言以支援多語言](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}