---
category: general
date: 2026-02-21
description: SmartMarker का उपयोग करके एक्सेल में डेटा को जल्दी दोहराएँ—जानें कैसे
  एक्सेल टेम्पलेट को भरें और पंक्तियों को सहजता से दोहराएँ।
draft: false
keywords:
- repeat data in excel
- populate excel template
- how to repeat rows
- repeat rows in excel
- populate excel from data
language: hi
og_description: SmartMarker का उपयोग करके एक्सेल में डेटा दोहराएँ। जानें कैसे एक्सेल
  टेम्पलेट को भरें, पंक्तियों को दोहराएँ, और अपनी स्प्रेडशीट्स को स्वचालित करें।
og_title: Excel में डेटा दोहराएँ – SmartMarker के साथ टेम्पलेट भरें
tags:
- excel
- csharp
- smartmarker
- automation
title: Excel में डेटा दोहराएँ – SmartMarker के साथ टेम्पलेट भरें
url: /hi/net/smart-markers-dynamic-data/repeat-data-in-excel-populate-template-with-smartmarker/
---

< blocks/products/products-backtop-button >}}

Now ensure we didn't translate any code placeholders or shortcodes.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में डेटा दोहराएँ – SmartMarker के साथ टेम्पलेट भरें

क्या आपको कभी **repeat data in Excel** करने की ज़रूरत पड़ी, लेकिन मैन्युअल कॉपी‑पेस्ट से बचना नहीं जानते थे? आप अकेले नहीं हैं। कई रिपोर्टिंग परिदृश्यों में आपके पास आइटमों की एक सूची होती है जिसे स्वचालित रूप से पंक्तियों में विस्तारित करना पड़ता है, और इसे हाथ से करना त्रुटियों का कारण बनता है।

यहाँ बात है—**GemBox.Spreadsheet** लाइब्रेरी के `SmartMarkerProcessor` का उपयोग करके आप केवल एक C# लाइन से **populate an Excel template** कर सकते हैं और प्रत्येक आइटम के लिए पंक्तियों को दोहरा सकते हैं। इस गाइड में हम सटीक चरणों को दिखाएंगे, पूरा कोड देंगे, और समझाएंगे कि प्रत्येक भाग क्यों महत्वपूर्ण है, ताकि आप बिना किसी परेशानी के Excel में पंक्तियों को दोहरा सकें।

## आप क्या सीखेंगे

* डेटा संरचना को परिभाषित करना जो दोहराव ऑपरेशन को संचालित करती है।  
* कैसे `SmartMarkerProcessor` को एक वर्कबुक से जोड़ें जिसमें छिपा हुआ टेम्पलेट शीट हो।  
* कैसे `${Repeat:Item}` मार्कर स्वचालित रूप से कई पंक्तियों में विस्तारित होता है।  
* खाली संग्रह या कस्टम फ़ॉर्मेटिंग जैसे किनारे के मामलों को संभालने के टिप्स।  

इस ट्यूटोरियल के अंत तक आप **populate excel from data** को इस तरह से कर पाएँगे जो स्केलेबल, रखरखाव में आसान, और किसी भी .NET प्रोजेक्ट के साथ काम करता हो।

---

## आवश्यकताएँ

