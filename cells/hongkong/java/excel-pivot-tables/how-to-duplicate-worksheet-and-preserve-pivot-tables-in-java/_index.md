---
category: general
date: 2026-08-17
description: 如何在 Java 中使用 Aspose.Cells 複製工作表，保留樞紐分析表，將樞紐分析表複製到新工作簿，以及從工作表建立工作簿。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate worksheet
- how to copy pivot
- how to preserve pivot
- copy pivot to workbook
- create workbook from sheet
language: zh-hant
lastmod: 2026-08-17
og_description: 如何在 Java 中使用 Aspose.Cells 複製工作表，保留樞紐分析表，將樞紐分析表複製到新活頁簿，並從工作表建立活頁簿——完整步驟說明。
og_image_alt: Screenshot of Java code duplicating an Excel worksheet with a pivot
  table using Aspose.Cells
og_title: 如何複製工作表並保留樞紐分析表 – Java 指南
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  headline: How to duplicate worksheet and preserve pivot tables in Java
  type: TechArticle
- description: How to duplicate worksheet in Java using Aspose.Cells, preserving the
    pivot table, copying pivot to a new workbook, and creating a workbook from a sheet.
  name: How to duplicate worksheet and preserve pivot tables in Java
  steps:
  - name: – Load the workbook that contains the pivot table
    text: '```java import com.aspose.cells.*;'
  - name: – Create a new workbook and duplicate the entire worksheet
    text: '```java // Create an empty destination workbook Workbook destinationWorkbook
      = new Workbook();'
  - name: – Save the new workbook
    text: '```java // Save the duplicated workbook; the pivot remains functional destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
      } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
- Workbook
title: 如何在 Java 中複製工作表並保留樞紐分析表
url: /zh-hant/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中複製工作表並保留樞紐分析表

在自動化 Excel 報告時，如何在保持樞紐分析表完整的情況下複製工作表是一個常見需求。本指南將示範如何使用 Aspose.Cells for Java 將樞紐分析表複製到新工作簿，並說明在從工作表建立工作簿時如何保留樞紐分析表。

您將學習如何載入現有工作簿、複製包含樞紐分析表的工作表，並將結果儲存為新檔案。本教學假設您具備基本的 Java 開發環境以及有效的 Aspose.Cells 授權（免費評估版可用於測試）。除 Aspose.Cells JAR 外，無需其他外部工具。

## 前置條件

在開始之前，請確保您已具備：

* Java Development Kit (JDK) 8 或更新版本。
* 用於管理 Aspose.Cells 相依性的 Maven 或 Gradle。
* 一個 Excel 檔案（`source.xlsx`），其第一個工作表上至少有一個樞紐分析表。
* 一個目錄，可用於讀取來源檔案並寫入複製後的工作簿。

將 Aspose.Cells 相依性加入您的 `pom.xml`（Maven）或 `build.gradle`（Gradle）。以下為 Maven 範例：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

## 如何在包含樞紐分析表的工作表上進行複製

核心操作為三步驟流程：載入、複製與儲存。以下說明每一步。

### 步驟 1 – 載入包含樞紐分析表的工作簿

```java
import com.aspose.cells.*;

public class CopyPivotTable {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceWorksheet = sourceWorkbook.getWorksheets().get(0);
```

*此步驟的重要性*：`Workbook` 物件代表整個 Excel 檔案。透過取得第一個工作表（`get(0)`），即可鎖定您欲複製的樞紐分析表所在的工作表。

### 步驟 2 – 建立新工作簿並複製整個工作表

```java
        // Create an empty destination workbook
        Workbook destinationWorkbook = new Workbook();

        // Duplicate the source worksheet, preserving its pivot table
        destinationWorkbook.getWorksheets().addCopy(sourceWorksheet);
```

`addCopy` 會克隆工作表 **包括** 所有嵌入物件、公式與樞紐快取。這是建議的 **how to copy pivot** 方式，因為樞紐定義與其資料來源會一起轉移。

### 步驟 3 – 儲存新工作簿

```java
        // Save the duplicated workbook; the pivot remains functional
        destinationWorkbook.save("YOUR_DIRECTORY/copy_with_pivot.xlsx");
    }
}
```

