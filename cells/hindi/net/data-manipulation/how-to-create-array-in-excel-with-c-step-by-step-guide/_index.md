---
category: general
date: 2026-02-09
description: C# के साथ Excel में एरे कैसे बनाएं, मिनटों में समझाया गया – अनुक्रम संख्या
  उत्पन्न करना सीखें, COT का उपयोग करें, और वर्कबुक को XLSX के रूप में सहेजें।
draft: false
keywords:
- how to create array
- create excel workbook c#
- generate sequence numbers
- save workbook as xlsx
- how to use cot
language: hi
og_description: C# के साथ Excel में एरे कैसे बनाएं, यह चरण-दर-चरण समझाया गया है, जिसमें
  क्रमांक उत्पन्न करना, COT का उपयोग करना, और वर्कबुक को XLSX के रूप में सहेजना शामिल
  है।
og_title: C# के साथ Excel में ऐरे कैसे बनाएं – त्वरित गाइड
tags:
- C#
- Excel
- Aspose.Cells
title: C# के साथ Excel में एरे कैसे बनाएं – चरण-दर-चरण गाइड
url: /hi/net/data-manipulation/how-to-create-array-in-excel-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में C# के साथ array कैसे बनाएं – चरण-दर-चरण गाइड

क्या आप कभी सोचते रहे हैं कि C# का उपयोग करके Excel में **how to create array** कैसे बनाएं बिना दस्तावेज़ों में घंटों खोदे? आप अकेले नहीं हैं। कई डेवलपर्स को तब रुकावट आती है जब उन्हें एक डायनेमिक स्पिल रेंज, एक तेज़ त्रिकोणमितीय मान, या बस एक साफ़ XLSX फ़ाइल डिस्क पर सहेजनी होती है। इस ट्यूटोरियल में हम इस समस्या को तुरंत हल करेंगे—एक छोटा वर्कबुक बनाकर जो एक विस्तारित array फ़ॉर्मूला लिखता है, एक कोटैन्जेंट गणना जोड़ता है, और सब कुछ XLSX फ़ाइल के रूप में सहेजता है।  

हम कुछ अतिरिक्त ट्रिक्स भी जोड़ेंगे: क्रमांक उत्पन्न करना, `COT` फ़ंक्शन को महारत हासिल करना, और फ़ाइल को इच्छित स्थान पर सुनिश्चित करना। अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं। कोई फालतू नहीं, सिर्फ काम करने वाला कोड।

> **Pro tip:** उदाहरण लोकप्रिय **Aspose.Cells** लाइब्रेरी का उपयोग करता है, लेकिन अवधारणाएँ अन्य Excel‑ऑटोमेशन पैकेजों (EPPlus, ClosedXML) में केवल छोटे बदलावों के साथ लागू होती हैं।

---

## आपको क्या चाहिए

- **.NET 6** या बाद का (कोड .NET Framework 4.7+ पर भी कंपाइल होता है)  
- **Aspose.Cells for .NET** – आप इसे NuGet से प्राप्त कर सकते हैं (`Install-Package Aspose.Cells`)  
- एक टेक्स्ट एडिटर या IDE (Visual Studio, Rider, VS Code…)  
- उस फ़ोल्डर में लिखने की अनुमति जहाँ आउटपुट फ़ाइल सहेजी जाएगी  

बस इतना ही—कोई अतिरिक्त कॉन्फ़िगरेशन नहीं, कोई COM इंटरऑप नहीं, सिर्फ एक साफ़ मैनेज्ड असेंबली।

---

## चरण 1: How to create array in Excel – Initialize the Workbook

जब आप Excel शीट में **how to create array** चाहते हैं, तो सबसे पहला काम वर्कबुक ऑब्जेक्ट बनाना है। वर्कबुक को एक खाली कैनवास की तरह सोचें; वर्कशीट वह जगह है जहाँ आप अपने फ़ॉर्मूले पेंट करेंगे।

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // <- fresh workbook
        Worksheet worksheet = workbook.Worksheets[0];    // first (and only) sheet

        // The rest of the steps follow...
