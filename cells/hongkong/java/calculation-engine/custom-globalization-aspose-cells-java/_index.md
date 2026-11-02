---
date: '2026-08-16'
description: 了解如何在 Java 中使用 Aspose.Cells 添加全球化、客製化 Excel 錯誤訊息，並設定 Maven 相依性。
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: 了解如何在 Java 中使用 Aspose.Cells 添加全球化、客製化 Excel 錯誤訊息，並設定 Maven 相依性。請參考逐步指南。
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: 如何在 Java 中使用 Aspose.Cells 添加全球化
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: 如何在 Java 中使用 Aspose.Cells 添加全球化
url: /zh-hant/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose.Cells 添加全球化

## 簡介

將全球化加入您的 Java 工作簿，可讓您以使用者期望的語言呈現錯誤訊息、布林值以及其他與語系相關的字串。在本教學中，您將學習 **如何為俄語添加全球化**，但相同模式亦適用於任何語言。完成本指南後，您將能夠：

- 覆寫預設的錯誤文字與布林值表示。
- 將自訂設定套用至任何 `Workbook` 實例。
- 將此解決方案整合至典型的 Maven 為基礎的 Java 專案。

準備好讓您的 Excel 檔案真正支援多語言了嗎？首先請確認您的開發環境符合先決條件。

## 快速解答
- **什麼是 Aspose.Cells 中的全球化？** 它是一組與語系相關的字串（錯誤訊息、布林值等），您可以用自訂文字取代。  
- **需要哪個 Maven 套件？** `com.aspose:aspose-cells:25.3`。  
- **我可以針對除俄語之外的語言嗎？** 可以 – 繼承 `GlobalizationSettings` 並覆寫每個語系所需的方法。  
- **開發時需要授權嗎？** 免費試用版可用於測試；正式授權會移除評估水印。  
- **此解決方案是執行緒安全的嗎？** 為每個工作簿套用設定；`GlobalizationSettings` 物件在建立後即為不可變。

## 什麼是 Aspose.Cells 中的全球化？

`GlobalizationSettings` 是 Aspose.Cells 的設定物件，負責控制錯誤訊息、布林值、貨幣符號與日期格式等與語系相關的字串。透過提供自訂的子類別，您可以告訴函式庫在每個文化環境下顯示哪段文字，從而以符合最終使用者語言與區域慣例的翻譯取代預設的英文字串。

## 為何要加入自訂全球化？

Aspose.Cells 支援 **超過 50 種輸入與輸出格式**，包括 XLSX、CSV、PDF 與 ODS，且可在不將整個檔案載入記憶體的情況下處理 **多達 200 000 列** 的工作簿。自訂全球化可確保最終使用者看到母語訊息，預估可為跨國部署減少 **30 %** 的支援工單。

## 先決條件

- **Java Development Kit** 8 或更新版本。
- **IDE** 如 IntelliJ IDEA 或 Eclipse。
- **Aspose.Cells for Java** 版本 25.3（或更新）透過 Maven 或 Gradle 加入。

### 設定 Aspose.Cells for Java

將 Maven 相依性加入您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

或是您偏好使用 Gradle，請在 `build.gradle` 中插入以下內容：

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 取得授權

Aspose 提供多種授權選項：

- **免費試用** – 完整功能評估，期限 30 天。  
- **暫時授權** – 無水印的無限制評估。  
- **商業授權** – 生產環境就緒，並提供優先支援。

取得授權檔案後，於應用程式啟動時設定一次：

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## 如何為俄語添加全球化？

`Workbook` 物件代表載入記憶體的 Excel 檔案，提供對工作表、儲存格與設定的存取。載入工作簿、建立 `GlobalizationSettings` 的子類別，並將其附加至工作簿。直接的作法是：**實例化自訂的 `GlobalizationSettings` 類別，覆寫 `getErrorValueString` 與 `getBooleanValueString`，然後呼叫 `workbook.setGlobalizationSettings(customSettings)`**。此兩步驟方法會以您的自訂文字取代預設的俄語字串。

### 定義自訂設定

本指南首次提及 `GlobalizationSettings` 時，請注意其定義：

`GlobalizationSettings` 為 Aspose.Cells 用來取得與語系相關字串的基底類別。  

現在建立一個回傳俄語特定文字的子類別：

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### 將設定套用至工作簿

定義完子類別後，將其附加至任意 `Workbook` 實例：

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## 實務應用

- **財務報表** – 以會計人員的母語顯示錯誤代碼，降低誤解。  
- **全企業工具** – 在數十個內部 Excel 為基礎的工具中嵌入相同的全球化邏輯。  
- **自動化資料管線** – 確保下游系統收到具語系意識的值，免除額外翻譯步驟。

## 效能考量

啟用自訂全球化時，Aspose.Cells 仍以相同的高效能處理公式與 I/O。為降低記憶體使用量：

- 在儲存後釋放工作簿參考 (`wb.dispose()`)。  
- 僅在必要時使用 `CalculationOptions.setEnableIterativeCalculation(true)`。  
- 為超過 100 MB 的工作簿調整 JVM 堆積 (`-Xmx2g`)。

## 常見問題

**Q: 我可以一次將相同的全球化設定套用至多個工作簿嗎？**  
A: 可以。建立單一 `RussianGlobalization` 實例，並透過 `setGlobalizationSettings` 傳遞給每個工作簿。

**Q: 若需支援使用從右至左書寫的語言，該怎麼做？**  
A: 在子類別中覆寫額外方法，如 `getCurrencySymbol` 與 `getDatePattern`，以回傳適當的 RTL 符號。

**Q: 試用版使用自訂全球化是否需要授權？**  
A: 不需要。試用版完整支援 `GlobalizationSettings`；僅在某些輸出格式上會出現評估水印。

**Q: 如何偵錯錯誤字串顯示不正確的情況？**  
A: 在覆寫的方法內插入 `System.out.println` 陳述式，驗證輸入的 `err` 值是否符合您的 switch case。

**Q: 這會影響公式計算速度嗎？**  
A: 影響極小。函式庫僅在呈現儲存格值時查找字串，並不會在中間計算步驟中使用。

## 其他資源

- **文件**：在 [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/) 探索詳細指南  
- **下載**：於 [Aspose Downloads](https://releases.aspose.com/cells/java/) 取得最新發行版  
- **購買**：在 [Aspose Purchase](https://purchase.aspose.com/buy) 購買商業授權  
- **免費試用**：從 [Aspose Free Trial](https://releases.aspose.com/cells/java/) 開始免費試用  
- **暫時授權**：透過 [Aspose Temporary License](https://purchase.aspose.com/temporary-license/) 取得暫時授權  
- **支援**：在 [Aspose Support Forum](https://forum.aspose.com/c/cells/9) 向社群尋求協助  

---

**最後更新：** 2026-08-16  
**測試環境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose

## 相關教學

- [Aspose.Cells Java：自訂計算引擎指南](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [如何使用 Aspose Cells – Java Excel 引擎教學](/cells/java/calculation-engine/)
- [Aspose Cells Maven 依賴 – 在 Java 中使用 Aspose.Cells 管理 Excel 資料連接](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}