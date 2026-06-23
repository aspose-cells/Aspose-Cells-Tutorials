---
date: 2026-01-24
description: 學習如何使用 IF 函數與 Aspose.Cells for Java 在 Excel 中計算成績。一步一步的指南，教您建立條件公式並在
  Excel 中套用條件邏輯。
linktitle: Calculate Grades Excel with IF Function
second_title: Aspose.Cells Java Excel Processing API
title: 使用 Aspose.Cells 的 IF 函數計算 Excel 成績
url: /zh-hant/java/basic-excel-functions/how-to-use-excel-if-function/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 計算 Excel 成績（IF 函數）

## 介紹

如果您需要 **快速且可靠地計算 Excel您的首選工具。結合 **Aspose.Cells for Java**，您可以在程式中產生、修改並儲存試算表，根本** 建立條件公式、巢狀 IF 陳述式，並以 Excel 方式套用條件邏輯——全部透過，無需安裝 Microsoft Office。  
- **我可以計算多少筆成績？** 無限制，只要將公式向下複製即可。  
- **需要授權嗎？** 開發階段可使用免費試用版；正式上線需購買商業授權。  
- **可以巢狀 IF 陳述式嗎？** 可以——您可以嵌入多個 IF 以處理複雜的成績等級。

## 什麼是「計算 Excel 成績」？
計算 Excel 成績是指在工作表內直接套用一組條件規則（例如，分數 ≥ 90 → 「A」），使用 IF 函數即可自動化此邏輯，讓每筆新分數即時得到正確的等級。

## 為什麼使用 Aspose.Cells for Java？
- **伺服器端處理** – 無需安裝 Excel。  
- **完整公式支援** – 所有 Excel 函數，包括巢狀 IF，皆可直接使用。  
- **高效能** – 能快速處理大型活頁簿。  
- **跨平台** – 可在任何相容 JVM 的環境執行。

## 前置條件

開始之前，請確保已具備以下條件：

- **Aspose.Cells for Java** – 必須將此函式庫加入 classpath。可從 [here](https://releases.aspose.com/cells/java/) 下載並 **安裝 Aspose.Cells**。  
- Java Development Kit (JDK) 8 或更新版本。  
- Java IDE 或建置工具（Maven/Gradle）以管理相依性。

## 第一步：設定 Java 專案

建立一個新的 Java 專案（或開啟既有專案），並將 Aspose.Cells 的 JAR 檔加入專案的 classpath。

## 第二步：匯入必要類別

在 Java 程式碼中，匯入 Aspose.Cells 函式庫的核心類別。

```java
import com.aspose.cells.*;
```

## 第三步：建立 Excel 活頁簿

接下來，我們會建立一個全新的活頁簿，新增工作表，並填入範例分數。

```java
// Create a new Workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);

// Add data to the worksheet
worksheet.getCells().get("A1").putValue("Score");
worksheet.getCells().get("A2").putValue(85);
worksheet.getCells().get("A3").putValue(60);
worksheet.getCells().get("A4").putValue(45);
```

## 第四步：使用 Excel魔法發述式** 依分數指派等級。

```java
// Apply the IF function to calculate grades
Cell cell = worksheet.getCells().get("B2");
cell.setFormula("=IF(A2>=90, \"A\", IF(A2>=80, \"B\", IF(A2>=70, \"C\", IF(A2>=60, \"D\", \"F\"))))");
```

公式說明：

- 若分數 ≥ 90 → 「A」  
- 否則若 ≥ 80 → 「B」  
- 否則若 ≥ 70 → 「C」  
- 否則若 ≥ 60 → 「D」  
- 其他情況 → 「F」

## 第五步：為所有分數計算等級

不必為每一列手動輸入公式，只要向下複製即可。這示範了 **以程式方式套用 Excel 條件邏輯**。

```java
// Copy the formula down to calculate grades for other scores
worksheet.getCells().copyRow(worksheet.getCells().getRows().get("2"), worksheet.getCells().getRows().get("3"), new CopyOptions());
worksheet.getCells().copyRow(worksheet.getCells().getRows().get("2"), worksheet.getCells().getRows().get("4"), new CopyOptions());
```

## 第六步：儲存 Excel 檔案

最後，將活頁簿寫入磁碟（或串流），即可在 Excel 中開啟並檢視結果。

```java
// Save the workbook to a file
workbook.save("Grades.xlsx");
```

## 常見使用情境與技巧

- **批次評分** – 匯入學生分數清單、套用巢狀 IF 公式，然後匯出已評分的報表。  
- **動態門檻** – 將硬編碼的數值（90、80、…）改為儲存格參照，讓使用者可在不修改程式碼的情況下調整成績標準。  
- **專業提示**：在設定公式後若需要立即取得計算結果，可呼叫 `worksheet.calculateFormula()`。

## 常見問題

### 如何安裝 Aspose.Cells for Java？

前往 [here](https://releases.aspose.com/cells/java/) 下載函式庫，並將 JAR 檔加入專案的 classpath。

### 可以在 Excel IF 函數中使用複雜條件嗎？

可以。您可以 **以 Excel 方式巢狀 IF 陳述式** 處理多重條件，就如同上述範例。Aspose.Cells 完全支援此類巢狀公式。

### Aspose.Cells for Java 有授權需求嗎？

Aspose.Cells for Java 為商業產品。提供免費評估授權供開發測試使用，正式上線則需購買付費授權。

### 能否將 IF 函數套用於整個儲存格範圍？

當然可以。使用相對參照（例如 `A2`）並向下複製公式，即可自動將 IF 函數套用至整欄儲存格。

### Aspose.Cells for Java 適合企業級應用嗎？

適合。它具備高效能、完整功能覆蓋與可靠支援，無論是小工具還是大型企業解決方案皆能勝任。

---

**最後更新日期：** 2026-01-24  
**測試環境：** Aspose.Cells for Java 24.12  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}