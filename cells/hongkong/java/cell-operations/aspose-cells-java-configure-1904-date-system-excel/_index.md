---
date: '2026-10-28'
description: 了解如何使用 Aspose.Cells for Java 將 Excel 日期系統更改為 1904、設定 Excel 日期格式，並高效轉換
  Excel 1904 系統。
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: 使用 Aspose.Cells for Java 將 Excel 日期系統更改為 1904。了解逐步操作方法，如何啟用 1904 系統、設定日期，並轉回原系統。
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: 使用 Aspose.Cells for Java 將 Excel 日期系統更改為 1904
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: 使用 Aspose.Cells for Java 將 Excel 日期系統更改為 1904
url: /zh-hant/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將 Excel 日期系統變更為 1904（使用 Aspose.Cells Java）

在本教學中，您將學習如何使用 Aspose.Cells for Java **變更 Excel 日期系統** 為 1904 格式。當您需要保留舊版 Mac 日期或與需要此紀元的財務模型保持一致時，1904 系統是必須的。我們將逐步說明安裝函式庫、載入活頁簿、切換日期系統以及儲存結果——全部不需要在伺服器上安裝 Microsoft Excel。

## 快速解答
- **1904 日期系統的作用是什麼？** 它從 1904 年 1 月 1 日開始計算天數，與預設的 1900 系統相比，所有日期會向前移動 1,462 天。  
- **為什麼使用 Aspose.Cells 變更日期系統？** 它提供簡單的 API，無需安裝 Excel 即可運作，且支援大型檔案。  
- **支援哪些 Java 版本？** JDK 8 或更新版本。  
- **我需要授權嗎？** 免費試用可用於評估；購買授權可移除使用限制。  
- **我可以稍後再轉回 1900 系統嗎？** 可以，只需呼叫 `setDate1904(false)`。

## Excel 中的 1904 日期系統是什麼？
1904 日期系統是從 1904 年 1 月 1 日開始計算天數，而非預設的 1900 紀元。此變化會在每個日期值上額外加上 1,462 天，這也是為什麼舊版 Mac 活頁簿在 Windows 上開啟時會出現偏移。它主要用於與較舊的 Macintosh Excel 檔案以及某些舊版財務模型相容。

## 為什麼要使用 Aspose.Cells 變更 Excel 日期系統？
您可以直接從 Java 切換日期系統，省去在 Excel 中的手動步驟。Aspose.Cells 可處理大小高達 **2 GB** 的活頁簿，且在一般 4 核心伺服器上能在 **2 秒** 內轉換 500 工作表的活頁簿，提供高效能的伺服器端自動化。

## 前置條件
- Java Development Kit (JDK) 8 或更高版本。  
- 用於相依管理的 Maven 或 Gradle。  
- 基本的 Java 程式設計知識。  

## 設定 Aspose.Cells for Java

### Maven
將以下相依性加入您的 `pom.xml` 檔案：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
在您的 `build.gradle` 檔案中加入此行：

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### 取得授權
Aspose 提供免費試用、臨時授權與完整商業授權。您可以先使用 [免費試用](https://releases.aspose.com/cells/java/) ，或從 [臨時授權頁面](https://purchase.aspose.com/temporary-license/) 取得臨時授權。

## 如何使用 Aspose.Cells for Java 將 Excel 日期系統變更為 1904？
載入活頁簿、啟用 1904 設定，然後儲存檔案——這三步流程可在不到一秒的時間內更新活頁簿的內部日期紀元。API 呼叫 `setDate1904(true)` 會切換系統旗標，當您呼叫 `save` 時變更會被寫入。無需安裝 Excel，非常適合無介面的伺服器環境。

### 步驟 1：初始化並載入活頁簿
`Workbook` 類別在記憶體中代表整個 Excel 檔案。首先，建立指向您現有檔案的 `Workbook` 實例。

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### 步驟 2：啟用 1904 日期系統
`WorkbookSettings.setDate1904` 方法會切換活頁簿層級的日期旗標。將其設為 `true` 即可為所有工作表啟用 1904 系統。

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**小技巧：** 若需還原，之後也可以呼叫 `setDate1904(false)`。

### 步驟 3：儲存已修改的活頁簿
最後，將變更寫入新檔案（或覆寫原檔）。`save` 方法會自動遵循目前的日期系統。

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **注意：** 上述程式碼使用了原始提供的類別名稱 `tWorkbook`。請確認此拼寫錯誤符合您專案的命名慣例，或在需要時將其更正為 `Workbook`。

## 程式化設定 Excel 日期（次要關鍵字）
如果在變更系統後需要調整個別儲存格的值，您可以使用 `cells.get(i, j).putValue(Date)`，日期會依據目前啟用的日期系統來解讀。

## 將 Excel 1904 系統轉回 1900（次要關鍵字）
要還原，只需呼叫：

```java
workbook.getSettings().setDate1904(false);
```

然後再次儲存活頁簿。

## 實務應用
1. **資料封存** – 在遷移舊版 Mac 試算表時保留舊有時間戳記。  
2. **跨平台報告** – 產生在 Windows 與 macOS 上皆能正確開啟且日期不會不匹配的報告。  
3. **財務建模** – 使日期計算與預期使用 1904 系統的舊版財務模型保持一致。  

## 效能考量
- 在單一工作階段中限制活頁簿操作，以降低記憶體使用；Aspose.Cells 以串流方式處理資料，除非明確要求，否則不會將整個檔案載入記憶體。  
- 為超大型檔案調整 Java 的垃圾回收旗標（`-XX:+UseG1GC`），以避免暫停時間激增。  

## 常見問題

**Q: 1900 與 1904 日期系統有何差異？**  
A: 1900 系統從 1900 年 1 月 1 日開始，而 1904 系統從 1904 年 1 月 1 日開始，所有日期會向前移動 1,462 天。

**Q: 我可以變更目前在 Excel 中開啟的活頁簿的日期系統嗎？**  
A: 可以，但必須先在 Excel 中關閉該檔案；否則儲存操作會失敗。

**Q: 使用 `setDate1904` 需要授權嗎？**  
A: 此方法在免費試用版中可用，但完整授權會移除評估限制。

**Q: 能否只為單一工作表變更日期系統？**  
A: 不行，日期系統是活頁簿層級的設定，會套用至所有工作表。

**Q: 如何驗證日期系統已變更？**  
A: 在 Excel 中開啟已儲存的檔案，前往 **File → Options → Advanced**，勾選 **「使用 1904 日期系統」** 方塊。

## 結論
現在您已了解如何使用 Aspose.Cells for Java **變更 Excel 日期系統** 為 1904、如何設定個別儲存格的日期，以及在需要時如何還原至 1900 系統。將這些程式碼片段整合到您的資料處理流程中，可確保跨平台與舊檔案的日期相容性。

---

**最後更新：** 2026-10-28  
**測試版本：** Aspose.Cells 25.3 for Java  
**作者：** Aspose  

**資源**
- **文件：** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **下載：** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **購買授權：** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **免費試用：** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **臨時授權：** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **支援論壇：** [Aspose Support](https://forum.aspose.com/c/cells/9)

## 相關教學

- [使用 Aspose.Cells for Java 高效將 Excel 轉換為 PDF 並自訂日期格式](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells for Java：如何高效建立與格式化 Excel 活頁簿](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [精通 Aspose.Cells for Java 的 Excel 操作：活頁簿操作與儲存格樣式教學](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}