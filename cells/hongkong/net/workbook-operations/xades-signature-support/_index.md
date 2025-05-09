---
"description": "了解如何使用 Aspose.Cells for .NET 在 Excel 工作簿中實作 XAdES 簽章支援。按照我們的逐步指南進行安全文件簽名。"
"linktitle": "使用 Aspose.Cells 在工作簿中支援 XAdESSignature"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "使用 Aspose.Cells 在工作簿中支援 XAdESSignature"
"url": "/zh-hant/net/workbook-operations/xades-signature-support/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 在工作簿中支援 XAdESSignature

## 介紹
在當今的數位世界中，數據的完整性和真實性至關重要。假設您正在傳送一份重要的 Excel 文檔，並且您想確保收件人知道它沒有被篡改。這就是數位簽名發揮作用的地方！使用 Aspose.Cells for .NET，您可以輕鬆地將 XAdES 簽章新增至您的 Excel 工作簿，確保您的資料保持安全可靠。在本教學中，我們將逐步引導您完成在 Excel 檔案中實現 XAdES 簽章支援的過程。讓我們開始吧！
## 先決條件
在開始之前，您需要做好以下幾點才能繼續學習本教學：
1. Aspose.Cells for .NET：請確保您已安裝 Aspose.Cells 函式庫。你可以下載它 [這裡](https://releases。aspose.com/cells/net/).
2. 開發環境：適合.NET開發的IDE，例如Visual Studio。
3. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解程式碼片段。
4. 數位憑證：一個有效的 PFX 檔案（個人資訊交換），其中包含您的數位憑證和存取它的密碼。
都拿到了嗎？偉大的！讓我們繼續下一步。
## 導入包
要開始使用 Aspose.Cells，您需要在 C# 專案中匯入必要的命名空間。這將允許您存取添加數位簽章所需的類別和方法。您可以按照以下步驟操作：
### 建立新的 C# 項目
1. 開啟 Visual Studio。
2. 建立一個新的控制台應用程式專案。
3. 給你的專案取一個容易辨識的名字，例如 `XAdESSignatureExample`。
### 新增 Aspose.Cells 引用
1. 在解決方案資源管理器中右鍵單擊您的專案並選擇 `Manage NuGet Packages`。
2. 搜尋 `Aspose.Cells` 並安裝最新版本。
### 導入必要的命名空間
在你的頂部 `Program.cs` 文件中，新增以下使用指令：
```csharp
using Aspose.Cells.DigitalSignatures;
using System;
using System.IO;
```
這將使您能夠在專案中使用 Aspose.Cells 類別和方法。
現在您已完成所有設置，讓我們將向工作簿添加 XAdES 簽名的過程分解為易於管理的步驟。
## 步驟 1：設定來源目錄和輸出目錄
在開始使用 Excel 檔案之前，您需要定義來源檔案的位置以及要儲存輸出檔案的位置。
```csharp
// 來源目錄
string sourceDir = "Your Document Directory";
// 輸出目錄
string outputDir = "Your Document Directory";
```
代替 `"Your Document Directory"` 使用您的 Excel 檔案的實際儲存路徑以及您想要儲存簽署檔案的位置。
## 第 2 步：載入工作簿
接下來，您將載入要簽署的 Excel 工作簿。這是使用 `Workbook` 來自 Aspose.Cells 的類別。
```csharp
Workbook workbook = new Workbook(sourceDir + "sourceFile.xlsx");
```
確保更換 `"sourceFile.xlsx"` 使用您的實際 Excel 檔案的名稱。
## 步驟3：準備您的數位證書
要新增數位簽名，您需要載入 PFX 檔案並提供其密碼。您可以按照以下步驟操作：
```csharp
string password = "pfxPassword"; // 替換為您的 PFX 密碼
string pfx = "pfxFile"; // PFX 檔案的路徑
```
確保更換 `"pfxPassword"` 使用您的實際密碼 `"pfxFile"` 以及您的 PFX 檔案的路徑。
## 步驟4：建立數位簽名
現在是時候使用 `DigitalSignature` 班級。您需要將 PFX 檔案讀入位元組數組，然後建立簽名。
```csharp
DigitalSignature signature = new DigitalSignature(File.ReadAllBytes(pfx), password, "testXAdES", DateTime.Now);
signature.XAdESType = XAdESType.XAdES;
```
這裡， `"testXAdES"` 是簽署的原因，並且 `DateTime.Now` 表示簽署時間。
## 步驟 5：將簽名新增至工作簿
要將簽名新增至工作簿，您需要建立一個 `DigitalSignatureCollection` 並添加您的簽名。
```csharp
DigitalSignatureCollection dsCollection = new DigitalSignatureCollection();
dsCollection.Add(signature);
```
## 步驟 6：將數位簽章設定為工作簿
現在您已經準備好了簽名集，是時候將其設定到工作簿了。
```csharp
workbook.SetDigitalSignature(dsCollection);
```
## 步驟 7：儲存工作簿
最後，保存應用了數位簽章的工作簿。
```csharp
workbook.Save(outputDir + "XAdESSignatureSupport_out.xlsx");
```
代替 `"XAdESSignatureSupport_out.xlsx"` 使用您想要的輸出檔名。
## 步驟8：確認成功
為了確保一切順利，您可以將成功訊息列印到控制台。
```csharp
Console.WriteLine("XAdESSignatureSupport executed successfully.");
```
## 結論
就是這樣！您已成功使用 Aspose.Cells for .NET 為您的 Excel 工作簿新增 XAdES 簽章支援。此強大功能不僅增強了文件的安全性，而且還有助於維護資料的完整性。如果您有任何疑問或遇到任何問題，請隨時查看 [Aspose.Cells 文檔](https://reference.aspose.com/cells/net/) 或訪問 [支援論壇](https://forum.aspose.com/c/cells/9) 尋求幫助。
## 常見問題解答
### 什麼是 XAdES？
XAdES（XML 進階電子簽名）是一種電子簽名標準，可確保電子文件的完整性和真實性。
### 我需要數位憑證才能使用 XAdES 簽章嗎？
是的，您需要一個有效的 PFX 格式的數位憑證來建立 XAdES 簽章。
### 我可以將 Aspose.Cells 用於其他檔案格式嗎？
是的，Aspose.Cells 主要適用於 Excel 文件，但它也支援各種其他電子表格格式。
### Aspose.Cells 有免費試用版嗎？
絕對地！您可以免費試用 [這裡](https://releases。aspose.com/).
### 在哪裡可以找到更多範例和教學？
您可以在 [Aspose.Cells網站](https://reference。aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}