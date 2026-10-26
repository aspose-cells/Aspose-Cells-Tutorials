---
category: general
date: 2026-10-26
description: प्रिंट एरिया सेट करें और C# में Excel शीट को PNG में निर्यात करें। इमेज
  निर्यात विकल्पों के बारे में जानें, PNG कैसे निर्यात करें, और वर्कबुक से प्रिंट
  करने योग्य इमेज प्राप्त करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: hi
lastmod: 2026-10-26
og_description: C# में प्रिंट एरिया सेट करें और Excel शीट को PNG में निर्यात करें।
  यह चरण‑दर‑चरण ट्यूटोरियल इमेज निर्यात विकल्पों और वर्कबुक से PNG निर्यात करने के
  तरीके को कवर करता है।
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: प्रिंट एरिया सेट करें और एक्सेल शीट को PNG में निर्यात करें – C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C# में प्रिंट एरिया सेट करें और एक्सेल शीट को PNG में निर्यात करें
url: /hi/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में प्रिंट एरिया सेट करें और Excel शीट को PNG में एक्सपोर्ट करें

यदि आपको Excel शीट को PNG में एक्सपोर्ट करने से पहले **प्रिंट एरिया सेट** करना है, तो यह गाइड आपको दिखाएगा कैसे। आप एक पूर्ण C# उदाहरण देखेंगे जो इमेज एक्सपोर्ट विकल्पों को कॉन्फ़िगर करता है, वर्कशीट के प्रिंट एरिया को समायोजित करता है, और परिणाम को इमेज के रूप में सहेजता है।

Excel शीट को PNG में एक्सपोर्ट करना अक्सर तब आवश्यक होता है जब आप किसी रिपोर्ट, ईमेल या वेब पेज में वर्कशीट का स्नैपशॉट एम्बेड करना चाहते हैं। नीचे दिया गया कोड किसी भी वर्कबुक के साथ काम करता है जिसमें पिवट टेबल हो, लेकिन यह तकनीक सामान्य डेटा रेंज पर भी लागू होती है। कोई बाहरी टूल्स आवश्यक नहीं—सिर्फ Aspose.Cells for .NET लाइब्रेरी की जरूरत है।

## आवश्यकताएँ

- .NET 6.0 या बाद का संस्करण (सैंपल .NET 6 को टार्गेट करता है, लेकिन कोई भी हालिया .NET संस्करण काम करेगा)
- Aspose.Cells for .NET (NuGet के माध्यम से इंस्टॉल करें: `Install-Package Aspose.Cells`)
- C# और Excel अवधारणाओं जैसे वर्कशीट और प्रिंट एरिया की बुनियादी समझ

## चरण 1: इमेज एक्सपोर्ट विकल्प कॉन्फ़िगर करें

सबसे पहले आपको `ImageOrPrintOptions` का एक इंस्टेंस बनाना होगा। यह ऑब्जेक्ट Aspose.Cells को बताता है कि शीट को इमेज के रूप में कैसे रेंडर किया जाए।

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**क्यों महत्वपूर्ण है:** `ImageOrPrintOptions` आउटपुट फ़ॉर्मेट, रिज़ॉल्यूशन और अन्य रेंडरिंग विवरणों को नियंत्रित करता है। PNG का उपयोग करने से लॉसलेस क्वालिटी मिलती है, जो उन रिपोर्टों के लिए आदर्श है जिन्हें स्पष्ट टेक्स्ट और ग्राफ़िक्स चाहिए।

## चरण 2: वर्कबुक लोड करें और लक्ष्य वर्कशीट तक पहुँचें

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**क्यों महत्वपूर्ण है:** आपको एक विशिष्ट `Worksheet` ऑब्जेक्ट के साथ काम करना आवश्यक है क्योंकि प्रिंट एरिया वर्कशीट‑लेवल सेटिंग है।

## चरण 3: वह रेंज पहचानें जिसे आप प्रिंट करना चाहते हैं

कई मामलों में वह डेटा जो आपको चाहिए पिवट टेबल के भीतर रहता है। नीचे दिया गया कोड शीट पर पहली पिवट टेबल का डेटा रेंज निकालता है।

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

