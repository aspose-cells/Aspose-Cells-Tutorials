---
category: general
date: 2026-10-07
description: 學習如何將 JSON 載入 Excel，並使用 Aspose.Cells 從 JSON 產生 XLSX。此一步一步的指南亦會示範如何從 JSON
  填充 Excel，並將工作簿儲存為 XLSX。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- load json into excel
- generate xlsx from json
- populate excel from json
- save workbook as xlsx
- create workbook from json
language: zh-hant
lastmod: 2026-10-07
og_description: 使用 Aspose.Cells for Java 將 JSON 載入 Excel，並從 JSON 生成 XLSX。請參考本指南，將
  JSON 填入 Excel，並將工作簿儲存為 XLSX。
og_image_alt: Screenshot of an Excel workbook that was loaded with JSON data using
  Aspose.Cells
og_title: 使用 Aspose.Cells 將 JSON 載入 Excel – 完整 Java 教學
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  headline: How to load JSON into Excel with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to load JSON into Excel and generate XLSX from JSON using
    Aspose.Cells. This step‑by‑step guide also shows how to populate Excel from JSON
    and save workbook as XLSX.
  name: How to load JSON into Excel with Aspose.Cells for Java
  steps:
  - name: 'Compile the program:'
    text: 'Compile the program:'
  - name: 'Run it:'
    text: 'Run it:'
  - name: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
    text: Verify that `JsonSingleCell.xlsx` appears in the working directory and opens
      without errors.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何使用 Aspose.Cells for Java 將 JSON 載入 Excel
url: /zh-hant/java/excel-import-export/how-to-load-json-into-excel-with-aspose-cells-for-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將 JSON 載入 Excel（使用 Aspose.Cells for Java）

如果您需要 **將 JSON 載入 Excel**，本教學將示範使用 Aspose.Cells for Java 的可靠方法。您將會看到如何從 JSON 產生 XLSX、從 JSON 填充 Excel，最後 **將工作簿儲存為 XLSX**——全部在一個獨立的程式中完成。

在試算表中處理 JSON 很常見，尤其是從 Web 服務、API 或 NoSQL 資料庫匯出資料時。完成本指南後，您將擁有一個可直接執行的 Java 類別，能從 JSON 建立工作簿並將結果寫入磁碟檔案。

## 前置條件

* Java 8 或更新版本已安裝（程式碼使用標準 Java 功能）。
* Aspose.Cells for Java 函式庫（版本 23.10 或更新）。您可從 [Aspose website](https://downloads.aspose.com/cells/java) 或 Maven Central 取得。
* 一個 IDE 或簡易文字編輯器，以及用於編譯與執行 Java 程式的終端機。
* 具備 JSON 語法與 Excel 概念的基本認識。

> **專業提示：** 若您使用 Maven，請將以下相依性加入 `pom.xml`，以避免手動管理 JAR：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

## 步驟 1：設定專案並匯入所需類別

建立一個名為 `JsonToExcelDemo` 的新 Java 類別。匯入在建立工作簿、處理工作表以及 Smart Marker 處理時所需的 Aspose.Cells 類別。

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // The full implementation starts in the next step.
    }
}
```

*此步驟重要原因：* 匯入正確的類別可確保編譯器能找到 Aspose.Cells API。`Workbook` 類別代表 Excel 檔案，而 `SmartMarkerProcessor` 則負責 JSON 轉 Excel 的轉換。

## 步驟 2：定義將載入 Excel 的 JSON 來源

本範例使用包含兩個物件的小型 JSON 陣列。在實際情況下，您可以從檔案、REST 端點或資料庫讀取 JSON。

```java
// Step 2: Define the JSON data that will be used as the smart‑marker source
String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";
```

*此步驟重要原因：* JSON 字串是 **從 JSON 填充 Excel** 操作的資料來源。將 JSON 保存在 `String` 變數中，可輕鬆傳遞給 `SmartMarkerProcessor`。

## 步驟 3：建立新工作簿並取得第一個工作表

全新的工作簿提供乾淨的起點。第一個工作表（索引 0）將放置 Smart Marker。

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();               // creates an empty XLSX workbook
Worksheet worksheet = workbook.getWorksheets().get(0);
```

*此步驟重要原因：* Aspose.Cells 使用 `Workbook` 物件，之後可儲存為 XLSX 檔案。存取第一個 `Worksheet` 讓我們能在已知的儲存格位置放置標記。

## 步驟 4：插入 Smart Marker，告訴 Aspose.Cells 如何處理 JSON

Smart Marker 是佔位符，Aspose.Cells 會以來源資料取代它。標記 `&=JSONData.ArrayAsSingle` 指示函式庫將整個 JSON 陣列視為單一儲存格值。

```java
// Step 4: Insert a smart‑marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");
```

*此步驟重要原因：* 使用 `ArrayAsSingle` 可避免預設將每個陣列元素展開為獨立列的行為。當您希望 JSON 文字原樣顯示於儲存格，或之後使用公式拆分時，這很有用。

