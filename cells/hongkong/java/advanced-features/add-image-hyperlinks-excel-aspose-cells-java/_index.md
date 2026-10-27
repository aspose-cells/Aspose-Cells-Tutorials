---
date: '2026-09-02'
description: 了解如何使用 Aspose.Cells for Java 建立可點擊圖像的 Excel 活頁簿，為圖片添加 hyperlinks，以實現互動式試算表。
keywords:
- create clickable image
- add image hyperlink
- add hyperlink to picture
- interactive excel spreadsheet
- how to add hyperlink
lastmod: '2026-09-02'
og_description: 了解如何使用 Aspose.Cells for Java 建立可點擊圖像的 Excel 活頁簿，添加 hyperlinks、screen
  tips，並在僅幾行 code 中 optimizing performance。
og_image_alt: 'Developer guide: create clickable image Excel using Aspose.Cells for
  Java'
og_title: 使用 Aspose.Cells for Java 建立可點擊圖像的 Excel
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  headline: Create clickable image Excel using Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create clickable image Excel workbooks with Aspose.Cells
    for Java, adding hyperlinks to pictures for interactive spreadsheets.
  name: Create clickable image Excel using Aspose.Cells for Java
  steps:
  - name: prepare your workbook
    text: We start by creating a new workbook and selecting the first sheet.
  - name: insert a label and adjust cell size
    text: Add a descriptive label and give the cell enough space for the picture.
  - name: add the image
    text: '`Picture` represents an image object placed on a worksheet. *Tip*: Replace
      `"path/to/aspose-logo.jpg"` with the actual path to your image file.'
  - name: configure placement and add the hyperlink
    text: '`Hyperlink` defines a link associated with a cell, shape, or picture, enabling
      navigation when clicked.'
  - name: set a screen tip and save the workbook
    text: Provide a helpful tooltip and write the workbook to disk.
  type: HowTo
- questions:
  - answer: Aspose.Cells for Java.
    question: What library is required?
  - answer: Yes – the API works with both .xls and .xlsx.
    question: Can I use .xlsx files?
  - answer: A trial works for evaluation; a permanent license is required for production.
    question: Do I need a license?
  - answer: About 20 lines to add a clickable image.
    question: How many lines of code?
  - answer: Workbook objects are not thread‑safe; create separate instances per thread.
    question: Is it thread‑safe?
  type: FAQPage
tags:
- create clickable image
- Aspose.Cells
- Java Excel automation
title: 使用 Aspose.Cells for Java 建立可點擊圖像的 Excel
url: /zh-hant/java/advanced-features/add-image-hyperlinks-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells for Java 建立可點擊圖像的 Excel

## 簡介

如果您想要 **建立可點擊圖像的 Excel** 工作簿，讓使用者只需點擊一次即可跳轉到網站、文件或其他資源，您來對地方了。在本教學中，我們將說明 Aspose.Cells for Java 如何讓您 **新增超連結 Excel 圖片** 物件、設定螢幕提示，並使您的試算表既美觀又實用。

### 您將學習
- 在 Java 中初始化 Aspose.Cells 工作簿。  
- 插入圖像並將其轉換為可點擊的超連結。  
- 重要方法如 `addHyperlink`、`setPlacement` 和 `setScreenTip`。  
- 性能與授權的最佳實踐。

## 快速答覆
- **需要的函式庫是什麼？** Aspose.Cells for Java。  
- **我可以使用 .xlsx 檔案嗎？** 可以 – API 同時支援 .xls 與 .xlsx。  
- **我需要授權嗎？** 試用版可用於評估；正式環境需使用永久授權。  
- **需要多少行程式碼？** 大約 20 行即可新增可點擊圖像。  
- **它是執行緒安全的嗎？** Workbook 物件不是執行緒安全的；請為每個執行緒建立獨立實例。  
- **我可以在 Excel 中加入螢幕提示嗎？** 可以 – 使用 `Hyperlink.setScreenTip()` 來顯示有用的懸停文字。

## 如何使用 Aspose.Cells for Java 建立可點擊圖像的 Excel

您可以透過載入或建立 `Workbook`、插入 `Picture` 物件、將 `Hyperlink` 附加到該圖片、（可選）設定螢幕提示，最後儲存檔案，來建立可點擊圖像的 Excel 工作簿。API 會處理所有低階的 Excel XML，因此您只需撰寫少量簡單的 Java 程式碼。

### 先決條件
在開始之前，請確保您已擁有：

- **Aspose.Cells for Java**（v25.3 或更新版本）。  
- 已安裝 **JDK 8+**。  
- 一個 IDE（IntelliJ IDEA、Eclipse 或 NetBeans）以及用於相依管理的 Maven 或 Gradle。

### 必要的函式庫
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

### 取得授權
Aspose.Cells 為商業軟體，但您可以先使用免費試用版或申請臨時授權：

