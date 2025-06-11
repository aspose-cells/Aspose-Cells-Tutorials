---
"description": "透過本逐步指南了解如何使用 Aspose.Cells for .NET 將 Xades 簽章新增至 Excel 檔案。保護您的文件。"
"linktitle": "Xades 簽名支持"
"second_title": "Aspose.Cells for .NET API參考"
"title": "Xades 簽名支持"
"url": "/zh-hant/net/excel-workbook/xades-signature-support/"
"weight": 190
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Xades 簽名支持

## 介紹

在當今的數位世界中，保護文件安全比以往任何時候都更加重要。無論您處理的是敏感的商業資訊還是個人數據，確保文件的完整性和真實性至關重要。實現此目的的一種方法是透過數位簽名，特別是 Xades 簽名。如果您是 .NET 開發人員，並希望在您的應用程式中實現 Xades 簽名支持，那麼您來對地方了！在本指南中，我們將引導您完成使用 Aspose.Cells for .NET 將 Xades 簽章新增至 Excel 檔案的過程。那麼，就讓我們開始吧！

## 先決條件

在我們開始之前，您需要做好以下幾點：

1. Aspose.Cells for .NET：請確保您已安裝 Aspose.Cells 函式庫。您可以輕鬆地從 [Aspose 網站](https://releases。aspose.com/cells/net/).
2. 開發環境：一個可用的 .NET 開發環境（如 Visual Studio），您可以在其中編寫和執行程式碼。
3. 數位憑證：您需要一個有效的數位憑證（PFX 檔案）及其密碼。此憑證對於建立數位簽章至關重要。
4. C# 基礎知識：熟悉 C# 程式設計將幫助您更好地理解範例。

一旦滿足了這些先決條件，您就可以開始在 Excel 檔案中實作 Xades 簽名了！

## 導入包

若要使用 Aspose.Cells for .NET，您需要匯入必要的命名空間。您可以按照以下步驟操作：

```csharp
using Aspose.Cells.DigitalSignatures;
using System;
using System.IO;
```

這些命名空間提供處理 Excel 檔案和管理數位簽章所需的類別和方法的存取。

現在我們已經完成所有設置，讓我們將向 Excel 文件添加 Xades 簽名的過程分解為清晰、易於管理的步驟。

## 步驟 1：設定來源目錄和輸出目錄

首先，我們需要定義來源 Excel 檔案的位置以及我們想要儲存簽章輸出檔案的位置。這是一個至關重要的一步，因為它有助於有效地組織您的文件。

```csharp
// 來源目錄
string sourceDir = "Your Document Directory";
// 輸出目錄
string outputDir = "Your Output Directory";
```

## 第 2 步：載入工作簿

接下來，讓我們載入要簽署的 Excel 工作簿。您將在此處載入現有的 Excel 檔案。

```csharp
Workbook workbook = new Workbook(sourceDir + "sourceFile.xlsx");
```

在這裡，我們建立一個新的實例 `Workbook` 類，傳遞來源 Excel 檔案的路徑。確保檔案名稱與來源目錄中的檔案名稱相符。

## 步驟3：準備您的數位證書

要建立數位簽名，您需要加載您的數位憑證。這涉及讀取 PFX 檔案並提供其密碼。

```csharp
string password = "pfxPassword"; // 替換為您的 PFX 密碼
string pfx = "pfxFile"; // 替換為 PFX 檔案的路徑
```

在此步驟中，替換 `pfxPassword` 使用您的實際密碼 `pfxFile` 以及您的 PFX 檔案的路徑。這是簽署文件的關鍵！

## 步驟4：建立數位簽名

現在，讓我們使用 `DigitalSignature` 班級。這就是奇蹟發生的地方！

```csharp
DigitalSignature signature = new DigitalSignature(File.ReadAllBytes(pfx), password, "testXAdES", DateTime.Now);
signature.XAdESType = XAdESType.XAdES;
```

在此程式碼片段中，我們將 PFX 檔案讀入位元組數組並建立一個新的 `DigitalSignature` 目的。我們還設定了 `XAdESType` 到 `XAdES`，這對於我們的簽名至關重要。

## 步驟 5：將簽名新增至工作簿

建立數位簽章後，下一步是將其新增至工作簿。

```csharp
DigitalSignatureCollection dsCollection = new DigitalSignatureCollection();
dsCollection.Add(signature);
workbook.SetDigitalSignature(dsCollection);
```

在這裡，我們創建一個 `DigitalSignatureCollection`，在其中新增我們的簽名，然後將此集合設定到工作簿中。這就是我們將簽名附加到 Excel 檔案的方式。

## 步驟 6：儲存已簽署的工作簿

最後，是時候將簽署的工作簿儲存到輸出目錄了。此步驟完成整個過程。

```csharp
workbook.Save(outputDir + "XAdESSignatureSupport_out.xlsx");
Console.WriteLine("XAdESSignatureSupport executed successfully.");
```

在這段程式碼中，我們用新名稱儲存工作簿， `XAdESSignatureSupport_out.xlsx`，在輸出目錄中。此步驟完成後，您將在控制台中看到一條成功訊息。

## 結論

就是這樣！您已成功使用 Aspose.Cells for .NET 將 Xades 簽章新增至您的 Excel 檔案。此過程不僅增強了文件的安全性，而且還透過確保文件的真實性與使用者建立了信任。 
數位簽章是現代文件管理的重要組成部分，借助 Aspose.Cells 的強大功能，您可以輕鬆地在應用程式中實現它們。

## 常見問題解答

### Xades 簽名是什麼？
Xades（XML 高級電子簽名）是一種數位簽名標準，它提供了用於確保電子文件的完整性和真實性的附加功能。

### 我需要數位憑證來建立 Xades 簽名嗎？
是的，您需要一個有效的數位憑證（PFX 檔案）來建立 Xades 簽章。

### 我可以在購買之前測試 Aspose.Cells for .NET 嗎？
絕對地！您可以從 [Aspose 網站](https://releases。aspose.com/).

### Aspose.Cells 是否與所有版本的 .NET 相容？
Aspose.Cells 支援各種版本的 .NET 框架。檢查 [文件](https://reference.aspose.com/cells/net/) 了解相容性詳細資訊。

### 如果遇到問題，我可以在哪裡獲得支援？
您可以訪問 [Aspose 論壇](https://forum.aspose.com/c/cells/9) 尋求社區支持和援助。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}