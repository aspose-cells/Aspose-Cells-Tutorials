---
category: general
date: 2026-11-16
description: Aspose.Cells, डायनामिक एरे फ़ंक्शन और लैम्ब्डा रिड्यूसर का उपयोग करके
  Excel में एरे को कैसे विस्तारित किया जाए, सीखें, फिर C# से Excel फ़ाइल लिखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to expand array
- create excel workbook
- how to use lambda
- dynamic array functions
- write excel file
language: hi
lastmod: 2026-11-16
og_description: Aspose.Cells, डायनामिक एरे फ़ंक्शन्स और लैम्ब्डा रिड्यूसर का उपयोग
  करके Excel में एरे को कैसे विस्तारित करें। Excel फ़ाइल लिखने के लिए पूरा C# उदाहरण
  देखें।
og_image_alt: Diagram illustrating how to expand array in an Excel worksheet
og_title: Aspose.Cells के साथ Excel में एरे कैसे विस्तारित करें – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to expand array in Excel using Aspose.Cells, dynamic array
    functions, and a lambda reducer, then write the Excel file from C#.
  headline: How to expand array in Excel with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. `EXPAND` pads missing columns with blank cells. The same works for
      rows.
    question: Can I expand to more columns than the source provides?
  - answer: '`EXPAND` will treat the source as a single row; you can still specify
      rows and columns to reshape it.'
    question: What if the source array is horizontal (`{1,2,3,4,5}`)?
  - answer: The lambda must return a value compatible with the accumulator type. For
      text concatenation you could use `LAMBDA(acc, val, acc & val)`.
    question: Does `REDUCE` work with non‑numeric data?
  - answer: Only when you need the computed values before saving. Excel will recalculate
      on open if you skip it.
    question: Do I need to call `CalculateFormula` for every change?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cells के साथ Excel में एरे को कैसे विस्तारित करें
url: /hi/net/calculation-engine/how-to-expand-array-in-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में Aspose.Cells के साथ array को कैसे विस्तारित करें

यदि आपको C# से Excel वर्कशीट में **array को विस्तारित करने** की आवश्यकता है, तो यह ट्यूटोरियल सटीक चरण दिखाता है। आप एक Excel वर्कबुक बनाएँगे, `EXPAND` और `REDUCE` जैसे डायनेमिक एरे फ़ंक्शन का उपयोग करेंगे, एक **lambda** एक्यूमुलेटर लागू करेंगे, और अंत में **Excel फ़ाइल को** डिस्क पर लिखेंगे। यह तरीका Aspose.Cells 23.10 या बाद के संस्करण के साथ काम करता है और किसी मैनुअल Excel इंस्टॉलेशन की आवश्यकता नहीं होती।

इस गाइड के अंत तक आपके पास एक पूर्ण कार्यात्मक `ExpandReduceDemo.xlsx` होगा जो प्रोग्रामेटिक संदर्भ में डायनेमिक एरे फ़ॉर्मूले की शक्ति को दर्शाता है।

## आपको क्या चाहिए

- .NET 6.0 (या Aspose.Cells द्वारा समर्थित कोई भी .NET संस्करण)
- Aspose.Cells for .NET पैकेज (`dotnet add package Aspose.Cells`)
- एक कोड एडिटर या IDE (Visual Studio, VS Code, Rider, आदि)

कोई अतिरिक्त COM इंटरऑप या Office इंस्टॉलेशन आवश्यक नहीं है क्योंकि Aspose.Cells फ़ाइल फ़ॉर्मेट को आंतरिक रूप से संभालता है।

## चरण 1: Excel वर्कबुक बनाएँ

पहला कार्य मेमोरी में **excel वर्कबुक बनाना** है। Aspose.Cells `Workbook` क्लास प्रदान करता है, जो पूरी XLSX फ़ाइल का प्रतिनिधित्व करता है।

```csharp
using System;
using Aspose.Cells;

class ExpandReduceDemo
{
    static void Main()
    {
        // Step 1: instantiate a new workbook and get the default worksheet
        Workbook workbook = new Workbook();              // creates an empty .xlsx structure
        Worksheet sheet = workbook.Worksheets[0];        // the first (and only) sheet by default
```

