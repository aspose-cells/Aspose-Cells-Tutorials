---
category: general
date: 2026-11-19
description: ऐरे डेटा के साथ एक्सेल को भरते समय वर्कशीट को दोहराने का तरीका। कुछ चरणों
  में कई वर्कशीट बनाना और सूची से वर्कशीट को भरना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to repeat worksheet
- populate excel with array
- generate multiple worksheets
- populate worksheet from list
language: hi
lastmod: 2026-11-19
og_description: SmartMarkerProcessor का उपयोग करके वर्कशीट को दोहराने का तरीका। इस
  गाइड का पालन करके एरे डेटा के साथ एक्सेल को भरें, कई वर्कशीट बनाएं, और सूची से वर्कशीट
  को भरें।
og_image_alt: Screenshot showing repeated worksheets in an Excel workbook after processing
og_title: Excel में वर्कशीट को दोहराने का तरीका – चरण-दर-चरण गाइड
schemas:
- author: GroupDocs
  dateModified: '2026-11-19'
  description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  headline: How to repeat worksheet in Excel with SmartMarkerProcessor
  type: TechArticle
- description: How to repeat worksheet while populating Excel with array data. Learn
    to generate multiple worksheets and populate worksheet from list in a few steps.
  name: How to repeat worksheet in Excel with SmartMarkerProcessor
  steps:
  - name: Expected output
    text: 'When you open the resulting workbook, you should see:'
  - name: Empty or null arrays
    text: 'If `Dept` is null or empty, the processor will not create any additional
      worksheets. To avoid a completely blank workbook, you can add a guard:'
  - name: Custom worksheet names
    text: 'The default naming scheme may not suit every reporting requirement. After
      processing, rename each sheet using a loop:'
  - name: Populating additional columns
    text: 'If you need to **populate excel with array** values beyond a single marker,
      extend the data object:'
  type: HowTo
tags:
- Excel automation
- SmartMarkerProcessor
- .NET
title: SmartMarkerProcessor के साथ Excel में वर्कशीट को दोहराने का तरीका
url: /hi/net/smart-markers-dynamic-data/how-to-repeat-worksheet-in-excel-with-smartmarkerprocessor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SmartMarkerProcessor के साथ Excel में वर्कशीट को दोहराने का तरीका

यदि आपको Excel रिपोर्ट बनाते समय **how to repeat worksheet** की आवश्यकता है, तो यह गाइड आपको एक पूर्ण, चलाने योग्य समाधान दिखाता है। ट्यूटोरियल के अंत तक आप SmartMarkerProcessor लाइब्रेरी का उपयोग करके **populate Excel with array** डेटा, **generate multiple worksheets**, और **populate worksheet from list** कर पाएँगे।

एक वर्कशीट को दोहराना आम आवश्यकता है जब प्रत्येक विभाग, क्षेत्र, या समय अवधि को अपना टैब चाहिए होता है। नीचे दिया गया उदाहरण सटीक चरणों को दर्शाता है, बताता है कि प्रत्येक सेटिंग क्यों महत्वपूर्ण है, और खाली सूचियों या कस्टम नामकरण जैसे एज केस को कवर करता है।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- .NET 6.0 या बाद का संस्करण स्थापित
- **GroupDocs.Viewer** (या समतुल्य) NuGet पैकेज का रेफ़रेंस जिसमें `SmartMarkerProcessor` शामिल है
- एक Excel टेम्पलेट वर्कबुक (`.xlsx`) जिसमें `${repeat:Dept}` जैसे मार्कर को उस पंक्ति में रखा गया हो जिसे आप दोहराना चाहते हैं
- C# और LINQ की बुनियादी जानकारी (वैकल्पिक लेकिन सहायक)

कोई अतिरिक्त थर्ड‑पार्टी लाइब्रेरी आवश्यक नहीं है।

## Step 1: Create the SmartMarkerProcessor instance

