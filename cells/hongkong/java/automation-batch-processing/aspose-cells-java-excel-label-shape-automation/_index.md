---
date: '2025-12-29'
description: 學習如何使用 Aspose.Cells for Java 建立 Excel 工作簿、設定 Aspose Cells 授權，並以標籤形狀儲存
  Excel 工作簿。非常適合 Java 產生 Excel 的任務。
keywords:
- Excel automation with Java
- Aspose.Cells label shape
- Aspose.Cells workbook creation
title: 如何使用 Aspose.Cells for Java 建立 Excel 活頁簿 - 加入標籤形狀
url: /zh-hant/java/automation-batch-processing/aspose-cells-java-excel-label-shape-automation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells for Java 自動化建立 Excel 工作簿：新增標籤形狀

## 簡介

如果您需要在 Java 中以程式方式 **create excel workbook**，Aspose.Cells for Java 可讓此過程快速且可靠。在本教學中，您將了解如何設定函式庫、套用 **aspose cells license**、新增標籤形狀，最後 **save excel workbook** 到磁碟。完成後，您將熟悉 **java generate excel** 的核心步驟，並知道在一般專案中 **how to use aspose** 的方式。

**您將學會**
- 如何使用 Aspose.Cells for Java **create excel workbook**  
- 存取工作簿中的工作表  
- 在工作表中新增與自訂標籤形狀  
- 設定標籤屬性，如文字、放置類型與填色  
- 使用 **aspose cells maven** 或 Gradle 來引用函式庫  

準備好開始了嗎？讓我們一步一步走過整個流程！

## 快速解答
- **需要的函式庫是什麼？** Aspose.Cells for Java (available via Maven or Gradle).  
- **我可以使用免費試用嗎？** Yes – download from Aspose’s website and apply a temporary license.  
- **如何新增標籤形狀？** Use `sheet.getShapes().addShape(MsoDrawingType.LABEL, …)`.  
- **哪個版本支援標籤形狀？** Version 25.3 or later.  
- **如何儲存工作簿？** Call `workbook.save("path/filename.xls")`.

## 什麼是使用 Aspose.Cells 建立 Excel 工作簿？

建立 Excel 工作簿指的是以程式方式從 Java 程式碼產生 `.xls` 或 `.xlsx` 檔案。Aspose.Cells 抽象化了低層的檔案格式細節，讓您能專注於業務邏輯，而非檔案處理。

## 為什麼選擇 Aspose.Cells for Java？
- **Full‑featured API** – 支援圖表、形狀、公式等多種功能。  
- **No Microsoft Office required** – 可在任何伺服器或雲端環境執行。  
- **High performance** – 為大型資料集與多執行緒進行最佳化。  
- **Robust licensing** – 提供彈性的 **aspose cells license** 選項，適用於試用、臨時或企業版。

## 前提條件
- **Java Development Kit (JDK)：** 8 版或以上。  
- **IDE：** IntelliJ IDEA、Eclipse 或 NetBeans。  
- **Aspose.Cells for Java Library：** 25.3 版或更新。  
- 基本的 Java 程式設計知識。

## 設定 Aspose.Cells for Java

### 使用 Maven（**aspose cells maven**）

在您的 `pom.xml` 中加入以下相依性：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### 使用 Gradle

在您的 `build.gradle` 檔案中加入此行：

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### 取得許可證步驟

