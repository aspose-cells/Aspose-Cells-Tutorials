---
category: general
date: 2026-06-08
description: 使用 Java 程式化建立 Excel。學習如何寫入數值、設定小數位，並使用 Aspose.Cells 儲存工作簿 Excel 檔案。
draft: false
keywords:
- create excel programmatically
- write numeric value
- save workbook excel
- save excel file
- how to set digits
language: zh-hant
og_description: 在 Java 中以程式方式建立 Excel。本指南說明如何寫入數值、控制小數位精度，以及儲存 Excel 檔案。
og_title: 以程式方式建立 Excel – 完整 Java 教學
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel programmatically with Java. Learn how to write numeric
    value, set digits, and save workbook Excel file using Aspose.Cells.
  headline: Create Excel programmatically in Java – Step‑by‑Step Guide
  type: TechArticle
- questions:
  - answer: Create a separate `ExportTableOptions` instance for each cell and assign
      it individually.
    question: What if I need more than one cell with different digit settings?
  - answer: Yes—use `Range.getExportTableOptions().set(exportOptions)` on a `Range`
      object that spans multiple cells.
    question: Can I apply the same setting to an entire range?
  - answer: No. The raw double (`12345.6789`) stays unchanged; only the visual representation
      is limited to the specified significant digits.
    question: Does this affect the underlying value?
  - answer: Aspose.Cells supports both `.xlsx` and `.xls`. Just change the file extension
      in `workbook.save()` and the library handles the conversion automatically.
    question: What about older Excel formats (`.xls`)?
  type: FAQPage
tags:
- Java
- Excel
- Aspose.Cells
title: 在 Java 中以程式方式建立 Excel – 步驟指南
url: /zh-hant/java/spreadsheet-automation/create-excel-programmatically-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中以程式方式建立 Excel – 完整指南

有沒有曾經需要**以程式方式建立 Excel**，卻不知從何入手？依我的經驗，最大的障礙是弄清楚如何*寫入數值*，以取得所需的精確度，同時仍能**儲存工作簿 Excel**檔案而不出問題。  

在本教學中，我們將逐步示範一個真實案例，說明**如何設定位數**、將數字寫入儲存格，最後**將 Excel 檔案**儲存至磁碟——全部使用 Aspose.Cells for Java 函式庫。沒有冗贅，只有可直接複製貼上的可運作解決方案。

## 前置條件

- Java 8 或更新版本（程式碼同樣適用於 Java 11+）  
- Maven 或 Gradle 以取得 Aspose.Cells 相依性  
- 基本了解 Java 語法（只要會寫 `main` 方法即可）  

> *專業提示:* 若您尚未擁有授權，可先使用 Aspose.Cells 的免費評估版——對以下範例而言功能完整。

## 步驟 1：設定專案並匯入 Aspose.Cells

首先，將 Aspose.Cells 的 Maven 套件加入 `pom.xml`。如果您偏好 Gradle，亦可使用相同的座標。

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

相依性解決後，您即可在 Java 檔案中匯入所需的類別：

```java
import com.aspose.cells.*;
```

## 步驟 2：建立新 Workbook – **create excel programmatically** 的核心

現在我們真的**以程式方式建立 Excel**。`Workbook` 物件代表整個試算表檔案。

```java
// Step 2: Instantiate a new workbook (blank Excel file)
Workbook workbook = new Workbook();
```

那一行程式碼為您提供一個乾淨的畫布——可視為一個待填寫的空白 Excel 檔案。

## 步驟 3：存取第一個工作表

每個 workbook 預設至少包含一個工作表。取得它以便開始寫入資料。

```java
// Step 3: Grab the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

您也可以建立其他工作表，但在此示範中預設工作表已足夠。

## 步驟 4：**寫入數值** 並以受控精度

這裡就是魔法發生的地方。我們會將數字寫入儲存格 **A1**，然後告訴 Aspose.Cells **how to set digits**——具體而言，我們希望匯出檔案時僅顯示四個有效位數。

```java
// Step 4: Put a numeric value into cell A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue(12345.6789); // raw value with many decimals
```

### 定義匯出選項 – **how to set digits**

Aspose.Cells 允許透過 `ExportTableOptions` 來控制有效位數。將其設定為 `4` 表示匯出的 Excel 會顯示 `1.235E+04`（或等效的四捨五入值），同時保留底層資料不變。

```java
// Step 5: Create export options to keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setSignificantDigits(4);

