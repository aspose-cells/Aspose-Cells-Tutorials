---
category: general
date: 2026-02-26
description: C# का उपयोग करके Excel से PowerPoint में चार्ट निर्यात करें। जानें कैसे
  Excel को PowerPoint में बदलें, Excel को PowerPoint के रूप में सहेजें और आकृतियों
  को संपादन योग्य रखें।
draft: false
keywords:
- export chart to powerpoint
- convert excel to powerpoint
- save excel as powerpoint
- how to convert excel to ppt
- save workbook as pptx
language: hi
og_description: C# का उपयोग करके Excel से PowerPoint में चार्ट निर्यात करें। यह गाइड
  दिखाता है कि Excel को PowerPoint में कैसे बदलें, वर्कबुक को PPTX के रूप में सहेजें
  और आकृतियों को संपादन योग्य रखें।
og_title: C# के साथ चार्ट को PowerPoint में निर्यात करें – पूर्ण प्रोग्रामिंग ट्यूटोरियल
tags:
- Aspose.Cells
- C#
- Office Automation
title: C# के साथ चार्ट को PowerPoint में निर्यात करें – पूर्ण चरण‑दर‑चरण मार्गदर्शिका
url: /hi/net/chart-rendering-and-conversion/export-chart-to-powerpoint-with-c-complete-step-by-step-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PowerPoint में चार्ट निर्यात करें – पूर्ण प्रोग्रामिंग ट्यूटोरियल

क्या आपने कभी सोचा है कि **चार्ट को PowerPoint में निर्यात** करते समय संपादन योग्यता कैसे बनी रहे? कई रिपोर्टिंग परिदृश्यों में आपको स्लाइड डेक के अंदर एक लाइव चार्ट चाहिए होता है, फिर भी मैन्युअल कॉपी‑पेस्ट बहुत झंझट है। अच्छी खबर यह है कि आप इसे कुछ ही पंक्तियों के C# कोड से प्रोग्रामेटिकली कर सकते हैं।

इस गाइड में हम पूरी प्रक्रिया को चरण‑दर‑चरण देखेंगे: Excel वर्कबुक को लोड करना जिसमें एक चार्ट और टेक्स्टबॉक्स है, निर्यात को इस तरह कॉन्फ़िगर करना कि टेक्स्टबॉक्स और शैप्स संपादन योग्य रहें, और अंत में परिणाम को **PowerPoint** फ़ाइल के रूप में सहेजना। अंत तक आप यह भी जान जाएंगे कि **Excel को PowerPoint में कैसे बदलें**, **Excel को PowerPoint के रूप में सहेजें**, और किन विकल्पों को किन किनारे‑केस पर ट्यून कर सकते हैं।

## आपको क्या चाहिए

- **Aspose.Cells for .NET** (संस्करण 23.10 या बाद का)। यह लाइब्रेरी परिवर्तन को आसान बनाती है।
- **.NET 6+** रनटाइम – कोई भी नवीनतम SDK चलेगा।
- एक साधारण Excel फ़ाइल (`ChartWithTextbox.xlsx`) जिसमें कम से कम एक चार्ट और एक टेक्स्टबॉक्स हो।
- Visual Studio या आपका पसंदीदा IDE।

Aspose.Cells के अलावा कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है, लेकिन C# की बुनियादी समझ मददगार होगी।

## PowerPoint में चार्ट निर्यात – चरण‑दर‑चरण

नीचे हम समाधान को छोटे‑छोटे, आसानी से समझ में आने वाले चरणों में बाँटते हैं। प्रत्येक चरण में आवश्यक कोड और एक छोटा “क्यों” पैराग्राफ शामिल है जो पीछे की तर्क को समझाता है।

### चरण 1: वह Excel वर्कबुक लोड करें जिसमें चार्ट है

सबसे पहले हमें स्रोत फ़ाइल को मेमोरी में लाना होगा। Aspose.Cells की `Workbook` क्लास पूरे स्प्रेडशीट को पढ़ती है, जिसमें चार्ट, इमेज और एम्बेडेड ऑब्जेक्ट्स शामिल होते हैं।

