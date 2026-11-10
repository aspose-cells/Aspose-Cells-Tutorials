---
category: general
date: 2026-10-01
description: 學習如何在 Java 中使用 ShapeExportOptions 匯出形狀，並在使用 Aspose.Cells 轉換為 PPTX 時保持形狀可編輯。
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export shape with ShapeExportOptions
- Aspose Cells export shape
- Java export shape to PPTX
- editable shape export
- ShapeExportOptions setExportAsEditable
- export textbox shape
language: zh-hant
lastmod: 2026-10-01
og_description: 使用 Java 的 ShapeExportOptions 匯出圖形，以建立可編輯的 PPTX 檔案。本教學將帶領您使用 Aspose.Cells
  完整步驟。
og_image_alt: Screenshot showing Java code exporting a textbox shape to PPTX using
  ShapeExportOptions
og_title: 在 Java 中使用 ShapeExportOptions 匯出形狀 – 步驟指南
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  headline: How to export shape with ShapeExportOptions in Java
  type: TechArticle
- description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  name: How to export shape with ShapeExportOptions in Java
  steps:
  - name: Expected result
    text: '- `textbox.pptx` appears in the specified directory. - Opening the file
      in PowerPoint shows a single slide with the original textbox. - The textbox
      is fully editable (you can change text, font, size, etc.).'
  - name: Verify programmatically
    text: '```java // Load the generated PPTX to confirm it contains one slide Presentation
      presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx"); int slideCount
      = presentation.getSlides().size(); System.out.println("Slides in exported PPTX:
      " + slideCount); ```'
  - name: 'Edge case: Multiple shapes'
    text: 'If the worksheet contains several shapes and you only want a specific one,
      locate it by name:'
  - name: 'Edge case: Shape not found'
    text: '```java if (worksheet.getShapes().size() == 0) { throw new IllegalStateException("No
      shapes found on the worksheet."); } ```'
  - name: 'Edge case: Export to other formats'
    text: '`ShapeExportOptions` also supports PNG, JPEG, SVG, and EMF. Change the
      file extension and optionally set `exportOptions.setImageFormat(ImageFormat.PNG)`.'
  - name: Conclusion
    text: You now know how to **export shape with ShapeExportOptions** in Java, preserving
      editability when converting a textbox (or any other shape) to a PPTX file. By
      following the steps above—setting up the library, loading the workbook, configuring
      `ShapeExportOptions`, and invoking `exportToImage`—you ca
  type: HowTo
tags:
- Aspose.Cells
- Java
- ShapeExportOptions
- PPTX
- Export
title: 如何在 Java 中使用 ShapeExportOptions 匯出圖形
url: /zh-hant/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 ShapeExportOptions 匯出圖形

如果您需要從 Excel 活頁簿 **export shape with ShapeExportOptions** 匯出圖形，本指南將向您展示具體步驟。您將了解在將圖形轉換為 PPTX 檔案時如何保持圖形可編輯，這對於在 PowerPoint 中的後續編輯至關重要。

在從試算表產生投影片組時，匯出圖形是一項常見任務——無論您是製作銷售簡報、報告儀表板，或是自動化簡報。本教學涵蓋您所需的全部內容，從專案設定到驗證匯出檔案，並使用 **Aspose.Cells for Java** 函式庫。

## 您需要的條件

- Java 17 或更新版本（程式碼可在任何近期的 JDK 上編譯）
- Maven 或 Gradle 用於相依性管理
- 一個 Excel 檔案（`Shapes.xlsx`），其中至少包含一個文字方塊或其他圖形
- 對 Aspose.Cells API 有基本了解

## 步驟 1：將 Aspose.Cells 加入您的專案（Aspose Cells export shape）

如果您使用 Maven，請將以下相依性加入您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest stable version -->
</dependency>
```

若使用 Gradle，請將以下內容放入 `build.gradle`：

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** 盡早註冊授權以避免評估水印。  
> ```java
> License license = new License();
> license.setLicense("Aspose.Total.Java.lic");
> ```

## 步驟 2：載入包含圖形的活頁簿

```java
// Load the workbook that contains the shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

`Workbook` 物件代表整個 Excel 檔案。載入它是進行任何圖形操作的第一個前提條件。

## 步驟 3：存取工作表並取得目標圖形（Java export shape to PPTX）

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);

