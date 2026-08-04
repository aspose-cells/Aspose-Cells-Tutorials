---
date: '2026-02-16'
description: 學習如何使用 Aspose.Cells for Java 建立可點擊圖片的 Excel，為圖片添加超連結以製作互動式試算表。
keywords:
- image hyperlinks in Excel
- Aspose.Cells for Java
- interactive Excel spreadsheets
title: 使用 Aspose.Cells for Java 建立可點擊圖片的 Excel
url: /zh-hant/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells for Java 建立可點擊圖像 Excel

## 簡介

如果您想要建立可點擊圖像 Excel 工作簿，讓使用者只需點擊一次即可跳轉至網站、文件或其他資源，您來對地方了。在本教學中，我們將說明 Aspose.Cells for Java 如何讓您新增超連結圖像物件、設定螢幕提示，並讓您的試算表既美觀又具功能性。

### 您將學會
- 在 Java 中初始化 Aspose.Cells 工作簿。  
- 插入圖像並將其轉換為可點擊的超連結。  
- 關鍵方法，如 `addHyperlink`、`setPlacement` 和 `setScreenTip`。  
- 效能與授權的最佳實踐。

## 快速答覆
- **需要的函式庫是什麼？** Aspose.Cells for Java。  
- **我可以使用 .xlsx 檔案嗎？** 可以 — API 同時支援 .xls 與 .xlsx。  
- **我需要授權嗎？** 試用版可用於評估；正式環境需購買永久授權。  
- **需要多少行程式碼？** 大約 20 行即可新增可點擊圖像。  
- **它是執行緒安全的嗎？** Workbook 物件非執行緒安全；每個執行緒請建立獨立實例。  
- **我可以在 Excel 中加入螢幕提示嗎？** 可以 — 使用 `Hyperlink.setScreenTip()` 來顯示提示文字。

## 如何使用 Aspose.Cells for Java 建立可點擊圖像 Excel

### 先決條件
在開始之前，請確保您已具備：

- **Aspose.Cells for Java**（v25.3 或更新版本）。  
- **JDK 8+** 已安裝。  
- 一個 IDE（IntelliJ IDEA、Eclipse 或 NetBeans）以及 Maven 或 Gradle 來管理相依性。  

### 必要函式庫
將 Aspose.Cells 加入您的專案：

**Maven**  
```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 授權取得
Aspose.Cells 為商業授權，但您可以先使用免費試用或申請臨時授權：

- 免費試用：從 [Aspose Downloads](https://releases.aspose.com/cells/java/) 下載。  
- 臨時授權：可於 [Temporary License page](https://purchase.aspose.com/temporary-license/) 申請。  
- 購買：長期使用請前往 [Aspose Purchase](https://purchase.aspose.com/buy)。

### 基本初始化
建立工作簿並取得第一個工作表：

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

// Initialize workbook
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## 逐步實作

### 步驟 1：準備工作簿
我們先建立一個新的工作簿，並選取第一個工作表。

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### 步驟 2：插入標籤並調整儲存格大小
加入說明文字標籤，並調整儲存格大小以容納圖片。

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```

### 步驟 3：加入圖片
載入圖片檔案並將其放置於工作表上。

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```
*提示*：將 `"path/to/aspose-logo.jpg"` 替換為實際的圖片檔案路徑。

### 步驟 4：設定位置並加入超連結
將圖片設定為自由浮動，並為其附加超連結。

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```

### 步驟 5：設定螢幕提示並儲存工作簿
設定有用的提示文字，並將工作簿寫入磁碟。

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```

## 為什麼要在 Excel 圖片上加入超連結？

將可點擊的圖片嵌入 Excel，可將品牌元素、圖示或圖表轉換為直接的導向點。這可減少使用者在行銷儀表板、技術手冊與教學工作表中前往相關內容所需的點擊次數，提升使用體驗。

## 如何在 Excel 中加入螢幕提示

`setScreenTip` 方法可讓您定義使用者將游標停留在圖片上時顯示的提示文字。這非常適合提供上下文說明，例如「檢視產品詳細資訊」或「開啟教學影片」。

## 故障排除技巧
- **圖片路徑錯誤** — 請再次確認檔案位置，並確保應用程式具備讀取權限。  
- **授權未套用** — 若試用版過期，超連結可能失效；請使用 `License.setLicense` 套用有效授權。  
- **超連結無法點擊** — 請確認圖片的 `PlacementType` 已設定為 `FREE_FLOATING`。

## 實務應用
在許多情境中嵌入可點擊的圖片都很有用：

1. **行銷報告** — 將品牌標誌連結至產品頁面。  
2. **技術文件** — 附加可開啟詳細圖紙的圖示。  
3. **教學工作表** — 將圖示轉為補充影片的快捷方式。  
4. **專案儀表板** — 讓狀態圖示開啟相關任務追蹤器。

## 效能考量
- 保持圖片檔案大小適中；過大的圖片會增加工作簿的記憶體使用量。  
- 在迴圈處理大量檔案時，釋放未使用的物件（`workbook.dispose()`）。  
- 升級至最新的 Aspose.Cells 版本，以獲得效能提升與錯誤修正。

## 結論
現在您已了解如何使用 Aspose.Cells for Java 在 Excel 圖片上 **加入超連結**，從而建立更豐富、更具互動性的 **可點擊圖像 Excel** 工作簿。可自行嘗試不同的 URL、螢幕提示與圖片位置，以符合您的報表需求。接下來，您可以探索為圖形加入超連結，或在多個工作表中自動批次插入圖片。

## 常見問題

**Q:** Aspose.Cells for Java 支援的最大圖片尺寸為何？  
**A:** 沒有嚴格限制，但過大的圖片會影響效能並增加檔案大小。

**Q:** 我可以在 .xlsx 檔案中使用此功能嗎？  
**A:** 可以，API 同時支援 `.xls` 與 `.xlsx` 格式。

**Q:** 在加入超連結時應如何處理例外情況？  
**A:** 將程式碼包在 try‑catch 區塊中，並記錄 `Exception` 詳細資訊，以診斷路徑或授權問題。

**Q:** 加入超連結後，是否可以從圖片移除？  
**A:** 可以 — 取得 `Picture` 物件後呼叫 `pic.getHyperlink().remove()`，或從集合中刪除該圖片。

**Q:** 為何我的超連結可能無法正常運作？  
**A:** 常見原因包括 URL 字串不正確、缺少 `http://`/`https://` 前綴，或未授權的試用版會停用某些功能。

## 其他資源
- **文件**： [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **下載**： [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **購買與試用**：前往 [Aspose Purchase](https://purchase.aspose.com/buy) 或 [Temporary License Page](https://purchase.aspose.com/temporary-license/) 了解授權方案。  
- **支援論壇**：如需協助，請參閱 [Aspose Support Forum](https://forum.aspose.com/c/cells/9)。

---

**最後更新**： 2026-02-16  
**測試環境**： Aspose.Cells for Java 25.3  
**作者**： Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}