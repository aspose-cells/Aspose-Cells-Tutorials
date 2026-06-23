---
category: general
date: 2026-03-18
description: नया वर्कबुक बनाएं और एक्सेल को TXT में निर्यात करें जबकि संख्यात्मक सटीकता
  को बनाए रखें। जानें कि वर्कशीट को TXT के रूप में कैसे सहेजें और वर्कशीट को प्रभावी
  ढंग से TXT में कैसे परिवर्तित करें।
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: hi
og_description: नया वर्कबुक बनाएं और सटीकता के साथ एक्सेल को TXT में निर्यात करें।
  यह ट्यूटोरियल दिखाता है कि कैसे वर्कशीट को TXT के रूप में सहेजा जाए और C# का उपयोग
  करके वर्कशीट को TXT में परिवर्तित किया जाए।
og_title: नया वर्कबुक बनाएं – एक्सेल को TXT में निर्यात करने की गाइड
tags:
- Aspose.Cells
- C#
- Excel automation
title: नया वर्कबुक बनाएं – पूर्ण सटीकता के साथ एक्सेल को TXT में निर्यात करें
url: /hi/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# नया वर्कबुक बनाएं – पूर्ण सटीकता के साथ Excel को TXT में निर्यात करें

क्या आपको कभी C# में **create new workbook** बनाकर डेटा को साधारण‑पाठ फ़ाइल में डालने की ज़रूरत पड़ी है? शायद आप किसी लेगेसी सिस्टम से रिपोर्ट निकाल रहे हैं और नीचे की टूल केवल `.txt` फ़ीड स्वीकार करती है। अच्छी खबर? आपको संख्यात्मक सटीकता का बलिदान नहीं करना पड़ेगा, और आपको CSV स्ट्रिंग्स को हाथ से बनाना भी नहीं पड़ेगा।

इस गाइड में हम **export excel to txt** की पूरी प्रक्रिया को समझेंगे, जिसमें वर्कबुक को इनिशियलाइज़ करने से लेकर जब आप **save worksheet as txt** करते हैं तो ट्रेलिंग ज़ीरो को संरक्षित रखने तक सब कुछ शामिल है। अंत तक आपके पास एक तैयार‑चलाने योग्य स्निपेट होगा जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं—कोई अतिरिक्त यूटिलिटी की आवश्यकता नहीं।

## आपको क्या चाहिए

- **ASP.NET/ .NET 6+** (कोड .NET Framework 4.6+ पर भी काम करता है)  
- **Aspose.Cells for .NET** – वह लाइब्रेरी जो `Workbook`, `Worksheet`, और `TxtSaveOptions` क्लासेज़ को शक्ति देती है। आप इसे NuGet से `Install-Package Aspose.Cells` के साथ प्राप्त कर सकते हैं।  
- C# की बुनियादी समझ (यदि आप `using` स्टेटमेंट्स से सहज हैं, तो आप तैयार हैं)।  

बस इतना ही—कोई Excel इंटरऑप नहीं, कोई COM ऑब्जेक्ट नहीं, और निश्चित रूप से कोई मैन्युअल स्ट्रिंग कंकैटनेशन नहीं।

---

## चरण 1: नया वर्कबुक इनिशियलाइज़ करें (Primary Keyword)

पहला काम जो आपको करना है वह है **create new workbook**। वर्कबुक को एक खाली कैनवास की तरह सोचें जहाँ आप बाद में संख्याएँ, टेक्स्ट या फ़ॉर्मूले पेस्ट करेंगे।

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **क्यों यह महत्वपूर्ण है:** `Workbook` को बिना किसी फ़ाइल को लोड किए इंस्टैंशिएट करने से आपको एक साफ़ स्लेट मिलता है। फिर आप प्रोग्रामेटिकली डेटा जोड़ सकते हैं, जो **convert worksheet to txt** परिदृश्यों के लिए आदर्श है जहाँ आपके पास मौजूदा `.xlsx` नहीं है।

---

## चरण 2: सेल्स को भरें – ट्रेलिंग ज़ीरो को रखें

संख्याओं को टेक्स्ट में डंप करते समय एक सामान्य समस्या ट्रेलिंग ज़ीरो (`123.45000` बन जाता है `123.45`) खो देना है। यदि डाउनस्ट्रीम सिस्टम फिक्स्ड‑विथ फ़ील्ड्स पर निर्भर हैं, तो यह नुकसान सब कुछ बिगाड़ सकता है।

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **प्रो टिप:** `PutValue` स्वचालित रूप से डेटा टाइप का अनुमान लगाता है। यदि आपको ऐसा स्ट्रिंग चाहिए जो संख्या जैसा दिखे, तो `PutValue("123.45000")` का उपयोग करें।

---

## चरण 3: TXT सेव ऑप्शन्स कॉन्फ़िगर करें – संख्यात्मक सटीकता को संरक्षित रखें

यहीं पर जादू होता है। `PreserveNumericPrecision` को टॉगल करके, आप Aspose.Cells को वह सटीक मान लिखने के लिए निर्देश देते हैं जो आपने दर्ज किया है, जिसमें कोई भी अप्रासंगिक ट्रेलिंग ज़ीरो शामिल है।

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **यह क्यों सक्षम करें?** जब आप **save excel as txt** करते हैं, तो डिफ़ॉल्ट व्यवहार अनावश्यक दशमलव को काट देता है। `PreserveNumericPrecision = true` सेट करने से आउटपुट सेल के प्रदर्शित मान को प्रतिबिंबित करता है, जो वित्तीय रिपोर्ट या वैज्ञानिक डेटा के लिए महत्वपूर्ण है।

---

## चरण 4: वर्कशीट को TXT के रूप में सेव करें – अंतिम निर्यात

