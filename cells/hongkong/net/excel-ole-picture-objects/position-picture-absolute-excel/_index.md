---
title: 在 Excel 中定位圖片（絕對）
linktitle: 在 Excel 中定位圖片（絕對）
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過這個全面的逐步教學，了解如何使用 Aspose.Cells for .NET 在 Excel 中絕對定位影像。
weight: 13
url: /zh-hant/net/excel-ole-picture-objects/position-picture-absolute-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中定位圖片（絕對）

## 介紹
您是否曾發現自己很難在 Excel 電子表格中正確定位影像？你並不孤單！許多用戶都面臨著這項挑戰，特別是當他們的數據視覺化需求需要絕對定位以獲得更好的美觀或清晰度時。好吧，別再猶豫了；本指南將引導您完成使用 Aspose.Cells for .NET 在 Excel 工作表中絕對定位圖片的簡單程序。無論您是從事 Excel 操作的開發人員還是希望增強報表的資料分析師，我們的逐步教學都可以幫助您簡化 Excel 使用影像的體驗！
## 先決條件
在深入研究程式碼和細節之前，您需要準備好一些東西：
1.  Aspose.Cells 函式庫：確保您擁有最新版本的 Aspose.Cells for .NET 函式庫。您可以從[發布頁面](https://releases.aspose.com/cells/net/).
2. 開發環境：確保您設定了有效的 .NET 開發環境。您可以使用 Visual Studio 或您選擇的任何其他 IDE。
3. C#基礎知識：熟悉C#程式語言將有利於理解程式碼片段。
4. 影像檔案：將影像檔案（例如「logo.jpg」）儲存在您計劃插入到 Excel 工作表中的指定文件目錄中。

## 導入包
首先，讓我們確保導入專案所需的套件。您的專案檔案應包含以下命名空間：
```csharp
using System.IO;
using Aspose.Cells;
```
透過導入這些命名空間，我們確保我們的程式可以利用 Aspose.Cells 提供的功能。
為了清楚起見，讓我們將其分解為可管理的步驟。
## 第 1 步：設定您的文件目錄
在此初始步驟中，您需要定義文件所在的目錄。這對於程式知道在哪裡保存或獲取文件至關重要。設定方法如下：
```csharp
string dataDir = "Your Document Directory";
```
只需更換`"Your Document Directory"`與影像檔案所在的實際路徑。這可能是這樣的`"C:\\Users\\YourUsername\\Documents\\"`.
## 第 2 步：實例化工作簿對象
接下來，您需要建立一個新的實例`Workbook`班級。該物件代表您的 Excel 檔案：
```csharp
Workbook workbook = new Workbook();
```
此時，您已準備好一個工作簿，可填入資料和影像。
## 第 3 步：新增工作表
現在您已經有了工作簿，您需要在其中新增工作表。這就是添加和定位圖像的神奇之處：
```csharp
int sheetIndex = workbook.Worksheets.Add();
```
此行在您的工作簿中建立一個新工作表並返回其索引，我們將其儲存在變數中`sheetIndex`.
## 第 4 步：取得新工作表
讓我們參考新建立的工作表。使用我們剛剛獲得的索引，我們可以存取工作表並對其進行操作：
```csharp
Worksheet worksheet = workbook.Worksheets[sheetIndex];
```
現在您可以使用`worksheet`物件添加內容，包括圖像。
## 第5步：新增圖片
現在是令人興奮的部分！這是我們將圖片添加到工作表中的地方。我們指定要錨定圖片的行索引和列索引（在本例中為儲存格“F6”，即第 5 行和第 5 列）：
```csharp
int pictureIndex = worksheet.Pictures.Add(5, 5, dataDir + "logo.jpg");
```
該行有效地將影像鎖定在相對於整個工作表的指定位置。然而，目前，它仍然需要與單元格一起調整大小。
## 步驟6：存取新新增的圖片
要進一步操作圖片，您需要存取其屬性：
```csharp
Aspose.Cells.Drawing.Picture picture = worksheet.Pictures[pictureIndex];
```
這樣，您就可以存取我們剛剛新增的映像的屬性！
## 第7步：設定圖片的絕對定位
要絕對定位圖片（以像素為單位），您需要使用`Left`和`Top`特性。您可以在此處控制影像的顯示位置：
```csharp
picture.Left = 60;
picture.Top = 10;
```
您可以根據需要調整這兩個值；它們分別代表影像的水平和垂直位置。
## 第 8 步：儲存 Excel 文件
最後，完成所有修改後，是時候儲存工作簿了：
```csharp
workbook.Save(dataDir + "book1.out.xls");
```
這將會建立一個名為的 Excel 文件`book1.out.xls`在您先前定義的文件目錄中，其中包含絕對放置圖片的工作表。

## 結論
現在你就擁有了！您已使用 Aspose.Cells for .NET 在 Excel 工作表中成功定位圖片並進行絕對定位。這個簡單的過程不僅增強了 Excel 文件的視覺呈現效果，而且還確保圖像準確地保持在您想要的位置 - 無論單元格大小和行高如何更改。現在，無論您是準備報告還是建立儀表板，您都可以確保您的圖片每次都完美放置。
## 常見問題解答
### 什麼是 Aspose.Cells for .NET？
Aspose.Cells for .NET 是一個 .NET 函式庫，使開發人員能夠以程式設計方式建立、操作和轉換 Excel 電子表格，而無需 Microsoft Excel。
### 我可以使用 Aspose.Cells 執行其他圖像操作嗎？
是的，除了定位之外，您還可以使用 Aspose.Cells 庫調整 Excel 電子表格中的圖像大小、旋轉和修改圖像。
### Aspose.Cells 可以免費使用嗎？
 Aspose.Cells 是一款商業產品，但您可以從其網站上的免費試用版開始[免費試用頁面](https://releases.aspose.com/).
### 如何取得 Aspose.Cells 的臨時授權？
您可以透過以下方式申請臨時許可證[臨時許可證頁面](https://purchase.aspose.com/temporary-license/)由 Aspose 提供。
### 在哪裡可以找到更多範例和文件？
這[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/)包含廣泛的資源，包括程式碼範例和更詳細的功能。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