> **यह क्यों महत्वपूर्ण है:** `Workbook` का इंस्टैंसिएशन आपको एक साफ़ कैनवास देता है। डिफ़ॉल्ट वर्कशीट पहले से तैयार होती है, इसलिए आपको मैन्युअल रूप से जोड़ने की आवश्यकता नहीं है जब तक आप कई शीट नहीं चाहते।

## चरण 2: एक वर्टिकल एरे कॉन्स्टेंट डालें

Excel का डायनेमिक एरे इंजन लिटरल एरे कॉन्स्टेंट के साथ काम कर सकता है। हम वर्टिकल एरे `{1;2;3;4;5}` को सेल **A1** में रखेंगे।

```csharp
        // Step 2: put a vertical array constant into A1
        sheet.Cells["A1"].PutValue("{1;2;3;4;5}");
```

> **टिप:** सेमिकॉलन (`;`) कॉन्स्टेंट में पंक्तियों को अलग करता है, जबकि कॉमा (`,`) कॉलम को अलग करता। यह Excel की अपनी सिंटैक्स को दर्शाता है।

## चरण 3: एरे को मैट्रिक्स में विस्तारित करें

अब हम मुख्य प्रश्न का उत्तर देते हैं – **array को कैसे विस्तारित करें** – `EXPAND` फ़ंक्शन का उपयोग करके। यह फ़ॉर्मूला सिंगल‑कॉलम एरे को 5‑पंक्ति × 2‑कॉलम मैट्रिक्स में विस्तारित करता है, जो **B1** से शुरू होता है।

```csharp
        // Step 3: use EXPAND to create a 5‑row by 2‑column matrix
        sheet.Cells["B1"].Formula = "EXPAND(A1,5,2)";
```

> **EXPAND क्यों?** `EXPAND(source, rows, cols)` स्रोत रेंज को निर्दिष्ट आकार में ले जाता है, आवश्यक होने पर खाली सेल से पैड करता है। यह एकल एरे से बड़ा मैट्रिक्स बनाने का सबसे पठनीय तरीका है।

## चरण 4: lambda एक्यूमुलेटर के साथ मैट्रिक्स को Reduce करें

`REDUCE` फ़ंक्शन एक रेंज पर इटररेट करता है और **lambda** अभिव्यक्ति का उपयोग करके मानों को एकत्रित करता है। यहाँ हम प्रत्येक कॉलम मान को एकल कॉलम में जोड़ते हैं, परिणाम **D1** में रखते हैं।

```csharp
        // Step 4: REDUCE the expanded matrix using a lambda accumulator
        sheet.Cells["D1"].Formula = "REDUCE(A1, B1:E5, LAMBDA(acc, val, acc+val))";
```

> **lambda का उपयोग कैसे करें:** `LAMBDA(acc, val, acc+val)` वर्तमान एक्यूमुलेटर (`acc`) और अगली सेल वैल्यू (`val`) लेता है। यह नया एक्यूमुलेटर लौटाता है, प्रभावी रूप से एक रनिंग टोटल बनाता है। यह कोड से Excel फ़ॉर्मूले में **lambda का उपयोग कैसे करें** को दर्शाता है।

## चरण 5: फ़ॉर्मूले की गणना करें ताकि परिणाम दिखें

Aspose.Cells फ़ॉर्मूले सेट करने पर स्वचालित रूप से उनका मूल्यांकन नहीं करता। `CalculateFormula` को कॉल करने से इंजन वर्कबुक में प्रत्येक फ़ॉर्मूला की गणना करता है।

```csharp
        // Step 5: recalculate all formulas so the results are materialized
        workbook.CalculateFormula();
```

> **नोट:** यदि आप उत्पन्न फ़ाइल को Excel में खोलते हैं, तो मान पहले से ही दिखाई देंगे क्योंकि वे पहले से ही प्री‑कैल्कुलेटेड हैं।

## चरण 6: Excel फ़ाइल को डिस्क पर लिखें

अंत में, `Save` मेथड का उपयोग करके **excel फ़ाइल लिखें**। वह फ़ोल्डर चुनें जहाँ आपके पास लिखने की अनुमति हो।

