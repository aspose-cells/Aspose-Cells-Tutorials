---
title: 在 .NET 中以程式設計方式設定資料透視表的自動格式
linktitle: 在 .NET 中以程式設計方式設定資料透視表的自動格式
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此詳細的逐步教學中，了解如何使用 Aspose.Cells for .NET 以程式設計方式設定 Excel 資料透視表的自動格式。
weight: 18
url: /zh-hant/net/creating-and-configuring-pivot-tables/setting-auto-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中以程式設計方式設定資料透視表的自動格式

## 介紹
在分析資料時，Excel 中的資料透視表可以改變遊戲規則。它們允許您動態總結和分析數據，幫助您收集幾乎不可能手動提取的見解。但是，如果您想在 .NET 中自動化格式化資料透視表的過程該怎麼辦？在這裡，我將向您展示如何使用強大的 .NET 的 Aspose.Cells 庫以程式設計方式設定資料透視表的自動格式。
在本指南中，我們將探討要點，介紹先決條件，導入必要的包，然後深入了解逐步教程，讓您像專業人士一樣格式化資料透視表。聽起來不錯嗎？讓我們直接跳進去吧！
## 先決條件
在開始之前，讓我們確保您擁有開始所需的一切：
1. .NET 開發環境：確保您擁有 Visual Studio（或任何支援 .NET 的 IDE）的工作實例。
2.  Aspose.Cells 函式庫：為了順利處理 Excel 文件，您需要安裝 Aspose.Cells 函式庫。如果您還沒有這樣做，您可以從[下載頁面](https://releases.aspose.com/cells/net/).
3. C#基礎知識：熟悉C#程式設計將有助於您更好地理解步驟。
4.  Excel 文件（範本）：您首先需要一個 Excel 範本文件，我們的範例將對其進行處理。為簡單起見，您可以建立一個名為的範例文件`Book1.xls`.
## 導入包
要在專案中使用 Aspose.Cells，您需要匯入必要的套件。以下是在 .NET 專案中進行設定的方法：
### 建立一個新項目
首先在您首選的 IDE 中建立一個新的 .NET 專案。 
### 新增參考文獻
確保新增對 Aspose.Cells 庫的引用。如果您下載了該程式庫，請新增提取的 DLL。如果您使用 NuGet，則只需執行：
```bash
Install-Package Aspose.Cells
```
### 導入命名空間
現在，在程式碼檔案中，您需要匯入 Aspose.Cells 命名空間。您可以透過在 C# 檔案頂部新增以下行來完成此操作：
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
完成這些步驟後，您就可以編寫一些程式碼了！
現在，讓我們將您提供的程式碼分解為詳細的步驟，並解釋每個部分的作用。 
## 第 1 步：定義您的文件目錄
首先，您需要設定 Excel 檔案所在文件目錄的路徑。在我們的範例中，我們將這樣定義它：
```csharp
string dataDir = "Your Document Directory";  //根據需要修改
```
此行建立一個字串變數`dataDir`它保存文檔的文件路徑。確保更換`"Your Document Directory"`與系統上的實際路徑。
## 步驟2：載入模板文件
接下來，您需要載入包含資料透視表的現有工作簿：
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
該行初始化一個新的`Workbook`透過載入指定的 Excel 檔案來取得物件。該文件應至少包含一個資料透視表，以便後續步驟有效。
## 第 3 步：存取所需的工作表
確定您需要處理哪個工作表才能存取資料透視表。在這種情況下，我們只會得到第一個：
```csharp
int pivotIndex = 0;  //資料透視表的索引
Worksheet worksheet = workbook.Worksheets[0];
```
這裡，`worksheet`從工作簿中檢索第一個工作表。資料透視表索引設定為`0`，這意味著我們正在存取該工作表中的第一個資料透視表。
## 步驟 4：找到資料透視表
準備好工作表後，就可以存取資料透視表了：
```csharp
PivotTable pivotTable = worksheet.PivotTables[pivotIndex];
```
這會初始化一個新的`PivotTable`透過從工作表中取得指定索引處的資料透視表來取得物件。
## 第5步：設定自動格式屬性
現在進入有趣的部分：為資料透視表設定自動格式選項。
```csharp
pivotTable.IsAutoFormat = true; //啟用自動格式
```
該行啟用資料透視表的自動格式功能。當設定為`true`，資料透視表將根據預先定義的樣式自動格式化自身。
## 步驟 6：選擇特定的自動格式類型
我們還需要指定資料透視表應採用哪種自動格式樣式。 Aspose.Cells 有多種格式可供我們選擇。設定方法如下：
```csharp
pivotTable.AutoFormatType = Aspose.Cells.Pivot.PivotTableAutoFormatType.Report5;
```
透過這一行，我們為資料透視表指派特定的自動格式類型。`Report5`只是一種風格的範例；您可以根據需要從多種選項中進行選擇。 
## 第 7 步：儲存工作簿
最後，不要忘記在進行所有更改後保存工作簿：
```csharp
workbook.Save(dataDir + "output.xls");
```
這行程式碼將修改後的工作簿儲存到一個名為`output.xls`在指定目錄中。請務必檢查此文件以查看格式精美的資料透視表！
## 結論
恭喜！您剛剛使用 .NET 中的 Aspose.Cells 將 Excel 資料透視表編程為自動格式化。此過程不僅可以節省您準備報告的時間，還可以確保每次運行時資料外觀的一致性。只需幾行程式碼，您就可以顯著增強您的 Excel 檔案 — 就像數位魔術師一樣。
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的 .NET 程式庫，用於處理 Excel 文件，無需安裝 Microsoft Excel。
### 我可以格式化工作簿中的多個資料透視表嗎？
是的，您可以循環存取工作簿中的多個資料透視表對象，以一一格式化它們。
### Aspose.Cells 是否有免費試用版？
絕對地！您可以從可用的免費試用版開始[這裡](https://releases.aspose.com/).
### 如果我的資料透視表格式不正確怎麼辦？
確保正確引用資料透視表並且存在自動格式類型 - 否則，它可能會回退到預設值。
### 我可以透過計劃任務自動執行此程序嗎？
是的！透過將此程式碼合併到排程任務中，您可以定期自動產生報告並設定格式。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
