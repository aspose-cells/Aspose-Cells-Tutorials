---
category: general
date: 2026-02-09
description: C# में पिवट रेफ़रेंस रेंज बनाएं और पिवट टेबल की छवि निर्यात करें। Aspose.Cells
  का उपयोग करके Excel रेंज को PNG के रूप में सहेजना सीखें – तेज़, पूर्ण मार्गदर्शिका।
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: hi
og_description: C# में पिवट रेफ़रेंस रेंज बनाएं और पिवट टेबल की छवि को PNG में निर्यात
  करें। Excel रेंज को PNG के रूप में सहेजने के लिए पूर्ण चरण‑दर‑चरण गाइड।
og_title: पिवट रेफ़रेंस रेंज बनाएं – पिवट टेबल की छवि को PNG के रूप में निर्यात करें
tags:
- Aspose.Cells
- C#
- Excel
title: पिवट रेफ़रेंस रेंज बनाएं – पिवट टेबल छवि को PNG के रूप में निर्यात करें
url: /hi/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# पिवट रेफ़रेंस रेंज बनाएं – पिवट टेबल इमेज को PNG के रूप में एक्सपोर्ट करें

क्या आपको C# का उपयोग करके Excel वर्कबुक में **पिवट रेफ़रेंस रेंज** बनानी है? आप केवल कुछ लाइनों के कोड से **पिवट टेबल इमेज एक्सपोर्ट** कर सकते हैं और **Excel रेंज को PNG के रूप में सेव** कर सकते हैं। मेरे अनुभव में, लाइव पिवट को एक स्थैतिक इमेज में बदलना रिपोर्ट, ईमेल या डैशबोर्ड में एनालिटिक्स एम्बेड करने का एक सुविधाजनक तरीका है, बिना पूरे वर्कबुक को साथ लाए।

इस ट्यूटोरियल में हम वह सब कवर करेंगे जो आपको जानना आवश्यक है: आवश्यक लाइब्रेरीज़, सटीक कोड, प्रत्येक कॉल का महत्व, और कुछ संभावित समस्याएँ जिनका आप सामना कर सकते हैं। अंत तक आप किसी भी पिवट टेबल की PNG फ़ाइल आत्मविश्वास के साथ जेनरेट कर पाएँगे, और समझ पाएँगे कि इस पैटर्न को कई शीट्स या कस्टम इमेज फ़ॉर्मेट्स के लिए कैसे अनुकूलित किया जाए।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- **Aspose.Cells for .NET** (टेस्टिंग के लिए फ्री ट्रायल पर्याप्त है)।  
- **.NET 6.0** या बाद का संस्करण – हम जो API उपयोग कर रहे हैं वह .NET Standard 2.0+ के साथ पूरी तरह संगत है, इसलिए पुराने फ्रेमवर्क भी कंपाइल हो जाएंगे।  
- एक बेसिक C# प्रोजेक्ट (Console App, WinForms, या ASP.NET – कोई भी प्रोजेक्ट जो NuGet पैकेज रेफ़र कर सके)।  

यदि आपने अभी तक Aspose.Cells इंस्टॉल नहीं किया है, तो चलाएँ:

```bash
dotnet add package Aspose.Cells
```

बस इतना ही – कोई COM इंटरऑप नहीं, सर्वर पर Excel इंस्टॉल नहीं होना आवश्यक है।

## Step 1: Open the Workbook and Access the First Worksheet

सबसे पहले आपको वर्कबुक फ़ाइल लोड करनी है और वह वर्कशीट प्राप्त करनी है जिसमें पिवट टेबल मौजूद है। हम जानबूझकर **पहली वर्कशीट** (`Worksheets[0]`) चुनते हैं क्योंकि अधिकांश डेमो फ़ाइलें पिवट वहीं रखती हैं, लेकिन आप अपनी पसंद के अनुसार इंडेक्स को नाम से भी बदल सकते हैं।

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Why this matters:* `Worksheet` किसी भी रेंज‑आधारित ऑपरेशन का एंट्री पॉइंट है। यदि आप गलत शीट चुनते हैं, तो अगले `PivotTables[0]` कॉल से `IndexOutOfRangeException` फेंका जाएगा।

## Step 2: Create Pivot Reference Range

अब हम पिवट टेबल से **रेफ़रेंस रेंज** प्राप्त करने को कहते हैं। यह रेंज पिवट के सभी सेल्स—हेडर, डेटा रो और टोटल्स—को दर्शाती है। `CreateReferenceRange()` मेथड अंदरूनी तौर पर मर्ज्ड सेल्स और हिडन रो को संभालता है।

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **Pro tip:** यदि आपके वर्कबुक में कई पिवट हैं, तो `worksheet.PivotTables` को इटरेट करें और `Name` प्रॉपर्टी के आधार पर आवश्यक पिवट चुनें।

## Step 3: Render the Reference Range as an Image

Aspose.Cells किसी भी `Range` को इमेज में रेंडर कर सकता है। रिटर्न किया गया ऑब्जेक्ट रास्टर (PNG, JPEG) और वेक्टर (SVG) दोनों फ़ॉर्मेट को सपोर्ट करता है। यहाँ हम डिफ़ॉल्ट रास्टर इमेज ले रहे हैं, जो `System.Drawing.Image`‑कम्पैटिबल ऑब्जेक्ट है।

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*What’s happening under the hood?* API रेंज के विज़ुअल लेआउट का स्नैपशॉट लेती है, सेल स्टाइल्स, फ़ॉन्ट्स और कंडीशनल फ़ॉर्मेटिंग को सम्मानित करते हुए। यह मूल रूप से स्क्रीनशॉट लेने जैसा है, लेकिन प्रोग्रामेटिक रूप से और बिना UI के।

