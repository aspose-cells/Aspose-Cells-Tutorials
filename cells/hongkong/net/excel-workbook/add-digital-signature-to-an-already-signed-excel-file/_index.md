---
"description": "透過本詳細的逐步指南了解如何使用 Aspose.Cells for .NET 將數位簽章新增至已簽署的 Excel 檔案。"
"linktitle": "為已簽署的 Excel 檔案新增數位簽名"
"second_title": "Aspose.Cells for .NET API參考"
"title": "為已簽署的 Excel 檔案新增數位簽名"
"url": "/zh-hant/net/excel-workbook/add-digital-signature-to-an-already-signed-excel-file/"
"weight": 30
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 為已簽署的 Excel 檔案新增數位簽名

## 介紹

在當今的數位世界中，保護文件安全比以往任何時候都更加重要。數位簽章提供了一種確保文件真實性和完整性的方法，尤其是在處理敏感資訊時。如果您正在使用 Excel 檔案並想要在已經簽名的工作簿中新增新的數位簽名，那麼您來對地方了！在本指南中，我們將引導您完成使用 Aspose.Cells for .NET 為已簽署的 Excel 檔案新增數位簽章的流程。那麼，就讓我們開始吧！

## 先決條件

在我們深入討論編碼細節之前，您需要先做好以下幾點：

1. Aspose.Cells for .NET：請確保您的 .NET 專案中安裝了 Aspose.Cells 函式庫。您可以從 [地點](https://releases。aspose.com/cells/net/).
2. 證書文件：您需要一個有效的證書文件（通常是 `.pfx` 該文件包含您的數位憑證。確保您知道該文件的密碼。
3. 開發環境：使用 Visual Studio 或任何其他支援 .NET 的 IDE 設定您的開發環境。
4. C# 基礎知識：熟悉 C# 程式設計將幫助您順利完成。
5. 範例文件：有一個已經過數位簽章的範例 Excel 檔案。這將是您要新增簽署的檔案。

現在我們已經準備好一切，讓我們開始編碼吧！

## 導入包

首先，您需要在 C# 檔案中匯入必要的套件。以下是操作方法：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

這些命名空間將允許您處理 Excel 檔案並無縫處理數位簽章。

## 步驟 1：設定來源目錄和輸出目錄

在操作 Excel 檔案之前，您需要定義來源檔案的位置以及要儲存輸出檔案的位置。具體操作如下：

```csharp
// 來源目錄
string sourceDir = "Your Document Directory";
// 輸出目錄
string outputDir = "Your Document Directory";
```

在此步驟中，我們使用一種方法來取得來源目錄和輸出目錄的路徑。確保這些目錄存在並包含所需的檔案。

## 步驟 2：載入已簽署的工作簿

接下來，您需要載入要修改的 Excel 工作簿。這是透過創建 `Workbook` 類別並傳遞簽名檔案的路徑。

```csharp
// 載入已經過數位簽章的工作簿
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```

這裡，我們正在加載名為 `sampleDigitallySignedByCells.xlsx`。確保此文件已簽署。

## 步驟3：建立數位簽章集合

現在，讓我們建立一個數位簽章集合。此集合將保存您想要新增至工作簿的所有數位簽章。

```csharp
// 建立數位簽章集合
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```

此步驟至關重要，因為它允許您在需要時管理多個簽名。

## 步驟 4：建立新證書

您需要載入您的憑證檔案來建立新的數位簽章。這是您指定路徑的地方 `.pfx` 文件及其密碼。

```csharp
// 證書文件及其密碼
string certFileName = sourceDir + "AsposeDemo.pfx";
string password = "aspose";

// 建立新證書
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```

確保更換 `AsposeDemo.pfx` 並將密碼替換為您的實際憑證檔案名稱和密碼。

## 步驟5：建立數位簽名

有了證書，您現在就可以建立數位簽章。您還需要提供簽名的原因以及目前的日期和時間。

```csharp
// 建立新的數位簽章並將其新增至數位簽章集合中
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
```

此步驟將新簽名新增至您的收藏中，稍後您可以將其套用到工作簿。

## 步驟 6：將數位簽章集合新增至工作簿

現在是時候將數位簽章集合新增至工作簿了。這就是奇蹟發生的地方！

```csharp
// 在工作簿中新增數位簽章集合
workbook.AddDigitalSignature(dsCollection);
```

透過執行此行，您可以有效地將新的數位簽章附加到已簽署的工作簿。

## 步驟 7：儲存並處理工作簿

最後，您需要將修改後的工作簿儲存到輸出目錄並釋放正在使用的任何資源。

```csharp
// 儲存工作簿並處理它。
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```

此步驟可確保您的變更已儲存，並且工作簿已正確處理以釋放資源。

## 步驟8：確認執行

總而言之，最好確認您的程式碼已成功執行。您可以透過簡單的控制台訊息來完成此操作。

```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```

這提供了操作成功的回饋，這總是令人高興的！

## 結論

就是這樣！您已成功使用 Aspose.Cells for .NET 將新的數位簽章新增至已簽署的 Excel 檔案。數位簽章是確保文件真實性的有效方法，現在您知道如何以程式設計方式管理它們。無論您處理的是財務文件、合約或任何敏感訊息，實施數位簽章都可以增強安全性和信任。

## 常見問題解答

### 什麼是數位簽章？
數位簽章是一種用於驗證訊息或文件的真實性和完整性的加密方法。

### 我可以為同一個 Excel 檔案新增多個數位簽章嗎？
是的，您可以建立一個數位簽章集合並將多個簽章新增至同一個工作簿。

### Aspose.Cells 支援哪些格式的數位簽章？
Aspose.Cells 支援多種格式，包括 `.pfx` 用於證書。

### 我是否需要特定版本的 .NET 才能使用 Aspose.Cells？
檢查 [Aspose.Cells 文檔](https://reference.aspose.com/cells/net/) 與您的 .NET 版本相容。

### 如何取得 Aspose.Cells 的臨時授權？
您可以從 [Aspose的購買頁面](https://purchase。aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}