---
category: general
date: 2026-02-09
description: C# में हल्के नीले बैकग्राउंड के साथ वर्कबुक कैसे बनाएं और हेडर के साथ
  डेटा इम्पोर्ट करें। हल्का नीला बैकग्राउंड जोड़ना, डिफ़ॉल्ट एक्सेल स्टाइल का उपयोग
  करना और डेटाटेबल इम्पोर्ट करना सीखें।
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: hi
og_description: C# में हल्के नीले बैकग्राउंड के साथ वर्कबुक कैसे बनाएं, हेडर के साथ
  डेटा इम्पोर्ट करें, और डिफ़ॉल्ट एक्सेल स्टाइल लागू करें—सब कुछ एक संक्षिप्त गाइड
  में।
og_title: वर्कबुक कैसे बनाएं – हल्का नीला पृष्ठभूमि, डेटा आयात
tags:
- C#
- Excel
- Aspose.Cells
title: वर्कबुक कैसे बनाएं – हल्का नीला पृष्ठभूमि, डेटा आयात
url: /hi/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Create Workbook – Light Blue Background, Data Import

क्या आपने कभी सोचा है **how to create workbook** C# में ऐसा बनाने के बारे में जो बॉक्स से बाहर निकलते ही थोड़ा अधिक आकर्षक दिखे? शायद आपने डेटाबेस से एक `DataTable` निकाला है और आप साधे, डिफ़ॉल्ट‑सफ़ेद सेल्स से थक चुके हैं। इस ट्यूटोरियल में हम एक नया वर्कबुक बनाना, किसी कॉलम में हल्का‑नीला बैकग्राउंड जोड़ना, और हेडर के साथ डेटा इम्पोर्ट करना—सब कुछ Excel द्वारा प्रदान किए गए डिफ़ॉल्ट स्टाइल का उपयोग करके—का चरण‑दर‑चरण विवरण देंगे।

हम कुछ “what‑if” परिदृश्यों को भी शामिल करेंगे, जैसे null मानों को संभालना या एक से अधिक कॉलम को कस्टमाइज़ करना। अंत तक, आपके पास एक पूरी तरह से स्टाइल किया हुआ Excel फ़ाइल होगा जिसे आप बिना किसी पोस्ट‑प्रोसेसिंग के स्टेकहोल्डर्स को भेज सकते हैं।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* **.NET 6+** (कोड .NET Framework 4.6+ पर भी काम करता है)  
* **Aspose.Cells for .NET** – वह लाइब्रेरी जो `Workbook`, `Style`, और `ImportDataTable` कॉल्स को सक्षम बनाती है। इसे NuGet के माध्यम से इंस्टॉल करें:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* एक `DataTable` स्रोत – हम उदाहरण में एक नकली बनाते हैं, लेकिन आप इसे किसी भी ADO.NET क्वेरी से बदल सकते हैं।

सब तैयार है? बढ़िया, चलिए शुरू करते हैं।

## Step 1: Initialize a New Workbook (Primary Keyword)

सबसे पहला काम है **how to create workbook** – जैसा कि कहा जाता है। `Workbook` क्लास पूरे Excel फ़ाइल का प्रतिनिधित्व करती है, और इसका कंस्ट्रक्टर आपको एक साफ़ स्लेट देता है।

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Why this matters:** एक नई `Workbook` से शुरू करने से आप प्रारम्भ से ही हर स्टाइल को नियंत्रित कर सकते हैं। यदि आप मौजूदा फ़ाइल खोलते हैं, तो आपको मूल लेखक द्वारा छोड़े गए सभी स्टाइल मिलेंगे, जिससे फॉर्मेटिंग असंगत हो सकती है।

## Step 2: Prepare the DataTable You’ll Import

