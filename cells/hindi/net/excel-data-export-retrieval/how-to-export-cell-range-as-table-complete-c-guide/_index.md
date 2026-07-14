---
category: general
date: 2026-07-13
description: C# और ExportTableOptions का उपयोग करके सेल रेंज को टेबल के रूप में निर्यात
  कैसे करें। चरण‑दर‑चरण वर्कबुक सेटअप, फॉर्मेटिंग और टेबल निर्यात सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export cell range as table
- ExportTableOptions usage
- Workbook and Worksheet handling
- cell value formatting C#
- scientific notation export
language: hi
lastmod: 2026-07-13
og_description: C# में ExportTableOptions के साथ सेल रेंज को टेबल के रूप में कैसे
  एक्सपोर्ट करें। इस गाइड का पालन करके सेल्स को फॉर्मेट करें, एक वर्कबुक बनाएं, और
  आसानी से टेबल एक्सपोर्ट करें।
og_image_alt: Diagram illustrating a C# code snippet that exports a single cell range
  as a formatted table
og_title: सेल रेंज को टेबल के रूप में निर्यात कैसे करें – पूर्ण C# मार्गदर्शन
schemas:
- author: Aspose
  dateModified: '2026-07-13'
  description: How to export cell range as table using C# and ExportTableOptions.
    Learn step‑by‑step workbook setup, formatting, and table export.
  headline: How to Export Cell Range as Table – Complete C# Guide
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel automation
- data export
title: सेल रेंज को टेबल के रूप में निर्यात कैसे करें – पूर्ण C# गाइड
url: /hi/net/excel-data-export-retrieval/how-to-export-cell-range-as-table-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# सेल रेंज को टेबल के रूप में एक्सपोर्ट कैसे करें – पूर्ण C# गाइड

क्या आपने कभी सोचा है **सेल रेंज को टेबल के रूप में एक्सपोर्ट कैसे करें** बिना फ़ॉर्मेटिंग की अजीबताओं से परेशान हुए? आप अकेले नहीं हैं। चाहे आप डेटा को रिपोर्टिंग पाइपलाइन में फीड कर रहे हों या सिर्फ एक तेज़ CSV‑स्टाइल डंप चाहिए, एक्सपोर्ट प्रक्रिया में महारत हासिल करने से आप मैन्युअल कॉपी‑पेस्टिंग में घंटों बचा सकते हैं।

इस ट्यूटोरियल में हम ठीक‑ठीक चरण‑दर‑चरण बताएँगे कि कैसे एक न्यूमेरिक सेल को वैज्ञानिक नोटेशन में बदलें और **ExportTableOptions** का उपयोग करके उसे टेबल के रूप में एक्सपोर्ट करें। अंत तक आपके पास एक रन‑एबल स्निपेट होगा, प्रत्येक कॉल के *क्यों* को समझेंगे, और बड़े रेंज या अलग फ़ॉर्मेट के लिए कोड को कैसे ट्यून करें, यह जानेंगे।

## आवश्यकताएँ

- .NET 6 या बाद का (API .NET Framework 4.7+ पर भी समान काम करता है)
- Aspose.Cells for .NET स्थापित (`Install-Package Aspose.Cells`)
- C# सिंटैक्स की बुनियादी समझ; Excel के गहरे इंटर्नल्स की आवश्यकता नहीं

ये सब हैं? बढ़िया—चलिए शुरू करते हैं।

## चरण 1: एक्सपोर्ट विकल्प सेट करें – कैसे सेल रेंज को टेबल के रूप में एक्सपोर्ट करें

पहले आपको एक **ExportTableOptions** इंस्टेंस चाहिए जो लाइब्रेरी को बताता है कि सेल कंटेंट को कैसे ट्रीट करना है। इसके बिना, एक्सपोर्ट डिफ़ॉल्ट रूप से रॉ न्यूमेरिक वैल्यू देता है, जो टेक्स्ट की उम्मीद करने वाले डाउनस्ट्रीम कंज्यूमर्स को तोड़ सकता है।

```csharp
// Step 1: Define export options – export the cell value as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Return the cell content as text
    CustomFormat = "0.00E+00"       // Apply scientific notation format
};
```

**यह क्यों महत्वपूर्ण है:**  
- `ExportAsString = true` लाइब्रेरी को सेल के प्रदर्शित टेक्स्ट को लिखने के लिए मजबूर करता है, न कि उसके अंडरलाइनिंग डबल को।  
- `CustomFormat` आपको **वैज्ञानिक नोटेशन एक्सपोर्ट** लागू करने देता है, जो बहुत बड़े या बहुत छोटे नंबरों के साथ काम करते समय उपयोगी है।

