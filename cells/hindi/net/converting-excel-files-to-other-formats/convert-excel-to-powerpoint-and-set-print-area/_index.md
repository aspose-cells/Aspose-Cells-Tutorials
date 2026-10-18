---
category: general
date: 2026-10-10
description: Aspose.Cells के साथ C# में Excel को PowerPoint में बदलें और प्रिंट एरिया
  सेट करें – जानें कैसे Excel को एक्सपोर्ट करें, प्रिंट एरिया सेट करें, और PPTX फ़ाइल
  जनरेट करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: hi
lastmod: 2026-10-10
og_description: Aspose.Cells के साथ Excel को PowerPoint में बदलें। यह ट्यूटोरियल दिखाता
  है कि प्रिंट एरिया कैसे सेट करें, Excel को एक्सपोर्ट करें, और C# में PPTX फ़ाइल
  कैसे बनाएं।
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Excel को PowerPoint में बदलें – C# डेवलपर्स के लिए पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: एक्सेल को पॉवरपॉइंट में बदलें और प्रिंट एरिया सेट करें
url: /hi/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को PowerPoint में परिवर्तित करें और प्रिंट एरिया सेट करें

यदि आपको **Excel को PowerPoint में परिवर्तित करना** है, तो यह गाइड आपको C# में इसे कैसे करना है, बिल्कुल दिखाता है। पहले प्रिंट एरिया निर्धारित करके, आप नियंत्रित करते हैं कि प्रत्येक स्लाइड पर कौन‑से सेल दिखेंगे, और अंतिम PPTX फ़ाइल आपके लेआउट अपेक्षाओं से मेल खाती है। यह समाधान “how to export Excel” और “how to set print area” दोनों प्रश्नों का उत्तर उसी कोड बेस का उपयोग करके देता है।

इस ट्यूटोरियल में आप करेंगे:

* एक मौजूदा वर्कबुक लोड करें।
* एक वर्कशीट के लिए प्रिंट एरिया सेट करें (**set print area excel** चरण)।
* PowerPoint आउटपुट के लिए कन्वर्ज़न विकल्प कॉन्फ़िगर करें।
* एक ही मेथड कॉल में **convert excel to pptx** फ़ाइल उत्पन्न करें।

सभी आवश्यक कोड शामिल हैं, इसलिए आप इसे तुरंत कॉपी, पेस्ट और चलाकर उपयोग कर सकते हैं।

## पूर्वापेक्षाएँ

शुरू करने से पहले, सुनिश्चित करें कि आपके पास है:

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6.0 or later** | यह उदाहरण .NET 6+ को लक्षित करता है, लेकिन कोई भी .NET संस्करण जो C# 10 का समर्थन करता है, काम करेगा। |
| **Aspose.Cells for .NET** | यह लाइब्रेरी `Workbook`, `ImageOrPrintOptions`, और `ConvertToPdf` (PPTX के लिए उपयोग किया जाता है) मेथड प्रदान करती है। इसे NuGet के माध्यम से इंस्टॉल करें: `dotnet add package Aspose.Cells` |
| **An input Excel file** | ट्यूटोरियल `input.xlsx` फ़ाइल का उपयोग करता है। इसे ऐसे फ़ोल्डर में रखें जिसे आप कोड से रेफ़र कर सकें। |
| **Write permission to the output folder** | प्रोग्राम `output.pptx` लिखता है। सुनिश्चित करें कि डायरेक्टरी मौजूद है और लिखने योग्य है। |

> **Pro tip:** यदि आप कई वर्कशीट्स के साथ काम कर रहे हैं, तो कन्वर्ज़न से पहले प्रत्येक शीट के लिए प्रिंट‑एरिया चरण को दोहराएँ।

## चरण 1: एक नया C# कंसोल प्रोजेक्ट बनाएं

एक टर्मिनल या PowerShell विंडो खोलें और चलाएँ:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

यह **ExcelToPowerPointDemo** नाम का नया प्रोजेक्ट बनाता है और Aspose.Cells पैकेज जोड़ता है, जो अन्य फ़ॉर्मैट्स में **how to export Excel** करने के लिए मुख्य निर्भरता है।

## चरण 2: कन्वर्ज़न कोड लिखें

`Program.cs` की सामग्री को नीचे दिए गए पूर्ण उदाहरण से बदलें। यह कोड **convert excel to powerpoint** को दर्शाता है, **how to set print area** दिखाता है, और एक **convert excel to pptx** फ़ाइल उत्पन्न करता है।

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### प्रत्येक भाग क्यों महत्वपूर्ण है

