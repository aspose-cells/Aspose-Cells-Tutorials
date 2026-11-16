---
category: general
date: 2026-11-16
description: WRAPCOLS को C# में उपयोग करना सीखें ताकि एक पंक्ति को कॉलम में विभाजित
  किया जा सके, Excel वर्कबुक को स्वचालित किया जा सके, सूत्रों की गणना की जा सके, और
  Excel फ़ाइल को सहेजा जा सके।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split row into columns
- automate excel workbook
- excel formula calculation
- save excel file c#
language: hi
lastmod: 2026-11-16
og_description: C# में WRAPCOLS का उपयोग करके एक पंक्ति को कॉलम में विभाजित करना,
  Excel वर्कबुक को स्वचालित करना, फ़ॉर्मूला गणना चलाना और Excel फ़ाइल को सहेजना।
og_image_alt: Screenshot showing WRAPCOLS function splitting a row into columns in
  an Excel workbook
og_title: C# में WRAPCOLS का उपयोग कैसे करें – पंक्तियों को विभाजित करें, सूत्रों
  की गणना करें, और Excel फ़ाइलें सहेजें
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  headline: How to use WRAPCOLS to split a row into columns in C#
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a row into columns, automate
    an Excel workbook, calculate formulas, and save the Excel file.
  name: How to use WRAPCOLS to split a row into columns in C#
  steps:
  - name: How WRAPCOLS works
    text: '* **Source range** – `A1:T1` contains the original 20 values. * **Column
      count** – `5` tells Excel to create five columns per row. * **Result** – Excel
      fills cells `A2:E5` with the wrapped data automatically.'
  - name: Expected output
    text: 'Open `WrapColsDemo.xlsx` and you’ll see:'
  - name: Next steps
    text: '* Explore other dynamic array functions such as `SEQUENCE`, `FILTER`, and
      `UNIQUE` to enrich your Excel automation toolkit. * Combine `WRAPCOLS` with
      chart generation APIs to produce ready‑to‑publish reports. * Integrate the code
      into a background service that processes CSV uploads and outputs resha'
  type: HowTo
tags:
- Excel automation
- C#
- Aspose.Cells
title: C# में WRAPCOLS का उपयोग करके पंक्ति को कॉलम में विभाजित कैसे करें
url: /hi/net/row-and-column-management/how-to-use-wrapcols-to-split-a-row-into-columns-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में WRAPCOLS का उपयोग करके एक पंक्ति को कॉलम में विभाजित कैसे करें

यदि आपको C# प्रोजेक्ट में **how to use WRAPCOLS** की आवश्यकता है, तो यह गाइड आपको एक पूर्ण, चलाने योग्य समाधान दिखाता है। आप देखेंगे कि कैसे एक पंक्ति को कॉलम में विभाजित किया जाए, Excel वर्कबुक को ऑटोमेट किया जाए, Excel फ़ॉर्मूला की गणना ट्रिगर की जाए, और अंत में Excel फ़ाइल को C# स्टाइल में सहेजा जाए।

प्रोग्रामेटिक रूप से Excel के साथ काम करना अक्सर बड़े डेटा सेट को संभालने का मतलब होता है, और `WRAPCOLS` फ़ंक्शन आपको मैन्युअल लूपिंग के बिना एकल पंक्ति को मैट्रिक्स में पुनः आकार देने की सुविधा देता है। नीचे दिए गए चरण सभी आवश्यक चीज़ों को कवर करते हैं—वर्कबुक निर्माण से लेकर अंतिम फ़ाइल आउटपुट तक—ताकि आप इस तकनीक को किसी भी .NET एप्लिकेशन में एकीकृत कर सकें।

## इस ट्यूटोरियल में क्या कवर किया गया है

* नई वर्कबुक बनाना और उसकी पहली वर्कशीट तक पहुँच प्राप्त करना।  
* क्रमिक मानों (1‑20) के साथ एक पंक्ति को भरना।  
* पंक्ति को 5‑कॉलम ब्लॉकों में विभाजित करने के लिए `WRAPCOLS` Excel फ़ॉर्मूला लागू करना।  
* **excel formula calculation** चलाना ताकि परिणाम शीट का हिस्सा बन जाए।  
* **save excel file c#** का उपयोग करके वर्कबुक को डिस्क पर लिखना।  

