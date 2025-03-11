---
title: 在工作表中實施凍結窗格
linktitle: 在工作表中實施凍結窗格
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過這份詳細的逐步指南，了解如何使用 Aspose.Cells for .NET 在 Excel 中實現凍結窗格。有效增強工作表的可用性。
weight: 15
url: /zh-hant/net/worksheet-display/implement-freeze-panes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在工作表中實施凍結窗格

## 介紹
想像一下，您有一個包含大量資料集的 Excel 工作表，每次向下或橫向滾動時，您都會忘記那些重要的標題。如果這些標題在您滾動時可以保持在原位，那不是很方便嗎？這就是凍結窗格的用武之地，它使導航變得流暢而有效率。 Aspose.Cells for .NET 簡化了這個過程，使您能夠無縫地實現凍結窗格。本指南將引導您完成整個過程，逐步分解，以便您可以立即設定這些凍結的標頭。
## 先決條件
在投入之前，請確保您已準備好一些東西：
-  Aspose.Cells for .NET Library：您需要從以下位置下載庫：[Aspose 的發佈頁面](https://releases.aspose.com/cells/net/).
- 已安裝 .NET Framework：確保您的開發環境中已設定 .NET。
- C# 基礎知識：熟悉 C# 將有助於後續操作。
- Excel 檔案：準備一個 Excel 檔案（例如「book1.xls」），您將對其套用凍結窗格。
您可以在其網站上探索有關 Aspose.Cells 的更多詳細信息[文件頁](https://reference.aspose.com/cells/net/).

## 導入包
讓我們從導入必要的套件開始。打開您的 C# 項目，並確保導入這些：
```csharp
using System.IO;
using Aspose.Cells;
```
設定好軟體包後，讓我們進入逐步指南。
我們將詳細介紹使用 Aspose.Cells for .NET 設定凍結窗格的每個階段。仔細執行每個步驟，您將毫不費力地將凍結窗格套用至您的工作表。
## 第 1 步：定義文檔目錄的路徑
在開啟 Excel 檔案之前，您需要指定文件的路徑。設定一個`dataDir`儲存檔案目錄路徑的變數。
```csharp
//文檔目錄的路徑。
string dataDir = "Your Document Directory";
```
代替`"Your Document Directory"`與儲存 Excel 檔案的實際路徑。這將幫助程式找到您的文件。
## 步驟 2：使用 FileStream 開啟 Excel 文件
接下來，我們需要載入 Excel 文件，以便 Aspose.Cells 發揮其魔力。為此，我們將建立一個文件流並使用該流開啟 Excel 文件。
```csharp
//建立包含要開啟的 Excel 檔案的檔案流
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
透過使用文件流，您可以開啟文件供 Aspose.Cells 訪問，而無需更改原始文件，直到您明確保存任何更改為止。
## 第 3 步：實例化工作簿對象
文件流就位後，是時候創建一個`Workbook`目的。該物件至關重要，因為它代表整個 Excel 工作簿，可讓您處理文件中的各個工作表、儲存格和設定。
```csharp
//實例化 Workbook 物件
//透過檔案流程開啟Excel文件
Workbook workbook = new Workbook(fstream);
```
想想`Workbook`作為將所有紙張固定在一起的活頁夾。打開活頁夾後，您可以訪問其中的任何頁面（工作表）。
## 第 4 步：存取第一個工作表
現在您的工作簿已加載，您可以選擇要套用凍結窗格的工作表。在此範例中，我們將使用第一張工作表。 Aspose.Cells 可以輕鬆地透過索引選擇工作表。
```csharp
//存取 Excel 文件中的第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```
如果您需要在不同的工作表上工作，只需調整索引即可`workbook.Worksheets[0]`.
## 第 5 步：套用凍結窗格設定
這就是奇蹟發生的地方！若要設定凍結窗格，請使用`FreezePanes`方法，指定要開始凍結的行和列，以及要凍結的行數和列數。
```csharp
//套用凍結窗格設定
worksheet.FreezePanes(3, 2, 3, 2);
```
我們來分解一下參數：
- 第一行 (3)：從第 3 行開始凍結。
- 第一列 (2)：從第 2 列開始凍結。
- 行計數 (3)：凍結 3 行。
- 列數 (2)：凍結 2 列。
根據您的具體需求調整這些數值。凍結點將是指定行和列的交點。
## 步驟6：保存修改後的Excel文件
套用凍結窗格後，就可以儲存變更了。儲存修改後的工作簿檔案可確保保留您的凍結設定。您可以使用以下命令儲存更新的文件`Save`方法。
```csharp
//儲存修改後的Excel文件
workbook.Save(dataDir + "output.xls");
```
如果您還想保留原始文件，請確保使用不同的名稱來保存它。
## 步驟7：關閉文件流
最後，記得關閉文件流。這將釋放系統資源並完成所有開啟的檔案連線。
```csharp
//關閉文件流以釋放所有資源
fstream.Close();
```
可以將關閉流視為在完成文件後將文件放回架子上。這是一個好的看家習慣。

## 結論
恭喜！您已使用 Aspose.Cells for .NET 成功將凍結窗格套用到 Excel 工作表。此技術對於管理大型資料集非常有用，可確保在捲動資料時標題或特定行和列保持可見。透過遵循此逐步指南，您可以自信地實施凍結窗格並增強電子表格的可用性。
## 常見問題解答
### 我可以凍結工作簿中的多張工作表嗎？
是的，只需重複`FreezePanes`方法在您想要應用它的每張紙上。
### 如果我使用超出工作表範圍的行和列值，會發生什麼情況？
Aspose.Cells 會拋出異常，因此請確保您的值在工作表的範圍內。
### 我可以在應用凍結窗格設定後調整它們嗎？
絕對地！只需致電`FreezePanes`再次使用新參數來更新設定。
### 凍結窗格適用於所有版本的 Excel 檔案嗎？
是的，凍結窗格將以 Aspose.Cells 支援的大多數 Excel 格式（例如 XLS、XLSX）保留。
### 我可以解凍窗格嗎？
若要刪除凍結窗格，只需調用`UnfreezePanes()`在工作表上。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
