---
category: general
date: 2026-07-03
description: 如何使用智慧標記填充 Excel 範本來產生報告。學習建立詳細工作表、使用智慧標記及自動化資料插入。
draft: false
keywords:
- how to generate report
- populate excel template
- how to create detail
- create detail sheet
- use smart markers
language: zh-hant
og_description: 如何在 Java 中使用 Smart Markers 產生報表。本指南說明如何填充 Excel 模板、建立明細工作表以及自動化主從報表。
og_title: 如何使用 Excel 智慧標記生成報表 – Java 教程
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to generate report by populating an Excel template using Smart
    Markers. Learn to create detail sheet, use smart markers and automate data insertion.
  headline: How to Generate Report with Excel Smart Markers – Full Java Guide
  type: TechArticle
- description: How to generate report by populating an Excel template using Smart
    Markers. Learn to create detail sheet, use smart markers and automate data insertion.
  name: How to Generate Report with Excel Smart Markers – Full Java Guide
  steps:
  - name: What the code does, step by step
    text: '| Step | Explanation | |------|-------------| | **Load workbook** | Reads
      the template, preserving all formatting. | | **Insert marker** | Guarantees
      the placeholder exists even if you built the template programmatically. | |
      **Prepare data** | The `Map` key (`"Orders"`) must match the Smart Marker '
  - name: 5.1 Multiple Detail Datasets
    text: 'You can embed several Smart Markers in the same template, e.g., `{{Detail:Customers}}`
      and `{{Detail:Orders}}`. Just add corresponding entries to the `Map`:'
  - name: 5.2 Custom Sheet Names per Row
    text: 'If you need a unique sheet per order (instead of a single detail sheet),
      use the `DetailSheetNewName` pattern with placeholders:'
  - name: 5.3 Handling Large Datasets
    text: 'When dealing with thousands of rows, enable streaming to keep memory usage
      low:'
  - name: 5.4 Formatting Numbers and Dates
    text: Smart Markers respect the cell’s existing format. If column B in the template
      is formatted as **Currency**, the amounts will automatically display with the
      correct symbol. For custom date formats, just set the cell’s number format before
      processing.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel Automation
title: 如何使用 Excel 智慧標記生成報告 – 完整 Java 指南
url: /zh-hant/java/templates-reporting/how-to-generate-report-with-excel-smart-markers-full-java-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Excel Smart Markers 產生報告 – 完整 Java 指南

有沒有想過 **如何產生報告** 從 Excel 範本，而不必寫上千行迴圈程式碼？你並不孤單。許多開發人員在需要從資料庫提取資料、填入主從工作簿，且仍保持版面精緻時，常會卡關。

好消息是？使用 Aspose.Cells **Smart Markers**，您只需一次可讀的呼叫即可 **populate Excel template**——不需要繁瑣的逐格操作。在本教學中，我們將完整說明從準備範本到儲存最終檔案的整個流程，並示範 **how to create detail** 工作表的即時產生方式。

在本指南結束時，您將能夠：

* 載入作為主工作表的預先設計好的工作簿。  
* 插入 Smart Marker 佔位符，讓 Aspose 用真實的訂單資料取代。  
* 提供 Java `Map` 作為資料來源，並設定 **create detail sheet** 選項。  
* 執行處理器，產生可直接分享的精緻主從報告。

> **Pro tip:** 如果您已經有一個業務團隊喜愛的範本，根本不需要更動版面——只要在正確的儲存格放入 Smart Marker 標籤即可。

---

## 前置條件

在深入程式碼之前，請確保您具備以下條件：

| Requirement | Why it matters |
|-------------|----------------|
| **Aspose.Cells for Java** (latest version) | 提供 `SmartMarkerProcessor`、`Workbook` 以及相關 API。 |
| **Java 8+** | 範例使用 Java 9 引入的 `Map.of` 工廠方法以及串流，若您使用 Java 8，請自行調整。 |
| **An Excel template** (`template.xlsx`) with a placeholder cell for the Smart Marker | 這是您將載入並稍後儲存為 `masterDetail.xlsx` 的檔案。 |
| **A simple data model** (e.g., `Order` class) | 為處理器提供具體的資料以取代標記。 |

