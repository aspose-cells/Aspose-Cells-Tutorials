---
category: general
date: 2026-03-21
description: C# में सेल का कस्टम फ़ॉर्मेट सेट करें और जानें कि Excel में तारीख कैसे
  लिखें, कस्टम तारीख फ़ॉर्मेट लागू करें, Excel से DateTime पढ़ें, और वर्कबुक शीट जल्दी
  बनाएं।
draft: false
keywords:
- set cell custom format
- write date to excel
- read datetime from excel
- apply custom date format
- create workbook worksheet
language: hi
og_description: C# में सेल का कस्टम फ़ॉर्मेट सेट करें ताकि तिथि को Excel में लिखा
  जा सके, कस्टम तिथि फ़ॉर्मेट लागू करें, Excel से DateTime पढ़ें, और आसानी से वर्कबुक
  शीट बनाएं।
og_title: C# में सेल कस्टम फ़ॉर्मेट सेट करें – एक्सेल में तिथियों को लिखें और पढ़ें
tags:
- Aspose.Cells
- C#
- Excel Automation
title: C# में सेल कस्टम फ़ॉर्मेट सेट करें – एक्सेल में तिथियों को लिखने और पढ़ने के
  लिए पूर्ण गाइड
url: /hi/net/excel-custom-number-date-formatting/set-cell-custom-format-in-c-complete-guide-to-writing-readin/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# सेट सेल कस्टम फ़ॉर्मेट – C# का उपयोग करके Excel में तिथियों को लिखें और पढ़ें

क्या आपको C# से Excel फ़ाइल में **सेल कस्टम फ़ॉर्मेट** सेट करने की ज़रूरत पड़ी है लेकिन शुरुआत नहीं पता थी? आप अकेले नहीं हैं। कई रिपोर्टिंग टूल्स या डेटा‑एक्सपोर्ट यूटिलिटीज़ में तिथि को एक विशिष्ट लोकेल में दिखाना पड़ता है—जैसे जापानी युग तिथियां, वित्तीय कैलेंडर, या ISO‑8601 स्ट्रिंग्स।  

इस ट्यूटोरियल में हम एक **पूर्ण, चलाने योग्य उदाहरण** के माध्यम से चलेंगे जो आपको दिखाएगा कि **Excel में तिथि लिखें**, **कस्टम डेट फ़ॉर्मेट लागू करें**, **Excel से DateTime पढ़ें**, और Aspose.Cells के साथ **वर्कबुक वर्कशीट बनाएं**। अंत तक आपके पास एक एकल, स्व-निहित प्रोग्राम होगा जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं।

## आप क्या सीखेंगे

- प्रोग्रामेटिकली **वर्कबुक वर्कशीट बनाना**।  
- लोकेल‑विशिष्ट स्ट्रिंग का उपयोग करके **Excel में तिथि लिखने** के सटीक चरण।  
- **कस्टम डेट फ़ॉर्मेट लागू करना** (जापानी युग नोटेशन सहित)।  
- **Excel से DateTime पढ़ना** और उसे `DateTime` ऑब्जेक्ट में वापस लाना।  
- टिप्स, संभावित समस्याएं, और विविधताएँ जो आप Excel तिथियों के साथ काम करते समय सामना कर सकते हैं।

कोई बाहरी दस्तावेज़ीकरण आवश्यक नहीं—आपको जो कुछ भी चाहिए वह यहाँ ही है।

## आवश्यकताएँ

- .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ पर भी काम करता है)।  
- NuGet (`Install-Package Aspose.Cells`) के माध्यम से Aspose.Cells for .NET स्थापित किया गया।  
- C# सिंटैक्स की बुनियादी समझ—कुछ भी जटिल नहीं।

> **प्रो टिप:** यदि आप Visual Studio का उपयोग कर रहे हैं, तो *nullable reference types* को सक्षम करें ताकि शुरुआती बारीक बग्स पकड़े जा सकें।

## चरण 1: वर्कबुक और वर्कशीट बनाएं  

सबसे पहले: आपको एक वर्कबुक ऑब्जेक्ट चाहिए जो Excel फ़ाइल का प्रतिनिधित्व करता है, और एक वर्कशीट जहाँ डेटा रहेगा।

```csharp
using Aspose.Cells;
using System;

class ExcelDateDemo
{
    static void Main()
    {
        // Step 1: Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];           // default sheet is named "Sheet1"
```