## 步驟 5：以 JSON 資料來源設定 SmartMarkerProcessor

現在將 JSON 字串綁定至邏輯名稱 `JSONData`。處理器會以實際資料取代標記。

```java
// Step 5: Configure the SmartMarkerProcessor with the JSON data source
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
processor.setDataSource("JSONData", jsonData);
processor.process();   // expands the marker and writes JSON into the worksheet
```

*此步驟重要原因：* `setDataSource` 將標記中使用的名稱（`JSONData`）與實際的 JSON 負載連結。`process()` 承擔主要工作：解析 JSON、套用標記邏輯，並將結果寫入工作表。

## 步驟 6：將產生的工作簿儲存為 XLSX 檔案

最後，將工作簿寫入磁碟。`SaveFormat.XLSX` 常數確保使用正確的 Office Open XML 格式。

```java
// Step 6: Save the resulting workbook
String outputPath = "JsonSingleCell.xlsx";   // adjust the path as needed
workbook.save(outputPath, SaveFormat.XLSX);
System.out.println("Workbook saved to " + outputPath);
```

*此步驟重要原因：* 儲存檔案完成 **從 JSON 產生 XLSX** 工作流程。產生的檔案可在 Excel、LibreOffice 或任何支援 XLSX 的試算表程式中開啟。

### 完整原始碼

將所有部件組合起來，以下是完整且可執行的程式，能 **從 JSON 建立工作簿**、**從 JSON 填充 Excel**，以及 **將工作簿儲存為 XLSX**。

```java
package com.example.exceljson;

import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerProcessor;
import com.aspose.cells.SaveFormat;

public class JsonToExcelDemo {
    public static void main(String[] args) throws Exception {
        // 1. JSON source – replace with your own data if needed
        String jsonData = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":25}]";

        // 2. Create a fresh workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3. Place a smart‑marker that treats the JSON array as a single cell
        worksheet.getCells().putValue(0, 0, "&=JSONData.ArrayAsSingle");

        // 4. Bind the JSON string to the marker name and process it
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
        processor.setDataSource("JSONData", jsonData);
        processor.process();

        // 5. Save the workbook as an XLSX file
        String outputPath = "JsonSingleCell.xlsx";
        workbook.save(outputPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

### 預期結果

當您開啟 `JsonSingleCell.xlsx` 時，會看到 JSON 陣列在儲存格 **A1** 中完整顯示，與原始字串相同：

```
[{"Name":"John","Age":30},{"Name":"Anna","Age":25}]
```

如果您希望每個物件位於不同列，請將標記改為 `&=JSONData`（不含 `.ArrayAsSingle`）。處理器將把陣列展開為個別列，示範另一種 **從 JSON 填充 Excel** 的技巧。

## 常見變化與邊緣情況

| 情況 | 調整方式 |
|-----------|------------|
| **大型 JSON 載荷（> 10 MB）** | 增加 JVM 堆積大小（`-Xmx2g`），並考慮以串流方式處理 JSON，以避免 `OutOfMemoryError`。 |
| **巢狀物件** | 在表格內使用階層式標記，如 `&=JSONData.Name` 與 `&=JSONData.Age`，將每個屬性對映至欄位。 |
| **JSON 檔案而非字串** | 使用 `java.nio.file.Files.readString(Path.of("data.json"))` 讀取檔案為 `String`，再傳遞給 `setDataSource`。 |
| **需要保留原始 JSON 格式** | 保留 `.ArrayAsSingle` 後綴，或在 JSON 外層加上 CDATA，若您之後打算使用 Excel 公式解析 JSON。 |
| **多個工作表** | 建立額外工作表（`workbook.getWorksheets().add("Sheet2")`），並在每張工作表上重複插入標記。 |

> **警告：** Smart Marker 区分大小寫。請確保邏輯名稱（`JSONData`）在標記與 `setDataSource` 之間完全相符。

## 測試解決方案

1. 編譯程式：

   ```bash
   javac -cp ".:aspose-cells-23.10.jar" com/example/exceljson/JsonToExcelDemo.java
   ```

2. 執行程式：

   ```bash
   java -cp ".:aspose-cells-23.10.jar" com.example.exceljson.JsonToExcelDemo
   ```

3. 驗證 `JsonSingleCell.xlsx` 已出現在工作目錄中，且能正常開啟且無錯誤。

## 接下來您應該學習什麼？

以下教學涵蓋與本指南緊密相關的主題，建立在此處示範的技巧之上。每個資源皆包含完整可運作的程式碼範例與逐步說明，協助您精通其他 API 功能，並在自己的專案中探索替代實作方式。

- [從 JSON 建立 Excel 工作簿 – 完整 Aspose.Cells 指南](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [建立 Excel 工作簿 C# – 插入 JSON 並儲存為 XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)
- [從 JSON 儲存 Excel 工作簿 – 完整指南](/cells/english/net/templates-reporting/save-excel-workbook-from-json-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}