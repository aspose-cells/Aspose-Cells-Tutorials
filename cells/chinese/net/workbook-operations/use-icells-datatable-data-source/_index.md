---
"description": "学习使用 ICellsDataTableDataSource 和 Aspose.Cells for .NET 动态填充 Excel 工作表。非常适合在工作簿中自动处理客户数据。"
"linktitle": "使用 ICellsDataTableDataSource 作为工作簿设计器"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "使用 ICellsDataTableDataSource 作为工作簿设计器"
"url": "/zh/net/workbook-operations/use-icells-datatable-data-source/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用 ICellsDataTableDataSource 作为工作簿设计器

## 介绍
创建具有自动数据集成功能的高级电子表格可能会带来翻天覆地的变化，尤其是在商业应用中。在本教程中，我们将深入探讨如何使用 `ICellsDataTableDataSource` 适用于 Aspose.Cells for .NET 中的工作簿设计器。我们将指导您构建一个简单易懂的解决方案，将自定义数据动态加载到 Excel 文件中。如果您正在处理客户列表、销售数据或类似数据，那么本指南非常适合您！
## 先决条件
首先，请确保您具备以下条件：
- Aspose.Cells for .NET Library – 您可以从以下位置下载 [这里](https://releases.aspose.com/cells/net/) 或获取免费试用版。
- .NET 开发环境 – Visual Studio 是一个很好的选择。
- 对 C# 的基本了解 – 熟悉类和数据处理将帮助您跟上进度。
在我们继续之前，请确保您的开发环境已设置必要的软件包。
## 导入包
为了有效地使用 Aspose.Cells，您需要导入必要的软件包。以下是所需命名空间的快速参考：
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## 步骤 1：定义客户数据类
首先，创建一个简单的 `Customer` 类。此类将保存客户的基本详细信息，例如 `FullName` 和 `Address`。可以将其视为定义数据“形状”的一种方法。
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
## 步骤 2：设置客户列表类
接下来，定义一个 `CustomerList` 扩展的类 `ArrayList`。此自定义列表将包含 `Customer` 并允许对每个条目进行索引访问。
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
在此步骤中，我们将数据包装成 Aspose.Cells 可以识别和处理的格式。
## 步骤 3：创建客户数据源类
事情开始变得有趣了。我们将创建一个 `CustomerDataSource` 类实现 `ICellsDataTable` 使我们的数据与 Aspose.Cells 的工作簿设计器兼容。
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
这种习俗 `CustomerDataSource` 类使得 Aspose.Cells 能够解释每个 `Customer` 对象作为 Excel 文件中的一行。
## 步骤4：初始化客户数据
现在，让我们将一些客户添加到列表中。这里我们将加载要写入工作簿的数据。您可以根据需要添加更多条目。
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
在此示例中，我们处理的数据集较小。不过，您可以通过从数据库或其他来源加载数据来轻松扩展此列表。
## 步骤 5：加载工作簿
现在，让我们打开一个包含所需智能标记的现有 Excel 工作簿。此工作簿将作为我们的模板，Aspose.Cells 将动态地用客户数据替换智能标记。
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
确保 `"SmartMarker1.xlsx"` 包含占位符，例如 `&=Customer.FullName` 和 `&=Customer.Address` 应填写数据的位置。
## 步骤 6：设置工作簿设计器
现在，让我们配置工作簿设计器以将我们的客户数据源与工作簿的智能标记链接起来。
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
这 `SetDataSource` 方法绑定我们的 `CustomerDataSource` 到工作簿中的智能标记。每个标记都标有 `&=Customer` Excel 中的数据现在将被相应的客户数据所取代。
## 步骤 7：处理并保存工作簿
最后，让我们处理工作簿以填充数据并保存结果。
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
此代码触发智能标记处理，用数据替换所有占位符，并将结果保存为 `dest。xlsx`.
## 结论
恭喜！您已成功实施 `ICellsDataTableDataSource` 适用于使用 Aspose.Cells for .NET 的工作簿设计人员。这种方法非常适合自动填充电子表格中的数据，尤其是在处理客户列表或产品库存等动态数据时。掌握这些技能后，您就可以轻松构建数据驱动的应用程序，让基于 Excel 的报表制作变得轻而易举！
## 常见问题解答
### 什么是 `ICellsDataTable` 在 Aspose.Cells 中？  
它是一个允许自定义数据源与 Aspose.Cells Smart Markers 链接以实现动态数据填充的接口。
### 如何自定义工作簿模板中的数据？  
占位符称为智能标记，例如 `&=Customer.FullName`，被使用。在处理过程中，这些标记会被替换为真实数据。
### Aspose.Cells for .NET 免费吗？  
Aspose.Cells 提供免费试用，但完整访问权限需要付费许可证。请查看他们的 [免费试用](https://releases.aspose.com/) 或者 [买](https://purchase.aspose.com/buy) 选项。
### 我可以动态添加更多客户数据吗？  
当然！只需填写 `CustomerList` 在运行程序之前添加附加条目。
### 如果我遇到困难，可以去哪里寻求帮助？  
Aspose 有一个 [支持论坛](https://forum.aspose.com/c/cells/9) 用户可以在这里提出问题并获得社区和 Aspose 团队的帮助。

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}