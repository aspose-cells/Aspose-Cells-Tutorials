---
title: 中斷或取消工作簿的公式計算
linktitle: 中斷或取消工作簿的公式計算
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此詳細的逐步指南中了解如何使用 Aspose.Cells for .NET 中斷 Excel 公式計算。
weight: 15
url: /zh-hant/net/excel-formulas-and-calculation-options/interrupt-or-cancel-formula-calculation-of-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 中斷或取消工作簿的公式計算

## 介紹
您是否厭倦了 Excel 計算運行時間超過應有的時間？有時您可能想要停止或中斷工作簿中冗長的公式計算。無論您要處理大量資料集還是複雜公式，了解如何控制此過程都可以為您節省大量時間和麻煩。在本文中，我們將引導您了解如何使用 Aspose.Cells for .NET 有效地中斷或取消 Excel 工作簿中的公式計算。 
## 先決條件
在我們深入學習教程之前，讓我們確保您已完成所有設定：
1. Visual Studio：您需要在電腦上安裝 Visual Studio。任何支援.NET開發的版本都可以。
2. Aspose.Cells for .NET：從下列位置下載並安裝 Aspose.Cells 函式庫：[這裡](https://releases.aspose.com/cells/net/).
3. C# 基礎知識：熟悉 C# 程式語言將很有幫助，因為我們將一起編寫程式碼片段。
4. Excel 檔案：在本教學中，我們將引用名為的範例 Excel 文件`sampleCalculationMonitor.xlsx`。確保您的作業目錄中有它。
一旦所有這些都準備就緒，我們就可以直接進入程式碼了！
## 導入包
在您的 Visual Studio 專案中，您需要匯入幾個與 Aspose.Cells 相關的命名空間。以下是您想要包含在程式碼檔案頂部的套件：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
透過包含這些命名空間，您將能夠存取操作 Excel 工作簿所需的類別和方法。
現在您已準備好先決條件和軟體包，讓我們將任務分解為可管理的步驟。每個步驟都會有一個標題和一個簡潔的解釋。
## 第 1 步：設定您的工作簿
首先，您需要載入工作簿。該文件包含您可能想要中斷的計算。方法如下：
```csharp
//原始碼目錄
string sourceDir = "Your Document Directory"; //使用您的實際目錄路徑進行更新。
Workbook wb = new Workbook(sourceDir + "sampleCalculationMonitor.xlsx");
```
在這一步中，我們創建一個`Workbook`透過將其指向我們的 Excel 檔案來實例化。這為所有進一步的行動奠定了基礎。
## 第 2 步：建立計算選項
接下來，我們將建立一個計算選項並將其與計算監視器類別配對。這對於控制我們的計算運作方式至關重要。
```csharp
CalculationOptions opts = new CalculationOptions();
opts.CalculationMonitor = new clsCalculationMonitor();
```
在這裡，我們實例化`CalculationOptions`並分配`clsCalculationMonitor`— 接下來我們將定義一個自訂類別。這將使我們能夠監控計算並應用中斷。
## 第 3 步：實施計算監視器
現在，讓我們創建我們的`clsCalculationMonitor`班級。該類別將繼承自`AbstractCalculationMonitor`並將包含我們中斷計算的邏輯。
```csharp
class clsCalculationMonitor : AbstractCalculationMonitor
{
    public override void BeforeCalculate(int sheetIndex, int rowIndex, int colIndex)
    {
        //尋找單元格名稱
        string cellName = CellsHelper.CellIndexToName(rowIndex, colIndex);
        //列印工作表、行和列索引以及儲存格名稱
        System.Diagnostics.Debug.WriteLine(sheetIndex + "----" + rowIndex + "----" + colIndex + "----" + cellName);
        //如果儲存格名稱為B8，則中斷/取消公式計算
        if (cellName == "B8")
        {
            this.Interrupt("Interrupt/Cancel the formula calculation");
        } //如果
    } //計算前
} //cls計算監視器
```
在這個類別中，我們重寫了`BeforeCalculate`方法，在任何單元格計算之前觸發。我們檢查當前單元格是否是`B8`。如果是的話，我們打電話`this.Interrupt()`停止計算。
## 第四步：計算有選項的公式
有了我們的選項和監視器，就可以執行計算了：
```csharp
wb.CalculateFormula(opts);
```
該命令將在監視中斷的同時執行計算。如果計算到B8，按照我們之前的邏輯就會停止。
## 結論
恭喜你自己！您剛剛學習如何使用 Aspose.Cells for .NET 中斷 Excel 工作簿中的公式計算。此過程使您可以更好地控制計算，確保它們不會不必要地拖延。 
無論您是開發複雜的財務模型還是處理大型資料集，管理運算都可以大大提高效能和可用性。我希望本教程能夠提供有關該主題的價值和清晰度。不要忘記進一步探索 Aspose.Cells 文件以發現更多功能。
## 常見問題解答
### 我可以免費使用 Aspose.Cells 嗎？
是的！您可以從 Aspose.Cells 的免費試用開始[這裡](https://releases.aspose.com/).
### 我可以使用 Aspose.Cells 開發哪些類型的應用程式？
您可以建立廣泛的應用程序，包括數據分析、報告工具和自動化 Excel 處理實用程式。
### 在我的 .NET 應用程式中實作 Aspose.Cells 是否困難？
一點也不！ Aspose.Cells 提供了優秀的文件和範例，幫助您將其順利整合到您的應用程式中。
### 我可以使用 Aspose.Cells 有條件地計算公式嗎？
是的！您可以根據應用程式的需求應用各種邏輯和計算，包括本教程中所示的中斷計算的條件。
### 在哪裡可以找到對 Aspose.Cells 的支援？
您可以透過 Aspose 論壇獲得支持[這裡](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
