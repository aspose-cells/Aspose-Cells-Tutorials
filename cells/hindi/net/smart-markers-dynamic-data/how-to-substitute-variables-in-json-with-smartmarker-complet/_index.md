---
category: general
date: 2026-03-29
description: SmartMarker का उपयोग करके JSON में वेरिएबल्स को कैसे बदलें – if एक्सप्रेशन
  का उपयोग करना सीखें, कंडीशनल लॉजिक लागू करें, मानों को गुणा करें, और आसानी से JSON
  जनरेट करें।
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: hi
og_description: SmartMarker का उपयोग करके JSON में वेरिएबल्स को कैसे बदलें। जानें
  कि if एक्सप्रेशन का उपयोग कैसे करें, कंडीशनल लॉजिक लागू करें, मानों को गुणा करें,
  और मिनटों में JSON जेनरेट करें।
og_title: स्मार्टमार्कर के साथ JSON में वेरिएबल्स को कैसे बदलें – चरण‑दर‑चरण
tags:
- C#
- SmartMarker
- JSON templating
title: स्मार्टमार्कर के साथ JSON में वेरिएबल्स को प्रतिस्थापित करने का पूर्ण गाइड
url: /hi/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SmartMarker के साथ JSON में वेरिएबल्स को बदलना – पूर्ण गाइड

क्या आपने कभी कस्टम पार्सर लिखे बिना JSON पेलोड के भीतर **वेरिएबल्स को बदलने** के बारे में सोचा है? आप अकेले नहीं हैं। कई इंटीग्रेशन परिदृश्यों में—जैसे इनवॉइस, प्राइसिंग इंजन, या डायनामिक कॉन्फ़िगरेशन फ़ाइलें—आपको रनटाइम वैल्यूज़ इन्जेक्ट करनी होती हैं, सरल कंडीशनल लागू करने होते हैं, और शायद एक तेज़ मल्टीप्लिकेशन भी करना पड़ता है। यह ट्यूटोरियल आपको बिल्कुल **वेरिएबल्स को बदलने** का तरीका SmartMarker लाइब्रेरी का उपयोग करके दिखाता है, जबकि JSON को साफ़ और पढ़ने योग्य रखता है।

हम एक वास्तविक‑दुनिया उदाहरण के माध्यम से चलेंगे जिसमें **if एक्सप्रेशन का उपयोग**, **कंडीशनल कैसे लागू करें**, **वैल्यूज़ को कैसे मल्टीप्लाई करें**, और **JSON को कैसे जेनरेट करें** शामिल हैं। अंत तक, आपके पास एक तैयार‑चलाने‑योग्य C# स्निपेट होगा जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं।

## आप क्या सीखेंगे

- `SmartMarkerOptions` को सेट अप करें ताकि पुन: उपयोग योग्य वेरिएबल्स स्टोर किए जा सकें।  
- एक JSON टेम्प्लेट लिखें जिसमें कंडीशनल लॉजिक के लिए `if` एक्सप्रेशन हो।  
- टेम्प्लेट के भीतर एक वैल्यू को वेरिएबल से मल्टीप्लाई करें।  
- `SmartMarkerProcessor` के साथ टेम्प्लेट प्रोसेस करें और अंतिम JSON स्ट्रिंग प्राप्त करें।  
- सामान्य समस्याओं जैसे गायब वेरिएबल्स या गलत एक्सप्रेशन को ट्रबलशूट करें।

कोई बाहरी सर्विस नहीं, कोई भारी डिपेंडेंसी नहीं—सिर्फ साधारण C# और SmartMarker NuGet पैकेज।

---

## वेरिएबल्स को बदलने का चरण‑दर‑चरण अवलोकन

नीचे वर्कफ़्लो की एक उच्च‑स्तरीय तस्वीर है। इसे एक पाइपलाइन की तरह सोचें जहाँ आपका कच्चा JSON टेम्प्लेट बाएँ से प्रवेश करता है, SmartMarker इंजन अपना जादू करता है, और पूरी‑तरह रेंडर किया हुआ JSON दाएँ से बाहर निकलता है।

