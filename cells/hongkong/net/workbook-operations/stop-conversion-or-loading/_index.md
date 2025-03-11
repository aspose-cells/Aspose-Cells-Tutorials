---
title: 使用中斷監視器停止轉換或載入
linktitle: 使用中斷監視器停止轉換或載入
second_title: Aspose.Cells .NET Excel 處理 API
description: 透過詳細的逐步教學，了解如何使用中斷監視器在 Aspose.Cells for .NET 中停止工作簿轉換。
weight: 26
url: /zh-hant/net/workbook-operations/stop-conversion-or-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用中斷監視器停止轉換或載入

## 介紹
處理大型 Excel 文件通常涉及冗長的過程，可能會佔用時間和資源。但是，如果您意識到某些內容需要更改時可以中途停止轉換過程，該怎麼辦？ Aspose.Cells for .NET 有一個稱為中斷監視器的功能，它允許您中斷工作簿到另一種格式（如 PDF）的轉換。這可能是一個救星，尤其是在處理大量資料檔案時。在本指南中，我們將介紹如何使用 Aspose.Cells for .NET 中的中斷監視器來中斷轉換過程。
## 先決條件
在投入之前，請確保您已具備以下條件：
1.  Aspose.Cells for .NET - 下載[這裡](https://releases.aspose.com/cells/net/).
2. .NET 開發環境 - 例如 Visual Studio。
3. C# 程式設計的基本知識 - 熟悉 C# 文法將有助於您跟進。
## 導入包
首先，讓我們導入必要的套件。這些進口產品包括：
- Aspose.Cells：用於操作 Excel 檔案的主要庫。
- System.Threading：用於管理線程，因為本範例將執行兩個並行進程。
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
讓我們將這個過程分解為詳細的步驟。每個步驟將幫助您了解設定和使用中斷監視器來管理 Excel 工作簿轉換的重要性。
## 步驟1：建立類別並設定輸出目錄
首先，我們需要一個類別來封裝我們的函數，以及一個保存輸出檔案的目錄。
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
代替`"Your Document Directory"`與您想要儲存 PDF 檔案的實際路徑。
## 第 2 步：實例化中斷監視器
接下來，建立一個 InterruptMonitor 物件。該監視器將透過設定在任何給定點中斷過程的能力來幫助控制過程。
```csharp
InterruptMonitor im = new InterruptMonitor();
```
此中斷監視器將附加到我們的工作簿中，使我們能夠管理轉換過程。
## 步驟 3：設定轉換工作簿
現在，讓我們建立一個工作簿對象，為其分配 InterruptMonitor，然後存取第一個工作表以插入一些範例文字。
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
上面的程式碼會建立一個工作簿，為其設定 InterruptMonitor，並將文字放置在遠端儲存格中 (`J1000000`）。將文字放置在此單元格位置可確保處理工作簿將更加耗時，從而為 InterruptMonitor 提供足夠的時間進行幹預。
## 步驟 4：將工作簿另存為 PDF 並處理中斷
現在，我們嘗試將工作簿儲存為 PDF。我們將使用一個`try-catch`區塊來處理可能發生的任何中斷。
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
如果進程被中斷，異常將捕獲它並顯示適當的訊息。否則，工作簿將另存為 PDF。
## 第 5 步：中斷轉換過程
這裡的主要特點是能夠中斷流程。我們將使用添加延遲`Thread.Sleep`然後調用`Interrupt()`10秒後停止轉換的方法。
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
此延遲使工作簿有時間在發送中斷訊號之前開始轉換為 PDF。
## 第 6 步：同時執行線程
為了將所有內容整合在一起，我們需要在單獨的執行緒中啟動這兩個函數。這樣，工作簿轉換和中斷等待可以同時發生。
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
上面的程式碼運行`CreateWorkbookAndConvertItToPdfFormat`和`WaitForWhileAndThenInterrupt`在並行執行緒中，在兩個行程完成後將它們連接起來。
## 第7步：最終執行
最後，我們將添加一個`Run()`方法來執行程式碼。
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
這`Run`方法是啟動和觀察中斷操作的入口點。
## 結論
在本教學中，我們探討如何中斷 Aspose.Cells for .NET 中的轉換過程。處理大型 Excel 檔案時，中斷監視器是一個有用的工具，它允許您停止進程而無需等待它們完成。這在時間和資源寶貴且需要快速回饋的場景中尤其有用。
## 常見問題解答
### Aspose.Cells for .NET 中的中斷監視器是什麼？  
中斷監視器可讓您中途停止工作簿轉換或載入程序。
### 我可以將中斷監視器用於 PDF 以外的其他格式嗎？  
是的，您也可以中斷到其他支援格式的轉換。
### Thread.Sleep() 如何影響中斷計時？  
Thread.Sleep() 在觸發中斷之前建立一個延遲，為轉換開始提供時間。
### 我可以在 10 秒之前中斷該過程嗎？  
是的，修改延遲`WaitForWhileAndThenInterrupt()`到更短的時間。
### 中斷過程會影響效能嗎？  
影響很小，對於管理長期運作的流程非常有益。
欲了解更多信息，請參閱[Aspose.Cells for .NET 文檔](https://reference.aspose.com/cells/net/)。如果您需要協助，請查看[支援論壇](https://forum.aspose.com/c/cells/9)或得到一個[免費試用](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
