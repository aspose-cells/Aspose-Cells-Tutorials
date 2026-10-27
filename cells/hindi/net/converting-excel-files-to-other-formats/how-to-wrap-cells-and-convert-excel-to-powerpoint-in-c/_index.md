---
category: general
date: 2026-09-18
description: Excel वर्कबुक में सेल्स को रैप कैसे करें और इसे PowerPoint फ़ाइल के रूप
  में सहेजें। WRAPCOLS का उपयोग करना सीखें, वर्कबुक शीट बनाएं, और PPTX में निर्यात
  करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to wrap cells
- convert excel to powerpoint
- save excel as powerpoint
- how to use wrapcols
- create workbook worksheet
language: hi
lastmod: 2026-09-18
og_description: Excel में सेल्स को रैप करने और C# का उपयोग करके वर्कबुक को एक संपादन
  योग्य PowerPoint फ़ाइल के रूप में निर्यात करने का तरीका। WRAPCOLS और वर्कबुक वर्कशीट
  निर्माण में निपुण होने के लिए चरण‑दर‑चरण गाइड का पालन करें।
og_image_alt: Diagram showing how to wrap cells in Excel before exporting to PowerPoint
og_title: C# में सेल्स को रैप करना और एक्सेल को पावरपॉइंट में बदलना कैसे करें
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: How to wrap cells in an Excel workbook and save it as a PowerPoint
    file. Learn to use WRAPCOLS, create workbook worksheet, and export to PPTX.
  headline: How to wrap cells and convert Excel to PowerPoint in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: C# में सेल्स को रैप करना और Excel को PowerPoint में बदलना कैसे करें
url: /hi/net/converting-excel-files-to-other-formats/how-to-wrap-cells-and-convert-excel-to-powerpoint-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में सेल को रैप करने और Excel को PowerPoint में बदलने का तरीका

यदि आपको Excel शीट में **सेल को रैप कैसे करें** करने की आवश्यकता है और फिर उस शीट को PowerPoint प्रस्तुति में बदलना है, तो यह गाइड आपको एक पूर्ण, तैयार‑चलाने योग्य समाधान दिखाता है। पहले दो वाक्यों के अंत तक आप ठीक‑ठीक जान जाएंगे कि कौन से API कॉल रैप को निष्पादित करते हैं और कौन सी विधि फ़ाइल को PPTX के रूप में सहेजती है।

हम Aspose.Cells for .NET का उपयोग करेंगे, एक लाइब्रेरी जो Microsoft Office स्थापित किए बिना Excel वर्कबुक को मैनीपुलेट करने देती है। ट्यूटोरियल में **convert Excel to PowerPoint**, **how to use WRAPCOLS** और **create workbook worksheet** की सर्वोत्तम प्रथाओं को दर्शाया गया है। कोई बाहरी उपकरण आवश्यक नहीं है—सिर्फ एक .NET विकास वातावरण।

## आवश्यकताएँ

- .NET 6.0 या बाद का (कोड .NET Framework 4.6+ के साथ भी काम करता है)
- Aspose.Cells for .NET NuGet पैकेज (`Install-Package Aspose.Cells`)
- C# और वर्कशीट्स की अवधारणा से बुनियादी परिचितता
- Visual Studio या VS Code जैसे IDE

> **Pro tip:** प्रयोग के दौरान Aspose.Cells का मुफ्त इवैल्यूएशन लाइसेंस उपयोग करें; उत्पादन से पहले इसे पूर्ण लाइसेंस से बदल दें।

## चरण 1: एक वर्कबुक बनाएं और एक वर्कशीट जोड़ें

पहला काम जो आपको **create workbook worksheet** करना है वह है `Workbook` ऑब्जेक्ट का इंस्टैंसिएशन। डिफ़ॉल्ट रूप से Aspose.Cells एक वर्कशीट (इंडेक्स 0) बनाता है, जिसे हम डेमो के लिए उपयोग करेंगे।

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Step 1: Initialize a new workbook (creates one worksheet automatically)
        Workbook workbook = new Workbook();

        // Reference the first worksheet for later operations
        Worksheet ws = workbook.Worksheets[0];