- 免費試用：從 [Aspose Downloads](https://releases.aspose.com/cells/java/) 下載。  
- 臨時授權：透過 [Temporary License page](https://purchase.aspose.com/temporary-license/) 申請。  
- 購買：長期使用請前往 [Aspose Purchase](https://purchase.aspose.com/buy)。

### 基本初始化
`Workbook` 類別代表記憶體中的整個 Excel 檔案。您會實例化它，然後取得第一個工作表的參考。`Worksheet` 代表工作簿中的單一工作表。

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
新增描述性標籤，並為圖片留出足夠的儲存格空間。

```java
worksheet.getCells().get("C2").setValue("Image Hyperlink");
worksheet.getCells().setRowHeight(3, 100); // Set row height for C4
worksheet.getCells().setColumnWidth(2, 21); // Adjust column width for C column
```  

### 步驟 3：加入圖像
`Picture` 代表放置於工作表上的圖像物件。

```java
int index = worksheet.getPictures().add(3, 2, "path/to/aspose-logo.jpg");
```  
*提示*：將 `"path/to/aspose-logo.jpg"` 替換為實際的圖像檔案路徑。

### 步驟 4：設定放置位置並新增超連結
`Hyperlink` 定義與儲存格、圖形或圖片相關聯的連結，點擊時可進行導向。

```java
import com.aspose.cells.Picture;
import com.aspose.cells.PlacementType;

Picture pic = worksheet.getPictures().get(index);
pic.setPlacement(PlacementType.FREE_FLOATING);

// Add hyperlink to the picture
pic.addHyperlink("http://www.aspose.com/");
```  

### 步驟 5：設定螢幕提示並儲存工作簿
提供有用的工具提示，並將工作簿寫入磁碟。

```java
import com.aspose.cells.Hyperlink;

Hyperlink hlink = pic.getHyperlink();
hlink.setScreenTip("Click to go to Aspose site");

workbook.save("AIHyperlinks_out.xls");
```  

## 為何要在 Excel 圖片中加入超連結？

嵌入可點擊的圖片可將品牌元素、圖示或圖表轉換為直接的導向點，減少使用者前往相關內容所需的點擊次數。此方式可提升行銷儀表板、技術手冊與教育工作表的使用者效率。

## 如何在 Excel 中加入螢幕提示

您可以在附加於圖片的 `Hyperlink` 物件上呼叫 `hyperlink.setScreenTip("Your tip here")` 來加入螢幕提示。當游標懸停於圖像上時，提示會顯示，為使用者提供情境指引而不會弄亂工作表。

## 故障排除提示
- **圖像路徑錯誤** – 請再次確認檔案位置，並確保應用程式具有讀取權限。  
- **授權未套用** – 若試用版過期，超連結可能無法運作；請使用 `License.setLicense` 套用有效授權。  
- **超連結無法點擊** – 請確認圖片的 `PlacementType` 已設定為 `FREE_FLOATING`。

## 實務應用
嵌入可點擊圖像在許多情境中都很有用：

1. **行銷報告** – 將品牌標誌連結至產品頁面。  
2. **技術文件** – 附加圖表以開啟詳細的示意圖。  
3. **教育工作表** – 將圖示轉為補充影片的快捷方式。  
4. **專案儀表板** – 讓狀態圖示開啟相關的任務追蹤器。

## 效能考量
- 保持圖像檔案大小適中；大型圖片會增加工作簿的記憶體使用量。  
- 在迴圈處理大量檔案時，釋放未使用的物件（`workbook.dispose()`）。  
- 升級至最新的 Aspose.Cells 版本，以獲得效能提升與錯誤修正。

## 結論
您現在已了解如何使用 Aspose.Cells for Java 在 Excel 圖片中加入超連結，讓您能 **建立可點擊圖像的 Excel** 工作簿，使其更豐富且具互動性。可嘗試不同的 URL、螢幕提示與圖片放置方式，以符合您的報表需求。接下來，您或許會想探索在圖形上加入超連結，或在多個工作表中自動批量插入圖像。

## 常見問題

**Q:** Aspose.Cells for Java 支援的最大圖像尺寸是多少？  
**A:** 沒有嚴格限制，但非常大的圖像會影響效能並增加檔案大小。

**Q:** 我可以在 .xlsx 檔案中使用此功能嗎？  
**A:** 可以，API 同時支援 `.xls` 與 `.xlsx` 格式。

**Q:** 在新增超連結時應如何處理例外情況？  
**A:** 將程式碼包在 try‑catch 區塊中，並記錄 `Exception` 詳細資訊，以診斷路徑或授權問題。

**Q:** 加入後是否可以從圖像中移除超連結？  
**A:** 可以 – 取得 `Picture` 物件，呼叫 `pic.getHyperlink().remove()` 或從集合中刪除該圖片。

**Q:** 為何我的超連結可能無法如預期運作？  
**A:** 常見原因包括 URL 字串不正確、缺少 `http://`/`https://` 前綴，或未授權的試用版會停用某些功能。

## 其他資源
- **文件說明**： [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **下載**： [Aspose Cells Release](https://releases.aspose.com/cells/java/)  
- **購買與試用**： 前往 [Aspose Purchase](https://purchase.aspose.com/buy) 或 [Temporary License Page](https://purchase.aspose.com/temporary-license/) 了解授權選項。  
- **支援論壇**： 如需協助，請參考 [Aspose Support Forum](https://forum.aspose.com/c/cells/9)。

---

**最後更新：** 2026-09-02  
**測試環境：** Aspose.Cells for Java 25.3  
**作者：** Aspose

## 相關教學

- [如何使用 Aspose.Cells for Java 在 Excel 中建立超連結 - 步驟指南](/cells/java/advanced-features/create-hyperlinks-excel-aspose-cells-java/)
- [如何使用 Aspose.Cells for Java 為 Excel 儲存格設定樣式與加入超連結](/cells/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [使用 Aspose.Cells for Java 為 Excel 註解加入圖像：完整指南](/cells/java/comments-annotations/add-image-excel-comment-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}