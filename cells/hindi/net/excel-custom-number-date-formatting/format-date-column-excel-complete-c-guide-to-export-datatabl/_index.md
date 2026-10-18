---
category: general
date: 2026-07-13
description: डेटा टेबल को C# से एक्सपोर्ट करते समय Excel में डेट कॉलम को फॉर्मेट करें।
  मिनटों में Excel एक्सपोर्ट डेटाटेबल C# सीखें और स्टाइलिंग के साथ डेटाटेबल को Excel
  में इम्पोर्ट करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- format date column excel
- excel export datatable c#
- import datatable to excel
language: hi
lastmod: 2026-07-13
og_description: Excel में तिथि कॉलम को आसानी से फ़ॉर्मेट करें। यह गाइड आपको दिखाता
  है कि C# में डेटाटेबल को Excel में कैसे निर्यात करें और कस्टम स्टाइल के साथ डेटाटेबल
  को Excel में कैसे आयात करें।
og_image_alt: Screenshot showing a formatted date column in an Excel sheet generated
  from C#
og_title: एक्सेल में तिथि कॉलम को फ़ॉर्मेट करें – चरण‑दर‑चरण C# निर्यात ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  headline: Format Date Column Excel – Complete C# Guide to Export DataTable
  type: TechArticle
- description: Format date column Excel while exporting a DataTable from C#. Learn
    excel export datatable c# and import datatable to excel with styling in minutes.
  name: Format Date Column Excel – Complete C# Guide to Export DataTable
  steps:
  - name: What if My DataTable Has More Than Three Columns?
    text: Just extend the `columnStyles` array. For any column you don’t explicitly
      style, leave the entry `null`; Excel will apply the default General format.
  - name: How to Apply a Custom Date Format (e.g., “dd‑MMM‑yyyy”)?
    text: 'Replace the built‑in number with a custom string:'
  - name: Can I Use This Approach with EPPlus or ClosedXML?
    text: 'Yes, the concept is identical: create a style object, assign it to a column,
      then load the `DataTable`. The API differs, but the **excel export datatable
      c#** pattern remains the same.'
  - name: What About Large DataSets (100k+ rows)?
    text: '`ImportDataTable` is optimized for bulk writes, but you might hit memory
      limits. In that case, consider streaming rows with `Cells.ImportDataTable` in
      chunks, or use `Worksheet.Cells["A1"].PutValue` in a loop while reusing the
      style objects.'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Export
title: Excel में तिथि कॉलम को फ़ॉर्मेट करें – DataTable निर्यात करने के लिए पूर्ण
  C# गाइड
url: /hi/net/excel-custom-number-date-formatting/format-date-column-excel-complete-c-guide-to-export-datatabl/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# फ़ॉर्मेट डेट कॉलम एक्सेल – डेटा टेबल निर्यात के लिए पूर्ण C# गाइड

क्या आपको कभी डेटाबेस से डेटा निकालते समय **format date column Excel** करने की ज़रूरत पड़ी है, लेकिन सेल्स में कच्चे टाइमस्टैम्प दिखते रहे? आप अकेले नहीं हैं। कई व्यावसायिक ऐप्स में डिफ़ॉल्ट निर्यात `DateTime` मान जैसे `2024‑03‑15 00:00:00` को डंप कर देता है और कोई भी इस अव्यवस्था को नहीं चाहता।

अच्छी खबर यह है कि आप C# से सीधे प्रत्येक कॉलम की सटीक दिखावट को नियंत्रित कर सकते हैं। इस ट्यूटोरियल में हम एक एंड‑टू‑एंड समाधान पर चलेंगे जो **excel export datatable c#** करता है, पहले कॉलम पर डेट स्टाइल, दूसरे पर करंसी स्टाइल लागू करता है, और अंत में **import datatable to excel** को शून्य‑दर्द शैली के साथ करता है।

अंत तक आपके पास एक पुन: उपयोग योग्य मेथड होगा जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं, चाहे आप .NET 6, .NET Framework 4.8, या किसी बाद के संस्करण का उपयोग कर रहे हों।

---

## आपको क्या चाहिए

