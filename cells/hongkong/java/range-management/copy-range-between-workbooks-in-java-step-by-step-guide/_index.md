---
category: general
date: 2026-08-14
description: 使用 Aspose.Cells 於 Java 複製工作簿之間的範圍。學習如何複製樞紐分析表工作簿、將圖片匯出至 PowerPoint，以及從
  Excel 表格中移除自動篩選。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: zh-hant
lastmod: 2026-08-14
og_description: 在 Java 中於工作簿之間複製範圍。本指南說明如何複製樞紐分析表工作簿、將圖片匯出至 PowerPoint，以及從 Excel 表格移除自動篩選。
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: 在 Java 中於工作簿之間複製範圍 – 完整 Aspose.Cells 教學
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: 在 Java 中於工作簿之間複製範圍 – 步驟指南
url: /zh-hant/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Java 中跨工作簿複製範圍 – 步驟指南

如果您需要在 Java 中 **copy range between workbooks**，Aspose.Cells 提供了簡潔的 API，能處理樞紐分析表與圖片等複雜物件。本教學示範如何 **copy pivot table workbook**、**export picture to PowerPoint**，以及 **remove AutoFilter from Excel table**，同時保持程式碼易於閱讀與維護。

您將學會：

* 載入來源工作簿並定義來源範圍。  
* 建立目標工作簿並複製範圍，使樞紐分析表保持完整。  
* 將工作表上的第一張圖片匯出為可編輯的 PowerPoint 物件。  
* 從第一個 Excel 表格中移除 AutoFilter。  
* 使用 `SmartMarkerOptions` 載入工作簿，將 JSON 陣列視為單一儲存格值。

本範例使用 Aspose.Cells 23.10 for Java，但概念同樣適用於較早的版本。

---

## 前置條件

| 需求 | 重要原因 |
|------|----------|
| Java 17 或更新版本 | 最新 Aspose.Cells 執行環境所需。 |
| Aspose.Cells for Java（Maven 套件 `com.aspose:aspose-cells`） | 提供程式碼中使用的 `Workbook`、`Worksheet`、`Range` 等類別。 |
| 一個包含樞紐分析表、圖片與具 AutoFilter 的表格的來源 Excel 檔 (`src.xlsx`) | 教學會操作這些物件以示範各項功能。 |

將 Maven 相依性加入 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## 跨工作簿複製範圍 – 載入來源與目標

第一步是開啟來源工作簿、選取欲複製的資料範圍，並建立一個空的目標工作簿。

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **重要說明：** 透過 `Range.copy`，Aspose.Cells 不僅會複製原始儲存格值，還會同步複製底層的樞紐快取，讓目標工作簿中的樞紐分析表仍能正常運作。

---

## 複製樞紐分析表工作簿同時複製範圍

現在將先前定義的範圍從來源工作簿複製到目標工作簿。因為範圍已包含樞紐快取，樞紐分析表會自動保留。

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **結果：** 開啟 `destination.xlsx` 後，可看到與 `src.xlsx` 相同的樞紐分析表版面，無需額外程式碼重建樞紐快取。

---

## 匯出圖片至 PowerPoint

Aspose.Cells 可將圖片標記為可匯出為可編輯 PowerPoint 物件。以下程式碼會選取目標工作表上的第一張圖片並設定匯出旗標。

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **您會看到：** 在 PowerPoint 中開啟 `destination.pptx` 時，圖片會以原生圖形呈現，您可以編輯、調整大小或加入動畫。

---

## 從 Excel 表格移除 AutoFilter

如果來源工作表的表格帶有 AutoFilter，複製後可能需要將其清除。下列程式碼會取得第一個表格並移除其篩選功能。

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **效果：** 表格仍保留於工作簿中，但下拉篩選箭頭已消失，呈現乾淨的資料檢視。

---

## 使用 SmartMarker 選項載入工作簿 – 將 JSON 陣列視為單一儲存格

在從 JSON 產生報表時，Aspose.Cells 能將整個陣列視為單一儲存格值，避免自動展開為多列或多欄。

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **使用情境：** 若您的 JSON 內容包含陣列，且希望在模板中以 JSON 字串形式顯示於單一儲存格，`setArrayAsSingle(true)` 可防止 Aspose.Cells 將陣列展開。

---

![在 Java 中跨工作簿複製範圍 – Aspose.Cells 程式碼範例](copy-range-workbooks.png)

*圖片說明：* **在 Java 中跨工作簿複製範圍 – Aspose.Cells 程式碼範例**（符合主要關鍵字）。

---

## 預期輸出

| 檔案名稱                | 內容 |
|--------------------------|------|
| `destination.xlsx`       | 已複製範圍，且樞紐分析表功能正常。 |
| `destination.pptx`       | 已匯出圖片為可編輯的 PowerPoint 形狀。 |
| `final_output.xlsx`      | 表格已移除 AutoFilter 下拉箭頭。 |
| `template_filled.xlsx`   | JSON 陣列以單一儲存格值儲存。 |

在相應的應用程式（Excel 或 PowerPoint）中開啟每個檔案，即可驗證操作是否成功。

---

## 結論

現在您已掌握如何在 Java 中使用 Aspose.Cells **copy range between workbooks**，同時保留樞紐分析表、將圖片匯出至 PowerPoint，並從 Excel 表格中移除 AutoFilter。相同的模式亦可延伸至複製任意 Excel 範圍至新工作簿、處理 SmartMarker JSON 陣列，或串接其他轉換流程。

接下來可探索的方向：

* **Copy Excel range to new workbook**，支援多工作表。  
* 使用 **export picture to PowerPoint** 進行批次影像抽取。  
* 在更大型的報表管線中 **remove autofilter from excel table**。  
* 結合 Aspose.Slides，實現完整的 Excel → PowerPoint 自動化。

歡迎嘗試不同的範圍地址、複數樞紐分析表或自訂圖片格式。Aspose.Cells API 為程式化彈性而設計，您可以依需求調整本教學所示的模式，以符合任何企業級 Excel 自動化情境。

## 接下來您應該學習什麼？

以下教學與本指南緊密相關，能進一步深化您對 API 功能的掌握，並提供其他實作方式供您在專案中參考。

- [Copy Images Between Sheets in Excel Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Copy Page Setup Settings Between Worksheets in Excel Using Aspose.Cells Java](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [Excel Copy Worksheets Between Workbooks](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}