```csharp
using Aspose.Cells;

// Step 1: Load the Excel workbook that contains the chart with a textbox
Workbook workbook = new Workbook(@"C:\Samples\ChartWithTextbox.xlsx");

// Verify that the workbook actually contains a chart
if (workbook.Worksheets[0].Charts.Count == 0)
{
    throw new InvalidOperationException("No chart found in the first worksheet.");
}
```

*क्यों यह महत्वपूर्ण है:* यदि वर्कबुक को सही पाथ निर्दिष्ट किए बिना खोला जाता है, तो आपको `FileNotFoundException` मिलेगा। यह त्वरित जाँच बाद में खाली स्लाइड निर्यात होने से बचाती है।

### चरण 2: शैप्स को संपादन योग्य रखने के लिए प्रेजेंटेशन विकल्प तैयार करें

Aspose.Cells आपको यह तय करने देता है कि निर्यात के बाद टेक्स्टबॉक्स, शैप्स और यहाँ तक कि चार्ट स्वयं **संपादन योग्य** रहें या नहीं। `ExportTextBoxes` और `ExportShapes` को `true` सेट करने से ये ऑब्जेक्ट्स स्थिर इमेज की बजाय नेटिव PowerPoint एलिमेंट्स के रूप में रखे जाते हैं।

```csharp
using Aspose.Cells.Drawing;

// Step 2: Set up presentation options to keep textboxes and shapes editable in the output
PresentationOptions presentationOptions = new PresentationOptions
{
    ExportTextBoxes = true, // Preserve editable textboxes
    ExportShapes    = true  // Preserve shapes such as the chart itself
};
```

*क्यों यह महत्वपूर्ण है:* यदि आप इन फ़्लैग्स को डिफ़ॉल्ट (`false`) पर छोड़ देते हैं, तो परिणामी स्लाइड में चार्ट की एक बिटमैप इमेज होगी, जिसे बाद में सीरीज़ एडिट या कैप्शन बदलना असंभव होगा। दोनों विकल्पों को सक्षम करने से आपको एक वास्तविक PowerPoint चार्ट मिलेगा जो मैन्युअली बनाये गए चार्ट जैसा व्यवहार करता है।

### चरण 3: Excel को PowerPoint में बदलें और फ़ाइल सहेजें

अब हम `Save` मेथड को कॉल करते हैं, जिसमें `SaveFormat.Pptx` एन्नम और हमने अभी कॉन्फ़िगर किए हुए विकल्प पास करते हैं। लाइब्रेरी Excel चार्ट ऑब्जेक्ट को PowerPoint चार्ट शैप में बदलने का काम करती है।

```csharp
// Step 3: Save the workbook as a PowerPoint presentation using the configured options
workbook.Save(@"C:\Samples\Result.pptx", SaveFormat.Pptx, presentationOptions);
```

*क्यों यह महत्वपूर्ण है:* `Save` कॉल सभी भारी काम संभालता है—Excel सीरीज़ को PowerPoint सीरीज़ में मैप करना, एक्सिस फॉर्मेटिंग को बरकरार रखना, और किसी भी लिंक्ड टेक्स्टबॉक्स को कॉपी करना। इस लाइन के चलने के बाद आपके पास एक पूरी‑तरह से संपादन योग्य `.pptx` फ़ाइल होगी, जिसे Microsoft PowerPoint में खोला जा सकता है।

### परिणाम की जाँच करें

`Result.pptx` को PowerPoint में खोलें। आपको एक स्लाइड दिखनी चाहिए जिसमें:

- मूल चार्ट अभी भी अपने डेटा से जुड़ा हुआ है (सीरीज़ एडिट करने के लिए डबल‑क्लिक करें)।
- Excel शीट में मौजूद कोई भी टेक्स्टबॉक्स अब एक नेटिव PowerPoint टेक्स्ट बॉक्स के रूप में है।
- स्लाइड लेआउट स्वचालित रूप से चुना गया है (आमतौर पर ब्लैंक स्लाइड)।

यदि कोई तत्व गायब दिखे, तो दोबारा जाँचें कि स्रोत वर्कबुक में वास्तव में दृश्य ऑब्जेक्ट्स थे और `ExportTextBoxes` / `ExportShapes` को `true` सेट किया गया था।

### Excel को PowerPoint में बदलना: कई वर्कशीट्स को संभालना

