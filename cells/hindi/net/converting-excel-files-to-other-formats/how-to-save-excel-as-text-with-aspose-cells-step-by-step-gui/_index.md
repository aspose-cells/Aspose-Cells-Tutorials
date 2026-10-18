---
category: general
date: 2026-10-10
description: Aspose.Cells का उपयोग करके C# में Excel को टेक्स्ट के रूप में सहेजना
  सीखें। यह गाइड Excel को txt में बदलने, XLSX को txt में निर्यात करने, और Excel से
  पूर्ण कोड के साथ txt बनाने को कवर करता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as text
- convert excel to txt
- export xlsx to txt
- create txt from excel
language: hi
lastmod: 2026-10-10
og_description: Aspose.Cells for .NET का उपयोग करके Excel को टेक्स्ट के रूप में सहेजें।
  इस गाइड का पालन करके Excel को txt में बदलें, XLSX को txt में निर्यात करें, और नमूना
  कोड के साथ Excel से txt बनाएं।
og_image_alt: Screenshot of C# code that saves an Excel workbook as a plain‑text file
og_title: C# में Excel को टेक्स्ट के रूप में सहेजें – पूर्ण Aspose.Cells ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  headline: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to save Excel as text in C# using Aspose.Cells. This guide
    covers convert Excel to txt, export XLSX to txt, and create txt from Excel with
    full code.
  name: How to save Excel as text with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Prerequisites
    text: '* .NET 6.0 or later (the code also works with .NET Framework 4.7.2+). *
      Basic familiarity with C# and Visual Studio (or any .NET IDE). * An active Aspose.Cells
      for .NET license or a free evaluation key. * The Excel file you want to convert
      (`input.xlsx` in the examples).'
  - name: Full runnable program
    text: 'Putting the pieces together, here is a complete, self‑contained console
      application:'
  - name: Verify programmatically
    text: 'You can read the generated file back into memory to confirm that the export
      succeeded:'
  - name: Common edge cases
    text: '| Situation | What to watch for | Recommended fix | |----------------------------------------|---------------------------------------------------|-----------------|
      | Cells contain formulas | The exported value is the **calculated result**,
      not the formula text. | Ensure the workbook is fully calcul'
  - name: What’s next?
    text: '* Try exporting to CSV (`CsvSaveOptions`) for Excel‑compatible comma‑separated
      files. * Explore the `PdfSaveOptions` class to **export Excel to PDF** in a
      single line. * Combine multiple worksheets into one text file by iterating over
      `workbook.Worksheets`.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Text export
title: Aspose.Cells के साथ Excel को टेक्स्ट के रूप में कैसे सहेजें – चरण‑दर‑चरण गाइड
url: /hi/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells के साथ Excel को टेक्स्ट के रूप में सहेजें – चरण‑दर‑चरण गाइड

यदि आपको **Excel को तेज़ी से टेक्स्ट के रूप में सहेजना** है, तो यह ट्यूटोरियल आपको C# में Aspose.Cells के साथ यह कैसे करना है, दिखाता है। आप देखेंगे कि **Excel को txt में कैसे बदलें**, संख्यात्मक परिशुद्धता को कैसे नियंत्रित करें, और सामान्य किनारी मामलों को कैसे संभालें—सब एक ही चलाने योग्य उदाहरण में।

आगे के सेक्शन में आप पूरी कार्यप्रवाह सीखेंगे, लाइब्रेरी को इंस्टॉल करने से लेकर आउटपुट फ़ाइल की पुष्टि तक। कोई बाहरी दस्तावेज़ आवश्यक नहीं; यहाँ सब कुछ शामिल है।

## आप क्या हासिल करेंगे

इस गाइड के अंत तक आप सक्षम होंगे:

* डिस्क से किसी भी `.xlsx` वर्कबुक को लोड करना।  
* `TxtSaveOptions` को कॉन्फ़िगर करके महत्वपूर्ण अंकों की संख्या सीमित करना।  
* एक ही `Save` कॉल के साथ **XLSX को txt में निर्यात** करना।  
* जब आप **Excel से txt बनाते** हैं तो फ़ॉर्मेटिंग समस्याओं का समाधान समझना।

### पूर्वापेक्षाएँ

* .NET 6.0 या बाद का (कोड .NET Framework 4.7.2+ के साथ भी काम करता है)।  
* C# और Visual Studio (या किसी भी .NET IDE) की बुनियादी जानकारी।  
* एक सक्रिय Aspose.Cells for .NET लाइसेंस या एक मुफ्त इवैल्यूएशन कुंजी।  
* वह Excel फ़ाइल जिसे आप बदलना चाहते हैं (`input.xlsx` उदाहरणों में)।