प्रोसेसर मार्कर प्रतिस्थापन और वर्कशीट डुप्लिकेशन को समन्वयित करता है। बिना आर्ग्यूमेंट के इंस्टैंसिएट करने से डिफ़ॉल्ट विकल्प उपयोग होते हैं।

```csharp
// Step 1: Create a SmartMarkerProcessor instance
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

प्रोसेसर को जल्दी बनाकर आप ग्लोबल विकल्पों को डेटा लागू होने से पहले कॉन्फ़िगर कर सकते हैं। यह **how to repeat worksheet** को सही ढंग से करने की नींव है।

## Step 2: Enable worksheet repetition

डिफ़ॉल्ट रूप से प्रोसेसर केवल वर्तमान शीट पर मार्कर बदलता है। `RepeatWorksheet` को `true` सेट करने से इंजन डेटा कलेक्शन के प्रत्येक आइटम के लिए पूरी वर्कशीट को क्लोन करता है।

```csharp
// Step 2: Enable worksheet repetition for the ${repeat:Dept} marker
processor.Options.RepeatWorksheet = true;
```

इस विकल्प को सक्षम करना **generate multiple worksheets** का मुख्य कुंजी है—प्रोसेसर `Dept` एरे के प्रत्येक तत्व के लिए एक नया टैब बनाएगा और मूल फ़ॉर्मेटिंग को बरकरार रखेगा।

## Step 3: Prepare the data source as an array or list

SmartMarkerProcessor किसी भी enumerable के साथ काम करता है, लेकिन एरे का उपयोग करने से इरादा स्पष्ट हो जाता है जब आप **populate worksheet from list** करना चाहते हैं। यहाँ हम एक अनाम ऑब्जेक्ट बनाते हैं जिसमें `Dept` प्रॉपर्टी एक स्ट्रिंग एरे रखती है।

```csharp
// Step 3: Prepare the data source with a list of departments
var data = new { Dept = new[] { "HR", "IT", "Finance" } };
```

यदि आपके पास पहले से ही `List<string>` है तो आप उसे सीधे पास कर सकते हैं; प्रोसेसर इसे उसी तरह ट्रीट करेगा। महत्वपूर्ण बात यह है कि प्रॉपर्टी नाम (`Dept`) टेम्पलेट में `${repeat:Dept}` मार्कर से मेल खाता हो।

## Step 4: Load the template worksheet

मान लीजिए आपके पास `ExcelPackage` (EPPlus से) या `Workbook` ऑब्जेक्ट है, तो वह वर्कशीट प्राप्त करें जिसे आप दोहराना चाहते हैं। वेरिएबल `ws` उस शीट को दर्शाता है।

```csharp
// Example using EPPlus to load the template workbook
using var package = new OfficeOpenXml.ExcelPackage(new FileInfo("Template.xlsx"));
var ws = package.Workbook.Worksheets[0]; // first worksheet
```

यदि आप कोई अलग लाइब्रेरी (जैसे ClosedXML) पसंद करते हैं, तो वही सिद्धांत लागू होता है: आवश्यक इंटरफ़ेस को इम्प्लीमेंट करने वाला वर्कशीट ऑब्जेक्ट प्राप्त करें।

## Step 5: Process the worksheet with the data

अब डेटा को टेम्पलेट पर लागू करें। प्रोसेसर प्रत्येक विभाग के लिए वर्कशीट को क्लोन करता है, `${repeat:Dept}` मार्कर को वास्तविक विभाग नाम से बदलता है, और शीट के बाकी हिस्से को जैसा का तैसा छोड़ देता है।

```csharp
// Step 5: Apply the data to the template worksheet (ws)
processor.Process(ws, data);
```

`Process` पूरा होने के बाद, `ws` कई वर्कशीट्स में से पहली बन जाता है—प्रत्येक विभाग के लिए एक। मूल शीट का नाम बरकरार रहता है, जबकि डुप्लिकेट्स को क्रमिक सुफ़िक्स (जैसे “Sheet1 (1)”, “Sheet1 (2)”) मिलता है। यदि आप कस्टम नामकरण चाहते हैं तो बाद में उन्हें रीनेम कर सकते हैं।

### Expected output

जब आप परिणामी वर्कबुक खोलेंगे, तो आपको दिखना चाहिए:

- **Sheet1** – मूल टेम्पलेट (अक्सर खाली या मास्टर के रूप में उपयोग किया जाता है)
- **Sheet1 (1)** – “HR” से भरपूर
- **Sheet1 (2)** – “IT” से भरपूर
- **Sheet1 (3)** – “Finance” से भरपूर

प्रत्येक शीट में वही लेआउट होगा लेकिन जहाँ `${repeat:Dept}` आया था वहाँ विभाग नाम प्रतिस्थापित होगा।

## Handling edge cases

### Empty or null arrays

यदि `Dept` null या खाली है, तो प्रोसेसर कोई अतिरिक्त वर्कशीट नहीं बनाता। पूरी तरह खाली वर्कबुक से बचने के लिए आप एक गार्ड जोड़ सकते हैं:

```csharp
if (data.Dept != null && data.Dept.Any())
{
    processor.Process(ws, data);
}
else
{
    // Optionally write a warning or keep the original sheet unchanged
}
```

### Custom worksheet names

डिफ़ॉल्ट नामकरण योजना हर रिपोर्टिंग आवश्यकता के लिए उपयुक्त नहीं हो सकती। प्रोसेसिंग के बाद, लूप का उपयोग करके प्रत्येक शीट को रीनेम करें:

```csharp
for (int i = 1; i <= data.Dept.Length; i++)
{
    var sheet = package.Workbook.Worksheets[i]; // index 0 is the original
    sheet.Name = data.Dept[i - 1]; // use department name as tab title
}
```

### Populating additional columns

यदि आपको **populate excel with array** मानों को एकल मार्कर से आगे भरना है, तो डेटा ऑब्जेक्ट को विस्तारित करें:

```csharp
var data = new
{
    Dept = new[]
    {
        new { Name = "HR", Headcount = 12 },
        new { Name = "IT", Headcount = 25 },
        new { Name = "Finance", Headcount = 8 }
    }
};
```

फिर टेम्पलेट मार्करों को `${repeat:Dept.Name}` और `${repeat:Dept.Headcount}` में बदलें। प्रोसेसर प्रत्येक विभाग के लिए पंक्ति को दोहराएगा और दोनों कॉलम भर देगा।

## Full working example

नीचे एक स्व-निहित कंसोल एप्लिकेशन दिया गया है जो टेम्पलेट लोडिंग से लेकर अंतिम वर्कबुक सेव करने तक का पूरा फ्लो दर्शाता है।

```csharp
using System;
using System.IO;
using OfficeOpenXml;               // Install-Package EPPlus
using GroupDocs.Viewer.Markup;    // SmartMarkerProcessor namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Enable worksheet repetition
        processor.Options.RepeatWorksheet = true;

        // 3️⃣ Define data source (array of departments)
        var data = new { Dept = new[] { "HR", "IT", "Finance" } };

        // 4️⃣ Load template workbook (ensure Template.xlsx exists)
        var fileInfo = new FileInfo("Template.xlsx");
        using var package = new ExcelPackage(fileInfo);
        var ws = package.Workbook.Worksheets[0]; // first sheet contains ${repeat:Dept}

        // 5️⃣ Process template
        processor.Process(ws, data);

        // Optional: rename generated sheets
        for (int i = 1; i <= data.Dept.Length; i++)
        {
            var sheet = package.Workbook.Worksheets[i];
            sheet.Name = data.Dept[i - 1];
        }

        // Save the result
        var output = new FileInfo("Result.xlsx");
        package.SaveAs(output);

        Console.WriteLine("Workbook generated with repeated worksheets.");
    }
}
```

**Explanation of key sections**

- **Processor creation** – वह इंजन स्थापित करता है जो मार्करों की व्याख्या करेगा।
- **RepeatWorksheet option** – वह कोर फीचर सक्रिय करता है जो *how to repeat worksheet* का उत्तर देता है।
- **Data source** – एरे (`new[]`) का उपयोग करता है ताकि **populate excel with array** पूरा हो सके।
- **Template loading** – वर्कशीट ऑब्जेक्ट प्राप्त करने का सामान्य तरीका दर्शाता है।
- **Processing** – एक कॉल में डुप्लिकेशन और डेटा इन्सर्शन करता है।
- **Renaming** – दिखाता है कि सामान्य “(1)”, “(2)” नामों को अर्थपूर्ण शीर्षकों में कैसे बदला जाए, जो **generate multiple worksheets** के बाद अक्सर आवश्यक होता है।

इस प्रोग्राम को चलाने पर `Result.xlsx` तीन विभाग‑विशिष्ट टैब्स के साथ बनता है, प्रत्येक एरे से भरपूर।

## Common pitfalls and pro tips

- **Marker spelling** – मार्कर को प्रॉपर्टी नाम के साथ बिल्कुल मिलना चाहिए (`${repeat:Dept}`)। टाइपो दोहराव को रोक देगा।
- **Worksheet index** – प्रोसेसिंग के बाद, मूल शीट इंडेक्स 0 पर रहती है; जेनरेटेड शीट्स क्रमिक रूप से आती हैं। गलत इंडेक्सिंग से गलत टैब रीनेम हो सकता है।
- **Large data sets** – सैकड़ों वर्कशीट्स बनाना फ़ाइल साइज को बहुत बढ़ा सकता है। यदि परफ़ॉर्मेंस समस्या बनती है तो रिपोर्ट को विभाजित करने या एक ही शीट में ग्रुप्ड सेक्शन उपयोग करने पर विचार करें।
- **Thread safety** – `SmartMarkerProcessor` थ्रेड‑सेफ़ नहीं है। यदि आप कई वर्कबुक्स को समानांतर प्रोसेस कर रहे हैं तो प्रत्येक थ्रेड के लिए अलग इंस्टेंस बनाएँ।

## Conclusion

अब आप SmartMarkerProcessor का उपयोग करके Excel में **how to repeat worksheet**, **populate excel with array** डेटा, **generate multiple worksheets**, और **populate worksheet from list** को प्रभावी ढंग से कर सकते हैं। पूर्ण उदाहरण सभी अवधारणाओं को जोड़ता है, और वैकल्पिक रीनेमिंग स्टेप आपको साफ़, उपयोगकर्ता‑मैत्री टैब नाम बनाने की सुविधा देता है।

आगे आप खोज सकते हैं:

- जटिल ऑब्जेक्ट्स (नेस्टेड कलेक्शन) के साथ **populate worksheet from list** का उपयोग
- वर्कशीट डुप्लिकेशन के बाद कंडीशनल फ़ॉर्मेटिंग लागू करना
- उत्पन्न वर्कबुक को PDF या CSV में एक्सपोर्ट करना ताकि डाउनस्ट्रीम कंजम्प्शन हो सके

कोड को अपने रिपोर्टिंग परिदृश्यों के अनुसार अनुकूलित करें, और Excel वर्कबुक्स को ऑटोमेट करने का आनंद लें!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Repeat Worksheets – Complete Guide for Excel Automation](/cells/english/net/smart-markers-dynamic-data/how-to-repeat-worksheets-complete-guide-for-excel-automation/)
- [Create Worksheet Per Item – How to Repeat Worksheet in C#](/cells/english/net/worksheet-operations/create-worksheet-per-item-how-to-repeat-worksheet-in-c/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}