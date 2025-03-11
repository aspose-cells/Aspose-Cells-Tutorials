---
title: 將數位簽章新增至已簽署的 Excel 文件
linktitle: 將數位簽章新增至已簽署的 Excel 文件
second_title: Aspose.Cells for .NET API 參考
description: 透過這份詳細的逐步指南，了解如何使用 Aspose.Cells for .NET 將數位簽章新增至已簽署的 Excel 檔案。
weight: 30
url: /zh-hant/net/excel-workbook/add-digital-signature-to-an-already-signed-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 將數位簽章新增至已簽署的 Excel 文件

## 介紹

在當今的數位世界中，保護文件比以往任何時候都更加重要。數位簽章提供了一種確保文件真實性和完整性的方法，特別是在處理敏感資訊時。如果您正在使用 Excel 文件並希望為已簽名的工作簿添加新的數位簽名，那麼您來對地方了！在本指南中，我們將引導您完成使用 Aspose.Cells for .NET 將數位簽章新增至已簽署的 Excel 檔案的過程。那麼，讓我們深入了解一下吧！

## 先決條件

在我們深入了解編碼的本質之前，您需要先做好以下幾件事：

1.  Aspose.Cells for .NET：請確定您的.NET專案中安裝了Aspose.Cells程式庫。您可以從[地點](https://releases.aspose.com/cells/net/).
2. 證書文件：您需要一個有效的證書文件（通常是`.pfx`文件）包含您的數位憑證。確保您知道該文件的密碼。
3. 開發環境：使用 Visual Studio 或任何其他支援 .NET 的 IDE 設定開發環境。
4. C# 基礎：熟悉 C# 程式設計將有助於您順利掌握。
5. 範例文件：擁有已進行數位簽章的範例 Excel 檔案。這將是您要新增簽署的檔案。

現在一切準備就緒，讓我們開始編碼吧！

## 導入包

首先，您需要在 C# 檔案中匯入必要的套件。操作方法如下：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

這些命名空間將允許您無縫地處理 Excel 檔案並處理數位簽章。

## 第 1 步：設定來源目錄和輸出目錄

在操作 Excel 檔案之前，您需要定義來源檔案所在位置以及輸出檔案的儲存位置。操作方法如下：

```csharp
//原始碼目錄
string sourceDir = "Your Document Directory";
//輸出目錄
string outputDir = "Your Document Directory";
```

在此步驟中，我們使用一種方法來取得來源目錄和輸出目錄的路徑。確保這些目錄存在並包含所需的檔案。

## 第 2 步：載入已簽署的工作簿

接下來，您需要載入要修改的 Excel 工作簿。這是透過建立一個實例來完成的`Workbook`類別並傳遞簽名檔案的路徑。

```csharp
//載入已經數位簽署的工作簿
Aspose.Cells.Workbook workbook = new Aspose.Cells.Workbook(sourceDir + "sampleDigitallySignedByCells.xlsx");
```

在這裡，我們正在載入名為的工作簿`sampleDigitallySignedByCells.xlsx`。確保該文件已簽署。

## 第 3 步：建立數位簽章集合

現在，讓我們建立一個數位簽章集合。此集合將保存您要新增至工作簿中的所有數位簽章。

```csharp
//建立數位簽章集合
Aspose.Cells.DigitalSignatures.DigitalSignatureCollection dsCollection = new Aspose.Cells.DigitalSignatures.DigitalSignatureCollection();
```

此步驟至關重要，因為它允許您在需要時管理多個簽名。

## 第 4 步：建立新證書

您需要載入憑證檔案來建立新的數位簽章。您可以在此處指定您的路徑`.pfx`文件及其密碼。

```csharp
//證書文件及其密碼
string certFileName = sourceDir + "AsposeDemo.pfx";
string password = "aspose";

//建立新證書
System.Security.Cryptography.X509Certificates.X509Certificate2 certificate = new System.Security.Cryptography.X509Certificates.X509Certificate2(certFileName, password);
```

確保更換`AsposeDemo.pfx`密碼為您的實際憑證檔案名稱和密碼。

## 第 5 步：建立數位簽名

有了證書，您現在就可以建立數位簽章了。您還需要提供簽名的原因以及當前日期和時間。

```csharp
//建立新的數位簽章並將其新增至數位簽章集合中
Aspose.Cells.DigitalSignatures.DigitalSignature signature = new Aspose.Cells.DigitalSignatures.DigitalSignature(certificate, "Aspose.Cells added new digital signature in existing digitally signed workbook.", DateTime.Now);
```

此步驟將新簽名新增至您的集合中，稍後您將其套用到工作簿。

## 步驟 6：將數位簽章集合新增至工作簿中

現在是時候將數位簽章集合新增至工作簿了。這就是魔法發生的地方！

```csharp
//在工作簿中新增數位簽章集合
workbook.AddDigitalSignature(dsCollection);
```

透過執行此行，您可以有效地將新的數位簽章附加到已簽署的工作簿中。

## 第 7 步：儲存並處置工作簿

最後，您需要將修改後的工作簿儲存到輸出目錄並釋放正在使用的所有資源。

```csharp
//保存工作簿並將其丟棄。
workbook.Save(outputDir + "outputDigitallySignedByCells.xlsx");
workbook.Dispose();
```

此步驟可確保儲存您的更改，並正確處理工作簿以釋放資源。

## 第8步：確認執行

總而言之，最好確認您的程式碼是否成功執行。您可以使用簡單的控制台訊息來完成此操作。

```csharp
Console.WriteLine("AddDigitalSignatureToAnAlreadySignedExcelFile executed successfully.\r\n");
```

這會提供您的操作成功的回饋，這總是令人高興的！

## 結論

現在你就擁有了！您已使用 Aspose.Cells for .NET 成功將新的數位簽章新增至已簽署的 Excel 檔案。數位簽章是確保文件真實性的強大方法，現在您知道如何以程式設計方式管理它們。無論您處理的是財務文件、合約或任何敏感訊息，實施數位簽章都可以增強安全性和信任。

## 常見問題解答

### 什麼是數位簽章？
數位簽章是一種用於驗證訊息或文件的真實性和完整性的加密方法。

### 我可以為同一個 Excel 檔案新增多個數位簽章嗎？
是的，您可以建立數位簽章集合並將多個簽章新增至相同工作簿。

### Aspose.Cells 支援哪些格式的數位簽章？
 Aspose.Cells 支援多種格式，包括`.pfx`用於證書。

### 我需要特定版本的 .NET 才能使用 Aspose.Cells 嗎？
檢查[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/)為了與您的 .NET 版本相容。

### 我如何獲得 Aspose.Cells 的臨時許可證？
您可以向以下機構申請臨時許可證[Aspose的購買頁面](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