अब हम वास्तव में **save worksheet as txt** करेंगे। आप पाथ को किसी भी स्थान पर सेट कर सकते हैं जहाँ आपके पास लिखने की अनुमति हो; उदाहरण में `output` नामक एक रिलेटिव फ़ोल्डर का उपयोग किया गया है।

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **अपेक्षित आउटपुट** (`num-preserve.txt`):

```
123.45000
```

ध्यान दें कि ट्रेलिंग ज़ीरो बरकरार हैं—बिल्कुल वही जो आपने माँगा था।

---

## चरण 5: परिणाम की पुष्टि करें – त्वरित जांच

प्रोग्राम चलने के बाद, किसी भी टेक्स्ट एडिटर में `num-preserve.txt` खोलें। आपको एकल लाइन `123.45000` दिखनी चाहिए। यदि आप `123.45` देखते हैं, तो दोबारा जांचें कि `PreserveNumericPrecision` `true` पर सेट है और आप Aspose.Cells (v23.10+) का नवीनतम संस्करण उपयोग कर रहे हैं।

---

## सामान्य विविधताएँ और किनारे के मामलों

### कई सेल्स या रेंजेज़ निर्यात करना

यदि आपको पूरे रेंज के लिए **export excel to txt** करना है, तो सेव करने से पहले बस अधिक सेल्स भरें:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose डिफ़ॉल्ट रूप से प्रत्येक सेल को नई लाइन पर लिखेगा। आप `txtSaveOptions.Separator` के माध्यम से डिलिमिटर (टैब, कॉमा) भी बदल सकते हैं।

### विभिन्न एन्कोडिंग्स के साथ वर्कशीट को TXT में बदलना

कभी-कभी डाउनस्ट्रीम सिस्टम को UTF‑8 BOM या ASCII की आवश्यकता होती है। एन्कोडिंग को इस प्रकार समायोजित करें:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### बड़े वर्कबुक को संभालना

जब बड़ी शीट्स (सैकड़ों हज़ार पंक्तियों) से निपट रहे हों, तो आउटपुट को स्ट्रीम करने पर विचार करें:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## प्रो टिप्स और गॉटचाज़

- **`Save` कॉल करने से पहले आउटपुट डायरेक्टरी बनाना न भूलें**, अन्यथा आपको `DirectoryNotFoundException` मिलेगा।  
- **लोकैल‑विशिष्ट दशमलव सेपरेटर पर ध्यान दें**। यदि आपका वातावरण कॉमा (`1,23`) उपयोग करता है, तो डॉट लागू करने के लिए `txtSaveOptions.DecimalSeparator = '.'` सेट करें।  
- **वर्ज़न संगतता**: `PreserveNumericPrecision` फ़्लैग Aspose.Cells 20.6 में पेश किया गया था। यदि आप पुराने वर्ज़न पर हैं, तो यह फ़्लैग मौजूद नहीं होगा और आपको सेव करने से पहले सेल को टेक्स्ट के रूप में फॉर्मेट करना पड़ेगा।

![नया वर्कबुक बनाने का उदाहरण](excel-to-txt.png "नया वर्कबुक बनाएं")

*छवि वैकल्पिक पाठ: "नया वर्कबुक बनाएं और संख्यात्मक सटीकता संरक्षित रखते हुए Excel को TXT में निर्यात करें"*

---

## पुनरावलोकन – हमने क्या कवर किया

- **Create new workbook** का उपयोग Aspose.Cells के साथ किया।  
- एक सेल को ट्रेलिंग ज़ीरो सहित संख्या से भरें।  
- `TxtSaveOptions.PreserveNumericPrecision = true` सेट करें ताकि **save excel as txt** करते समय सटीकता न खोएँ।  
- फ़ाइल को डिस्क पर लिखें, यह सत्यापित करते हुए कि आउटपुट मूल मान से मेल खाता है।  

यह पूरी **convert worksheet to txt** वर्कफ़्लो है, जो C# की 50 लाइनों से कम में पूरी हो जाती है।

---

## अगले कदम और संबंधित विषय

अब जब आप **export excel to txt** को पूर्ण सटीकता के साथ कर सकते हैं, तो आप निम्नलिखित का अन्वेषण करना चाहेंगे:

- कस्टम डिलिमिटर (`TxtSaveOptions.Separator`) के साथ **Exporting to CSV**।  
- TSV (`SaveFormat.TabDelimited`) जैसे अन्य प्लेन‑टेक्स्ट फ़ॉर्मेट में **Saving as other plain‑text formats**।  
- `Directory.GetFiles` का उपयोग करके फ़ोल्डर में कई वर्कबुक्स की **Batch processing**।  
- क्लाउड में ऑन‑डिमांड कन्वर्ज़न के लिए **Integrating with Azure Functions**।

इनमें से प्रत्येक समान `Workbook` → `Worksheet` → `TxtSaveOptions` पैटर्न पर आधारित है, इसलिए आपको यह सहज लगेगा।

---

### अंतिम विचार

यदि आप साथ रहे हैं, तो अब आप बिल्कुल जानते हैं कि **create new workbook** कैसे करें, उसे भरें, और **save worksheet as txt** कैसे करें जबकि आप जिस भी दशमलव अंक को चाहते हैं उसे बरकरार रखें। यह कोड का एक छोटा टुकड़ा है, लेकिन यह एक आश्चर्यजनक रूप से सामान्य समस्या को हल करता है जब लेगेसी पाइपलाइन प्लेन‑टेक्स्ट इनपुट की मांग करती हैं।

इसे आज़माएँ, विकल्पों को समायोजित करें, और डेटा को बिल्कुल उसी तरह प्रवाहित होने दें जैसा आप चाहते हैं। कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}