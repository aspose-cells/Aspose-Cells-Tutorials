---
date: '2026-03-15'
description: 學習如何使用 Aspose.Cells Java 在一步一步的教學中將姓名拆分至不同欄位，並將工作簿儲存為 xlsx。
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – 將姓名拆分為欄位
url: /zh-hant/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 掌握 **aspose cells java**：將姓名拆分為欄位

歡迎閱讀我們的完整 **aspose cells java** 教學。本指南將教您 **如何拆分姓名**，將儲存在單一 Excel 欄位的姓名拆分為兩個欄位——名與姓——使用強大的文字分欄功能。無論您是要清理聯絡人清單、為 CRM 匯入做資料準備，或只是需要快速重構試算表，本教學都會明確示範如何在轉換後 **save workbook xlsx**。

## 快速解答
- **What does this tutorial cover?** 使用 Aspose.Cells for Java 將全名字串拆分為名與姓欄位。  
- **Which library version is used?** 最新的穩定版（截至 2026 年）。  
- **Do I need a license?** 開發階段可使用免費試用版；正式上線需購買商業授權。  
- **Can I split on other delimiters?** 可以，只需在 `TxtLoadOptions` 中更改分隔符。  
- **Is the output an .xlsx file?** 當然，工作簿會以 XLSX 格式儲存。

## 什麼是 **aspose cells java**？
**Aspose.Cells java** 是一個高效能的 Java API，讓開發者能在不需要 Microsoft Office 的情況下建立、修改、轉換與呈現 Excel 檔案。它支援所有主要的 Excel 格式，並提供公式、圖表與資料操作等進階功能。

## 為何使用 **aspose cells java** 來拆分姓名？
- **Zero‑install**：可在任何伺服器端 Java 環境運行。  
- **Speed**：處理大型試算表的速度快於原生 Excel 互操作。  
- **Precision**：可完整控制分隔符、欄位範圍與輸出格式。  
- **Reliability**：無需 COM 或 Office 依賴，適合雲端或容器部署。

## 前置條件
- Java Development Kit (JDK) 8 或更新版本。  
- 如 IntelliJ IDEA 或 Eclipse 等 IDE（可選，但建議使用）。  
- Maven 或 Gradle 用於相依管理。  

### Maven 設定
將 Aspose.Cells 相依加入您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle 設定
將函式庫加入您的 `build.gradle`：

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Pro tip:** 在開發期間使用 Aspose 入口網站提供的臨時授權，以解鎖全部功能。

## 步驟說明實作

### 步驟 1：建立工作簿並存取第一個工作表
首先，匯入核心類別並實例化一個新的工作簿。這會為您提供一個乾淨的 Excel 檔案，準備好插入資料。

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### 步驟 2：以範例姓名填充工作表
接著，將幾筆全名字串加入 **A** 欄。實際專案中，您可能會從資料庫或 CSV 檔讀取這些資料。

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### 步驟 3：設定文字載入選項以進行欄位拆分
`TxtLoadOptions` 類別告訴 Aspose.Cells 如何解析文字。此處我們使用空格 (`' '`) 作為分隔符。

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### 步驟 4：將文字拆分為兩個欄位
現在對包含姓名的儲存格區域呼叫 `textToColumns()`。參數 `(0, 0, 5, opts)` 表示 *從第 0 列、第 0 欄開始，處理 5 列，使用剛才定義的選項*。

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

呼叫完成後，A 欄會保存名，B 欄會保存姓。

### 步驟 5：將工作簿儲存為 XLSX 檔案
最後，將修改後的工作簿寫入磁碟。`SaveFormat` 列舉確保檔案以現代的 XLSX 格式儲存。

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **Why this matters:** 透過使用 **save workbook xlsx**，您可確保與最新版本的 Excel、Google Sheets 以及其他試算表工具相容。

## 實務應用
- **Data Cleaning:** 快速在載入分析管線前分離合併欄位。  
- **CRM Integration:** 將平面聯絡人清單轉換為結構化表格以供匯入。  
- **HR Systems:** 為薪資或福利處理將員工全名拆分。  

## 效能考量
當處理數千列資料時：

1. **Batch Updates:** 使用 `ws.getCells().setRowHeight()` 或類似的批次方法以減少開銷。  
2. **Memory Management:** 僅在必要時呼叫 `wb.calculateFormula()`，並及時釋放大型物件。  
3. **Garbage Collection:** 使用適當的堆積設定（如大型檔案使用 `-Xmx2g`）執行 JVM，以避免 OutOfMemory 錯誤。

## 常見問題與解決方案

| 問題 | 解決方案 |
|-------|----------|
| **姓名包含中間縮寫**（例如 “John A. Doe”） | 調整分隔符或在第二欄後處理以擷取姓氏。 |
| **出現意外的空儲存格** | 確認來源範圍（`textToColumns` 參數）與實際資料列相符。 |
| **找不到授權** | 將臨時授權檔案（`Aspose.Cells.lic`）放置於專案根目錄，或以程式方式設定授權。 |

## 常見問答

**Q: What is Aspose.Cells Java?**  
A: 一個強大的函式庫，允許您使用 Java 程式化地建立、修改與轉換 Excel 檔案。

**Q: Can I split columns based on delimiters other than spaces?**  
A: 可以，依需求自訂 `TxtLoadOptions` 的分隔符即可。

**Q: How do I handle large datasets with Aspose.Cells?**  
A: 如上所述，透過管理記憶體與減少工作簿操作來最佳化效能。

**Q: Is there support available if I encounter issues?**  
A: 前往 [Aspose Forum](https://forum.aspose.com/c/cells/9) 取得社群協助，或直接聯絡 Aspose 支援團隊。

**Q: What formats can Aspose.Cells save workbooks in?**  
A: 支援多種 Excel 檔案格式，包括 XLSX、XLS、CSV 等。

## 資源

- **Documentation**: [Aspose.Cells Java 參考文件](https://reference.aspose.com/cells/java/)
- **Download**: [Aspose.Cells Java 版本下載](https://releases.aspose.com/cells/java/)
- **Purchase**: [購買 Aspose.Cells](https://purchase.aspose.com/buy)
- **Free Trial**: [免費試用 Aspose.Cells](https://releases.aspose.com/cells/java/)
- **Temporary License**: [申請臨時授權](https://purchase.aspose.com/temporary-license/)

祝開發順利，盡情運用 **aspose cells java** 的完整功能於您的專案中！

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**最後更新：** 2026-03-15  
**測試環境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose