---
category: general
date: 2026-11-25
description: 使用 Aspose.Cells 智慧標記將 JSON 陣列綁定為單一值的 Excel 工作簿 Java 程式碼範例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: zh-hant
lastmod: 2026-11-25
og_description: 使用 Aspose.Cells 於 Java 建立 Excel 工作簿，輕鬆將 JSON 陣列匯出為單一儲存格。請依步驟說明操作。
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: 使用 Java 建立 Excel 工作簿 – Aspose.Cells 智能標記指南
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: 如何在 Java 中使用 Aspose.Cells 標記建立 Excel 活頁簿
url: /zh-hant/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 標記在 Java 中建立 Excel 活頁簿

如果您需要 **在 Java 中建立 Excel 活頁簿** 的程式碼，將 JSON 陣列寫入單一儲存格，本教學將一步步示範。透過 Aspose.Cells 智能標記，您可以將整個陣列視為一個值，免除手動迴圈與逐格寫入的繁瑣。

您將學會如何設定活頁簿、定義智能標記、綁定包含 JSON 風格陣列的 `Map` 資料來源，最後儲存檔案。此範例相容於 Java 17+、Maven 以及免費的 Aspose.Cells for Java 試用版。

---

![Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="使用 Aspose.Cells 智能標記在 Java 中建立的 Excel 工作簿截圖"}

## 前置條件

| 前置條件 | 為何重要 |
|----------|----------|
| Java 17 或更新版本 | 提供最新語言功能與安全性更新 |
| Maven 3.6+ | 簡化相依性管理 |
| Aspose.Cells for Java (v23.12 或更新) | 提供本範例使用的 `Workbook`、`Worksheet` 與智能標記 API |
| 基本的 Java 集合知識 | 您需要建立 `Map<String, Object>` 作為資料來源 |

將 Aspose.Cells 相依性加入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## 建立 Excel 活頁簿 Java – 完整範例

以下程式是一個 **完整、可執行** 的解決方案。將它複製到名為 `ExcelSmartMarkerDemo.java` 的檔案中，編譯並執行。

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### 程式碼說明

1. **建立全新活頁簿** – `new Workbook()` 會在記憶體中產生一個預設工作表的 Excel 檔案。  
2. **在儲存格 A1 放置智能標記** – `{{jsonArray:ArrayAsSingle}}` 告訴 Aspose.Cells 用 *整個* 陣列取代此標記，並以逗號串接。  
3. **建立 `Map` 資料來源** – 鍵名 `"jsonArray"` 必須與標記名稱相同；值則為 `String[]`。  
4. **呼叫 `setSmartMarkerData`** – 這會將 Map 綁定至標記並執行取代。  
5. **儲存檔案** – `workbook.save(...)` 會將 `JsonSingleValue.xlsx` 寫入磁碟。

開啟產生的 Excel 檔案時，儲存格 **A1** 會顯示：

```
One, Two, Three
```

因為使用了 `ArrayAsSingle` 選項，陣列會以單一、逗號分隔的字串呈現。

---

## 使用 Aspose.Cells 智能標記綁定 JSON 資料

Aspose.Cells 智能標記是一種強大的方式，可直接將複雜物件（包括類 JSON 結構）映射到工作表。語法 `{{fieldName:Option}}` 類似模板引擎：

* **fieldName** – 資料來源中的鍵（`Map`、POJO 或 `DataTable`）。  
* **Option** – 控制集合的處理方式。`ArrayAsSingle` 會將整個集合視為單一值；其他選項如 `Array` 會將陣列展開至多列。

**為何使用智能標記而非迴圈？**  
使用迴圈需要手動計算儲存格位址、處理易錯的索引，且需額外撰寫樣式程式碼。智能標記讓您以宣告式佔位符取代繁瑣程式，保持 Java 程式碼簡潔，並讓函式庫自行處理版面配置。

---

## 設定 Java Map 資料來源

`Map<String, Object>` 是 Aspose.Cells 最簡單的資料容器：

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*鍵名 (`jsonArray`) 必須與標記名稱完全相符。*  
您也可以使用 `List<String>`、自訂 POJO，或甚至是巢狀 `Map` 來表示更複雜的 JSON 結構。Aspose.Cells 會自動遍歷物件圖。

**小技巧：** 若需要以其他分隔符（例如分號）串接字串，可在將陣列放入 Map 前於 Java 中先行處理：

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## 儲存活頁簿並驗證輸出

```java
workbook.save("JsonSingleValue.xlsx");
```

`save` 方法支援多種格式（`.xlsx`、`.xls`、`.csv`、`.pdf`）。本教學使用預設的 Excel Open XML 格式。

**驗證步驟**

1. 在 Microsoft Excel、LibreOffice Calc 或 Google Sheets 中開啟 `JsonSingleValue.xlsx`。  
2. 確認儲存格 **A1** 內容為 `One, Two, Three`。  
3. 檢查是否未額外產生列或欄——智能標記已在原位取代。

若儲存格仍顯示原始標記文字 (`{{jsonArray:ArrayAsSingle}}`)，請再次確認：

* 標記名稱與 Map 鍵名完全相同（區分大小寫）。  
* `setSmartMarkerData` 必須在標記放置 **之後** 呼叫。  
* 您使用的 Aspose.Cells 版本支援 `ArrayAsSingle`（自 v20.3 起提供）。

---

## 常見變形與邊緣情況

| 情境 | 調整方式 |
|------|----------|
| **不同的分隔符** | 搭配 `ArrayAsSingle`，在 Java 中自行使用自訂的 join（參考上方小技巧）。 |
| **同一工作表中有多個陣列** | 在其他儲存格放置額外標記，例如 `{{anotherArray:ArrayAsSingle}}`，並在 Map 中加入對應項目。 |
| **巢狀 JSON 物件** | 提供巢狀 `Map<String, Object>`；使用點記法引用欄位（`{{parent.child}}`）。 |
| **大型資料集** | 若資料列數達千級，建議使用 `Array` 選項，讓 Aspose.Cells 自動展開列。 |

## 接下來您可以學習什麼？

以下教學與本指南緊密相關，能進一步深化您對 API 的運用，並探索在實務專案中的其他實作方式。每篇資源皆提供完整可執行的程式碼範例與逐步說明。

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑by‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}