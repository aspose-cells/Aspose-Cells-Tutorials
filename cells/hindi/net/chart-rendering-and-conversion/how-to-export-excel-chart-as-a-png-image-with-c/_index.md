---
category: general
date: 2026-11-19
description: Aspose.Cells का उपयोग करके Excel चार्ट को PNG इमेज के रूप में निर्यात
  कैसे करें। कुछ ही चरणों में Excel चार्ट इमेज को सहेजना और इमेज फ़ॉर्मेट PNG सेट
  करना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: hi
lastmod: 2026-11-19
og_description: Aspose.Cells के साथ Excel चार्ट को PNG इमेज के रूप में कैसे एक्सपोर्ट
  करें। इस चरण‑दर‑चरण गाइड का पालन करके Excel चार्ट इमेज को सहेजें और इमेज फ़ॉर्मेट
  PNG को प्रभावी ढंग से सेट करें।
og_image_alt: How to export Excel chart as a PNG image
og_title: Excel चार्ट को PNG इमेज के रूप में निर्यात कैसे करें – तेज़ C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: C# के साथ Excel चार्ट को PNG इमेज के रूप में कैसे एक्सपोर्ट करें
url: /hi/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel चार्ट को PNG इमेज के रूप में C# के साथ एक्सपोर्ट कैसे करें

यदि आपको **how to export Excel chart** को एक पोर्टेबल इमेज में बदलने की आवश्यकता है, तो यह गाइड एक पूर्ण, तैयार‑चलाने योग्य समाधान दिखाता है। Aspose.Cells का उपयोग करके आप केवल तीन पंक्तियों के कोड से **save Excel chart image** को PNG फ़ॉर्मेट में सहेज सकते हैं, और ट्यूटोरियल यह भी समझाता है कि कैसे **set image format png** और **save Excel picture file** को सुरक्षित रूप से किया जाए।

आप इस लेख को एक runnable प्रोग्राम के साथ समाप्त करेंगे जो एक workbook लोड करता है, पहला chart रेंडर करता है, और डिस्क पर `pivot.png` फ़ाइल लिखता है। कोई अतिरिक्त टूल नहीं, कोई मैन्युअल कॉपी‑पेस्ट नहीं—सिर्फ साफ़ C# कोड जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं।

## आवश्यकताएँ

* .NET 6.0 SDK या बाद का (कोड .NET Framework 4.6+ के साथ भी काम करता है)
* Visual Studio 2022 या कोई भी C# एडिटर
* Aspose.Cells for .NET लाइसेंस (या एक अस्थायी इवैल्यूएशन की)
* एक Excel फ़ाइल (`pivot.xlsx`) जिसमें पहले worksheet पर कम से कम एक chart हो

ये आइटम केवल बाहरी निर्भरताएँ हैं; ट्यूटोरियल को मशीन पर Office स्थापित होने की आवश्यकता नहीं है।

## चरण 1: Aspose.Cells स्थापित करें

अपने प्रोजेक्ट फ़ोल्डर में एक टर्मिनल खोलें और चलाएँ:

```bash
dotnet add package Aspose.Cells
```

यह पैकेज `Aspose.Cells` नेमस्पेस जोड़ता है, जो `Workbook`, `ImageOrPrintOptions`, और अन्य क्लासेज़ प्रदान करता है जो **save Excel chart image** के लिए आवश्यक हैं।

## चरण 2: एक न्यूनतम कंसोल प्रोग्राम बनाएं

एक नया कंसोल ऐप बनाएं (`dotnet new console -n ExportChartDemo`) और ऑटो‑जेनरेटेड `Program.cs` को नीचे दिए गए कोड से बदलें। यह प्रोग्राम **how to export Excel chart** को दर्शाता है और प्रत्येक निर्णय को समझाने वाले कमेंट्स शामिल करता है।

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### प्रत्येक भाग क्यों महत्वपूर्ण है

* **Loading the workbook** – `Workbook` `.xlsx` फ़ाइल को पार्स करता है बिना Microsoft Excel स्थापित किए।
* **ImageOrPrintOptions** – यह ऑब्जेक्ट आउटपुट फ़ॉर्मेट को नियंत्रित करता है। `ImageFormat = ImageFormat.Png` सेट करने से **sets image format png** होता है, जो लॉसलैस और व्यापक रूप से समर्थित है।
* **RenderToImage** – `RenderToImage` मेथड chart (एक `Picture` ऑब्जेक्ट) को इमेज फ़ाइल में बदलता है। यह मेथड स्वचालित रूप से स्केलिंग, DPI, और ट्रांसपैरेंसी को भी संभालता है।
* **Error handling** – `sheet.Pictures.Count == 0` की जाँच रनटाइम एक्सेप्शन को रोकती है यदि worksheet में कोई chart नहीं है, जो उपयोगकर्ताओं के गलत शीट चुनने पर आम है।

