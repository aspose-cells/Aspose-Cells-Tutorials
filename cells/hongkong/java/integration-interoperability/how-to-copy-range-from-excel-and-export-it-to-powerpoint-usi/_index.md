---
category: general
date: 2026-09-05
description: 學習如何在 Excel 中複製範圍、將 Excel 匯出至 PowerPoint，並使用完整的 Java 範例將 Excel 轉換為 pptx。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- export excel to powerpoint
- convert excel to pptx
- copy pivot table sheet
- how to export excel
language: zh-hant
lastmod: 2026-09-05
og_description: 如何使用 Java 複製範圍並將 Excel 匯出至 PowerPoint。請參考此一步一步的指南，高效地將 Excel 轉換為 PPTX。
og_image_alt: Screenshot showing how to copy range from Excel to PowerPoint in a Java
  IDE
og_title: 如何在 Java 中從 Excel 複製範圍並匯出至 PowerPoint
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to copy range in Excel, export excel to PowerPoint and convert
    excel to pptx with a complete Java example.
  headline: How to copy range from Excel and export it to PowerPoint using Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: 如何使用 Java 從 Excel 複製範圍並匯出至 PowerPoint
url: /zh-hant/java/integration-interoperability/how-to-copy-range-from-excel-and-export-it-to-powerpoint-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中從 Excel 複製範圍並匯出至 PowerPoint

如果您需要 **how to copy range** 從 Excel 工作簿，然後 **export excel to PowerPoint**，本指南將提供完整、可直接執行的解決方案。您將會看到如何複製包含樞紐分析表的範圍、為複製建立新工作表，最後只需一次方法呼叫即可 **convert Excel to PPTX**。

在程式化產生報告、投影片或儀表板時，複製範圍與匯出工作簿是常見需求。完成本教學後，您將擁有一個 Java 程式，能夠：

* 載入現有的 `.xlsx` 檔案。
* 將範圍 `A1:H20`（包含樞紐分析表）複製到新工作表。
* 將工作簿儲存為可編輯的 `.pptx` 簡報。

您只需要 Aspose.Cells for Java 函式庫；不需要其他相依性。

## 前置條件

在開始之前，請確保您已具備以下條件：

* 已安裝 Java 17（或更新版本）。
* 使用 Maven 或 Gradle 來管理相依性。
* Aspose.Cells for Java 23.9（或最新版本）——如下方 Maven 片段所示，將其加入您的專案。
* 一個包含您想要複製之資料與樞紐分析表的 Excel 檔案（`input.xlsx`）。

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

## 步驟 1：從檔案載入工作簿

在 **how to copy range** 的第一個操作是開啟來源工作簿。這讓您可以存取工作表、儲存格與樞紐分析表。

```java
// Load the workbook from a file
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*為什麼需要這一步？*  
載入檔案會在記憶體中建立 Excel 文件的表示，讓您能在不觸及原始檔案的情況下操作其內容。

## 步驟 2：取得包含資料的來源工作表

通常第一張工作表即為您想要複製的資料所在。您可以透過索引取得它。

```java
// Get the source worksheet (first sheet) that contains the data/pivot table
Worksheet sourceSheet = workbook.getWorksheets().get(0);
```

如果您的工作簿將樞紐分析表放在其他工作表，請將 `0` 替換為相應的索引，或使用 `get("SheetName")`。

## 步驟 3：為複製的範圍新增工作表

建立目的工作表可將複製的資料隔離，並讓之後的匯出更為乾淨。

```java
// Add a new worksheet that will receive the copied range
Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
```

您可以自行命名工作表；名稱「Copy」能清楚表示它保存了複製的範圍。

## 步驟 4：複製範圍（how to copy range），包括樞紐分析表

現在我們執行核心的 **how to copy range** 操作。`copyRange` 方法會同時複製數值與格式，且會保留樞紐分析表的定義。

```java
// Copy the range A1:H20 (including the pivot table) to the new sheet starting at A1
sourceSheet.getCells().copyRange(
        "A1:H20",
        destinationSheet.getCells().get("A1"),
        new CopyOptions()   // default options copy values, formats, and objects
);
```

*為什麼使用 `CopyOptions`？*  
提供 `CopyOptions` 實例可讓您微調要複製的內容（例如公式、欄寬）。預設建構子會複製全部，這在您想要完整複製 **copy pivot table sheet** 時非常理想。

## 步驟 5：準備選項以將工作簿匯出為可編輯的 PowerPoint 簡報

匯出至 PowerPoint 透過 `ImageOrPrintOptions` 完成。將儲存格式設定為 `SaveFormat.PPTX`，即告訴 Aspose.Cells 產生 PowerPoint 檔案而非影像。

```java
// Prepare options to export the workbook as an editable PowerPoint presentation
ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
pptOptions.setSaveFormat(SaveFormat.PPTX);   // this enables export excel to powerpoint
```

如果需要自訂版面，您也可以透過 `pptOptions` 調整投影片尺寸、DPI 以及其他簡報設定。

## 步驟 6：將工作簿儲存為 PPTX 檔案（convert excel to pptx）

最後，使用 PPTX 選項呼叫 `workbook.save`。此步驟 **how to export excel** 成為投影片。

```java
// Save the workbook to a PPTX file using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);
```

程式執行完畢後，`output.pptx` 會包含一張投影片，複製的範圍會與 Excel 中完全相同，且保留樞紐分析表的控制項。

### 預期輸出

在 Microsoft PowerPoint 或任何相容的檢視器中開啟 `output.pptx`。您應該會看到一張投影片，顯示範圍 `A1:H20`，保留儲存格顏色、邊框與樞紐分析表的版面配置。此投影片可完全編輯——您可以移動、調整大小或格式化表格，就像任何原生 PowerPoint 內容一樣。

## 完整可執行範例

將所有步驟整合在一起，即可得到一個自包含的 Java 類別：

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Get the source worksheet (first sheet)
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // 3. Add a destination worksheet
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // 4. Copy the range A1:H20 (including pivot table)
        sourceSheet.getCells().copyRange(
                "A1:H20",
                destinationSheet.getCells().get("A1"),
                new CopyOptions()
        );

        // 5. Configure export options for PowerPoint
        ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
        pptOptions.setSaveFormat(SaveFormat.PPTX);

        // 6. Save as PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);

        System.out.println("Export completed: output.pptx created successfully.");
    }
}
```

