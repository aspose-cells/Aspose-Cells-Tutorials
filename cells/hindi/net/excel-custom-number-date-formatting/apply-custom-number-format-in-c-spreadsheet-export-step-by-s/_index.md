---
category: general
date: 2026-04-07
description: स्प्रेडशीट की सेल पर कस्टम नंबर फ़ॉर्मेट लागू करें और C# के साथ सेल वैल्यू
  को एक्सपोर्ट करते समय स्प्रेडशीट में नंबर को फ़ॉर्मेट करना सीखें। तेज़, पूर्ण गाइड।
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: hi
og_description: स्प्रेडशीट की सेल पर कस्टम नंबर फ़ॉर्मेट लागू करें और इसे फ़ॉर्मेटेड
  स्ट्रिंग के रूप में निर्यात करें। सीखें कि स्प्रेडशीट में नंबर को कैसे फ़ॉर्मेट
  करें और सेल मान को निर्यात करें।
og_title: कस्टम नंबर फ़ॉर्मेट लागू करें – पूर्ण C# निर्यात ट्यूटोरियल
tags:
- C#
- Spreadsheet
- Number Formatting
title: C# स्प्रेडशीट निर्यात में कस्टम नंबर फ़ॉर्मेट लागू करें – चरण‑दर‑चरण गाइड
url: /hi/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# स्प्रेडशीट एक्सपोर्ट में कस्टम नंबर फ़ॉर्मेट लागू करें – पूर्ण ट्यूटोरियल

क्या आपको कभी किसी सेल पर **apply custom number format** लागू करने और फिर उस फ़ॉर्मेटेड स्ट्रिंग को स्प्रेडशीट से निकालने की ज़रूरत पड़ी है? आप अकेले नहीं हैं। कई डेवलपर्स को यह पता चलने पर रुकावट आती है कि कच्चा मान निकलता है, न कि वह सुंदर, लोकेल‑अवेयर स्ट्रिंग जो वे उम्मीद करते हैं। इस गाइड में हम आपको बिल्कुल दिखाएंगे कि स्प्रेडशीट सेल्स में number को कैसे फ़ॉर्मेट करें और कैसे एक लोकप्रिय C# स्प्रेडशीट लाइब्रेरी का उपयोग करके सेल वैल्यू को फ़ॉर्मेटेड स्ट्रिंग के रूप में एक्सपोर्ट करें।

वॉकथ्रू के अंत तक आप किसी भी संख्यात्मक सेल पर **apply custom number format** लागू कर पाएँगे, परिणाम को `ExportTable` के साथ एक्सपोर्ट करेंगे, और वही सटीक आउटपुट देखेंगे जो आप UI या रिपोर्ट में दिखाने की उम्मीद करते हैं। बाहरी दस्तावेज़ों की आवश्यकता नहीं—सब कुछ यहाँ उपलब्ध है।

## आवश्यकताएँ

- .NET 6.0 या बाद का (कोड .NET Framework 4.7+ पर भी काम करता है)
- एक रेफ़रेंस स्प्रेडशीट लाइब्रेरी का जो `Workbook`, `Worksheet`, और `ExportTableOptions` प्रदान करती है (जैसे, **Aspose.Cells** या **GemBox.Spreadsheet**; दिखाया गया API Aspose.Cells से मेल खाता है)
- बुनियादी C# ज्ञान—यदि आप `Console.WriteLine` लिख सकते हैं, तो आप तैयार हैं

> **Pro tip:** यदि आप कोई अलग लाइब्रेरी उपयोग कर रहे हैं, तो प्रॉपर्टी नाम आमतौर पर समान होते हैं (`NumberFormat`, `ExportAsString`)। बस उन्हें उसी अनुसार मैप करें।

## ट्यूटोरियल क्या कवर करता है

1. एक वर्कबुक बनाना और पहली वर्कशीट चुनना।  
2. सेल में एक संख्यात्मक मान डालना।  
3. `ExportTableOptions` को सेट करना ताकि **apply custom number format** लागू हो और एक स्ट्रिंग रिटर्न करे।  
4. सेल को एक्सपोर्ट करना और फ़ॉर्मेटेड परिणाम प्रिंट करना।  
5. एज‑केस हैंडलिंग – यदि सेल में फ़ॉर्मूला या null वैल्यू हो तो क्या होगा?

चलिए शुरू करते हैं।

