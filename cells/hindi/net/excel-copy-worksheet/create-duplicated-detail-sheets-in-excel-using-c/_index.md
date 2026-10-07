---
category: general
date: 2026-10-07
description: C# का उपयोग करके Excel में डुप्लिकेट डिटेल शीट्स बनाएं। जानें कि कैसे
  एक ही रन में कई वर्कशीट्स जेनरेट करें और टेबल्स से रिपोर्ट बनाएं।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicated detail sheets
- how to generate multiple worksheets
- generate excel report from tables
language: hi
lastmod: 2026-10-07
og_description: C# के साथ Excel में डुप्लिकेट डिटेल शीट्स बनाएं। यह ट्यूटोरियल दिखाता
  है कि कैसे कई वर्कशीट्स जेनरेट करें और टेबल्स से एक पूर्ण Excel रिपोर्ट तैयार करें।
og_image_alt: Screenshot of an Excel file that has create duplicated detail sheets
  output
og_title: Excel में डुप्लिकेट डिटेल शीट्स बनाएं – चरण‑दर‑चरण C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  headline: Create duplicated detail sheets in Excel using C#
  type: TechArticle
- description: Create duplicated detail sheets in Excel using C#. Learn how to generate
    multiple worksheets and build a report from tables in a single run.
  name: Create duplicated detail sheets in Excel using C#
  steps:
  - name: '**Obtain the data source** that contains a master table and two detail
      tables.'
    text: '**Obtain the data source** that contains a master table and two detail
      tables.'
  - name: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
    text: '**Configure the Smart‑marker processor** so each duplicated detail sheet
      receives a unique name.'
  - name: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
    text: '**Create a new workbook** and place a smart‑marker that references the
      master table.'
  - name: '**Run the processor** to generate the master sheet and all detail sheets.'
    text: '**Run the processor** to generate the master sheet and all detail sheets.'
  - name: '**Save the workbook** – each detail sheet now has a distinct name.'
    text: '**Save the workbook** – each detail sheet now has a distinct name.'
  type: HowTo
tags:
- C#
- Excel automation
- Aspose.Cells
title: C# का उपयोग करके Excel में डुप्लिकेट विवरण शीट्स बनाएं
url: /hi/net/excel-copy-worksheet/create-duplicated-detail-sheets-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# का उपयोग करके Excel में डुप्लिकेटेड डिटेल शीट्स बनाएं

यदि आपको एक Excel वर्कबुक में **डुप्लिकेटेड डिटेल शीट्स** बनानी हैं, तो यह गाइड पूरी प्रक्रिया को चरण‑दर‑चरण दिखाता है। आप देखेंगे कि **मास्टर‑डिटेल डेटा सेट** से कई वर्कशीट्स कैसे जेनरेट करें और टेबल्स से सीधे एक पॉलिश्ड Excel रिपोर्ट कैसे बनाएं।

टेबल्स से Excel रिपोर्ट बनाना बिलिंग सिस्टम, इन्वेंटरी डैशबोर्ड, या किसी भी स्थिति में सामान्य आवश्यकता है जहाँ एक मास्टर रिकॉर्ड के कई संबंधित डिटेल रो होते हैं। इस ट्यूटोरियल के अंत तक आपके पास एक रन करने योग्य C# प्रोग्राम होगा जो एक वर्कबुक बनाता है जिसमें एक मास्टर शीट और प्रत्येक डिटेल ग्रुप के लिए एक यूनिक नाम वाली शीट होती है।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास ये हैं:

* .NET 6.0 (या बाद का) स्थापित हो  
* Visual Studio 2022 या कोई भी C#‑compatible IDE  
* **Aspose.Cells for .NET** NuGet पैकेज (`SmartMarkerProcessor` प्रदान करता है)  

आप पैकेज को निम्न कमांड से जोड़ सकते हैं:

```bash
dotnet add package Aspose.Cells
```

## समाधान का Overview

समाधान निम्न पाँच चरणों में विभाजित है:

1. **डेटा स्रोत प्राप्त करें** जिसमें एक मास्टर टेबल और दो डिटेल टेबल्स हों।  
2. **Smart‑marker प्रोसेसर को कॉन्फ़िगर करें** ताकि प्रत्येक डुप्लिकेटेड डिटेल शीट को एक यूनिक नाम मिले।  
3. **एक नया वर्कबुक बनाएं** और मास्टर टेबल को रेफ़र करने वाला smart‑marker रखें।  
4. **प्रोसेसर चलाएँ** ताकि मास्टर शीट और सभी डिटेल शीट्स जेनरेट हो सकें।  
5. **वर्कबुक को सेव करें** – अब प्रत्येक डिटेल शीट का नाम अलग है।

हर चरण नीचे विस्तार से समझाया गया है, साथ में पूरा कोड और तर्क।

## Step 1: Obtain the data source that contains a master table and two detail tables