如果您尚未取得 Aspose.Cells，請從官方網站取得免費試用版，並將 JAR 加入專案的 classpath。

---

## 步驟 1：設定 Excel 範本 (populate excel template)

在 Excel 中開啟並建立名為 `template.xlsx` 的工作簿。於第一個工作表的 **A1** 儲存格輸入 Smart Marker 標籤：

```
{{Detail:Orders}}
```

此標籤告訴 Aspose 將 `Orders` 集合視為 **detail** 資料集，並為每筆項目產生列。將檔案儲存於稍後會參考的資料夾，例如 `C:/Reports/`。

**Why this matters:** 透過將標記直接嵌入範本，您可將視覺設計與程式碼分離。設計師能調整字型、顏色與公式，而不必觸碰 Java 程式。

---

## 步驟 2：建立 Java 專案結構

以下是一段最小化的 Maven `pom.xml` 片段，用於引入 Aspose.Cells：

```xml
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-cells</artifactId>
        <version>24.9</version> <!-- Use the latest version -->
    </dependency>
</dependencies>
```

建立套件 `com.example.report`，並新增兩個類別：`ReportGenerator`（主程式）與 `Order`（資料模型）。

```java
package com.example.report;

public class Order {
    public String orderId;
    public String customer;
    public double amount;

    public Order(String orderId, String customer, double amount) {
        this.orderId = orderId;
        this.customer = customer;
        this.amount = amount;
    }

    // Getters are optional for Smart Marker; public fields work fine.
}
```

---

## 步驟 3：載入工作簿並插入 Smart Marker (use smart markers)

現在我們撰寫核心邏輯。請注意程式碼與原始片段相似，但加入了匯入、錯誤處理與說明註解，以提升可讀性。

```java
package com.example.report;

import com.aspose.cells.*;
import java.util.*;

public class ReportGenerator {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the workbook that contains the master sheet
            Workbook wb = new Workbook("C:/Reports/template.xlsx");

            // 2️⃣ Grab the first worksheet (the master)
            Worksheet master = wb.getWorksheets().get(0);

            // 3️⃣ Insert a Smart Marker placeholder if you prefer to do it programmatically.
            //    This is optional because we already placed {{Detail:Orders}} in A1.
            master.getCells().putValue("A1", "{{Detail:Orders}}");

            // 4️⃣ Prepare the data source for the Smart Marker
            Map<String, Object> data = new HashMap<>();
            data.put("Orders", getOrders()); // getOrders() returns List<Order>

            // 5️⃣ Configure Smart Marker options – this is where we **create detail sheet**
            SmartMarkerOptions smOpt = new SmartMarkerOptions();
            smOpt.setDetailSheetNewName("OrderDetail"); // New sheet will be named "OrderDetail"

            // 6️⃣ Process the Smart Marker to generate the master‑detail report
            SmartMarkerProcessor processor = new SmartMarkerProcessor();
            processor.process(master, data, smOpt);

            // 7️⃣ Save the resulting workbook
            wb.save("C:/Reports/masterDetail.xlsx");

            System.out.println("Report generated successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Simulates fetching order data from a database or service.
     * In a real‑world scenario replace this with JDBC/ORM calls.
     */
    private static List<Order> getOrders() {
        return Arrays.asList(
            new Order("ORD001", "Acme Corp", 1250.75),
            new Order("ORD002", "Beta Ltd.", 980.00),
            new Order("ORD003", "Gamma Inc.", 432.50)
        );
    }
}
```

### 程式碼逐步說明

| Step | Explanation |
|------|-------------|
| **Load workbook** | 讀取範本，保留所有格式。 |
| **Insert marker** | 確保佔位符存在，即使您以程式方式建立範本亦是如此。 |
| **Prepare data** | `Map` 的鍵 (`"Orders"`) 必須與 Smart Marker 標籤 (`{{Detail:Orders}}`) 相符。 |
| **Configure options** | `setDetailSheetNewName` 告訴 Aspose 建立一個名為 *OrderDetail* 的 **create detail sheet**。 |
| **Process** | `SmartMarkerProcessor` 逐一檢視工作簿，取代標記，並在新工作表產生列。 |
| **Save** | 將最終的 `masterDetail.xlsx` 寫入磁碟。 |