यदि आपकी वर्कशीट में पिवट टेबल नहीं है, तो आप `pivotDataRange` को किसी भी `CellArea` से बदल सकते हैं जिसे आप मैन्युअली बनाते हैं, उदाहरण के लिए:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## चरण 4: **प्रिंट एरिया सेट** करें ताकि वह चयनित रेंज से मेल खाए

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**क्यों महत्वपूर्ण है:** प्रिंट एरिया Excel (और Aspose.Cells) को बताता है कि इमेज रेंडर करते समय किन सेल्स को शामिल किया जाए। प्रिंट एरिया को पिवट डेटा रेंज के साथ संरेखित करने से खाली मार्जिन से बचा जा सकता है और एक्सपोर्टेड PNG में केवल संबंधित डेटा ही रहेगा।

## चरण 5: वर्कशीट को PNG इमेज में एक्सपोर्ट करें

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**क्यों महत्वपूर्ण है:** `worksheet.ToImage` पहले सेट किए गए प्रिंट एरिया का सम्मान करता है, इसलिए PNG फ़ाइल में बिल्कुल वही सेल्स होते हैं जो आपने परिभाषित किए हैं। इमेज को पिक्चर शेप में असाइन करने से आप आवश्यकता पड़ने पर उसे फिर से वर्कबुक में एम्बेड कर सकते हैं, जबकि डिस्क पर सहेजने से आपको एक स्टैंडअलोन फ़ाइल मिलती है।

## पूर्ण कार्यशील उदाहरण

सभी चरणों को मिलाकर एक स्व-समाहित प्रोग्राम बनता है जिसे आप तुरंत चला सकते हैं।

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### अपेक्षित आउटपुट

प्रोग्राम चलाने पर `C:\Temp\WorksheetExport.png` बनता है। फ़ाइल खोलने पर एक स्पष्ट PNG इमेज दिखती है जिसमें केवल **सेट प्रिंट एरिया** द्वारा परिभाषित सेल्स (इस उदाहरण में पिवट टेबल डेटा) होते हैं। इस इमेज को Word दस्तावेज़, PowerPoint स्लाइड या वेब पेज में अतिरिक्त रूपांतरण चरणों के बिना डाला जा सकता है।

## कई वर्कशीट्स या पिवट टेबल्स को संभालना

- **कई वर्कशीट्स:** `wb.Worksheets` पर लूप करें और प्रत्येक शीट के लिए चरण 3‑5 दोहराएँ जिन्हें आप एक्सपोर्ट करना चाहते हैं।
- **कई पिवट टेबल्स:** उपयुक्त `PivotTables[index]` चुनें या `worksheet.PivotTables` पर इटररेट करके प्रत्येक टेबल को अलग‑अलग एक्सपोर्ट करें।
- **कोई पिवट टेबल नहीं:** मैन्युअली `CellArea` बनाएं (स्टेप 3 में टिप्पणी देखें) और उसे `PrintArea` को असाइन करें।

## व्यावहारिक टिप्स (E‑E‑A‑T)

- **प्रो टिप:** प्रिंट‑रेडी PNG के लिए `HorizontalResolution` और `VerticalResolution` को 300 DPI पर सेट करें; वेब उपयोग के लिए फ़ाइल आकार कम करने हेतु कम मान भी उपयोग कर सकते हैं।
- **खाली पिक्चर शेप्स से सावधान रहें:** यदि वर्कशीट में कोई पिक्चर शेप नहीं है, तो इमेज असाइन करने से पहले एक जोड़ें:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **परफ़ॉर्मेंस:** कई वर्कशीट्स के लिए एक ही `ImageOrPrintOptions` इंस्टेंस का पुनः उपयोग करने से अनावश्यक मेमोरी अलोकेशन बचता है।
- **कम्पैटिबिलिटी:** Aspose.Cells 23.9+ पूरी तरह से .NET 6 और बाद के संस्करणों को सपोर्ट करता है; पुराने संस्करणों में API नामों में कुछ समायोजन की आवश्यकता हो सकती है।

## निष्कर्ष

अब आप जानते हैं कि **प्रिंट एरिया सेट** करके Excel को PNG में कैसे एक्सपोर्ट किया जाता है।

## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Excel को PNG में एक्सपोर्ट करने की पूरी स्टेप‑बाय‑स्टेप गाइड](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [C# और Aspose.Cells के साथ Excel रेंज को इमेज के रूप में एक्सपोर्ट करना](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel sheet to png – C# में पिवट टेबल को PNG के रूप में एक्सपोर्ट करना](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}