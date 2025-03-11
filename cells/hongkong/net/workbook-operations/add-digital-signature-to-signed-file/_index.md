---
title: 將數位簽章新增至已簽署的 Excel 文件
linktitle: 將數位簽章新增至已簽署的 Excel 文件
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此逐步指南中了解如何使用 Aspose.Cells for .NET 將數位簽章新增至已簽署的 Excel 檔案。保護您的文件。
weight: 12
url: /zh-hant/net/workbook-operations/add-digital-signature-to-signed-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將數位簽章新增至已簽署的 Excel 文件

## 介紹
在當今的數位世界中，確保文件的真實性和完整性至關重要。數位簽章是驗證文件未被更改且來自合法來源的可靠方法。如果您正在 .NET 中處理 Excel 檔案並想要為已簽署的檔案新增數位簽名，那麼您來對地方了！在本指南中，我們將引導您完成使用 Aspose.Cells for .NET 將新數位簽章新增至現有簽章 Excel 檔案的過程。 
## 先決條件
在我們深入討論細節之前，讓我們確保您已具備開始使用所需的一切：
1.  Aspose.Cells for .NET：首先，您需要在 .NET 環境中安裝 Aspose.Cells。您可以從[發布頁面](https://releases.aspose.com/cells/net/).
2. .NET Framework：請確定您的電腦上安裝了 .NET Framework。本指南假設您熟悉基本的 .NET 程式設計概念。
3. 數位憑證：您需要有效的數位憑證（.pfx 格式）來建立數位簽章。如果您沒有，您可以建立自簽名憑證用於測試目的。
4. 開發環境：程式碼編輯器或 IDE（例如 Visual Studio），您可以在其中編寫和執行 C# 程式碼。
5. 範例 Excel 檔案：您應該有一個已進行數位簽章的現有 Excel 檔案。這將是我們添加另一個簽名的文件。
滿足了這些先決條件後，讓我們開始寫程式碼吧！
## 導入包
在開始編碼之前，請確保導入必要的命名空間。以下是您需要在 C# 檔案頂部包含的內容：
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
這些命名空間將使您能夠存取操作 Excel 檔案和處理數位簽章所需的類別和方法。
現在，讓我們將該流程分解為可管理的步驟。我們將完成每個步驟，以確保您了解如何在已簽署的 Excel 檔案中新增數位簽章。
## 第 1 步：定義您的目錄
首先，您需要指定原始檔案所在的位置以及輸出檔案的儲存位置。這很簡單但至關重要：
```csharp
//原始碼目錄
string sourceDir = "Your Document Directory"; //替換為你的實際目錄
//輸出目錄
string outputDir = "Your Document Directory"; //替換為你的實際目錄
```
代替`"Your Document Directory"`與儲存檔案的實際路徑。這為您的文件操作奠定了基礎。
## 第 2 步：載入現有的簽名工作簿
接下來，您將載入已簽署的現有 Excel 工作簿。這就是魔法開始的地方：
```csharp
//載入已經數位簽署的工作簿以新增新的數位簽名
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```
該行初始化一個新的`Workbook`具有指定文件的物件。確保檔案名稱與您現有的簽章 Excel 檔案相符。
## 第 3 步：建立數位簽章集合
要管理您的數位簽名，您需要建立一個集合。這允許您在需要時持有多個簽名：
```csharp
//建立數位簽章集合
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```
您可以在該集合中新增的數位簽名，然後再將其套用到工作簿。
## 第 4 步：載入您的證書
現在，是時候加載您的數位憑證了。該證書將用於建立新簽章：
```csharp
//證書文件及其密碼
string certFileName = sourceDir + "AsposeDemo.pfx"; //您的證書文件
string password = "aspose"; //您的憑證密碼
//建立新證書
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```
確保更換`AsposeDemo.pfx`與您的憑證檔案的名稱並相應地更新密碼。此步驟至關重要，因為如果沒有正確的證書，您將無法建立有效的簽名。
## 第 5 步：建立新的數位簽名
加載證書後，您現在可以建立新的數位簽章。此簽名將添加到您的收藏中：
```csharp
//建立新的數位簽章並將其新增至數位簽章集合中
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
dsCollection.Add(signature);
```
在這裡，您提供一條描述簽名的訊息，這對於保存記錄很有幫助。時間戳確保簽名與正確的時間點相關聯。
## 步驟 6：將簽章集合新增至工作簿中
建立簽名後，需要將整個集合新增至工作簿：
```csharp
//在工作簿中新增數位簽章集合
workbook.AddDigitalSignature(dsCollection);
```
此步驟有效地將您的新數位簽章套用到工作簿，並為其添加了附加的真實性標記。
## 第 7 步：儲存工作簿
最後，儲存包含新數位簽章的工作簿。這是你所有的努力得到回報的時刻：
```csharp
//保存工作簿並將其丟棄。
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```
確保指定輸出檔案的名稱。這將是您的 Excel 文件的新版本，並帶有附加的數位簽章。
## 第8步：確認成功
總而言之，一旦操作成功完成，最好提供回饋：
```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```
此行將向控制台列印確認訊息，讓您知道一切順利。
## 結論
現在你就擁有了！您已使用 Aspose.Cells for .NET 成功將新的數位簽章新增至已簽署的 Excel 檔案。此過程不僅增強了文件的安全性，而且還確保它們是值得信賴和可驗證的。 
數位簽章在當今的數位環境中至關重要，特別是對於需要維護文件完整性的企業和專業人士而言。透過遵循本指南，您可以輕鬆管理 Excel 文件中的數位簽名，確保您的資料保持安全和真實。
## 常見問題解答
### 什麼是數位簽章？
數位簽章是一種用於驗證數位訊息或文件的真實性和完整性的數學方案。它確保文件未被更改並確認簽署者的身分。
### 我需要特殊憑證來建立數位簽章嗎？
是的，您需要由受信任的憑證授權單位 (CA) 頒發的數位憑證來建立有效的數位簽章。
### 我可以使用自簽名憑證進行測試嗎？
絕對地！您可以建立自簽名憑證用於開發和測試目的，但對於生產，最好使用來自受信任 CA 的憑證。
### 如果我嘗試在未簽名的文件中添加簽名，會發生什麼情況？
如果您嘗試將數位簽章新增至尚未簽署的文件中，它將正常運作，但不會出現原始簽章。
### 在哪裡可以找到有關 Aspose.Cells 的更多資訊？
您可以檢查[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/)取得詳細指南和 API 參考。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
