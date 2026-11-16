---
category: general
date: 2026-11-16
description: Excel को PowerPoint के रूप में सहेजना और प्रोग्रामेटिकली Excel को PowerPoint
  में बदलना सीखें। यह चरण‑दर‑चरण गाइड Excel को PPTX में निर्यात करने और वर्कबुक को
  PPTX के रूप में सहेजने को भी कवर करता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: hi
lastmod: 2026-11-16
og_description: Aspose.Cells का उपयोग करके Excel को PowerPoint के रूप में सहेजें।
  Excel को PowerPoint में बदलने, Excel को PPTX में निर्यात करने और मिनटों में वर्कबुक
  को PPTX के रूप में सहेजने के लिए इस गाइड का पालन करें।
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Excel को PowerPoint के रूप में सहेजें – पूर्ण C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: Aspose.Cells के साथ C# में Excel को PowerPoint के रूप में कैसे सहेजें
url: /hi/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells के साथ C# में Excel को PowerPoint के रूप में कैसे सहेजें

यदि आपको प्रोग्रामेटिकली **Excel को PowerPoint के रूप में सहेजना** है, तो यह ट्यूटोरियल आपको एक पूर्ण, तैयार‑चलाने योग्य समाधान देता है। चाहे आप एक रिपोर्टिंग इंजन बना रहे हों या एक स्वचालित स्लाइड जेनरेटर, नीचे दिए गए चरण आपको केवल कुछ कोड लाइनों में Excel वर्कशीट को एक संपादन योग्य PPTX स्लाइड में बदलने की अनुमति देते हैं।

आप सीखेंगे कि **Excel को PowerPoint में कैसे बदलें**, शीट को PPTX फ़ाइल में निर्यात करें, और टेक्स्ट बॉक्स व शैप्स को संपादन योग्य रखें – सब .NET वातावरण से बाहर निकले बिना।

## आवश्यकताएँ

