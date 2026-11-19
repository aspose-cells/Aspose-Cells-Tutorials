---
category: general
date: 2026-11-19
description: Aspose.Cells में CopyOptions का उपयोग करके रेंज को कॉपी करना सीखें, फ़ॉर्मेटिंग
  और पिवट टेबल्स को संरक्षित रखते हुए फ़ॉर्मेटिंग के साथ Excel रेंज को कॉपी करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: hi
lastmod: 2026-11-19
og_description: Aspose.Cells में CopyOptions का उपयोग करके रेंज कॉपी करने से आप Excel
  डेटा को पूरी फ़ॉर्मेटिंग और पिवट टेबल्स को संरक्षित रखते हुए डुप्लिकेट कर सकते हैं,
  जिससे विश्वसनीय वर्कबुक मैनिपुलेशन संभव होता है।
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Aspose.Cells में CopyOptions का उपयोग करके रेंज कॉपी करें – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cells में CopyOptions का उपयोग करके रेंज कैसे कॉपी करें
url: /hi/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# CopyOptions का उपयोग करके Aspose.Cells में रेंज कॉपी कैसे करें

यदि आपको Aspose.Cells में **CopyOptions का उपयोग करके रेंज कॉपी** करनी है, तो यह गाइड आपको दिखाता है कि कैसे सेल्स के एक ब्लॉक को डुप्लिकेट किया जाए जबकि सभी फ़ॉर्मेटिंग और एम्बेडेड पिवट टेबल्स को बरकरार रखा जाए। कई डेवलपर्स को वर्कशीट्स के बीच डेटा मूव करते समय स्टाइल को संरक्षित करने में समस्या होती है, और `CopyOptions` क्लास इस समस्या को अतिरिक्त मैनुअल कदमों के बिना हल करती है।

इस ट्यूटोरियल में आप सीखेंगे:

* Excel वर्कबुक में स्रोत और गंतव्य क्षेत्रों को परिभाषित करना।  
* `CopyOptions` का उपयोग करके सेल फ़ॉर्मेटिंग, कॉलम चौड़ाई और पिवट टेबल्स को बनाए रखना।  
* परिणाम को नई फ़ाइल में सहेजना, जो आगे की प्रोसेसिंग के लिए तैयार हो।

उदाहरण किसी भी `.xlsx` फ़ाइल के साथ काम करता है और केवल Aspose.Cells for .NET लाइब्रेरी की आवश्यकता होती है।

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* .NET 6.0 या बाद का संस्करण स्थापित हो।  
* एक वैध Aspose.Cells for .NET लाइसेंस (या एक मुफ्त इवैल्यूएशन की)।  
* Visual Studio 2022 या कोई भी C# IDE जो आप पसंद करते हैं।  

`Aspose.Cells` के अलावा कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है।

## चरण 1: प्रोजेक्ट सेट अप करें और नेमस्पेस इम्पोर्ट करें

एक नया कंसोल एप्लिकेशन बनाएं और Aspose.Cells रेफ़रेंस जोड़ें:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

`using Aspose.Cells;` निर्देश आपको `Workbook`, `CellArea`, और `CopyOptions` तक पहुँच देता है।

## चरण 2: वह वर्कबुक लोड करें जिसे आप संशोधित करना चाहते हैं

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook` पूरे Excel फ़ाइल का प्रतिनिधित्व करता है। `YOUR_DIRECTORY` को उस फ़ोल्डर से बदलें जिसमें आपका स्रोत फ़ाइल स्थित है।

## चरण 3: स्रोत और गंतव्य रेंज को परिभाषित करें

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea` शीर्ष‑बाएँ और नीचे‑दाएँ सेल पतों के आधार पर एक आयताकार क्षेत्र बनाता है। आप कॉपी करने वाले ब्लॉक के आकार के अनुसार निर्देशांक समायोजित कर सकते हैं।

## चरण 4: फ़ॉर्मेटिंग और पिवट टेबल्स को संरक्षित रखते हुए रेंज कॉपी करें

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

`CopyOptions` ऑब्जेक्ट Aspose.Cells को बताता है कि क्या रखना है। `CopyPivotTables = true` सेट करना **CopyOptions का उपयोग करके रेंज कॉपी** करने की कुंजी है जब आपके स्रोत में पिवट टेबल्स शामिल हों। अन्य फ़्लैग यह सुनिश्चित करते हैं कि **फ़ॉर्मेटिंग के साथ Excel रेंज कॉपी** स्वचालित रूप से प्राप्त हो—कॉपी के बाद स्टाइल को पुनः लागू करने के लिए कोई अतिरिक्त कोड आवश्यक नहीं है।

### क्यों `CopyOptions` महत्वपूर्ण है

* **Performance** – लाइब्रेरी एकल आंतरिक ऑपरेशन करती है, न कि सेल‑बाय‑सेल कॉपी।  
* **Accuracy** – सभी दृश्य पहलू (फ़ॉन्ट, रंग, बॉर्डर) स्थानांतरण के बाद भी बरकरार रहते हैं, जिससे उत्पन्न रिपोर्ट में दृश्य विचलन समाप्त हो जाता है।  
* **Reliability** – पिवट टेबल्स कार्यात्मक रहती हैं क्योंकि उनका कैश और स्रोत रेफ़रेंसेज़ डुप्लिकेट हो जाते हैं।