1. **Free Trial：** 從 [Aspose's website](https://releases.aspose.com/cells/java/) 下載免費評估版。  
2. **Temporary License：** 前往 [Aspose's Temporary License page](https://purchase.aspose.com/temporary-license/) 申請測試用的臨時授權（無限制）。  
3. **Purchase：** 前往 [Aspose's Purchase Page](https://purchase.aspose.com/buy) 購買授權，以取得完整功能與企業版支援。

**基本初始化：**

```java
import com.aspose.cells.License;
// Initialize Aspose.Cells License
License license = new License();
license.setLicense("path/to/your/license/file");
```

## 實作指南

### 建立新工作簿

要開始，我們建立一個新的 Excel 工作簿實例。這是任何 **java generate excel** 工作流程的起點。

```java
import com.aspose.cells.Workbook;
// Create an empty workbook
Workbook workbook = new Workbook();
```

### 存取第一個工作表

接著，存取此新建立工作簿的第一個工作表，以執行新增形狀或資料輸入等操作。

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.Worksheets;
// Get the first worksheet from the workbook
Worksheet sheet = workbook.getWorksheets().get(0);
```

### 新增標籤形狀

加入視覺元素（如標籤）可提升 Excel 報表的可讀性。此處，我們使用 `MsoDrawingType` 新增標籤形狀。

```java
import com.aspose.cells.Label;
import com.aspose.cells.MsoDrawingType;
// Add a label shape to the worksheet
Label label = (Label) sheet.getShapes().addShape(MsoDrawingType.LABEL, 2, 2, 2, 0, 60, 120);
```

### 設定標籤文字

透過設定文字自訂您的標籤。此步驟允許您指定標籤要顯示的內容。

```java
// Set text for the label
label.setText("This is a Label");
```

### 配置標籤放置類型

為確保位置的彈性，請在工作表中設定標籤的放置類型。

```java
import com.aspose.cells.PlacementType;
// Configure label placement
label.setPlacement(PlacementType.FREE_FLOATING);
```

### 設定漸層填滿顏色

透過設定漸層填色來提升視覺效果，這有助於區分區段或突顯資訊。

```java
import com.aspose.cells.Color;
import com.aspose.cells.GradientStyleType;
// Set one-color gradient as fill for the label
label.getFill().setOneColorGradient(Color.getYellow(), 1, GradientStyleType.HORIZONTAL, 1);
```

### 儲存工作簿

最後，將 **save excel workbook** 至輸出目錄。此步驟完成文件，讓其可供分發或進一步處理。

```java
// Define output directory and save the workbook
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "/AddingLabelControl_out.xls");
```

## 實際應用

Aspose.Cells 可應用於各種實務情境，例如：

1. **自動化報表產生：** 自動建立每月的財務或銷售報表。  
2. **資料輸入與處理：** 從資料庫或 API 填充 Excel 工作簿。  
3. **發票產生：** 產生具備自訂品牌與計算的發票。  
4. **儀表板開發：** 建立即時資料視覺化的動態儀表板。  

將其與 CRM、ERP 或自訂 Java 應用程式整合，可大幅簡化業務流程。

## 效能注意事項

在大規模 **create excel workbook** 時，為取得最佳效能：

- 釋放不再需要的物件以節省記憶體。  
- 利用 Aspose.Cells 的多執行緒功能處理大型資料集。  
- 保持函式庫為最新版本，以獲得效能提升。  
- 優雅地處理例外並監控記憶體使用情況。

## 常見問題及解決方案

| 問題 | 解決方案 |
|-------|----------|
| **OutOfMemoryError** 在處理大型檔案時發生 | 使用 `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`，並分批處理資料。 |
| **License not applied** | 確認授權檔案路徑，且在任何工作簿操作前呼叫 `license.setLicense()`。 |
| **Shape not appearing** | 確認形狀的座標與尺寸位於工作表可見範圍內。 |

## 常見問題解答

**Q: 如何在工作表中新增多個形狀？**  
A: 反覆呼叫 `addShape` 方法，並為每個形狀調整參數。

**Q: Aspose.Cells 能有效處理大型 Excel 檔案嗎？**  
A: 可以，但需監控記憶體使用，對於極大資料集建議使用串流 API。

**Q: Aspose.Cells 提供哪些授權選項？**  
A: 您可以先使用免費試用版，取得測試用的臨時授權，或購買完整的 **aspose cells license** 以供正式上線。

**Q: 除了標籤外，是否能自訂其他形狀？**  
A: 當然可以。您可以使用不同的 `MsoDrawingType` 值加入圖表、圖片及其他繪圖類型。

**Q: 若遇到問題，該向何處尋求協助？**  
A: 前往社群論壇 [Aspose's Support Forum](https://forum.aspose.com/c/cells/9) 或參考官方文件 [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)。  

## 資源

- **文件說明：** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **下載：** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)  
- **購買：** [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **免費試用：** [Aspose Cells Free Trial Download](https://releases.aspose.com/cells/java/)  
- **臨時授權：** [Request Temporary License](https://purchase.aspose.com/temporary-license/)

遵循本指南，您現在已具備建立 **create excel workbook** 檔案、加入豐富標籤形狀，並將 Aspose.Cells 整合至 Java 專案的堅實基礎。

---

**最後更新：** 2025-12-29  
**測試環境：** Aspose.Cells for Java 25.3  
**作者：** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
