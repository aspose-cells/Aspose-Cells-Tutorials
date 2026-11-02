---
category: general
date: 2026-06-08
description: C# और Aspose.Cells का उपयोग करके Excel रेंज को इमेज के रूप में निर्यात
  करें। केवल कुछ सरल चरणों में Excel वर्कशीट को इमेज के रूप में सहेजना सीखें।
draft: false
keywords:
- export excel range as image
- save excel worksheet as image
- Aspose.Cells image export
- C# Excel automation
- pivot table to image
language: hi
og_description: C# के साथ Excel रेंज को इमेज के रूप में निर्यात करें। यह ट्यूटोरियल
  दिखाता है कि कैसे Excel वर्कशीट को जल्दी और भरोसेमंद तरीके से इमेज के रूप में सहेजा
  जाए।
og_title: एक्सेल रेंज को इमेज के रूप में निर्यात करें – पूर्ण C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  headline: Export Excel Range as Image – Complete C# Guide
  type: TechArticle
- description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  name: Export Excel Range as Image – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - Aspose.Cells
      for .NET ≥ 23.9 (you can grab a free trial from the Aspose website). - A basic
      understanding of C# and file I/O.'
  - name: What the code does
    text: '- `exportRange.ToImage` captures only the cells inside the range (pivot
      table or custom block). - `worksheet.ToImage` captures the *entire* visible
      area of the worksheet, effectively **save excel worksheet as image**.'
  - name: Multiple Pivot Tables
    text: 'If your workbook contains more than one pivot table, you can loop through
      them:'
  - name: Very Large Ranges
    text: 'Exporting a massive range (e.g., thousands of rows) can consume a lot of
      memory. Mitigate this by:'
  - name: Transparent Backgrounds
    text: 'If you need a transparent background (useful for overlaying on web pages),
      set the background color to `Color.Transparent` before export:'
  - name: File Permissions
    text: Make sure the target directory exists and your process has write permission.
      Otherwise `ToImage` throws an `IOException`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- ImageExport
title: एक्सेल रेंज को इमेज के रूप में निर्यात करें – पूर्ण C# गाइड
url: /hi/net/image-and-chart-operations/export-excel-range-as-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel रेंज को इमेज के रूप में एक्सपोर्ट करें – पूर्ण C# गाइड

क्या आपको कभी **export Excel range as image** करने की ज़रूरत पड़ी लेकिन सही API कॉल का पता नहीं चला? आप अकेले नहीं हैं। चाहे आप एक रिपोर्टिंग डैशबोर्ड बना रहे हों या PowerPoint स्लाइड के लिए पिवट टेबल का स्नैपशॉट चाहिए, सेल ब्लॉक को PNG में बदलना एक उपयोगी ट्रिक है।

इस गाइड में हम एक स्व-निहित उदाहरण के माध्यम से चलेंगे जो न केवल **export excel range as image** करता है बल्कि आपको **save excel worksheet as image** करने का तरीका भी दिखाता है पूरे शीट के लिए। कोई बाहरी स्क्रिप्ट नहीं, सिर्फ शुद्ध C# और Aspose.Cells, ताकि आप कोड को कॉपी‑पेस्ट करके तुरंत काम करता देख सकें।

## What You’ll Learn

- मौजूदा वर्कबुक को लोड करना और एक विशिष्ट रेंज (पिवट टेबल या कोई भी सेल ब्लॉक) को ढूँढना।  
- इमेज एक्सपोर्ट विकल्पों को कॉन्फ़िगर करना जैसे फॉर्मेट, रिज़ॉल्यूशन, और स्केलिंग।  
- एकल रेंज को PNG, JPEG, या BMP में एक्सपोर्ट करना।  
- उसी लॉजिक को **save excel worksheet as image** करने के लिए एक लाइन में विस्तारित करना।  
- कई पिवट टेबल, बड़े रेंज, और सामान्य समस्याओं को संभालने के टिप्स।

### Prerequisites

- .NET 6.0 या बाद का (कोड .NET Framework 4.7+ पर भी काम करता है)।  
- Aspose.Cells for .NET ≥ 23.9 (आप Aspose वेबसाइट से फ्री ट्रायल ले सकते हैं)।  
- C# और फ़ाइल I/O की बुनियादी समझ।  

अगर आपके पास ये सब है, तो चलिए शुरू करते हैं।

## Step 1: Set Up the Project and Import Namespaces

