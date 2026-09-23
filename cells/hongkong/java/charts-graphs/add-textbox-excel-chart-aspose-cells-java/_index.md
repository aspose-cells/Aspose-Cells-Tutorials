---
date: '2026-04-05'
description: 學習如何使用 Aspose.Cells for Java 為 Excel 圖表新增文字方塊，涵蓋載入活頁簿與儲存 Excel 檔案的 Java
  程式。
keywords:
- how to add textbox
- save excel file java
- excel chart textbox
- load excel workbook java
- Aspose.Cells Java
title: 如何使用 Aspose.Cells Java 為 Excel 圖表新增文字方塊
url: /zh-hant/java/charts-graphs/add-textbox-excel-chart-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Excel 圖表中使用 Aspose.Cells Java 添加 TextBox

## 介紹

在資料視覺化的世界中航行可能充滿挑戰，尤其是當您需要直接在 Excel 工作表的圖表上加入自訂文字註解或標籤時。本教學將指引您使用 Aspose.Cells for Java——一個功能強大的函式庫，簡化此類工作，讓您無縫地在 Excel 圖表中整合 TextBox。

**您將學會：**
- 使用 Aspose.Cells for Java 載入與操作 Excel 檔案。
- 存取與修改 Excel 活頁簿中的圖表物件。
- 在圖表上新增與自訂 TextBox 控制項。
- 將變更儲存回 Excel 檔案。

### 快速回答
- **載入工作簿的主要類別是什麼？** `Workbook` 來自 `com.aspose.cells`。
- **哪個方法可在圖表中加入 TextBox？** 圖表的 shape 集合中的 `addTextBoxInChart`。
- **我可以變更 TextBox 的填色嗎？** 可以，透過 `FillFormat` 與 `SolidFill`。
- **如何儲存已修改的檔案？** 使用 `workbook.save` 並指定 `SaveFormat`。
- **生產環境需要授權嗎？** 需要，商業授權會移除評估限制。

## 如何在 Excel 圖表中添加 TextBox

既然您已了解整體工作流程，接下來讓我們深入逐步實作。每一步都會包含一段保持不變的程式碼片段，以及對其功能的清晰說明。

## 前置條件

- **必要函式庫：** Aspose.Cells for Java 版本 25.3 或更新。本教學使用 Maven 與 Gradle 設定。
- **環境設定：** 您的機器上已安裝相容的 Java Development Kit (JDK)。
- **知識前提：** 具備 Java 程式設計的基本概念，並熟悉 Excel 檔案結構。

## 設定 Aspose.Cells for Java

要在專案中使用 Aspose.Cells，您需要將其加入為相依性。以下示範如何使用 Maven 或 Gradle 完成設定：

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### 授權取得

Aspose.Cells 提供免費試用、暫時授權（供延長測試使用）以及商業購買選項：