```csharp
        // Step 6: save the workbook as an .xlsx file
        string outputPath = @"YOUR_DIRECTORY\ExpandReduceDemo.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

### अपेक्षित परिणाम

| A | B | C | D |
|---|---|---|---|
| {1;2;3;4;5} | 1 |  | 15 |
|            | 2 |  |    |
|            | 3 |  |    |
|            | 4 |  |    |
|            | 5 |  |    |

- **कॉलम B** और **C** में `EXPAND` द्वारा उत्पन्न 5 × 2 मैट्रिक्स है।
- **सेल D1** में `15` दिखता है, जो `REDUCE` + **lambda** फ़ॉर्मूले द्वारा सभी संख्याओं का योग है।

## सामान्य प्रश्न और किनारे के मामले

- **क्या मैं स्रोत से अधिक कॉलम में विस्तारित कर सकता हूँ?**  
  हाँ। `EXPAND` गायब कॉलम को खाली सेल से पैड करता है। पंक्तियों के लिए भी यही लागू होता है।

- **यदि स्रोत एरे क्षैतिज है (`{1,2,3,4,5}`) तो क्या होगा?**  
  `EXPAND` इसे एकल पंक्ति के रूप में लेगा; आप फिर भी पंक्तियों और कॉलम को निर्दिष्ट करके उसे रीशेप कर सकते हैं।

- **क्या `REDUCE` गैर‑संख्यात्मक डेटा के साथ काम करता है?**  
  lambda को एक्यूमुलेटर प्रकार के साथ संगत मान लौटाना चाहिए। टेक्स्ट संयोजन के लिए आप `LAMBDA(acc, val, acc & val)` उपयोग कर सकते हैं।

- **क्या मुझे हर बदलाव के बाद `CalculateFormula` कॉल करना चाहिए?**  
  केवल तब जब आपको सहेजने से पहले गणना किए हुए मान चाहिए हों। यदि आप इसे छोड़ते हैं, तो Excel खोलते समय पुनः‑गणना करेगा।

## प्रो टिप्स

- **प्रदर्शन:** बड़े वर्कबुक के लिए, सभी फ़ॉर्मूले सेट करने के बाद एक बार `workbook.CalculateFormula` कॉल करें, प्रत्येक सेल के बाद नहीं।
- **संस्करण सुरक्षा:** `EXPAND` और `REDUCE` Excel 365 और बाद के संस्करणों में उपलब्ध हैं। Aspose.Cells इन्हें लक्ष्य Excel संस्करण की परवाह किए बिना लागू करता है क्योंकि गणना इंजन अंतर्निहित है।
- **फ़ॉर्मूले डिबग करना:** `sheet.Cells["B1"].Formula` का उपयोग करके आप सेट की गई स्ट्रिंग को वापस पढ़ सकते हैं; यह गतिशील रूप से फ़ॉर्मूले बनाते समय मददगार होता है।

## निष्कर्ष

अब आप **Excel में array को विस्तारित करने** के लिए Aspose.Cells का उपयोग, **डायनेमिक एरे फ़ंक्शन** को लागू, `REDUCE` के साथ **lambda** का प्रयोग, और C# से **excel फ़ाइल लिखना** जानते हैं। यह एंड‑टू‑एंड उदाहरण अधिक जटिल डेटा ट्रांसफ़ॉर्मेशन जैसे मैट्रिक्स ट्रांसपोज़िशन, संचयी योग, या कस्टम एग्रीगेशन के लिए अनुकूलित किया जा सकता है।

---

*अगले कदम:*  
- `FILTER`, `SORT`, और `UNIQUE` जैसे अन्य डायनेमिक फ़ंक्शन का अन्वेषण करें।  
- पुन: उपयोग योग्य यूज़र‑डिफाइंड फ़ंक्शन बनाने के लिए कई `LAMBDA` अभिव्यक्तियों को संयोजित करें।  
- ऑन‑द‑फ़्लाई रिपोर्ट निर्माण के लिए ASP.NET Core APIs में वर्कबुक जेनरेशन को एकीकृत करें।

## आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकते हैं और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकते हैं।

- [How to create Excel workbook C# with a dynamic array formula](/cells/english/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-c-with-a-dynamic-array-formula/)
- [How to expand array in Excel and populate a template](/cells/english/net/templates-reporting/how-to-expand-array-in-excel-and-populate-a-template/)
- [How to Expand Array in C# with Aspose.Cells – Step‑by‑Step Guide](/cells/english/net/excel-formulas-and-calculation-options/how-to-expand-array-in-c-with-aspose-cells-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}