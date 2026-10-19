---
category: general
date: 2026-08-11
description: 在 Java 中使用 Aspose 建立新工作簿，新增自訂屬性 Excel，然後將工作簿儲存為 XLSB，並提供完整的逐步範例。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: zh-hant
lastmod: 2026-08-11
og_description: 在 Java 中使用 Aspose 建立新工作簿，新增 Excel 自訂屬性，並將工作簿儲存為 XLSB，提供完整、可直接執行的範例。
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: 建立新工作簿 Aspose – 新增自訂屬性 Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: 建立新工作簿 Aspose – 為 Excel 添加自訂屬性並儲存為 XLSB
url: /zh-hant/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 建立新的 Aspose 工作簿 – 新增自訂屬性 Excel 並儲存為 XLSB

如果您需要在 Java 應用程式中 **create new workbook Aspose**，本指南將會精確說明如何操作。您將學會 **add custom property Excel**、取得其值，並 **save workbook as XLSB**，且不會遺失任何中繼資料。

本教學涵蓋從專案設定到已儲存檔案驗證的全部步驟。無需外部文件說明，只需依照步驟操作並執行程式碼。

## 前置條件

- 已安裝 Java Development Kit (JDK) 8 或更新版本。
- 使用 Maven 或 Gradle 來管理相依性（本範例使用 Maven）。
- 具備有效的 Aspose.Cells for Java 授權（或使用免費評估模式進行測試）。

## 步驟 1：將 Aspose.Cells 加入您的專案

將 Aspose.Cells 的 Maven 套件加入您的 `pom.xml`。此相依性提供建立 **create new workbook Aspose** 物件所需的類別。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **專業提示：** 如果您偏好使用 Gradle，請將 Maven 片段替換為等效的 `implementation "com.aspose:aspose-cells:23.12"` 行。

## 步驟 2：建立新的 Aspose 工作簿

第一個功能步驟是實例化 `Workbook` 物件。此物件在記憶體中代表一個 Excel 檔案，且是所有後續操作的入口點。

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

建立新的 Aspose 工作簿會為您提供一個帶有預設工作表的全新工作簿，已準備好進行自訂。

## 步驟 3：新增自訂屬性 Excel

自訂屬性讓您能在 Excel 檔案中儲存任意的中繼資料。此處我們 **add custom property Excel** 名為 `ProjectId`，且值為數字。

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

`add` 方法接受屬性名稱以及任意支援類型的值（字串、數字、日期等）。此中繼資料會隨檔案一起被複製。

## 步驟 4：取得並顯示自訂屬性

讀回屬性可驗證其是否正確儲存。您亦可在業務邏輯中使用取得的值。

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

轉型為 `int` 可行，因為我們儲存的是數字值。若儲存的是字串，請改用 `(String)`。

## 步驟 5：將工作簿儲存為 XLSB

現在您 **save workbook as XLSB**。XLSB 格式以二進位方式儲存工作簿，開啟速度更快且檔案大小更小。所有自訂屬性會自動保留。

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

若需將檔案儲存於特定目錄，請將 `"WithCustomProps.xlsb"` 替換為絕對路徑。`SaveFormat.XLSB` 列舉告訴 Aspose.Cells 使用二進位格式寫入。

## 步驟 6：驗證輸出

從 IDE 或命令列執行程式：

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

您應該會看到：

```
ProjectId = 12345
```

在 Excel 中開啟 `WithCustomProps.xlsb`。前往 **File → Info → Properties → Advanced Properties → Custom**。會列出 `ProjectId` 及其值 `12345`，證實 **add custom property excel** 步驟成功，且 **save workbook as xlsb** 操作保留了中繼資料。

## 常見問題與邊緣情況

### 如果需要儲存字串屬性該怎麼辦？

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

使用以下方式取得：

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### 是否能一次新增多個自訂屬性？

可以。對每個名稱/值組合重複呼叫 `add`。Aspose.Cells 對自訂屬性的數量沒有限制，但請保持總大小在合理範圍內，以免檔案過大。

### 二進位格式如何影響效能？

XLSB 檔案載入更快，因為省略了 XML 解析。對於包含大量列、公式或嵌入圖像的工作簿，差異尤為明顯。

### 如果需要處理現有的 XLSX 檔案該怎麼辦？

將 `new Workbook()` 建構子改為 `new Workbook("ExistingFile.xlsx")`。其餘步驟（新增屬性、儲存為 XLSB）保持不變。

## 完整原始碼

以下為完整、可直接執行的範例。請將其複製到 `src/main/java` 資料夾下，檔名為 `CustomPropertiesXlsb.java`。

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

執行此類別會產生包含自訂屬性的 XLSB 檔案，且可在任何新版 Microsoft Excel 中開啟。

## 結論

您現在已了解如何使用 Java **create new workbook Aspose**、**add custom property Excel**，以及 **save workbook as XLSB**。此範例展示了完整的生命週期：初始化、注入中繼資料、驗證與二進位序列化。

接下來，您可以探索相關主題，例如 **setting document properties**、**working with Excel formulas**，或 **converting between XLSX and XLSB**。這些皆基於您剛使用的 Aspose.Cells API，無需學習新函式庫即可擴充解決方案。

歡迎嘗試不同的資料類型、多張工作表或密碼保護——Aspose.Cells 內建支援所有這些情境。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南技術緊密相關的主題。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您精通其他 API 功能，並在專案中探索替代實作方式。

- [建立與儲存 Excel 工作簿 Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 建立並儲存 Excel 工作簿為 SVG](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [使用 Aspose.Cells for Java 建立 Excel 工作簿並新增標籤](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}