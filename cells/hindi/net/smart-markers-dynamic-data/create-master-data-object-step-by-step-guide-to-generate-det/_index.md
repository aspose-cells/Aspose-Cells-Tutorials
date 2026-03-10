---
category: general
date: 2026-02-14
description: C# में मास्टर डेटा ऑब्जेक्ट बनाएं और आसानी से डिटेल शीट जनरेट करें। व्यावहारिक
  कोड उदाहरणों के साथ पूर्ण SmartMarker वर्कफ़्लो सीखें।
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: hi
og_description: C# में मास्टर डेटा ऑब्जेक्ट बनाएं और SmartMarker के साथ डिटेल शीट
  जनरेट करें। तैयार‑से‑चलाने योग्य समाधान के लिए हमारे विस्तृत ट्यूटोरियल का पालन
  करें।
og_title: मास्टर डेटा ऑब्जेक्ट बनाएं – पूर्ण गाइड
tags:
- C#
- SmartMarker
- Excel Automation
title: मास्टर डेटा ऑब्जेक्ट बनाएं – डिटेल शीट उत्पन्न करने के लिए चरण‑दर‑चरण मार्गदर्शिका
url: /hi/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

sure to preserve all markdown formatting, headings, lists, code block placeholders.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# मास्टर डेटा ऑब्जेक्ट बनाएं – पूर्ण ट्यूटोरियल

क्या आपको कभी Excel वर्कशीट के लिए **create master data object** बनाने की ज़रूरत पड़ी है लेकिन यह नहीं पता था कि इसे SmartMarker डिटेल शीट से कैसे जोड़ें? आप अकेले नहीं हैं। कई रिपोर्टिंग परिदृश्यों में मास्टर ऑब्जेक्ट एक डायनामिक डिटेल शीट को नियंत्रित करता है, और सही कनेक्शन बनाना बिना चित्र के पहेली जोड़ने जैसा महसूस हो सकता है।  

इस गाइड में हम पूरी प्रक्रिया को चरण‑बद्ध रूप से देखेंगे—मास्टर डेटा ऑब्जेक्ट बनाना, SmartMarker विकल्पों को **generate detail sheet** के लिए कॉन्फ़िगर करना, और अंत में प्रोसेसर को चलाना। अंत तक आपके पास एक रन करने योग्य स्निपेट होगा जिसे आप किसी भी .NET प्रोजेक्ट में पेस्ट कर सकते हैं जो GrapeCity Documents for Excel (GcExcel) लाइब्रेरी का उपयोग करता है।

## What You’ll Need

- .NET 6+ (या .NET Framework 4.7.2) के साथ `GcExcel.dll` का रेफ़रेंस
- बुनियादी C# परिचितता (वेरिएबल्स, anonymous types, object initializers)
- एक Excel वर्कबुक जिसमें पहले से ही SmartMarker टैग जैसे `{{OrderId}}` और लाइन आइटम्स के लिए एक टेबल हो
- Visual Studio, Rider, या कोई भी एडिटर जो आप पसंद करते हैं

बस इतना ही—कोर GcExcel वितरण के अलावा कोई अतिरिक्त NuGet पैकेज नहीं।

## चरण 1: मास्टर डेटा ऑब्जेक्ट बनाएं

पहला काम जो आपको करना है वह है **create master data object** बनाना जो SmartMarker टैग्स द्वारा अपेक्षित संरचना को प्रतिबिंबित करता है। इसे एक छोटा इन‑मेमोरी रिपोर्ट मॉडल मानें।

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

यहाँ anonymous type क्यों उपयोग करें? क्योंकि यह आपको एक हल्का कंटेनर परिभाषित करने देता है बिना पूरी‑तरह की क्लास घोषित किए—तेज़ डेमो या जब संरचना बदलने की संभावना कम हो, तब यह परफेक्ट है। यदि बाद में आपको पुन: उपयोग योग्य मॉडल चाहिए, तो बस `var` को एक उचित POCO से बदल दें।

> **Pro tip:** प्रॉपर्टी नाम (`OrderId`, `Product`, `Quantity`) को अपने वर्कशीट में प्लेसहोल्डर्स के समान रखें; SmartMarker उन्हें केस‑इन्सेंसिटिव मैच करता है।

## चरण 2: SmartMarker विकल्पों को Configure करके **generate detail sheet** बनाएं

अब हम SmartMarker को बताते हैं कि हमें लाइन‑आइटम टेबल के लिए एक अलग वर्कशीट चाहिए। यहाँ **generate detail sheet** कीवर्ड काम आता है।

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

`DetailSheetNewName` पैटर्न कर्ली‑ब्रैकेट प्लेसहोल्डर्स का उपयोग करता है जो रनटाइम पर बदलते हैं। हमारे उदाहरण में शीट का नाम `Order_1` होगा। यदि आप बाद में कई ऑर्डर्स पर लूप करते हैं, तो प्रत्येक को अपना टैब मिलेगा—बिल्कुल वही जो अधिकांश अकाउंटेंट्स उम्मीद करते हैं।

