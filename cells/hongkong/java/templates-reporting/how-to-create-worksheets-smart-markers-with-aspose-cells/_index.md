---
category: general
date: 2026-08-20
description: 使用 Aspose.Cells 在 Java 中建立工作表智慧標記，並使用 SmartMarkerOptions 控制明細工作表的命名。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: zh-hant
lastmod: 2026-08-20
og_description: 在 Java 中使用 Aspose.Cells 建立工作表智慧標記。了解如何使用 SmartMarkerOptions 動態命名明細工作表。
og_image_alt: create worksheets smart markers example diagram
og_title: 建立工作表智慧標記 – Aspose.Cells Java 指南
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: 如何使用 Aspose.Cells 建立工作表智慧標記
url: /zh-hant/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 Aspose.Cells 建立工作表智慧標記

如果您需要在 Java 工作簿中 **建立工作表智慧標記**，本指南將向您展示使用 Aspose.Cells 的具體步驟。您將看到如何設定 `SmartMarkerOptions`，使每個明細工作表獲得唯一且可預測的名稱。

在金融、庫存和報告系統中，產生擴展主從模板的 Excel 報表是常見需求。使用智慧標記可消除手動工作表複製，讓您專注於資料本身，而非繁瑣的流程。

## 您將學習到

* 如何載入包含智慧標記的主工作簿。  
* 如何設定 `SmartMarkerOptions` 以控制產生的明細工作表名稱。  
* 如何提供帶有範例資料的 `DataTable` 並套用至智慧標記。  
* 如何儲存結果，使每個明細工作表都有唯一名稱，避免工作表名稱重複。  

**先決條件**  
* Java 17 或更新版本（程式碼亦可在 JDK 8+ 編譯）。  
* Aspose.Cells for Java 23.9 或更新版本 – 此函式庫提供 `Workbook`、`SmartMarkerOptions` 及相關類別。  
* 如 IntelliJ IDEA、Eclipse 或 VS Code 等 IDE。  

您將會接觸的次要概念包括 **Aspose.Cells Java**、**smart marker options**，以及在模板展開時處理 **duplicate sheet names**。

## 建立工作表智慧標記 – 步驟指南

以下各節將流程拆分為獨立且可重複使用的步驟。每個步驟都包含程式碼片段、重要性說明，以及避免常見陷阱的實用提示。

### 步驟 1：設定 Maven 專案並加入 Aspose.Cells

建立新的 Maven 模組（或 Gradle 專案），並加入 Aspose.Cells 相依性：

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**此步驟的重要性** – 此函式庫提供 `Workbook` 類別，用於讀寫 Excel 檔案，並包含自動展開模板的智慧標記引擎。若未加入正確的相依性，編譯器將無法解析後續的 API 呼叫。

> **專業提示：** 若您位於公司代理伺服器後，請設定 Maven 的 `settings.xml` 以安全取得 Aspose 儲存庫。

### 步驟 2：載入包含智慧標記的主工作簿

載入主工作簿的程式碼如下：

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**此步驟的重要性** – 主工作簿定義了版面配置、公式以及引擎將取代的佔位標籤（`«SmartMarker»`）。一次載入檔案可降低記憶體使用，並允許在多個資料集間重複使用同一工作簿。

### 步驟 3：設定 SmartMarkerOptions 以自訂明細工作表名稱

設定自訂明細工作表名稱的程式碼：

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**此步驟的重要性** – 預設情況下，Aspose.Cells 會以「DetailSheet」等通用名稱建立明細工作表。當模板因多筆資料展開時，這些名稱會衝突，導致 **duplicate sheet names** 並拋出執行時例外。使用 `"DetailSheet_{0}"` 模式可保證每列產生唯一名稱，解決重複問題。

### 步驟 4：建立符合智慧標記欄位的 DataTable

建立符合智慧標記欄位的 DataTable 程式碼：

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**此步驟的重要性** – `DataTable` 提供實際值以取代智慧標記佔位符。欄位名稱必須與模板中的標記名稱相符，否則引擎會靜默跳過取代。

> **常見錯誤：** 使用大小寫不同的欄位名稱（例如 “id” 與 “Id”）會導致產生的工作表缺少資料。

### 步驟 5：使用命名選項將資料套用至智慧標記

將資料套用至智慧標記的程式碼：

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**此步驟的重要性** – `apply` 方法會觸發智慧標記引擎。它會讀取每一列資料，依照 `SmartMarkerOptions` 的命名模式建立新明細工作表，並將該列資料填入工作表。這一呼叫即可取代手動複製工作表與填寫儲存格的多行程式碼。

### 步驟 6：儲存工作簿並驗證結果

儲存工作簿的程式碼：

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

執行完畢後，開啟 `MasterDetailDuplicatedNames.xlsx`。您應該會看到：

* 原始的主工作表保持不變。  
* 兩個新工作表分別命名為 `DetailSheet_1` 和 `DetailSheet_2`。  
* 每個明細工作表都包含 `DataTable` 中對應列的值。  

**此步驟的重要性** – 將工作簿持久化即完成智慧標記的展開。此檔案可傳送至下游系統、作為電子郵件附件，或在 Excel 中開啟進一步分析。

## 處理邊緣案例與變化

### 多個主工作表

如果您的模板包含多於一個主工作表，請遍歷每個工作表的智慧標記：

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### 超越列索引的自訂命名

您可以使用 `{ColumnName}` 之類的佔位符，將任意資料欄位嵌入工作表名稱：

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

請確保在提供的 `DataTable` 中存在 `OrderId` 欄位。

### 防止工作表名稱過長

Excel 限制工作表名稱最多 31 個字元。若您的命名模式可能超過此上限，請截斷或雜湊該值：

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

然後在傳遞給 Aspose 之前，使用 `StringUtils.abbreviate` 進行後處理。

## 完整可執行範例

以下為完整的來源檔案，您可以直接複製、調整檔案路徑後執行：

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**預期輸出**

* `MasterDetailDuplicatedNames.xlsx` 包含：

## 接下來您應該學習什麼？

以下教學涵蓋與本指南技術密切相關的主題，並在此基礎上延伸。每個資源皆提供完整可運作的程式碼範例與步驟說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [精通 Aspose.Cells Java：在工作表中使用智慧標記處理動態資料](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [使用智慧標記在 Aspose.Cells for Java 中建立動態圖表 | 步驟指南](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Aspose Cells Java 智慧標記工作表](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}