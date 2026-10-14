---
category: general
date: 2026-10-13
description: Aspose.Cells के साथ Excel को TXT के रूप में सहेजना सीखें। यह गाइड कुछ
  ही चरणों में Excel को TXT में निर्यात करना, सेल में मान लिखना, और महत्वपूर्ण अंकों
  को सेट करना कवर करता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as txt
- export excel to txt
- write value to cell
- set significant digits
- export spreadsheet as txt
language: hi
lastmod: 2026-10-13
og_description: Aspose.Cells के साथ Excel को TXT के रूप में सहेजें। सीखें कि कैसे
  Excel को TXT में निर्यात करें, सेल में मान लिखें, और केवल कुछ ही C# कोड लाइनों में
  महत्वपूर्ण अंकों को सेट करें।
og_image_alt: Screenshot showing a workbook saved as a TXT file using save excel as
  txt
og_title: Excel को TXT के रूप में सहेजें – .NET डेवलपर्स के लिए चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Learn how to save Excel as TXT with Aspose.Cells. This guide covers
    export Excel to TXT, write value to cell, and set significant digits in just a
    few steps.
  headline: How to save Excel as TXT using Aspose.Cells in C#
  type: TechArticle
- questions:
  - answer: It rounds to the nearest value based on the specified number of significant
      digits, ensuring the output is mathematically accurate to that precision.
    question: Does `SignificantDigits` round or truncate?
  - answer: 'Yes. Replace the file path with a `MemoryStream` instance: `workbook.Save(stream,
      txtOptions);`. This is handy for web APIs that need to return the TXT content
      without touching the file system.'
    question: Can I export directly to a memory stream?
  - answer: 'Use `txtOptions.ExportFormattedValues = true`. This forces Aspose.Cells
      to write the cell’s displayed text rather than the raw value. ## Conclusion
      You now know how to **save Excel as TXT** with full control over precision,
      formatting, and output location. By following the four steps—create a workbo'
    question: What if I need to keep the original formatting (e.g., dates)?
  type: FAQPage
tags:
- Excel
- TXT
- Aspose.Cells
- .NET
title: Aspose.Cells का उपयोग करके C# में Excel को TXT के रूप में कैसे सहेजें
url: /hi/net/converting-excel-files-to-other-formats/how-to-save-excel-as-txt-using-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to save Excel as TXT using Aspose.Cells in C#

यदि आपको **Excel को TXT के रूप में सहेजना** जल्दी से करना है, तो यह ट्यूटोरियल पाँच मिनट से कम समय में पूरी प्रक्रिया दिखाता है। आप देखेंगे कि Excel को TXT में कैसे एक्सपोर्ट करें, सेल में वैल्यू कैसे लिखें, और सिग्निफिकेंट डिजिट्स कैसे सेट करें ताकि टेक्स्ट फ़ाइल में ठीक वही डेटा हो जो आप चाहते हैं।

स्प्रेडशीट को TXT के रूप में एक्सपोर्ट करना उपयोगी होता है जब डाउनस्ट्रीम सिस्टम केवल प्लेन‑टेक्स्ट इनपुट स्वीकार करते हैं, जब आपको लॉग जनरेट करने होते हैं, या जब आप गणनाओं का मानव‑पठनीय डंप चाहते हैं। नीचे दिया गया उदाहरण Aspose.Cells v25.10 या बाद के संस्करण के साथ काम करता है और किसी भी .NET 6+ रनटाइम पर चलता है।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* **Aspose.Cells for .NET** की लाइसेंस्ड कॉपी (टेस्टिंग के लिए फ्री ट्रायल चलती है)।
* .NET 6 SDK या बाद का संस्करण इंस्टॉल हो।
* Visual Studio 2022, VS Code, या Rider जैसा IDE।
* बेसिक C# ज्ञान—उन्नत Excel ऑटोमेशन का अनुभव आवश्यक नहीं।

आप Aspose.Cells NuGet पैकेज को इस तरह इंस्टॉल कर सकते हैं:

```bash
dotnet add package Aspose.Cells
```

## Step 1: Create a workbook and access its first worksheet (save excel as txt)

जब आप **Excel को TXT के रूप में सहेजना** चाहते हैं, तो सबसे पहले एक `Workbook` ऑब्जेक्ट बनाते हैं। यह ऑब्जेक्ट मेमोरी में पूरी Excel फ़ाइल का प्रतिनिधित्व करता है।

```csharp
using Aspose.Cells;

