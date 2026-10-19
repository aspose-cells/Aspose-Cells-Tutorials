---
category: general
date: 2026-09-24
description: Aspose.Cells का उपयोग करके C# में एक्सेल रेंज को इमेज के रूप में एक्सपोर्ट
  करें – वर्कशीट क्षेत्र को PNG या JPEG के रूप में सहेजने के लिए चरण‑दर‑चरण गाइड.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- Aspose.Cells export range
- C# Excel to PNG
- ImageOrPrintOptions usage
- export pivot table as image
language: hi
lastmod: 2026-09-24
og_description: Aspose.Cells के साथ C# में एक्सेल रेंज को इमेज के रूप में निर्यात
  करें। जानें कि कैसे किसी भी वर्कशीट क्षेत्र, जिसमें पिवट टेबल्स शामिल हैं, को मिनटों
  में PNG या JPEG में बदलें।
og_image_alt: Screenshot of a C# program exporting an Excel range to a PNG image
og_title: C# के साथ एक्सेल रेंज को इमेज के रूप में निर्यात करें – पूर्ण Aspose.Cells
  गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  headline: How to export excel range as image with C# and Aspose.Cells
  type: TechArticle
- description: Export excel range as image in C# using Aspose.Cells – step‑by‑step
    guide to save a worksheet area as PNG or JPEG.
  name: How to export excel range as image with C# and Aspose.Cells
  steps:
  - name: '**Load** the workbook from disk.'
    text: '**Load** the workbook from disk.'
  - name: '**Define** the cell area that will become the image (the *print area*).'
    text: '**Define** the cell area that will become the image (the *print area*).'
  - name: '**Export** the area using `ImageOrPrintOptions` and write the file.'
    text: '**Export** the area using `ImageOrPrintOptions` and write the file.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- Image export
title: C# और Aspose.Cells के साथ Excel रेंज को इमेज के रूप में निर्यात कैसे करें
url: /hi/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# और Aspose.Cells के साथ Excel रेंज को इमेज के रूप में एक्सपोर्ट कैसे करें

यदि आपको .NET एप्लिकेशन में **export excel range as image** करने की आवश्यकता है, तो यह गाइड आपको एक पूर्ण, तुरंत चलाने योग्य समाधान दिखाता है। चाहे आप डैशबोर्ड प्रकाशित कर रहे हों, वेब पेज में पिवट टेबल एम्बेड कर रहे हों, या रिपोर्ट थंबनेल बना रहे हों, आप केवल कुछ ही C# कोड लाइनों से किसी भी वर्कशीट क्षेत्र को PNG (या JPEG) में बदल सकते हैं।

इस ट्यूटोरियल में आप सीखेंगे कि कैसे:

* एक मौजूदा वर्कबुक लोड करें (`Workbook` class)  
* वह सटीक सेल रेंज निर्धारित करें जिसे आप कैप्चर करना चाहते हैं (`PrintArea`)  
* इमेज एक्सपोर्ट विकल्प कॉन्फ़िगर करें (`ImageOrPrintOptions`)  
* परिणामी चित्र को डिस्क पर सहेजें  

सभी आवश्यक पूर्वशर्तें, किनारे के मामलों, और सामान्य समस्याओं को कवर किया गया है ताकि आप कोड को अपने प्रोजेक्ट्स में बिना किसी आश्चर्य के अनुकूल बना सकें।

## पूर्वापेक्षाएँ

शुरू करने से पहले, सुनिश्चित करें कि आपके पास है:

| आवश्यकता | कारण |
|-------------|--------|
| **Aspose.Cells for .NET** (latest version) | उदाहरण में उपयोग किए गए `Workbook`, `Worksheet`, और `ImageOrPrintOptions` APIs प्रदान करता है। |
| **.NET 6.0 or later** | सैंपल .NET 6 को टार्गेट करता है, लेकिन कोई भी .NET Core/Framework संस्करण जो Aspose.Cells को सपोर्ट करता है, काम करेगा। |
| **A valid Excel file** (e.g., `input.xlsx`) | वह वर्कबुक जिसे आप कनवर्ट करना चाहते हैं। |
| **Write permission to the output folder** | `Save` को सफल होने के लिए आवश्यक है। |

आप NuGet के माध्यम से Aspose.Cells इंस्टॉल कर सकते हैं:

```bash
dotnet add package Aspose.Cells
```

## Excel रेंज को इमेज के रूप में एक्सपोर्ट – प्रक्रिया का अवलोकन

ऑपरेशन तीन तार्किक चरणों में विभाजित है:

1. **Load** वर्कबुक को डिस्क से लोड करें।  
2. **Define** वह सेल क्षेत्र जो इमेज बन जाएगा ( *print area* )।  
3. **Export** क्षेत्र को `ImageOrPrintOptions` का उपयोग करके एक्सपोर्ट करें और फ़ाइल लिखें।  

नीचे प्रत्येक चरण को एक समर्पित स्टेप में विभाजित किया गया है जिसमें पूर्ण स्रोत कोड और व्याख्या शामिल है।