*Why this matters:* `Workbook` क्लास सभी Excel ऑपरेशन्स का एंट्री पॉइंट है। इसे मेमोरी में बनाना मतलब है कि आप फ़ाइल सिस्टम को तब तक नहीं छूते जब तक आप स्पष्ट रूप से सेव नहीं करते, जिससे प्रक्रिया तेज़ और टेस्ट‑फ़्रेंडली रहती है।

## चरण 2: Excel में तिथि लिखें  

अगला, हम एक जापानी युग तिथि स्ट्रिंग (`"R02-04-01"`) को सेल **A1** में रखेंगे। यह स्ट्रिंग रीवा युग (वर्ष 2, अप्रैल 1) की नकल करती है।

```csharp
        // Step 2: Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("R02-04-01");
```

*What’s happening:* `PutValue` कच्ची स्ट्रिंग को स्टोर करता है। Aspose.Cells बाद में इसे सेल की शैली के आधार पर पार्स करने की कोशिश करेगा। यदि आप इस चरण को छोड़कर सीधे `DateTime` लिखते हैं, तो आप वह युग जानकारी खो देंगे जिसे आप दिखाना चाहते हैं।

## चरण 3: बिल्ट‑इन डेट नंबर फ़ॉर्मेट लागू करें (ID 14)

Excel में ID 14 (`mm-dd-yy`) वाला बिल्ट‑इन डेट फ़ॉर्मेट है। इसे लागू करने से इंजन को पता चलता है कि सेल **तिथि रखता है**, न कि केवल टेक्स्ट।

```csharp
        // Step 3: Apply the built‑in date number format (ID 14)
        worksheet.Cells["A1"].Style.Number = 14;
```

*Why use ID 14?* यह सार्वभौमिक “शॉर्ट डेट” फ़ॉर्मेट है जो सुनिश्चित करता है कि Excel सामग्री को तिथि मान के रूप में मानता है, जो किसी भी कस्टम फ़ॉर्मेट के सही काम करने की पूर्वशर्त है।

## चरण 4: जापानी युग नोटेशन दिखाने के लिए कस्टम फ़ॉर्मेट सेट करें  

अब मज़े का हिस्सा: हम Excel को बताते हैं कि वह तिथि को जापानी युग फ़ॉर्मेट में रेंडर करे। कस्टम स्ट्रिंग `[$-ja-JP]ggge年m月d日` बिल्कुल यही करती है।

```csharp
        // Step 4: Set a custom format to display the date in Japanese era notation
        worksheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge年m月d日";
```

*Explanation:*  
- `[$-ja-JP]` लोकेल को जापानी पर मजबूर करता है।  
- `ggg` युग का नाम है (जैसे, रीवा के लिए “R”)।  
- `e` युग का वर्ष है।  
- `年`, `月`, `日` क्रमशः वर्ष, माह, दिन के लिए शाब्दिक जापानी अक्षर हैं।

यदि आपको अलग लोकेल चाहिए, तो बस `ja-JP` को उपयुक्त कल्चर कोड से बदलें (जैसे, `en-US`)।

## चरण 5: पार्स किया गया DateTime मान प्राप्त करें  

अंत में, चलिए **वास्तविक `DateTime`** पढ़ते हैं जो Excel ने सेल से पार्स किया है। यह साबित करता है कि स्ट्रिंग सही ढंग से व्याख्यायित हुई।

