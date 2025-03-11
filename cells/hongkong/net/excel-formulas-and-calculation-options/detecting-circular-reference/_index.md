---
title: 以程式設計方式偵測 Excel 中的循環引用
linktitle: 以程式設計方式偵測 Excel 中的循環引用
second_title: Aspose.Cells .NET Excel 處理 API
description: 使用 Aspose.Cells for .NET 輕鬆偵測 Excel 中的循環參考。請遵循我們的逐步指南，以確保電子表格中的計算準確。
weight: 13
url: /zh-hant/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 以程式設計方式偵測 Excel 中的循環引用

## 介紹
在處理 Excel 文件時，您可能遇到的最令人沮喪的問題之一是循環引用。當公式直接或間接引用回其自身的儲存格時，就會發生這種情況，從而創建一個可能會混淆 Excel 計算引擎的循環。但不要害怕！使用 Aspose.Cells for .NET，您可以以程式設計方式偵測這些討厭的循環引用，確保您的電子表格保持功能和準確。在本指南中，我們將逐步引導您完成整個過程，使其變得非常簡單。
## 先決條件
在我們深入探討檢測循環引用的細節之前，讓我們確保您已具備開始使用所需的一切：
1. Visual Studio：確保您的電腦上安裝了 Visual Studio。這將是您的開發環境。
2. .NET Framework：確保您使用的是相容版本的 .NET Framework（至少為 .NET Framework 4.0）。
3.  Aspose.Cells 函式庫：您需要擁有 Aspose.Cells 函式庫。您可以從[阿斯普斯網站](https://releases.aspose.com/cells/net/).
4. C# 基礎知識：熟悉 C# 程式設計將會很有幫助，因為我們將使用這種語言編寫程式碼。
5. Excel 文件：準備一個 Excel 文件，其中包含用於測試的循環參考。您可以建立一個簡單的或下載一個範例。
現在我們已經具備了先決條件，讓我們繼續有趣的部分！
## 導入包
在開始編碼之前，您需要匯入必要的套件。操作方法如下：
### 建立一個新項目
- 開啟 Visual Studio 並建立一個新的 C# 控制台應用程式專案。
### 加入 Aspose.Cells 參考
- 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
- 選擇“管理 NuGet 套件”。
- 搜尋“Aspose.Cells”並安裝最新版本。
### 導入所需的命名空間
在你的頂部`Program.cs`文件中，匯入必要的命名空間：
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

現在我們已完成所有設置，讓我們深入研究用於檢測 Excel 文件中的循環引用的程式碼。
## 第 1 步：定義輸入目錄
首先，您需要指定 Excel 檔案所在的目錄。您將在此處載入 Excel 文件。
```csharp
//輸入目錄
string sourceDir = "Your Document Directory";
```
代替`"Your Document Directory"`與 Excel 檔案的實際路徑。
## 第 2 步：使用 LoadOptions 載入工作簿
接下來，您將載入 Excel 工作簿。這就是魔法開始的地方！
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
在這裡，我們建立一個新實例`LoadOptions`並從指定路徑載入工作簿。確保您的 Excel 檔案名稱符合！
## 第 3 步：啟用迭代設定
為了允許循環引用，您需要在工作簿中啟用迭代設定。
```csharp
objWB.Settings.Iteration = true;
```
這告訴 Aspose.Cells 在計算過程中允許循環引用。
## 第 4 步：建立計算選項和循環監視器
現在，讓我們建立計算選項和自訂圓形監視器。
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
在這裡，我們建立一個實例`CalculationOptions`和一個習慣`CircularMonitor`。該監視器將幫助追蹤計算過程中發現的任何循環引用。
## 第 5 步：計算公式
現在，是時候計算工作簿中的公式了。
```csharp
objWB.CalculateFormula(copts);
```
該行執行計算並檢查循環引用。
## 第 6 步：計算循環引用
計算完成後，就可以統計找到了多少個循環引用。
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
這將輸出在 Excel 檔案中偵測到的循環引用的數量。
## 第 7 步：顯示結果
最後，讓我們顯示結果並確認我們的方法執行成功。
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## 第 8 步：實作 CircularMonitor 類
要完成該過程，您需要實施`CircularMonitor`班級。該類別將繼承自`AbstractCalculationMonitor`並處理循環引用的檢測。
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
此類捕獲找到的每個循環引用的詳細信息，包括工作表名稱和單元格索引。
## 結論
一旦將其分解為可管理的步驟，使用 Aspose.Cells for .NET 檢測 Excel 中的循環參考是一個簡單的過程。透過遵循本指南，您可以輕鬆識別和處理電子表格中的循環引用，確保您的計算保持準確和可靠。無論您是經驗豐富的開發人員還是新手，Aspose.Cells 都提供了強大的工具來增強您的 Excel 操作能力。 
## 常見問題解答
### Excel中的循環參考是什麼？
當公式引用回其自身的單元格時，就會發生循環引用，從而導致計算中出現無限循環。
### 如何以程式設計方式檢測循環引用？
您可以使用 .NET 中的 Aspose.Cells 函式庫透過實作自訂計算監視器以程式設計方式偵測循環參考。
### 使用 Aspose.Cells 的先決條件是什麼？
您需要安裝 Visual Studio、.NET Framework 和 Aspose.Cells 函式庫。
### 我可以免費使用 Aspose.Cells 嗎？
是的，Aspose.Cells 提供免費試用版，您可以使用它來探索其功能。
### 在哪裡可以找到有關 Aspose.Cells 的更多資訊？
您可以訪問[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/)取得詳細資訊和範例。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
