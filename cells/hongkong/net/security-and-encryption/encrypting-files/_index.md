---
"description": "使用 Aspose.Cells for .NET 透過密碼保護來保護您的 Excel 檔案。本指南將引導您逐步完成加密。"
"linktitle": "在 .NET 中加密文件"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "在 .NET 中加密文件"
"url": "/zh-hant/net/security-and-encryption/encrypting-files/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 在 .NET 中加密文件

## 介紹
在當今的數位世界中，資料安全是重中之重。無論您是企業主、會計師還是資料分析師，保護 Excel 文件中的敏感資訊都至關重要。您肯定不希望他人未經授權存取您的寶貴數據，對吧？幸運的是，如果您使用 .NET，Aspose.Cells 提供了出色的工具來輕鬆加密您的 Excel 電子表格。在本教學中，我們將逐步介紹加密 Excel 檔案的過程。從先決條件到實際程式碼，我擁有保護文件所需的一切！
## 先決條件
在深入研究程式碼之前，讓我們確保您擁有開始所需的一切。以下是一份清單：
1. .NET Framework：請確保您安裝了相容版本的 .NET Framework。 Aspose.Cells 與 .NET 版本配合得很好，所以請選擇適合您專案的版本。
2. Aspose.Cells 庫：從 [下載頁面](https://releases.aspose.com/cells/net/)。這個強大的程式庫將允許您毫不費力地操作和加密 Excel 文件。
3. Visual Studio：一個好的 IDE 會讓事情變得更容易，所以請確保您已經為您的開發工作設定了 Visual Studio（或任何與 .NET 相容的 IDE）。
4. 對 C# 的基本了解：如果您知道如何測量配料，那麼烘烤蛋糕就更容易了，對嗎？同樣，一點 C# 知識將幫助您了解如何有效地編寫此任務的程式碼。
一旦您勾選了這些項目，您就可以繼續前進了！
## 導入包
我們編碼之旅的第一步是將必要的 Aspose.Cells 套件匯入到您的專案中。您可以按照以下步驟操作：
### 建立新專案
開啟 Visual Studio 並建立一個新的 C# 專案。為了簡單起見，選擇一個控制台應用程式。
### 新增 Aspose.Cells 引用
1. 在解決方案資源管理器中以滑鼠右鍵按一下您的專案。
2. 選擇“管理 NuGet 套件”。
3. 搜尋“Aspose.Cells”並安裝它。
該軟體包將允許您存取加密 Excel 文件所需的所有方法。
### 使用命名空間
在主程式檔案的頂部，新增以下行以包含 Aspose.Cells 命名空間：
```csharp
using System.IO;
using Aspose.Cells;
```
這一步就像拿到工具箱的鑰匙；它將解鎖您將使用的所有功能。

現在，讓我們進入任務的核心：加密 Excel 檔案。請依照這些詳細步驟建立加密的 Excel 檔案。
## 步驟 1：定義文件目錄
首先，讓我們為您的 Excel 文件準備一個路徑。這是您儲存輸入和輸出檔案的地方。
```csharp
string dataDir = "Your Document Directory";
```
在這裡，替換 `"Your Document Directory"` 使用您的 Excel 檔案所在的實際路徑以及您想要儲存加密檔案的位置。
## 步驟 2：實例化工作簿對象
現在，讓我們建立一個 Workbook 物件來處理您的 Excel 檔案。
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
這行程式碼開啟指定的 Excel 檔案（`Book1.xls`)，這樣您就可以開始進行更改。想像一下打開一本您想要編輯的書。
## 步驟 3：指定加密選項
接下來，是時候設定加密選項了。您可以按照以下步驟操作：

當談到 Aspose.Cells 中的加密時，您可以選擇。對於此範例，您將設定 XOR 和強加密提供者加密。 
```csharp
// 指定 XOR 加密類型。
workbook.SetEncryptionOptions(EncryptionType.XOR, 40);
// 指定強加密類型（RC4、Microsoft 強加密提供者）。
workbook.SetEncryptionOptions(EncryptionType.StrongCryptographicProvider, 128);
```
將這些選項想像成您可能使用的鎖 - 有些更短且更容易撬開（XOR），而其他一些則更具挑戰性（強加密提供者）。
## 步驟4：密碼保護文件
現在，讓我們為您的文件添加密碼。這是鎖門的秘密鑰匙：
```csharp
workbook.Settings.Password = "1234";
```
隨意改變 `"1234"` 任何你喜歡的密碼。請記住，密碼越強，保護效果越好！
## 步驟5：儲存加密的Excel文件
最後，讓我們保存更改以建立加密檔案。
```csharp
workbook.Save(dataDir + "encryptedBook1.out.xls");
```
這行程式碼將工作簿儲存為 `encryptedBook1.out.xls` 在您指定的目錄中。這就像把書放回書架上，安全地鎖起來！
## 結論
就這樣！您剛剛學習如何使用 .NET 中的 Aspose.Cells 加密 Excel 檔案。透過遵循這些步驟，您可以確保您的敏感資料得到良好的保護。請記住 - 保護從您開始，因此請始終採取必要措施來保護您的資訊。 
## 常見問題解答
### 什麼是 Aspose.Cells？
Aspose.Cells 是一個功能強大的.NET 函式庫，用於管理和處理 Excel 檔案。
### 我可以使用不同強度的密碼加密 Excel 檔案嗎？
是的，您可以在使用 Aspose.Cells 時指定不同的加密類型和強度。
### Aspose.Cells 有免費試用版嗎？
是的，你可以從他們的網站下載免費試用版 [網站](https://releases。aspose.com/).
### 在哪裡可以找到對 Aspose.Cells 的支援？
您可以透過 Aspose 論壇取得支持 [Aspose 支援](https://forum。aspose.com/c/cells/9).
### 如何購買 Aspose.Cells？
您可以從 [購買頁面](https://purchase。aspose.com/buy).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}