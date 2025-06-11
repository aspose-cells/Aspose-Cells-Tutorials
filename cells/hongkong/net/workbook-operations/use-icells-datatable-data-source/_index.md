---
"description": "學習使用 ICellsDataTableDataSource 和 Aspose.Cells for .NET 來動態填入 Excel 表。非常適合在工作簿中自動化處理客戶資料。"
"linktitle": "使用 ICellsDataTableDataSource 作為工作簿設計器"
"second_title": "Aspose.Cells .NET Excel 處理 API"
"title": "使用 ICellsDataTableDataSource 作為工作簿設計器"
"url": "/zh-hant/net/workbook-operations/use-icells-datatable-data-source/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 ICellsDataTableDataSource 作為工作簿設計器

## 介紹
創建具有自動資料整合功能的高級電子表格可能會改變遊戲規則，尤其是在商業應用中。在本教程中，我們將深入探討如何使用 `ICellsDataTableDataSource` 用於 Aspose.Cells for .NET 中的工作簿設計器。我們將引導您建立一個簡單、人類可讀的解決方案，以將自訂資料動態載入到 Excel 檔案中。因此，如果您正在處理客戶名單、銷售數據或任何類似數據，本指南適合您！
## 先決條件
首先，請確保您具備以下條件：
- Aspose.Cells for .NET Library – 您可以從以下位置下載 [這裡](https://releases.aspose.com/cells/net/) 或取得免費試用版。
- .NET 開發環境 – Visual Studio 是一個很好的選擇。
- 對 C# 的基本了解 – 熟悉類別和資料處理將幫助您跟上進度。
在我們繼續之前，請確保您的開發環境已設定必要的軟體包。
## 導入包
為了有效地使用 Aspose.Cells，您需要匯入必要的套件。以下是所需命名空間的快速參考：
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## 步驟 1：定義客戶資料類
首先，創建一個簡單的 `Customer` 班級。此類將保存客戶的基本詳細信息，例如 `FullName` 和 `Address`。將其視為定義資料“形狀”的一種方法。
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## 步驟 2：設定客戶清單類
接下來，定義一個 `CustomerList` 擴展的類 `ArrayList`。此自訂清單將包含 `Customer` 並允許對每個條目進行索引存取。
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
在此步驟中，我們將資料包裝成 Aspose.Cells 可以識別和處理的格式。
## 步驟 3：建立客戶資料來源類
事情從這裡開始變得有趣。我們將創建一個 `CustomerDataSource` 類別實現 `ICellsDataTable` 使我們的資料與 Aspose.Cells 的工作簿設計器相容。
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
這種習俗 `CustomerDataSource` 類別使得 Aspose.Cells 能夠解釋每個 `Customer` 物件作為 Excel 文件中的一行。
## 步驟4：初始化客戶數據
現在，讓我們將一些客戶添加到我們的清單中。這裡我們將要寫入工作簿的資料載入進去。根據需要隨意添加更多條目。
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
在這個例子中，我們正在處理一個小資料集。但是，您可以透過從資料庫或其他來源載入資料輕鬆擴展此列表。
## 步驟 5：載入工作簿
現在，讓我們開啟一個包含必要的智慧標記的現有 Excel 工作簿。此工作簿將作為我們的模板，Aspose.Cells 將以客戶資料動態取代智慧標記。
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
確保 `"SmartMarker1.xlsx"` 包含佔位符，例如 `&=Customer.FullName` 和 `&=Customer.Address` 應填寫數據的位置。
## 步驟 6：設定工作簿設計器
現在，讓我們配置工作簿設計器以將我們的客戶資料來源與工作簿的智慧標記連結起來。
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
這 `SetDataSource` 方法綁定我們的 `CustomerDataSource` 到工作簿中的智慧標記。每個標記都標有 `&=Customer` Excel 中的資料現在將會被對應的客戶資料取代。
## 步驟 7：處理並儲存工作簿
最後，讓我們處理工作簿以填入資料並儲存結果。
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
此程式碼觸發智慧標記處理，用資料取代所有佔位符，並將結果儲存為 `dest。xlsx`.
## 結論
恭喜！您已成功實施 `ICellsDataTableDataSource` 對於使用 Aspose.Cells for .NET 的工作簿設計者。這種方法非常適合自動填入電子表格中的數據，尤其是在處理客戶清單或產品庫存等動態數據時。有了這些技能，您就可以順利建立數據驅動的應用程序，讓基於 Excel 的報告變得輕而易舉！
## 常見問題解答
### 什麼是 `ICellsDataTable` 在 Aspose.Cells 中？  
它是一個允許自訂資料來源與 Aspose.Cells Smart Markers 連結以實現動態資料填充的介面。
### 如何自訂工作簿範本中的資料？  
佔位符稱為智慧標記，例如 `&=Customer.FullName`，均被使用。這些標記在處理過程中被真實資料取代。
### Aspose.Cells for .NET 免費嗎？  
Aspose.Cells 提供免費試用，但完全存取需要付費許可證。檢查他們的 [免費試用](https://releases.aspose.com/) 或者 [買](https://purchase.aspose.com/buy) 選項。
### 我可以動態新增更多客戶資料嗎？  
絕對地！只需填充 `CustomerList` 在執行程式之前新增附加條目。
### 如果我遇到困難，可以去哪裡尋求協助？  
Aspose 有一個 [支援論壇](https://forum.aspose.com/c/cells/9) 用戶可以在這裡提出問題並獲得社區和 Aspose 團隊的幫助。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}