पहला काम एक `DataSet` बनाना है जो उस डेटा की नकल करता है जिसे आप सामान्यतः डेटाबेस से प्राप्त करेंगे। `DataSet` में **Master** नाम की एक टेबल और एक या अधिक **Detail** नाम की टेबल्स होनी चाहिए। Smart‑marker इंजन इन टेबल नामों को मार्कर के रूप में उपयोग करके वर्कबुक को भरता है।

```csharp
using System.Data;

/// <summary>
/// Returns a DataSet with a master table and two detail tables.
/// In a real application you would fill these tables from a database.
/// </summary>
static DataSet GetReportDataSet()
{
    var ds = new DataSet();

    // Master table – one row per invoice
    var master = new DataTable("Master");
    master.Columns.Add("InvoiceId", typeof(int));
    master.Columns.Add("CustomerName", typeof(string));
    master.Columns.Add("InvoiceDate", typeof(DateTime));
    master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
    master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
    ds.Tables.Add(master);

    // Detail table – multiple rows per invoice
    var detail = new DataTable("Detail");
    detail.Columns.Add("InvoiceId", typeof(int));
    detail.Columns.Add("Product", typeof(string));
    detail.Columns.Add("Quantity", typeof(int));
    detail.Columns.Add("Price", typeof(decimal));

    // Detail rows for Invoice 101
    detail.Rows.Add(101, "Widget A", 5, 9.99m);
    detail.Rows.Add(101, "Widget B", 2, 19.95m);

    // Detail rows for Invoice 102
    detail.Rows.Add(102, "Gadget X", 1, 99.00m);
    detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
    ds.Tables.Add(detail);

    return ds;
}
```

**Why this matters:**  
*Smart‑marker* `DataSet` ऑब्जेक्ट्स के साथ काम करता है; प्रत्येक टेबल नाम एक मार्कर बन जाता है जिसे इंजन बदल सकता है। इस तरह डेटा को स्ट्रक्चर करने से प्रोसेसर को हर अलग `InvoiceId` के लिए डिटेल शीट को ऑटोमैटिकली डुप्लिकेट करने में मदद मिलती है।

## Step 2: Configure the Smart‑marker processor to give each duplicated detail sheet a unique name

जब प्रोसेसर डिटेल मार्कर को देखता है, तो वह प्रत्येक रो ग्रुप के लिए एक नई वर्कशीट बनाता है। डिफ़ॉल्ट रूप से नई शीट्स का नाम समान रहता है, जिससे नामकरण टकराव हो जाता है। `DetailSheetNewName` सेट करने से इंजन को बताया जाता है कि प्रत्येक कॉपी को कैसे री‑नाम किया जाए।

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