```

**Why this matters:** वर्कबुक को इनिशियलाइज़ करने से आपको एक साफ़ कैनवास मिलता है। डिफ़ॉल्ट वर्कशीट पहले से ही `Worksheets` कलेक्शन का हिस्सा है, इसलिए आपको `Add()` कॉल करने की आवश्यकता नहीं है जब तक आप अतिरिक्त शीट्स नहीं चाहते।

## चरण 2: स्रोत रेंज (A2:A10) को भरें

सेल को रैप करने से पहले, हमें रैप करने के लिए कुछ डेटा चाहिए। यह चरण सेल A2 से A10 तक नमूना टेक्स्ट भरता है।

```csharp
        // Fill cells A2:A10 with a long string to demonstrate wrapping
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }
```

**Edge case:** यदि स्रोत रेंज खाली है, तो `WRAPCOLS` `#VALUE!` लौटाता है। हमेशा सुनिश्चित करें कि रेंज में कम से कम एक गैर‑खाली सेल हो।

## चरण 3: WRAPCOLS फ़ॉर्मूला लागू करें

अब हम मुख्य प्रश्न **how to use WRAPCOLS** का उत्तर देते हैं। फ़ॉर्मूला एक वर्टिकल रेंज लेता है और उसे निर्दिष्ट संख्या के कॉलम में वितरित करता है। हम फ़ॉर्मूला को सेल `A1` में लिखते हैं; resulting array स्वचालित रूप से निकटवर्ती सेल्स में फैल जाएगा।

```csharp
        // Step 3: Apply WRAPCOLS to wrap A2:A10 into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";
```

**What happens under the hood:** `WRAPCOLS` स्रोत रेंज का मूल्यांकन करता है, आइटम्स को लक्ष्य कॉलम्स में समान रूप से (या जितना संभव हो) विभाजित करता है, और मानों को एक आयताकार ब्लॉक में लिखता है। ब्लॉक का आकार डायनामिक होता है, इसलिए आपको गंतव्य रेंज पहले से परिभाषित करने की जरूरत नहीं है।

## चरण 4: वर्कबुक को एक संपादन योग्य PowerPoint फ़ाइल के रूप में सहेजें

अंत में, हम **convert Excel to PowerPoint** और **save Excel as PowerPoint** को संबोधित करते हैं। Aspose.Cells एक वर्कशीट को सीधे PPTX में एक्सपोर्ट कर सकता है, लेआउट को एक संपादन योग्य शैप के रूप में संरक्षित रखता है।

