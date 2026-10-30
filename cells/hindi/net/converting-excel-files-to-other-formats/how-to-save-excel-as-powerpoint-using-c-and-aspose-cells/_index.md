---
category: general
date: 2026-08-17
description: C# के साथ Excel को PowerPoint में सहेजें – XLSX फ़ाइलों को बदलने, टेक्स्टबॉक्स
  को संपादन योग्य बनाने, और PPTX आउटपुट उत्पन्न करने के लिए चरण‑दर‑चरण गाइड।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: hi
lastmod: 2026-08-17
og_description: C# में पूर्ण कोड उदाहरण के साथ Excel को PowerPoint के रूप में सहेजें।
  जानें कि XLSX को कैसे परिवर्तित करें, टेक्स्टबॉक्स को संपादन योग्य बनाएं, और PPTX
  में निर्यात करें।
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: C# में Excel को PowerPoint के रूप में सहेजें – पूर्ण रूपांतरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: C# और Aspose.Cells का उपयोग करके Excel को PowerPoint के रूप में कैसे सहेजें
url: /hi/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# और Aspose.Cells का उपयोग करके Excel को PowerPoint के रूप में सहेजना

यदि आपको .NET प्रोजेक्ट में **Excel को PowerPoint के रूप में सहेजना** है, तो यह गाइड आपको एक पूर्ण, तुरंत चलाने योग्य समाधान दिखाता है। आप देखेंगे कि कैसे XLSX वर्कबुक लोड करें, शीट पर प्रत्येक टेक्स्टबॉक्स को संपादन योग्य बनाएं, और परिणाम को PPTX फ़ाइल में निर्यात करें—सिर्फ कुछ ही C# लाइनों के साथ।

Excel को PowerPoint में बदलना रिपोर्टिंग डैशबोर्ड, स्लाइड डेक या स्वचालित प्रस्तुति निर्माण के लिए एक सामान्य आवश्यकता है। यह ट्यूटोरियल **टेक्स्टबॉक्स को प्रोग्रामेटिकली कैसे संपादित करें** को भी कवर करता है, ताकि आप सहेजने से पहले स्लाइड सामग्री को कस्टमाइज़ कर सकें।

## पूर्वापेक्षाएँ