/// <summary>
/// Configures the SmartMarkerProcessor to rename duplicated detail sheets.
/// The placeholder {0} is replaced with a sequential number (1, 2, …).
/// </summary>
static SmartMarkerProcessor ConfigureProcessor()
{
    var processor = new SmartMarkerProcessor();

    // The pattern "Detail_{0}" becomes Detail_1, Detail_2, …
    processor.Options.DetailSheetNewName = "Detail_{0}";

    // Optional: keep the original sheet as a template (if you have one)
    processor.Options.KeepTemplateSheet = false;

    return processor;
}
```

**Why this matters:**  
यदि यूनिक नाम पैटर्न नहीं दिया गया तो प्रोसेसर दूसरे डिटेल शीट को जोड़ते समय एक्सेप्शन फेंकेगा। प्लेसहोल्डर `{0}` सुनिश्चित करता है कि प्रत्येक शीट को एक अलग, प्रेडिक्टेबल नाम मिले।

## Step 3: Create a new workbook and place a smart‑marker that references the master table

अब आप एक नया `Workbook` बनाते हैं, एक मार्कर जोड़ते हैं जो **Master** टेबल की ओर इशारा करता है, और वैकल्पिक रूप से हेडर रो को फॉर्मेट करते हैं।

```csharp
/// <summary>
/// Creates a workbook with a single cell that contains the master smart‑marker.
/// </summary>
static Workbook CreateTemplateWorkbook()
{
    var workbook = new Workbook();
    var sheet = workbook.Worksheets[0];

    // Put the master smart‑marker in cell A1.
    // The double braces {{ }} tell SmartMarker to replace the content with the Master table.
    sheet.Cells["A1"].PutValue("{{Master}}");

    // Optional: add a header row for visual clarity.
    sheet.Cells["A2"].PutValue("Invoice ID");
    sheet.Cells["B2"].PutValue("Customer");
    sheet.Cells["C2"].PutValue("Date");
    sheet.Cells["A2:C2"].Style.Font.IsBold = true;

    return workbook;
}
```

**Why this matters:**  
मार्कर `{{Master}}` प्रोसेसर को निर्देश देता है कि मास्टर टेबल को `A1` से शुरू करके विस्तारित करे। इसके बाद की रोज़ प्रत्येक मास्टर रिकॉर्ड की डेटा रो बन जाती हैं। यह **generate excel report from tables** का एंट्री पॉइंट है।

## Step 4: Run the smart‑marker processor to generate the master sheet and the detail sheets

डेटा स्रोत, प्रोसेसर, और टेम्पलेट तैयार होने के बाद, आप `Process` को कॉल करते हैं। इंजन मास्टर मार्कर को विस्तारित करता है, फिर प्रत्येक अलग `InvoiceId` के लिए एक अलग डिटेल शीट बनाता है।

```csharp
static void GenerateReport()
{
    // 1️⃣ Obtain data
    DataSet reportData = GetReportDataSet();

    // 2️⃣ Configure processor
    SmartMarkerProcessor processor = ConfigureProcessor();

    // 3️⃣ Create template workbook
    Workbook workbook = CreateTemplateWorkbook();

    // 4️⃣ Process the smart‑markers – this creates the master sheet and duplicated detail sheets
    processor.Process(workbook, reportData);

    // 5️⃣ Save the file
    string outputPath = Path.Combine(
        Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
        "DuplicatedDetailSheets.xlsx");
    workbook.Save(outputPath);

    Console.WriteLine($"Report generated successfully: {outputPath}");
}
```

**Why this matters:**  
`processor.Process` भारी काम करता है: यह मास्टर रोज़ पढ़ता है, प्रत्येक यूनिक की के लिए एक डिटेल शीट बनाता है, और पहले परिभाषित पैटर्न के अनुसार उन शीट्स को री‑नाम करता है। परिणामस्वरूप एक ऐसी वर्कबुक मिलती है जो **how to generate multiple worksheets** की आवश्यकता को पूरा करती है।

## Step 5: Save the resulting workbook – each detail sheet now has a distinct name

`Save` कॉल फाइल को डिस्क पर लिख देता है। जब आप वर्कबुक खोलेंगे, तो आपको दिखेगा:

* **Sheet1** – मास्टर शीट जिसमें इनवॉइस हेडर होते हैं।  
* **Detail_1**, **Detail_2**, … – प्रत्येक शीट में **Detail** टेबल की वो रोज़ होती हैं जो किसी विशेष इनवॉइस से संबंधित हैं।

नीचे अपेक्षित वर्कबुक लेआउट का एक मॉक‑अप दिया गया है (इमेज केवल उदाहरणात्मक है; आप चाहें तो इसे वास्तविक स्क्रीनशॉट से बदल सकते हैं)।

![Screenshot of an Excel file that has create duplicated detail sheets output](https://example.com/images/duplicated-detail-sheets.png)

### Expected output

| Sheet name | Content description |
|------------|----------------------|
| **Sheet1** | Master rows: InvoiceId, CustomerName, InvoiceDate |
| **Detail_1** | Detail rows where `InvoiceId = 101` |
| **Detail_2** | Detail rows where `InvoiceId = 102` |

`DuplicatedDetailSheets.xlsx` खोलने पर ठीक यही संरचना दिखनी चाहिए।

## Full source code (ready to copy)

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelDetailSheetsDemo
{
    class Program
    {
        static void Main()
        {
            GenerateReport();
        }

        // ------------------------------------------------------------
        // Step 1 – data source
        // ------------------------------------------------------------
        static DataSet GetReportDataSet()
        {
            var ds = new DataSet();

            var master = new DataTable("Master");
            master.Columns.Add("InvoiceId", typeof(int));
            master.Columns.Add("CustomerName", typeof(string));
            master.Columns.Add("InvoiceDate", typeof(DateTime));
            master.Rows.Add(101, "Acme Corp", new DateTime(2024, 12, 01));
            master.Rows.Add(102, "Beta Ltd.", new DateTime(2024, 12, 03));
            ds.Tables.Add(master);

            var detail = new DataTable("Detail");
            detail.Columns.Add("InvoiceId", typeof(int));
            detail.Columns.Add("Product", typeof(string));
            detail.Columns.Add("Quantity", typeof(int));
            detail.Columns.Add("Price", typeof(decimal));
            detail.Rows.Add(101, "Widget A", 5, 9.99m);
            detail.Rows.Add(101, "Widget B", 2, 19.95m);
            detail.Rows.Add(102, "Gadget X", 1, 99.00m);
            detail.Rows.Add(102, "Gadget Y", 3, 49.50m);
            ds.Tables.Add(detail);

            return ds;
        }

        // ------------------------------------------------------------
        // Step 2 – processor configuration
        // ------------------------------------------------------------
        static SmartMarkerProcessor ConfigureProcessor()
        {
            var processor = new SmartMarkerProcessor();
            processor.Options.DetailSheetNewName = "Detail_{0}";
            processor.Options.KeepTemplate


## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [How to Name Sheets Automatically – Generate Multiple Sheets in C#](/cells/english/net/smart-markers-dynamic-data/how-to-name-sheets-automatically-generate-multiple-sheets-in/)
- [How to Create Worksheets – Step‑by‑Step Guide for Dynamic Excel Generation](/cells/english/net/worksheet-operations/how-to-create-worksheets-step-by-step-guide-for-dynamic-exce/)
- [How to Generate Excel Report in C# – Full Guide Using SmartMarker](/cells/english/net/smart-markers-dynamic-data/how-to-generate-excel-report-in-c-full-guide-using-smartmark/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}