---
category: general
date: 2026-08-11
description: C# में एक्सेल को txt में निर्यात करने के लिए चरण-दर-चरण मार्गदर्शिका।
  Aspose.Cells का उपयोग करके xlsx को साधारण टेक्स्ट में कैसे बदलें, सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: hi
lastmod: 2026-08-11
og_description: C# में एक्सेल को तेज़ी से txt में निर्यात करें। यह ट्यूटोरियल दिखाता
  है कि xlsx को साधारण टेक्स्ट में कैसे बदलें, फ़ॉर्मैट कॉन्फ़िगर करें, और बड़े वर्कशीट्स
  को कैसे संभालें।
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: C# में Excel को TXT में निर्यात करें – डेवलपर्स के लिए चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: C# में एक्सेल को TXT में निर्यात – पूर्ण प्रोग्रामिंग गाइड
url: /hi/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में एक्सेल को txt में निर्यात करें – पूर्ण प्रोग्रामिंग गाइड

यदि आपको **export excel to txt** करने की आवश्यकता है, तो आप कुछ ही पंक्तियों के C# कोड से परिणाम प्राप्त कर सकते हैं। यह गाइड दिखाता है कि कैसे `.xlsx` वर्कबुक को एक plain‑text फ़ाइल में परिवर्तित किया जाए जबकि आप द्वारा परिभाषित डेटा फ़ॉर्मेट को संरक्षित रखा जाए।

वर्कशीट को टेक्स्ट फ़ाइल के रूप में निर्यात करना एक सामान्य आवश्यकता है जब डाउनस्ट्रीम सिस्टम केवल डिलिमिटेड डेटा स्वीकार करते हैं या जब आपको कच्चे सेल मानों का ऑडिट करना होता है। अगले सेक्शनों में आप सीखेंगे कि तिथि और संख्या फ़ॉर्मेट कैसे कॉन्फ़िगर करें, बड़े शीट्स को कैसे संभालें, और सामान्य समस्याओं से कैसे बचें।

## xlsx को plain text में परिवर्तित करने के लिए आवश्यकताएँ

* .NET 6.0 (या बाद का) स्थापित हो – कोड .NET Standard 2.0 को टार्गेट करता है, इसलिए यह .NET Framework 4.6+ के साथ भी काम करता है।  
* **Aspose.Cells** का लाइसेंस (फ़्री इवैल्यूएशन परीक्षण के लिए काम करता है)।  
* Visual Studio 2022 या Visual Studio Code जैसा IDE।  
* `input.xlsx` नाम की एक Excel फ़ाइल जिसे आप अपने प्रोजेक्ट से रेफ़रेंस कर सकें, किसी फ़ोल्डर में रखी हुई हो।

ये आइटम केवल बाहरी आवश्यकताएँ हैं; ट्यूटोरियल अतिरिक्त NuGet पैकेजों पर निर्भर नहीं करता।

## Aspose.Cells का उपयोग करके excel को txt में निर्यात कैसे करें

Aspose.Cells `ExportTableOptions` क्लास प्रदान करता है जो आपको यह नियंत्रित करने देता है कि सेल मान स्ट्रिंग्स के रूप में कैसे रेंडर हों। `ExportAsString` को `true` सेट करके आप प्रत्येक सेल को टेक्स्ट के रूप में लिखने के लिए मजबूर करते हैं, जो एक निर्धारित plain‑text आउटपुट चाहते समय आवश्यक है।

### चरण 1 – वर्कबुक लोड करें

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*`Workbook` कंस्ट्रक्टर Excel फ़ाइल को मेमोरी में पढ़ता है। यदि फ़ाइल मौजूद नहीं है, तो एक एक्सेप्शन थ्रो होता है, इसलिए प्रोडक्शन कोड में आप इस कॉल को try‑catch ब्लॉक में रैप करना चाहेंगे।*

### चरण 2 – पहली वर्कशीट प्राप्त करें

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*Worksheets शून्य‑आधारित होते हैं, इसलिए इंडेक्स 0 पहली टैब को दर्शाता है। जब आपको किसी विशिष्ट टैब को टार्गेट करना हो, तो आप इंडेक्स को शीट नाम (`workbook.Worksheets["Sheet1"]`) से बदल सकते हैं।*

### चरण 3 – टेक्स्ट रूपांतरण के लिए निर्यात विकल्प निर्धारित करें

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString` यह गारंटी देता है कि प्रत्येक सेल, चाहे उसका मूल प्रकार कुछ भी हो, आउटपुट फ़ाइल में स्ट्रिंग बन जाता है। `DateTimeFormat` और `NumberFormat` प्रॉपर्टीज़ आपको यह नियंत्रित करने देती हैं कि तिथियाँ और संख्याएँ कैसे दिखें, जो कि **convert xlsx to plain text** करने के समय उन सिस्टमों के लिए महत्वपूर्ण है जो विशिष्ट पैटर्न की अपेक्षा करते हैं।*

### चरण 4 – वर्कशीट को टेक्स्ट फ़ाइल के रूप में निर्यात करें

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable` आपके द्वारा प्रदान किए गए विकल्पों का उपयोग करके वर्कशीट सामग्री को एक plain‑text फ़ाइल में लिखता है। डिफ़ॉल्ट डिलिमिटर एक टैब कैरेक्टर (`\t`) है। यदि आपको अलग डिलिमिटर चाहिए, तो आप उस ओवरलोड का उपयोग कर सकते हैं जो `ExportTableOptions` इंस्टेंस को स्वीकार करता है और `ExportTableOptions.Separator` निर्दिष्ट करता है। परिणामी फ़ाइल को किसी भी टेक्स्ट एडिटर में खोला जा सकता है या डेटाबेस में इम्पोर्ट किया जा सकता है।*