Aspose.Cells for .NET लाइब्रेरी (या कोई भी संगत API जो `WRAPCOLS` को सपोर्ट करता हो) के अलावा कोई बाहरी कॉन्फ़िगरेशन आवश्यक नहीं है। गाइड के अंत तक आपके पास `WrapColsDemo.xlsx` नामक फ़ाइल होगी, जिसमें मूल एकल‑पंक्ति डेटा से चार पंक्तियों में पाँच‑पाँच कॉलम होंगे।

## आवश्यकताएँ

* .NET 6.0 या बाद का (कोड .NET Core 3.1 और .NET Framework 4.7+ के साथ भी काम करता है)।  
* **Aspose.Cells** का रेफ़रेंस (NuGet के माध्यम से उपलब्ध: `Install-Package Aspose.Cells`)।  
* C# सिंटैक्स और Excel फ़ॉर्मूलों की बुनियादी समझ।  

> **Pro tip:** यदि आप एक मुफ्त विकल्प पसंद करते हैं, तो ओपन‑सोर्स EPPlus लाइब्रेरी भी कस्टम फ़ॉर्मूलों को सपोर्ट करती है, लेकिन `WRAPCOLS` केवल उन लाइब्रेरीज़ में बिल्ट‑इन होता है जो पूर्ण Excel कैलकुलेशन इंजन को लागू करती हैं, जैसे Aspose.Cells।

## चरण 1: नई वर्कबुक बनाएं और पहली वर्कशीट प्राप्त करें

पहला ऑपरेशन `Workbook` ऑब्जेक्ट को इंस्टैंशिएट करना और उसकी डिफ़ॉल्ट वर्कशीट को फ़ेच करना है। यह ऑब्जेक्ट मेमोरी में पूरे Excel फ़ाइल का प्रतिनिधित्व करता है।

```csharp
using Aspose.Cells;

...

// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                 // creates an empty workbook
Worksheet sheet = workbook.Worksheets[0];           // the first worksheet (named "Sheet1")
```

प्रोग्रामेटिक रूप से वर्कबुक बनाना **automate excel workbook** कार्यों की नींव है। `Worksheet` रेफ़रेंस आपको सेल्स को सीधे मैनीपुलेट करने की अनुमति देता है।

## चरण 2: पहली पंक्ति को मान 1‑20 से भरें

अब, `A1` से `T1` तक के सेल्स को 1 से 20 तक के नंबरों से भरें। एक साधारण `for` लूप प्रत्येक मान को उपयुक्त कॉलम इंडेक्स में लिखता है।

```csharp
// Step 2: Fill the first row with values 1‑20
for (int col = 0; col < 20; col++)
{
    sheet.Cells[0, col].PutValue(col + 1);   // Row 0 = first row, column index starts at 0
}
```

प्रोग्रामेटिक रूप से मान लिखने का कारण क्या है? यह सुनिश्चित करता है कि डेमो किसी भी मशीन पर मैन्युअल डेटा एंट्री के बिना काम करे, जो बैच प्रोसेस में **automate excel workbook** जेनरेशन के लिए आवश्यक है।

## चरण 3: WRAPCOLS फ़ंक्शन लागू करके पंक्ति को 5‑कॉलम ब्लॉकों में विभाजित करें

अब हम Excel फ़ॉर्मूला `WRAPCOLS` का उपयोग करेंगे। यह स्रोत रेंज और कॉलम काउंट लेता है, फिर एक दो‑आयामी एरे लौटाता है जो स्रोत डेटा को निर्दिष्ट कॉलम संख्या में “रैप” करता है।

```csharp
// Step 3: Use the WRAPCOLS function to split the row into 5‑column blocks
sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";
```

फ़ॉर्मूला को सेल `A2` में रखने से Excel को आउटपुट दूसरी पंक्ति से शुरू करने का निर्देश मिलता है। परिणाम 4 × 5 मैट्रिक्स होगा क्योंकि 20 आइटम को 5 कॉलम में विभाजित करने पर चार पंक्तियाँ बनती हैं।