## Step 4: Save the Generated Image to a File

अंत में हम इमेज को फ़ाइल में सेव करते हैं। `Save` मेथड स्वचालित रूप से “.png” एक्सटेंशन मिलने पर PNG चुन लेता है। यदि आपको DPI कंट्रोल या कोई अन्य फ़ॉर्मेट चाहिए तो आप `SaveOptions` ऑब्जेक्ट भी पास कर सकते हैं।

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

इस लाइन के चलने के बाद, `pivot.png` खोलें और आप पिवट टेबल का पिक्सेल‑परफ़ेक्ट स्नैपशॉट देखेंगे, जिसे आप कहीं भी एम्बेड कर सकते हैं।

## Full Working Example

सब कुछ एक साथ रखने के लिए, यहाँ एक सेल्फ‑कंटेन्ड कंसोल प्रोग्राम है जिसे आप कॉपी‑पेस्ट करके चला सकते हैं:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Expected output:** `YOUR_DIRECTORY` में स्थित `pivot.png` नाम की फ़ाइल। इसे किसी भी इमेज व्यूअर में खोलें – आपको मूल पिवट का बिल्कुल वही लेआउट दिखेगा, जिसमें कॉलम हेडिंग्स, डेटा रो और ग्रैंड टोटल्स शामिल हैं।

## Export Pivot Table Image – Customizing Size and DPI

कभी‑कभी डिफ़ॉल्ट इमेज प्रेज़ेंटेशन स्लाइड के लिए बहुत छोटी होती है। आप `ImageOrVectorSaveOptions` ऑब्जेक्ट पास करके रिज़ॉल्यूशन नियंत्रित कर सकते हैं:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Why adjust DPI?* उच्च DPI से किनारे अधिक शार्प दिखते हैं, विशेषकर जब PNG को PowerPoint या PDF में स्केल किया जाता है।

## Save Excel Range as PNG – Handling Multiple Worksheets

यदि आपको कई शीट्स से पिवट एक्सपोर्ट करने हैं, तो `Workbook.Worksheets` पर लूप करें और ऊपर बताए गए स्टेप्स दोहराएँ। यहाँ एक संक्षिप्त स्निपेट है:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

यह पैटर्न **export pivot table image** को वर्कबुक के हर पिवट के लिए लागू करता है, और प्रत्येक फ़ाइल का नाम उसकी शीट और पिवट के अनुसार रखा जाता है – बैच प्रोसेसिंग के लिए एकदम उपयुक्त।

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| `IndexOutOfRangeException` on `PivotTables[0]` | वर्कशीट में कोई पिवट टेबल नहीं है। | एक्सेस करने से पहले `worksheet.PivotTables.Count` जांचें। |
| Blank image output | पिवट सभी रो को छिपा रहा है। | पिवट में विज़िबल डेटा सुनिश्चित करें, या रेंज बनाने से पहले `pivot.RefreshData();` कॉल करें। |
| Low‑resolution PNG | डिफ़ॉल्ट DPI 96 है। | ऊपर दिखाए अनुसार `ImageOrVectorSaveOptions.Resolution` का उपयोग करें। |
| File‑path errors | `YOUR_DIRECTORY` में अवैध कैरेक्टर हैं। | `Path.Combine` और `Path.GetInvalidPathChars()` का उपयोग करके पाथ को सैनिटाइज़ करें। |

## Verification – Quick Test

पूरा उदाहरण चलाने के बाद:

1. `pivot.png` को Windows Photo Viewer में खोलें।  
2. जाँचें कि कॉलम हेडर, डेटा रो और टोटल रो Excel व्यू से मेल खाते हैं।  
3. यदि कुछ रो गायब दिखें, तो दोबारा जांचें कि `CreateReferenceRange()` से पहले पिवट की **RefreshData** मेथड कॉल की गई थी।

## Bonus: Embedding the PNG into a Word Document

क्योंकि इमेज पहले से ही PNG है, आप इसे सीधे Aspose.Words में फीड कर सकते हैं:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

अब आपके पास एक Word रिपोर्ट है जिसमें पिवट का बिल्कुल वही स्नैपशॉट है – मैन्युअल कॉपी‑पेस्ट की कोई जरूरत नहीं।

## Conclusion

आपने अभी-अभी **create pivot reference range**, **export pivot table image**, और **save Excel range as png** को Aspose.Cells के साथ C# में उपयोग करना सीख लिया है। मुख्य बिंदु ये हैं:

- पिवट के विज़ुअल एरिया को अलग करने के लिए `PivotTable.CreateReferenceRange()` का उपयोग करें।  
- उस रेंज को इमेज में बदलने के लिए `Range.ToImage()` कॉल करें।  
- इमेज को PNG के रूप में सेव करें, प्रिंट क्वालिटी के लिए DPI को वैकल्पिक रूप से ट्यून करें।  

अब आप बैच एक्सपोर्ट, विभिन्न इमेज फ़ॉर्मेट (SVG, JPEG) या PNG को PDF/Word डॉक्यूमेंट में एम्बेड करने जैसी चीज़ों का अन्वेषण कर सकते हैं। पिवट को स्थैतिक ग्राफ़िक में कैप्चर करने के बाद संभावनाएँ अनंत हैं।

कोई सवाल या जटिल परिदृश्य है? नीचे कमेंट करें, और हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}