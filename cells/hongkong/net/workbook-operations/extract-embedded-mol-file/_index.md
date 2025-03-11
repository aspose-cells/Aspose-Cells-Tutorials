---
title: 從工作簿中提取嵌入的 Mol 文件
linktitle: 從工作簿中提取嵌入的 Mol 文件
second_title: Aspose.Cells .NET Excel 處理 API
description: 在此詳細的逐步教學中，了解如何使用 Aspose.Cells for .NET 從 Excel 工作簿中提取嵌入的 MOL 檔案。
weight: 18
url: /zh-hant/net/workbook-operations/extract-embedded-mol-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 從工作簿中提取嵌入的 Mol 文件

## 介紹
在管理 Excel 工作簿中的資料時，有時您會遇到各種非標準格式的嵌入物件。其中一種格式是 MOL（分子結構檔），它通常在化學中用於表示分子資訊。如果您希望使用 Aspose.Cells for .NET 從 Excel 工作簿中提取這些 MOL 文件，那麼您已經找到了正確的指南。在本文中，我們將逐步引導您完成整個過程，並揭開每個部分的神秘面紗。
## 先決條件
在深入研究程式碼之前，必須確保您擁有必要的技能和工具。這是您需要的：
1. 對 .NET 程式設計的基本了解：您應該熟悉 C# 和 .NET 框架。
2.  Aspose.Cells for .NET：請確保您擁有 Aspose.Cells 函式庫。你可以[在這裡下載](https://releases.aspose.com/cells/net/).
3. IDE：您可以使用 Visual Studio 或任何其他 .NET 相容 IDE。
4. 具有嵌入式 MOL 檔案的 Excel 工作簿：對於本教學課程，您需要一個包含 MOL 物件的 Excel 檔案。您可以建立自己的文件或使用任何範例文件。
## 導入包
首先，您需要在專案中匯入必要的命名空間。這對於存取 Aspose.Cells 功能至關重要。您可以這樣做：

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

這些命名空間將允許您操作工作簿、存取工作表以及處理一般文件。
現在我們已經解決了先決條件，讓我們深入研究程式碼並了解從 Excel 工作簿提取嵌入的 MOL 檔案所涉及的每個步驟。 
## 第 1 步：設定您的目錄
第一步是定義來源文件所在的位置以及要儲存提取的 MOL 檔案的位置。讓我們設定這些目錄。
```csharp
string SourceDir = "Your Document Directory"; //替換為您的目錄路徑
string outputDir = "Your Document Directory"; //替換為你的輸出路徑
```
在這裡，你替換`"Your Document Directory"`與您的實際目錄的路徑。來源目錄和輸出目錄都可供您的應用程式存取，這一點很重要。
## 第 2 步：載入工作簿
設定好目錄後，下一個任務是載入 Excel 工作簿。我們現在就這樣做吧。

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

我們正在建立一個實例`Workbook`類別並傳入名為的 Excel 檔案的路徑`EmbeddedMolSample.xlsx`。此步驟將初始化工作簿，以便您存取其內容。
## 第 3 步：迭代工作表
現在您的工作簿已加載，您需要循環訪問工作簿中的每個工作表。這使您可以檢查每個工作表中是否有嵌入的物件。

```csharp
var index = 1; //用於命名提取的 MOL 文件
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    //進一步的提取邏輯在這裡
}
```

在這裡，您使用的是`foreach`循環瀏覽工作表。對於每個工作表，您可以訪問`OleObjects`集合，其中包含所有嵌入物件。
## 步驟 4：提取 MOL 文件
現在到了關鍵部分——從 OLE 物件中提取 MOL 檔案。這需要工作表循環內的另一個循環。

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

對於您找到的每個 OLE 對象，您將在輸出目錄中建立一個新檔案。這`ObjectData`的財產`OleObject`儲存嵌入物件的數據，您可以使用以下命令將其寫入新建立的文件`FileStream`。該文件按順序命名（`OleObject1.mol`, `OleObject2.mol`等）基於`index`多變的。
## 第 5 步：確認流程完成
最後，一旦提取了所有 MOL 文件，最好通知用戶該過程已成功完成。

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

此行只是將一條訊息列印到控制台，讓您知道提取已成功。對於用戶回饋來說這是一個很好的接觸。
## 結論
現在你就擁有了！您已使用 Aspose.Cells for .NET 成功從 Excel 工作簿中提取嵌入的 MOL 檔案。該流程整合了一些核心步驟，確保採用結構化方法來處理嵌入式物件。無論您是從事科學研究、化學分析，還是只是處理複雜的資料集，能夠提取和操作這些文件類型都可以對您管理資訊的方式產生重大影響。 
## 常見問題解答
### 我可以從 Excel 中提取 MOL 以外的其他文件類型嗎？
是的，您可以使用類似的技術來提取各種其他嵌入文件類型。
### Aspose.Cells 可以免費使用嗎？
 Aspose.Cells 是一個商業庫，但您可以[限時免費試用](https://releases.aspose.com/).
### 此方法適用於所有 Excel 版本嗎？
是的，只要 Aspose.Cells 支援該檔案格式即可。
### 我可以自動化這個提取流程嗎？
絕對地！您可以將程式碼放入排程任務或腳本中來自動化此過程。
### 在哪裡可以找到有關 Aspose.Cells 的更多文件？
您可以查看[Aspose.Cells 文檔](https://reference.aspose.com/cells/net/)了解更多詳細資訊和範例。
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
