---
title: Use ICellsDataTableDataSource for Workbook Designer
linktitle: Use ICellsDataTableDataSource for Workbook Designer
second_title: Aspose.Cells .NET Excel Processing API
description: Learn to use ICellsDataTableDataSource with Aspose.Cells for .NET to dynamically populate Excel sheets. Perfect for automating customer data in workbooks.
weight: 21
url: /net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Use ICellsDataTableDataSource for Workbook Designer

## Introduction
Creating advanced spreadsheets with automated data integration can be a game-changer, especially in business applications. In this tutorial, we’ll dive into how to use `ICellsDataTableDataSource` for a workbook designer in Aspose.Cells for .NET. We’ll walk you through building a simple, human-readable solution to load custom data into an Excel file dynamically. So, if you're working with customer lists, sales data, or anything similar, this guide is for you!
## Prerequisites
To get started, make sure you have the following:
- Aspose.Cells for .NET Library – You can download it from [here](https://releases.aspose.com/cells/net/) or get a free trial version.
- .NET Development Environment – Visual Studio is a great choice.
- Basic Understanding of C# – Familiarity with classes and data handling will help you follow along.
Before we proceed, ensure that your development environment is set up with the necessary packages.
## Import Packages
To use Aspose.Cells effectively, you need to import essential packages. Below is a quick reference for the required namespaces:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Step 1: Define a Customer Data Class
To start, create a simple `Customer` class. This class will hold basic customer details like `FullName` and `Address`. Think of it as a way to define the "shape" of your data.
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
## Step 2: Set Up the Customer List Class
Next, define a `CustomerList` class that extends `ArrayList`. This customized list will hold instances of `Customer` and allow indexed access to each entry.
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
In this step, we’re wrapping our data into a format that Aspose.Cells can recognize and process.
## Step 3: Create the Customer Data Source Class
Here’s where things get interesting. We’ll create a `CustomerDataSource` class implementing `ICellsDataTable` to make our data compatible with Aspose.Cells’ workbook designer.
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
This custom `CustomerDataSource` class makes it possible for Aspose.Cells to interpret each `Customer` object as a row in the Excel file.
## Step 4: Initialize the Customer Data
Now, let’s add some customers to our list. Here’s where we load the data to be written into the workbook. Feel free to add more entries as needed.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
In this example, we’re working with a small dataset. However, you could easily expand this list by loading data from a database or other sources.
## Step 5: Load the Workbook
Now, let’s open an existing Excel workbook that contains the necessary Smart Markers. This workbook will serve as our template, and Aspose.Cells will dynamically replace Smart Markers with the customer data.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
Ensure that `"SmartMarker1.xlsx"` contains placeholders like `&=Customer.FullName` and `&=Customer.Address` where data should be filled in.
## Step 6: Set Up the Workbook Designer
Now, let’s configure the workbook designer to link our customer data source with the workbook’s Smart Markers.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
The `SetDataSource` method binds our `CustomerDataSource` to the Smart Markers in the workbook. Each marker labeled `&=Customer` in Excel will now be replaced by the corresponding customer data.
## Step 7: Process and Save the Workbook
Finally, let’s process the workbook to fill in the data and save the results.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
This code triggers the Smart Marker processing, replaces all placeholders with data, and saves the result as `dest.xlsx`.
## Conclusion
Congratulations! You’ve successfully implemented `ICellsDataTableDataSource` for a workbook designer using Aspose.Cells for .NET. This approach is ideal for automating data population in spreadsheets, especially when dealing with dynamic data like customer lists or product inventories. With these skills, you’re well on your way to building data-driven applications that make Excel-based reporting a breeze!
## FAQ's
### What is `ICellsDataTable` in Aspose.Cells?  
It’s an interface allowing custom data sources to be linked with Aspose.Cells Smart Markers for dynamic data population.
### How can I customize data in the workbook template?  
Placeholders called Smart Markers, such as `&=Customer.FullName`, are used. These markers are replaced with real data during processing.
### Is Aspose.Cells for .NET free?  
Aspose.Cells offers a free trial, but full access requires a paid license. Check their [free trial](https://releases.aspose.com/) or [buy](https://purchase.aspose.com/buy) options.
### Can I add more customer data dynamically?  
Absolutely! Simply populate the `CustomerList` with additional entries before running the program.
### Where can I get help if I’m stuck?  
Aspose has a [support forum](https://forum.aspose.com/c/cells/9) where users can ask questions and get assistance from the community and Aspose team.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
