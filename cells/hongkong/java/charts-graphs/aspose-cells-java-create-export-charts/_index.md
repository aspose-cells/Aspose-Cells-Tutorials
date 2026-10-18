---
date: '2026-04-05'
description: 學習如何使用 Aspose.Cells 在 Java 中建立圖表，將 Excel 圖表轉換為圖像，並高效匯出圖表。
keywords:
- how to create chart
- excel chart to image
- convert excel chart
- aspose cells chart
- how to export chart
- create chart java
title: 使用 Aspose.Cells 在 Java 中建立圖表並匯出為圖像 – 完整指南
url: /zh-hant/java/charts-graphs/aspose-cells-java-create-export-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 使用 Aspose.Cells 建立圖表並匯出為影像 – 完整指南

## 介紹

如果您正在尋找一種可靠的方式 **how to create chart** 直接從 Java 程式碼建立圖表物件，Aspose.Cells for Java 讓這個過程變得簡單。在本教學中，您將學習如何建立金字塔圖表、設定高解析度影像輸出，最後將圖表匯出為 PNG 影像。完成後，您也會了解如何 **convert excel chart** 為影像檔，以及為何此方法非常適合自動化報告。

**您將學習**
- 設定 Aspose.Cells for Java
- 使用 Java 在 Excel 活頁簿中建立金字塔圖表
- 設定影像輸出選項以獲得高品質渲染
- 將圖表匯出為影像，用於儀表板、電子郵件或 PDF

現在讓我們逐步檢視先決條件，並準備好您的開發環境。

## 快速解答
- **需要的函式庫是什麼？** Aspose.Cells for Java (v25.3+)
- **示範的圖表類型是？** 金字塔圖表（您可以切換為其他類型）
- **如何匯出圖表？** 使用 `Chart.toImage()` 搭配 `ImageOrPrintOptions`
- **可以匯出為其他格式嗎？** 可以 – 支援 PNG、JPEG、BMP、GIF 與 TIFF
- **需要授權嗎？** 免費試用授權可用於評估；商業授權則需於正式環境使用

## Aspose.Cells 如何「建立圖表」？

Aspose.Cells 提供功能豐富的 API，讓開發人員能以程式方式產生 Excel 工作表、加入圖表，並將其渲染為影像——完全不需安裝 Microsoft Office。這使其非常適合伺服器端報告、資料分析儀表板以及自動化文件產生。

## 為何使用 Aspose.Cells 轉換 Excel 圖表為影像？

- **無需 Office 相依性：** 可在任何支援 Java 的平台上執行。
- **高保真渲染：** 支援抗鋸齒與 DPI 設定，產生清晰影像。
- **廣泛格式支援：** 可匯出為 PNG、JPEG、SVG、PDF 等多種格式。
- **效能導向：** 能有效處理大型活頁簿，且可結合多執行緒使用。

## 前置條件

- **必要函式庫：** Aspose.Cells for Java 版本 25.3 或以上。
- **開發環境 (IDE)：** IntelliJ IDEA、Eclipse，或任何相容 Java 的 IDE。
- **JDK：** Java 8 或更新版本。
- **基礎知識：** 熟悉 Java、Maven/Gradle 以及 Excel 檔案概念。

## 設定 Aspose.Cells for Java

### Maven
Add the following dependency to your `pom.xml` file:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Include this line in your `build.gradle` file:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