सबसे पहले, एक नया कंसोल ऐप बनाएं (या कोड को किसी मौजूदा प्रोजेक्ट में इंटीग्रेट करें)। Aspose.Cells NuGet पैकेज जोड़ें:

```bash
dotnet add package Aspose.Cells
```

फिर आवश्यक नेमस्पेसेज़ को स्कोप में लाएँ:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // For ImageOrPrintOptions
using System.Drawing.Imaging; // For ImageFormat enum
```

> **Pro tip:** अपने `using` स्टेटमेंट्स को फ़ाइल के शीर्ष पर रखें; इससे कोड स्कैन करना आसान हो जाता है—विशेषकर जब आप बाद में और Aspose फीचर्स जोड़ते हैं।

## Step 2: Load the Workbook Containing the Target Range

डिस्क पर एक वर्कबुक चाहिए। `YOUR_DIRECTORY/input.xlsx` को अपनी फ़ाइल के वास्तविक पाथ से बदलें।

```csharp
// Step 2: Load the workbook containing the data you want to capture
Workbook workbook = new Workbook(@"YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – make sure the file loaded correctly
if (workbook == null)
{
    Console.WriteLine("Failed to load workbook. Check the file path.");
    return;
}
```

यह कदम क्यों महत्वपूर्ण है: `Workbook` ऑब्जेक्ट हर Aspose.Cells ऑपरेशन का एंट्री पॉइंट है। इसके बिना आप वर्कशीट, रेंज, या पिवट टेबल को रेफ़र नहीं कर सकते।

## Step 3: Identify the Range to Export

आपके पास दो सामान्य परिदृश्य हैं:

1. **एक विशिष्ट पिवट टेबल** – आपके द्वारा पोस्ट किया गया कोड `PivotTables[0].PivotTableRange` का उपयोग करता है।  
2. **एक मनमाना सेल ब्लॉक** – आप `worksheet.Cells.CreateRange("B2:D10")` का उपयोग कर सकते हैं।

नीचे हम दोनों को हैंडल करते हैं, ताकि आप अपनी आवश्यकता के अनुसार चुन सकें।

```csharp
// Step 3a: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Option A: Export the first pivot table's range
Range exportRange;
if (worksheet.PivotTables.Count > 0)
{
    exportRange = worksheet.PivotTables[0].PivotTableRange;
}
else
{
    // Option B: Fallback to a manual range (e.g., B2:D10)
    exportRange = worksheet.Cells.CreateRange("B2:D10");
}
```

> **Why we check for pivot tables first:** Many reporting files rely on dynamic pivot data. If none exist, the fallback ensures the tutorial still works.

## Step 4: Configure Image Export Options

Aspose.Cells आपको आउटपुट इमेज पर सूक्ष्म नियंत्रण देता है। सबसे आम सेटिंग्स हैं फॉर्मेट, रिज़ॉल्यूशन (DPI), और ग्रिडलाइन शामिल करना या नहीं।

```csharp
// Step 4: Set up image export options
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG works well for lossless quality
    HorizontalResolution = 300,      // 300 DPI for crisp prints
    VerticalResolution = 300,
    // Optional: uncomment to hide gridlines
    // IsGridlinesVisible = false
};
```

अगर आपका डाउनस्ट्रीम सिस्टम JPEG या BMP पसंद करता है तो `ImageFormat.Jpeg` या `ImageFormat.Bmp` में स्विच कर सकते हैं। DPI सेटिंग तब महत्वपूर्ण होती है जब आप इमेज को हाई‑रेज़ॉल्यूशन PDFs या स्लाइड डेक में एम्बेड करते हैं।

## Step 5: Export the Range (or Whole Worksheet) as an Image

अब जादू होता है। `ToImage` मेथड रेंज का विज़ुअल प्रतिनिधित्व सीधे डिस्क पर लिखता है।

```csharp
// Step 5a: Export the selected range to an image file
string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
exportRange.ToImage(rangeImagePath, imgOptions);
Console.WriteLine($"Range exported to: {rangeImagePath}");