अक्सर एक वर्कबुक में एक से अधिक शीट होती हैं, प्रत्येक में अपना चार्ट होता है। डिफ़ॉल्ट रूप से Aspose.Cells सभी वर्कशीट्स के **सभी** चार्ट्स को अलग‑अलग स्लाइड्स में निर्यात करता है। यदि आपको केवल कुछ ही चाहिए, तो आप सेव करने से पहले उन्हें फ़िल्टर कर सकते हैं:

```csharp
// Example: Export only charts from the first worksheet
Worksheet firstSheet = workbook.Worksheets[0];
foreach (Chart chart in firstSheet.Charts)
{
    chart.IsVisible = true; // Ensure visibility
}

// Hide charts from other sheets
for (int i = 1; i < workbook.Worksheets.Count; i++)
{
    foreach (Chart chart in workbook.Worksheets[i].Charts)
    {
        chart.IsVisible = false;
    }
}
```

*प्रो टिप:* `chart.IsVisible = false` सेट करना, चार्ट को पूरी तरह हटाने से सस्ता पड़ता है, और यह आपको स्रोत फ़ाइल को बदले बिना शामिल/बहिष्कृत करने की सुविधा देता है।

### Excel को PowerPoint के रूप में सहेजें – स्लाइड आकार को कस्टमाइज़ करना

PowerPoint डिफ़ॉल्ट रूप से 10‑इंच बाय 5.63‑इंच स्लाइड देता है। यदि आपका चार्ट भीड़भाड़ जैसा दिख रहा है, तो आप `PresentationOptions` ऑब्जेक्ट के माध्यम से स्लाइड के आयाम बदल सकते हैं:

```csharp
presentationOptions.SlideSize = new SizeF(13.33f, 7.5f); // 16:9 widescreen
```

अब निर्यात किया गया चार्ट अधिक जगह रखेगा, और सभी टेक्स्टबॉक्स अपनी मूल लेआउट को बरकरार रखेंगे।

### Excel को PPT में बदलना: छिपे हुए ऑब्जेक्ट्स को संभालना

छिपी हुई पंक्तियाँ, कॉलम या शैप्स कभी‑कभी निर्यात में शामिल हो जाते हैं। उन्हें हटाने के लिए, सहेजने से पहले एक त्वरित क्लीन‑अप चलाएँ:

```csharp
// Remove hidden rows/columns that might affect chart layout
foreach (Worksheet sheet in workbook.Worksheets)
{
    sheet.Cells.HideRows = false;
    sheet.Cells.HideColumns = false;
}
```

यह चरण हमेशा आवश्यक नहीं होता, लेकिन यह आपके अंतिम स्लाइड डेक में अप्रत्याशित गैप्स को रोकता है।

### वर्कबुक को PPTX के रूप में सहेजें – पूर्ण कार्यशील उदाहरण

सब कुछ मिलाकर, यहाँ एक तैयार‑चलाने‑योग्य कंसोल प्रोग्राम है जो पूरे प्रवाह को दर्शाता है:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing; // For SizeF

