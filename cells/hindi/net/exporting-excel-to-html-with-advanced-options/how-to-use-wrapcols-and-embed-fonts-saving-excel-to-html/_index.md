---
category: general
date: 2026-10-20
description: Aspose.Cells में wrapcols का उपयोग कैसे करें, HTML में फ़ॉन्ट एम्बेड
  करें, और पूर्ण C# उदाहरण के साथ Excel को HTML के रूप में सहेजना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: hi
lastmod: 2026-10-20
og_description: Aspose.Cells में wrapcols का उपयोग कैसे करें, HTML में फ़ॉन्ट एम्बेड
  करें, और डेवलपर्स के लिए स्पष्ट C# वॉकथ्रू के साथ वर्कबुक को HTML में परिवर्तित
  करें।
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Excel को HTML में निर्यात करते समय wrapcols का उपयोग और फ़ॉन्ट एम्बेड कैसे
  करें
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Excel को HTML में सहेजते समय wrapcols का उपयोग और फ़ॉन्ट एम्बेड कैसे करें
url: /hi/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# wrapcols का उपयोग और फ़ॉन्ट एम्बेड करके Excel को HTML में सहेजना

यदि आपको Aspose.Cells फ़ॉर्मूला में **wrapcols का उपयोग कैसे करें** की आवश्यकता है, तो यह गाइड आपको सटीक चरण दिखाता है। आप यह भी सीखेंगे कि **HTML में फ़ॉन्ट कैसे एम्बेड करें** और **Excel को HTML के रूप में सहेजें** ताकि आउटपुट सभी ब्राउज़रों में समान दिखे।  

यह ट्यूटोरियल तीन व्यावहारिक परिदृश्यों को कवर करता है: `WRAPCOLS` फ़ंक्शन का उपयोग, एम्बेडेड फ़ॉन्ट्स के साथ वर्कबुक निर्यात करना, और Smart Markers के साथ मास्टर‑डिटेल रिपोर्ट बनाना। अंत में आपके पास एक एकल, चलाने योग्य C# प्रोग्राम होगा जो इन सभी सुविधाओं को दर्शाता है।

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास:

* .NET 6.0 (या बाद का) स्थापित हो।
* Aspose.Cells for .NET को अपने प्रोजेक्ट में जोड़ें (`dotnet add package Aspose.Cells`)।
* C# और Excel फ़ॉर्मूले की बुनियादी समझ।

कोई अतिरिक्त थर्ड‑पार्टी लाइब्रेरी आवश्यक नहीं है; Aspose.Cells आंतरिक रूप से HTML रूपांतरण और फ़ॉन्ट एम्बेडिंग को संभालता है।

## चरण 1: फ़ॉर्मूला में **wrapcols का उपयोग कैसे करें** फ़ंक्शन को प्रदर्शित करें

`WRAPCOLS` फ़ंक्शन एक-आयामी रेंज को दो‑आयामी एरे में विभाजित करता है, पहले कॉलम भरते हुए। यह तब उपयोगी होता है जब आपको रिपोर्टिंग या चार्टिंग के लिए डेटा को पुनः आकार देना हो।

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**यह क्यों काम करता है:**  
`WRAPCOLS` दो तर्क लेता है – स्रोत रेंज और कॉलमों की संख्या। फ़ंक्शन एरे को कॉलम‑वार भरता है, अतिरिक्त मानों को छोड़ देता है (उदाहरण में `3`)। परिणाम लक्ष्य रेंज (`B1`) की ऊपर‑बाएँ सेल में दिखाई देता है, और यदि आपको पूरा एरे चाहिए तो आप रेंज को मैन्युअली विस्तारित कर सकते हैं।

> **प्रो टिप:** फ़ॉर्मूला सेट करने के बाद, `workbook.CalculateFormula()` को कॉल करें ताकि सेल मान पढ़ने से पहले परिणाम अद्यतित हो।

## चरण 2: **वर्कबुक को HTML में बदलें** और **HTML में फ़ॉन्ट एम्बेड करें**

जब आप Excel फ़ाइल को HTML में निर्यात करते हैं, तो अक्सर फ़ॉन्ट ब्राउज़र के डिफ़ॉल्ट फ़ॉन्ट से बदल दिए जाते हैं, जिससे दृश्य लेआउट बिगड़ सकता है। Aspose.Cells आपको वर्कबुक में उपयोग किए गए सटीक फ़ॉन्ट को सीधे HTML फ़ाइल में एम्बेड करने की सुविधा देता है।

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**फ़ॉन्ट एम्बेड करना क्यों महत्वपूर्ण है:**  
जब `EmbedFonts` `true` होता है, तो Aspose.Cells प्रत्येक उपयोग किए गए TrueType/OpenType फ़ॉन्ट को जेनरेटेड HTML के भीतर Base64‑एन्कोडेड `@font-face` नियम में बदल देता है। इससे क्लाइंट मशीन पर समान फ़ॉन्ट स्थापित होने की आवश्यकता समाप्त हो जाती है, और पिक्सेल‑परफेक्ट रेंडरिंग सुनिश्चित होती है।

> **एज केस:** यदि स्रोत वर्कबुक में कोई ऐसा फ़ॉन्ट संदर्भित है जो सर्वर पर स्थापित नहीं है, तो Aspose.Cells डिफ़ॉल्ट फ़ॉन्ट पर फ़ॉल बैक करेगा और एक चेतावनी देगा। सुनिश्चित करें कि आवश्यक फ़ॉन्ट उपलब्ध हों।

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन तरीकों का पता लगाने में मदद करती हैं।

- [C# में WRAPCOLS का उपयोग – Wrap फ़ंक्शन्स के साथ Excel वर्कबुक बनाना](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [HTML में फ़ॉन्ट एम्बेड करना – C# के साथ Excel को HTML में बदलना](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Aspose.Cells for .NET का उपयोग करके Excel फ़ाइलों को HTML में बदलना: ओवरले कंटेंट को छिपाना](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}