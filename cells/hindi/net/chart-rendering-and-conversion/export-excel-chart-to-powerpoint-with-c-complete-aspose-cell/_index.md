---
category: general
date: 2026-08-04
description: Aspose.Cells का उपयोग करके C# में Excel चार्ट को PowerPoint में निर्यात
  करें। इस चरण‑दर‑चरण Excel से PowerPoint रूपांतरण गाइड का पालन करें और आकृतियों को
  संपादन योग्य रखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: hi
lastmod: 2026-08-04
og_description: Aspose.Cells के साथ C# में Excel चार्ट को PowerPoint में निर्यात करें।
  जानें कैसे एक संपादन योग्य PPTX बनाएं, चार्ट डेटा को संरक्षित रखें, और Excel से
  PowerPoint रूपांतरण को स्वचालित करें।
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: C# के साथ Excel चार्ट को PowerPoint में निर्यात करें – पूर्ण Aspose.Cells
  ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: C# के साथ Excel चार्ट को PowerPoint में निर्यात करें – पूर्ण Aspose.Cells गाइड
url: /hi/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel चार्ट को PowerPoint में C# के साथ निर्यात करें – पूर्ण Aspose.Cells गाइड

यदि आपको **Excel चार्ट को PowerPoint में निर्यात** करना है, तो यह ट्यूटोरियल आपको दिखाता है कि इसे Aspose.Cells और Aspose.Slides के साथ C# में कैसे किया जाए। आपको एक पूरी तरह से संपादन योग्य PPTX मिलेगा जो चार्ट डेटा और आकारों को संरक्षित रखता है, जिससे रूपांतरण आगे के डिज़ाइन कार्य के लिए तैयार हो जाता है।

Excel से PowerPoint में चार्ट निर्यात करना स्वचालित रिपोर्टिंग पाइपलाइन, बिक्री डेक या प्रशिक्षण सामग्री बनाते समय एक सामान्य आवश्यकता है। इस गाइड में आप **Excel से PowerPoint रूपांतरण** के सटीक चरण सीखेंगे जो सभी चार्ट तत्वों को संपादन योग्य रखता है। कोई मैन्युअल कॉपी‑पेस्ट आवश्यक नहीं है, और कोड .NET 6+ तथा क्लासिक .NET Framework दोनों के साथ काम करता है।

## आवश्यकताएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- एक वैध Aspose.Cells लाइसेंस (या एक मुफ्त मूल्यांकन कुंजी)  
- प्रोजेक्ट में Aspose.Slides for .NET जोड़ें (लाइब्रेरी PPTX आउटपुट संभालती है)  
- .NET 6 SDK या बाद का संस्करण स्थापित हो  
- एक Excel वर्कबुक जिसमें कम से कम एक चार्ट हो (इस उदाहरण के लिए हम `Shapes.xlsx` का उपयोग करते हैं)  

आप निम्नलिखित कमांड्स के साथ NuGet पैकेज इंस्टॉल कर सकते हैं:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## चरण 1: Excel वर्कबुक लोड करें

पहला कार्य वह वर्कबुक खोलना है जिसमें वह चार्ट हो जिसे आप निर्यात करना चाहते हैं। `Workbook` क्लास पूरे Excel फ़ाइल का प्रतिनिधित्व करता है।

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Why this matters:** वर्कबुक लोड करने से आपको उसकी वर्कशीट्स, चार्ट्स और फ़ॉर्मेटिंग तक पहुँच मिलती है। Aspose.Cells फ़ाइल को बिना Microsoft Office स्थापित किए पढ़ता है, जिससे समाधान हल्का और सर्वर‑फ़्रेंडली रहता है।

## चरण 2: वर्कशीट चुनें और प्रिंट एरिया निर्धारित करें

एक वर्कशीट में कई चार्ट हो सकते हैं, लेकिन आप आमतौर पर एक विशिष्ट क्षेत्र निर्यात करते हैं। `PrintArea` सेट करने से Aspose.Cells को पता चलता है कि कौन‑से सेल (चार्ट सहित) रेंडर किए जाएँ।

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Why this matters:** निर्यात को परिभाषित प्रिंट एरिया तक सीमित करके आप अनावश्यक खाली स्लाइड्स से बचते हैं और PPTX फ़ाइल का आकार छोटा रखते हैं। इस क्षेत्र को आपके चार्ट की सटीक रेंज के अनुसार समायोजित किया जा सकता है।