### WRAPCOLS कैसे काम करता है

* **Source range** – `A1:T1` में मूल 20 मान होते हैं।  
* **Column count** – `5` Excel को प्रति पंक्ति पाँच कॉलम बनाने को कहता है।  
* **Result** – Excel स्वचालित रूप से `A2:E5` सेल्स को रैप्ड डेटा से भर देता है।

यदि आपको किसी अलग ब्लॉक आकार के साथ **split row into columns** करने की आवश्यकता हो, तो केवल दूसरे आर्ग्यूमेंट को बदलें। उदाहरण के लिए, `WRAPCOLS(A1:T1,4)` पाँच पंक्तियों में चार‑चार कॉलम उत्पन्न करेगा।

## चरण 4: फ़ॉर्मूला की गणना करें ताकि WRAPCOLS परिणाम वास्तविक हो जाए

नया जोड़ा गया फ़ॉर्मूला तब तक अनइवैल्यूएटेड रहता है जब तक कैलकुलेशन इंजन नहीं चलता। `CalculateFormula()` को कॉल करके आप सुनिश्चित करते हैं कि **excel formula calculation** चरण वास्तविक मानों को वर्कशीट में लिखे।

```csharp
// Step 4: Calculate formulas so the WRAPCOLS result is materialised
workbook.CalculateFormula();
```

गणना चलाना महत्वपूर्ण है क्योंकि बाद में आप **save excel file c#** करेंगे, और सहेजी गई फ़ाइल में गणना किए हुए मान होने चाहिए, न कि केवल फ़ॉर्मूला टेक्स्ट। इस चरण के बिना आउटपुट वर्कबुक `#N/A` या कच्चा फ़ॉर्मूला दिखाएगी, न कि अपेक्षित संख्याएँ।

## चरण 5: वर्कबुक को डिस्क पर सहेजें

अंत में, `Save` मेथड का उपयोग करके वर्कबुक को स्थायी बनाएं। आप कोई भी वैध फ़ाइल पाथ निर्दिष्ट कर सकते हैं; उदाहरण में एक प्लेसहोल्डर डायरेक्टरी उपयोग की गई है जिसे आपको अपने अनुसार बदलना चाहिए।

