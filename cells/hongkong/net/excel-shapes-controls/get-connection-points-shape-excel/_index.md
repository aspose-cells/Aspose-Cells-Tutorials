---
title: 在Excel中取得形狀的連接點
linktitle: 在Excel中取得形狀的連接點
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 在 Excel 中取得形狀連接點。按照我們的逐步指南，以程式設計方式輕鬆提取和顯示形狀點。
weight: 11
url: /zh-hant/net/excel-shapes-controls/get-connection-points-shape-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在Excel中取得形狀的連接點

## 介紹
以程式設計方式處理 Excel 檔案時，我們經常需要與工作表中嵌入的形狀進行互動。您可以執行的更高級任務之一是從形狀中提取連接點。連接點用於透過連接器連接形狀並更精確地管理其佈局。如果您想在 Excel 中取得形狀的連接點，Aspose.Cells for .NET 就是您需要的工具。在本教程中，我們將引導您逐步完成此任務。
## 先決條件
在深入研究程式碼之前，請確保您符合以下先決條件：
- Aspose.Cells for .NET：您需要在開發環境中安裝 Aspose.Cells。如果您還沒有，您可以[在這裡下載最新版本](https://releases.aspose.com/cells/net/).
- 開發環境：確保您安裝了可以正常運作的 Visual Studio 或任何其他 .NET 相容的 IDE。
- C# 基礎知識：本教學假設您對 C# 程式設計和物件導向原理有基本了解。
您也可以註冊一個[免費試用 Aspose.Cells](https://releases.aspose.com/)如果你還沒有。這將使您能夠存取本指南所需的所有功能。

## 導入包
要在專案中使用 Aspose.Cells，您需要包含必要的命名空間。以下導入語句應放置在程式碼的頂部：
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing;
```
這些命名空間可讓您存取 Aspose.Cells 的核心功能，並讓您操作工作表和形狀。

## 取得形狀連接點的逐步指南
在本節中，我們將引導您了解如何擷取 Excel 工作表中形狀的連接點。仔細遵循每個步驟以獲得清晰的理解。
## 第 1 步：實例化新工作簿
首先，我們需要建立一個實例`Workbook`班級。這代表 Aspose.Cells 中的 Excel 檔案。如果您沒有現有文件，沒問題 — 您可以從空白工作簿開始。
```csharp
//實例化一個新的工作簿
Workbook workbook = new Workbook();
```
在此步驟中，我們建立了一個空的 Excel 工作簿，但您也可以透過將檔案路徑傳遞到`Workbook`構造函數。
## 第 2 步：存取第一個工作表
接下來，我們需要存取要處理形狀的工作表。在本例中，我們將使用工作簿的第一個工作表。
```csharp
//取得工作簿中的第一個工作表
Worksheet worksheet = workbook.Worksheets[0];
```
此行存取工作簿中工作表集合中的第一個工作表。如果您正在使用特定工作表，則可以取代索引`0`與所需的索引。
## 第 3 步：新增文字方塊（形狀）
現在，讓我們為工作表新增一個形狀。我們將創建一個文字框，它是一種形狀。您也可以添加其他類型的形狀，但為了簡單起見，我們將在本教程中堅持使用文字方塊。
```csharp
//將新文字方塊新增至集合中
int textboxIndex = worksheet.TextBoxes.Add(2, 1, 160, 200);
```
這是我們所做的：
- 在行中新增了一個文字框`2`， 柱子`1`.
- 將文字方塊的尺寸設定為`160`寬度單位和`200`高度單位。
## 第 4 步：從 Shapes 集合中存取形狀
新增文字方塊後，它就成為工作表形狀集合的一部分。現在我們將使用以下方法存取該形狀`Shapes`收藏。
```csharp
//從形狀集合中存取形狀（文字方塊）
Shape shape = workbook.Worksheets[0].Shapes[0];
```
在此步驟中，我們從集合中檢索第一個形狀（我們的文字方塊）。如果您有多個形狀，您可以指定索引，甚至可以按名稱尋找形狀。
## 第 5 步：檢索連接點
現在我們已經有了形狀，讓我們提取它的連接點。這些點用於將連接器連接到形狀。這`ConnectionPoints`形狀的屬性傳回所有可用的連接點。
```csharp
//取得該形狀的所有連接點
var connectionPoints = shape.ConnectionPoints;
```
這為我們提供了該形狀可用的所有連接點的集合。
## 第 6 步：顯示連接點
最後，我們要顯示每個連接點的座標。這是我們循環連接點並將它們列印到控制台的地方。
```csharp
//顯示所有形狀點
foreach (var pt in connectionPoints)
{
    System.Console.WriteLine(string.Format("X = {0}, Y = {1}", pt.X, pt.Y));
}
```
此循環遍歷每個連接點並列印`X`和`Y`座標。這對於調試或直觀地確認形狀的連接點非常有用。
## 步驟7：執行並完成
設定完上述所有步驟後，您就可以執行程式碼了。這是確保該過程成功完成的最後一行：
```csharp
System.Console.WriteLine("GetShapeConnectionPoints executed successfully.");
```
此行只是將一條訊息記錄到控制台，指示該過程已完成。

## 結論
在本教學中，我們介紹如何使用 Aspose.Cells for .NET 在 Excel 中擷取形狀的連接點。透過將任務分解為易於理解的小步驟，我們探索了建立工作簿、添加形狀和提取連接點的過程。
透過了解如何以程式設計方式操作形狀，您可以開啟建立動態和互動式 Excel 工作表的無限可能。無論您是建立報告、設計儀表板還是建立圖表，這些知識都會派上用場。
## 常見問題解答
### 什麼是形狀中的連接點？
連接點是形狀上的特定點，您可以在其中連接連接器或將其連結到其他形狀。
### 我可以檢索工作表中所有形狀的連接點嗎？
是的，Aspose.Cells 允許您檢索支援它們的任何形狀的連接點。只需循環遍歷工作表中的形狀集合即可。
### 我需要許可證才能使用 Aspose.Cells 嗎？
是的，雖然您可以免費試用，但完整功能需要許可證。你可以[在這裡購買許可證](https://purchase.aspose.com/buy)或得到一個[臨時執照](https://purchase.aspose.com/temporary-license/).
### 如何在 Aspose.Cells 中加入不同類型的形狀？
您可以使用`Add`適用於矩形、橢圓形等形狀的方法。每個形狀都有您可以自訂的特定參數。
### 如何載入現有 Excel 文件而不是建立新文件？
若要載入現有文件，請將文件路徑傳遞給`Workbook`構造函數，像這樣：  
```csharp
Workbook workbook = new Workbook("path_to_file.xlsx");
```
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
