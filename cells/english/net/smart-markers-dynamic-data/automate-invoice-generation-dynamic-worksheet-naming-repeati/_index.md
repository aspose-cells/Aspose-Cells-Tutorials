---
category: general
date: 2026-02-14
description: 'Automate invoice generation with SmartMarker: learn how to repeat worksheets,
  name them dynamically, and master dynamic worksheet naming in minutes.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: en
og_description: Automate invoice generation with SmartMarker. This guide shows how
  to repeat worksheets, name them dynamically, and master dynamic worksheet naming.
og_title: Automate Invoice Generation – Dynamic Worksheet Naming & Repeating
tags:
- C#
- SmartMarker
- Excel Automation
title: Automate Invoice Generation – Dynamic Worksheet Naming & Repeating in C#
url: /net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Automate Invoice Generation – Dynamic Worksheet Naming & Repeating in C#

Ever wondered how to **automate invoice generation** without manually copying sheets for each order? You're not alone. Many developers hit a wall when they need a separate worksheet per invoice but also want the sheet name to reflect the order number. In this tutorial we’ll solve that problem using SmartMarker’s `SmartMarkerProcessor` and show you **how to name worksheets** dynamically while also covering **how to repeat worksheet** for each record. By the end you’ll have a ready‑to‑run C# sample that produces a workbook where each invoice lives on its own, nicely‑named tab.

We’ll walk through every step—from pulling orders from a data source to configuring `SmartMarkerOptions` for dynamic worksheet naming. No external docs required; everything you need is right here. A little prerequisite knowledge of C# and a reference to the Aspose.Cells library (or any SmartMarker‑compatible engine) will do.

---

## What You’ll Build

- Retrieve a collection of order objects.
- Configure SmartMarker to **repeat a worksheet** for each order.
- Apply **dynamic worksheet naming** using the `{OrderId}` placeholder.
- Generate an Excel file where each tab is named `Invoice_12345`, `Invoice_67890`, etc.
- Verify the output by opening the workbook.

---

## Prerequisites

- .NET 6.0 or later (the code compiles with .NET 5+ as well).
- Aspose.Cells for .NET (or any library that implements SmartMarker). Install via NuGet:

```bash
dotnet add package Aspose.Cells
```

- A basic `Order` class (you can replace it with your own DTO).

---

## Step 1: Set Up the Project and Model

First, create a new console app and define the data model that represents an order.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Pro tip:** Keep the model lightweight for the demo; you can always enrich it later with line items, tax details, etc.

---

## Step 2: Prepare the Excel Template

SmartMarker works against a template workbook. Create a file called `InvoiceTemplate.xlsx` with a single worksheet named `InvoiceTemplate`. In cell **A1** place a SmartMarker placeholder like:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

You can format the cells any way you like—bold headers, currency formatting, etc. Save the file in the project’s root folder.

> **Why a template?** It separates layout from code, letting designers tweak the look without touching the logic.

---

## Step 3: Configure SmartMarker Options – Repeat & Name Worksheets

Now we’ll tell SmartMarker to *repeat* the template worksheet for every order and to give each copy a name that includes the order ID. This is the core of **dynamic worksheet naming**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### How It Works

- **`RepeatWorksheet = true`** tells the engine to duplicate the source sheet for each element in the `orders` collection. This satisfies the **how to repeat worksheet** requirement.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** is a template string where `{OrderId}` is a placeholder that SmartMarker replaces with the current order’s ID. That’s the answer to **how to name worksheets** and **dynamic worksheet naming**.
- The processor merges each order’s fields (`{{OrderId}}`, `{{Customer}}`, etc.) into the duplicated sheet, producing a fully‑filled invoice.

---

## Step 4: Run the Application and Verify Output

Compile and run the console app:

```bash
dotnet run
```

You should see the success message in the console. Open `GeneratedInvoices.xlsx` and you’ll find three tabs:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Each sheet contains the order data substituted into the placeholders. The layout you designed in the template is preserved, proving that **automate invoice generation** works end‑to‑end.

### Expected Screenshot (alt text for SEO)

![automate invoice generation example showing three dynamically named worksheets](/images/invoice-automation.png)

> *Image alt text includes the primary keyword to satisfy SEO.*

---

## Step 5: Edge Cases & Common Variations

### What if an OrderId contains illegal characters?

Excel sheet names can’t contain `\ / ? * [ ] :`. If your IDs might include those, sanitize them:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Add a computed property to `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Need to keep the original template sheet?

Set `smartMarkerOptions.RemoveTemplate = false;` (default is `true`). This leaves the original `InvoiceTemplate` untouched as a reference.

### Want to group invoices by customer?

You can nest **repeat groups**. First repeat by customer, then by orders inside each customer worksheet. The syntax gets a bit more involved, but the principle stays the same—use `RepeatWorksheet` and a naming pattern that reflects the hierarchy.

---

## Full Working Example (All Code in One Place)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Copy‑paste this into `Program.cs`, place `InvoiceTemplate.xlsx` beside it, and you’re good to go.

---

## Frequently Asked Questions

**Q: Does this approach work with large data sets (thousands of invoices)?**  
A: Yes. SmartMarker streams data efficiently, but keep an eye on memory usage. If you hit limits, consider processing in batches and writing each batch to a separate workbook.

**Q: Can I add a logo to every invoice automatically?**  
A: Absolutely. Place the logo image on the template sheet. Since the sheet is duplicated, the logo appears on each generated invoice without extra code.

**Q: What if I need to protect the worksheets?**  
A: After processing, loop through `wb.Worksheets` and call `ws.Protect(Password, ProtectionType.All)`.

---

## Conclusion

We’ve just **automate invoice generation** by leveraging SmartMarker’s repeat‑worksheet feature and a clever naming pattern. The tutorial covered **how to name worksheets**, demonstrated **how to repeat worksheet** for each order, and showcased **dynamic worksheet naming** that keeps your workbook tidy and searchable.  

From pulling data, setting up a template, configuring `SmartMarkerOptions`, to handling edge cases, you now have a complete, runnable solution. Next, try adding line‑item tables, applying conditional formatting, or exporting the same data to PDF for a fully‑automated billing pipeline.

Ready to level up? Explore related topics such as “bulk Excel export with Aspose.Cells”, “PDF conversion of worksheets”, or “emailing generated invoices directly from C#”. The sky’s the limit—happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}