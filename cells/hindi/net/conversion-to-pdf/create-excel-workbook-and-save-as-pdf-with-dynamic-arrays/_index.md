---
category: general
date: 2026-09-15
description: C# में Excel वर्कबुक बनाएं और EXPAND फ़ंक्शन का उपयोग करके डायनेमिक एरेज़
  को स्पिल करते हुए वर्कबुक को PDF के रूप में सहेजना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save workbook as pdf
- spill dynamic array
- use expand function
- how to create dynamic array in excel
language: hi
lastmod: 2026-09-15
og_description: C# में Excel वर्कबुक बनाएं और EXPAND फ़ंक्शन का उपयोग करके डायनेमिक
  एरे को स्पिल करते हुए वर्कबुक को जल्दी से PDF के रूप में सहेजें।
og_image_alt: Create Excel workbook screenshot showing dynamic array and PDF output
og_title: डायनामिक एरेज़ के साथ एक्सेल वर्कबुक बनाएं और पीडीएफ के रूप में सहेजें
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Create Excel workbook in C# and learn how to save workbook as PDF while
    spilling dynamic arrays using the EXPAND function.
  headline: Create Excel workbook and save as PDF with dynamic arrays
  type: TechArticle
tags:
- excel
- csharp
- aspose-cells
- pdf
- dynamic-array
title: डायनामिक एरेज़ के साथ एक्सेल वर्कबुक बनाएं और पीडीएफ के रूप में सहेजें
url: /hi/net/conversion-to-pdf/create-excel-workbook-and-save-as-pdf-with-dynamic-arrays/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel वर्कबुक बनाएं और डायनामिक एरेज़ के साथ PDF के रूप में सहेजें

यदि आपको प्रोग्रामेटिकली **Excel वर्कबुक** बनानी है और फिर **वर्कबुक को PDF के रूप में सहेजना** है, तो यह गाइड C# में एक पूर्ण, एंड‑टू‑एंड समाधान दिखाता है। आप यह भी देखेंगे कि **EXPAND फ़ंक्शन** का उपयोग करके **डायनामिक एरे** परिणाम कैसे स्पिल किए जाते हैं, जो VBA के बिना एरे जेनरेट करने का आधुनिक तरीका है।