> **प्रो टिप:** यदि आपको डेट या करंसी फ़ॉर्मेट चाहिए, तो `"0.00E+00"` को क्रमशः `"yyyy‑MM‑dd"` या `"$#,##0.00"` से बदलें।

## चरण 2: एक वर्कबुक बनाएं और पहला वर्कशीट प्राप्त करें – वर्कबुक और वर्कशीट हैंडलिंग

एक **Workbook** पूरे Excel फ़ाइल का प्रतिनिधित्व करता है, जबकि एक **Worksheet** एकल टैब होता है। सरल एक्सपोर्ट के लिए हम पहले शीट (इंडेक्स 0) का उपयोग करेंगे।

```csharp
// Step 2: Create a new workbook and access the first worksheet
Workbook workbook = new Workbook();
Worksheet sheet = workbook.Worksheets[0];
```

**यह क्यों महत्वपूर्ण है:**  
एक नया `Workbook` बनाना एक साफ़ स्लेट सुनिश्चित करता है—कोई छिपी हुई स्टाइल या बचा हुआ डेटा नहीं जो आपको उलझा दे। `Worksheets[0]` तक पहुंचना सक्रिय शीट को जल्दी से प्राप्त करने का सबसे तेज़ तरीका है, बिना शीट नामों की चिंता किए।

## चरण 3: लक्ष्य सेल को भरें – सेल वैल्यू फ़ॉर्मेटिंग C#

अब हम सेल **A1** (पंक्ति 0, कॉलम 0) में एक न्यूमेरिक वैल्यू डालते हैं। हम जो वैल्यू चुनते हैं वह जानबूझकर लंबा‑डेसिमल है ताकि आप वैज्ञानिक नोटेशन को क्रिया में देख सकें।

```csharp
// Step 3: Insert a numeric value into cell A1 (row 0, column 0)
sheet.Cells[0, 0].PutValue(12345.6789);
```

**यह क्यों महत्वपूर्ण है:**  
`PutValue` कॉल स्वचालित रूप से सेल का डेटा टाइप निर्धारित करता है। क्योंकि हम बाद में स्ट्रिंग के रूप में एक्सपोर्ट करेंगे, रॉ डबल को पहले सेट किए गए फ़ॉर्मेट के अनुसार बदल दिया जाएगा, जिससे हमें एक साफ़ `"1.23E+04"` आउटपुट मिलता है।

## चरण 4: परिभाषित सेल रेंज को टेबल के रूप में एक्सपोर्ट करें – सेल रेंज को टेबल के रूप में एक्सपोर्ट करना

विकल्प और डेटा तैयार होने के बाद, अंतिम चरण है Aspose.Cells को रेंज लिखने को कहना। `ExportTable` मेथड को स्टार्ट रो/कॉलम, रेंज का आकार, और हमने बनाया हुआ विकल्प ऑब्जेक्ट चाहिए।

```csharp
// Step 4: Export the defined cell range as a table using the options above
// Parameters: startRow, startColumn, totalRows, totalColumns, options
sheet.ExportTable(0, 0, 1, 1, exportOptions);
```

**यह क्यों महत्वपूर्ण है:**  
- `totalRows = 1` और `totalColumns = 1` एक्सपोर्ट को केवल एक सेल तक सीमित करते हैं, लेकिन आप इन संख्याओं को बढ़ाकर बड़े ब्लॉक्स (जैसे `5, 3` 5‑रो × 3‑कॉलम रेंज) को कवर कर सकते हैं।  
- यह मेथड डेटा को एक इंटरनल टेबल स्ट्रक्चर में लिखता है जिसे CSV, HTML, या सीधे क्लाइंट को स्ट्रीम किया जा सकता है।

### परिणाम सहेजना (वैकल्पिक)

यदि आप एक्सपोर्टेड टेबल को डिस्क पर सहेजना चाहते हैं, तो इसे CSV फ़ाइल में लिख सकते हैं:

```csharp
// Optional: Save the exported table as CSV for verification
using (var stream = new MemoryStream())
{
    sheet.ExportTableToCSV(stream, exportOptions);
    File.WriteAllBytes("ExportedTable.csv", stream.ToArray());
}
```

ऊपर वाला कोड चलाने से एक फ़ाइल बनेगी जिसमें होगा:

```
1.23E+04
```

## किनारे के केस और सामान्य विविधताएँ

