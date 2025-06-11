---
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 中取得形狀連接點。按照我們的逐步指南，可以輕鬆地以程式設計方式提取和顯示形狀點。"
"linktitle": "在 Excel 中取得形狀的連結點"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 Excel 中取得形狀的連結點"
"url": "/zh-hant/net/excel-shapes-controls/get-connection-points-shape-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 Excel 中取得形狀的連結點

## 介紹
當以程式方式處理 Excel 檔案時，我們經常需要與工作表中嵌入的形狀進行互動。您可以執行的更高級的任務之一是從形狀中提取連接點。連接點用於將形狀與連接器連接起來並更精確地管理其佈局。如果您希望取得 Excel 中形狀的連結點，Aspose.Cells for .NET 就是您需要的工具。在本教程中，我們將引導您逐步實現這一目標。
## 先決條件
在深入研究程式碼之前，請確保您符合以下先決條件：
- Aspose.Cells for .NET：您需要在開發環境中安裝 Aspose.Cells。如果你還沒有，你可以 [點此下載最新版本](https://releases。aspose.com/cells/net/).
- 開發環境：確保您已安裝 Visual Studio 或任何其他與 .NET 相容的 IDE。
- C# 基礎知識：本教學假設您對 C# 程式設計和物件導向原則有基本的了解。
您也可以註冊 [Aspose.Cells 免費試用](https://releases.aspose.com/) 如果你還沒有這樣做的話。這將使您能夠存取本指南所需的所有功能。

## 導入包
為了在您的專案中使用 Aspose.Cells，您需要包含必要的命名空間。以下導入語句應放在程式碼的頂部：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
這些命名空間讓您可以存取 Aspose.Cells 的核心功能，並讓您操作工作表和形狀。

## 取得形狀連接點的逐步指南
在本節中，我們將引導您了解如何擷取 Excel 工作表內形狀的連接點。仔細遵循每個步驟以獲得清晰的理解。
## 步驟 1：實例化新工作簿
首先，我們需要創建一個 `Workbook` 班級。這代表 Aspose.Cells 中的 Excel 檔案。如果您沒有現有文件，沒問題 - 您可以從空白工作簿開始。
```csharp
// 實例化新的工作簿
Workbook workbook = new Workbook();
```
在此步驟中，我們建立了一個空的 Excel 工作簿，但您也可以透過將檔案路徑傳遞給 `Workbook` 構造函數。
## 第 2 步：存取第一個工作表
接下來，我們需要存取我們想要使用形狀的工作表。在這種情況下，我們將使用工作簿的第一個工作表。
```csharp
// 取得工作簿中的第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```
此行從工作簿的工作表集合中存取第一個工作表。如果您正在使用特定工作表，則可以取代索引 `0` 使用所需的索引。
## 步驟 3：新增文字方塊（形狀）
現在，讓我們為工作表新增一個形狀。我們將創建一個文字框，它是一種形狀。您也可以添加其他類型的形狀，但為了簡單起見，我們將在本教程中堅持使用文字方塊。
```csharp
// 在集合中新增新的文字框
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
以下是我們所做的工作：
- 在行中新增了文字框 `2`， 柱子 `1`。
- 將文字方塊的尺寸設定為 `160` 寬度單位和 `200` 高度單位。
## 步驟 4：從 Shapes 集合存取 Shape
一旦我們新增了文字框，它就會成為工作表形狀集合的一部分。現在我們將使用 `Shapes` 收藏。
```csharp
// 從形狀集合存取形狀（文字方塊）
Shape shape = workbook.Worksheets[0].Shapes[0];
```
在這一步驟中，我們從集合中檢索第一個形狀（我們的文字方塊）。如果您有多個形狀，您可以指定索引，甚至可以透過名稱找到形狀。
## 步驟 5：檢索連接點
現在我們有了形狀，讓我們提取它的連接點。這些點用於將連接器附加到形狀。這 `ConnectionPoints` 形狀的屬性傳回所有可用的連接點。
```csharp
// 取得此形狀中的所有連接點
var connectionPoints = shape.ConnectionPoints;
```
這為我們提供了該形狀可用的所有連接點的集合。
## 步驟6：顯示連接點
最後，我們要顯示每個連接點的座標。這是我們循環遍歷連接點並將它們列印到控制台的地方。
```csharp
// 顯示所有形狀點
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
此循環遍歷每個連接點並列印 `X` 和 `Y` 座標。這對於調試或直觀地確認形狀的連接點很有用。
## 步驟 7：執行並完成
設定完上述所有步驟後，即可執行程式碼。這是確保該過程成功完成的最後一行：
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
此行只是向控制台記錄一條訊息，表示該過程已完成。

## 結論
在本教學中，我們介紹如何使用 Aspose.Cells for .NET 擷取 Excel 中形狀的連接點。透過將任務分解為小的、易於理解的步驟，我們探索了創建工作簿、添加形狀和提取連接點的過程。
透過了解如何以程式設計方式操作形狀，您可以解鎖建立動態和互動式 Excel 表的無限可能性。無論您是建立報告、設計儀表板還是建立圖表，這些知識都將派上用場。
## 常見問題解答
### 形狀中的連接點是什麼？
連接點是形狀上的特定點，您可以在此連接或將其連結到其他形狀。
### 我可以檢索工作表中所有形狀的連接點嗎？
是的，Aspose.Cells 允許您檢索支援它們的任何形狀的連接點。只需循環遍歷工作表中的形狀集合。
### 我需要許可證才能使用 Aspose.Cells 嗎？
是的，雖然您可以免費試用，但要使用全部功能則需要許可證。你可以 [在這裡購買許可證](https://purchase.aspose.com/buy) 或得到 [臨時執照](https://purchase。aspose.com/temporary-license/).
### 如何在 Aspose.Cells 中加入不同類型的形狀？
您可以使用 `Add` 適用於矩形、橢圓形等形狀的方法。每種形狀都有您可以自訂的特定參數。
### 如何載入現有的 Excel 檔案而不是建立新檔案？
若要載入現有文件，請將文件路徑傳遞給 `Workbook` 建構函數，如下所示：  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}