स्पष्टीकरण के लिए, चलिए एक सरल `DataTable` बनाते हैं। वास्तविक परिदृश्यों में आप संभवतः एक स्टोरड प्रोसीज़र या ORM मेथड को कॉल करेंगे।

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **Tip:** यदि आपको कॉलम क्रम को बिल्कुल वैसे ही रखना है जैसा डेटाबेस में है, तो `ImportDataTable` के `importColumnNames` पैरामीटर को `true` सेट करें। यह Aspose.Cells को आपके लिए कॉलम हेडर लिखने को कहता है।

## Step 3: Define Column Styles – Default + Light‑Blue Background

अब हम **add light blue background** भाग को हल करेंगे। Aspose.Cells आपको `Style` ऑब्जेक्ट्स की एक एरे पास करने की अनुमति देता है जो आप इम्पोर्ट कर रहे प्रत्येक कॉलम से मेल खाती है। पहला एंट्री कॉलम 0 के लिए, दूसरा कॉलम 1 के लिए, आदि। यदि आपके पास कॉलम की संख्या से कम स्टाइल हैं, तो बाकी कॉलम डिफ़ॉल्ट स्टाइल को अपनाते हैं।

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Why only two styles?** हमारे नमूने में चार कॉलम हैं, लेकिन हम केवल दूसरे कॉलम (Name) को हाइलाइट करना चाहते हैं। एरे की लंबाई कॉलम गिनती से मेल खाने की ज़रूरत नहीं है; कोई भी गायब एंट्री स्वचालित रूप से वर्कबुक की डिफ़ॉल्ट स्टाइल को विरासत में ले लेती है।

## Step 4: Import the DataTable with Headers and Styles

यहाँ हम **excel import datatable c#** और **import data with headers** को एक साथ लाते हैं। `ImportDataTable` मेथड भारी काम संभालता है: यह कॉलम नाम, पंक्तियों को लिखता है, और हमने अभी जो स्टाइल एरे बनाया था उसे लागू करता है।

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Expected Result

प्रोग्राम चलाने के बाद, `workbook` में एक ही वर्कशीट होगी जो इस प्रकार दिखेगी:

| **ID** | **Name** (हल्का‑नीला) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(खाली)*    | 75000      |

* **Name** कॉलम हल्का‑नीला बैकग्राउंड रखता है, जिससे यह साबित होता है कि स्टाइल एरे काम कर रहा है।  
* कॉलम हेडर स्वचालित रूप से जेनरेट होते हैं क्योंकि हमने `importColumnNames` के लिए `true` पास किया था।  
* Null मान खाली सेल के रूप में दिखते हैं, जो Aspose.Cells का डिफ़ॉल्ट व्यवहार है।

## Step 5: Save the Workbook (Optional but Useful)

आप संभवतः फ़ाइल को डिस्क पर लिखना या वेब क्लाइंट को स्ट्रीम करना चाहेंगे। सेव करना सीधा‑सादा है:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro tip:** यदि आप पुराने Excel संस्करणों को टार्गेट कर रहे हैं, तो `SaveFormat.Xlsx` को `SaveFormat.Xls` में बदल दें। API आपके लिए कन्वर्ज़न संभाल लेगा।

## Edge Cases & Variations

### Multiple Styled Columns

यदि आपको एक से अधिक स्टाइल्ड कॉलम चाहिए, तो बस `columnStyles` एरे को विस्तारित करें:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

अब दोनों **Name** और **Salary** हल्का‑नीला हो जाएंगे।

### Conditional Formatting Instead of Fixed Styles

कभी‑कभी आप चाहते हैं कि कोई कॉलम मान किसी थ्रेशहोल्ड से अधिक होने पर लाल हो जाए। यही वह जगह है जहाँ **use default style excel** को कंडीशनल फॉर्मेटिंग से जोड़ा जाता है:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Importing Without Headers

यदि आपका डाउनस्ट्रीम सिस्टम पहले से अपने हेडर प्रदान करता है, तो `importColumnNames` आर्ग्यूमेंट के लिए `false` पास करें। डेटा `A1` से शुरू होगा और आप बाद में कस्टम हेडर लिख सकते हैं।

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Full Working Example (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}