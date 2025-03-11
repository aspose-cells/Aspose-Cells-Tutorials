---
title: XLSB檔案的外部連線讀寫
linktitle: XLSB檔案的外部連線讀寫
second_title: Aspose.Cells for .NET API 參考
description: 在此綜合教學中了解如何使用 Aspose.Cells for .NET 管理 XLSB 檔案中的外部連線。
weight: 130
url: /zh-hant/net/excel-workbook/read-and-write-external-connection-of-xlsb-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# XLSB檔案的外部連線讀寫

## 介紹

嘿，Excel 愛好者！您準備好進入 XLSB 檔案和外部連接的迷人世界了嗎？如果您曾經使用過 Excel，您就會知道它有多強大和多才多藝，但有時它也有其怪癖，尤其是在處理與外部資料庫的連接時。這就是 Aspose.Cells for .NET 的用武之地！這個漂亮的庫允許您以簡單的方式操作 Excel 文件。在本文中，我們將引導您逐步了解如何在 XLSB 檔案中讀取和寫入外部連線。

## 先決條件

在我們開始之前，您需要以下一些東西：

1. C# 基礎知識：了解 C# 程式語言將有很大幫助。如果您能夠輕鬆編寫 C# 程式碼，那麼就可以開始了！
2.  Aspose.Cells for .NET：您需要在開發環境中安裝此程式庫。如果您還沒有這樣做，您可以輕鬆下載[這裡](https://releases.aspose.com/cells/net/). 
3. IDE：您需要一個程式碼編輯器或整合開發環境 (IDE)，例如 Visual Studio。 
4. 範例 XLSB 檔案：我們將使用包含外部連接的範例 XLSB 檔案。您可以建立自己的範例或線上下載範例。 

一旦滿足了所有這些先決條件，我們就可以開始編寫程式碼了！

## 導入包

首先，讓我們在專案中導入必要的套件。確保您已在專案中新增對 Aspose.Cells 的引用。以下是在 C# 中執行此操作的方法：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

透過這些匯入，您可以存取操作 Excel 檔案及其連接所需的功能。

## 第 1 步：設定目錄

在使用 XLSB 檔案之前，您需要設定來源目錄和輸出目錄。此步驟對於保持文件井井有條至關重要。

```csharp
//原始碼目錄
string sourceDir = "Your Document Directory";
//輸出目錄
string outputDir = "Your Output Directory";
```

在此程式碼片段中，`"Your Document Directory"`和`"Your Document Directory"`假定取得輸入和輸出檔案所在位置的對應路徑。如果您願意，可以用硬編碼路徑替換這些方法。

## 第 2 步：載入 XLSB 文件

現在是時候將 Excel 檔案載入到 Workbook 物件中了。這使您能夠操縱其中的數據。

```csharp
//載入來源 Excel Xlsb 文件
Workbook wb = new Workbook(sourceDir + "sampleExternalConnection_XLSB.xlsb");
```

只需確保您的 XLSB 檔案位於指定的位置`sourceDir`。如果路徑正確，您的工作簿就可以進行操作了！

## 第 3 步：存取外部連接

載入工作簿後，您可以存取其外部連線。在我們的例子中，我們將檢索第一個資料庫連線。

```csharp
//讀取第一個外部連接，它實際上是一個 DB-Connection
Aspose.Cells.ExternalConnections.DBConnection dbCon = wb.DataConnections[0] as Aspose.Cells.ExternalConnections.DBConnection;
```

這裡，`DataConnections[0]`指工作簿中的第一個連接。我們將其鑄造為`DBConnection`類型以進行進一步操作。

## 第 4 步：提取連接訊息

現在您已經可以存取資料庫連線了，讓我們提取其詳細資訊並將其列印到控制台。這將幫助我們準確地了解我們正在做什麼。

```csharp
//列印 DB 連接的名稱、命令和連接訊息
Console.WriteLine("Connection Name: " + dbCon.Name);
Console.WriteLine("Command: " + dbCon.Command);
Console.WriteLine("Connection Info: " + dbCon.ConnectionInfo);
```

此步驟可讓您驗證外部連線的目前狀態。您將看到連接名稱、使用的命令以及列印到控制台的連接資訊。

## 步驟5：修改連接

有時，只需更改名稱即可使事情變得更清晰或符合新的命名約定。讓我們將現有的連線名稱變更為更相關的名稱。

```csharp
//修改連接名稱
dbCon.Name = "NewCust";
```

這行程式碼有效地將您的連線從原始名稱重新命名為“NewCust”。這是一個簡單但有影響力的改變！

## 第 6 步：儲存您的更改

進行修改後，您需要將變更儲存回 XLSB 檔案。操作方法如下：

```csharp
//儲存 Excel Xlsb 文件
wb.Save(outputDir + "outputExternalConnection_XLSB.xlsb");
```

此行程式碼儲存更新的工作簿，保留所有更改，包括新的連線名稱。

## 第7步：確認執行

最後，讓我們確認一切順利。最後一條簡單的訊息就會清楚地說明這一點。

```csharp
Console.WriteLine("ReadAndWriteExternalConnectionOfXLSBFile executed successfully.\r\n");
```

此訊息將向您保證您的程式碼已成功運行，並且所有變更均已按預期保存。

## 結論

現在你就擁有了！您已成功學習如何使用 Aspose.Cells for .NET 在 XLSB 檔案中讀取和寫入外部連線。透過執行這些步驟，您可以有效地管理 Excel 資料連接，讓您的 Excel 工作更加簡化、更少令人沮喪。請記住，無論您是處理大量資料集還是只是組織訊息，Aspose.Cells 都能提供您所需的工具。

## 常見問題解答

### 什麼是 .XLSB 檔？  
XLSB 檔案是一種二進位 Excel 檔案格式，以二進位格式儲存電子表格數據，使其更加緊湊且開啟速度更快。

### 如何安裝 Aspose.Cells for .NET？  
您可以輕鬆地從 Aspose 網站下載它[這裡](https://releases.aspose.com/cells/net/).

### 我可以免費使用 Aspose.Cells 嗎？  
是的！您可以從免費試用開始[這裡](https://releases.aspose.com/).

### Aspose.Cells 支援其他檔案格式嗎？  
絕對地！ Aspose.Cells 支援多種檔案格式，包括 XLSX、CSV 等。

### 如果遇到問題，我可以在哪裡尋求協助？  
您可以從 Aspose 論壇獲得支持[這裡](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
