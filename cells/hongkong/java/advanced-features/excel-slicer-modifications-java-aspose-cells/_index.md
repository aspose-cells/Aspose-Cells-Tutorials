---
date: '2026-05-18'
description: 了解如何使用 Aspose.Cells for Java 在 Excel 中為樞紐分析表新增切片器——載入活頁簿、客製化切片器，並有效儲存
  Excel 檔案。
keywords:
- add slicer to pivot
- save excel file java
- load excel workbook java
- Aspose.Cells Java
- Excel slicer automation
schemas:
- author: Aspose
  dateModified: '2026-05-18'
  description: Learn how to add slicer to pivot in Excel using Aspose.Cells for Java—load
    workbooks, customize slicers, and save Excel files efficiently.
  headline: How to Add Slicer to Pivot in Excel Using Aspose.Cells for Java
  type: TechArticle
- questions:
  - answer: Yes, it handles formulas, charts, pivot tables, conditional formatting,
      and more across 50+ formats.
    question: Does Aspose.Cells support other Excel features besides slicers?
  - answer: Absolutely. Aspose.Cells works with Java 8, 11, 17, and 21.
    question: Is the library compatible with Java 11 and newer?
  - answer: Yes. Because Aspose.Cells is pure Java, it runs on any OS with a compatible
      JVM.
    question: Can I run this code on a Linux server?
  - answer: Call `slicer.setStyleType(SlicerStyleType.YOUR_CHOSEN_STYLE);` where the
      enum provides dozens of predefined styles.
    question: How do I apply a custom style to a slicer?
  - answer: The Aspose.Cells documentation and the official GitHub repository contain
      extensive examples for slicers, pivot tables, and chart automation.
    question: Where can I find more code samples?
  type: FAQPage
title: 如何在 Excel 中使用 Aspose.Cells for Java 為樞紐分析表新增切片器
url: /zh-hant/java/advanced-features/excel-slicer-modifications-java-aspose-cells/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells for Java 在 Excel 中為樞紐分析表新增切片器

## 介紹

如果您希望以程式方式 **為樞紐分析表新增切片器**，Aspose.Cells for Java 提供純 Java API，無需 Microsoft Office 即可處理切片器。在許多報表專案中，開發人員需要花費數小時手動調整切片器；使用此函式庫，您可以在數秒內自動化這些變更，提高一致性，並在各環境中保持儀表板即時更新。本指南將帶您了解顯示版本資訊、**載入 Excel 活頁簿 (Java)**、存取工作表、自訂切片器屬性，最後 **儲存 Excel 檔案 (Java)**。

## 快速答覆
- **哪個函式庫支援切片器自動化？** Aspose.Cells for Java  
- **我可以以程式方式為樞紐分析表新增切片器嗎？** 可以 – 使用 `Slicer` 類別  
- **在正式環境是否需要授權？** 評估可使用免費試用版；商業使用需購買授權  
- **支援哪些 Java 版本？** JDK 8 及以上（含 11、17、21）  
- **在哪裡可以找到 Maven 相依性？** 在 Maven Central 上的 `com.aspose:aspose-cells`

## 在此情境下「為樞紐分析表新增切片器」是什麼意思？

**為樞紐分析表新增切片器** 指以程式方式建立或修改切片器，讓其控制樞紐分析表的篩選條件，使用者即可互動式地切分資料。透過 Aspose.Cells API，您可以設定切片器的位置、樣式與關聯欄位，然後將其附加至一個或多個樞紐分析表，使切片器的變更即時篩選底層資料，免除手動操作。

## 為什麼要使用 Aspose.Cells 進行 Excel 切片器自動化？

Aspose.Cells 支援 **50 多種輸入與輸出格式**，且可在不將整個檔案載入記憶體的情況下處理 **多達 10,000 列** 的活頁簿，提供 Windows、Linux 與 macOS 上的高效能自動化。此函式庫讓您完整掌控切片器的外觀、樣式與關聯的樞紐分析表，省去 COM 相依性並降低執行時開銷。

## 先決條件

- Java Development Kit (JDK) 8 或更新版本  
- IntelliJ IDEA、Eclipse 等 IDE  
- Maven 或 Gradle 進行相依性管理  

### 必要的函式庫與相依性

我們將使用 Aspose.Cells for Java，這是一套強大的函式庫，可在 Java 應用程式中操作 Excel 檔案。以下為安裝細節：

**Maven:**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 取得授權