## चरण 5: संशोधित वर्कबुक सहेजें

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

`Save` कॉल करने के बाद फ़ाइल `output.xlsx` में मूल डेटा के साथ गंतव्य स्थान पर डुप्लिकेट ब्लॉक शामिल होगा, जिसमें फ़ॉर्मेटिंग और पिवट टेबल्स दोनों ही मौजूद होंगे।

## संदर्भ के लिए पूर्ण स्रोत कोड

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

इस प्रोग्राम को चलाने पर यह आउटपुट देगा:

```
Range copied successfully. Output saved to output.xlsx
```

`output.xlsx` को Excel में खोलें – आपको ब्लॉक A1:H30 का डुप्लिकेट A35:H64 पर दिखाई देगा, सभी सेल रंग, बॉर्डर, नंबर फ़ॉर्मेट और पिवट टेबल्स सहित।

## सामान्य प्रश्न और एज‑केस हैंडलिंग

### यदि गंतव्य क्षेत्र स्रोत के साथ ओवरलैप करता है तो क्या होगा?

Aspose.Cells `ArgumentException` फेंकता है। इसे टालने के लिए ऐसा गंतव्य निर्धारित करें जो स्रोत के साथ नहीं intersect करता, या किसी अलग वर्कशीट में कॉपी करें:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### विभिन्न वर्कबुक्स के बीच कैसे कॉपी करें?

लक्ष्य फ़ाइल के लिए दूसरा `Workbook` इंस्टेंस बनाएं और वही `CopyOptions` ऑब्जेक्ट उपयोग करें:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### क्या `CopyOptions` मर्ज्ड सेल्स को भी कॉपी करता है?

हां। `CopyStyle` फ़्लैग में मर्ज्ड‑सेल जानकारी शामिल होती है। यदि आपको अधिक सूक्ष्म नियंत्रण चाहिए, तो `options.CopyMergedCells = true` सेट करें (नए संस्करणों में उपलब्ध)।

### बड़े रेंज (हजारों पंक्तियों) के बारे में क्या?

ऑपरेशन मेमोरी‑कुशल है, लेकिन बहुत बड़े फ़ाइलों के लिए आप `WorkbookSettings` के `MemorySetting` को `MemorySetting.MemoryPreference` पर बढ़ा सकते हैं।

## प्रो टिप्स

* कई कॉपी ऑपरेशन्स के लिए **एक ही `CopyOptions`** इंस्टेंस को पुनः उपयोग करें – इससे ऑब्जेक्ट अलोकेशन ओवरहेड कम होता है।  
* कॉपी करने से पहले **रेंज वैधता** जांचें: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` टाइपो‑संबंधी त्रुटियों को जल्दी पकड़ने में मदद करता है।  
* बड़े डेटा सेट कॉपी करते समय **कैल्कुलेशन बंद** (`workbook.Settings.CalcMode = CalculationMode.Manual`) करें ताकि प्रक्रिया तेज़ हो, और कॉपी के बाद यदि अपडेटेड परिणाम चाहिए तो `workbook.CalculateFormula()` कॉल करें।

## निष्कर्ष

अब आप जानते हैं कि Aspose.Cells में **CopyOptions का उपयोग करके रेंज कॉपी** कैसे की जाती है, जिससे **फ़ॉर्मेटिंग के साथ Excel रेंज कॉपी** पूरी तरह से प्राप्त होती है जबकि पिवट टेबल्स और अन्य उन्नत फीचर्स संरक्षित रहते हैं। यह तरीका मैनुअल स्टाइल पुनः लागू करने की आवश्यकता को समाप्त करता है और आपके Excel ऑटोमेशन को मजबूत और मेंटेन करने योग्य बनाता है।

आप आगे इन चरणों का अन्वेषण कर सकते हैं:

* `CopyOptions` का उपयोग करके पूरी वर्कशीट्स को डुप्लिकेट करें।  
* टेम्पलेट‑आधारित रिपोर्ट जनरेशन के लिए कॉपी ऑपरेशन को `WorksheetCollection.AddCopy` के साथ संयोजित करें।  
* कोड को ASP.NET Core API में इंटीग्रेट करें ताकि ऑन‑द‑फ़्लाई Excel ट्रांसफ़ॉर्मेशन प्रदान किया जा सके।

विभिन्न स्रोत/गंतव्य निर्देशांक के साथ प्रयोग करने के लिए स्वतंत्र महसूस करें, और अपने परिणाम टिप्पणी में साझा करें!

## आगे आप क्या सीख सकते हैं?

निम्नलिखित ट्यूटोरियल्स इस गाइड में प्रदर्शित तकनीकों पर आधारित निकट-संबंधित विषयों को कवर करते हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Excel Aspose Cells .NET रेंज डेटा कॉपी](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET रेंज डेटा कॉपी](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells .NET रेंज डेटा कॉपी](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}