執行後，`copy_with_pivot.xlsx` 會包含原始工作表的完整副本，且樞紐分析表可直接運作，無需額外設定。

**預期結果**：在 Excel 中開啟 `copy_with_pivot.xlsx`，會看到複製的工作表，其樞紐布局、篩選條件與計算欄位皆與來源檔案相同。

## 如何將樞紐分析表複製到其他工作簿

如果您需要在不複製整個工作表的情況下搬移樞紐分析表，可提取樞紐快取並將其附加到新工作表。以下程式碼片段示範此方法：

```java
// Assume sourceWorkbook and sourceWorksheet are already loaded
PivotTable pivot = sourceWorksheet.getPivotTables().get(0);

// Create a new workbook and a blank worksheet
Workbook targetWorkbook = new Workbook();
Worksheet targetSheet = targetWorkbook.getWorksheets().add("PivotCopy");

// Import the pivot table definition
targetSheet.getPivotTables().addCopy(pivot);
targetWorkbook.save("YOUR_DIRECTORY/pivot_only_copy.xlsx");
```

此程式碼透過僅複製樞紐物件（而非整個工作表）回應 **how to copy pivot**。`PivotTables` 集合上的 `addCopy` 方法確保樞紐快取被複製，滿足 **how to preserve pivot** 的需求。

## 如何在從工作表建立工作簿時保留樞紐分析表

有時您會從不屬於任何工作簿的工作表開始（例如，在記憶體中產生工作表）。若要在 **create workbook from sheet** 時保留樞紐分析表，請依照以下步驟操作：

```java
// Create a worksheet in memory
Worksheet tempSheet = new Worksheet();
PivotTable pivot = tempSheet.getPivotTables().add("A1", "B10", "MyPivot");

// Configure the pivot source range, rows, columns, data fields, etc.
// (Omitted for brevity – see Aspose.Cells docs for detailed setup)

// Wrap the worksheet in a new workbook
Workbook newWorkbook = new Workbook();
newWorkbook.getWorksheets().addCopy(tempSheet);
newWorkbook.save("YOUR_DIRECTORY/created_from_sheet.xlsx");
```

在樞紐分析表完整定義後，將工作表加入全新的 `Workbook`，即可確保即使工作表來源於既有檔案之外，**how to preserve pivot** 仍能正常運作。

## 實用技巧與常見陷阱

| 技巧 | 為何重要 |
|-----|----------|
| 使用 `addCopy` 而非 `copy` | `addCopy` 會克隆底層的樞紐快取；單純的 `copy` 可能會失去與資料來源的連結。 |
| 將來源與目的檔案放在同一檔案系統上 | 樞紐分析表資料來源的相對路徑會正確解析，減少「找不到來源」的錯誤。 |
| 複製後驗證樞紐快取 | 若在複製與儲存之間來源資料有變更，請呼叫 `pivot.refresh()`。 |
| 完成後釋放工作簿 | `sourceWorkbook.dispose();` 釋放原生資源，對於大型檔案尤為重要。 |

## 可能遇到的邊緣情況

* **多個工作表之間的樞紐分析表相互依賴** – 請逐一複製每個工作表；共用快取會自動被複製，但可能需要重新指派外部資料連線。
* **基於外部 SQL 查詢的樞紐分析表** – 確保目的環境能連接相同的資料庫；否則樞紐分析表會顯示 “#REF!” 錯誤。
* **大型工作簿（>100 MB）** – 使用 `WorkbookSettings.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` 以降低複製過程中的記憶體壓力。

## 完整、可執行的範例

以下為結合所有步驟的完整程式。將其儲存為 `CopyPivotTable.java`，調整檔案路徑後，即可使用您偏好的 IDE 或透過 `javac`/`java` 執行。



## 接下來該學什麼？

以下教學涵蓋與本指南技術密切相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通更多 API 功能，並在專案中探索替代實作方式。

- [如何使用 Aspose.Cells for Java 在 Excel 中建立樞紐分析表：完整指南](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 更新 Excel 樞紐分析表來源：完整指南](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 在樞紐分析表中實作切片器：完整指南](/cells/english/java/data-analysis/implement-slicers-pivot-tables-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}