> **प्रो टिप:** यदि आप इसे सर्वर पर चलाने की योजना बना रहे हैं, तो लाइसेंस फ़ाइल को सुरक्षित स्थान पर रखें और एप्लिकेशन स्टार्ट‑अप पर एक बार लोड करें।

## चरण 1: विकास पर्यावरण सेट अप करें

1. एक नया कंसोल प्रोजेक्ट बनाएं:

   ```bash
   dotnet new console -n ExcelToTxtDemo
   cd ExcelToTxtDemo
   ```

2. Aspose.Cells NuGet पैकेज जोड़ें:

   ```bash
   dotnet add package Aspose.Cells
   ```

   यह नवीनतम स्थिर संस्करण को जोड़ता है (2026‑10‑10 तक यह 23.9 है)।

3. (वैकल्पिक) यदि आपके पास लाइसेंस फ़ाइल है, तो `Aspose.Cells.lic` को प्रोजेक्ट रूट में रखें और `Program.cs` की शुरुआत में निम्न कोड जोड़ें:

   ```csharp
   // Load Aspose.Cells license (required for production use)
   var license = new Aspose.Cells.License();
   license.SetLicense("Aspose.Cells.lic");
   ```

   लाइसेंस लोड करने से इवैल्यूएशन वाटरमार्क हट जाते हैं और आकार सीमाएँ निष्क्रिय हो जाती हैं।

## चरण 2: Excel वर्कबुक लोड करें

पहली कार्यात्मक पंक्ति एक `Workbook` इंस्टेंस बनाती है जो पूरी Excel फ़ाइल का प्रतिनिधित्व करता है।

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 2: Load the workbook you want to convert
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
        // Continue with export logic...
    }
}
```

**यह क्यों महत्वपूर्ण है:** `Workbook` शीट्स, सेल्स, फ़ॉर्मूले और फ़ॉर्मेटिंग को एब्स्ट्रैक्ट करता है। फ़ाइल को एक बार लोड करके आप रूपांतरण को तेज़ और मेमोरी‑कुशल रख सकते हैं।

## चरण 3: सटीक अंक नियंत्रण के लिए TxtSaveOptions कॉन्फ़िगर करें

जब आप **Excel को txt में बदलते** हैं, तो संख्यात्मक मानों में कई दशमलव स्थान हो सकते हैं। `TxtSaveOptions` आपको आउटपुट को विशिष्ट महत्वपूर्ण अंकों की संख्या तक सीमित करने देता है, जो अक्सर डाउनस्ट्रीम सिस्टमों के लिए आवश्यक होता है जो फिक्स्ड‑विथ टेक्स्ट की अपेक्षा करते हैं।

```csharp
// Step 3: Create and configure TxtSaveOptions
var txtOptions = new TxtSaveOptions
{
    // Keep only 5 significant digits (e.g., 123.45678 → 123.46)
    SignificantDigits = 5,

    // Optional: Use tab as the delimiter for column separation
    Separator = "\t",

    // Optional: Export only the first worksheet
    ExportActiveWorksheetOnly = true
};
```

**व्याख्या:**  
* `SignificantDigits` फ्लोटिंग‑पॉइंट शोर को हटाता है जबकि अधिकांश व्यावसायिक गणनाओं के लिए पर्याप्त परिशुद्धता बनाए रखता है।  
* `Separator` डिफ़ॉल्ट रूप से स्पेस है; इसे `\t` (टैब) पर सेट करने से उत्पन्न फ़ाइल को डेटाबेस या स्प्रेडशीट में आयात करना आसान हो जाता है।  
* `ExportActiveWorksheetOnly` छिपी हुई शीट्स के आकस्मिक निर्यात को रोकता है, जिससे टेक्स्ट फ़ाइल का आकार अनावश्यक रूप से नहीं बढ़ता।

## चरण 4: कॉन्फ़िगर किए गए विकल्पों के साथ XLSX को txt में निर्यात करें

अब आपके पास **Excel को टेक्स्ट के रूप में सहेजने** के लिए सब कुछ है। `Save` मेथड प्लेन‑टेक्स्ट प्रतिनिधित्व को लक्ष्य पथ पर लिखता है।

```csharp
// Step 4: Save the workbook as a plain‑text file
workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);
Console.WriteLine("Export completed: output.txt");
```

जनरेट किया गया `output.txt` टैब‑सेपरेटेड वैल्यूज़ की पंक्तियों को रखेगा, प्रत्येक सेल को आपके सेट किए गए विकल्पों के अनुसार प्लेन टेक्स्ट में रेंडर किया जाएगा।

### पूर्ण चलाने योग्य प्रोग्राम

सभी हिस्सों को मिलाकर, यहाँ एक संपूर्ण, स्व-निर्भर कंसोल एप्लिकेशन है:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load license if you have one (remove comments if not needed)
        // var license = new License();
        // license.SetLicense("Aspose.Cells.lic");

        // 1️⃣ Load the Excel workbook
        var workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Configure TxtSaveOptions
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5,
            Separator = "\t",
            ExportActiveWorksheetOnly = true
        };

        // 3️⃣ Export XLSX to TXT
        workbook.Save(@"YOUR_DIRECTORY\output.txt", txtOptions);

        Console.WriteLine("✅ Excel workbook successfully saved as text at: output.txt");
    }
}
```