- **Aspose.Cells for .NET** (या कोई भी लाइब्रेरी जो `CreateStyle` और `ImportDataTable` प्रदान करती है)। कोड स्निपेट्स Aspose का उपयोग करते हैं क्योंकि इसका API साफ़ और व्यापक रूप से अपनाया गया है।
- एक **DataTable** जिसे आप पहले से ही SQL, CSV, या किसी अन्य स्रोत से भरते हैं।
- Visual Studio (या आपका पसंदीदा IDE)।
- .NET रनटाइम 5.0+ (सैंपल .NET 6 को टार्गेट करता है, लेकिन पुराने फ्रेमवर्क भी समान रूप से काम करते हैं।

यदि आपके पास अभी तक Aspose.Cells नहीं है, तो आधिकारिक साइट से मुफ्त ट्रायल प्राप्त करें—कोई क्रेडिट‑कार्ड आवश्यक नहीं।

---

## चरण 1: स्रोत डेटा को DataTable के रूप में प्राप्त करें

सबसे पहले, आपको एक `DataTable` चाहिए। वास्तविक‑दुनिया के परिदृश्यों में यह आमतौर पर `SqlDataAdapter.Fill` से आता है, लेकिन स्पष्टता के लिए हम एक सरल टेबल को मॉक करेंगे:

```csharp
using System;
using System.Data;

DataTable GetSampleData()
{
    var dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("TotalAmount", typeof(decimal));
    dt.Columns.Add("Customer", typeof(string));

    dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
    dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
    dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");

    return dt;
}
```

> **प्रो टिप:** जब आप डेटा सीधे स्टोरड प्रोसीजर से निकालते हैं, तो सुनिश्चित करें कि कॉलम प्रकार इच्छित Excel फ़ॉर्मेट से मेल खाते हों। एक `datetime` कॉलम बाद में हमारे **format date column excel** स्टाइल का लक्ष्य होगा।

## चरण 2: एक Excel वर्कबुक बनाएं और कॉलम स्टाइल्स परिभाषित करें

अब हम एक नई वर्कबुक बनाते हैं। **format date column excel** का ट्रिक एक `Style` ऑब्जेक्ट बनाने में है, उसकी `Number` प्रॉपर्टी को बिल्ट‑इन Excel डेट फ़ॉर्मेट (कोड 14) पर सेट करने में, और उस स्टाइल को उपयुक्त कॉलम इंडेक्स पर असाइन करने में।

```csharp
using Aspose.Cells;

Workbook wb = new Workbook();               // creates a blank workbook
Worksheet sheet = wb.Worksheets[0];        // we’ll work with the first sheet

// Prepare a style array – one entry per DataTable column
Style[] columnStyles = new Style[dt.Columns.Count];

// Column 0 – format as a short date (e.g., 03/15/2024)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Excel built‑in date format

// Column 1 – format as currency (e.g., $1,245.67)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].Number = 2;                // Built‑in currency format

// Column 2 – no special formatting; leave null or default
columnStyles[2] = null;
```

क्यों `Number = 14`? Excel तिथियों को सीरियल नंबरों के रूप में संग्रहीत करता है; फ़ॉर्मेट 14 प्रोग्राम को उन नंबरों को लोकल की शॉर्ट‑डेट पैटर्न के साथ रेंडर करने के लिए बताता है। यदि आपको कस्टम पैटर्न चाहिए (जैसे `dd‑MMM‑yyyy`), तो आप `columnStyles[0].Custom = "dd-MMM-yyyy"` सेट कर सकते हैं।

## चरण 3: स्टाइल्स के साथ DataTable को वर्कशीट में इम्पोर्ट करें

स्टाइल एरे तैयार होने के साथ, इम्पोर्ट कॉल एक ही लाइन में है। यह **excel export datatable c#** का हृदय है और वह स्थान भी जहाँ हम **import datatable to excel** करते हुए अपना फ़ॉर्मेटिंग बनाए रखते हैं।

```csharp
// Import the DataTable, include column headers, start at cell A1 (row 0, column 0)
sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
```

`ImportDataTable` ओवरलोड जिसे हम उपयोग कर रहे हैं, स्टाइल एरे को स्वीकार करता है, डेटा लिखते समय प्रत्येक स्टाइल को मिलते‑जुलते कॉलम पर लागू करता है। कोई पोस्ट‑प्रोसेसिंग लूप आवश्यक नहीं—आपका डेट कॉलम पहले से ही सुंदर रूप से फ़ॉर्मेटेड है।

## चरण 4: वर्कबुक को सेव करें (या सीधे ब्राउज़र में स्ट्रीम करें)

आपके परिदृश्य के आधार पर आप डिस्क, मेमोरी स्ट्रीम में सेव कर सकते हैं, या फ़ाइल को HTTP रिस्पॉन्स के रूप में रिटर्न कर सकते हैं। यहाँ तीन सामान्य पैटर्न हैं:

```csharp
// 1️⃣ Save to a physical file
wb.Save("ExportedReport.xlsx");

// 2️⃣ Save to a MemoryStream (useful for ASP.NET Core)
using var ms = new MemoryStream();
wb.Save(ms, SaveFormat.Xlsx);
ms.Position = 0; // rewind for downstream consumers

// 3️⃣ Return as a file download in ASP.NET MVC
public IActionResult DownloadReport()
{
    var dt = GetSampleData();
    var wb = BuildWorkbook(dt); // encapsulate steps 2‑3 in a method
    using var ms = new MemoryStream();
    wb.Save(ms, SaveFormat.Xlsx);
    return File(ms.ToArray(), 
                "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "Report.xlsx");
}
```

> **ध्यान दें:** यदि आप ASP.NET Core में `FileResult` का उपयोग कर रहे हैं, तो फ़ाइल के ऑन‑द‑फ़्लाई जनरेट होने पर `Response.Headers["Cache-Control"] = "no-cache"` सेट करना सुनिश्चित करें। यह ब्राउज़र को पुराना संस्करण सर्व करने से रोकता है।

## चरण 5: परिणाम सत्यापित करें – Excel शीट कैसी दिखती है

कोड चलाने के बाद, `ExportedReport.xlsx` खोलें। आपको यह दिखना चाहिए:

| OrderDate (formatted) | TotalAmount (currency) | Customer |
|-----------------------|------------------------|----------|
| 03/13/2024            | $1,245.67              | Acme Corp|
| 03/14/2024            | $980.00                | Beta Ltd |
| 03/15/2024            | $1,500.25              | Gamma Inc|

![format date column excel उदाहरण](/images/format-date-column-excel.png)

*छवि वैकल्पिक पाठ: format date column excel – Excel शीट का स्क्रीनशॉट जिसमें डेट कॉलम सही ढंग से फ़ॉर्मेट किया गया है।*

## सामान्य प्रश्न और किनारे के मामले

### यदि मेरे DataTable में तीन से अधिक कॉलम हैं तो क्या करें?

सिर्फ `columnStyles` एरे को विस्तारित करें। किसी भी कॉलम के लिए जिसे आप स्पष्ट रूप से स्टाइल नहीं करते, एंट्री `null` रखें; Excel डिफ़ॉल्ट General फ़ॉर्मेट लागू करेगा।

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 10; // Percent format, for example
```

### कस्टम डेट फ़ॉर्मेट (जैसे “dd‑MMM‑yyyy”) कैसे लागू करें?

बिल्ट‑इन नंबर को कस्टम स्ट्रिंग से बदलें:

```csharp
columnStyles[0].Custom = "dd-MMM-yyyy";
```

### क्या मैं इस दृष्टिकोण को EPPlus या ClosedXML के साथ उपयोग कर सकता हूँ?

हाँ, अवधारणा समान है: एक स्टाइल ऑब्जेक्ट बनाएं, उसे कॉलम को असाइन करें, फिर `DataTable` लोड करें। API अलग है, लेकिन **excel export datatable c#** पैटर्न वही रहता है।

### बड़े डेटा सेट (100k+ पंक्तियों) के बारे में क्या?

`ImportDataTable` बल्क राइट्स के लिए ऑप्टिमाइज़्ड है, लेकिन आप मेमोरी लिमिट तक पहुँच सकते हैं। ऐसे में, `Cells.ImportDataTable` को चंक्स में उपयोग करके पंक्तियों को स्ट्रीम करने पर विचार करें, या लूप में `Worksheet.Cells["A1"].PutValue` का उपयोग करें जबकि स्टाइल ऑब्जेक्ट्स को पुन: उपयोग करें।

## पूर्ण कार्यशील उदाहरण (सभी चरण एक मेथड में)

नीचे एक स्व-निहित मेथड है जिसे आप किसी भी कंसोल ऐप या ASP.NET कंट्रोलर में कॉपी‑पेस्ट कर सकते हैं। यह पूरे फ्लो को दर्शाता है—डेटा रिट्रीवल से लेकर स्टाइल्ड Excel निर्यात तक।

```csharp
using System;
using System.Data;
using System.IO;
using Aspose.Cells;

public class ExcelExporter
{
    // Entry point for demonstration
    public static void Main()
    {
        DataTable dt = GetSampleData();
        Workbook wb = BuildWorkbook(dt);
        wb.Save("StyledExport.xlsx");
        Console.WriteLine("Excel file created – check StyledExport.xlsx");
    }

    // Generates the sample DataTable (Step 1)
    private static DataTable GetSampleData()
    {
        var dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("TotalAmount", typeof(decimal));
        dt.Columns.Add("Customer", typeof(string));

        dt.Rows.Add(DateTime.Today.AddDays(-2), 1245.67m, "Acme Corp");
        dt.Rows.Add(DateTime.Today.AddDays(-1), 980.00m, "Beta Ltd");
        dt.Rows.Add(DateTime.Today, 1500.25m, "Gamma Inc");
        return dt;
    }

    // Builds the workbook with styled columns (Steps 2‑3)
    private static Workbook BuildWorkbook(DataTable dt)
    {
        var wb = new Workbook();
        var sheet = wb.Worksheets[0];

        // Allocate style array
        Style[] columnStyles = new Style[dt.Columns.Count];

        // Format column 0 as short date
        columnStyles[0] = wb.CreateStyle();
        columnStyles[0].Number = 14; // short date

        // Format column 1 as currency
        columnStyles[1] = wb.CreateStyle();
        columnStyles[1].Number = 2; // currency

        // No style for column 2 (Customer name)
        columnStyles[2] = null;

        // Import with headers, start at A1
        sheet.Cells.ImportDataTable(dt, true, 0, 0, columnStyles);
        return wb;
    }
}
```

प्रोग्राम चलाएँ, `StyledExport.xlsx` खोलें, और आप देखेंगे कि **format date column excel** पूरी तरह से लागू हो गया है।

## सारांश और अगले कदम

हमने अभी-अभी बताया कि **excel export datatable c#** करते समय **format date column excel** कैसे किया जाता है, और कैसे एक ही कॉल में प्रति‑कॉलम स्टाइलिंग के साथ **import datatable to excel** किया जाता है। मुख्य बिंदु:

1. प्रत्येक कॉलम के लिए जिसे आप फ़ॉर्मेट करना चाहते हैं, एक `Style` बनाएं।
2. डेट्स के लिए `Number = 14` उपयोग करें, करंसी के लिए `Number = 2`, या कोई भी कस्टम फ़ॉर्मेट जिसकी आपको आवश्यकता हो।
3. स्टाइल एरे को `ImportDataTable` को पास करें—लाइब्रेरी भारी काम करती है।

आप आगे क्या एक्सप्लोर कर सकते हैं?

- **Conditional formatting** ताकि ओवरड्यू डेट्स को हाइलाइट किया जा सके।
- ** 

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं ताकि आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर कर सकें।

- [Aspose.Cells for .NET का उपयोग करके DataTable को Excel में इम्पोर्ट कैसे करें (स्टेप‑बाय‑स्टेप गाइड)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Aspose.Cells for .NET का उपयोग करके Excel डेटा को DataTable में एक्सपोर्ट करें: एक पूर्ण गाइड](/cells/english/net/import-export/export-excel-data-datatatable-aspose-cells-net/)
- [Aspose.Cells for .NET का उपयोग करके Excel से HTML स्ट्रिंग्स को DataTable में एक्सपोर्ट करें: एक स्टेप‑बाय‑स्टेप गाइड](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}