// Create a new workbook (an empty Excel file)
Workbook workbook = new Workbook();

// Access the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

> **Why this matters:** `Workbook` क्लास सभी स्प्रेडशीट ऑपरेशन्स का एंट्री पॉइंट है। एक नई वर्कबुक से शुरू करके आप किसी भी छिपे फॉर्मेटिंग से बचते हैं जो प्लेन‑टेक्स्ट आउटपुट को प्रभावित कर सकती है।

## Step 2: Write a high‑precision number into a cell (write value to cell)

अब आपको **write value to cell** A1 करना है। `PutValue` मेथड डेटा टाइप को ऑटोमैटिकली डिटेक्ट करता है और उसे न्यूमेरिक वैल्यू के रूप में स्टोर करता है।

```csharp
// Write a high‑precision number into cell A1
worksheet.Cells["A1"].PutValue(12345.6789012345);
```

> **Tip:** बाद में यदि आपको स्ट्रिंग, डेट या फ़ॉर्मूला लिखने की ज़रूरत पड़े, तो वही `PutValue` मेथड काम करेगा—सिर्फ उचित .NET टाइप पास करें।

## Step 3: Configure the export options to keep only the needed precision (set significant digits)

TXT फ़ाइल में एक्सपोर्ट करते समय अक्सर आप डिजिट्स की संख्या सीमित करना चाहते हैं ताकि फ़ाइल साइज छोटा रहे या किसी डाउनस्ट्रीम स्पेसिफिकेशन से मेल खाए। `TxtSaveOptions` क्लास इस उद्देश्य के लिए `SignificantDigits` प्रॉपर्टी प्रदान करती है।

```csharp
// Configure TXT save options to retain only 6 significant digits
TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
{
    SignificantDigits = 6   // New option in v25.10
};
```

> **Why you should set significant digits:** इस सेटिंग के बिना, Aspose.Cells पूरी डबल‑प्रिसिशन वैल्यू लिखता है, जिससे `12345.6789012345` जैसी लंबी स्ट्रिंग बन सकती है। `SignificantDigits = 6` सेट करने से आउटपुट `12345.7` तक सीमित हो जाता है, जो अधिकांश रिपोर्टिंग आवश्यकताओं को पूरा करता है।

## Step 4: Export the workbook as a TXT file (export excel to txt)

अंत में, आप **export Excel to TXT** `Workbook.Save` को पहले कॉन्फ़िगर किए गए ऑप्शन्स के साथ कॉल करके करते हैं।

```csharp
// Save the workbook as a TXT file using the configured options
string outputPath = @"C:\Temp\LimitedDigits.txt";
workbook.Save(outputPath, txtSaveOptions);
```

जब कोड समाप्त हो जाता है, `LimitedDigits.txt` में यह होगा:

```
12345.7
```

> **Result verification:** फ़ाइल को किसी भी टेक्स्ट एडिटर (Notepad, VS Code) में खोलें और पुष्टि करें कि केवल छह सिग्निफिकेंट डिजिट्स मौजूद हैं और कोई अतिरिक्त कॉमा या टैब डिलिमिटर नहीं है।

## Full, runnable example

