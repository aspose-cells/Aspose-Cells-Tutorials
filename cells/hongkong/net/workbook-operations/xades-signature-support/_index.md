---
title: 使用 Aspose.Cells 的工作簿中的 XAdESSignature 支援
linktitle: 使用 Aspose.Cells 的工作簿中的 XAdESSignature 支援
second_title: Aspose.Cells .NET Excel 處理 API
description: 了解如何使用 Aspose.Cells for .NET 在 Excel 工作簿中實作 XAdES 簽章支援。請遵循我們的安全文件簽名逐步指南。
weight: 29
url: /zh-hant/net/workbook-operations/xades-signature-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 使用 Aspose.Cells 的工作簿中的 XAdESSignature 支援

## 介紹
在當今的數位世界中，數據完整性和真實性至關重要。想像一下，您正在發送一個重要的 Excel 文檔，並且您希望確保收件人知道該文檔沒有被篡改。這就是數位簽名發揮作用的地方！透過 Aspose.Cells for .NET，您可以輕鬆地將 XAdES 簽章新增至 Excel 工作簿中，確保您的資料保持安全且值得信賴。在本教學中，我們將引導您逐步完成在 Excel 檔案中實現 XAdES 簽章支援的過程。讓我們深入了解一下吧！
## 先決條件
在我們開始之前，您需要準備好一些東西才能遵循本教程：
1. Aspose.Cells for .NET：請確保您已安裝 Aspose.Cells 函式庫。你可以下載它[這裡](https://releases.aspose.com/cells/net/).
2. 開發環境：適合.NET開發的IDE，例如Visual Studio。
3. C# 基礎知識：熟悉 C# 程式設計將有助於您更好地理解程式碼片段。
4. 數位憑證：有效的 PFX 檔案（個人資訊交換），其中包含您的數位憑證和存取它的密碼。
東西都齊全了嗎？偉大的！讓我們繼續下一步。
## 導入包
要開始使用 Aspose.Cells，您需要在 C# 專案中匯入必要的命名空間。這將允許您存取添加數位簽章所需的類別和方法。您可以這樣做：
### 建立一個新的 C# 項目
1. 打開視覺工作室。
2. 建立一個新的控制台應用程式專案。
3. 將您的項目命名為易於識別的名稱，例如`XAdESSignatureExample`.
### 加入 Aspose.Cells 參考
1. 在解決方案資源管理器中右鍵單擊您的專案並選擇`Manage NuGet Packages`.
2. 搜尋`Aspose.Cells`並安裝最新版本。
### 導入必要的命名空間
在你的頂部`Program.cs`文件中，加入以下 using 指令：
```csharp
using Aspose.Cells.DigitalSignatures;
using System;
using System.IO;
```
這將使您能夠在專案中使用 Aspose.Cells 類別和方法。
現在您已完成所有設置，讓我們將向工作簿添加 XAdES 簽名的過程分解為可管理的步驟。
## 第 1 步：設定來源目錄和輸出目錄
在開始使用 Excel 檔案之前，您需要定義來源檔案所在的位置以及輸出檔案的儲存位置。
```csharp
//原始碼目錄
string sourceDir = "Your Document Directory";
//輸出目錄
string outputDir = "Your Document Directory";
```
代替`"Your Document Directory"`與儲存 Excel 檔案的實際路徑以及要儲存簽署檔案的位置。
## 第 2 步：載入工作簿
接下來，您將載入要簽署的 Excel 工作簿。這是使用以下方法完成的`Workbook`來自 Aspose.Cells 的類別。
```csharp
Workbook workbook = new Workbook(sourceDir + "sourceFile.xlsx");
```
確保更換`"sourceFile.xlsx"`與您實際的 Excel 檔案的名稱。
## 第 3 步：準備您的數位證書
要新增數位簽名，您需要載入 PFX 檔案並提供密碼。您可以按照以下方法執行此操作：
```csharp
string password = "pfxPassword"; //替換為您的 PFX 密碼
string pfx = "pfxFile"; // PFX 檔案的路徑
```
確保更換`"pfxPassword"`使用您的實際密碼和`"pfxFile"`以及 PFX 檔案的路徑。
## 第 4 步：建立數位簽名
現在是時候使用以下命令建立數位簽章了`DigitalSignature`班級。您需要將 PFX 檔案讀入位元組數組，然後建立簽名。
```csharp
DigitalSignature signature = new DigitalSignature(File.ReadAllBytes(pfx), password, "testXAdES", DateTime.Now);
signature.XAdESType = XAdESType.XAdES;
```
這裡，`"testXAdES"`是簽名的原因，並且`DateTime.Now`表示簽署時間。
## 步驟 5：將簽名新增至工作簿
要將簽名新增到您的工作簿中，您需要建立一個`DigitalSignatureCollection`並添加您的簽名。
```csharp
DigitalSignatureCollection dsCollection = new DigitalSignatureCollection();
dsCollection.Add(signature);
```
## 步驟 6：為工作簿設定數位簽名
現在您已準備好簽名集合，是時候將其設定到工作簿中了。
```csharp
workbook.SetDigitalSignature(dsCollection);
```
## 第 7 步：儲存工作簿
最後，保存應用了數位簽章的工作簿。
```csharp
workbook.Save(outputDir + "XAdESSignatureSupport_out.xlsx");
```
代替`"XAdESSignatureSupport_out.xlsx"`與您想要的輸出檔名。
## 第8步：確認成功
為了確保一切順利，您可以將成功訊息列印到控制台。
```csharp
Console.WriteLine("XAdESSignatureSupport executed successfully.");
```
## 結論
現在你就擁有了！您已使用 Aspose.Cells for .NET 成功將 XAdES 簽章支援新增至您的 Excel 工作簿。這項強大的功能不僅增強了文件的安全性，還有助於維護資料的完整性。如果您有任何疑問或遇到任何問題，請隨時查看[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/)或訪問[支援論壇](https://forum.aspose.com/c/cells/9)尋求幫助。
## 常見問題解答
### 什麼是 XAdES？
XAdES（XML進階電子簽名）是一種電子簽名標準，可確保電子文件的完整性和真實性。
### 我是否需要數位憑證才能使用 XAdES 簽署？
是的，您需要 PFX 格式的有效數位憑證才能建立 XAdES 簽章。
### 我可以將 Aspose.Cells 用於其他檔案格式嗎？
是的，Aspose.Cells 主要適用於 Excel 文件，但它也支援各種其他電子表格格式。
### Aspose.Cells 是否有免費試用版？
絕對地！您可以獲得免費試用[這裡](https://releases.aspose.com/).
### 在哪裡可以找到更多範例和教學？
您可以探索更多範例和詳細文檔[Aspose.Cells 網站](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