```

`Workbook()` को बिना पैरामीटर के क्यों उपयोग करें? यह आपको एक इन‑मेमोरी वर्कबुक देता है जिसमें डिफ़ॉल्ट शीट होती है, जो तेज़, प्रोग्रामेटिक कार्यों के लिए परफेक्ट है। यदि आपको मौजूदा फ़ाइल खोलनी है, तो बस फ़ाइल पाथ को कंस्ट्रक्टर में पास कर दें।

---

## चरण 2: EXPAND और SEQUENCE के साथ क्रमांक उत्पन्न करें

अब हमारे पास एक शीट है, चलिए **generate sequence numbers** भाग का उत्तर देते हैं। Excel के नए डायनेमिक एरे फ़ंक्शन (`SEQUENCE`, `EXPAND`) हमें 3‑पंक्तियों की वर्टिकल लिस्ट बनाने और उसे स्वचालित रूप से 3 × 5 रेंज में फैलाने की अनुमति देते हैं।

```csharp
        // Write a dynamic array formula that expands a 3‑row sequence into a 3×5 spill range
        // EXPAND pads the result to 5 columns, SEQUENCE generates numbers 1‑3 vertically
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

**क्या हो रहा है यहाँ?**  
- `SEQUENCE(3,1,1,1)` → एक वर्टिकल एरे `{1;2;3}` बनाता है।  
- `EXPAND(...,5,1)` → उस तीन‑पंक्ति कॉलम को पाँच कॉलम तक फैलाता है, अतिरिक्त सेल्स को खाली छोड़ता है।  

जब आप परिणामी `output.xlsx` खोलेंगे, तो आपको **A1** से शुरू होने वाला 3 × 5 ब्लॉक दिखेगा जहाँ पहली कॉलम में 1, 2, 3 हैं और बाकी चार कॉलम खाली हैं। यह तकनीक **how to create array**‑स्टाइल स्पिल रेंज बनाने की रीढ़ है, बिना प्रत्येक सेल को मैन्युअल लिखे।

---

## चरण 3: COT का उपयोग कैसे करें – त्रिकोणमितीय फ़ॉर्मूला जोड़ना

यदि आप Excel फ़ॉर्मूला में **how to use cot** के बारे में भी जिज्ञासु हैं, तो `COT` फ़ंक्शन एक उपयोगी तरीका है रैडियन में व्यक्त कोण का कोटैन्जेंट प्राप्त करने का। चलिए `cot(π/4)` की गणना करते हैं, जिसका मान **1** होना चाहिए।

```csharp
        // Write a simple trigonometric formula that calculates cotangent of 45° (π/4)
        // COT(π/4) evaluates to 1
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";
```

ध्यान दें हमने `PI()` का उपयोग 180° के रैडियन मान को प्राप्त करने के लिए किया, फिर 4 से विभाजित करके 45° तक पहुँचे। Excel भारी काम करता है, और सेल **B1** वर्कबुक खोलते ही `1` दिखाएगा। यह **how to use cot** को तेज़ इंजीनियरिंग या फ़ाइनेंस गणनाओं के लिए बिना अलग मैथमेटिकल लाइब्रेरी के उपयोग को दर्शाता है।

---

## चरण 4: वर्कबुक को XLSX के रूप में सहेजें – फ़ाइल को स्थायी बनाना

एक एरे बनाना और फ़ॉर्मूले डालना मज़ेदार है, लेकिन यदि आप फ़ाइल को डिस्क पर नहीं लिखते तो सब व्यर्थ है। यहाँ Aspose.Cells का उपयोग करके **save workbook as xlsx** करने का सीधा तरीका है:

```csharp
        // Save the workbook to verify the formulas (optional)
        string outputPath = @"C:\Temp\output.xlsx";   // adjust to your folder
        workbook.Save(outputPath, SaveFormat.Xlsx);

        // Let the user know we’re done
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

`SaveFormat.Xlsx` निर्दिष्ट क्यों करें? यह आधुनिक OpenXML फ़ॉर्मेट को सुनिश्चित करता है, जो सार्वभौमिक रूप से पढ़ा जा सकता है (Excel, LibreOffice, Google Sheets)। यदि आपको पुरानी `.xls` फ़ाइल चाहिए, तो बस एन्नुम को बदल दें।

---

## पूर्ण कार्यशील उदाहरण (सभी चरण एक साथ)

नीचे पूरा, तैयार‑चलाने‑योग्य प्रोग्राम है। इसे कॉन्सोल प्रोजेक्ट में कॉपी‑पेस्ट करें, Aspose.Cells NuGet पैकेज रिस्टोर करें, और **F5** दबाएँ।

```csharp
using Aspose.Cells;