```csharp
// Step 5: Save the workbook
string outputPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "WrapColsDemo.xlsx");
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

`Save` कॉल **save excel file c#** को सबसे सरल रूप में दर्शाता है। Aspose.Cells फ़ाइल एक्सटेंशन के आधार पर स्वचालित रूप से XLSX फ़ॉर्मेट चुनता है। यदि आपको पुराना `.xls` फ़ाइल चाहिए, तो एक्सटेंशन को उसी अनुसार बदलें।

### अपेक्षित आउटपुट

`WrapColsDemo.xlsx` खोलें और आप देखेंगे:

| A | B | C | D | E |
|---|---|---|---|---|
| 1 | 2 | 3 | 4 | 5 |
| 6 | 7 | 8 | 9 |10 |
|11 |12 |13 |14 |15 |
|16 |17 |18 |19 |20 |

मूल एकल पंक्ति को **split row into columns** करके चार पंक्तियों में पाँच‑पाँच कॉलम में विभाजित किया गया है।

## पूर्ण स्रोत कोड

सभी चरणों को मिलाकर एक कॉम्पैक्ट, सेल्फ‑कंटेन्ड प्रोग्राम बनता है:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 1: Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Fill first row with values 1‑20
        for (int col = 0; col < 20; col++)
        {
            sheet.Cells[0, col].PutValue(col + 1);
        }

        // Step 3: Apply WRAPCOLS to split into 5‑column blocks
        sheet.Cells["A2"].Formula = "WRAPCOLS(A1:T1,5)";

        // Step 4: Force calculation so values are materialised
        workbook.CalculateFormula();

        // Step 5: Save the workbook (change the path as needed)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "WrapColsDemo.xlsx");
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

कोड को एक नए कंसोल प्रोजेक्ट में कॉपी करें, Aspose.Cells NuGet पैकेज को रिस्टोर करें, और चलाएँ। प्रोग्राम कुछ सेकंड में आपके डेस्कटॉप पर Excel फ़ाइल बना देगा।

## सामान्य वैरिएशन और एज केस

| Situation | Adjustment |
|-----------|------------|
| **Different block size** | `WRAPCOLS(A1:T1,5)` को `WRAPCOLS(A1:T1, n)` में बदलें जहाँ `n` इच्छित कॉलम काउंट हो। |
| **Multiple source rows** | `WRAPCOLS(A1:A10,5)` का उपयोग करके एक वर्टिकल रेंज को 5‑कॉलम मैट्रिक्स में रैप करें। |
| **Dynamic source range** | फ़ॉर्मूला असाइन करने से पहले C# में एड्रेस स्ट्रिंग बनाएं (`$"A1:{CellIndexToName(0, lastCol)}1"`). |
| **Large worksheets** | `workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` कॉल करके उन सेल्स को स्किप करें जो एरर उत्पन्न करते हैं और प्रदर्शन सुधारें। |
| **Saving as CSV** | `workbook.Save(outputPath)` को `workbook.Save(outputPath, SaveFormat.Csv)` से बदलें। |

इन वैरिएशन से पता चलता है कि वही **how to use wrapcols** पैटर्न कई डेटा‑रीशेपिंग परिदृश्यों में अनुकूलित किया जा सकता है।

## ट्रबलशूटिंग टिप्स

* **Formula not evaluated** – फ़ॉर्मूला सेट करने के *बाद* `workbook.CalculateFormula()` कॉल करना सुनिश्चित करें। इस चरण को छोड़ने से सेल में कच्चा `WRAPCOLS` टेक्स्ट रह जाता है।  
* **File access denied** – लक्ष्य डायरेक्टरी मौजूद है और आपके प्रोसेस के पास लिखने की अनुमति है, यह जांचें। `Environment.SpecialFolder.Desktop` का उपयोग अधिकांश अनुमति समस्याओं से बचाता है।  
* **Incorrect number of rows** – `WRAPCOLS` के दूसरे आर्ग्यूमेंट को दोबारा चेक करें। यह कॉलम काउंट को परिभाषित करता है, न कि पंक्ति काउंट; पंक्तियाँ स्रोत सेल्स की कुल संख्या को कॉलम काउंट से विभाजित करके प्राप्त होती हैं।

## निष्कर्ष

अब आप C# में **how to use WRAPCOLS** करके **split row into columns**, पूरी **automate excel workbook** निर्माण, **excel formula calculation** चलाना, और **save excel file c#** को एक साफ़ कोडबेस के साथ कर सकते हैं। यह तकनीक मैन्युअल कॉपी‑पेस्ट ऑपरेशन्स को समाप्त करती है और बड़े डेटा‑ट्रांसफ़ॉर्मेशन पाइपलाइन के लिए आसानी से स्केल करती है।

### अगले कदम

* `SEQUENCE`, `FILTER`, और `UNIQUE` जैसे अन्य डायनामिक एरे फ़ंक्शन्स का अन्वेषण करें ताकि आपके Excel ऑटोमेशन टूलकिट को समृद्ध किया जा सके।  
* `WRAPCOLS` को चार्ट जेनरेशन API के साथ मिलाकर तैयार‑से‑पब्लिश रिपोर्ट बनाएं।  
* कोड को बैकग्राउंड सर्विस में इंटीग्रेट करें जो CSV अपलोड प्रोसेस करे और रीशेप्ड Excel फ़ाइलें डाउनस्ट्रीम एनालिटिक्स के लिए आउटपुट करे।

विभिन्न स्रोत रेंज और कॉलम काउंट के साथ प्रयोग करने में संकोच न करें—फ़ॉर्मूला को समायोजित करें, गणना फिर से चलाएँ, और देखें कि वर्कबुक तुरंत अपडेट हो जाती है। Happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [how to use wrapcols in C# – Full Guide with Excel WRAPROWS & Recalculate Formulas](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [How to Use WRAPCOLS – Complete Guide for C# Excel Automation](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)
- [How to Use WRAPCOLS in C# – Reshape an Array to a Matrix in Excel](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}