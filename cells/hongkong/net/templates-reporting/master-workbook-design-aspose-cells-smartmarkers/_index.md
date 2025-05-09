---
"date": "2025-04-06"
"description": "了解如何使用 Aspose.Cells .NET 和 SmartMarkers 建立動態 Excel 工作簿、自動產生報表並有效管理資料。"
"title": "使用 Aspose.Cells .NET 和 SmartMarkers 進行主工作簿設計，以實現高效報告"
"url": "/zh-hant/net/templates-reporting/master-workbook-design-aspose-cells-smartmarkers/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# 使用 Aspose.Cells .NET 中的 SmartMarkers 掌握工作簿設計

## 介紹

以程式設計方式創建高效、乾淨的工作簿設計可能具有挑戰性，尤其是在處理動態資料時。這就是 Aspose.Cells for .NET 的優勢所在，它提供了強大的功能，例如 SmartMarkers，可以簡化複雜工作簿的設計。使用 SmartMarkers，您可以將 Excel 範本直接連結到資料來源，從而實現無縫更新，反映資料集的即時變更。

在本教程中，我們將探討如何使用 Aspose.Cells .NET 設計使用 SmartMarkers 的工作簿並實現自訂資料來源以實現靈活高效的資料管理。您將學習如何：
- 在您的專案中設定 Aspose.Cells
- 將 WorkbookDesigner 類別與 SmartMarkers 結合使用
- 建立並使用自訂資料來源
- 在實際應用中應用這些技術

在開始之前，我們先回顧一下先決條件。

## 先決條件

在開始之前，請確保您已準備好以下內容：
- **.NET 環境**：安裝.NET（最好是.NET Core或.NET Framework 4.5+）。
- **Aspose.Cells for .NET函式庫**：使用 NuGet 安裝。
- **基本 C# 知識**：需要熟悉 C# 程式設計。

## 設定 Aspose.Cells for .NET

首先，透過以下方式安裝 Aspose.Cells for .NET 套件：

**使用 .NET CLI：**
```bash
dotnet add package Aspose.Cells
```

**使用套件管理器控制台：**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### 許可證獲取

Aspose 提供免費試用許可證以供評估。從 [臨時執照](https://purchase.aspose.com/temporary-license/) 頁。如需完全存取權限，請考慮透過其購買 [購買頁面](https://purchase。aspose.com/buy).

## 實施指南

在本節中，我們將示範如何使用 Aspose.Cells 實作 SmartMarkers 和自訂資料來源。

### 使用 SmartMarkers 設計工作簿

**概述**：此功能將您的電子表格範本與資料來源連結。使用 SmartMarkers 可以簡化工作簿的動態填充。

#### 步驟 1：初始化您的環境
設定目錄並載入包含 SmartMarkers 的範本工作簿。
```csharp
using Aspose.Cells;
using System.Collections;

string SourceDir = "YOUR_SOURCE_DIRECTORY";
string OutputDir = "YOUR_OUTPUT_DIRECTORY";

Workbook workbook = new Workbook(SourceDir + "SmartMarker1.xlsx");
```

#### 第 2 步：設定資料來源
建立客戶資料清單來填入 SmartMarkers。
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```

#### 步驟3：初始化WorkbookDesigner並設定資料來源
使用 `WorkbookDesigner` 類別將您的資料來源與 SmartMarkers 連結。
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```

#### 步驟 4：處理智慧標記
處理工作簿以以清單中的實際資料取代所有 SmartMarker。
```csharp
designer.Process();
workbook.Save(OutputDir + "dest.xlsx");
```

### 工作簿設計器自訂資料來源實現

**概述**：實作自訂資料來源可以靈活地管理資料並將其對應到 Excel 範本。

#### 步驟 1：定義客戶資料來源類
實施 `ICellsDataTable` 接口，允許 Aspose.Cells 與您的自訂資料結構進行互動。
```csharp
using System;
using System.Collections;
using System.Reflection;

public class CustomerDataSource : ICellsDataTable
{
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

    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private System.Reflection.PropertyInfo[] m_Properties;

    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;

    public void BeforeFirst() { this.m_IEnumerator = this.m_DataSource.GetEnumerator(); }

    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);

    public object this[string columnName]
        => ((System.Reflection.PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);

    public bool Next() { return m_IEnumerator != null && m_IEnumerator.MoveNext(); }
}
```

### Customer 和 CustomerList 類

**概述**：這些類別提供了一種管理記憶體中客戶資料的簡單方法。

#### 步驟 1：實作客戶類
此類包含個人客戶詳細資料。
```csharp
class Customer
{
    public string FullName { get; set; }
    public string Address { get; set; }

    public Customer(string fullName, string address)
    {
        FullName = fullName;
        Address = address;
    }
}
```

#### 步驟 2：實作 CustomerList 類
延長 `ArrayList` 管理客戶清單。
```csharp
class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```

## 實際應用

以下是在 Aspose.Cells 中使用 SmartMarkers 和自訂資料來源的一些實際用例：
1. **自動化財務報告**：透過將 Excel 範本與最新的交易資料連結起來，快速產生動態財務報告。
2. **庫存管理**：透過從中央資料庫自動更新電子表格來有效地管理庫存水準。
3. **客戶關係管理 (CRM)**：無縫同步不同部門之間的客戶數據，增強溝通與效率。

## 性能考慮

使用 Aspose.Cells for .NET 時，請考慮以下技巧來優化效能：
- 使用高效的資料結構，例如 `ArrayList` 或根據您的需求自訂系列。
- 如果處理大型資料集，則分批處理工作簿以有效管理記憶體使用情況。
- 快取經常存取的資源以減少處理時間。

## 結論

在本教學中，您學習如何使用 Aspose.Cells for .NET 使用 SmartMarkers 設計 Excel 工作簿並實作自訂資料來源。這些技術可以簡化您的工作流程，讓您更容易處理電子表格中的動態資料。

接下來，考慮探索 Aspose.Cells 的更多高級功能或將這些解決方案整合到更大的應用程式中。透過嘗試不同的資料結構和範本來深入了解哪種方法最適合您的特定用例。

## 常見問題部分

**問題 1：Aspose.Cells 中的 SmartMarkers 是什麼？**
SmartMarkers 允許您將 Excel 範本單元格直接與資料來源欄位鏈接，從而實現無縫的動態更新。

**問題2：如何使用 Aspose.Cells 處理大型資料集？**
考慮以較小的批次處理工作簿並使用高效的資料結構來有效地管理記憶體使用情況。

**問題 3：我可以將 SmartMarkers 用於非 Excel 檔案格式嗎？**
Aspose.Cells 主要針對 Excel 檔案設計；但是，您可以在套用 SmartMarkers 之前將其他檔案格式轉換為 Excel。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}