#### अपेक्षित आउटपुट

मान लीजिए `input.xlsx` में यह है:

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Sample text|

उपरोक्त विकल्पों के साथ `Exported.txt` फ़ाइल में यह होगा:

```
2023-05-01	1,234.50	Sample text
```

प्रत्येक कॉलम टैब से अलग किया गया है, तिथियाँ `yyyy‑MM‑dd` फ़ॉर्मेट का पालन करती हैं, और संख्याएँ हज़ारों विभाजक के रूप में कॉमा तथा दो दशमलव स्थानों के साथ प्रदर्शित होती हैं।

## वर्कशीट को टेक्स्ट फ़ाइल के रूप में निर्यात करते समय सामान्य समस्याएँ

| समस्या | क्यों होता है | कैसे बचें |
|-------|----------------|-----------------|
| लोकेल‑निर्भर संख्या फ़ॉर्मेटिंग | डिफ़ॉल्ट फ़ॉर्मेट OS संस्कृति का सम्मान करता है, जिससे कॉमा या पीरियड असंगत रूप से उत्पन्न हो सकते हैं। | `ExportTableOptions` में स्पष्ट रूप से `NumberFormat` सेट करें। |
| छिपी हुई पंक्तियाँ या कॉलम आउटपुट में दिखाई देते हैं | Aspose.Cells पूरी उपयोग की गई रेंज को निर्यात करता है, जिसमें छिपी हुई पंक्तियाँ भी शामिल हैं। | यदि आप उन्हें छोड़ना चाहते हैं तो `ExportTableOptions.ExportHiddenRows = false` और `ExportHiddenColumns = false` सेट करें। |
| बड़े वर्कशीट्स मेमोरी पर दबाव डालते हैं | निर्यात से पहले पूरी वर्कबुक मेमोरी में लोड होती है। | मेमोरी उपयोग कम करने के लिए `Workbook.LoadOptions` के साथ `LoadDataOnly = true` उपयोग करें, या फ़ाइल को भागों में प्रोसेस करें। |
| स्रोत फ़ाइल में तिथि सेल्स टेक्स्ट के रूप में संग्रहीत हैं | यदि किसी सेल में पहले से ही फ़ॉर्मेटेड स्ट्रिंग है, तो एक्सपोर्टर इसे टेक्स्ट मानता है और `DateTimeFormat` को अनदेखा करता है। | सुनिश्चित करें कि स्रोत वर्कबुक तिथियों को उचित Excel तिथि प्रकारों के रूप में संग्रहीत करे। |

इन समस्याओं को हल करने से **how to export excel worksheet as text** प्रक्रिया विभिन्न वातावरणों में विश्वसनीय बनती है।

## समाधान का विस्तार – कस्टम डिलिमिटर और स्ट्रीमिंग निर्यात

यदि आपको टैब‑डिलिमिटेड फ़ाइल के बजाय कॉमा‑सेपरेटेड वैल्यूज़ (CSV) फ़ाइल चाहिए, तो विकल्पों को इस प्रकार संशोधित करें:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

500 MB से बड़ी फ़ाइलों के लिए, स्ट्रीमिंग आउटपुट एप्लिकेशन को RAM समाप्त होने से बचाता है:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

`Stream` को स्वीकार करने वाला ओवरलोड पंक्तियों को क्रमिक रूप से लिखता है, जो बैच जॉब्स या वेब सर्विसेज़ के लिए आदर्श है जो टेक्स्ट फ़ाइल को सीधे क्लाइंट को रिटर्न करती हैं।

## प्रोग्रामेटिक रूप से परिणाम सत्यापित करें

निर्यात समाप्त होने के बाद आप पहले लाइन को मेमोरी में वापस पढ़ सकते हैं ताकि फ़ॉर्मेट की पुष्टि हो सके:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

इस स्निपेट को चलाने पर *अपेक्षित आउटपुट* सेक्शन में दिखी हुई वही लाइन प्रिंट होनी चाहिए, जिससे आपको यह भरोसा होगा कि रूपांतरण सफल रहा।

## संपूर्ण कोड का सारांश

सभी हिस्सों को मिलाकर एक स्व-निहित प्रोग्राम बनता है जिसे आप कंसोल एप्लिकेशन में कॉपी कर सकते हैं:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

प्रोग्राम को कंपाइल और रन करें; `Exported.txt` फ़ाइल स्रोत वर्कबुक के समान डायरेक्टरी में दिखाई देगी।

## अगले कदम और संबंधित विषय

* **Export worksheet as text file** – विभिन्न डिलिमिटर, एन्कोडिंग (UTF‑8 बनाम ASCII), और लाइन‑एंडिंग स्टाइल्स के साथ प्रयोग करें ताकि क्रॉस‑प्लेटफ़ॉर्म संगतता सुनिश्चित हो सके।  
* **Bulk conversion** – `workbook.Worksheets` पर लूप लगाकर प्रत्येक टैब के लिए अलग टेक्स्ट फ़ाइल जनरेट करें।  
* **Integration with databases** – जनरेट किए गए टेक्स्ट को सीधे SQL Server या PostgreSQL के लिए बल्क‑इन्सर्ट ऑपरेशन में पाइप करें।  
* **

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकटतम संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Aspose.Cells का उपयोग करके .NET में Excel फ़ाइलें निर्यात करने का व्यापक गाइड](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Aspose.Cells for .NET के साथ दृश्यमान Excel पंक्तियों को निर्यात करने का चरण‑दर‑चरण गाइड](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Aspose.Cells for .NET के साथ Excel चार्ट्स को PDF में निर्यात करने का चरण‑दर‑चरण गाइड](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}