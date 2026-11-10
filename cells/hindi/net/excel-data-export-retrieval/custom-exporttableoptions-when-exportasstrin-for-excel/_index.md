---
category: general
date: 2026-10-26
description: जब ExportAsStrin के साथ कस्टम ExportTableOptions का उपयोग किया जाता है,
  तो आप C# में Excel डेटा को स्ट्रिंग्स के रूप में निर्यात कर सकते हैं। निर्यात को
  कॉन्फ़िगर करने और चलाने के लिए चरण‑दर‑चरण गाइड का पालन करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: hi
lastmod: 2026-10-26
og_description: जब ExportAsStrin कस्टम ExportTableOptions स्ट्रिंग‑केवल Excel निर्यात
  को सक्षम करता है। C# में निर्यात को कॉन्फ़िगर और चलाने के सटीक चरण जानें।
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: कस्टम ExportTableOptions जब ExportAsString – C# में Excel को स्ट्रिंग के
  रूप में निर्यात करें
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Excel के लिए ExportAsStrin के समय कस्टम ExportTableOptions
url: /hi/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – Excel को स्ट्रिंग के रूप में एक्सपोर्ट करना C# में

यदि आपको **Custom ExportTableOptions when ExportAsStrin** की आवश्यकता है ताकि प्रत्येक सेल का मान एक साधारण स्ट्रिंग के रूप में प्राप्त हो, तो यह गाइड आपको ठीक‑ठीक बताता है कि इसे कैसे किया जाए। चाहे आप डेटा‑इम्पोर्ट पाइपलाइन बना रहे हों या एक साफ़ CSV‑तैयार डंप चाहिए, आप देखेंगे कि इस तरह विकल्पों को कॉन्फ़िगर करने से टाइप‑कन्वर्ज़न की आश्चर्यजनक स्थितियों से बचा जा सकता है।

इस ट्यूटोरियल में आप सीखेंगे **Excel को स्ट्रिंग के रूप में एक्सपोर्ट करना** Aspose.Cells लाइब्रेरी का उपयोग करके, पूरा, चलाने योग्य कोड देखेंगे, और प्रत्येक सेटिंग के पीछे की तर्क को समझेंगे। कोई बाहरी दस्तावेज़ीकरण आवश्यक नहीं – सब कुछ यहाँ उपलब्ध है।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित हों:

* .NET 6.0 SDK या बाद का संस्करण स्थापित हो  
* Visual Studio 2022 (या कोई भी IDE जो .NET को सपोर्ट करता हो)  
* Aspose.Cells for .NET पैकेज (NuGet के माध्यम से इंस्टॉल करें: `Install-Package Aspose.Cells`)  
* एक Excel वर्कबुक (`sample.xlsx`) जो प्रोजेक्ट की रूट फ़ोल्डर में रखी हो  

ये ही एकमात्र निर्भरताएँ हैं; कोड Windows, Linux, या macOS पर अतिरिक्त लाइब्रेरीज़ के बिना चलता है।

## Step 1: Load the workbook you want to export

**Custom ExportTableOptions when ExportAsStrin** का उपयोग करते समय पहला कदम है लोड किए गए वर्कबुक से एक `Worksheet` ऑब्जेक्ट प्राप्त करना। यह ऑब्जेक्ट आपको पंक्तियों, कॉलमों और एक्सपोर्ट API तक पहुँच देता है।

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*यह क्यों महत्वपूर्ण है:*  
`Workbook` फ़ाइल को एक बार पढ़ता है और सभी फ़ॉर्मेटिंग जानकारी को मेमोरी में रखता है। एक विशिष्ट `Worksheet` चुनकर आप एक्सपोर्ट का दायरा सीमित करते हैं और छिपी शीटों की अनावश्यक प्रोसेसिंग से बचते हैं।

## Step 2: Configure ExportTableOptions with ExportAsString = true

**Custom ExportTableOptions when ExportAsStrin** का मूल भाग है `ExportTableOptions` ऑब्जेक्ट। `ExportAsString` सेट करने से एक्सपोर्टर प्रत्येक सेल को स्ट्रिंग के रूप में ट्रीट करता है, चाहे उसका मूल डेटा टाइप (डेट, नंबर, बूलियन आदि) कुछ भी हो। `PreserveFormatting` को सक्षम करने से परिणामस्वरूप स्ट्रिंग में विज़ुअल स्टाइल (जैसे, मुद्रा चिह्न) बरकरार रहता है।

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*यह क्यों महत्वपूर्ण है:*  
जब आप बाद में `ExportDataTable` को कॉल करते हैं, तो लाइब्रेरी सामान्यतः प्रत्येक कॉलम के .NET टाइप का अनुमान लगाने की कोशिश करती है। `ExportAsString = true` होने पर यह अनुमान चरण छोड़ दिया जाता है, जिससे अप्रत्याशित `DateTime` या `double` रूपांतरणों से बचा जा सकता है जो डाउनस्ट्रीम CSV पार्सर को तोड़ सकते हैं।

## Step 3: Export a range to a DataTable using the custom options

अब आप वर्कशीट से एक आयताकार रेंज (पंक्तियाँ 0‑9, कॉलम 0‑4) को एक्सपोर्ट कर सकते हैं। यह मेथड एक `DataTable` लौटाता है जहाँ प्रत्येक फ़ील्ड `string` होती है।

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*यह क्यों महत्वपूर्ण है:*  
`ExportDataTable` Excel डेटा को एक रिलेशनल स्ट्रक्चर में ले जाने का सबसे सुविधाजनक तरीका है जिसे कई .NET APIs पहले से समझते हैं (जैसे, Entity Framework, Dapper)। **Custom ExportTableOptions when ExportAsStrin** पास करके आप सुनिश्चित करते हैं कि प्रत्येक `DataColumn.DataType` `typeof(string)` होगा।

## Step 4: Verify the result – all values are strings

यह सुनिश्चित करने के लिए कि एक्सपोर्ट अपेक्षित रूप से हुआ है, नीचे दिया गया लूप प्रत्येक सेल और उसके रनटाइम टाइप को प्रिंट करता है।

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Expected output**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

प्रत्येक सेल `String` को अपने टाइप के रूप में दिखाता है, जिससे पुष्टि होती है कि **Custom ExportTableOptions when ExportAsStrin** सही ढंग से काम किया।

## Step 5: Optional – write the DataTable to CSV

यदि आपका अंतिम लक्ष्य एक साधारण‑टेक्स्ट फ़ाइल बनाना है, तो आप आसानी से `DataTable` को CSV में सीरियलाइज़ कर सकते हैं:



## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच का पता लगा सकें।

- [Export HTML Strings from Excel to DataTable using Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Export Custom Properties Excel Pdf Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Custom Load Filters Excel Export](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}