---
title: 保護 Excel 工作表中的行
linktitle: 保護 Excel 工作表中的行
second_title: Aspose.Cells for .NET API 參考
description: 在本教學中了解如何使用 Aspose.Cells for .NET 保護 Excel 電子表格的行。 C# 逐步教學。
weight: 60
url: /zh-hant/net/protect-excel-file/protect-row-in-excel-worksheet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 保護 Excel 工作表中的行

## 介紹

使用 Excel 工作表時，通常需要保護特定行以保持資料的完整性。無論您是管理團隊專案、監督財務報告還是共用文檔，限制對某些行的存取都可以防止不必要的變更。在本教學中，我們將探討如何利用 Aspose.Cells for .NET 來保護 Excel 工作表中的特定行。因此，拿起您的編碼帽子，讓我們深入了解使用 C# 操作 Excel 的激動人心的世界！

## 先決條件

在我們開始實踐部分之前，讓我們確保您已完成所有設定。以下是一些先決條件：

1.  Aspose.Cells for .NET：從下列位置下載資料庫：[阿斯普斯網站](https://releases.aspose.com/cells/net/)。確保您擁有所有新功能和錯誤修復的最新版本。
2. Visual Studio：像 Visual Studio（社群版、專業版或企業版）這樣的整合開發環境 (IDE) 將協助您有效地編譯和執行 C# 程式碼。
3. .NET Framework：您需要 .NET Framework 的相容版本。 Aspose.Cells 支援多個版本，因此請確保您的版本是最新的。 
4. C# 基礎知識：對 C# 的基本了解將有助於我們在本指南中編寫程式碼。
5. 參考文件：熟悉[Aspose.Cells for .NET 文檔](https://reference.aspose.com/cells/net/)有關所使用的方法和類別的更多詳細資訊。

## 導入包

我們旅程的第一步是在 C# 專案中匯入必要的套件。 Aspose.Cells 透過一組我們需要包含的類別進行操作：

```csharp
using System.IO;
using Aspose.Cells;
```

現在我們已經匯入了所需的套件，讓我們逐步完成建立 Excel 工作簿並保護特定行的步驟。 

## 第 1 步：定義目錄

在此步驟中，我們將指定 Excel 檔案的儲存位置。確保該目錄存在非常重要，否則我們將在需要時以程式設計方式建立它。

```csharp
string dataDir = "YOUR DOCUMENT DIRECTORY"; //替換為您的文件路徑
bool IsExists = Directory.Exists(dataDir);
if (!IsExists)
{
    Directory.CreateDirectory(dataDir);
}
```
在此代碼中，替換`YOUR DOCUMENT DIRECTORY`與您要儲存 Excel 檔案的實際路徑。

## 第 2 步：建立新工作簿

接下來，我們將建立一個新的工作簿，所有操作都會在其中發生。這是一個基本步驟，就像在建造夢想之家之前奠定基礎一樣。

```csharp
Workbook wb = new Workbook();
```
這一行初始化了一個新的實例`Workbook`類，建立一個新的工作表供我們處理。

## 第 3 步：訪問工作表

建立工作簿後，讓我們開始處理第一個工作表。請記住，一個 Excel 檔案可以包含多個工作表，因此選擇正確的工作表至關重要。

```csharp
Worksheet sheet = wb.Worksheets[0]; //造訪第一張工作表
```

## 第 4 步：解鎖所有列

在鎖定特定行之前，最好先解鎖所有列。這使我們能夠控制哪些數據以後仍可編輯。

```csharp
Style style;
StyleFlag flag;

//循環遍歷所有列並解鎖它們
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
此循環迭代前 256 列，解鎖每一列以確保預設編輯權限。

## 步驟5：鎖定特定行

現在，我們將鎖定工作表的第一行。此步驟可確保使用者無法對該行中包含的關鍵資料進行未經授權的變更。

```csharp
style = sheet.Cells.Rows[0].Style; //取得第一行的樣式
style.IsLocked = true; //鎖定行
flag = new StyleFlag();
flag.Locked = true; //設定鎖定標誌
sheet.Cells.ApplyRowStyle(0, style, flag); //將樣式套用到第一行
```
在這裡，我們檢索第一行的樣式，將其標記為鎖定，並套用鎖定樣式。這類似於給一個重要的抽屜上一把鎖，這對於保護敏感資訊至關重要！

## 第 6 步：保護紙張

鎖定行後，讓我們採取額外的步驟並完全保護工作表。這將在定義的所有功能上強制執行鎖定`ProtectionType`.

```csharp
sheet.Protect(ProtectionType.All); //保護板材的所有功能
```
透過套用此保護，使用者無法編輯鎖定的行或進行任何可能影響鎖定區域的變更。

## 第 7 步：儲存工作簿

最後一步涉及保存工作簿。這是我們所有辛勤工作得到回報的地方，我們可以看到我們美麗的、受保護的電子表格變得栩栩如生！

```csharp
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
確保已儲存的檔案名稱和格式符合您的要求。在本例中，我們將其另存為較舊的 Excel 格式 (Excel 97-2003)。

## 結論

現在你就擁有了！您已成功學習如何使用 Aspose.Cells for .NET 保護 Excel 工作表中的特定行。只需幾行程式碼，您不僅創建了工作簿，而且還設法保護敏感訊息，確保您的 Excel 文件保持完整且值得信賴。無論是財務報告、考勤表或協作專案計劃，保護關鍵資料至關重要。 

## 常見問題解答

### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的 .NET 程式庫，可讓使用者以程式設計方式建立、操作和轉換 Excel 檔案。

### 我可以使用 Aspose.Cells 一次保護多行嗎？
是的，您可以透過迭代多行並對每行套用類似的樣式變更來擴展鎖定技術。

### 有沒有辦法在保護後解鎖行？
是的，您可以先取消保護工作表，然後調整`IsLocked`所需行的屬性，隨後重新套用保護。

### Aspose.Cells 是否支援 Excel 以外的其他格式？
絕對地！ Aspose.Cells 可以將工作簿轉換並儲存為各種格式，包括 CSV、PDF 和 HTML。

### 我可以在哪裡獲得 Aspose.Cells 的支援？
您可以訪問[Aspose 支援論壇](https://forum.aspose.com/c/cells/9)尋求幫助和社區指導。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
