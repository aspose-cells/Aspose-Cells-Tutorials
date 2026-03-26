---
date: '2026-02-22'
description: 學習如何使用 Aspose.Cells for Java 將 Excel 日期系統更改為 1904、設定 Excel 日期格式，並高效轉換
  Excel 1904 系統。
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: 使用 Aspose.Cells Java 將 Excel 日期系統改為 1904
url: /zh-hant/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

. We'll use Chinese punctuation for readability.

Now produce final translation.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells Java 將 Excel 日期系統變更為 1904

管理 Excel 中的歷史資料可能相當具挑戰性，因為 Excel 支援兩種不同的日期系統。**在本教學中，你將學會如何使用 Aspose.Cells for Java 將 Excel 日期系統變更為 1904 格式**，讓處理舊有日期變得輕鬆。我們將逐步說明如何初始化活頁簿、啟用 1904 日期系統，並將變更寫入檔案。

## 快速解答
- **1904 日期系統的作用是什麼？** 它從 1904 年 1 月 1 日開始計算天數，與預設的 1900 系統相比會將所有日期向前平移 1462 天。  
- **為什麼要使用 Aspose.Cells 變更日期系統？** 它提供簡易的 API，無需安裝 Excel，且支援大型檔案。  
- **支援哪些 Java 版本？** JDK 8 或更新版本。  
- **需要授權嗎？** 免費試用可用於評估；購買授權後可移除使用限制。  
- **之後可以再轉回 1900 系統嗎？** 可以，只要呼叫 `setDate1904(false)` 即可。

## 什麼是 Excel 中的 1904 日期系統？
1904 日期系統最初由早期的 Macintosh 版 Excel 使用。它從 1904 年 1 月 1 日開始計算天數，對於相容舊版試算表及某些財務模型相當有用。

## 為什麼要使用 Aspose.Cells 變更 Excel 日期系統？
- **跨平台相容性** – 可在 Windows、Linux 與 macOS 上執行。  
- **不需安裝 Excel** – 非常適合伺服器端處理。  
- **高效能** – 能以最小記憶體開銷處理大型活頁簿。  

## 前置條件
- Java Development Kit (JDK) 8 或以上。  
- Maven 或 Gradle 以管理相依性。  
- 基本的 Java 程式設計知識。  

## 設定 Aspose.Cells for Java

### Maven
在 `pom.xml` 檔案中加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
在 `build.gradle` 檔案中加入此行：

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### 取得授權
Aspose 提供免費試用、臨時授權與正式商業授權。你可以先從 [免費試用](https://releases.aspose.com/cells/java/) 開始，或在 [臨時授權頁面](https://purchase.aspose.com/temporary-license/) 取得臨時授權。

## 使用 Aspose.Cells Java 變更 Excel 日期系統

以下為實際 **變更 Excel 日期系統** 的逐步說明。每一步都包含簡短說明與完整程式碼。

### 步驟 1：初始化並載入活頁簿
首先，建立指向既有 Excel 檔案的 `Workbook` 例項。

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### 步驟 2：啟用 1904 日期系統
使用活頁簿設定切換日期系統。

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**小技巧：** 若日後需要回復，可呼叫 `setDate1904(false)`。

### 步驟 3：儲存已修改的活頁簿
最後，將變更寫入新檔案（或覆寫原檔）。

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

> **注意：** 上述程式碼使用的類別名稱 `tWorkbook` 為原始範例中的拼寫。請確保此名稱符合你的專案命名慣例，或視需要改為 `Workbook`。

## 以程式方式設定 Excel 日期（次要關鍵字）
若在變更系統後需調整個別儲存格的值，可使用 `Cells.get(i, j).putValue(Date)`，日期會依目前啟用的日期系統解讀。

## 將 Excel 1904 系統轉回 1900（次要關鍵字）
只要呼叫：

```java
workbook.getSettings().setDate1904(false);
```

然後再次儲存活頁簿即可。

## 實務應用
1. **資料封存** – 在遷移舊版 Mac 試算表時保留舊有時間戳記。  
2. **跨平台報表** – 產生的報表可在 Windows 與 macOS 上開啟，且不會出現日期錯位。  
3. **財務模型** – 與仍使用 1904 系統的舊版財務模型保持日期計算一致。

## 效能考量
- 在單一工作階段內限制活頁簿操作，以降低記憶體使用量。  
- 對於極大型檔案，可調整 Java 的垃圾回收設定。

## 常見問題

**Q: 1900 與 1904 日期系統有何差異？**  
A: 1900 系統從 1900 年 1 月 1 日開始計算，1904 系統則從 1904 年 1 月 1 日開始，兩者相差 1462 天。

**Q: 可以變更目前正由 Excel 開啟的活頁簿的日期系統嗎？**  
A: 可以，但必須先在 Excel 中關閉該檔案，否則儲存會失敗。

**Q: 使用 `setDate1904` 需要授權嗎？**  
A: 試用版亦可使用此方法，但正式授權可移除評估限制。

**Q: 能否只為單一工作表變更日期系統？**  
A: 無法，日期系統是活頁簿層級的設定，會套用至所有工作表。

**Q: 如何驗證日期系統已變更？**  
A: 開啟已儲存的檔案，前往 **檔案 → 選項 → 進階**，確認勾選 **「使用 1904 日期系統」** 方塊。

## 結論
現在你已掌握如何使用 Aspose.Cells for Java **將 Excel 日期系統變更為 1904**、設定 Excel 日期格式，以及在需要時將系統轉回。將這些程式碼片段整合到資料處理流程中，即可確保跨平台的日期相容性。

---

**最後更新：** 2026-02-22  
**測試環境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose  

**資源**
- **文件說明：** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **下載：** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **購買授權：** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **免費試用：** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **臨時授權：** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **支援論壇：** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}