Aspose.Cells for Java 提供免費試用版供您快速上手。若需大量使用，可取得臨時授權或購買正式授權。請前往 [purchase Aspose](https://purchase.aspose.com/buy) 了解更多選項。

## 設定 Aspose.Cells for Java

在 Java 檔案的最上方加入必要的匯入語句：

```java
import com.aspose.cells.*;
```

確保資料目錄正確設定：

```java
String dataDir = "YOUR_DATA_DIRECTORY";
String outDir = "YOUR_OUTPUT_DIRECTORY";
```

## 如何使用 Aspose.Cells 在 Excel 中為樞紐分析表新增切片器？

要新增切片器，首先載入活頁簿，找到包含目標樞紐分析表的工作表，然後建立與該樞紐分析表關聯的 `Slicer` 物件。設定其樣式、位置與要篩選的欄位，最後儲存活頁簿。此流程確保切片器完整運作且正確連結至樞紐分析表，為最終使用者提供互動式篩選體驗。

### 顯示 Aspose.Cells for Java 版本

`VersionInfo` 類別提供目前 Aspose.Cells 函式庫的版本資訊。  
```java
public class VersionDisplay {
    public static void displayVersion() throws Exception {
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

### 載入 Excel 活頁簿 (Java)

`Workbook` 類別代表已載入記憶體的完整 Excel 檔案。  
```java
public class LoadExcelFile {
    public static Workbook loadWorkbook() throws Exception {
        return new Workbook(dataDir + "/sampleFormattingSlicer.xlsx");
    }
}
```

### 存取工作表

`Worksheet` 物件對應活頁簿中的單一工作表。  
```java
public class AccessWorksheet {
    public static Worksheet getFirstWorksheet(Workbook wb) throws Exception {
        return wb.getWorksheets().get(0);
    }
}
```

### 自訂 Excel 儀表板切片器

`Slicer` 類別封裝與樞紐分析表關聯的切片器，允許自訂篩選設定。  
```java
public class ModifySlicerProperties {
    public static void configureSlicer(Worksheet ws) throws Exception {
        Slicer slicer = ws.getSlicers().get(0);
        
        // Set number of columns displayed by the slicer
        slicer.setNumberOfColumns(2);
        
        // Change the style type for better visual appeal
        slicer.setStyleType(SlicerStyleType.SLICER_STYLE_LIGHT_6);
    }
}
```

### 儲存 Excel 檔案 (Java)

`Workbook` 的 `save` 方法將修改後的活頁簿寫入檔案。  
```java
public class SaveWorkbook {
    public static void saveModifiedWorkbook(Workbook wb) throws Exception {
        wb.save(outDir + "/outputFormattingSlicer.xlsx", SaveFormat.XLSX);
    }
}
```

## 常見問題與解決方案

- **切片器儲存後未顯示：** 確認切片器已連結至現有的樞紐分析表，且 `setShowHeader` 設為 `true`。  
- **大型檔案效能下降：** 僅處理必要的工作表，並使用 `WorkbookSettings.setRecalcMode(RecalcMode.Manual)` 停用自動重新計算。  
- **樣式未套用：** 檢查所選的 `SlicerStyleType` 是否在目標 Excel 版本中受支援。

## 常見問答

**Q: Aspose.Cells 是否支援除切片器之外的其他 Excel 功能？**  
A: 支援，包含公式、圖表、樞紐分析表、條件格式等，覆蓋 50 多種格式。

**Q: 此函式庫是否相容於 Java 11 及更新版本？**  
A: 完全相容。Aspose.Cells 可在 Java 8、11、17、21 上執行。

**Q: 我可以在 Linux 伺服器上執行此程式碼嗎？**  
A: 可以。因為 Aspose.Cells 為純 Java 函式庫，只要 JVM 相容，即可在任何作業系統上執行。

**Q: 如何為切片器套用自訂樣式？**  
A: 呼叫 `slicer.setStyleType(SlicerStyleType.YOUR_CHOSEN_STYLE);`，其中列舉提供數十種預設樣式。

**Q: 哪裡可以找到更多程式碼範例？**  
A: Aspose.Cells 官方文件與 GitHub 倉庫中提供大量關於切片器、樞紐分析表與圖表自動化的範例。

## 結論

本教學說明了如何使用 Aspose.Cells for Java 在 Excel 中 **為樞紐分析表新增切片器**——檢查函式庫版本、**載入 Excel 活頁簿 (Java)**、存取正確的工作表、**自訂 Excel 儀表板切片器**，最後 **儲存 Excel 檔案 (Java)**。透過自動化這些步驟，您可以建立動態、互動式的儀表板，省去手動操作的繁瑣。

**下一步：**  
- 嘗試不同的 `SlicerStyleType` 以符合企業品牌形象。  
- 結合切片器自動化與樞紐分析表資料重新整理，打造全自動化的報表管線。  

準備好在自己的專案中實作這些技巧了嗎？立即試試看吧！

---

**最後更新：** 2026-05-18  
**測試環境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose  

{{< blocks/products/products-backtop-button >}}

## 相關教學

- [Master Aspose.Cells for Java: Efficiently Load and Access Pivot Tables in Excel](/cells/java/data-analysis/aspose-cells-java-load-pivot-tables/)
- [Save Excel File Java & Update Slicers with Aspose.Cells](/cells/java/advanced-features/update-slicers-java-excel-aspose-cells/)
- [Refresh Excel Slicer and Customize with Aspose.Cells for Java](/cells/java/advanced-features/customize-slicers-excel-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}