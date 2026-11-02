---
category: general
date: 2026-03-22
description: Excel में प्रिंट एरिया सेट करें और Excel को संपादन योग्य आकारों के साथ
  PowerPoint में बदलें। जानें कैसे शीर्षक पंक्ति को दोहराएँ, Excel से PowerPoint बनाएँ
  और Excel को PPTX में निर्यात करें।
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: hi
og_description: Excel में प्रिंट एरिया सेट करें और इसे संपादन योग्य आकारों के साथ
  PowerPoint स्लाइड में बदलें। शीर्षक पंक्ति को दोहराने और Excel को PPTX में निर्यात
  करने के लिए इस पूर्ण गाइड का पालन करें।
og_title: एक्सेल में प्रिंट एरिया सेट करें – पावरपॉइंट में निर्यात ट्यूटोरियल
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: एक्सेल में प्रिंट एरिया सेट करें और पावरपॉइंट में निर्यात करें – चरण‑दर‑चरण
  गाइड
url: /hi/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में प्रिंट एरिया सेट करें और PowerPoint में एक्सपोर्ट करें – पूर्ण प्रोग्रामिंग ट्यूटोरियल

क्या आपको कभी **प्रिंट एरिया सेट** करना पड़ा है Excel वर्कशीट में और फिर उस हिस्से को PowerPoint स्लाइड में बदलना पड़ा है? आप अकेले नहीं हैं। कई रिपोर्टिंग पाइपलाइन में वही डेटा जो प्रिंट में अच्छा दिखता है, उसे प्रेजेंटेशन में भी दिखाना पड़ता है, अक्सर पहली पंक्ति को शीर्षक के रूप में दोहराया जाता है। अच्छी खबर? कुछ ही C# लाइनों से आप **excel को powerpoint में बदल** सकते हैं, सभी टेक्स्ट बॉक्स को एडिटेबल रख सकते हैं, और यहाँ तक कि **शीर्षक पंक्ति दोहराएँ** स्वचालित रूप से।

इस गाइड में हम सब कुछ कवर करेंगे: प्रिंट एरिया को कॉन्फ़िगर करने से लेकर एक PPTX फ़ाइल बनाने तक जिसे आप सीधे PowerPoint में एडिट कर सकते हैं। अंत तक आप **excel से powerpoint बनाना**, परिणाम को **excel को pptx में एक्सपोर्ट** करना, और उसी कोड को किसी भी .NET प्रोजेक्ट में पुनः उपयोग करना सीख जाएंगे। कोई जादू नहीं, सिर्फ़ स्पष्ट कदम और एक पूर्ण, चलाने योग्य उदाहरण।

## What You’ll Need

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- **.NET 6.0** या बाद का संस्करण (API .NET Framework के साथ भी काम करता है)
- **Aspose.Cells for .NET** (लाइब्रेरी जो `Workbook`, `ImageOrPrintOptions` आदि प्रदान करती है)
- एक बेसिक C# IDE (Visual Studio, Rider, या C# एक्सटेंशन वाला VS Code)
- एक Excel फ़ाइल (`input.xlsx`) जिसमें वह डेटा हो जिसे आप एक्सपोर्ट करना चाहते हैं

बस इतना ही—Aspose.Cells के अलावा कोई अतिरिक्त NuGet पैकेज नहीं चाहिए। यदि आपने अभी तक लाइब्रेरी नहीं जोड़ी है, तो चलाएँ:

```bash
dotnet add package Aspose.Cells
```

अब हम तैयार हैं।

## Step 1: Load the Workbook – the Starting Point for Export

सबसे पहले आपको वह वर्कबुक लोड करनी होगी जिसमें वह शीट है जिसे आप स्लाइड में बदलना चाहते हैं। वर्कबुक को स्रोत दस्तावेज़ समझें; इसके बिना बाकी सब बेकार है।

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**क्यों महत्वपूर्ण है:** वर्कबुक लोड करने से आपको वर्कशीट कलेक्शन, पेज‑सेटअप विकल्प, और एक्सपोर्ट इंजन तक पहुँच मिलती है। यदि आप इस कदम को छोड़ देंगे तो आप **प्रिंट एरिया** सेट नहीं कर पाएंगे और न ही कोई पंक्तियों को दोहरा पाएंगे।