**授權取得：** Aspose.Cells 提供免費試用授權，您可從他們的[購買頁面](https://purchase.aspose.com/buy)取得。將臨時授權套用於開發期間，即可解鎖完整功能。

### 基本初始化

首先，建立一個 `Workbook` 實例。此物件將保存您的資料與圖表：
```java
import com.aspose.cells.Workbook;

public class AsposeCellsInit {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        // Your chart creation code will go here.
    }
}
```

## 如何在 Java 使用 Aspose.Cells 建立圖表

### 在 Excel 中建立金字塔圖表

#### 步驟 1：初始化 Workbook 與 Worksheet
首先，設定活頁簿並取得預設工作表的參考。
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorksheetCollection;

String dataDir = "YOUR_DATA_DIRECTORY"; // Update with your directory path

Workbook workbook = new Workbook();
WorksheetCollection worksheets = workbook.getWorksheets();
```

#### 步驟 2：加入金字塔圖表
使用 `ChartCollection` 插入金字塔圖表。此範例說明 **aspose cells chart** 的建立流程。
```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;

Worksheet sheet = worksheets.get(0);
ChartCollection charts = sheet.getCharts();
int chartIndex = charts.add(ChartType.PYRAMID, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);
```

## 設定影像輸出選項（如何匯出圖表）

### 步驟 1：設定解析度與抗鋸齒
微調渲染設定，以獲得清晰的 **excel chart to image** 轉換效果。
```java
import com.aspose.cells.ImageOrPrintOptions;
import java.awt.RenderingHints;

ImageOrPrintOptions options = new ImageOrPrintOptions();
options.setVerticalResolution(300);
options.setHorizontalResolution(300);
options.setRenderingHint(RenderingHints.KEY_ANTIALIASING, RenderingHints.VALUE_ANTIALIAS_ON);
options.setRenderingHint(RenderingHints.KEY_TEXT_ANTIALIASING, RenderingHints.VALUE_TEXT_ANTIALIAS_ON);
```

## 匯出圖表為影像（轉換 Excel 圖表）

### 步驟 1：將圖表儲存為影像
最後，使用先前設定的選項將圖表寫入 PNG 檔案。
```java
chart.toImage(dataDir + "chart.png", options);
```

**故障排除提示**
- 確認 `dataDir` 指向可寫入的資料夾。
- 確保您的 Aspose.Cells 版本為 25.3 或更新；較舊版本可能不支援此處使用的 `toImage` 重載。

## 實務應用

以下是 **how to export chart** 功能常見的應用情境：

1. **商業報告：** 自動產生每月銷售儀表板。
2. **教育工具：** 為學生製作視覺化績效報告。
3. **醫療分析：** 為簡報渲染患者統計資料，無需手動操作 Excel。

這些使用案例說明了開發人員為何選擇 Aspose.Cells 進行伺服器端圖表產生與影像匯出。

## 效能考量

在擴充規模時：

- 釋放未使用的 `Workbook` 物件以節省記憶體。
- 對大量資料使用串流 API。
- 在同時產生多份報告時，平行化圖表建立程序。

遵循上述建議，可確保您的 Java 服務在高負載下仍保持回應性。

## 結論

您現在已具備使用 Aspose.Cells for Java 建立 **how to create chart** 物件、客製化渲染以及 **export chart** 影像的堅實基礎。可嘗試其他 `ChartType` 值、套用樣式，或將 PNG 輸出整合至 PDF、網頁或電子郵件附件中。

**下一步**
- 透過替換 `ChartType.PYRAMID` 嘗試折線圖、長條圖或圓餅圖。
- 探索 `Chart` 類別以自訂標題、圖例與座標軸。
- 加入社群以獲得更深入的見解。

可考慮造訪 [Aspose 論壇](https://forum.aspose.com/c/cells/9) 取得更多技巧與實務範例。

## 常見問題

**Q: 如何加入不同的圖表類型？**  
A: 使用 `ChartType` 列舉中的其他值，例如 `ChartType.BAR` 或 `ChartType.PIE`。

**Q: 能否從現有的 Excel 檔案產生圖表？**  
A: 可以。使用 `new Workbook("existing.xlsx")` 載入活頁簿，然後加入或修改圖表。

**Q: 使用 **excel chart to image** 時常見的陷阱是什麼？**  
A: 檔案路徑不正確、寫入權限不足，或使用低於 25.3 版的 Aspose.Cells。

**Q: 如何有效處理非常大的活頁簿？**  
A: 利用 Aspose.Cells 的串流 API，並及時釋放物件以降低記憶體使用。

**Q: 能否自訂圖表標題或圖例？**  
A: 當然可以。`Chart` 類別提供 `setTitle()`、`setLegend()`、`setSeries()` 等方法，以進行完整客製化。

**最後更新：** 2026-04-05  
**測試環境：** Aspose.Cells for Java 25.3  
**作者：** Aspose  

**資源**
- [Documentation](https://reference.aspose.com/cells/java/)
- [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)
- [Purchase a License](https://purchase.aspose.com/buy)
- [Free Trial Download](https://releases.aspose.com/cells/java/)
- [Obtain a Temporary License](https://purchase.aspose.com/temporary-license/)
- [Support Forum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}