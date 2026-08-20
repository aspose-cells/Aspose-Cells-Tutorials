---
category: general
date: 2026-02-14
description: डिस्काउंट टेम्पलेट जल्दी बनाएं और सीखें कि स्प्रेडशीट में डिस्काउंट कैसे
  लागू करें, टेम्पलेट में डेटा इन्जेक्ट करें, और स्मार्ट मार्कर्स के लिए वैरिएबल प्रीफ़िक्स
  निर्धारित करें।
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: hi
og_description: C# के साथ डिस्काउंट टेम्प्लेट बनाएं। स्प्रेडशीट में डिस्काउंट लागू
  करना सीखें, टेम्प्लेट में डेटा इंजेक्ट करें, और स्मार्ट मार्कर्स के लिए वैरिएबल
  प्रीफ़िक्स निर्धारित करें।
og_title: डिस्काउंट टेम्पलेट बनाएं – पूर्ण C# मार्गदर्शन
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: C# में डिस्काउंट टेम्पलेट बनाएं – चरण-दर-चरण मार्गदर्शिका
url: /hi/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# डिस्काउंट टेम्प्लेट बनाएं – पूर्ण C# वॉकथ्रू

क्या आपको कभी **डिस्काउंट टेम्प्लेट बनाना** पड़ा है किसी सेल्स रिपोर्ट के लिए, लेकिन यह नहीं पता था कि नंबरों को स्वचालित रूप से स्प्रेडशीट में कैसे फीड किया जाए? आप अकेले नहीं हैं। इस ट्यूटोरियल में हम आपको दिखाएंगे कि **डिस्काउंट टेम्प्लेट कैसे बनाएं**, फिर **स्प्रेडशीट में डिस्काउंट लागू करें**, **डेटा को टेम्प्लेट में इंजेक्ट करें**, और यहाँ तक कि आपके स्मार्ट मार्कर्स के लिए **वेरिएबल प्रीफ़िक्स कैसे परिभाषित करें**—सभी साफ़ C# कोड के साथ।

हम समस्या का संक्षिप्त विवरण देंगे, फिर सीधे एक कार्यशील समाधान में कूदेंगे जिसे आप कॉपी‑पेस्ट कर सकते हैं। अंत तक आपके पास एक पुन: उपयोग योग्य पैटर्न होगा जो इनवॉइस, प्राइस‑लिस्ट या किसी भी स्प्रेडशीट के लिए काम करेगा जिसे डायनामिक डिस्काउंट की आवश्यकता है।

---

## आप क्या सीखेंगे

- डिस्काउंट‑अवेयर स्प्रेडशीट टेम्प्लेट कैसे डिज़ाइन करें।
- कस्टम `VariablePrefix` / `VariableSuffix` कैसे कॉन्फ़िगर करें ताकि मार्कर्स आसानी से दिखें।
- एक अनाम ऑब्जेक्ट (`discountData`) को `SmartMarkerProcessor` में कैसे पास करें।
- परिणामी फ़ॉर्मूला (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) कैसे स्वचालित रूप से अंतिम कीमत की गणना करता है।
- ज़ीरो‑डिस्काउंट पंक्तियों या कई डिस्काउंट टियर्स जैसे एज केस को कैसे संभालें।

**Prerequisites** – एक हालिया .NET रनटाइम (≥ .NET 6), `Aspose.Cells` (या समान) लाइब्रेरी का रेफ़रेंस जो `SmartMarkerProcessor` प्रदान करती है, और C# सिंटैक्स की बुनियादी समझ। कोई जटिल चीज़ नहीं।

---

## चरण 1: अपने स्प्रेडशीट में डिस्काउंट टेम्प्लेट बनाएं

सबसे पहले, एक नई वर्कबुक खोलें (या मौजूदा का उपयोग करें) और वह प्लेसहोल्डर रखें जहाँ डिस्काउंट लागू होगा। टेम्प्लेट को एक साधारण Excel फ़ाइल के रूप में सोचें जिसमें “स्मार्ट मार्कर्स” हों, जिन्हें प्रोसेसर बाद में बदल देगा।

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**यह क्यों महत्वपूर्ण है:** फ़ॉर्मूला के अंदर `#Discount#` एम्बेड करके हम प्रोसेसर को ठीक वही बताते हैं जहाँ डिस्काउंट वैल्यू रखनी है। `SmartMarkerProcessor` बाद में `#Discount#` को आपके द्वारा प्रदान किए गए नंबर से बदल देगा, जबकि फ़ॉर्मूला का बाकी हिस्सा अपरिवर्तित रहेगा।

---

## चरण 2: स्मार्ट मार्कर्स के लिए वेरिएबल प्रीफ़िक्स परिभाषित करें

डिफ़ॉल्ट रूप से, कई लाइब्रेरी `${Variable}` या `{{Variable}}` देखती हैं। हमारे मामले में हम एक साफ़, मानव‑पठनीय मार्कर चाहते हैं, इसलिए हम **वेरिएबल प्रीफ़िक्स** और सफ़िक्स को स्पष्ट रूप से परिभाषित करते हैं।

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** `#` का उपयोग करने से मार्कर्स छोटा और Excel के फ़ॉर्मूला बार में आसानी से दिखाई देता है। यदि आपको मौजूदा Excel फ़ंक्शन्स के साथ टकराव से बचना है, तो एक अलग जोड़ी चुनें (जैसे `[[` और `]]`)।