## चरण 3: संपादन योग्य PPTX के लिए निर्यात विकल्प कॉन्फ़िगर करें

Aspose.Cells `ImageOrPrintOptions` क्लास का उपयोग आउटपुट फ़ॉर्मेट और संपादन क्षमता को नियंत्रित करने के लिए करता है। `ImageFormat` को `ImageFormat.Pptx` सेट करने से PowerPoint फ़ाइल बनती है, जबकि `ExportEditableShapes = true` चार्ट ऑब्जेक्ट्स को संपादन योग्य आकारों के रूप में संरक्षित रखता है।

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Why this matters:** `ExportEditableShapes` फ़्लैग **PowerPoint में संपादन योग्य आकार** प्राप्त करने की कुंजी है। इसके बिना चार्ट एक इमेज के रूप में रास्टराइज़ हो जाएगा, जिससे बाद में डेटा पॉइंट्स या स्टाइलिंग को बदलना संभव नहीं रहेगा।

## चरण 4: वर्कशीट को PowerPoint प्रस्तुति के रूप में सहेजें

अंत में, `Workbook` ऑब्जेक्ट पर `Save` मेथड को कॉल करें। `SaveFormat.Pptx` एनेम Aspose.Cells को PowerPoint फ़ाइल बनाने के लिए निर्देश देता है।

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

जब कोड समाप्त हो जाए, तो `ShapesExport.pptx` को PowerPoint में खोलें। आपको एक स्लाइड दिखेगी जिसमें मूल Excel चार्ट एक मूल PowerPoint चार्ट ऑब्जेक्ट के रूप में मौजूद है। डेटा को संपादित करने, रंग बदलने या एनीमेशन जोड़ने के लिए चार्ट पर डबल‑क्लिक करें—जैसे आपने सीधे PowerPoint में चार्ट बनाया हो।

### अपेक्षित आउटपुट

| फ़ाइल नाम                | स्लाइड पर सामग्री                         |
|--------------------------|------------------------------------------|
| `ShapesExport.pptx`      | `Shapes.xlsx` से चार्ट को एक संपादन योग्य PowerPoint चार्ट के रूप में रेंडर किया गया, जिसमें अक्ष लेबल, लेजेंड और डेटा श्रृंखला बरकरार हैं। |

## पूर्ण, चलाने योग्य उदाहरण

नीचे पूरा प्रोग्राम दिया गया है जिसे आप कॉपी, पेस्ट और रन कर सकते हैं। इसमें सभी आवश्यक `using` स्टेटमेंट्स, एरर हैंडलिंग और कमेंट्स शामिल हैं।

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**प्रत्येक ब्लॉक की व्याख्या**

| ब्लॉक | उद्देश्य |
|-------|----------|
| `using` निर्देश | Aspose.Cells और Aspose.Slides नेमस्पेस को इम्पोर्ट करता है। |
| `Workbook workbook = new Workbook(excelPath);` | Office स्थापित किए बिना Excel फ़ाइल लोड करता है। |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | निर्यात को उस क्षेत्र तक सीमित करता है जिसमें चार्ट स्थित है। |
| `ImageOrPrintOptions` | PPTX आउटपुट कॉन्फ़िगर करता है और **Aspose.Cells PPTX export** को संपादन योग्य आकारों के साथ सक्षम करता है। |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | PowerPoint फ़ाइल को डिस्क पर लिखता है। |
| `try / catch` | फ़ाइल न मिलने या लाइसेंस समस्याओं के लिए बुनियादी एरर हैंडलिंग प्रदान करता है। |

इस प्रोग्राम को चलाने पर एक PowerPoint स्लाइड बनती है जिसे आप Microsoft PowerPoint, Google Slides (कन्वर्ज़न के बाद) या किसी भी संगत व्यूअर में खोल सकते हैं।