## चरण 3: SmartMarker प्रोसेसर चलाएँ

डेटा और विकल्प तैयार होने के बाद, अंतिम कदम टार्गेट वर्कशीट पर प्रोसेसर को कॉल करना है।

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

पर्दे के पीछे, SmartMarker वर्कशीट को टैग्स के लिए स्कैन करता है, `orderData` मानों को इंजेक्ट करता है, और क्योंकि `DetailSheet` `true` है, यह टेम्पलेट को `Order_1` नाम की नई शीट में क्लोन करता है। सभी लाइन आइटम्स डिटेल एरिया में दिखते हैं, और टेम्पलेट में लागू कोई भी फॉर्मेटिंग बरकरार रहती है।

### पूर्ण कार्यशील उदाहरण

नीचे एक स्व-निहित कंसोल प्रोग्राम है जो टेम्पलेट वर्कबुक (`Template.xlsx`) खोलता है, तीन चरण चलाता है, और परिणाम को `Result.xlsx` के रूप में सहेजता है। आप इसे नई कंसोल प्रोजेक्ट में कॉपी‑पेस्ट कर **F5** दबा सकते हैं।

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### अपेक्षित आउटपुट

- **Result.xlsx** में `Order_1` नाम की शीट होती है।
- सेल `A1` (या जहाँ भी आपने `{{OrderId}}` रखा है) अब `1` दिखाता है।
- SmartMarker ब्लॉक से शुरू होने वाली टेबल दो पंक्तियों को सूचीबद्ध करती है:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

यदि आप फ़ाइल खोलते हैं, तो आप देखेंगे कि टेम्पलेट से फॉर्मेटिंग बरकरार है—बॉर्डर्स, फ़ॉन्ट्स, कंडीशनल फॉर्मेटिंग—सब कुछ अछूता है।

## सामान्य प्रश्न और किनारे के मामले

### यदि मेरे पास कई ऑर्डर्स हों तो क्या करें?

मास्टर ऑब्जेक्ट को एक कलेक्शन में रैप करें और SmartMarker को स्वचालित रूप से इटररेट करने दें:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

प्रत्येक ऑर्डर अपना शीट (`Order_1`, `Order_2`, …) बनाता है। प्रोसेसर बाहरी एरे को मास्टर कलेक्शन के रूप में मानता है।

### शीट की पोजीशन कैसे नियंत्रित करें?

नया शीट दूसरे टैब के बाद रखने के लिए `smartMarkerOptions.DetailSheetInsertIndex = 2;` सेट करें, या नामित शीट के बाद डालने के लिए `DetailSheetInsertAfter = "Summary"` उपयोग करें।

### क्या मैं किसी विशेष रन के लिए डिटेल शीट को डिसेबल कर सकता हूँ?

सिर्फ `DetailSheet = false;` सेट करें। फिर SmartMarker लाइन आइटम्स को उसी शीट में लिखेगा जहाँ मास्टर टैग्स मौजूद हैं।

### बड़े डेटा सेट के बारे में क्या?

SmartMarker डेटा को कुशलता से स्ट्रीम करता है, लेकिन यदि आप कुछ सौ हजार पंक्तियों से अधिक हो जाते हैं तो आप Excel की 1,048,576‑पंक्ति सीमा तक पहुँच सकते हैं। ऐसे में डेटा को कई मास्टर रिकॉर्ड्स में बाँटें या CSV में एक्सपोर्ट करने पर विचार करें।

## दृश्य अवलोकन

![SmartMarker का उपयोग करके मास्टर डेटा ऑब्जेक्ट बनाने और डिटेल शीट जनरेट करने का आरेख](/images/smartmarker-flow.png)

*यह चित्र C# मास्टर ऑब्जेक्ट → SmartMarker विकल्प → वर्कशीट प्रोसेसिंग → नई डिटेल शीट के प्रवाह को दर्शाता है।*

## निष्कर्ष

अब आप जानते हैं कि C# में **create master data object** कैसे बनाते हैं और SmartMarker को **generate detail sheet** स्वचालित रूप से कैसे कॉन्फ़िगर करते हैं। तीन‑चरणीय पैटर्न—डेटा, विकल्प, प्रोसेसर—GcExcel के साथ अधिकांश Excel ऑटोमेशन परिदृश्यों को कवर करता है।  

अब आप आगे खोज सकते हैं:

- प्रत्येक डिटेल शीट में हेडर/फूटर डेटा जोड़ना
- ऑर्डर स्टेटस के आधार पर कंडीशनल फॉर्मेटिंग का उपयोग करना
- `workbook.SaveAsPdf(...)` के साथ जेनरेटेड वर्कबुक को PDF में एक्सपोर्ट करना

बिना झिझक प्रयोग करें, चीज़ें तोड़ें, और फिर उन्हें फिर से जोड़ें। यही वर्कशीट ऑटोमेशन में महारत हासिल करने का सबसे तेज़ तरीका है। कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}