नीचे एक सेल्फ‑कंटेन्ड कंसोल एप्लिकेशन दिया गया है जिसे आप कॉपी‑पेस्ट करके तुरंत चला सकते हैं।

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // 2️⃣ Write a high‑precision number to cell A1
            worksheet.Cells["A1"].PutValue(12345.6789012345);

            // 3️⃣ Set up TXT save options with 6 significant digits
            TxtSaveOptions txtOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                SignificantDigits = 6
            };

            // 4️⃣ Save as TXT
            string path = @"C:\Temp\LimitedDigits.txt";
            workbook.Save(path, txtOptions);

            Console.WriteLine($"Workbook exported to TXT at: {path}");
        }
    }
}
```

**Explanation of each block**

| Block | Purpose |
|-------|---------|
| `using Aspose.Cells;` | `Workbook`, `Worksheet`, और `TxtSaveOptions` के लिए आवश्यक Aspose.Cells नेमस्पेस इम्पोर्ट करता है। |
| `Workbook workbook = new Workbook();` | मेमोरी में एक खाली Excel वर्कबुक इंस्टैंशिएट करता है। |
| `worksheet.Cells["A1"].PutValue(...);` | **write value to cell** A1 में डबल‑प्रिसिशन नंबर लिखता है। |
| `TxtSaveOptions` | **set significant digits** व्यवहार को कॉन्फ़िगर करता है TXT एक्सपोर्ट के लिए। |
| `workbook.Save(..., txtOptions);` | **export excel to txt** ऑपरेशन को एग्जीक्यूट करता है, जिससे प्लेन‑टेक्स्ट फ़ाइल बनती है। |

## Edge cases and additional tips

| Scenario | How to handle |
|----------|---------------|
| **Large worksheets** (many rows/columns) | यदि Unicode सपोर्ट चाहिए तो `txtOptions.Encoding = Encoding.UTF8` सेट करें, और मेमोरी उपयोग कम रखने के लिए `Workbook.Save(Stream, txtOptions)` के साथ स्ट्रीमिंग पर विचार करें। |
| **Custom delimiters** (comma‑separated values) | `TxtSaveOptions` में `Separator` प्रॉपर्टी भी होती है—इसे `','` पर सेट करें ताकि TXT फॉर्मेट में CSV‑स्टाइल आउटपुट मिल सके। |
| **Preserving formulas** | `txtOptions.ExportFormulas = true` सेट करें ताकि फ़ॉर्मूला टेक्स्ट लिखा जाए, न कि कैलकुलेटेड वैल्यू। |
| **Locale‑specific decimal separators** | यूरोपीय लोकेल के लिए `txtOptions.DecimalSeparator` को `','` पर बदलें। |
| **Multiple worksheets** | `workbook.Worksheets` पर लूप चलाएँ और प्रत्येक के लिए `Save` कॉल करें, फ़ाइल नाम में वर्कशीट का नाम जोड़ें। |

## Frequently asked questions

**Q: Does `SignificantDigits` round or truncate?**  
A: यह निर्दिष्ट सिग्निफिकेंट डिजिट्स की संख्या के आधार पर निकटतम वैल्यू पर राउंड करता है, जिससे आउटपुट गणितीय रूप से उस प्रिसीजन तक सटीक रहता है।

**Q: Can I export directly to a memory stream?**  
A: हाँ। फ़ाइल पाथ को `MemoryStream` इंस्टेंस से बदलें: `workbook.Save(stream, txtOptions);`। यह वेब API के लिए उपयोगी है जो फ़ाइल सिस्टम को छुए बिना TXT कंटेंट रिटर्न करना चाहते हैं।

**Q: What if I need to keep the original formatting (e.g., dates)?**  
A: `txtOptions.ExportFormattedValues = true` इस्तेमाल करें। यह Aspose.Cells को सेल के डिस्प्ले किए गए टेक्स्ट को रॉ वैल्यू की बजाय लिखने के लिए मजबूर करता है।

## Conclusion

अब आप **Excel को TXT के रूप में सहेजना** पूरी प्रिसीजन, फॉर्मेटिंग और आउटपुट लोकेशन कंट्रोल के साथ कर सकते हैं। चार चरणों—वर्कबुक बनाना, **write value to cell**, **set significant digits**, और **export Excel to TXT**—को फॉलो करके आप किसी भी .NET एप्लिकेशन में प्लेन‑टेक्स्ट एक्सपोर्ट को इंटीग्रेट कर सकते हैं।

अगले चरण में, **custom delimiters के साथ एक्सपोर्ट स्प्रेडशीट as TXT**, **Excel को CSV में कन्वर्ट करना**, या **Aspose.Cells से JSON रिपोर्ट जनरेट करना** जैसे संबंधित टॉपिक एक्सप्लोर करें। ये सभी यहाँ दिखाए गए कोर कॉन्सेप्ट्स पर आधारित हैं, जिससे आप विभिन्न प्लेटफ़ॉर्म्स के बीच डेटा इंटरचेंज के लिए एक बहुमुखी टूलकिट प्राप्त करेंगे।

Happy coding!

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और स्टेप‑बाय‑स्टेप एक्सप्लानेशन शामिल है, जिससे आप अतिरिक्त API फीचर्स को मास्टर कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Save Excel as Text – Complete C# Guide to Export Excel to TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Create New Workbook and Export Excel to TXT with Precision](/cells/english/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/)
- [Create new workbook – Export Excel to TXT with Full Precision](/cells/english/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}