---

## चरण 3: SmartMarkerProcessor का उपयोग करके डेटा को टेम्प्लेट में इंजेक्ट करें

अब हम वास्तविक डिस्काउंट वैल्यू फीड करते हैं। प्रोसेसर वर्कशीट स्कैन करेगा, हर `#Discount#` को ढूँढेगा, और उसे अनाम ऑब्जेक्ट से प्राप्त वैल्यू से बदल देगा।

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

इस कॉल के बाद, `B2` में फ़ॉर्मूला इस प्रकार हो जाता है:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

जब वर्कबुक कैलकुलेट होती है, तो `B2` दिखाता है **90**, यानी मूल कीमत 100 पर 10 % डिस्काउंट लागू हुआ।

**यह क्यों काम करता है:** `StartSmartMarkerProcessing` हर सेल को पार करता है, `#Discount#` टोकन को खोजता है, और संख्यात्मक वैल्यू से प्रतिस्थापित करता है। क्योंकि टोकन एक `IF` स्टेटमेंट के अंदर है, स्प्रेडशीट अभी भी उन मामलों को संभालती है जहाँ डिस्काउंट शून्य हो सकता है।

---

## चरण 4: स्प्रेडशीट में डिस्काउंट लागू करें – परिणाम की जाँच करें

आइए कैलकुलेशन ट्रिगर करें और अंतिम कीमत को कंसोल पर आउटपुट करें। यह चरण प्रमाणित करता है कि **स्प्रेडशीट में डिस्काउंट लागू करने** वाला वर्कफ़्लो सफल रहा।

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**अपेक्षित आउटपुट**

```
Original: 100
Discounted (10%): 90
```

यदि आप `discountData.Discount` को `0.25` बदलते हैं और प्रोसेसर को फिर से चलाते हैं, तो आउटपुट स्वचालित रूप से 25 % डिस्काउंट दिखाएगा—कोई अतिरिक्त कोड नहीं चाहिए।

---

## चरण 5: एज केस और मल्टीपल डिस्काउंट को संभालना

### ज़ीरो‑डिस्काउंट पंक्तियाँ

कभी‑कभी कोई प्रोडक्ट सेल पर नहीं होता। फ़ॉर्मूला को मजबूत रखने के लिए, आपने पहले रखी `IF` शर्त पहले से ही इस स्थिति को कवर करती है: जब `#Discount#` `0` हो, तो मूल कीमत बिना परिवर्तन के पास हो जाती है।

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### कई डिस्काउंट कॉलम

यदि आपको प्रत्येक पंक्ति के लिए अलग डिस्काउंट चाहिए, तो प्रत्येक पंक्ति को अपना मार्कर दें, जैसे `#Discount1#`, `#Discount2#`, और एक कलेक्शन पास करें:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

प्रोसेसर मार्कर्स को क्रमिक रूप से मिलाता है, इसलिए प्रत्येक पंक्ति को सही वैल्यू मिलती है।

---

## पूर्ण कार्यशील उदाहरण

नीचे पूरा, कॉपी‑रेडी प्रोग्राम दिया गया है जो ऊपर बताए गए सभी चरणों को सम्मिलित करता है। इसे `Program.cs` के रूप में सेव करें, `Aspose.Cells` का रेफ़रेंस जोड़ें, और चलाएँ।

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

इसे चलाने पर अपेक्षित संख्याएँ प्रिंट होंगी और एक `DiscountedPricing.xlsx` फ़ाइल बनेगी जिसे आप Excel में खोलकर फ़ॉर्मूला पहले से ही रिजॉल्व्ड देख सकते हैं।

---

## निष्कर्ष

अब आप जानते हैं कि **डिस्काउंट टेम्प्लेट कैसे बनाएं**, **स्प्रेडशीट में डिस्काउंट कैसे लागू करें**, **टेम्प्लेट में डेटा कैसे इंजेक्ट करें**, और **स्मार्ट मार्कर्स के लिए वेरिएबल प्रीफ़िक्स कैसे परिभाषित करें**—सिर्फ कुछ संक्षिप्त C# लाइनों के साथ। यह पैटर्न स्केलेबल है—सिर्फ अनाम ऑब्जेक्ट बदलें या बैच अपडेट के लिए कलेक्शन फीड करें, और वही टेम्प्लेट किसी भी डिस्काउंट परिदृश्य को संभाल लेगा।

अगले स्तर के लिए तैयार हैं? आज़माएँ:

- डिस्काउंट के साथ टैक्स कैलकुलेशन जोड़ना।
- डिस्काउंट प्रतिशत को हार्ड‑कोड करने के बजाय डेटाबेस से लाना।
- उच्च डिस्काउंट वाली पंक्तियों को हाइलाइट करने के लिए कंडीशनल फ़ॉर्मेटिंग का उपयोग करना।

इन एक्सटेंशन से कोर आइडिया बना रहेगा, जबकि आपके डिस्काउंट टेम्प्लेट की उपयोगिता बढ़ेगी।

कोई सवाल या कूल यूज़‑केस है? नीचे कमेंट करें, और हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}