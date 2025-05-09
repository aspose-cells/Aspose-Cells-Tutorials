---
"description": "了解如何在 Aspose.Cells 中使用带有智能标记的匿名类型在 .NET 中生成动态 Excel 报告。请遵循我们的简易指南。"
"linktitle": "使用智能标记 Aspose.Cells 的匿名类型"
"second_title": "Aspose.Cells .NET Excel 处理 API"
"title": "使用智能标记 Aspose.Cells 的匿名类型"
"url": "/zh/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 使用智能标记 Aspose.Cells 的匿名类型

## 介绍
在 .NET 应用程序中生成动态 Excel 报表时，Aspose.Cells 是一款功能强大的工具。其最佳功能之一是能够使用智能标记和匿名类型。如果您不熟悉此概念，不用担心！本指南将分解您需要了解的所有内容，从先决条件到实际操作示例，同时保持引人入胜且易于理解。
## 先决条件
在深入研究代码之前，让我们确保您拥有顺利运行本教程中的示例所需的一切。
### 1. .NET 环境
确保本地计算机上已设置好正常运行的 .NET 环境。您可以使用 Visual Studio 或任何其他您选择的 IDE。
### 2. Aspose.Cells库
你需要 Aspose.Cells 库。如果你还没有下载，可以很容易地找到它。 [这里](https://releases.aspose.com/cells/net/)。您也可以通过以下网址免费试用 [此链接](https://releases。aspose.com/).
### 3. C#基础知识
对 C# 编程有基本的了解将有助于你更轻松地学习本教程。如果你熟悉类、对象和属性等术语，那就没问题了！
## 导入包
要在项目中使用 Aspose.Cells 库，必须导入相关的命名空间。在 C# 文件的顶部添加以下 using 指令：
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
这些命名空间将使您能够访问稍后讨论的所有必要的类和方法。
现在，让我们进入本教程的正题！您将学习如何使用自定义类创建带有智能标记的 Excel 文件。别担心，我们会把所有内容分解成易于操作的步骤！
## 步骤 1：创建自定义类
首先，我们需要一个简单的类来表示我们要添加到 Excel 文件中的数据。这个类将保存关于一个人的信息。
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
这里我们定义一个类，叫做 `Person` 具有两个属性， `Name` 和 `Age`构造函数初始化这些属性。 
## 步骤 2：设置工作簿设计器
接下来，让我们创建一个 `WorkbookDesigner` 类，我们将使用它来设计带有智能标记的 Excel 文件。
```csharp
// 文档目录的路径。
string dataDir = "Your Document Directory";
// 实例化工作簿设计器对象。
WorkbookDesigner report = new WorkbookDesigner();
```
代替 `"Your Document Directory"` 替换为您想要保存 Excel 文件的实际文件路径。 `WorkbookDesigner` 类是此操作的核心，您可以在其中定义模板。
## 步骤 3：向单元格添加标记
现在，我们需要在工作表中添加智能标记。这些标记将作为我们稍后输入的数据的占位符。
```csharp
// 获取工作簿中的第一个工作表。
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// 向单元格输入一些标记。
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
我们指定第一个工作表并设置标题单元格的值。智能标记的前缀为 `&=` 这告诉 Aspose 这些是稍后插入数据的占位符。
## 步骤 4：创建人员列表
现在让我们创建一个使用我们的 `Person` 我们将使用这个类来填充智能标记。
```csharp
// 根据自定义类实例化列表集合。
IList<Person> list = new List<Person>();
// 使用自定义类对象为标记提供值。
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
我们创建一个列表并添加 `Person` 到它。此列表作为我们填充 Excel 模板时的数据源。
## 步骤5：设置数据源和流程标记
准备好列表后，我们需要将其设置为 `WorkbookDesigner` 实例，然后处理标记。
```csharp
// 设置数据源。
report.SetDataSource("MyProduct", list);
// 处理标记。
report.Process(false);
```
这 `SetDataSource` 方法将我们之前定义的列表链接到标记。 `Process` 方法用我们对象的实际值替换工作簿中的智能标记。
## 步骤6：保存Excel文件
最后，我们将修改后的工作簿保存到我们指定的目录中。
```csharp
// 保存 Excel 文件。
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
此行将工作簿保存到指定的文件路径。您可以使用 Excel 打开此文件来查看插入的数据。
## 结论
就这样！您已成功使用 Aspose.Cells 中的智能标记和自定义类创建了一个 Excel 文件。这种方法不仅使您的数据管理更加动态，而且还使您的代码保持整洁有序。
因此，无论您是生成用于分析、跟踪信息还是任何其他与数据相关的任务的报告，智能标记都是您的盟友，可以使 Excel 报告更易于管理和更灵活！
## 常见问题解答
### Aspose.Cells 中的智能标记是什么？
智能标记是 Excel 文档中的特殊占位符，允许您在运行时动态插入数据。
### 我可以将匿名类型用于智能标记吗？
是的！智能标记可以用于任何对象类型，包括匿名类型，只要它们符合预期的数据结构。
### Aspose.Cells 可以免费使用吗？
Aspose.Cells 是一款付费产品，但您可以先免费试用以探索其功能。
### Aspose.Cells 支持哪些文件格式？
它支持多种文件格式，包括 XLS、XLSX、CSV 等。
### 在哪里可以找到有关 Aspose.Cells 的更多信息？
欲了解更多详情，请查看 [文档](https://reference.aspose.com/cells/net/) 或访问 [支持论坛](https://forum。aspose.com/c/cells/9).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}