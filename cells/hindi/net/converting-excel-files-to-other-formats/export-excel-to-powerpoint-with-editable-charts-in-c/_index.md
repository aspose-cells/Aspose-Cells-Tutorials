---
category: general
date: 2026-09-21
description: Aspose.Cells का उपयोग करके Excel को PowerPoint में संपादन योग्य चार्ट्स
  के साथ निर्यात करें। इस चरण‑दर‑चरण गाइड का पालन करके वर्कशीट को PPTX में बदलें और
  चार्ट्स को संपादन योग्य रखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: hi
lastmod: 2026-09-21
og_description: Aspose.Cells का उपयोग करके Excel को PowerPoint में संपादन योग्य चार्ट्स
  के साथ निर्यात करें। जानें कि कैसे एक वर्कशीट को PPTX में बदलें और चार्ट्स की पूरी
  संपादन क्षमता को बनाए रखें।
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: संपादन योग्य चार्ट्स के साथ एक्सेल को पावरपॉइंट में निर्यात करें – C# ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: C# में संपादन योग्य चार्ट के साथ Excel को PowerPoint में निर्यात करें
url: /hi/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को PowerPoint में निर्यात करें संपादन योग्य चार्ट्स के साथ C# में

Excel को PowerPoint में संपादन योग्य चार्ट्स के साथ निर्यात करना एक सामान्य आवश्यकता है जब आपको प्रस्तुतियों में स्प्रेडशीट विज़ुअल्स को पुन: उपयोग करना हो। यह गाइड आपको दिखाता है कि **export Excel to PowerPoint** कैसे किया जाए जबकि चार्ट की संपादन क्षमता को संरक्षित रखा जाए, Aspose.Cells for .NET का उपयोग करके।

आप सीखेंगे:

* चार्ट्स और टेक्स्ट बॉक्सेस वाले मौजूदा वर्कबुक को लोड करना।  
* PPTX निर्यात विकल्पों को कॉन्फ़िगर करना ताकि चार्ट्स और शेप्स संपादन योग्य रहें।  
* एक विशिष्ट वर्कशीट को PowerPoint फ़ाइल में बदलना जिसे Microsoft PowerPoint में खोला और संपादित किया जा सके।

यह ट्यूटोरियल मानता है कि आपके पास बुनियादी C# ज्ञान और .NET (≥ .NET 6) का हालिया संस्करण है। Aspose.Cells का पूर्व अनुभव आवश्यक नहीं है।

---

## Excel को PowerPoint में निर्यात – अवलोकन

**export Excel to PowerPoint** के पीछे मुख्य विचार यह है कि प्रत्येक वर्कशीट को एक इमेज स्रोत के रूप में माना जाए जिसे PPTX स्लाइड में रेंडर किया जा सके। `ExportChartAsEditableText` और `ExportShapeAsEditableText` फ़्लैग्स को टॉगल करके, Aspose.Cells चार्ट डेटा को फ्लैट बिटमैप की बजाय PowerPoint ड्रॉइंग ऑब्जेक्ट्स के रूप में लिखता है। इससे प्राप्त स्लाइड पूरी तरह से संपादन योग्य बनती है—जैसे कि PowerPoint में सीधे बनाया गया चार्ट।

> **संपादन योग्य चार्ट्स क्यों उपयोग करें?**  
> संपादन योग्य चार्ट्स प्रस्तुतकर्ताओं को डेटा, रंग, या लेबल्स को मूल Excel फ़ाइल पर वापस जाए बिना समायोजित करने की अनुमति देते हैं, जिससे अंतिम‑क्षण के बदलाव तेज़ होते हैं और प्रस्तुति वर्कफ़्लो सुगम रहता है।

## Convert a worksheet to PowerPoint (worksheet to PowerPoint)

नीचे एक पूर्ण, चलाने योग्य उदाहरण है जो **worksheet to PowerPoint** रूपांतरण को दर्शाता है।

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### प्रत्येक चरण की व्याख्या

| चरण | कोड क्या करता है | क्यों यह **export excel chart pptx** के लिए महत्वपूर्ण है |
|------|-------------------|----------------------------------------------|
| 1️⃣   | `input.xlsx` को एक `Aspose.Cells.Workbook` ऑब्जेक्ट में लोड करता है। | वर्कबुक उन चार्ट्स तक पहुंच प्रदान करता है जिन्हें आप निर्यात करना चाहते हैं। |
| 2️⃣   | `ExportType` को `Pptx` पर सेट करता है और `ExportChartAsEditableText` एवं `ExportShapeAsEditableText` को सक्षम करता है। | ये फ़्लैग्स **editable charts pptx** के लिए मुख्य हैं – ये लाइब्रेरी को चार्ट ज्योमेट्री को रास्टर इमेजेज़ के बजाय PowerPoint ड्रॉइंग ऑब्जेक्ट्स के रूप में लिखने के लिए निर्देश देते हैं। |
| 3️⃣   | पहले वर्कशीट पर `ConvertToImage` को कॉल करता है, जिससे `Worksheet.pptx` बनता है। | यह मेथड **export excel to powerpoint** ऑपरेशन करता है और एक PPTX फ़ाइल लिखता है जिसे सीधे PowerPoint में खोला जा सकता है। |

> **Pro tip:** यदि आपको *कई* वर्कशीट्स निर्यात करनी हों, तो `workbook.Worksheets` पर लूप करें और प्रत्येक के लिए `ConvertToImage` को कॉल करें, वैकल्पिक रूप से आउटपुट फ़ाइलों का नाम `Sheet1.pptx`, `Sheet2.pptx` आदि रखें।

## PPTX में संपादन योग्य चार्ट्स सक्षम करें (export excel chart pptx)