* .NET 6.0 या बाद का (कोड .NET Framework 4.7.2+ के साथ भी काम करता है)
* एक वैध Aspose.Cells लाइसेंस (नि:शुल्क ट्रायल मूल्यांकन के लिए काम करता है)
* Visual Studio 2022 (या कोई भी C# IDE)
* एक Excel वर्कबुक जिसमें वह डेटा और शैप्स हों जिन्हें आप निर्यात करना चाहते हैं

## चरण 1: Aspose.Cells स्थापित करें

Add the Aspose.Cells NuGet package to your project:

```bash
dotnet add package Aspose.Cells
```

> **Pro tip:** `-v` फ़्लैग का उपयोग करके किसी विशिष्ट संस्करण को लक्षित करें, उदाहरण के लिए, `Aspose.Cells.24.5`।

## चरण 2: वह वर्कबुक लोड करें जिसे आप निर्यात करना चाहते हैं

The first operation in the **save Excel as PowerPoint** workflow is loading the source workbook.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Why this matters:* वर्कबुक लोड करने से आपको उसकी वर्कशीट्स, पेज सेटअप, और ड्राइंग ऑब्जेक्ट्स तक पहुँच मिलती है जो संपादन योग्य PowerPoint शैप्स बनेंगे।

## चरण 3: संपादन योग्य PPTX स्लाइड के लिए निर्यात विकल्प कॉन्फ़िगर करें

To **convert Excel to PowerPoint** while preserving editability, you must set a few properties on `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Explanation:*  
* `SaveFormat = SaveFormat.Pptx` Aspose.Cells को PowerPoint फ़ाइल बनाने के लिए बताता है।  
* `ExportEditableText` और `ExportEditableShapes` सुनिश्चित करते हैं कि परिणामी स्लाइड एक मूल PowerPoint स्लाइड की तरह व्यवहार करे—आप टेक्स्ट बॉक्स या शैप पर क्लिक करके सीधे PowerPoint में उसे संपादित कर सकते हैं।

## चरण 4: निर्यात क्षेत्र निर्धारित करें और उसे एकल स्लाइड में फिट करें

When you **export Excel to PPTX**, you usually want a specific range to appear on the slide. Setting the print area and fitting options guarantees a clean, single‑slide output.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Why this matters:* `PrintArea` निर्यात को सेल्स A1 से G30 तक सीमित करता है, जबकि `FitToPagesTall` और `FitToPagesWide` सब कुछ एक स्लाइड में संकुचित कर देते हैं, जिससे अनावश्यक अतिरिक्त पेज नहीं बनते।

## चरण 5: वर्कशीट को संपादन योग्य PPTX फ़ाइल के रूप में सहेजें

Now you can finally **save workbook as PPTX** and complete the **save Excel as PowerPoint** process.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

After running the program, open `EditableShapes.pptx` in Microsoft PowerPoint. You’ll see a slide that mirrors the selected Excel range, and all text boxes and shapes are fully editable.

### अपेक्षित आउटपुट

* `EditableShapes.pptx` नामक फ़ाइल `C:\Output\` में स्थित होगी।
* एक PowerPoint स्लाइड जिसमें रेंज A1:G30 शामिल होगा।
* टेक्स्ट बॉक्स, चार्ट, और शैप्स जिन्हें आप डबल‑क्लिक करके सीधे PowerPoint में संपादित कर सकते हैं।

## पूर्ण स्रोत कोड (कॉपी करने के लिए तैयार)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## सामान्य प्रश्न और किनारे‑के‑केस हैंडलिंग

| प्रश्न | उत्तर |
|----------|--------|
| **यदि मेरे पास कई वर्कशीट्स हैं तो क्या करें?** | `workbook.Worksheets` पर लूप चलाएँ और प्रत्येक शीट के लिए चरण 3‑5 दोहराएँ, आउटपुट फ़ाइल नाम बदलें (उदा., `Sheet1.pptx`, `Sheet2.pptx`)। |
| **क्या मैं पूरी वर्कबुक को एक ही PowerPoint डेक में निर्यात कर सकता हूँ?** | हाँ। `ImageOrPrintOptions` पर `ExportAllSheets = true` सेट करें। प्रत्येक वर्कशीट एक अलग स्लाइड बन जाएगी। |
| **मेरे शैप्स इमेज के रूप में दिख रहे हैं, संपादन योग्य ऑब्जेक्ट नहीं।** | सुनिश्चित करें कि `ExportEditableShapes = true` है और आप Aspose.Cells 24.5+ का उपयोग कर रहे हैं (पहले के संस्करणों में यह सुविधा नहीं है)। |
| **जनरेट किया गया PPTX बहुत बड़ा है।** | प्रिंट एरिया कम करें, या `exportOptions.ImageResolution` के माध्यम से इमेज रेज़ॉल्यूशन घटाएँ। |
| **प्रोडक्शन उपयोग के लिए क्या मुझे लाइसेंस चाहिए?** | एक पेड लाइसेंस इवैल्यूएशन वाटरमार्क हटाता है और पूरी परफ़ॉर्मेंस अनलॉक करता है। नि:शुल्क ट्रायल टेस्टिंग के लिए काम करता है। |

## विश्वसनीय प्रोडक्शन कोड के लिए टिप्स

* **Validate file paths** before calling `Workbook` or `Save` to avoid `FileNotFoundException`।  
* **Wrap the export in a try/catch** block to handle licensing errors (`Aspose.Cells.LicenseException`)।  
* **Dispose of the workbook** (`workbook.Dispose()`) when done to free unmanaged resources।  
* **Use async I/O** (`FileStream` with `await`) if you are exporting many large sheets in a web service।

## अगले कदम

Now that you know how to **save Excel as PowerPoint**, you can explore related topics:

* **Export Excel to PPTX with custom slide layouts** – adjust `SlideSize` and add a master slide।  
* **Convert Excel slide to PDF** – use `SaveFormat.Pdf` for a printable version।  
* **Batch convert a folder of workbooks** – combine the loop shown above with `Directory.GetFiles`।

विभिन्न प्रिंट एरिया, स्केलिंग विकल्प, और PowerPoint थीम्स के साथ प्रयोग करें ताकि आउटपुट को अपने संगठन की ब्रांडिंग के अनुसार ढाल सकें।

---

*Happy coding! If this guide helped you **convert Excel to PowerPoint**, feel free to share it with teammates or open an issue on the Aspose.Cells GitHub repository for further assistance.*

## अगला आप क्या सीखें?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [C# और Aspose.Cells का उपयोग करके Excel को PowerPoint के रूप में सहेजें](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Excel से PPTX सहेजें – Excel शीट को PowerPoint में निर्यात करने की पूर्ण गाइड](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Excel को PowerPoint में बदलें – पूर्ण चरण‑दर‑चरण गाइड](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}