**अपेक्षित आउटपुट** (कंसोल):

```
✅ Excel workbook successfully saved as text at: output.txt
```

**परिणामी `output.txt` नमूना** (पहली तीन पंक्तियाँ):

```
Name    Age     Salary
Alice   30      55000
Bob     27      47000
```

संख्याएँ पाँच महत्वपूर्ण अंकों तक राउंड की गई हैं, और कॉलम टैब द्वारा अलग किए गए हैं।

## चरण 5: आउटपुट की पुष्टि करें और किनारी मामलों को संभालें

### प्रोग्रामेटिक रूप से सत्यापित करें

आप उत्पन्न फ़ाइल को मेमोरी में वापस पढ़ सकते हैं ताकि निर्यात सफल रहा यह पुष्टि हो सके:

```csharp
string[] lines = File.ReadAllLines(@"YOUR_DIRECTORY\output.txt");
if (lines.Length > 0)
{
    Console.WriteLine("First line of the txt file:");
    Console.WriteLine(lines[0]);
}
```

### सामान्य किनारी मामले

| स्थिति                                   | ध्यान देने योग्य बात                              | सुझाया गया समाधान |
|------------------------------------------|---------------------------------------------------|--------------------|
| सेल्स में फ़ॉर्मूले हैं                    | निर्यातित मान **गणना किया हुआ परिणाम** है, फ़ॉर्मूला टेक्स्ट नहीं। | `workbook.CalculateFormula();` को `Save` से पहले कॉल करें। |
| तिथियाँ सीरियल नंबर के रूप में दिखती हैं | Excel तिथियों को नंबरों के रूप में संग्रहीत करता है; वे `44745` जैसी दिख सकती हैं। | `txtOptions.ConvertDateTime = true;` सेट करके मानव‑पठनीय तिथि फ़ॉर्मेट लागू करें। |
| बड़े वर्कशीट्स (>10 000 पंक्तियाँ)       | मेमोरी उपयोग में अचानक वृद्धि हो सकती है।      | `txtOptions.ExportAllSheets = false;` उपयोग करें और शीट्स को व्यक्तिगत रूप से प्रोसेस करें। |
| यूनिकोड कैरेक्टर (जैसे इमोजी)           | डिफ़ॉल्ट एन्कोडिंग UTF‑8 है; पुराने सिस्टम ANSI की अपेक्षा कर सकते हैं। | आवश्यक होने पर `txtOptions.Encoding = Encoding.GetEncoding("windows-1252");` सेट करें। |

इन परिदृश्यों की पूर्वधारणा करके आप विभिन्न डेटा सेटों में **Excel से txt बनाना** विश्वसनीय बना सकते हैं।

## निष्कर्ष

अब आप जानते हैं कि Aspose.Cells for .NET का उपयोग करके **Excel को टेक्स्ट के रूप में कैसे सहेजें**, वर्कबुक लोड करने से लेकर `TxtSaveOptions` कॉन्फ़िगर करने और अंत में **XLSX को txt में निर्यात** करने तक। यह उदाहरण पूर्ण कोड पाथ दिखाता है, प्रत्येक सेटिंग के पीछे की तर्क को समझाता है, और जब आप **Excel को txt में बदलते** हैं तो सामान्य समस्याओं को कवर करता है।

### आगे क्या करें?

* CSV (`CsvSaveOptions`) में निर्यात करने की कोशिश करें ताकि Excel‑संगत कॉमा‑सेपरेटेड फ़ाइलें मिलें।  
* `PdfSaveOptions` क्लास का अन्वेषण करें ताकि **Excel को PDF में निर्यात** एक ही लाइन में हो सके।  
* `workbook.Worksheets` पर इटररेट करके कई शीट्स को एक ही टेक्स्ट फ़ाइल में मिलाएँ।  

विकल्पों के साथ प्रयोग करने में संकोच न करें—सेपरेटर, परिशुद्धता, या शीट चयन बदलें ताकि आपका वर्कफ़्लो बिल्कुल आपके अनुसार हो।

हैप्पी कोडिंग!

## आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर कर सकें।

- [Save Excel as Text File with Custom Separator using Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel as txt – Complete C# Guide to Export Numbers with Significant Digits](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/)
- [How to Save Excel Files in Multiple Formats Using Aspose.Cells .NET (2023 Guide)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}