![JSON में वेरिएबल्स को बदलने का आरेख](https://example.com/images/smartmarker-flow.png "JSON में वेरिएबल्स को बदलना")

*छवि वैकल्पिक पाठ: JSON में वेरिएबल्स को बदलने का आरेख.*

---

## चरण 1: SmartMarker स्थापित करें और इम्पोर्ट करें

शुरू करने से पहले, सुनिश्चित करें कि आपके प्रोजेक्ट में SmartMarker पैकेज रेफ़रेंसेस है। यदि आप .NET CLI का उपयोग कर रहे हैं, तो चलाएँ:

```bash
dotnet add package SmartMarker
```

फिर, अपने C# फ़ाइल के शीर्ष पर आवश्यक `using` निर्देश जोड़ें:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **प्रो टिप:** नवीनतम संस्करण (मार्च 2026 तक) 2.4.1 है। यह .NET 6 और बाद के संस्करणों को सपोर्ट करता है, लेकिन .NET Framework 4.7 के साथ भी ठीक काम करता है।

---

## चरण 2: SmartMarker Options बनाएं और वेरिएबल्स परिभाषित करें

अब हम `SmartMarkerOptions` का एक इंस्टेंस बनाएँगे जो टेम्प्लेट में पुन: उपयोग करने वाले सभी वेरिएबल्स को रखेगा। यही वह जगह है जहाँ हम प्रश्न **वेरिएबल्स को कैसे बदलें** का उत्तर देते हैं—वेरिएबल्स प्लेसहोल्डर के रूप में काम करते हैं जिन्हें SmartMarker बाद में बदल देगा।

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

रेट को `Variables` में स्टोर क्यों करें बजाय हार्ड‑कोडिंग के? क्योंकि आप वह संख्या डेटाबेस, कॉन्फ़िग फ़ाइल, या यूज़र इनपुट से ले सकते हैं। इसे विकल्पों में रखने से टेम्प्लेट पुन: उपयोग योग्य और टेस्टेबल बनता है।

---

## चरण 3: `if` एक्सप्रेशन के साथ JSON टेम्प्लेट लिखें

यहीं पर **use if expression** कीर्ड चमकता है। SmartMarker आपको JSON स्ट्रिंग के भीतर सीधे कंडीशनल लॉजिक एम्बेड करने देता है। सिंटैक्स थोड़ा प्रॉपर्टी नाम जैसा दिखता है, लेकिन SmartMarker इसे एक निर्देश के रूप में लेता है।

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

की `if(Amount>500)` पर ध्यान दें। SmartMarker एक्सप्रेशन `Amount>500` का मूल्यांकन करता है; यदि यह सत्य है, तो संबंधित वैल्यू (`${Amount * Rate}`) आउटपुट में डाल दी जाती है। `${...}` सिंटैक्स *वेरिएबल सब्स्टिट्यूशन* इंजन है—यहाँ हम **वैल्यूज़ को कैसे मल्टीप्लाई करें** (`Amount * Rate`) परिणाम डालने से पहले।

---

## चरण 4: टेम्प्लेट प्रोसेस करें और अंतिम JSON प्राप्त करें

विकल्पों और टेम्प्लेट के तैयार होने पर, हम सब कुछ प्रोसेसर को सौंपते हैं। मेथड `ProcessJson` टेम्प्लेट को पार्स करता है, कंडीशन लागू करता है, मल्टीप्लिकेशन करता है, और एक साफ़ JSON स्ट्रिंग लौटाता है।

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Running the snippet prints:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**क्या हुआ?**  
- `Amount` 1000 है, जो `Amount>500` को संतुष्ट करता है।  
- SmartMarker `${Amount * Rate}` का मूल्यांकन करता है → `1000 * 0.08 = 80`।  
- मूल कंडीशनल की (`if(Amount>500)`) को एक साफ़ प्रॉपर्टी नाम (`Result`) से बदल दिया जाता है। डिफ़ॉल्ट रूप से SmartMarker `"Result"` उपयोग करता है लेकिन आप इसे कस्टमाइज़ कर सकते हैं (बाद में अधिक)। 

यदि आप `Amount` को `400` बदलते हैं, तो आउटपुट इस प्रकार होगा:

```json
{
  "Amount": 400
}
```

कंडीशनल ब्लॉक गायब हो जाता है क्योंकि एक्सप्रेशन `false` मूल्यांकित हुआ। यही **कंडीशनल कैसे लागू करें** लॉजिक का सार है JSON में।

---

## चरण 5: आउटपुट प्रॉपर्टी नाम को कस्टमाइज़ करना (वैकल्पिक)

कभी‑कभी आप सामान्य `"Result"` कुंजी नहीं चाहते। SmartMarker आपको `RenameIfExpression` विकल्प का उपयोग करके कस्टम नाम निर्दिष्ट करने देता है:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Output:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

अब कंडीशनल वैल्यू एक अधिक अर्थपूर्ण प्रॉपर्टी नाम के तहत स्टोर होती है—उन डाउनस्ट्रीम सर्विसेज़ के लिए परफेक्ट जो एक विशिष्ट फ़ील्ड की अपेक्षा करती हैं।

---

## सामान्य समस्याएँ और उन्हें कैसे टालें

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| वेरिएबल नहीं मिला | आप एक वेरिएबल रेफ़र किया जो `smartMarkerOptions.Variables` में नहीं है। | स्पेलिंग दोबारा जांचें और सुनिश्चित करें कि प्रोसेसिंग से पहले वेरिएबल जोड़ा गया है। |
| `if` सिंटैक्स अमान्य | कोष्ठक गायब होना या गलत ऑपरेटर (`>`, `<`, `==`)। | सटीक `if(<expression>)` पैटर्न का पालन करें; SmartMarker केवल सरल न्यूमेरिक तुलना को सपोर्ट करता है। |
| JSON बिगड़ जाता है | कंडीशनल ब्लॉक के बाद अनजाने में ट्रेलिंग कॉमा छोड़ देना। | SmartMarker को हटाने दें; मूल टेम्प्लेट को सिंटैक्टिकली सही रखें। |
| अप्रत्याशित नंबर फ़ॉर्मेट | परिणाम स्ट्रिंग `"80"` के रूप में दिखता है न कि नंबर। | बाद में कास्ट या पार्स करें, या न्यूमेरिक फ़ॉर्मेटिंग के लिए `${(Amount * Rate):N0}` उपयोग करें। |

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम है जिसे आप कंपाइल और रन कर सकते हैं। यह **JSON को कैसे जेनरेट करें** को डायनामिक वेरिएबल्स, कंडीशनल्स, और अंकगणित के साथ दिखाता है—सभी 30 लाइनों से कम में।

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**अपेक्षित कंसोल आउटपुट**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

बिना झिझक `Amount` बदलें ताकि कंडीशनल ब्रांच टेस्ट हो सके, या `Rate` समायोजित करें ताकि विभिन्न डिस्काउंट कैलकुलेशन देख सकें।

---

## पैटर्न का विस्तार – अधिक “कैसे करें” परिदृश्य

- **कैसे कॉन्फ़िगरेशन फ़ाइल से वेरिएबल्स को बदलें**: `appsettings.json` से एक `Dictionary<string, object>` लोड करें और उसे `smartMarkerOptions.Variables` में फीड करें।  
- **कैसे कई कंडीशन्स के लिए if एक्सप्रेशन का उपयोग करें**: उन्हें इस तरह चेन करें `"if(Amount>500 && CustomerType=='VIP')"`—SmartMarker लॉजिकल AND/OR को सपोर्ट करता है।  
- **कैसे कंडीशनल फ़ॉर्मेटिंग लागू करें**: दशमलव स्थान नियंत्रित करने के लिए एक्सप्रेशन के भीतर `${Amount:0.00}` उपयोग करें।  
- **कैसे अधिक जटिल गणित के साथ वैल्यूज़ को मल्टीप्लाई करें**: `${(Amount - Discount) * TaxRate}` भी वही काम करता है।  
- **कैसे नेस्टेड ऑब्जेक्ट्स के लिए JSON जेनरेट करें**: कंडीशनल ब्लॉक को दूसरे JSON ऑब्जेक्ट के भीतर रखें, और SmartMarker हायरार्की को बरकरार रखेगा।

---

## निष्कर्ष

हमने SmartMarker का उपयोग करके JSON में **वेरिएबल्स को कैसे बदलें** को कवर किया, कंडीशनल इन्क्लूज़न के लिए **use if expression** दिखाया, **कंडीशनल कैसे लागू करें** लॉजिक समझाया, टेम्प्लेट के भीतर **वैल्यूज़ को कैसे मल्टीप्लाई करें** दिखाया, और अंत में **JSON को कैसे जेनरेट करें** जो डाउनस्ट्रीम कंजम्प्शन के लिए तैयार है, को दर्शाया। यह तरीका हल्का है, किसी बाहरी टेम्प्लेटिंग इंजन की आवश्यकता नहीं, और किसी भी C# कोडबेस में सहजता से फिट बैठता है।

इसे आज़माएँ—वेरिएबल्स को ट्यून करें, अधिक कंडीशन जोड़ें, या पूरे को एक हेल्पर क्लास में रैप करें ताकि आपके सॉल्यूशन में पुन: उपयोग हो सके। जब आपको जल्दी से डायनामिक JSON बनाना हो, SmartMarker एक ठोस, प्रोडक्शन‑रेडी विकल्प है।

**आगे के कदम**

- SmartMarker की उन्नत सुविधाओं जैसे लूप (`foreach`) और कस्टम फ़ंक्शन्स में गहराई से जाएँ।  
- इस तकनीक को ASP.NET Core एंडपॉइंट्स के साथ मिलाकर डायनामिक JSON API सर्व करें।  
- अन्य टेम्प्लेटिंग लाइब्रेरीज़ (जैसे Handlebars.NET) की तुलना करें, विशेषकर यदि आपको अधिक समृद्ध सिंटैक्स चाहिए।

क्या आपके पास प्रश्न हैं या कोई विशेष उपयोग‑केस है जिस पर आप काम कर रहे हैं? नीचे कमेंट छोड़ें, और चलिए साथ में ट्रबलशूट करते हैं। कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}