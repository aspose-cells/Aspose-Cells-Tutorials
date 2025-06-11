---
"description": "在本逐步指南中了解如何使用 Aspose.Cells for .NET 為已簽署的 Excel 檔案新增數位簽章。保護您的文件。"
"linktitle": "為已簽署的 Excel 檔案新增數位簽名"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "為已簽署的 Excel 檔案新增數位簽名"
"url": "/zh-hant/net/workbook-operations/add-digital-signature-to-signed-file/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 為已簽署的 Excel 檔案新增數位簽名

## 介紹
在當今的數位世界中，確保文件的真實性和完整性至關重要。數位簽章是一種強而有力的手段，可以驗證文件未被更改且來自合法來源。如果您正在 .NET 中使用 Excel 文件，並且想要在已簽署的文件中新增數位簽名，那麼您來對地方了！在本指南中，我們將引導您完成使用 Aspose.Cells for .NET 為現有簽章 Excel 檔案新增數位簽章的流程。 
## 先決條件
在深入討論細節之前，讓我們先確保您已準備好開始所需的一切：
1. Aspose.Cells for .NET：首先，您需要在 .NET 環境中安裝 Aspose.Cells。您可以從 [發布頁面](https://releases。aspose.com/cells/net/).
2. .NET Framework：確保您的機器上已安裝 .NET Framework。本指南假設您熟悉基本的 .NET 程式設計概念。
3. 數位憑證：您需要有效的數位憑證（.pfx 格式）來建立數位簽章。如果您沒有，您可以建立自簽名憑證以用於測試目的。
4. 開發環境：像 Visual Studio 這樣的程式碼編輯器或 IDE，您可以在其中編寫和執行 C# 程式碼。
5. 範例 Excel 檔案：您應該有一個已經過數位簽署的現有 Excel 檔案。這將是我們添加另一個簽名的文件。
滿足了這些先決條件後，我們就可以開始寫程式了！
## 導入包
在開始編碼之前，請確保導入必要的命名空間。以下是您需要在 C# 檔案頂部包含的內容：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
這些命名空間將使您能夠存取操作 Excel 檔案和處理數位簽章所需的類別和方法。
現在，讓我們將這個過程分解為易於管理的步驟。我們將逐步介紹每個步驟，以確保您了解如何在已簽署的 Excel 檔案中新增數位簽章。
## 步驟 1：定義目錄
首先，您需要指定原始檔案的位置以及輸出檔案的儲存位置。這很簡單但至關重要：
```csharp
// 來源目錄
string sourceDir = "Your Document Directory"; // 替換為您的實際目錄
// 輸出目錄
string outputDir = "Your Document Directory"; // 替換為您的實際目錄
```
代替 `"Your Document Directory"` 使用儲存檔案的實際路徑。這為您的文件操作奠定了基礎。
## 步驟 2：載入現有的簽章工作簿
接下來，您將載入已經簽署的現有 Excel 工作簿。這就是魔法開始的地方：
```csharp
// 載入已經數位簽署的工作簿以新增新的數位簽名
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```
這行初始化一個新的 `Workbook` 具有指定文件的物件。確保檔案名稱與您現有的簽章 Excel 檔案相符。
## 步驟3：建立數位簽章集合
要管理您的數位簽名，您需要建立一個集合。如果需要，您可以持有多個簽名：
```csharp
// 建立數位簽章集合
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```
在將新的數位簽章套用到工作簿之前，您可以在此集合中新增它。
## 步驟 4：載入您的證書
現在，是時候加載您的數位憑證了。該證書將用於建立新的簽名：
```csharp
// 證書文件及其密碼
string certFileName = sourceDir + "AsposeDemo.pfx"; // 您的證書文件
string password = "aspose"; // 您的憑證密碼
// 建立新證書
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```
確保更換 `AsposeDemo.pfx` 使用您的憑證檔案的名稱並相應地更新密碼。這一步至關重要，因為如果沒有正確的證書，您將無法建立有效的簽名。
## 步驟5：建立新的數位簽名
加載證書後，您現在可以建立新的數位簽章。此簽名將被添加到您的收藏中：
```csharp
// 建立新的數位簽章並將其新增至數位簽章集合中
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
dsCollection.Add(signature);
```
在這裡，您提供一條描述簽名的訊息，這有助於記錄保存。時間戳確保簽名與正確的時間點相關聯。
## 步驟 6：將簽章集合新增至工作簿
建立簽名後，就可以將整個集合新增到工作簿了：
```csharp
// 在工作簿中新增數位簽章集合
workbook.AddDigitalSignature(dsCollection);
```
此步驟可有效地將您的新數位簽章套用至工作簿，並為其新增真實性標記。
## 步驟 7：儲存工作簿
最後，儲存包含新數位簽章的工作簿。這是你所有努力得到回報的時刻：
```csharp
// 儲存工作簿並處理它。
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```
確保為輸出檔案指定一個名稱。這將是您的 Excel 文件的新版本，並帶有附加的數位簽章。
## 步驟8：確認成功
總而言之，操作成功完成後提供回饋是個好主意：
```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```
此行將向控制台列印確認訊息，讓您知道一切順利。
## 結論
就是這樣！您已成功使用 Aspose.Cells for .NET 將新的數位簽章新增至已簽署的 Excel 檔案。此過程不僅增強了文件的安全性，而且還確保了它們的可信度和可驗證性。 
在當今的數位環境中，數位簽章至關重要，特別是對於需要維護文件完整性的企業和專業人士而言。按照本指南，您可以輕鬆管理 Excel 文件中的數位簽名，確保資料的安全和真實。
## 常見問題解答
### 什麼是數位簽章？
數位簽章是一種用於驗證數位訊息或文件的真實性和完整性的數學方案。它確保文件未被更改並確認簽署者的身分。
### 我是否需要特殊憑證來建立數位簽章？
是的，您需要由受信任的憑證授權單位 (CA) 頒發的數位憑證來建立有效的數位簽章。
### 我可以使用自簽名憑證進行測試嗎？
絕對地！您可以建立自簽名憑證以用於開發和測試目的，但對於生產，最好使用來自受信任 CA 的憑證。
### 如果我嘗試在未簽名的文檔中添加簽名會發生什麼？
如果您嘗試將數位簽章新增至尚未簽署的文件中，它將正常運作，但原始簽名將不存在。
### 在哪裡可以找到有關 Aspose.Cells 的更多資訊？
您可以檢查 [Aspose.Cells 文檔](https://reference.aspose.com/cells/net/) 以取得詳細指南和 API 參考。


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}