## चरण 1: वर्कबुक लोड करें

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Path to the source Excel file
string inputPath = @"YOUR_DIRECTORY\input.xlsx";

// Create a Workbook object – this reads the file into memory
Workbook workbook = new Workbook(inputPath);
```

**यह क्यों महत्वपूर्ण है:**  
`Workbook` सभी Excel ऑपरेशनों का प्रवेश बिंदु है। फ़ाइल को एक बार लोड करने से मेमोरी उपयोग कम रहता है और बाद में किसी भी वर्कशीट तक पहुंच संभव होती है।

## चरण 2: लक्ष्य वर्कशीट तक पहुंचें

```csharp
// Get the first worksheet (index 0). Change the index or use the sheet name as needed.
Worksheet sheet = workbook.Worksheets[0];
```

**टिप:** यदि आपको नाम से कोई विशिष्ट शीट चाहिए, तो इंडेक्स को `workbook.Worksheets["SheetName"]` से बदलें। इससे वर्कबुक लेआउट बदलने पर त्रुटियों से बचा जा सकता है।

## चरण 3: वह रेंज निर्धारित करें जिसे आप एक्सपोर्ट करना चाहते हैं

```csharp
// Define the cell range that will be exported.
// Example: A1:G20 captures a typical pivot‑table area.
sheet.PageSetup.PrintArea = "A1:G20";
```

**`PrintArea` क्यों सेट करें?**  
Aspose.Cells इमेज बनाते समय *print area* को रेंडर करता है। इसे सटीक रेंज तक सीमित करके आप अतिरिक्त खाली जगह से बचते हैं और प्रदर्शन में सुधार करते हैं।

### वैकल्पिक: पूरी शीट को एक्सपोर्ट करें

यदि आप पूरी वर्कशीट चाहते हैं, तो बस `PrintArea` असाइनमेंट को छोड़ दें। Aspose.Cells डिफ़ॉल्ट रूप से शीट की उपयोग की गई रेंज का उपयोग करेगा।

## चरण 4: इमेज एक्सपोर्ट विकल्प कॉन्फ़िगर करें

```csharp
// Create an ImageOrPrintOptions object to control the output format.
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    // Choose PNG for lossless quality; change to Jpeg for smaller files.
    ImageFormat = ImageFormat.Png,

    // Optional: set the resolution (DPI). Higher DPI yields sharper images.
    HorizontalResolution = 300,
    VerticalResolution = 300,

    // Optional: set the page orientation if the range is wide.
    PageOrientation = PageOrientationType.Landscape
};
```

**मुख्य प्रॉपर्टीज़ की व्याख्या:**

* `ImageFormat` – फ़ाइल प्रकार निर्धारित करता है (`Png`, `Jpeg`, `Bmp`, आदि)। PNG चार्ट और टेक्स्ट के लिए आदर्श है क्योंकि यह स्पष्ट किनारों को बनाए रखता है।  
* `HorizontalResolution` / `VerticalResolution` – पिक्सेल घनत्व को नियंत्रित करते हैं। वेब थंबनेल के लिए 96 DPI पर्याप्त है; प्रिंट‑रेडी ग्राफिक्स के लिए 300 DPI की सिफारिश की जाती है।  
* `PageOrientation` – तब मदद करता है जब चयनित रेंज चौड़ी हो और ऊँची नहीं।  

## चरण 5: रेंज को इमेज फ़ाइल में एक्सपोर्ट करें

```csharp
// Define the output path for the image
string outputPath = @"YOUR_DIRECTORY\range.png";

// Save the first picture on the worksheet as an image.
// The Pictures collection is automatically populated after setting PrintArea.
sheet.Pictures[0].Save(outputPath, imgOptions);
```

**आंतरिक रूप से क्या होता है:**  
जब `PrintArea` सेट किया जाता है, तो Aspose.Cells उस क्षेत्र का एक अस्थायी चित्र बनाता है। फिर `Pictures[0]` ऑब्जेक्ट को आपके द्वारा प्रदान किए गए विकल्पों का उपयोग करके सहेजा जाता है।

### वर्कशीट में बिना चित्रों के हैंडलिंग

यदि वर्कशीट में पहले से कोई चित्र नहीं है (जैसे, एक नई फ़ाइल), तो आप इसे तुरंत बना सकते हैं:

```csharp
// Create a picture from the defined range and add it to the sheet
Picture pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
pic.Save(outputPath, imgOptions);
```

## पूर्ण, चलाने योग्य उदाहरण

सब कुछ मिलाकर, यहाँ एक स्वतंत्र कंसोल एप्लिकेशन है जिसे आप कॉपी, पेस्ट और चलाकर उपयोग कर सकते हैं:

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // 2️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 3️⃣ Define the range to export (e.g., a pivot table)
        sheet.PageSetup.PrintArea = "A1:G20";

        // 4️⃣ Set image export options (PNG, 300 DPI, landscape)
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300,
            PageOrientation = PageOrientationType.Landscape
        };

        // 5️⃣ Save the picture as an image file
        string outputPath = @"YOUR_DIRECTORY\range.png";

        // Ensure a picture exists; create one if necessary
        Picture pic;
        if (sheet.Pictures.Count == 0)
        {
            pic = sheet.Pictures[sheet.Pictures.Add(0, 0, sheet.PageSetup.PrintArea)];
        }
        else
        {
            pic = sheet.Pictures[0];
        }

        pic.Save(outputPath, imgOptions);

        System.Console.WriteLine($"Export completed: {outputPath}");
    }
}
```