```csharp
        // Step 4: Export the worksheet to an editable PPTX presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

**Why PPTX?** उत्पन्न PowerPoint में एक ही स्लाइड होती है जिसमें रैप किए गए सेल्स को टेबल के रूप में रेंडर किया गया है। आप फ़ाइल को Microsoft PowerPoint में खोल सकते हैं, टेक्स्ट संपादित कर सकते हैं, स्टाइल बदल सकते हैं, या अतिरिक्त स्लाइड्स जोड़ सकते हैं—सब कुछ पूरी तरह से संपादन योग्य रहता है।

### अपेक्षित आउटपुट

- **Excel side:** सेल `A1` मूल लंबी स्ट्रिंग्स का 3‑कॉलम एरे दिखाता है, प्रत्येक कॉलम में लगभग समान संख्या में पंक्तियाँ होती हैं।
- **PowerPoint side:** `ChartEditable.pptx` खोलने पर एक स्लाइड दिखती है जिसमें एक टेबल है जो रैप किए गए लेआउट को प्रतिबिंबित करता है। टेबल को चयनित, आकार बदल या संपादित किया जा सकता है जैसे कोई भी मूल PowerPoint ऑब्जेक्ट।

## सामान्य विविधताएँ और किन बातों पर ध्यान दें

| परिदृश्य | समायोजन |
|----------|------------|
| **अधिक कॉलम में रैप करें** | `WRAPCOLS` के दूसरे आर्ग्युमेंट को बदलें, उदाहरण के लिए `=WRAPCOLS(A2:A10,5)`। |
| **एक अलग रेंज को रैप करें** | फ़ॉर्मूला रेफ़रेंस अपडेट करें, उदाहरण के लिए `=WRAPCOLS(B2:B15,2)`। |
| **शीट का केवल एक भाग एक्सपोर्ट करें** | `Worksheet.ExportDataTable` का उपयोग करके एक `DataTable` निकालें और फिर कस्टम PPTX निर्माण के लिए `Presentation` APIs का उपयोग करें। |
| **बड़ी वर्कशीट्स ( > 10 000 पंक्तियाँ )** | प्रदर्शन बाधाओं से बचने के लिए एक्सपोर्ट को कई स्लाइड्स में विभाजित करने पर विचार करें। |

> **Watch out for:** जब वर्कबुक में चार्ट होते हैं तो डिफ़ॉल्ट PPTX एक्सपोर्ट वर्कशीट को एक सिंगल इमेज के रूप में रेंडर करता है। `WRAPCOLS` का उपयोग करने से डेटा टेबल के रूप में रहता है, जो संपादन योग्य बना रहता है।

## त्वरित कॉपी‑पेस्ट के लिए पूर्ण स्रोत कोड

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Create a new workbook (contains one default worksheet)
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Populate A2:A10 with sample long text
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }

        // Apply WRAPCOLS to wrap the range into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Save as an editable PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

फ़ाइल को `Program.cs` के रूप में सहेजें, NuGet पैकेज पुनर्स्थापित करें, और चलाएँ:

```bash
dotnet run
```

आपको कंसोल संदेश दिखाई देगा जो एक्सपोर्ट की पुष्टि करता है, और PPTX फ़ाइल निर्दिष्ट फ़ोल्डर में दिखाई देगी।

## निष्कर्ष

अब आप Excel वर्कशीट में **सेल को रैप कैसे करें** करना, **how to use WRAPCOLS** और Aspose.Cells का उपयोग करके **convert Excel to PowerPoint** तथा **save excel as powerpoint** करने के सटीक चरण जानते हैं। पूर्ण समाधान **create workbook worksheet** को दर्शाता है, रैप फ़ॉर्मूला लागू करता है, और एक संपादन योग्य PPTX फ़ाइल उत्पन्न करता है जो प्रस्तुति समायोजन के लिए तैयार है।

### अगले कदम

- एक्सपोर्ट करने से पहले अन्य Excel फ़ंक्शन्स (जैसे `TRANSPOSE`, `FILTER`) का अन्वेषण करें।
- लूप का उपयोग करके कई वर्कशीट्स को एक मल्टी‑स्लाइड PowerPoint डेक में संयोजित करें।
- एक्सपोर्ट के बाद Aspose.Slides को इंटीग्रेट करके कस्टम स्लाइड शीर्षक या ब्रांडिंग जोड़ें।

विभिन्न कॉलम काउंट, स्रोत रेंज, या एक ही PPTX में चार्ट और टेबल को संयोजित करने के साथ प्रयोग करने में संकोच न करें। कोडिंग का आनंद लें!

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच का अन्वेषण करने में मदद करती हैं।

- [Aspose.Cells for .NET का उपयोग करके Excel को PowerPoint में कैसे बदलें: एक पूर्ण गाइड](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Aspose.Cells for .NET का उपयोग करके Excel में टेक्स्ट को रैप कैसे करें | फ़ॉर्मेटिंग ट्यूटोरियल](/cells/english/net/formatting/wrap-text-excel-aspose-cells-net/)
- [Aspose.Cells for .NET का उपयोग करके Excel वर्कबुक और वर्कशीट प्रॉपर्टीज़ को HTML में एक्सपोर्ट करें](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}