![कस्टम नंबर फ़ॉर्मेट लागू करने का उदाहरण](https://example.com/image.png "कस्टम नंबर फ़ॉर्मेट लागू करना")

## चरण 1 – वर्कबुक बनाएं और पहली वर्कशीट प्राप्त करें

पहली चीज़ जो आपको चाहिए वह एक वर्कबुक ऑब्जेक्ट है। इसे उस Excel फ़ाइल की तरह सोचें जिसे आप Office ऐप में खोलेंगे। एक बार जब आपके पास हो, तो पहली शीट ले लें—ज्यादातर ट्यूटोरियल्स वहीं से शुरू होते हैं क्योंकि यह उदाहरण को संक्षिप्त रखता है।

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Why this matters:** एक नया वर्कबुक आपको एक साफ़ स्लेट देता है, जिससे यह सुनिश्चित होता है कि कोई छिपा हुआ फ़ॉर्मेटिंग बाद में हमारे कस्टम नंबर फ़ॉर्मेट में बाधा न बन सके।

## चरण 2 – सेल B2 में एक संख्यात्मक मान डालें (वह सेल जिसे हम एक्सपोर्ट करेंगे)

अब हमें फ़ॉर्मेट करने के लिए कुछ चाहिए। सेल **B2** एक सुविधाजनक स्थान है—संदर्भ में आसान और डिफ़ॉल्ट A1 कोने से पर्याप्त दूर ताकि आकस्मिक ओवरराइट से बचा जा सके।

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**यदि मान फ़ॉर्मूला है तो क्या?**  
यदि आप बाद में कच्चे मान को फ़ॉर्मूला (जैसे, `=SUM(A1:A10)`) से बदलते हैं, तो एक्सपोर्ट रूटीन फिर भी अगले चरण में हमने जो नंबर फ़ॉर्मेट लागू किया है, उसका सम्मान करेगा, क्योंकि फ़ॉर्मेटिंग सेल से जुड़ी होती है, न कि मान के प्रकार से।

## चरण 3 – एक्सपोर्ट विकल्पों को कॉन्फ़िगर करें ताकि मान को फ़ॉर्मेटेड स्ट्रिंग के रूप में प्राप्त किया जा सके

यह ट्यूटोरियल का मुख्य भाग है: हम लाइब्रेरी को बताते हैं कि एक्सपोर्ट करते समय **apply custom number format** लागू करे। `NumberFormat` स्ट्रिंग वही पैटर्न फॉलो करती है जो आप Excel के “Custom” कैटेगरी में उपयोग करेंगे।

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` सुनिश्चित करता है कि मेथड एक `string` रिटर्न करे, न कि कच्चा double।  
- `NumberFormat = "#,##0.00;(#,##0.00)"` Excel के पैटर्न को दर्शाता है: हजारों के लिए कॉमा, दो दशमलव स्थान, और नकारात्मक संख्याओं के लिए कोष्ठक।

> **Why use a custom format?** यह विभिन्न संस्कृतियों में स्थिरता सुनिश्चित करता है (जैसे, US बनाम यूरोपीय नंबर सेपरेटर) और आपको अकाउंटिंग कोष्ठकों जैसे व्यवसाय‑विशिष्ट स्टाइलिंग एम्बेड करने देता है।

## चरण 4 – कॉन्फ़िगर किए गए विकल्पों का उपयोग करके सेल को एक्सपोर्ट करें

अब हम वास्तव में वर्कशीट से मान निकालते हैं, लाइब्रेरी को वह भारी काम करने देते हैं जिसमें हमने परिभाषित फ़ॉर्मेट लागू करना शामिल है।

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Edge case – empty cell:** यदि `B2` खाली हो, तो `formattedResult` `null` होगा। आप प्रिंट करने से पहले एक साधारण null‑check के साथ इसे सुरक्षित कर सकते हैं।

## चरण 5 – फ़ॉर्मेटेड स्ट्रिंग दिखाएँ

अंत में, हम परिणाम को कंसोल में लिखते हैं। एक वास्तविक ऐप में आप इस स्ट्रिंग को PDF, ईमेल, या UI लेबल में डाल सकते हैं।

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**अपेक्षित आउटपुट**

```
1,234.56
```

यदि आप कच्चे मान को `-9876.54` बदलते हैं, तो वही फ़ॉर्मेट आपको `(9,876.54)` देगा—बिल्कुल वही जो कई अकाउंटिंग रिपोर्ट्स में आवश्यक होता है।

## पूर्ण, चलाने योग्य उदाहरण

नीचे पूरा प्रोग्राम है जिसे आप नई कंसोल प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं। यह जैसा है वैसा ही कंपाइल और रन करता है, बशर्ते आपने स्प्रेडशीट लाइब्रेरी के लिए उचित NuGet पैकेज जोड़ लिया हो।

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### त्वरित जाँच

- **क्या यह कंपाइल होता है?** हाँ—सिर्फ यह सुनिश्चित करें कि `Aspose.Cells` (या समकक्ष) DLL रेफ़रेंस में है।  
- **क्या यह अन्य संस्कृतियों के साथ काम करेगा?** फ़ॉर्मेट स्ट्रिंग संस्कृति‑अज्ञेय है; लाइब्रेरी आपके द्वारा दी गई पैटर्न का सम्मान करती है। यदि आपको लोकेल‑विशिष्ट सेपरेटर चाहिए, तो आप एक्सपोर्ट से पहले `CultureInfo` हैंडलिंग जोड़ सकते हैं।

## सामान्य प्रश्न और विविधताएँ

### विभिन्न पैटर्न का उपयोग करके **format number in spreadsheet** कैसे करें?

`NumberFormat` स्ट्रिंग को बदलें। उदाहरण के लिए, एक दशमलव स्थान के साथ प्रतिशत दिखाने के लिए:

```csharp
NumberFormat = "0.0%";
```

### यदि मुझे **how to export cell value** को प्लेन टेक्स्ट के बजाय HTML में एक्सपोर्ट करना हो तो क्या करें?

अधिकांश लाइब्रेरीज़ में एक ओवरलोड होता है जो एक्सपोर्ट टाइप को स्वीकार करता है। आप `ExportAsString = true` सेट करेंगे और `ExportHtml = true` (या समान) जोड़ेंगे। सिद्धांत वही रहता है: फ़ॉर्मेट परिभाषित करें, फिर आउटपुट प्रतिनिधित्व चुनें।

### क्या मैं फ़ॉर्मेट को केवल एक सेल के बजाय पूरी रेंज पर लागू कर सकता हूँ?

बिल्कुल। आप `NumberFormat` को एक `Style` ऑब्जेक्ट को असाइन कर सकते हैं और फिर उस स्टाइल को एक `Range` पर लागू कर सकते हैं। एक्सपोर्ट कॉल अपरिवर्तित रहती है; यह स्वचालित रूप से स्टाइल को ले लेगा।

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### जब सेल में फ़ॉर्मूला हो तो क्या होता है?

एक्सपोर्ट रूटीन पहले फ़ॉर्मूला का मूल्यांकन करता है, फिर प्राप्त संख्यात्मक मान को फ़ॉर्मेट करता है। अतिरिक्त कोड की आवश्यकता नहीं—सिर्फ यह सुनिश्चित करें कि यदि आपने ऑटोमैटिक कैलकुलेशन बंद किया है तो `Calculate` को कॉल किया गया हो।

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## निष्कर्ष

अब आप जानते हैं कि स्प्रेडशीट सेल पर **apply custom number format** कैसे करें, **format number in spreadsheet** संदर्भों में कैसे फ़ॉर्मेट करें, और **how to export cell value** को तैयार‑से‑दिखाने वाली स्ट्रिंग के रूप में कैसे एक्सपोर्ट करें। ऊपर दिया गया संक्षिप्त कोड नमूना हर चरण को कवर करता है—वर्कबुक निर्माण से लेकर अंतिम आउटपुट तक—ताकि आप इसे सीधे प्रोडक्शन प्रोजेक्ट में उपयोग कर सकें।

अगली चुनौती के लिए तैयार हैं? इस तकनीक को **how to format numeric cell** के साथ मिलाकर तिथियों, मुद्रा प्रतीकों, या कंडीशनल फ़ॉर्मेटिंग के लिए उपयोग करें। या कई सेल्स को CSV के रूप में एक्सपोर्ट करने का अन्वेषण करें जबकि प्रत्येक सेल के कस्टम फ़ॉर्मेट को संरक्षित रखें। संभावनाएँ असीमित हैं, और इन मूलभूत बातों के साथ आपके पास एक ठोस आधार है।

कोडिंग का आनंद लें, और प्रयोग करना न भूलें—कभी‑कभी सबसे अच्छे उत्तर तब मिलते हैं जब आप फ़ॉर्मेट स्ट्रिंग को थोड़ा‑बहुत बदलते हैं!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}