जब `ExportChartAsEditableText` को `true` पर सेट किया जाता है, तो Aspose.Cells प्रत्येक चार्ट को PPTX XML के भीतर `<a:graphic>` तत्वों के संग्रह के रूप में लिखता है। PowerPoint तब इन तत्वों को मूल चार्ट ऑब्जेक्ट्स के रूप में मानता है, जिन्हें आप डबल‑क्लिक करके चार्ट एडिटर खोल सकते हैं।

**सामान्य कठिनाइयाँ**

* **Aspose.Cells लाइसेंस गायब** – लाइसेंस के बिना लाइब्रेरी आउटपुट में वॉटरमार्क जोड़ देती है। अपने प्रोग्राम में जल्दी लाइसेंस रजिस्टर करें (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`)।  
* **असमर्थित चार्ट प्रकार** – जबकि अधिकांश 2‑D चार्ट्स (कॉलम, लाइन, पाई) पूरी तरह से संपादन योग्य होते हैं, कुछ जटिल 3‑D या कॉम्बो चार्ट्स इमेजेज़ में बदल सकते हैं। यदि आप पूरी संपादन क्षमता पर निर्भर हैं तो अपने विशिष्ट चार्ट प्रकारों का परीक्षण करें।  
* **बड़े वर्कशीट्स** – बहुत बड़े वर्कशीट्स को निर्यात करने से काफी मेमोरी उपयोग हो सकता है। `ImageOrPrintOptions` में `ExportMaxRows` या `ExportMaxColumns` का उपयोग करके परिवर्तित क्षेत्र को सीमित करने पर विचार करें।

## चार्ट्स को संपादन योग्य रखने के टिप्स (editable charts pptx)

1. **चार्ट डेटा रेंज को संरक्षित रखें** – सुनिश्चित करें कि चार्ट डेटा स्रोत उसी वर्कशीट में हो जिसे आप निर्यात कर रहे हैं। क्रॉस‑शीट रेफ़रेंसेज़ PPTX में स्थिर मानों में बदल जाती हैं।  
2. **नवीनतम Aspose.Cells संस्करण का उपयोग करें** – नई रिलीज़ अतिरिक्त चार्ट सुविधाओं के समर्थन को सुधारती हैं और PPTX निर्यात से संबंधित किनारे‑केस बग्स को ठीक करती हैं।  
3. **आउटपुट को वैध करें** – परिवर्तन के बाद, उत्पन्न PPTX को PowerPoint में खोलें और सत्यापित करें कि आप चार्ट शीर्षक, श्रृंखला, और अक्ष लेबल्स को संपादित कर सकते हैं। यदि कोई तत्व इमेज के रूप में दिखे, तो दोबारा जांचें कि `ExportChartAsEditableText` सक्षम है और चार्ट प्रकार समर्थित है।  
4. **बैच प्रोसेसिंग** – ऑटोमेशन परिदृश्यों के लिए (जैसे कई Excel रिपोर्ट्स से स्लाइड डेक बनाना), परिवर्तन लॉजिक को एक मेथड में रैप करें जो `Workbook`, `int worksheetIndex`, और `string outputPath` को स्वीकार करता है। यह **export excel to powerpoint** वर्कफ़्लो को अलग करता है और पुन: उपयोग योग्य बनाता है।

## पूर्ण कार्यशील उदाहरण सारांश

सब कुछ एक साथ रखते हुए, यहाँ न्यूनतम प्रोग्राम है जिसे आप नई .NET कंसोल प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**Expected result**

* `Worksheet.pptx` नाम की फ़ाइल `YOUR_DIRECTORY` में दिखाई देती है।  
* Microsoft PowerPoint में फ़ाइल खोलने पर एक स्लाइड दिखती है जिसमें मूल चार्ट और सभी टेक्स्ट बॉक्सेस होते हैं।  
* चार्ट पर डबल‑क्लिक करने से PowerPoint का चार्ट एडिटर खुलता है, जिससे आप श्रृंखला मान, रंग, या अक्ष शीर्षक बदल सकते हैं—जिससे यह पुष्टि होती है कि **editable charts pptx** फीचर इच्छित रूप से काम कर रहा है।

## निष्कर्ष

अब आपके पास **export Excel to PowerPoint** के लिए एक पूर्ण समाधान है जो चार्ट्स को संपादन योग्य रखता है। `ImageOrPrintOptions` को `ExportChartAsEditableText` और `ExportShapeAsEditableText` के साथ कॉन्फ़िगर करके, रूपांतरण प्रक्रिया एक मूल PPTX फ़ाइल उत्पन्न करती है जहाँ चार्ट्स बिल्कुल वैसे ही व्यवहार करते हैं जैसे PowerPoint में सीधे बनाए गए हों।  

अब आप कर सकते हैं:

* कोड को कई वर्कशीट्स को संभालने के लिए विस्तारित करें (**worksheet to PowerPoint** प्रत्येक के लिए)।  
* निर्यात को अन्य Aspose.Cells सुविधाओं के साथ मिलाएँ, जैसे स्लाइड शीर्षक जोड़ना या इमेजेस सम्मिलित करना।  
* संबंधित विषयों का अन्वेषण करें जैसे **export Excel chart PPTX** कस्टम थीम्स के साथ या पूरे स्लाइड‑डेक जेनरेशन पाइपलाइन को ऑटोमेट करना।

विभिन्न चार्ट प्रकारों के साथ प्रयोग करने, डेटा लेबल्स जोड़ने, या इस वर्कफ़्लो को बड़े रिपोर्टिंग सिस्टम में एकीकृत करने में संकोच न करें। Happy coding!

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का पता लगाने में मदद करेंगे।

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}