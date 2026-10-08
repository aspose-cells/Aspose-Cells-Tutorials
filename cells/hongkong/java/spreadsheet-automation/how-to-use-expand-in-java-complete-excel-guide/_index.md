---
category: general
date: 2026-06-21
description: 學習如何在 Java 中使用 expand 將陣列展開為多列、編寫 Excel 公式程式碼，以及以 Java 風格儲存 Excel 檔案——一次教學搞掂。
draft: false
keywords:
- how to use expand
- expand array to rows
- write excel formula code
- save excel file java
language: zh-hant
og_description: 如何在 Java 中使用 expand 操作 Excel 資料、將陣列展開為列、編寫 Excel 公式程式碼，並以 Java 方式儲存
  Excel 檔案。
og_title: 如何在 Java 中使用 Expand – 完整 Excel 指南
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to use expand in Java to expand array to rows, write Excel
    formula code, and save Excel file Java style—all in a single tutorial.
  headline: How to Use Expand in Java – Complete Excel Guide
  type: TechArticle
- description: Learn how to use expand in Java to expand array to rows, write Excel
    formula code, and save Excel file Java style—all in a single tutorial.
  name: How to Use Expand in Java – Complete Excel Guide
  steps:
  - name: Why This Works
    text: '- **`Workbook`**: Represents the entire Excel file. Creating a new one
      gives you a clean canvas; loading an existing file lets you augment a pre‑existing
      template. - **`Worksheet`**: Think of it as a single tab. We grab the first
      one because that’s where we’ll demonstrate the formula. - **`setFormul'
  - name: Real‑World Use Cases
    text: '| Scenario | How EXPAND Helps | |----------|------------------| | Generating
      a month‑long schedule from a short list of tasks | `=EXPAND(taskList,30)` |
      | Padding a matrix for a statistical model | `=EXPAND(matrix,10,10,0)` | | Creating
      placeholder rows for user input | `=EXPAND({""},20)` |'
  - name: Expected Output
    text: 'When you open `output.xlsx`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Formulas
title: 如何在 Java 中使用 Expand – 完整 Excel 指南
url: /zh-hant/java/spreadsheet-automation/how-to-use-expand-in-java-complete-excel-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 EXPAND – 完整 Excel 指南

有沒有想過在使用 Java 自動化 Excel 時 **如何使用 EXPAND**？你並非唯一有此疑問——開發者常常詢問如何在不寫無盡迴圈的情況下將陣列展開為列。好消息是，你只需要一個公式就能做到，而將該公式寫入活頁簿的 Java 程式碼出奇地簡短。

在本教學中，我們將逐步示範一個實務範例，說明如何使用 EXPAND、如何在 Java 中撰寫 Excel 公式程式碼，以及如何以 Java 方式儲存 Excel 檔案，讓你能即時檢視結果。完成後，你將擁有一個可執行的程式，能載入既有活頁簿、將 `EXPAND` 函式寫入儲存格，並將檔案寫回磁碟。

## 前置條件

在開始之前，請確保你已具備：

- 已安裝 Java 17（或任何較新的 JDK）。
- 使用 Maven 或 Gradle 來管理相依性。
- **Aspose.Cells for Java** 函式庫（從 Java 操作 Excel 最簡單的方式）。可從 Maven Central 取得：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest -->
</dependency>
```

不需要額外安裝 Excel；函式庫會在內部處理檔案格式。若偏好 Gradle，只需相應替換相依性區塊即可。

既然基礎已備妥，讓我們開始動手實作吧。

## 如何在 Java 中使用 EXPAND

`EXPAND` 函式是 Excel 動態陣列家族的一員。它接受來源陣列，並將其展開至指定大小，預設以 `#N/A` 填滿空白儲存格。在本例中，我們會提供一個簡單的一維陣列 `{1,2,3}`，並要求 Excel 展開為 **5 列**。

```java
// Import statements
import com.aspose.cells.*;

public class ExpandDemo {
    public static void main(String[] args) {
        try {
            // 1️⃣ Load or create a workbook
            Workbook wb = new Workbook(); // creates a blank workbook
            // Optionally, load an existing file:
            // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Get the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // 3️⃣ Apply the EXPAND function in cell A1
            // This is where we **write excel formula code** from Java.
            ws.getCells().get("A1").setFormula("=EXPAND({1,2,3},5)");

            // 4️⃣ Save the workbook — **save excel file java** style.
            wb.save("YOUR_DIRECTORY/output.xlsx");
            System.out.println("Workbook saved successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 為什麼這樣可行

- **`Workbook`**：代表整個 Excel 檔案。建立新檔案可得到乾淨的畫布；載入既有檔案則可在現有範本上增添內容。
- **`Worksheet`**：可視為單一工作表分頁。我們取得第一個分頁，因為要在此示範公式。
- **`setFormula`**：此方法以字串形式注入任何有效的 Excel 公式。此處我們傳入 `EXPAND` 函式，告訴 Excel **將陣列展開為列**（若指定亦可展開為欄）。
- **`save`**：將變更寫入磁碟。這就是 **save excel file java** 的步驟，確保之後能在 Excel 或其他檢視器中開啟檔案。

執行程式後，開啟 `output.xlsx`，你會看到 A 欄被填入 `1, 2, 3, #N/A, #N/A`。將 `EXPAND` 的第二個參數改為 `3`，則只會得到三列——非常適合動態報表。

## 使用 EXPAND 函式將陣列展開為列

如果你習慣手動迴圈逐列寫入，`EXPAND` 函式可以取代這些樣板程式碼。以下是語法的快速說明：

```
EXPAND(source, rows, columns, fill)
```