- **免費試用：** 下載函式庫以開始體驗其功能。
- **暫時授權：** 從 [此處](https://purchase.aspose.com/temporary-license/) 取得，以在無限制的情況下評估完整功能。
- **購買：** 若在生產環境持續使用，請於 [Aspose 購買](https://purchase.aspose.com/buy) 取得授權。

### 基本初始化與設定

加入函式庫後，若有授權檔案，請先進行初始化：

```java
License license = new License();
license.setLicense("path/to/your/license/file.lic");
```

## 實作指南

接下來我們將示範如何使用 Aspose.Cells for Java 為 Excel 圖表加入 TextBox。此指南將逐一說明每個功能。

### 載入 Excel 檔案

**概觀：** 我們先將既有的 Excel 檔案載入應用程式，以便程式化操作其內容。

#### 步驟 1：匯入必要類別
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

#### 步驟 2：載入工作簿
```java
String dataDir = "YOUR_DATA_DIRECTORY";
String filePath = dataDir + "/chart.xls";
Workbook workbook = new Workbook(filePath);
Worksheet worksheet = workbook.getWorksheets().get(0);
```
**說明：** `Workbook` 類別代表一個 Excel 檔案。載入後即可存取其所有工作表與內容。

### 存取圖表物件

**概觀：** 檔案載入後，我們需要從指定的工作表中取得圖表物件。

#### 步驟 3：匯入圖表類別
```java
import com.aspose.cells.Chart;
```

#### 步驟 4：存取第一個圖表
```java
Chart chart = worksheet.getCharts().get(0);
```
**說明：** 這段程式碼取得目前工作表中的第一個圖表，以便後續操作。

### 為圖表新增 TextBox 控制項

**概觀：** 現在，我們在圖表中加入自訂的 TextBox，以顯示任意文字註解。

#### 步驟 5：匯入必要類別
```java
import com.aspose.cells.TextBox;
import com.aspose.cells.FillFormat;
import com.aspose.cells.LineFormat;
import java.awt.Color;
import com.aspose.cells.MsoLineDashStyle;
```

#### 步驟 6：新增並自訂 TextBox
```java
TextBox txt = chart.getShapes().addTextBoxInChart(100, 100, 850, 2500);
txt.setText("Aspose");
txt.getFont().setItalic(true);
txt.getFont().setSize(20);
txt.getFont().setBold(true);

// Set Fill Format
FillFormat fillformat = txt.getFill();
fillformat.setFillType(FillFormat.FillType.SOLID);
fillformat.getSolidFill().setColor(Color.getSilver());

// Configure Line Format
LineFormat lineformat = txt.getLine();
lineformat.setWeight(2);
lineformat.setDashStyle(MsoLineDashStyle.SOLID);
```
**說明：** 這段程式碼在指定座標新增 TextBox，設定文字外觀，並套用填色與線條樣式。

### 儲存 Excel 檔案

**概觀：** 最後，將修改過的工作簿儲存回 Excel 檔案格式。

#### 步驟 7：匯入 SaveFormat 類別
```java
import com.aspose.cells.SaveFormat;
```

#### 步驟 8：儲存工作簿
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "/ATBoxControl_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
**說明：** 工作簿會依指定目錄儲存，保留執行期間所做的變更。

## 實務應用

以下是一些在實際情境中加入 TextBox 至 Excel 圖表的應用範例：

1. **報告註解：** 使用文字方塊直接在圖表上提供背景說明或突顯關鍵發現。
2. **自訂圖例與標籤：** 以額外資訊或說明補足標準圖例的不足，提升可讀性。
3. **品牌化：** 在圖表內加入公司標誌或品牌宣言，以便於簡報使用。

## 效能考量

處理大型 Excel 檔案時，請留意以下建議：

- **最佳化資源使用：** 減少圖表操作與物件建立的次數，以降低記憶體佔用。
- **Java 記憶體管理：** 使用完 `Workbook` 後務必關閉，以即時釋放資源。
- **有效的資料處理：** 只載入工作簿中必要的部分，避免一次性讀取龐大資料集。

## 如何在 Java 中儲存 Excel 檔案

最後一步——儲存工作簿——示範了 **save excel file java** 的工作流程。透過指定 `SaveFormat`，您可以輸出為傳統的 `.xls`、現代的 `.xlsx`，甚至是 CSV 格式，完整掌控下游流程所需的檔案類型。

## 如何在 Java 中載入 Excel 工作簿

前面的 `Workbook` 初始化說明了 **load excel workbook java** 的模式。Aspose.Cells 抽象化了二進位 Excel 結構的解析，讓您專注於業務邏輯，而非檔案 I/O 的細節。

## 結論

我們已完整示範如何使用 Aspose.Cells for Java 為 Excel 圖表加入 TextBox。此指南涵蓋了環境設定、檔案載入、圖表存取、文字方塊自訂與最終儲存的全流程。

**後續步驟：** 嘗試套用不同樣式或探索 Aspose.Cells 提供的其他圖表類型。更多進階功能請參考其文件於 [Aspose Reference](https://reference.aspose.com/cells/java/)。

## 常見問答

1. **我可以在同一圖表中加入多個 TextBox 嗎？**  
   - 可以，您只需依需求多次呼叫 `addTextBoxInChart`，並提供不同座標。

2. **如果我的 Excel 檔案沒有圖表會發生什麼？**  
   - 嘗試存取不存在的圖表會拋出例外。請先確保工作簿至少包含一個圖表。

3. **是否能將檔案儲存為 .xls 以外的格式？**  
   - 可以，您可使用 `SaveFormat` 的其他選項（如 `XLSX`）依需求儲存。

4. **如何在檔案操作期間處理例外？**  
   - 在載入與儲存程式碼周圍加入 try‑catch 區塊，以優雅地管理錯誤。

5. **Aspose.Cells for Java 能否與其他程式語言一起使用？**  
   - 雖然本指南聚焦於 Java，Aspose.Cells 亦提供 .NET、C++ 等版本。請參閱其 [文件](https://reference.aspose.com/cells/java/) 取得語言專屬指南。

## 常見問題

**Q: 加入 TextBox 會影響圖表效能嗎？**  
A: 影響極小；但若工作簿非常龐大，建議限制形狀物件的數量，以降低記憶體使用。

**Q: 可以使用儲存格參考而非像素座標來定位 TextBox 嗎？**  
A: 可以，您可以根據儲存格索引計算像素座標，或使用工作表的 `addTextBox` 方法以儲存格為基礎定位。

**Q: 有辦法將 TextBox 文字綁定至儲存格值嗎？**  
A: Aspose.Cells 未提供形狀的直接資料繫結，但您可在程式中讀取儲存格值後手動更新 TextBox 文字。

**Q: 商業部署需要什麼授權？**  
A: 購買的 Aspose.Cells 授權會移除所有評估限制，且是生產環境的必要條件。

**Q: 哪裡可以找到更多圖表操作的範例？**  
A: 官方的 Aspose.Cells 文件與範例倉庫提供大量情境，包括動態序列、圖表類型與樣式設定等。

## 資源

- **文件：** 前往 [Aspose Reference](https://reference.aspose.com/cells/java/) 探索完整指南。
- **下載：** 從 [Releases](https://releases.aspose.com/cells/java/) 取得最新函式庫版本。
- **購買與試用：** 透過 [Purchase Aspose](https://purchase.aspose.com/buy) 或 [Free Trial](https://releases.aspose.com/cells/java/) 取得授權或免費試用。
- **支援：** 加入 [Aspose Forum](https://forum.aspose.com/c/cells/9) 社群取得協助。

遵循本指南，您即可在 Java 專案中高效整合 Aspose.Cells，為 Excel 圖表增添自訂文字註解。祝開發順利！

---

**最後更新：** 2026-04-05  
**測試環境：** Aspose.Cells Java 25.3  
**作者：** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}