* **Loading the workbook** – यह किसी भी **how to export Excel** परिदृश्य में पहला कदम है। `Workbook` फ़ाइल को मेमोरी में पढ़ता है, जिससे आपको शीट्स, सेल्स और फ़ॉर्मैटिंग तक पूरी पहुँच मिलती है।
* **Setting the print area** – `PageSetup.PrintArea` असाइन करके, आप Aspose.Cells को बताते हैं कि कौन‑से सेल रेंडर करने हैं। यह **set print area excel** का मूल है; इसके बिना पूरी शीट एक्सपोर्ट हो जाएगी, जिससे बड़े और अपठनीय स्लाइड्स बन सकते हैं।
* **Choosing `SaveFormat.Pptx`** – `ImageOrPrintOptions` ऑब्जेक्ट आपको आउटपुट फ़ॉर्मैट बदलने देता है। `SaveFormat` को `Pptx` सेट करने से **convert excel to pptx** पाइपलाइन ट्रिगर होती है।
* **Calling `ConvertToPdf`** – मेथड नाम के बावजूद, जब `SaveFormat` `Pptx` होता है तो लाइब्रेरी PowerPoint फ़ाइल आउटपुट करती है। यह एक ही कॉल में **convert excel to powerpoint** करने का अनुशंसित तरीका है।

## चरण 3: प्रोग्राम चलाएँ

प्रोजेक्ट फ़ोल्डर से निष्पादित करें:

```bash
dotnet run
```

यदि सब कुछ सही ढंग से कॉन्फ़िगर किया गया है, तो आपको कंसोल आउटपुट समान दिखेगा:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

`output.pptx` को Microsoft PowerPoint या किसी भी संगत व्यूअर में खोलें। प्रत्येक स्लाइड वर्कशीट के प्रिंटेड पेज के अनुरूप है, जो आपने परिभाषित रेंज तक सीमित है।

## एकाधिक वर्कशीट्स को संभालना

यदि आपका वर्कबुक एक से अधिक शीट रखता है और आप प्रत्येक शीट को अलग स्लाइड डेक में चाहते हैं, तो संग्रह के माध्यम से लूप करें:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

यह पैटर्न **how to export Excel** डेटा को शीट‑बाय‑शीट दिखाता है जबकि प्रत्येक के लिए **setting print area** अलग‑अलग किया जाता है।

## एज केस और सर्वोत्तम‑प्रैक्टिस टिप्स

| Situation | Recommended approach |
|-----------|----------------------|
| **Very large worksheets** | प्रिंट एरिया को कम करें या `HorizontalResolution`/`VerticalResolution` बढ़ाएँ ताकि PPTX आकार प्रबंधनीय रहे। |
| **Different page orientations** | कन्वर्ज़न से पहले `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` सेट करें। |
| **Custom slide size** | `conversionOptions.OnePagePerSheet = false;` का उपयोग करें और `conversionOptions.Width` / `conversionOptions.Height` को समायोजित करें। |
| **Missing input file** | लोडिंग कोड को `try { … } catch (FileNotFoundException)` ब्लॉक में रखें ताकि स्पष्ट त्रुटि संदेश प्रदान किया जा सके। |
| **Non‑ASCII characters** | सुनिश्चित करें कि वर्कबुक UTF‑8 एन्कोडिंग के साथ सहेजी गई है; Aspose.Cells स्वचालित रूप से Unicode को संभालता है। |

## संदर्भ के लिए पूर्ण स्रोत कोड

नीचे पूरा प्रोग्राम है, जिसमें `using` निर्देश और टिप्पणियाँ शामिल हैं। इसे **Step 1** में बनाए गए प्रोजेक्ट के अंदर `Program.cs` के रूप में सहेजें।

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## अपेक्षित आउटपुट

प्रोग्राम चलाने से एक PowerPoint फ़ाइल (`output.pptx`) बनती है जिसमें:

* वर्कशीट के प्रत्येक प्रिंटेड पेज के लिए एक स्लाइड।
* प्रत्येक स्लाइड पर केवल **A1:G30** के भीतर के सेल दिखाए जाते हैं।
* फ़ॉर्मैटिंग (फ़ॉन्ट, रंग, बॉर्डर) को Excel में जैसा है वैसा ही संरक्षित रखा जाता है।

फ़ाइल को PowerPoint में खोलें ताकि यह सत्यापित किया जा सके कि लेआउट परिभाषित प्रिंट एरिया से मेल खाता है।

## निष्कर्ष

अब आप Aspose.Cells का उपयोग करके C# में **Excel को PowerPoint में परिवर्तित करना** और सटीक रूप से **set print area excel** कैसे करना है, जानते हैं। ट्यूटोरियल ने **how to export Excel** को कवर किया, **how to set print area** दिखाया, और पूर्ण **convert excel to pptx** प्रदर्शित किया।

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स इस गाइड में प्रदर्शित तकनीकों पर आधारित निकटतम संबंधित विषयों को कवर करते हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों की खोज करने में मदद करती हैं।

- [Aspose.Cells for .NET का उपयोग करके Excel में प्रिंट एरिया कैसे सेट करें](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Excel में प्रिंट एरिया सेट करें और PowerPoint में एक्सपोर्ट करें – चरण‑दर‑चरण गाइड](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Excel में प्रिंट एरिया सेट करें – Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}