> **Pro tip:** टेस्टिंग के दौरान एब्सोल्यूट पाथ इस्तेमाल करें, फिर प्रोडक्शन के लिए रिलेटिव या कॉन्फ़िगरेशन‑आधारित पाथ पर स्विच करें।

## Step 2: Configure Export Options – Keep Text Boxes and Shapes Editable

जब आप PowerPoint में एक्सपोर्ट करते हैं तो आमतौर पर आप चाहते हैं कि परिणामस्वरूप स्लाइड एडिटेबल हो। Aspose.Cells आपको `ImageOrPrintOptions` के साथ यह नियंत्रित करने देता है। `ExportTextBoxes` और `ExportShapeObjects` को `true` सेट करने से लाइब्रेरी उन ऑब्जेक्ट्स को नेेटिव PowerPoint एलिमेंट्स के रूप में रखती है, न कि इमेज में फ्लैटनिंग करके।

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**क्यों महत्वपूर्ण है:** यदि आपको कभी **excel को powerpoint में बदल**ना है और फिर स्लाइड को मैन्युअली ट्यून करना है, तो यह सेटिंग आपको टेक्स्ट बॉक्स को फिर से बनाने से बचाती है। यह यह भी सुनिश्चित करता है कि कोई भी शेप (जैसे एरो या चार्ट) वेक्टर ऑब्जेक्ट के रूप में रहे जिसे आप रिसाइज़ कर सकते हैं।

## Step 3: Set Print Area and Repeat the Title Row

अब हम ट्यूटोरियल के मुख्य भाग पर आते हैं: **प्रिंट एरिया सेट** करें और पहली पंक्ति को हर प्रिंट पेज (या हमारे मामले में, एक्सपोर्ट की गई स्लाइड) पर दोहराएँ। प्रिंट एरिया Excel को बताता है कि कौन‑से सेल्स को प्रिंट या हमारे परिदृश्य में एक्सपोर्ट करना है।

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**क्यों महत्वपूर्ण है:** एक्सपोर्ट को `A1:G20` तक सीमित करके आप बड़े खाली रेंज को खींचने से बचते हैं, जिससे रूपांतरण तेज़ होता है और स्लाइड साफ़ रहती है। `PrintTitleRows` लाइन पहली पंक्ति को हेडर की तरह बनाती है—बिल्कुल वही जो आप **शीर्षक पंक्ति दोहराएँ** चाहते हैं प्रेजेंटेशन में।

> **Edge case:** यदि आपका डेटा पंक्ति 2 से शुरू होता है, तो रेंज को उसी अनुसार बदलें (उदा., `PrintTitleRows = "$2:$2"`).

## Step 4: Save the Worksheet as a PowerPoint File

अंत में, हम स्लाइड को डिस्क पर लिखते हैं। `Save` मेथड लक्ष्य फ़ाइलनाम और पहले कॉन्फ़िगर किए गए विकल्प लेता है। परिणाम एक PPTX फ़ाइल है जिसमें एडिटेबल टेक्स्ट बॉक्स और शेप्स होते हैं, जिसे आप सीधे PowerPoint में खोल सकते हैं।

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**आपको क्या दिखेगा:** `SheetWithEditableShapes.pptx` को PowerPoint में खोलें। पहली पंक्ति शीर्षक के रूप में दिखेगी, `A1:G20` की सभी सेल्स रेंडर होंगी, और Excel में जो भी शेप्स जोड़े थे वे अभी भी मूवेबल और एडिटेबल रहेंगे। कोई रास्टराइज़्ड इमेज नहीं—सिर्फ़ नेेटिव PowerPoint ऑब्जेक्ट्स।

## Full Working Example – All Steps Combined