## चरण 3: प्रोग्राम चलाएँ और परिणाम सत्यापित करें

1. प्रोजेक्ट बनाएं: `dotnet build`।
2. इसे चलाएँ: `dotnet run --project ExportChartDemo`।

यदि सब कुछ सही ढंग से कॉन्फ़िगर किया गया है, तो आप देखेंगे:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

`pivot.png` को किसी भी इमेज व्यूअर से खोलें। आपको Excel chart का सटीक दृश्य प्रतिनिधित्व दिखेगा, जो पुष्टि करता है कि आपने सफलतापूर्वक **saved Excel picture file** किया है।

### अपेक्षित आउटपुट

![PNG इमेज के रूप में सहेजा गया एक्सेल चार्ट](images/exported-chart.png){: .center alt="Excel चार्ट को PNG इमेज के रूप में कैसे एक्सपोर्ट करें"}

## चरण 4: उन्नत विकल्प – कई चार्ट एक्सपोर्ट करना

यदि आपके workbook में एक से अधिक chart हैं, तो आप `Pictures` कलेक्शन पर लूप कर सकते हैं:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

यह पैटर्न आपको शीट पर प्रत्येक chart के लिए **save Excel chart image** करने देता है, जो रिपोर्टिंग पाइपलाइन के लिए उपयोगी है।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| `ArgumentOutOfRangeException` on `Pictures[0]` | वर्कशीट में कोई chart नहीं है या chart किसी अलग शीट पर है। | शीट इंडेक्स (`Worksheets[0]`) की जाँच करें और सुनिश्चित करें कि chart मौजूद है। आवश्यकता होने पर `Worksheets["SheetName"]` का उपयोग करें। |
| Exported image is blurry | DPI बहुत कम सेट है (डिफ़ॉल्ट 96)। | `ImageOrPrintOptions` में `HorizontalResolution` और `VerticalResolution` बढ़ाएँ। |
| PNG फ़ाइल खाली या भ्रष्ट है | लाइसेंस न होने के कारण इवैल्यूएशन प्रतिबंध लगते हैं। | वर्कबुक लोड करने से पहले एक वैध Aspose.Cells लाइसेंस लागू करें (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| फ़ाइल पाथ त्रुटियाँ (`FileNotFoundException`) | `YOUR_DIRECTORY` प्लेसहोल्डर गलत है। | एब्सोल्यूट पाथ्स का उपयोग करें या `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")`। |

इन समस्याओं को हल करने से एक सुगम **save excel picture file** अनुभव सुनिश्चित होता है।

## प्रो टिप: सीधे मेमोरी स्ट्रीम में एक्सपोर्ट करें

कभी‑कभी आपको इमेज मेमोरी में चाहिए (जैसे वेब API पर अपलोड करने के लिए) डिस्क पर लिखने के बजाय:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

इसी **set image format png** लॉजिक को लागू किया जाता है; आपको केवल फ़ाइल पाथ को स्ट्रीम से बदलना है।

## निष्कर्ष

अब आप Aspose.Cells for .NET का उपयोग करके Excel chart को PNG फ़ाइल के रूप में **how to export Excel chart** जानते हैं। ट्यूटोरियल ने निम्नलिखित कवर किया:

* लाइब्रेरी स्थापित करना
* workbook लोड करना
* **Setting image format png**
* **Saving Excel chart image** को डिस्क पर सहेजना
* कई charts और सामान्य त्रुटियों को संभालना

इस बुनियाद के साथ आप chart एक्सपोर्ट को ऑटोमेटेड रिपोर्टिंग, वेब सर्विसेज, या डेस्कटॉप यूटिलिटीज़ में एकीकृत कर सकते हैं। अगला, संबंधित विषयों का अन्वेषण करें जैसे **save excel picture file** को JPEG (`ImageFormat.Jpeg`) के रूप में या printable रिपोर्ट्स के लिए charts को PDF में बदलना।

कोडिंग का आनंद लें!

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर करने में मदद करती हैं।

- [Aspose.Cells .NET का उपयोग करके Excel पाई चार्ट को इमेज में बदलें: चरण‑दर‑चरण गाइड](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [चार्ट को PNG के रूप में एक्सपोर्ट करें – Aspose.Cells के साथ Excel को HTML में बदलने का पूर्ण गाइड](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Aspose.Cells .NET का उपयोग करके Excel सेल्स को इमेज में एक्सपोर्ट करें: चरण‑दर‑चरण गाइड](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}