**Why use Smart Markers?** 它們讓您描述 *想要什麼*（例如訂單表格），而非 *如何* 逐列逐欄迴圈。函式庫會自動處理分頁、樣式複製，甚至公式重新計算。

---

## 步驟 4：驗證輸出 (how to generate report – verification)

執行 `ReportGenerator` 類別。執行完畢後，您應該會看到兩個工作表：

1. **Sheet1** – 原始的主工作表（仍包含 `{{Detail:Orders}}`，但處理器會隱藏它）。  
2. **OrderDetail** – 全新工作表，為每個 `Order` 物件產生一列：

| 訂單編號 | 客戶       | 金額   |
|----------|------------|--------|
| ORD001   | Acme Corp  | 1250.75|
| ORD002   | Beta Ltd.  | 980.00 |
| ORD003   | Gamma Inc. | 432.50 |

若在 Excel 開啟檔案，您會發現欄寬、字型以及範本中預先套用的樣式皆保持不變。這就是 **use smart markers** 的魅力：在注入資料的同時仍保留版面呈現。

---

## 步驟 5：常見變形與例外情況 (populate excel template, how to create detail)

### 5.1 多個 Detail 資料集

您可以在同一範本中嵌入多個 Smart Markers，例如 `{{Detail:Customers}}` 與 `{{Detail:Orders}}`。只需在 `Map` 中加入對應的項目：

```java
data.put("Customers", getCustomers());
data.put("Orders", getOrders());
```

若適當設定 `DetailSheetNewName`，每個都會產生自己的工作表。

### 5.2 依列自訂工作表名稱

如果您需要為每筆訂單產生唯一的工作表（而非單一的 detail 工作表），可使用帶佔位符的 `DetailSheetNewName` 模式：

```java
smOpt.setDetailSheetNewName("Order_{OrderId}");
```

Aspose 會將 `{OrderId}` 取代為每列的實際值。

### 5.3 處理大型資料集

處理數千列資料時，請啟用串流以降低記憶體使用量：

```java
WorkbookSettings ws = wb.getSettings();
ws.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

### 5.4 數字與日期格式化

Smart Markers 會遵循儲存格現有的格式。若範本中 B 欄已設定為 **Currency**，金額會自動以正確的貨幣符號顯示。若需自訂日期格式，只要在處理前設定儲存格的數字格式即可。

---

## 步驟 6：技巧與注意事項 (how to create detail, use smart markers)

* **永遠不要在正式環境硬編碼檔案路徑**。請使用設定檔或環境變數。  
* **若手動開啟串流，務必關閉資源**；`Workbook` 類別在較新版本已實作 `AutoCloseable`。  
* **留意命名衝突**——若已有同名工作表，Aspose 會在名稱後加上數字後綴。為確保唯一性，可在名稱前加上時間戳記。  
* **測試空集合**。若 `Orders` 為空，處理器仍會建立工作表但保持空白——若不想出現多餘分頁，請在後續處理時加以判斷。  
* **除錯 Smart Markers**：設定 `smOpt.setThrowExceptionOnMissingData(true)`，當標記找不到對應資料欄位時會拋出明確例外。

![使用 Smart Markers 於 Java 產生報告](/images/how-to-generate-report-smart-markers.png "如何產生報告")

*圖片說明：最終的 `masterDetail.xlsx`，顯示主工作表與產生的 **OrderDetail** 工作表。*

---

## 結論

我們剛剛示範了如何透過 Aspose.Cells Smart Markers **populate an Excel template** 來 **how to generate report**，並說明了自動 **create detail sheet** 所需的全部步驟。此方法保留了...

## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [如何使用 Aspose.Cells for Java 自動化 Excel Smart Markers](/cells/english/java/automation-batch-processing/aspose-cells-java-smart-markers-excel/)
- [使用 Aspose.Cells 與 Smart Markers 填充 Excel 資料](/cells/english/java/cell-operations/populate-excel-aspose-cells-smart-markers/)
- [如何使用 Aspose.Cells for Java 在 Excel 中建立樞紐分析表：完整指南](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}