नीचे पूरा, कॉपी‑पेस्ट‑तैयार प्रोग्राम दिया गया है। इसे एक कंसोल ऐप के रूप में चलाएँ या किसी बड़े सॉल्यूशन में एम्बेड करें।

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**अपेक्षित आउटपुट:** प्रोग्राम चलाने के बाद कंसोल में सफलता संदेश प्रिंट होगा, और निर्दिष्ट स्थान पर PPTX फ़ाइल बन जाएगी। फ़ाइल खोलने पर एक ही स्लाइड दिखेगी जिसमें चयनित रेंज, एडिटेबल टेक्स्ट बॉक्स, और मूल शेप्स होंगी।

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| **Does this work with multiple worksheets?** | हाँ। `workbook.Worksheets` पर लूप करें और प्रत्येक शीट के लिए वही कदम दोहराएँ, प्रत्येक बार आउटपुट फ़ाइलनाम बदलें। |
| **What if I need to export more than one slide?** | `workbook.Save` को कई बार अलग‑अलग `ImageOrPrintOptions` ऑब्जेक्ट्स के साथ कॉल करें, आवश्यकतानुसार अलग `PageSetup` कॉन्फ़िगर करें। |
| **Can I change the slide size?** | स्लाइड DPI सेट करने के लिए `exportOptions.ImageFormat` उपयोग करें, या सेव करने से पहले `sheet.PageSetup.PaperSize` समायोजित करें। |
| **Is Aspose.Cells free?** | यह वॉटरमार्क के साथ एक फ्री इवैल्यूएशन देता है। प्रोडक्शन के लिए लाइसेंस आवश्यक है। |
| **What about Excel formulas?** | एक्सपोर्ट किए गए मान **एक्सपोर्ट के समय के गणना परिणाम** होते हैं। यदि आपको PowerPoint में लाइव फ़ॉर्मूले चाहिए, तो आपको अलग तरीका अपनाना पड़ेगा। |

## Tips for a Smooth Workflow

- **Pro tip:** एक्सपोर्ट से पहले `Workbook.Settings.CalcMode = CalculationModeType.Automatic` सेट करें ताकि सभी फ़ॉर्मूले अपडेटेड हों।
- **Watch out for:** बहुत बड़े रेंज मेमोरी प्रेशर पैदा कर सकते हैं। प्रिंट एरिया को आवश्यक न्यूनतम रेंज तक सीमित रखें।
- **Performance tip:** यदि आप कई शीट्स एक्सपोर्ट कर रहे हैं तो एक ही `ImageOrPrintOptions` इंस्टेंस को पुनः उपयोग करें; हर बार नया बनाना ओवरहेड बढ़ाता है।
- **Version note:** ऊपर दिया गया कोड Aspose.Cells 23.10 (नवंबर 2023) को टारगेट करता है। बाद के संस्करण समान API रखते हैं, लेकिन हमेशा रिलीज़ नोट्स में ब्रेकिंग चेंजेज़ की जाँच करें।

## Conclusion

हमने बताया कि कैसे **Excel वर्कशीट में प्रिंट एरिया सेट** करें, पहली पंक्ति को शीर्षक के रूप में दोहराएँ, और फिर **excel को pptx में एक्सपोर्ट** करें जबकि एडिटेबल टेक्स्ट बॉक्स और शेप्स को बरकरार रखें। संक्षेप में, अब आप भरोसेमंद तरीके से **excel को powerpoint में बदल**, **शीर्षक पंक्ति दोहराएँ**, और **excel से powerpoint बनाएँ** सिर्फ़ कुछ C# लाइनों से कर सकते हैं।

अगला कदम तैयार है? दर्जनों रिपोर्टों की बैच कन्वर्ज़न को ऑटोमेट करें, या एक्सपोर्ट के बाद PowerPoint SDK का उपयोग करके कस्टम स्लाइड लेआउट जोड़ें। संभावनाएँ अनंत हैं—प्रयोग करें, नई चीज़ें आज़माएँ, और प्रोग्रामेटिक डॉक्यूमेंट जेनरेशन की शक्ति का आनंद लें।

यदि यह ट्यूटोरियल आपके काम आया, तो इसे शेयर करें, अपने खुद के ट्वीक के साथ कमेंट डालें, या हमारे अन्य गाइड्स पर नज़र डालें **excel को pptx में एक्सपोर्ट** और संबंधित ऑटोमेशन टॉपिक्स पर। Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}