// Apply the options to the cell
cell.getExportTableOptions().set(exportOptions);
```

> **為何使用 `ExportTableOptions`？**  
> 它在記憶體中保留原始數值精度，同時強制視覺呈現遵守您指定的位數限制——對於需要一致四捨五入且不失真資料的報告而言相當理想。

## 步驟 5：**儲存 workbook Excel** – 拼圖的最後一塊

資料與格式設定完成後，就該**將 Excel 檔案**儲存至磁碟。選擇任意目錄即可；只要確保應用程式具備寫入權限。

```java
// Step 6: Save the workbook with the configured options
String outputPath = "significant-digits.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

執行程式後會在工作目錄產生 `significant-digits.xlsx`。在 Microsoft Excel 中開啟，即可看到 **A1** 的數字僅顯示四個有效位數。

## 完整可執行範例

將所有步驟整合起來，以下是一個可即時編譯執行的獨立類別：

```java
import com.aspose.cells.*;

public class ExcelProgrammaticDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Write a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(12345.6789);

        // 4️⃣ Define export options – keep only 4 significant digits
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setSignificantDigits(4);
        cell.getExportTableOptions().set(exportOptions);

        // 5️⃣ Save the workbook (this is how we **save workbook Excel**)
        String filePath = "significant-digits.xlsx";
        workbook.save(filePath);
        System.out.println("Excel file created: " + filePath);
    }
}
```

### 預期輸出

執行程式時，主控台會印出：

```
Excel file created: significant-digits.xlsx
```

開啟 `significant-digits.xlsx` 後會看到 **A1** 包含 `1.235E+04`（或根據 Excel 顯示設定的 `1235`），證實 **how to set digits** 選項如預期運作。

## 常見問題與邊緣案例

- **如果我需要多個儲存格使用不同的位數設定怎麼辦？**  
  為每個儲存格建立獨立的 `ExportTableOptions` 實例，並分別指派。

- **我可以將相同設定套用到整個範圍嗎？**  
  可以——對跨多個儲存格的 `Range` 物件使用 `Range.getExportTableOptions().set(exportOptions)`。

- **這會影響底層數值嗎？**  
  不會。原始的 double (`12345.6789`) 保持不變；僅視覺呈現受到指定的有效位數限制。

- **舊版 Excel 格式（`.xls`）呢？**  
  Aspose.Cells 同時支援 `.xlsx` 與 `.xls`。只要在 `workbook.save()` 中更改副檔名，函式庫會自動處理轉換。

## 往後的步驟

既然您已掌握如何**以程式方式建立 Excel**、**寫入數值**，以及**以精確位數儲存 workbook Excel**，接下來可以探索：

- 新增 **樣式** 與 **條件格式** 以突顯重要數字。  
- 將工作簿匯出為 **PDF** 或 **CSV** 供報表流程使用。  
- 使用 **自動調整** 與 **欄寬** 設定，使最終檔案更為精緻。

上述主題皆建立在此基礎之上，歡迎自行實驗與擴充程式碼。

---

![以程式方式建立的 Excel 工作簿](https://example.com/images/create-excel-programmatically.png "以程式方式建立 Excel")

*圖片說明:* 以程式方式建立 Excel – Java 範例展示已填寫的試算表

**恭喜！** 您剛剛掌握了在 Java 中**以程式方式建立 Excel**的關鍵步驟，從插入數值、控制位數精度，到最後**儲存 Excel 檔案**。持續玩弄 API——還有整個試算表自動化的世界等著您。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在此處示範的技巧之上。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在自己的專案中探索其他實作方式。

- [如何使用 Aspose.Cells for Java 建立並儲存 Excel 工作簿為 SVG](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [如何使用 Aspose.Cells Java 建立並匯出 Excel 為 HTML | 工作簿操作指南](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [如何使用 Aspose.Cells 在 Java 中建立 Excel 檔案並套用樣式](/cells/english/java/advanced-features/excel-master-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}