// Retrieve the first shape on the sheet.
// You can also use get("ShapeName") if you know the shape's name.
Shape textBoxShape = worksheet.getShapes().get(0);
```

> **Why this matters:** 圖形是依工作表儲存的，因此在匯出特定圖形之前，必須先切換至正確的工作表。

## 步驟 4：設定 **ShapeExportOptions** 以保持圖形可編輯（editable shape export）

```java
// Create export options and enable editable export
ShapeExportOptions exportOptions = new ShapeExportOptions();
exportOptions.setExportAsEditable(true); // <-- makes the shape editable in PPTX
```

將 `ExportAsEditable` 設為 `true` 會告訴 Aspose.Cells 保留圖形的向量資料，讓 PowerPoint 使用者在匯入後仍能修改圖形。

## 步驟 5：直接將圖形匯出為 PPTX 檔案（export textbox shape）

```java
// Export the shape as a PPTX file
textBoxShape.exportToImage("YOUR_DIRECTORY/textbox.pptx", exportOptions);
```

`exportToImage` 方法支援多種影像格式；當目標檔名以 `.pptx` 結尾時，Aspose.Cells 會寫入包含該圖形的 PowerPoint 投影片。

### 預期結果

- `textbox.pptx` 會出現在指定的目錄中。
- 在 PowerPoint 中開啟該檔案會顯示只有一張投影片，內容為原始的文字方塊。
- 文字方塊可完全編輯（您可以變更文字、字型、大小等）。

## 步驟 6：驗證輸出並處理常見的例外情況

### 程式化驗證

```java
// Load the generated PPTX to confirm it contains one slide
Presentation presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx");
int slideCount = presentation.getSlides().size();
System.out.println("Slides in exported PPTX: " + slideCount);
```

如果 `slideCount` 等於 `1`，則表示匯出成功。

### 例外情況：多個圖形

如果工作表中有多個圖形且您只想取得特定的圖形，可依名稱定位：

```java
Shape targetShape = worksheet.getShapes().get("MyTextBox");
targetShape.exportToImage("output.pptx", exportOptions);
```

### 例外情況：找不到圖形

```java
if (worksheet.getShapes().size() == 0) {
    throw new IllegalStateException("No shapes found on the worksheet.");
}
```

### 例外情況：匯出為其他格式

`ShapeExportOptions` 亦支援 PNG、JPEG、SVG 與 EMF。變更檔案副檔名，並可選擇設定 `exportOptions.setImageFormat(ImageFormat.PNG)`。

## 完整、可執行的範例

將所有程式碼組合起來，即可得到一個可自行執行的程式，您可以直接複製貼上到 IDE 中：

```java
import com.aspose.cells.*;

public class ExportShapeExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");

        // 2️⃣ Get first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Retrieve the first shape (or use get("ShapeName"))
        Shape shape = worksheet.getShapes().get(0);

        // 4️⃣ Prepare export options for editable PPTX
        ShapeExportOptions options = new ShapeExportOptions();
        options.setExportAsEditable(true); // keep shape editable

        // 5️⃣ Export to PPTX
        String outPath = "YOUR_DIRECTORY/textbox.pptx";
        shape.exportToImage(outPath, options);
        System.out.println("Shape exported to " + outPath);

        // 6️⃣ Optional verification
        Presentation pres = new Presentation(outPath);
        System.out.println("Slide count: " + pres.getSlides().size());
    }
}
```

執行程式後會產生 `textbox.pptx`。在 PowerPoint 中開啟它，右鍵點擊文字方塊，即可看到常見的編輯控制點——證實 **export shape with ShapeExportOptions** 已保留可編輯性。

## 常見問題

| 問題 | 答案 |
|----------|--------|
| *我可以匯出圖表圖形嗎？* | 可以。相同的 `exportToImage` 呼叫同時適用於圖表、影像與 SmartArt。 |
| *如果需要更高解析度的 PNG 該怎麼辦？* | 在匯出前設定 `options.setImageFormat(ImageFormat.PNG)` 並將 `options.setResolution(300)` 調整為更高的解析度。 |
| *匯出的 PPTX 能相容舊版 PowerPoint 嗎？* | 此函式庫會產生 Office Open XML (PPTX) 格式，支援 PowerPoint 2007 及之後的版本。 |
| *執行此功能是否需要授權？* | 免費評估版可使用，但會加上浮水印。註冊授權即可移除浮水印。 |

## 後續步驟

- 若需將多個匯出的圖形合併為單一投影片組，請探索 **Aspose.Slides for Java**。
- 當您偏好使用點陣圖（PNG/JPEG）以加快渲染速度時，可使用 **ShapeExportOptions.setExportAsEditable(false)**。
- 自動化批次處理：遍歷所有工作表，將每個圖形匯出為獨立的 PPTX 檔案。

---

### 結論

您現在已了解如何在 Java 中 **export shape with ShapeExportOptions**，在將文字方塊（或任何其他圖形）轉換為 PPTX 檔案時保留可編輯性。只要依照上述步驟——設定函式庫、載入活頁簿、配置 `ShapeExportOptions`，以及呼叫 `exportToImage`——即可將圖形匯出整合至任何自動化報告流程中。

歡迎嘗試不同的圖形、輸出格式與解析度設定。如果您覺得本指南有幫助，請與同事分享或將其加入書籤以備未來參考。祝開發愉快！

## 接下來該學什麼？

以下教學涵蓋與本指南緊密相關的主題，進一步延伸所示技巧。每個資源皆提供完整可執行的程式碼範例與逐步說明，協助您掌握更多 API 功能，並在專案中探索其他實作方式。

- [如何在 Excel 中使用 Aspose.Cells for Java 調整圖形邊距](/cells/english/java/images-shapes/excel-aspose-cells-java-shape-margins/)
- [如何在 Excel 中使用 Aspose.Cells for Java 套用 3D 圖形格式](/cells/english/java/images-shapes/aspose-cells-java-3d-shape-formatting/)
- [Aspose Cells Java 活頁簿圖形複製指南](/cells/hindi/java/images-shapes/aspose-cells-java-workbook-shape-copying-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}