## सामान्य विविधताएँ और किनारे के मामले

### कई वर्कशीट्स निर्यात करना

यदि आपको प्रत्येक वर्कशीट के लिए एक स्लाइड चाहिए, तो `workbook.Worksheets` पर लूप करें और प्रत्येक इटरेशन के लिए एक अनोखा फ़ाइल नाम देकर `Save` कॉल करें।

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### स्लाइड लेआउट नियंत्रित करना

Aspose.Slides आपको निर्यात के बाद एक कस्टम स्लाइड लेआउट जोड़ने की अनुमति देता है। एक नई प्रस्तुति बनाएं, जेनरेटेड स्लाइड इम्पोर्ट करें, और फिर एक मास्टर थीम लागू करें।

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### बाहरी डेटा स्रोतों वाले चार्ट को संभालना

यदि कोई चार्ट परिभाषित प्रिंट एरिया के बाहर के डेटा रेंज को संदर्भित करता है, तो `PrintArea` को उन सेल्स को शामिल करने के लिए विस्तारित करें। अन्यथा निर्यात के दौरान चार्ट डेटा श्रृंखला खो सकता है।

### लाइसेंसिंग विचार

Aspose लाइब्रेरीज़ मूल्यांकन मोड में वॉटरमार्क के साथ काम करती हैं। वॉटरमार्क हटाने के लिए किसी भी API कॉल से पहले लाइसेंस सेट करें:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

यदि आप Aspose.Slides की उन्नत सुविधाओं का उपयोग करते हैं तो उसी तरह लाइसेंस सेट करें।

## प्रो टिप्स

- **Reuse export options:** एक ही `ImageOrPrintOptions` इंस्टेंस बनाकर उसे प्रत्येक वर्कशीट को असाइन करें, जिससे कोड DRY रहता है।  
- **Batch processing:** बड़े‑पैमाने पर रिपोर्टिंग के लिए इस निर्यात लॉजिक को बैकग्राउंड वर्कर या Azure Function के साथ मिलाकर ऑन‑डिमांड PPTX फ़ाइलें जनरेट करें।  
- **Performance:** यदि आपको केवल चार्ट इमेज चाहिए (संपादन योग्य नहीं), तो `ExportEditableShapes = false` सेट करें। इससे मेमोरी उपयोग कम होता है और रूपांतरण तेज़ होता है।  
- **Testing:** उत्पन्न PPTX को Windows और macOS दोनों PowerPoint इंस्टॉलेशन पर वेरिफ़ाई करें, क्योंकि कुछ रेंडरिंग क्विर्क्स प्लेटफ़ॉर्म के बीच अलग हो सकते हैं।

## निष्कर्ष

अब आपके पास C# का उपयोग करके **Excel चार्ट को PowerPoint में निर्यात** करने का एक पूर्ण, एंड‑टू‑एंड समाधान है। ट्यूटोरियल ने वर्कबुक लोड करना, प्रिंट एरिया चुनना, **Aspose.Cells PPTX export** को **PowerPoint में संपादन योग्य आकार** के साथ कॉन्फ़िगर करना, और परिणाम को पूरी तरह से संपादन योग्य PPTX फ़ाइल के रूप में सहेजना कवर किया है।  

अब आप अतिरिक्त **Excel से PowerPoint रूपांतरण** परिदृश्यों जैसे बैच एक्सपोर्ट, कस्टम स्लाइड लेआउट, या प्रक्रिया को वेब API में इंटीग्रेट करना एक्सप्लोर कर सकते हैं। विभिन्न चार्ट प्रकारों के साथ प्रयोग करें, इमेज जोड़ें, या कई वर्कशीट्स को एक ही प्रस्तुति में मिलाकर आउटपुट को अपने व्यावसायिक जरूरतों के अनुसार कस्टमाइज़ करें।

रिपोर्टिंग वर्कफ़्लो को ऑटोमेट करने के लिए तैयार हैं? स्रोत फ़ाइल बदलें, प्रिंट एरिया समायोजित करें, और कोड को अपने मौजूदा .NET सर्विसेज़ में इंटीग्रेट करें। Happy coding!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}