* .NET 6.0 या बाद का (कोड आधुनिक C# फीचर्स का उपयोग करता है)।  
* **GemBox.Spreadsheet** NuGet पैकेज (फ्री संस्करण 150 पंक्तियों तक काम करता है)।  
* `Template.xlsx` नामक बेसिक Excel टेम्पलेट फ़ाइल जिसमें `HiddenTemplate` नाम की छिपी शीट हो।  
* C# ऑब्जेक्ट्स और LINQ की परिचितता मददगार है लेकिन आवश्यक नहीं।

---

## चरण 1 – दोहराव डेटा संरचना परिभाषित करें

पहले, आपको एक डेटा स्रोत चाहिए जिसे SmartMarker इंजन इटररेट कर सके। अधिकांश वास्तविक ऐप्स में यह डेटाबेस, API, या CSV फ़ाइल से आता है। स्पष्टता के लिए हम एक अनाम प्रकार का उपयोग करेंगे जिसमें `Item` नाम का एक प्रॉपर्टी है जो स्ट्रिंग्स की एरे रखता है।

```csharp
// Step 1: Define the data that will be repeated in the template
var repeatData = new { Item = new[] { "A", "B", "C" } };
```

> **Why this matters:** `${Repeat:Item}` मार्कर Excel टेम्पलेट के अंदर `Item` नाम की प्रॉपर्टी की तलाश करता है। यदि आप प्रॉपर्टी का नाम बदलते हैं, तो मार्कर को उसी अनुसार अपडेट करें। यह कड़ी कनेक्शन सुनिश्चित करता है कि टेम्पलेट आपके कोड के साथ सिंक में रहे, जिससे **populate excel template** आसान हो जाता है।

### सामान्य विविधताएँ

* **जटिल ऑब्जेक्ट्स:** साधारण स्ट्रिंग एरे की बजाय आप ऑब्जेक्ट्स की लिस्ट (`new[] { new { Name = "A", Qty = 10 } }`) दे सकते हैं। मार्कर पंक्तियों को दोहराएगा और आप शीट में `${Item.Name}` और `${Item.Qty}` का उपयोग कर सकते हैं।  
* **खाली संग्रह:** यदि `Item` खाली है, तो SmartMarker बस दोहराव ब्लॉक को हटा देता है, टेम्पलेट को जैसा है वैसा छोड़ देता है—वैकल्पिक सेक्शनों के लिए शानदार।

---

## चरण 2 – छिपी टेम्पलेट शीट के लिए SmartMarkerProcessor बनाएं

अब, अपनी वर्कबुक लोड करें और एक `SmartMarkerProcessor` इंस्टैंसिएट करें। इसे उस वर्कबुक की ओर इंगित करें जिसमें छिपी टेम्पलेट शीट है; SmartMarker उस शीट को एक दृश्यमान शीट में कॉपी करेगा और दोहराव मार्करों का विस्तार करेगा।

```csharp
using GemBox.Spreadsheet;

// Load the workbook that holds the hidden template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Step 2: Create a SmartMarkerProcessor for the workbook that holds the hidden template sheet
var processor = new SmartMarkerProcessor(wb);
```

> **Pro tip:** यदि आपके पास एक ही फ़ाइल में कई टेम्पलेट हैं, तो `processor.Process` कॉल करते समय स्रोत शीट का नाम निर्दिष्ट कर सकते हैं। यह तब मदद करता है जब आपको रिपोर्ट के विभिन्न सेक्शनों के लिए **repeat rows in excel** करना हो।

### किनारे के मामलों का प्रबंधन

* **टेम्पलेट शीट नहीं मिली:** लोड को try/catch में रखें और स्पष्ट त्रुटि लॉग करें—यह फ़ाइल पाथ गलत होने पर मौन विफलताओं को रोकता है।  
* **बड़े डेटा सेट्स:** हजारों पंक्तियों के लिए आउटपुट को फ़ाइल (`processor.Save`) में स्ट्रीम करने पर विचार करें, बजाय सभी डेटा को मेमोरी में रखने के।

---

## चरण 3 – डेटा लागू करें और `${Repeat:Item}` मार्कर का विस्तार करें

अब वह जादुई लाइन आती है जो वास्तव में पंक्तियों को दोहराती है। चरण 1 में बनाए गए ऑब्जेक्ट को `processor.Process` को पास करें। SmartMarker हर `${Repeat:Item}` मार्कर को खोजेगा, प्रत्येक तत्व के लिए पंक्ति को डुप्लिकेट करेगा, और प्लेसहोल्डर्स को वास्तविक मानों से बदल देगा।

```csharp
// Step 3: Apply the data to the template, expanding the ${Repeat:Item} marker
processor.Process(repeatData);

// Save the resulting workbook.
wb.Save("Result.xlsx");
```

### आपको क्या दिखना चाहिए

जब आप `Result.xlsx` खोलते हैं, तो छिपी टेम्पलेट शीट को डिफ़ॉल्ट रूप से `Sheet1` नाम की नई दृश्यमान शीट में कॉपी किया गया है। वह पंक्ति जिसमें `${Repeat:Item}` था, अब तीन बार दिखाई देती है, और सेल्स क्रमशः **A**, **B**, और **C** दिखाते हैं।

| आइटम |
|------|
| A    |
| B    |
| C    |

यदि आप `${Item.Price}` जैसी अतिरिक्त कॉलम जोड़ते हैं, तो वे डेटा स्रोत से स्वचालित रूप से भर जाएंगे।

---

## SmartMarker के बिना Excel में पंक्तियों को दोहराने का तरीका (त्वरित तुलना)

| दृष्टिकोण                | कोड जटिलता | रखरखाव | प्रदर्शन |
|-------------------------|------------|--------|----------|
| हाथ से कॉपी‑पेस्ट       | उच्च       | निम्न  | खराब     |
| VBA मैक्रो               | मध्यम      | मध्यम  | अच्छा    |
| **SmartMarkerProcessor**| निम्न      | उच्च   | उत्कृष्ट |

जैसा कि आप देख सकते हैं, SmartMarker का उपयोग करके **repeat data in excel** करने से टेम्पलेट डिज़ाइन और बिज़नेस लॉजिक के बीच सबसे साफ़ विभाजन मिलता है। यह भाषा‑निर्भर नहीं है—जावा, पायथन, और जावास्क्रिप्ट लाइब्रेरीज़ में भी समान अवधारणाएँ मौजूद हैं।

---

## उन्नत टिप्स और सामान्य समस्याएँ

### 1. दोहराई गई पंक्तियों का फ़ॉर्मेटिंग

SmartMarker पूरी पंक्ति कॉपी करता है—सेल स्टाइल्स, बॉर्डर्स, और कंडीशनल फ़ॉर्मेटिंग सहित। यदि आपको पहली या आखिरी पंक्ति के लिए अलग स्टाइल चाहिए, तो `${If:Item.IsFirst}` जैसे अतिरिक्त मार्कर जोड़ें और Excel में कंडीशनल फ़ॉर्मूले का उपयोग करें।

### 2. बड़े डेटा सेट्स से निपटना

10 000 से अधिक पंक्तियों के साथ काम करते समय प्रोसेसिंग से पहले Excel की ऑटोमैटिक कैलकुलेशन को डिसेबल करें:

```csharp
wb.WorkbookOptions = new WorkbookOptions { RecalculateAllFormulas = false };
```

सेव करने के बाद इसे फिर से एनेबल करें ताकि प्रदर्शन तेज़ रहे।

### 3. वास्तविक डेटाबेस से डेटा के साथ Excel भरना

```csharp
var orders = dbContext.Orders
    .Where(o => o.Date >= start && o.Date <= end)
    .Select(o => new { o.OrderId, o.CustomerName, o.Total })
    .ToArray();

processor.Process(new { Order = orders });
```

फिर टेम्पलेट में `${Repeat:Order}` का उपयोग करके प्रत्येक ऑर्डर को सूचीबद्ध करें। यह पैटर्न दिखाता है कि कैसे आसानी से **populate excel from data** को Entity Framework से सीधे किया जा सकता है।

### 4. कई दोहराव ब्लॉक्स का उपयोग

आप एक ही शीट या अलग-अलग शीट्स पर कई `${Repeat:...}` मार्कर रख सकते हैं। SmartMarker उन्हें क्रमिक रूप से प्रोसेस करता है, इसलिए क्रम केवल तभी मायने रखता है जब एक ब्लॉक दूसरे के आउटपुट पर निर्भर हो।

---

## पूर्ण चलाने योग्य उदाहरण

नीचे एक स्व-समाहित कंसोल एप्लिकेशन है जिसे आप Visual Studio में पेस्ट करके तुरंत चला सकते हैं। यह सभी तीन चरणों को दर्शाता है और फ़ाइल को सेव करता है।

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License free version (up to 150 rows). For production use, set your license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Define the data to repeat.
        var repeatData = new { Item = new[] { "A", "B", "C" } };

        // 2️⃣ Load the template workbook (ensure Template.xlsx exists next to the exe).
        var wb = ExcelFile.Load("Template.xlsx");

        // Create processor bound to the workbook.
        var processor = new SmartMarkerProcessor(wb);

        // 3️⃣ Process the data – this expands the ${Repeat:Item} marker.
        processor.Process(repeatData);

        // Save the populated workbook.
        wb.Save("Result.xlsx");

        Console.WriteLine("Excel file generated successfully – check Result.xlsx");
    }
}
```

**अपेक्षित आउटपुट:** `Result.xlsx` में एक शीट होगी जहाँ `${Repeat:Item}` वाली पंक्ति तीन बार दिखाई देती है, A, B, और C दिखाते हुए। कोई मैनुअल समायोजन आवश्यक नहीं।

---

## निष्कर्ष

अब आप SmartMarkerProcessor का उपयोग करके **repeat data in excel** को कुशलता से कर सकते हैं। एक सरल डेटा ऑब्जेक्ट परिभाषित करके, टेम्पलेट वर्कबुक लोड करके, और `Process` कॉल करके आप **populate excel template**, **repeat rows in excel**, और सामान्यतः **

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}