在 IDE 中或透過指令列執行此類別：

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPowerPoint
```

檔案寫入完成後，您會看到確認訊息。

## 常見問題與邊緣情況

| Question | Answer |
|----------|--------|
| **我可以複製非連續的範圍嗎？** | 使用包含多個區域的命名範圍呼叫 `copyRange`，或對每個區塊分別多次呼叫 `copyRange`。 |
| **如果來源工作表包含多個樞紐分析表該怎麼辦？** | 複製矩形內的每個樞紐分析表都會被轉移。對於矩形外的表，需另行複製。 |
| **如何將多個工作表匯出為獨立的投影片？** | 遍歷工作表，將每個工作表複製到暫存工作表，然後在每次迭代中使用 `pptOptions` 呼叫 `workbook.save`，透過 `Presentation` API 追加至同一個 PPTX。 |
| **產生的 PPTX 可編輯嗎？** | 是的。匯出會產生原生 PowerPoint 物件，您之後可以修改文字、重新調整表格形狀或加入動畫。 |
| **大型工作簿該如何處理？** | 可將 `pptOptions.setDpi(300)` 提高以獲得更高解析度，但需注意記憶體使用；必要時可分批處理工作表。 |

## 專業提示

* **保留欄寬** – 若需要精確的寬度匹配，請在複製前設定 `CopyOptions.setColumnWidth(true)`。
* **使用自訂投影片尺寸** – 使用 `pptOptions.setImageHeight(720); pptOptions.setImageWidth(1280);` 以符合 16:9 簡報。
* **加入標題投影片** – 匯出後，使用 Aspose.Slides 開啟 PPTX，並在最前面插入包含標題與日期的投影片。

## 結論

您現在已了解如何使用 Java 從 Excel 工作簿 **how to copy range**、**export excel to PowerPoint**，以及 **convert excel to pptx**。遵循上述六個步驟，即可自動化報告產生、從即時資料建立投影片，且保持樞紐分析表功能完整。

### 接下來做什麼？

* 探索 **copy pivot table sheet** 的變化，例如僅複製樞紐快取。
* 將此工作流程與 **Aspose.Slides** 結合，以加入自訂動畫或品牌標誌。
* 在排程工作中自動批次處理數十本工作簿。

歡迎自行嘗試各種選項，並將程式碼調整至您的報告流程中。若遇到任何問題，請參考 Aspose.Cells for Java 文件，以深入了解 `CopyOptions` 與 `ImageOrPrintOptions`。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南技術緊密相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [如何將 Excel 匯出至 PowerPoint – 步驟說明指南](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [如何使用 Aspose.Cells Java 複製 Excel 中的多欄位&#58; 完整指南](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells for .NET 將 Excel 轉換為 PowerPoint&#58; 完整指南](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}