* .NET 6.0 (या बाद का) SDK स्थापित हो  
* Visual Studio 2022 या VS Code जैसे विकास पर्यावरण  
* Aspose.Cells for .NET लाइसेंस (या मुफ्त मूल्यांकन कुंजी) – डाउनलोड करें [Aspose website](https://products.aspose.com/cells/net/)  
* वह `input.xlsx` फ़ाइल जिसे आप परिवर्तित करना चाहते हैं  

> **प्रो टिप:** यदि आप मुफ्त मूल्यांकन संस्करण का उपयोग करते हैं, तो आउटपुट PPTX में वॉटरमार्क होगा। लाइसेंस वाला संस्करण इसे हटा देता है।

## चरण 1: Aspose.Cells NuGet पैकेज स्थापित करें

अपने प्रोजेक्ट फ़ोल्डर में एक टर्मिनल खोलें और चलाएँ:

```bash
dotnet add package Aspose.Cells
```

## चरण 2: एक कंसोल एप्लिकेशन का ढांचा बनाएं

एक नया कंसोल प्रोजेक्ट बनाएं (यदि आपके पास पहले से नहीं है):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

जेनरेटेड `Program.cs` को अगले चरणों में दिखाए गए कोड से बदलें।

## चरण 3: वर्कबुक लोड करें और पहली वर्कशीट चुनें

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**यह क्यों महत्वपूर्ण है:**  
`Workbook` Excel फ़ाइल को मेमोरी में पढ़ता है, जबकि `Worksheet` आपको शीट की सेल्स, चार्ट और शैप्स तक पहुँच देता है। पहली वर्कशीट अक्सर वह डिफ़ॉल्ट रिपोर्ट होती है जिसे आप प्रस्तुत करना चाहते हैं।

## चरण 4: शीट पर प्रत्येक टेक्स्टबॉक्स को संपादन योग्य बनाएं

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**आपको यह क्यों चाहिए:**  
डिफ़ॉल्ट रूप से, Excel से आयात किए गए टेक्स्टबॉक्स PowerPoint में रेंडर होने पर केवल‑पढ़ने योग्य होते हैं। `IsEditable = true` सेट करने से आप (या बाद में PowerPoint उपयोगकर्ता) स्लाइड पर सीधे टेक्स्ट को संशोधित कर सकते हैं।

## चरण 5: वर्कबुक को PowerPoint प्रस्तुति के रूप में सहेजें

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**आंतरिक रूप से क्या होता है:**  
`Workbook.Save` `SaveFormat.Pptx` एनेम वैल्यू को पहचानता है और Excel शीट लेआउट—पंक्तियों, कॉलम, चार्ट और अब‑संपादन योग्य टेक्स्टबॉक्स—को PowerPoint स्लाइड ऑब्जेक्ट्स में परिवर्तित करता है।

## पूर्ण स्रोत कोड (चलाने योग्य)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### अपेक्षित आउटपुट

जब आप प्रोग्राम चलाते हैं (`dotnet run`), आपको यह दिखना चाहिए:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

`output.pptx` को Microsoft PowerPoint में खोलने पर एक स्लाइड दिखेगी जो मूल Excel शीट को प्रतिबिंबित करती है। सभी टेक्स्टबॉक्स को डबल‑क्लिक करके सीधे संपादित किया जा सकता है।

## सामान्य प्रश्न और किनारे के मामलों

| प्रश्न | उत्तर |
|----------|--------|
| **क्या मैं पहली वर्कशीट के बजाय किसी विशिष्ट वर्कशीट को परिवर्तित कर सकता हूँ?** | हां। `workbook.Worksheets[0]` को `workbook.Worksheets["SheetName"]` या अपनी आवश्यकतानुसार किसी भी इंडेक्स से बदलें। |
| **यदि वर्कबुक में कई शीट्स हों तो क्या करें?** | `workbook.Save` को प्रत्येक वर्कशीट के लिए एक बार कॉल करें, प्रत्येक के लिए अलग PPTX फ़ाइलनाम प्रदान करें, या Aspose.Slides के `Presentation` ऑब्जेक्ट्स का उपयोग करके उन्हें एक ही प्रस्तुति में संयोजित करें। |
| **क्या चार्ट्स संरक्षित रहेंगे?** | Aspose.Cells स्वचालित रूप से Excel चार्ट्स को PowerPoint चार्ट ऑब्जेक्ट्स में परिवर्तित करता है। अतिरिक्त कोड की आवश्यकता नहीं है। |
| **मैं स्लाइड का आकार कैसे बदलूँ?** | `workbook.Save` के बाद, आप उत्पन्न PPTX को Aspose.Slides से लोड कर सकते हैं और `Presentation.SlideSize` को समायोजित कर सकते हैं। |
| **यदि मुझे सहेजने से पहले टेक्स्टबॉक्स का टेक्स्ट संपादित करना हो तो क्या करें?** | लूप के भीतर `shapeItem.TextBox.Text` तक पहुँचें, इसे संशोधित करें, फिर `IsEditable = true` सेट करें। उदाहरण: `shapeItem.TextBox.Text = "New title";` |

## समस्या निवारण टिप्स

* **“ShapeType.TextBox” नहीं मिला** – सुनिश्चित करें कि आप Aspose.Cells संस्करण 25.11 या नया उपयोग कर रहे हैं; पुराने संस्करणों में `IsEditable` प्रॉपर्टी नहीं होती।  
* **फ़ाइल नहीं मिली त्रुटियाँ** – जाँचें कि `YOUR_DIRECTORY` एक पूर्ण पथ है या सापेक्ष पथ सही स्थान की ओर इशारा कर रहा है।  
* **लाइसेंस लागू नहीं हुआ** – वर्कबुक लोड करने से पहले `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` कॉल करें ताकि मूल्यांकन वॉटरमार्क हट जाए।

## निष्कर्ष

आप अब जानते हैं कि C# के साथ **Excel को PowerPoint के रूप में सहेजना** कैसे किया जाता है, XLSX वर्कबुक लोड करके, प्रत्येक टेक्स्टबॉक्स को संपादन योग्य बनाकर, और PPTX में निर्यात करके। यह विधि चार्ट्स, इमेजेज और सेल फ़ॉर्मेटिंग को स्वचालित रूप से संभालती है, जिससे आपको एक तैयार‑प्रस्तुति स्लाइड डेक मिल जाता है।

अब, **Aspose.Slides के साथ Excel को PowerPoint में कैसे बदलें**, **परिवर्तन के बाद टेक्स्टबॉक्स को प्रोग्रामेटिकली कैसे संपादित करें**, या **कई वर्कबुक्स को बैच‑प्रोसेस कैसे करें** जैसे संबंधित विषयों का अन्वेषण करें। ये सभी यहाँ कवर किए गए मूल चरणों पर आधारित हैं और आपके रिपोर्टिंग वर्कफ़्लो को और अधिक स्वचालित बना सकते हैं।

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का पता लगाने में मदद करेंगे।

- [Aspose.Cells for .NET का उपयोग करके Excel को PowerPoint में कैसे परिवर्तित करें: एक पूर्ण गाइड](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [C# में पिवट टेबल कैसे कॉपी करें – Excel को PPTX में परिवर्तित करें, रेंज कॉपी करें और टेक्स्टबॉक्स बनाएं](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Aspose.Cells .NET का उपयोग करके Excel फ़ाइलों को कई फ़ॉर्मैट में कैसे सहेजें (2023 गाइड)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}