class ExportChartDemo
{
    static void Main()
    {
        // Load workbook (Step 1)
        string sourcePath = @"C:\Samples\ChartWithTextbox.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // Verify chart existence
        if (workbook.Worksheets[0].Charts.Count == 0)
        {
            Console.WriteLine("No chart found. Exiting.");
            return;
        }

        // Configure presentation options (Step 2)
        PresentationOptions options = new PresentationOptions
        {
            ExportTextBoxes = true,
            ExportShapes    = true,
            SlideSize       = new SizeF(13.33f, 7.5f) // optional widescreen
        };

        // Optional: export only first worksheet charts
        for (int i = 1; i < workbook.Worksheets.Count; i++)
        {
            foreach (Chart c in workbook.Worksheets[i].Charts)
                c.IsVisible = false;
        }

        // Save as PowerPoint (Step 3)
        string targetPath = @"C:\Samples\Result.pptx";
        workbook.Save(targetPath, SaveFormat.Pptx, options);

        Console.WriteLine($"Export complete! File saved to {targetPath}");
    }
}
```

इस प्रोग्राम को चलाने से `Result.pptx` बन जाएगा, जिसमें एक संपादन योग्य चार्ट और टेक्स्टबॉक्स होगा—बिल्कुल वही जो आप **वर्कबुक को pptx के रूप में सहेजते** समय अपेक्षा करेंगे।

![PowerPoint में चार्ट निर्यात करने का उदाहरण](/images/export-chart-to-powerpoint.png "PowerPoint में चार्ट निर्यात – संपादन योग्य स्लाइड")

## सामान्य प्रश्न एवं किनारे‑केस

**यदि Excel फ़ाइल में बाहरी डेटा स्रोत से जुड़ा चार्ट हो तो क्या होगा?**  
Aspose.Cells वर्तमान डेटा मानों को PowerPoint चार्ट में कॉपी करता है। यह **बाहरी लिंक** को बरकरार नहीं रखता, क्योंकि PowerPoint उसी तरह Excel डेटा कनेक्शन को संदर्भित नहीं कर सकता। यदि आपको लाइव अपडेट चाहिए, तो PPTX में मूल Excel फ़ाइल को OLE ऑब्जेक्ट के रूप में एम्बेड करने पर विचार करें।

**क्या मैं कस्टम थीम वाला चार्ट निर्यात कर सकता हूँ?**  
हां। लाइब्रेरी Excel थीम रंगों को PowerPoint थीम स्लॉट्स में मैप करने की कोशिश करती है। अत्यधिक कस्टम पैलेट के लिए आपको निर्यात के बाद PowerPoint के अपने API (जैसे Aspose.Slides) से रंग समायोजित करने पड़ सकते हैं।

**चार्ट की संख्या पर कोई सीमा है?**  
व्यावहारिक रूप से नहीं—Aspose.Cells डेटा को स्ट्रीम करता है, इसलिए दर्जनों चार्ट वाले वर्कबुक भी निर्यात हो सकते हैं, हालांकि परिणामी PPTX का आकार रैखिक रूप से बढ़ेगा।

**क्या Aspose.Cells के लिए लाइसेंस चाहिए?**  
एक मुफ्त इवैल्यूएशन चलती है, लेकिन यह पहली स्लाइड पर वॉटरमार्क जोड़ती है। प्रोडक्शन उपयोग के लिए उचित लाइसेंस प्राप्त करें ताकि वॉटरमार्क हटे और पूरी परफ़ॉर्मेंस अनलॉक हो।

## सारांश

हमने C# का उपयोग करके **चार्ट को PowerPoint में निर्यात** करने की पूरी प्रक्रिया को कवर किया, Excel वर्कबुक को लोड करने, `PresentationOptions` को इस तरह कॉन्फ़िगर करने कि टेक्स्टबॉक्स और शैप्स संपादन योग्य रहें, और अंत में परिणाम को `.pptx` के रूप में सहेजने का सटीक कोड दिखाया। साथ ही आप अब **Excel को PowerPoint में कैसे बदलें**, **Excel को PowerPoint के रूप में सहेजें**, और “**Excel को ppt में कैसे बदलें**” प्रश्न का उत्तर एक पूर्ण, चलाने योग्य उदाहरण के साथ दे सकते हैं।

## आगे क्या?

- **वर्कबुक को PPTX के रूप में सहेजें** कई स्लाइड्स के साथ: प्रत्येक वर्कशीट पर लूप चलाएँ और प्रत्येक के लिए `PresentationOptions` के साथ `Save` कॉल करें।
- यदि आपको उत्पन्न PPTX को आगे प्रोग्रामेटिकली संशोधित करने की जरूरत है (जैसे ट्रांज़िशन, स्पीकर नोट्स आदि), तो **Aspose.Slides** का अन्वेषण करें।
- **पिवट चार्ट** या **3‑D चार्ट** निर्यात करने की कोशिश करें—विकल्प समान रहते हैं, लेकिन एक्सिस फॉर्मेटिंग को बाद में थोड़ा ट्यून करना पड़ सकता है।

यदि आपको कोई समस्या आती है, तो नीचे टिप्पणी छोड़ें या नवीनतम API बदलावों के लिए आधिकारिक Aspose.Cells दस्तावेज़ देखें। कोडिंग का आनंद लें, और कुछ ही पंक्तियों के C# कोड से अपने Excel चार्ट को परिष्कृत PowerPoint प्रस्तुतियों में बदलें!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}