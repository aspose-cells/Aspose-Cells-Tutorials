---
title: 使用首選解析器開啟 CSV 文件
linktitle: 使用首選解析器開啟 CSV 文件
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 中的自訂解析器開啟和解析 CSV 檔案。輕鬆處理文字和日期。非常適合開發人員。
weight: 11
url: /zh-hant/net/csv-file-handling/csv-file-opening-csv-files-with-preferred-parser/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用首選解析器開啟 CSV 文件

## 介紹
處理 CSV 檔案時，有時您會想要使用自訂解析器處理不同的資料類型。本教學將指導您如何使用 Aspose.Cells for .NET 透過首選解析器開啟 CSV 檔案。無論您想要處理文字、日期或其他自訂格式，本指南都將引導您完成每個步驟，並提供清晰的解釋。
## 先決條件
在深入研究程式碼之前，讓我們先介紹一下入門所需的基本內容。
1.  Aspose.Cells for .NET Library：請確保您已安裝 Aspose.Cells 函式庫。你可以下載它[這裡](https://releases.aspose.com/cells/net/)。您也可以使用免費試用版[這裡](https://releases.aspose.com/).
2. .NET 開發環境：建議使用 Visual Studio，但任何相容於 .NET 的 IDE 都可以使用。
3. C# 基礎知識：本教學假設您熟悉 C# 和物件導向程式設計。
## 導入包
要使用 Aspose.Cells，您需要在 C# 檔案頂部匯入必要的命名空間：
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
現在我們已經做好準備，讓我們逐步了解如何使用首選解析器開啟 CSV 文件，處理不同的資料格式（例如文字和日期）。
## 第 1 步：定義自訂解析器
要處理不同的資料類型，例如文字或特定的日期格式，您需要定義自訂解析器。在 Aspose.Cells 中，自訂解析器實現`ICustomParser`介面.
### 1.1 建立文字解析器
此解析器處理常規文字值。它不會修改格式，因此值按原樣返回。
```csharp
class TextParser : ICustomParser
{
    public object ParseObject(string value)
    {
        return value;
    }
    public string GetFormat()
    {
        return "";
    }
}
```
這`ParseObject`方法只是傳回輸入值。這就像在說：“不要更改任何內容，只需給我文字即可！”
### 1.2 建立日期解析器
對於日期，您需要確保 CSV 資料正確解析為`DateTime`對象。以下是建立日期解析器的方法：
```csharp
class DateParser : ICustomParser
{
    public object ParseObject(string value)
    {
        DateTime myDate = DateTime.ParseExact(value, "dd/MM/yyyy", 
            System.Globalization.CultureInfo.InvariantCulture);
        return myDate;
    }
    public string GetFormat()
    {
        return "dd/MM/yyyy";
    }
}
```
在此解析器中，我們使用`ParseExact`確保根據預定義格式正確解釋日期（`"dd/MM/yyyy"`）。這樣，您的 CSV 中任何遵循此格式的日期都將毫無問題地進行處理。
## 第 2 步：配置載入選項
接下來，您需要配置 CSV 檔案的載入方式。這是使用以下方法完成的`TxtLoadOptions`類，它允許您指定解析選項，包括編碼和自訂解析器。
### 2.1 設定載入選項
我們先初始化`TxtLoadOptions`並定義關鍵參數，例如分隔符號和編碼：
```csharp
TxtLoadOptions oTxtLoadOptions = new TxtLoadOptions(LoadFormat.Csv);
oTxtLoadOptions.Separator = Convert.ToChar(",");
oTxtLoadOptions.Encoding = Encoding.UTF8;
oTxtLoadOptions.ConvertDateTimeData = true;
```
- 分隔符號：定義用於分隔 CSV 檔案中的值的字元（在本例中為逗號）。
- 編碼：我們使用 UTF-8 編碼來處理各種字元。
-  ConvertDateTimeData：將此設為 true 可確保日期值自動轉換為`DateTime`盡可能的對象。
### 2.2 應用自訂解析器
接下來，我們將指派先前建立的解析器來處理 CSV 中的值：
```csharp
oTxtLoadOptions.PreferredParsers = new ICustomParser[] 
{ 
    new TextParser(), 
    new DateParser() 
};
```
這告訴 Aspose.Cells 使用`TextParser`對於一般文字值和`DateParser`對於 CSV 檔案中遇到的任何日期欄位。
## 第 3 步：載入並讀取 CSV 文件
現在已經配置了載入選項，您可以將 CSV 檔案載入到`Aspose.Cells.Workbook`目的。
### 3.1 載入CSV文件
我們透過傳遞文件路徑和配置來載入 CSV 文件`TxtLoadOptions`到`Workbook`構造函數：
```csharp
string sourceDir = "Your Document Directory";
Workbook oExcelWorkBook = new Aspose.Cells.Workbook(sourceDir + "samplePreferredParser.csv", oTxtLoadOptions);
```
此步驟將您的 CSV 資料轉換為功能齊全的 Excel 工作簿，並根據您的首選規則解析每個值。
## 第 4 步：存取並顯示儲存格數據
將 CSV 載入到工作簿後，您就可以開始使用資料。例如，您可能想要列印特定儲存格的類型和值。
### 4.1 檢索並顯示儲存格A1
讓我們檢索第一個儲存格 (A1) 並顯示其值和類型：
```csharp
Cell oCell = oExcelWorkBook.Worksheets[0].Cells["A1"];
Console.WriteLine("A1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
在這裡，`Type`屬性顯示資料類型（例如`String`或者`DateTime`）， 和`DisplayStringValue`為您提供格式化的值。
### 4.2 檢索並顯示儲存格B1
同樣，我們可以檢索並顯示另一個單元格，例如 B1：
```csharp
oCell = oExcelWorkBook.Worksheets[0].Cells["B1"];
Console.WriteLine("B1: " + oCell.Type.ToString() + " - " + oCell.DisplayStringValue);
```
您可以根據需要檢查的數量重複此過程。
## 第 5 步：儲存工作簿
使用資料後，您可能希望將工作簿儲存到新文件中。 Aspose.Cells 透過簡單的操作使這變得容易`Save`方法：
```csharp
string outputDir = "Your Document Directory";
oExcelWorkBook.Save(outputDir + "outputsamplePreferredParser.xlsx");
```
這會將工作簿另存為 Excel 文件，並保留您套用的所有格式和資料解析。
## 結論
在 Aspose.Cells for .NET 中使用首選解析器開啟 CSV 檔案是處理不同資料類型的靈活且強大的方法。透過建立自訂解析器並配置載入選項，您可以確保您的 CSV 檔案完全按照您需要的方式進行解析，無論您處理的是文字、日期還是其他自訂格式。透過本教程，您現在可以處理專案中更複雜的資料解析場景。
## 常見問題解答
### Aspose.Cells for .NET 中自訂解析器的用途是什麼？
自訂解析器可讓您定義載入 CSV 檔案時應如何解析特定資料類型（例如文字或日期）。
### 我可以在 CSV 檔案中使用不同的分隔符號嗎？
是的，您可以指定任何字元作為分隔符`TxtLoadOptions.Separator`財產。
### 載入 CSV 時如何處理 Aspose.Cells 中的編碼？
您可以設定`Encoding`的財產`TxtLoadOptions`任何編碼方案，如 UTF-8、ASCII 等。
### 如果 CSV 中的日期格式不同會發生什麼情況？
您可以使用自訂解析器定義特定的日期格式，確保正確解析日期值。
### 我可以將工作簿儲存為其他格式嗎？
是的，Aspose.Cells 允許您以各種格式儲存工作簿，例如 XLSX、CSV、PDF 等。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