**अपेक्षित आउटपुट:**  
`range.png` नाम की फ़ाइल `YOUR_DIRECTORY` में दिखाई देती है। इसे खोलने पर **A1 से G20** तक के सटीक सेल्स एक स्पष्ट PNG इमेज के रूप में दिखते हैं।

## सामान्य विविधताएँ और किनारे‑के‑मामले हैंडलिंग

| परिदृश्य | समायोजन |
|----------|------------|
| **Export to JPEG** | `ImageFormat = ImageFormat.Jpeg` में बदलें और वैकल्पिक रूप से `Quality = 90` सेट करें (रेंज 0‑100)। |
| **Multiple ranges** | `sheet.Pictures.Add` को प्रत्येक रेंज के लिए कॉल करें और प्रत्येक चित्र को अलग फ़ाइलनाम के साथ सहेजें। |
| **Large worksheets** | केवल आवश्यक रेंज के लिए `HorizontalResolution`/`VerticalResolution` बढ़ाएँ ताकि मेमोरी स्पाइक से बचा जा सके। |
| **No picture generated** | सुनिश्चित करें कि `PrintArea` सही ढंग से फॉर्मेट किया गया है (`"A1:G20"`). एक अमान्य पता खाली `Pictures` कलेक्शन का परिणाम देगा। |
| **Saving to a stream** | जब आपको इमेज मेमोरी में चाहिए (जैसे, ASP.NET रिस्पॉन्स के लिए), तो `pic.Save(Stream, imgOptions)` का उपयोग करें। |

## विश्वसनीय इमेज एक्सपोर्ट के लिए प्रो टिप्स

* **Print area को वैलिडेट करें** – `CellArea` पार्सिंग (`CellArea area = CellArea.CreateCellArea("A1", "G20")`) का उपयोग करके प्रोग्रामेटिकली रेंज बनाएं और टाइपो से बचें।  
* **संसाधनों को डिस्पोज़ करें** – यदि आप कई फ़ाइलें प्रोसेस कर रहे हैं तो `Workbook` को `using` ब्लॉक में रखें ताकि नेटिव रिसोर्सेज तुरंत मुक्त हो सकें।  
* **बैच प्रोसेसिंग** – जब दर्जनों रेंज एक्सपोर्ट कर रहे हों, तो एक ही `ImageOrPrintOptions` इंस्टेंस को पुन: उपयोग करें ताकि ऑब्जेक्ट अलोकेशन ओवरहेड कम हो।  
* **थ्रेड सुरक्षा** – Aspose.Cells ऑब्जेक्ट **थ्रेड‑सेफ़** नहीं हैं। प्रत्येक थ्रेड के लिए अलग `Workbook` बनाएं या एक्सेस को सिंक्रोनाइज़ करें।  

## निष्कर्ष

अब आपके पास C# और Aspose.Cells का उपयोग करके **export excel range as image** करने की एक पूर्ण, प्रोडक्शन‑रेडी विधि है। चरण—वर्कबुक लोड करना, प्रिंट एरिया सेट करना, `ImageOrPrintOptions` कॉन्फ़िगर करना, और चित्र सहेजना—दोनों “कैसे” और “क्यों” को कवर करते हैं, जिससे आप कोड को पिवट टेबल, चार्ट, या किसी भी कस्टम सेल ब्लॉक में अनुकूलित कर सकते हैं।

अगला, आप निम्नलिखित का अन्वेषण कर सकते हैं:

* **Export excel range as image** को अन्य फ़ॉर्मैट्स (SVG, BMP) में एक्सपोर्ट करें – एक और द्वितीयक कीवर्ड जिसे आप आज़मा सकते हैं।  
* Aspose.PDF का उपयोग करके PNG को PDF में एम्बेड करना, एंड‑टू‑एंड रिपोर्ट जनरेशन के लिए।  
* एक सरल कंसोल लूप के साथ कई वर्कबुक्स में बैच एक्सपोर्ट को ऑटोमेट करना।  

विभिन्न रिज़ॉल्यूशन, ओरिएंटेशन, और आउटपुट डायरेक्टरीज़ के साथ प्रयोग करने में संकोच न करें। कोडिंग का आनंद लें!

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर करने में मदद करती हैं।

- [Aspose.Cells .NET का उपयोग करके Excel सेल्स को इमेज में एक्सपोर्ट: चरण‑दर‑चरण गाइड](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Aspose.Cells for Java का उपयोग करके Excel वर्कबुक को इमेज में एक्सपोर्ट](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Aspose.Cells Java का उपयोग करके Excel वर्कशीट को PNG में एक्सपोर्ट कैसे करें](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}