चाहे आप एक रिपोर्टिंग सर्विस, ERP सिस्टम के लिए एक्सपोर्ट फीचर, या डेटा‑ड्रिवेन डैशबोर्ड बना रहे हों, नीचे दिए गए चरण आपको वर्कबुक जेनरेट करने, उसे स्मार्ट‑मार्कर डेटा से भरने, और एक ऐसा PDF बनाने की अनुमति देंगे जो उन्नत फ़ॉन्ट फीचर्स को संरक्षित रखे।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.8 के साथ भी काम करता है)
* **Aspose.Cells for .NET** का नवीनतम संस्करण (v25.8 या उससे नया) – यह `Workbook`, `PdfSaveOptions`, और `SmartMarkerProcessor` प्रदान करता है।
* Visual Studio 2022 जैसे कोई IDE (कोई भी एडिटर जो C# कंपाइल कर सके, चलेगा)।

अपने प्रोजेक्ट में NuGet पैकेज जोड़ें:

```bash
dotnet add package Aspose.Cells --version 25.8
```

## Step 1: Create Excel workbook and set up the first worksheet

पहला कार्य है **Excel वर्कबुक** बनाना और डिफ़ॉल्ट वर्कशीट का रेफ़रेंस प्राप्त करना। यह वर्कशीट डायनामिक एरे और Smart Marker टेम्प्लेट को होस्ट करेगी।

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook in memory
        Workbook wb = new Workbook();

        // Get the first (default) worksheet
        Worksheet ws = wb.Worksheets[0];
```

*Why this matters*: `Workbook` को इंस्टैंशिएट करने से आंतरिक वर्कबुक स्ट्रक्चर अलोकेट हो जाता है, जबकि `Worksheets[0]` तक पहुंचने से आपको मैन्युअली शीट जोड़ने की ज़रूरत के बिना एक तैयार‑टू‑यूज़ शीट मिलती है।

## Step 2: Spill dynamic array using the EXPAND function

Excel का **EXPAND फ़ंक्शन** एक स्थिर एरे लिटरल को किसी भी आकार के स्पिल रेंज में बदल सकता है। यहाँ हम Excel से `{1,2,3}` को `A1` से शुरू होने वाले 5‑row × 1‑column रेंज में विस्तारित करने को कह रहे हैं।

```csharp
        // Write the EXPAND formula into A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // Force calculation so the spill occurs immediately
        ws.Calculate();
```

*Why this matters*: `EXPAND` का उपयोग करने से C# में मैनुअल लूप्स की आवश्यकता नहीं रहती। इंजन स्पिल रेंज की गणना करता है और मान सीधे वर्कशीट में स्टोर करता है, जो बाद में PDF में दिखते हैं।

## Step 3: Save workbook as PDF while preserving font variation selectors

जब आपको **वर्कबुक को PDF के रूप में सहेजना** हो, तो आप उन्नत टाइपोग्राफिक फीचर्स जैसे फ़ॉन्ट वैरिएशन सिलेक्टर्स (Aspose.Cells v25.8 से उपलब्ध) को भी एनेबल कर सकते हैं। यह सुनिश्चित करता है कि PDFs जटिल स्क्रिप्ट्स को सही ढंग से रेंडर करें।

```csharp
        // Configure PDF options
        PdfSaveOptions pdfOpts = new PdfSaveOptions
        {
            FontVariationSelectors = true   // keeps variation selectors for OpenType fonts
        };

        // Save the current workbook (with the spilled array) as PDF
        wb.Save(@"YOUR_DIRECTORY\VarSelector.pdf", pdfOpts);
```

*Why this matters*: `FontVariationSelectors` को `true` सेट करना उन भाषाओं के लिए आवश्यक है जो ग्लिफ़ वैरिएशन पर निर्भर करती हैं (जैसे चीनी, जापानी, इमोजी)। उत्पन्न PDF स्क्रीन पर दिखे Excel दृश्य को प्रतिबिंबित करता है।

## Step 4: Insert a Smart Marker template that references a nested data source

Smart Markers आपको वर्कशीट में सीधे प्लेसहोल्डर एम्बेड करने की अनुमति देते हैं। नीचे दिया गया टेम्प्लेट ऑर्डर्स और उनके आइटम्स की सूची जेनरेट करेगा।

```csharp
        // Define a Smart Marker template in cell A1
        string template = "${Orders.OrderId}\n${Orders.Items:ItemName}\n";
        ws.Cells["A1"].PutValue(template);
```

*Why this matters*: `A1` में टेम्प्लेट रखकर आप Aspose.Cells को बताते हैं कि डेटा कहाँ से शुरू होना चाहिए। `:` सिंटैक्स (`Items:ItemName`) प्रोसेसर को नेस्टेड कलेक्शन पर इटरेट करने के लिए निर्देश देता है।

## Step 5: Define the nested data source (orders containing items)

हम ऑर्डर्स का एक अनाम एरे बनाते हैं, प्रत्येक में अपने स्वयं के आइटम ऑब्जेक्ट्स का कलेक्शन होता है। यह एक सामान्य मास्टर‑डिटेल परिदृश्य को दर्शाता है।

```csharp
        // Sample nested data source
        var orders = new[]
        {
            new
            {
                OrderId = 1,
                Items = new[]
                {
                    new { ItemName = "Apple" },
                    new { ItemName = "Banana" }
                }
            },
            new
            {
                OrderId = 2,
                Items = new[]
                {
                    new { ItemName = "Carrot" }
                }
            }
        };
```

*Why this matters*: नेस्टेड स्ट्रक्चर यह दर्शाता है कि **Excel में डायनामिक एरे कैसे बनाएं** Smart Markers के माध्यम से, बिना किसी VBA या मैनुअल सेल लूप के।

## Step 6: Process the Smart Markers and save the final Excel file

अब हम वर्कबुक और डेटा सोर्स को `SmartMarkerProcessor` को देते हैं। प्रोसेसिंग के बाद प्लेसहोल्डर वास्तविक पंक्तियों से बदल जाते हैं, और हम परिणाम को एक सामान्य `.xlsx` फ़ाइल के रूप में सहेजते हैं।

```csharp
        // Process the Smart Markers
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.Process(wb, orders);

        // Save the populated workbook
        wb.Save(@"YOUR_DIRECTORY\NestedSmartMarker.xlsx");
    }
}
```

*Why this matters*: `SmartMarkerProcessor` स्वचालित रूप से टेम्प्लेट को विस्तारित करता है, आवश्यक पंक्तियों को बनाता है, और डेटा से भरता है। अंतिम वर्कबुक को Excel में खोलकर आप सत्यापित कर सकते हैं कि प्रत्येक ऑर्डर और उसके आइटम सही ढंग से दिख रहे हैं।

## Expected output

* **VarSelector.pdf** – एक PDF फ़ाइल जिसमें संख्याएँ 1‑3 पाँच पंक्तियों में स्पिल होती दिखती हैं, और आपने जो भी OpenType फ़ॉन्ट वैरिएशन एनेबल किया है, वह लागू रहता है।
* **NestedSmartMarker.xlsx** – एक Excel फ़ाइल जिसमें निम्न पंक्तियाँ (`A1` से शुरू) होंगी:

| OrderId | ItemName |
|---------|----------|
| 1       | Apple    |
| 1       | Banana   |
| 2       | Carrot   |

PDF संस्करण वही न्यूमेरिक स्पिल रखता है क्योंकि वर्कशीट की स्थिति Smart Marker प्रोसेसिंग से पहले सहेजी गई थी; यदि आप अंतिम डेटा को PDF में भी चाहते हैं तो प्रोसेसिंग के बाद PDF सहेजना दोहराया जा सकता है।

## Pro tips and common pitfalls

| टिप | विवरण |
|-----|--------|
| **एक ही `PdfSaveOptions` को पुन: उपयोग करें** | विकल्प ऑब्जेक्ट को एक बार बनाकर पुन: उपयोग करने से रेंडरिंग में सूक्ष्म अंतर (जैसे वैरिएशन सिलेक्टर्स का अभाव) से बचा जा सकता है। |
| **फ़ॉर्मूला सेट करने के बाद `ws.Calculate()` कॉल करें** | स्पष्ट गणना के बिना स्पिल रेंज प्रोग्रामेटिकली वर्कबुक की जाँच करते समय खाली रह सकती है। |
| **Smart Marker टेम्प्लेट को साफ़ शीट पर रखें** | मौजूदा डेटा के साथ टेम्प्लेट मिलाने से अनपेक्षित पंक्ति इन्सर्शन हो सकता है। संभव हो तो समर्पित शीट का उपयोग करें। |
| **फ़ाइल पाथ्स का ध्यान रखें** | विभिन्न मशीनों पर हार्ड‑कोडेड डायरेक्टरीज़ से बचने के लिए `Path.Combine(Environment.CurrentDirectory, "output.pdf")` का उपयोग करें। |
| **वर्ज़न चेक** | `FontVariationSelectors` केवल संस्करण 25.8 से उपलब्ध है; पुराने संस्करण इस प्रॉपर्टी को अनदेखा करेंगे और कोई त्रुटि नहीं देंगे। |

## Next steps

अब जब आप जानते हैं कि **Excel वर्कबुक कैसे बनाएं**, **डायनामिक एरे कैसे स्पिल करें**, और **वर्कबुक को PDF के रूप में कैसे सहेजें**, तो आप आगे खोज सकते हैं:

* PDF कन्वर्ज़न से पहले चार्ट या इमेज जोड़ना।
* `Save` ओवरलोड्स का उपयोग करके उसी वर्कबुक को अन्य फ़ॉर्मैट (जैसे HTML, CSV) में एक्सपोर्ट करना।
* **Smart Marker एक्सप्रेशन्स** (`${Orders.Total:SUM(Items.Price)}`) का उपयोग करके ऑन‑द‑फ़्लाई एग्रीगेट्स की गणना करना।
* इस कोड को ASP.NET Core API में इंटीग्रेट करना ताकि उपयोगकर्ता वेब एंडपॉइंट से सीधे जेनरेटेड PDF डाउनलोड कर सकें।

---

**Summary** – इस ट्यूटोरियल ने आपको दिखाया कि कैसे **Excel वर्कबुक बनाएं**, **EXPAND फ़ंक्शन** का उपयोग करके **डायनामिक एरे स्पिल करें**, एक **Smart Marker** एम्बेड करें जो नेस्टेड डेटा सोर्स के साथ काम करता है, और अंत में **वर्कबुक को PDF के रूप में सहेजें** जबकि उन्नत फ़ॉन्ट फीचर्स को संरक्षित रखें। पूरा, रन करने योग्य उदाहरण किसी भी C# प्रोजेक्ट में कॉपी‑पेस्ट किया जा सकता है और आपके अपने डेटा स्ट्रक्चर के अनुसार अनुकूलित किया जा सकता है। Happy coding!

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [Create and Save Excel Workbook as PDF in ASP.NET Using Aspose.Cells](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}