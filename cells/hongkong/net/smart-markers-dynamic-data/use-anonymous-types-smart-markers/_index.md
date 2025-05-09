---
"description": "了解如何在 Aspose.Cells 中使用帶有智慧標記的匿名類型在 .NET 中產生動態 Excel 報表。遵循我們的簡單指南。"
"linktitle": "使用智慧標記 Aspose.Cells 的匿名類型"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "使用智慧標記 Aspose.Cells 的匿名類型"
"url": "/zh-hant/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用智慧標記 Aspose.Cells 的匿名類型

## 介紹
當談到在 .NET 應用程式中產生動態 Excel 報表時，Aspose.Cells 是一個脫穎而出的強大工具。其最佳功能之一是能夠使用智慧標記和匿名類型。如果您不熟悉這個概念，請不要擔心！本指南將分解您需要了解的所有內容，從先決條件到實際範例，同時保持其吸引力和易於遵循。
## 先決條件
在深入研究程式碼之前，讓我們確保您擁有順利運行本教程中的範例所需的一切。
### 1. .NET 環境
確保您的本機上已設定可正常運作的 .NET 環境。您可以使用 Visual Studio 或您選擇的任何其他 IDE。
### 2. Aspose.Cells庫
您將需要 Aspose.Cells 庫。如果你還沒有下載，你可以很容易地找到它 [這裡](https://releases.aspose.com/cells/net/)。您也可以透過以下網址免費試用 [此連結](https://releases。aspose.com/).
### 3. C#基礎知識
對 C# 程式設計的基本了解將幫助您更輕鬆地瀏覽本教學。如果您熟悉類別、物件和屬性等術語，那麼您就可以開始了！
## 導入包
若要在專案中使用 Aspose.Cells 庫，您必須匯入相關的命名空間。在 C# 檔案頂部新增以下使用指令：
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
這些命名空間將使您能夠存取稍後討論的所有必要的類別和方法。
現在，讓我們進入本教學的重點！您將看到如何使用自訂類別建立帶有智慧標記的 Excel 檔案。不用擔心;我們會把一切分解成易於管理的步驟！
## 步驟 1：建立自訂類
首先，我們需要一個簡單的類別來表示我們想要新增到 Excel 檔案中的資料。這個類別將保存有關一個人的信息。
```csharp
public class Person
{
    private string m_Name;
    private int m_Age;
    public string Name
    {
        get { return m_Name; }
        set { m_Name = value; }
    }
    public int Age
    {
        get { return m_Age; }
        set { m_Age = value; }
    }
    internal Person(string name, int age)
    {
        this.m_Name = name;
        this.m_Age = age;
    }
}
```
這裡我們定義一個類，叫做 `Person` 具有兩個屬性， `Name` 和 `Age`。構造函數初始化這些屬性。 
## 步驟 2：設定工作簿設計器
接下來，讓我們創建一個 `WorkbookDesigner` 類，我們將使用它來設計帶有智慧標記的 Excel 檔案。
```csharp
// 文檔目錄的路徑。
string dataDir = "Your Document Directory";
// 實例化工作簿設計器物件。
WorkbookDesigner report = new WorkbookDesigner();
```
代替 `"Your Document Directory"` 替換為您想要儲存 Excel 檔案的實際檔案路徑。這 `WorkbookDesigner` 類別是此操作的核心，您可以在其中定義模板。
## 步驟 3：向儲存格新增標記
現在，我們需要在工作表上新增智慧標記。這些標記將作為我們稍後輸入的資料的佔位符。
```csharp
// 取得工作簿中的第一個工作表。
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// 向儲存格輸入一些標記。
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
我們指定第一個工作表並設定標題儲存格的值。智慧標記的前綴為 `&=` 這告訴 Aspose 這些是稍後插入資料的佔位符。
## 步驟 4：建立人員列表
現在讓我們建立一個使用我們的 `Person` 我們將使用這個類別來填充智慧標記。
```csharp
// 根據自訂類別實例化清單集合。
IList<Person> list = new List<Person>();
// 使用自訂類別物件為標記提供值。
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
我們創建一個列表並添加 `Person` 對它。此清單作為我們填入 Excel 範本時的資料來源。
## 步驟5：設定資料來源和流程標記
準備好清單後，我們需要將其設定為 `WorkbookDesigner` 實例，然後處理標記。
```csharp
// 設定資料來源。
report.SetDataSource("MyProduct", list);
// 處理標記。
report.Process(false);
```
這 `SetDataSource` 方法將我們之前定義的列表連結到標記。這 `Process` 方法用我們物件的實際值替換工作簿中的智慧標記。
## 步驟6：儲存Excel文件
最後，我們將修改後的工作簿儲存到我們指定的目錄中。
```csharp
// 儲存 Excel 檔案。
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
此行將工作簿儲存到指定的檔案路徑。您可以使用 Excel 開啟此文件來查看插入的資料。
## 結論
就是這樣！您已成功使用 Aspose.Cells 中的智慧標記和您自己的自訂類別建立了 Excel 檔案。這種方法不僅使您的資料管理更加動態，而且還使您的程式碼保持乾淨和有序。
因此，無論您是產生用於分析、追蹤資訊或任何其他與數據相關的任務的報告，智慧標記都是您的盟友，可以使 Excel 報告更易於管理和更靈活！
## 常見問題解答
### Aspose.Cells 中的智慧標記是什麼？
智慧標記是 Excel 文件中的特殊佔位符，可讓您在執行時間動態插入資料。
### 我可以將匿名類型用於智慧標記嗎？
是的！智慧標記可用於任何物件類型，包括匿名類型，只要它們與預期的資料結構相符。
### Aspose.Cells 可以免費使用嗎？
Aspose.Cells 是一款付費產品，但您可以先免費試用以探索其功能。
### Aspose.Cells 支援哪些檔案格式？
它支援多種檔案格式，包括 XLS、XLSX、CSV 等。
### 在哪裡可以找到有關 Aspose.Cells 的更多資訊？
欲了解更多詳情，請查看 [文件](https://reference.aspose.com/cells/net/) 或訪問 [支援論壇](https://forum。aspose.com/c/cells/9).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}