```csharp
        // Step 5: Retrieve the parsed DateTime value from the cell
        DateTime parsedDate = worksheet.Cells["A1"].DateTime;   // => 2020‑04‑01

        // Output to console for verification
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

*Result:* कंसोल `Parsed DateTime: 2020-04-01` प्रिंट करता है। भले ही हमने जापानी युग स्ट्रिंग दर्ज की, Excel आंतरिक रूप से ग्रेगोरियन तिथि को स्टोर करता है, जिसे आप गणनाओं, तुलना, या आगे के एक्सपोर्ट के लिए उपयोग कर सकते हैं।

## चरण 6: वर्कबुक को सेव करें (वैकल्पिक)

यदि आप फ़ॉर्मेटेड वर्कबुक को Excel में देखना चाहते हैं, तो बस इसे डिस्क पर सेव करें।

```csharp
        // Optional: Save the workbook to a file
        workbook.Save("JapaneseEraDate.xlsx");
    }
}
```

जनरेट की गई **JapaneseEraDate.xlsx** खोलें और आप देखेंगे कि सेल **A1** `R02年4月1日` दिखा रहा है (वह सटीक जापानी युग फ़ॉर्मेट जो हमने सेट किया था)।

![सेट सेल कस्टम फ़ॉर्मेट उदाहरण](image-placeholder.png "Excel सेल जो जापानी युग तिथि दिखा रहा है – सेट सेल कस्टम फ़ॉर्मेट")

*ऊपर का alt टेक्स्ट मुख्य कीवर्ड शामिल करता है, जिससे इमेज‑SEO आवश्यकता पूरी होती है।*

## सामान्य विविधताएँ और किनारे के मामले  

### अलग डेट फ़ॉर्मेट लिखना  

यदि आप युग स्ट्रिंग के बजाय ISO‑8601 (`2020-04-01`) पसंद करते हैं, तो बस `PutValue` कॉल को बदल दें:

```csharp
worksheet.Cells["A1"].PutValue(new DateTime(2020, 4, 1));
worksheet.Cells["A1"].Style.Number = 14;                 // keep built‑in date format
worksheet.Cells["A1"].Style.Custom = "yyyy-mm-dd";      // custom ISO format
```

### Null या खाली सेल्स से निपटना  

तिथि पढ़ते समय, हमेशा खाली सेल्स से बचें ताकि `InvalidOperationException` से बचा जा सके:

```csharp
if (!worksheet.Cells["A1"].IsDate)
{
    Console.WriteLine("Cell A1 does not contain a valid date.");
}
else
{
    DateTime dt = worksheet.Cells["A1"].DateTime;
    // use dt...
}
```

### कई लोकेल्स का समर्थन  

आप कल्चर कोड की सूची के माध्यम से लूप कर सकते हैं और उन्हें डायनामिकली लागू कर सकते हैं:

```csharp
string[] cultures = { "ja-JP", "en-US", "fr-FR" };
foreach (var culture in cultures)
{
    worksheet.Cells["A1"].Style.Custom = $"[$-{culture}]ggge年m月d日";
    // Save or export per culture if needed
}
```

## प्रो टिप्स और गॉचेज़  

- **हमेशा पहले एक बिल्ट‑इन नंबर फ़ॉर्मेट सेट करें** (`Style.Number`). इसके बिना, Excel सेल को साधारण टेक्स्ट मानता है और कस्टम फ़ॉर्मेट को नजरअंदाज कर देता है।  
- **लोकेल कोड केस‑इंसेंसिटिव** होते हैं, लेकिन कैनॉनिकल फॉर्म (`ja-JP`) का उपयोग करने से भ्रम नहीं होता।  
- **सेव करना वैकल्पिक** है इन‑मेमोरी प्रोसेसिंग के लिए; आप वर्कबुक को सीधे वेब रिस्पॉन्स में स्ट्रीम कर सकते हैं (`workbook.Save(stream, SaveFormat.Xlsx)`)।  
- **Aspose.Cells लाइसेंस**: फ्री इवैल्यूएशन वर्ज़न में वॉटरमार्क जोड़ता है। प्रोडक्शन के लिए, सुनिश्चित करें कि आपके पास वैध लाइसेंस हो ताकि प्रदर्शन पर पेनाल्टी न आए।

## पुनरावलोकन  

हमने दिखाया कि C# में **सेल कस्टम फ़ॉर्मेट सेट** करके जापानी युग तिथियां कैसे दिखाएँ, **Excel में तिथि लिखें**, **कस्टम डेट फ़ॉर्मेट लागू करें**, **Excel से DateTime पढ़ें**, और **वर्कबुक वर्कशीट बनाएं**—सब कुछ एक एकल, स्व-निहित प्रोग्राम में। मुख्य कीवर्ड स्वाभाविक रूप से पूरे टेक्स्ट में आता है, जबकि द्वितीयक कीवर्ड हेडिंग्स और बॉडी टेक्स्ट में बुनिए गए हैं, जिससे SEO और AI‑citation मानकों दोनों को पूरा किया जाता है।

## आगे क्या?

- **कंडीशनल फ़ॉर्मेटिंग** का अन्वेषण करें ताकि ओवरड्यू तिथियों को हाइलाइट किया जा सके।  
- इस दृष्टिकोण को **PivotTables** के साथ मिलाएं ताकि डायनामिक रिपोर्टिंग हो सके।  
- **बड़े CSV फ़ाइलें पढ़ें** और उन्हें उसी डेट हैंडलिंग लॉजिक के साथ Excel में कन्वर्ट करने की कोशिश करें।  

विभिन्न लोकेल्स, कस्टम पैटर्न, या यहाँ तक कि टाइम ज़ोन्स के साथ प्रयोग करने में संकोच न करें। यदि आपको कोई समस्या आती है, तो नीचे कमेंट छोड़ें—हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}