- **source** – 想要展開的陣列。例如本例的 `{1,2,3}`。
- **rows** – 目標列數。我們使用 `5`。
- **columns** – 可選，預設為來源的欄數。
- **fill** – 空白儲存格的填充值（預設為 `#N/A`）。

### 真實案例應用

| 情境 | EXPAND 的幫助方式 |
|------|-------------------|
| 從短任務清單產生整月排程 | `=EXPAND(taskList,30)` |
| 為統計模型的矩陣補齊 | `=EXPAND(matrix,10,10,0)` |
| 為使用者輸入建立佔位列 | `=EXPAND({""},20)` |

讓 Excel 承擔繁重的運算，你的 Java 程式碼即可保持簡潔，避免不必要的迴圈。

## 在 Java 中撰寫 Excel 公式程式碼

你可能會想，「能否動態組合公式字串？」答案是肯定的。以下程式碼示範如何根據變數組合 `EXPAND` 呼叫：

```java
int[] numbers = {4, 5, 6};
int targetRows = 7;

// Convert int array to Excel‑style literal: {4,5,6}
StringBuilder sb = new StringBuilder("{");
for (int i = 0; i < numbers.length; i++) {
    sb.append(numbers[i]);
    if (i < numbers.length - 1) sb.append(",");
}
sb.append("}");

String formula = String.format("=EXPAND(%s,%d)", sb.toString(), targetRows);
ws.getCells().get("B2").setFormula(formula);
```

請注意，我們是以程式方式 **write excel formula code**，再將其寫入儲存格 `B2`。當需要即時產生公式（例如從資料庫抓取資料並產生動態報表）時，此作法相當具擴充性。

## 儲存 Excel 檔案（Java） – 持久化變更

將活頁簿儲存下來是最後一步。Aspose.Cells 提供了以下幾種方式：

- **`wb.save("path.xlsx")`** – 以預設的 XLSX 格式儲存。
- **`wb.save("path.xls", SaveFormat.EXCEL_97_TO_2003)`** – 用於舊版相容性。
- **`wb.save(outputStream, SaveFormat.XLSX)`** – 當需要以串流方式輸出檔案時（例如在 Web 應用程式中）。

以下範例將資料寫入 `ByteArrayOutputStream`，讓你可以從 REST 端點回傳位元組：

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
wb.save(baos, SaveFormat.XLSX);
byte[] excelBytes = baos.toByteArray();
// Now you can send `excelBytes` as a response payload.
```

這就是許多企業服務依賴的 **save excel file java** 模式。

## 常見陷阱與專業技巧

- **Formula Evaluation Timing** – Aspose.Cells 在 `save` 時**不會**自動計算公式。若需要計算結果，請在儲存前呼叫 `wb.calculateFormula()`。
- **Dynamic Array Support** – `EXPAND` 僅在 Excel 365 / 2021 以上版本提供。若在較舊版本開啟會顯示 `#NAME?`。若必須支援舊版客戶端，請考慮改用手動展開。
- **Locale Issues** – 無論活頁簿語系為何，都請使用英文函式名稱（`EXPAND`）；Aspose.Cells 依照英文語法解析。
- **Large Arrays** – 展開至數千列會增加檔案大小。請留意記憶體使用情況，必要時改用串流方式處理大型資料集。

## 完整範例程式

以下是完整、可直接貼到 IDE 中執行的程式碼，包含所有匯入、錯誤處理與說明註解。

```java
import com.aspose.cells.*;

public class ExpandDemoFull {
    public static void main(String[] args) {
        // Adjust these paths as needed
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/output.xlsx";

        try {
            // Step 1: Load an existing workbook or create a new one
            Workbook wb;
            if (new java.io.File(inputPath).exists()) {
                wb = new Workbook(inputPath);
                System.out.println("Loaded existing workbook.");
            } else {
                wb = new Workbook(); // brand‑new workbook
                System.out.println("Created a new workbook.");
            }

            // Step 2: Access the first worksheet
            Worksheet ws = wb.getWorksheets().get(0);

            // Step 3: Build a dynamic EXPAND formula (expand array to rows)
            int[] sourceArray = {1, 2, 3};
            int rowsDesired = 5;

            // Convert Java array to Excel literal syntax
            StringBuilder literal = new StringBuilder("{");
            for (int i = 0; i < sourceArray.length; i++) {
                literal.append(sourceArray[i]);
                if (i < sourceArray.length - 1) literal.append(",");
            }
            literal.append("}");

            String formula = String.format("=EXPAND(%s,%d)", literal, rowsDesired);
            ws.getCells().get("A1").setFormula(formula);
            System.out.println("Inserted formula: " + formula);

            // Optional: force calculation so the file contains values, not just formulas
            wb.calculateFormula();

            // Step 4: Save the workbook – **save excel file java** style
            wb.save(outputPath);
            System.out.println("Workbook saved to " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error occurred: " + ex.getMessage());
            ex.printStackTrace();
        }
    }
}
```

### 預期輸出

開啟 `output.xlsx` 後：

| A   |
|-----|
| 1   |
| 2   |
| 3   |
| #N/A |
| #N/A |

若將 `rowsDesired` 改為 `3`，則欄位只會顯示到第三列。`#N/A` 佔位符是 Excel 表示「此處無資料」的方式——你可以透過傳入 `EXPAND` 的第四個參數來替換它，例如 `=EXPAND({1,`（此處原文截斷）。

## 接下來該學什麼？

以下教學與本指南所示技巧緊密相關，提供完整的程式範例與逐步說明，協助你精通更多 API 功能，並在自己的專案中探索替代實作方式。

- [如何使用 Aspose.Cells for Java 在 Excel 活頁簿中插入列](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [如何使用 Aspose.Cells for Java 刪除 Excel 列 | 指南與教學](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells Java 以各種格式儲存 Excel 檔案](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}