public class ExcelArrayDemo
{
    public static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Create a dynamic spill range (how to create array)
        worksheet.Cells["A1"].Formula = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";

        // Step 3: Calculate cotangent (how to use cot)
        worksheet.Cells["B1"].Formula = "=COT(PI()/4)";

        // Step 4: Persist the file (save workbook as xlsx)
        string outputPath = @"C:\Temp\output.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);

        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**अपेक्षित परिणाम** `output.xlsx` खोलने के बाद:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 1 |   |   |   |
| 2 |   |   |   |   |
| 3 |   |   |   |   |

- कॉलम A में `SEQUENCE` द्वारा उत्पन्न 1‑3 संख्याएँ दिखती हैं।  
- कॉलम B में `COT` फ़ॉर्मूला से प्राप्त **1** मान है।  
- कॉलम C‑E खाली हैं, जो `EXPAND` के पैडिंग प्रभाव को दर्शाते हैं।

---

## सामान्य प्रश्न और किनारे के मामलों

### अगर मुझे अधिक पंक्तियों या कॉलमों की जरूरत हो तो?

बस `SEQUENCE` और `EXPAND` के आर्ग्युमेंट्स को बदलें।  
- `SEQUENCE(10,2,5,2)` 10‑पंक्ति × 2‑कॉलम मैट्रिक्स देगा, जो 5 से शुरू होकर 2 के अंतर से बढ़ेगा।  
- `EXPAND(...,10,5)` परिणाम को 10 कॉलम और 5 पंक्तियों तक पैड करेगा।

### क्या यह पुराने Excel संस्करणों के साथ काम करता है?

डायनेमिक एरे फ़ंक्शन (`SEQUENCE`, `EXPAND`) को Excel 365 या 2019+ की आवश्यकता होती है। लेगेसी फ़ाइलों के लिए आप क्लासिक फ़ॉर्मूले उपयोग कर सकते हैं या `Cells[row, col].PutValue(value)` के माध्यम से सीधे मान लिख सकते हैं।

### क्या मैं फ़ॉर्मूला को R1C1 शैली में लिख सकता हूँ?

बिल्कुल। `A1` को `Cells[0, 0]` से बदलें और `FormulaR1C1` प्रॉपर्टी का उपयोग करें:

```csharp
worksheet.Cells[0, 0].FormulaR1C1 = "=EXPAND(SEQUENCE(3,1,1,1),5,1)";
```

### संस्कृति‑विशिष्ट दशमलव विभाजकों के बारे में क्या?

Aspose.Cells वर्कबुक की लोकेल का सम्मान करता है। यदि आपको विशेष संस्कृति चाहिए, तो फ़ॉर्मूले लिखने से पहले `workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");` सेट करें।

---

## दृश्य सारांश

![C# का उपयोग करके Excel में array कैसे बनाएं](/images/how-to-create-array-excel-csharp.png "C# का उपयोग करके Excel में array कैसे बनाएं")

*स्क्रीनशॉट अंतिम स्पिल रेंज और कोटैन्जेंट परिणाम को दिखाता है।*

---

## निष्कर्ष

बस इतना ही—**how to create array** को C# के साथ Excel में शून्य से बनाना, क्रमांक उत्पन्न करना, `COT` फ़ंक्शन का उपयोग करना, और **save workbook as XLSX** को एक ही साफ़ प्रोग्राम में करना। मुख्य बिंदु:

1. `Workbook` और `Worksheet` ऑब्जेक्ट्स का उपयोग करके अपनी Excel ऑटोमेशन शुरू करें।  
2. लचीली स्पिल रेंज के लिए डायनेमिक एरे फ़ंक्शन (`SEQUENCE`, `EXPAND`) का लाभ उठाएँ।  
3. तेज़ गणनाओं के लिए `COT` जैसे त्रिकोणमितीय फ़ंक्शन जोड़ें, बिना अतिरिक्त लाइब्रेरी के।  
4. `SaveFormat.Xlsx` के साथ परिणाम को सहेजें ताकि फ़ाइल सार्वभौमिक रूप से पढ़ी जा सके।

अगले चरण के लिए तैयार हैं? `COT(PI()/4)` को बदलकर देखें

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}