| स्थिति | क्या बदलें | कारण |
|-----------|----------------|--------|
| **एकाधिक पंक्तियों को एक्सपोर्ट करना** | `totalRows` को समायोजित करें और आवश्यक होने पर पंक्तियों पर लूप लगाएँ | `ExportTable` को बार‑बार कॉल किए बिना बैच एक्सपोर्ट की अनुमति देता है |
| **फ़ॉर्मूले को संरक्षित रखना** | `ExportAsString = false` सेट करें | प्रदर्शित वैल्यू के बजाय मूल फ़ॉर्मूला को रखता है |
| **विभिन्न डिलिमिटर** | `ExportTableToCSV(..., ',', ...)` ओवरलोड का उपयोग करें | कॉमा‑सेपरेटेड से टैब‑सेपरेटेड या पाइप‑सेपरेटेड वैल्यूज़ में स्विच करता है |
| **बड़ी वर्कशीट्स** | मेमोरी ओवरफ़्लो से बचने के लिए स्ट्रीम एक्सपोर्ट करें | >10 000 पंक्तियों के लिए अच्छा काम करता है |

## पूर्ण कार्यशील उदाहरण

नीचे पूरा, कॉपी‑एंड‑पेस्ट‑रेडी प्रोग्राम दिया गया है। यह किसी भी .NET कंसोल प्रोजेक्ट में काम करता है जो Aspose.Cells को रेफ़रेंस करता है।

```csharp
using System;
using System.IO;
using Aspose.Cells;

class ExportCellRangeDemo
{
    static void Main()
    {
        // 1️⃣ Define export options – how to export cell range as table
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            CustomFormat = "0.00E+00"
        };

        // 2️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Put a numeric value into A1
        sheet.Cells[0, 0].PutValue(12345.6789);

        // 4️⃣ Export the single‑cell range as a table
        sheet.ExportTable(0, 0, 1, 1, exportOptions);

        // Optional: write to CSV to see the result
        using (var ms = new MemoryStream())
        {
            sheet.ExportTableToCSV(ms, exportOptions);
            File.WriteAllBytes("ExportedTable.csv", ms.ToArray());
        }

        Console.WriteLine("Export complete! Check ExportedTable.csv");
    }
}
```

**अपेक्षित आउटपुट:**  
`ExportedTable.csv` नाम की फ़ाइल जिसमें एक ही लाइन होगी:

```
1.23E+04
```

यदि आप CSV को टेक्स्ट एडिटर में खोलेंगे तो आपको वैज्ञानिक नोटेशन ठीक उसी तरह लागू हुआ दिखेगा जैसा परिभाषित किया गया था।

## निष्कर्ष

हमने **सेल रेंज को टेबल के रूप में एक्सपोर्ट कैसे करें** को शुरू से अंत तक कवर किया: `ExportTableOptions` सेट करना, `Workbook` बनाना, डेटा डालना, और अंत में `ExportTable` को कॉल करना। प्रत्येक भाग को समझकर आप अब इस दृष्टिकोण को बड़े रेंज, अलग फ़ॉर्मेट, या यहां तक कि वेब API में इंटीग्रेट कर सकते हैं जो Excel‑डेरिव्ड डेटा को रीयल‑टाइम सर्व करता है।

आगे देखते हुए, आप निम्नलिखित को एक्सप्लोर कर सकते हैं:

- **ExportTableToHTML** वेब‑रेडी प्रीव्यूज़ के लिए  
- **ExportTableToDataTable** सीधे ADO.NET पाइपलाइन में फीड करने के लिए  
- डेट, करंसी, या प्रतिशत के लिए उन्नत **कस्टम फ़ॉर्मेट्स**  

इनको आज़माएँ, और आप एक साधारण सेल एक्सपोर्ट को एक बहुमुखी डेटा‑डिलीवरी इंजन में बदल देंगे। कोई प्रश्न या अजीब केस है? नीचे कमेंट करें—हैप्पी कोडिंग!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Aspose.Cells for .NET का उपयोग करके दृश्यमान Excel पंक्तियों को एक्सपोर्ट कैसे करें: एक चरण‑दर‑चरण गाइड](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Aspose.Cells का उपयोग करके .NET में Excel फ़ाइलें एक्सपोर्ट कैसे करें: एक व्यापक गाइड](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Aspose.Cells for .NET का उपयोग करके नाम द्वारा Excel सेल तक पहुंच कैसे करें: एक चरण‑दर‑चरण गाइड](/cells/english/net/cell-operations/access-cell-by-name-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}