// Step 5b: If you need to **save excel worksheet as image**, use the worksheet's ToImage overload
string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";
worksheet.ToImage(sheetImagePath, imgOptions);
Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
```

### What the code does

- `exportRange.ToImage` केवल रेंज के भीतर के सेल्स (पिवट टेबल या कस्टम ब्लॉक) को कैप्चर करता है।  
- `worksheet.ToImage` वर्कशीट के *पूरे* दृश्य क्षेत्र को कैप्चर करता है, प्रभावी रूप से **save excel worksheet as image** करता है।  

दोनों कॉल्स आपके द्वारा पहले सेट किए गए विकल्पों का सम्मान करते हैं—इसलिए आपको 300 DPI रिज़ॉल्यूशन वाली PNG फ़ाइलें मिलेंगी।

## Handling Edge Cases & Common Questions

### Multiple Pivot Tables

अगर आपकी वर्कबुक में एक से अधिक पिवट टेबल हैं, तो आप उन्हें लूप कर सकते हैं:

```csharp
for (int i = 0; i < worksheet.PivotTables.Count; i++)
{
    Range ptRange = worksheet.PivotTables[i].PivotTableRange;
    string outPath = $@"YOUR_DIRECTORY/Pivot_{i}.png";
    ptRange.ToImage(outPath, imgOptions);
    Console.WriteLine($"Pivot {i} saved to {outPath}");
}
```

### Very Large Ranges

एक विशाल रेंज (जैसे हजारों पंक्तियों) को एक्सपोर्ट करने से बहुत मेमोरी खपत हो सकती है। इसे कम करने के लिए:

- `HorizontalResolution` / `VerticalResolution` को घटाएँ।  
- रेंज को छोटे ब्लॉक्स में विभाजित करके सेक्शन‑वाइज़ एक्सपोर्ट करें।  

### Transparent Backgrounds

अगर आपको ट्रांसपेरेंट बैकग्राउंड चाहिए (वेब पेज पर ओवरले करने के लिए उपयोगी), तो एक्सपोर्ट से पहले बैकग्राउंड कलर को `Color.Transparent` सेट करें:

```csharp
imgOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### File Permissions

सुनिश्चित करें कि टार्गेट डायरेक्टरी मौजूद है और आपके प्रोसेस के पास लिखने की अनुमति है। नहीं तो `ToImage` `IOException` फेंकेगा।

## Full Working Example

सब कुछ मिलाकर, यहाँ एक तैयार‑चलाने योग्य कंसोल प्रोग्राम है:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing.Imaging;

namespace ExcelImageExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths for your environment
            string inputPath = @"YOUR_DIRECTORY/input.xlsx";
            string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
            string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";

            // Load workbook
            Workbook workbook = new Workbook(inputPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // Determine which range to export
            Range exportRange;
            if (worksheet.PivotTables.Count > 0)
            {
                exportRange = worksheet.PivotTables[0].PivotTableRange;
            }
            else
            {
                exportRange = worksheet.Cells.CreateRange("B2:D10");
            }

            // Configure image options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // Export range as image
            exportRange.ToImage(rangeImagePath, imgOptions);
            Console.WriteLine($"Range exported to: {rangeImagePath}");

            // Export entire worksheet as image
            worksheet.ToImage(sheetImagePath, imgOptions);
            Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
        }
    }
}
```

**Expected output** (console):

```
Range exported to: YOUR_DIRECTORY/PivotRange.png
Worksheet exported to: YOUR_DIRECTORY/FullSheet.png
```

जनरेट की गई PNG फ़ाइलें खोलें और आप चयनित रेंज और पूरी शीट का पिक्सेल‑परफेक्ट स्नैपशॉट देखेंगे।

## Conclusion

हमने अभी-अभी वह सब कवर किया जो आपको **export excel range as image** करने और Aspose.Cells तथा C# का उपयोग करके **save excel worksheet as image** करने के लिए चाहिए। वर्कबुक लोड करने से लेकर इमेज विकल्पों को फाइन‑ट्यून करने और कई पिवट को संभालने तक, कदम सरल और पूरी तरह से दोहराने योग्य हैं।

आगे आप कर सकते हैं:

- विभिन्न `ImageFormat` वैल्यूज़ (JPEG, BMP) के साथ प्रयोग करें।  
- रिपोर्ट जनरेशन के लिए `Document` क्लास का उपयोग करके इमेज को PDF के साथ कॉम्बाइन करें।  
- फ़ोल्डर में फ़ाइलों के बैच के लिए प्रोसेस को ऑटोमेट करें।

कोड को अपने वर्कफ़्लो के अनुसार अनुकूलित करें—चाहे आप इमेज को वेब API में फीड कर रहे हों, ईमेल में एम्बेड कर रहे हों, या प्रिंटेबल रिपोर्ट बना रहे हों। हैप्पी कोडिंग, और आपके Excel डेटा को इमेज़ बोलने दें!

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का पता लगा सकें।

- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Export Excel Workbook As Image Using Aspose Cells For Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}