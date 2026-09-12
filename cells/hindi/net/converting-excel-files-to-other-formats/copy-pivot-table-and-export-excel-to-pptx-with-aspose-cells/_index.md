---
category: general
date: 2026-09-11
description: Aspose.Cells का उपयोग करके पिवट टेबल को कॉपी करें और Excel को PPTX में
  निर्यात करें। C# में संपादन योग्य PPTX उत्पन्न करना सीखें और वर्कबुक को PPTX के
  रूप में सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: hi
lastmod: 2026-09-11
og_description: Aspose.Cells का उपयोग करके C# में पिवट टेबल कॉपी करें और Excel को
  PPTX में निर्यात करें। कुछ ही कोड लाइनों से संपादन योग्य PPTX बनाएं और वर्कबुक को
  PPTX के रूप में सहेजें।
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: पिवट टेबल कॉपी करें और एक्सेल को PPTX में निर्यात करें – पूर्ण C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Aspose.Cells के साथ पिवट टेबल कॉपी करें और एक्सेल को PPTX में निर्यात करें
url: /hi/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells के साथ पिवट टेबल कॉपी करें और Excel को PPTX में एक्सपोर्ट करें

यदि आपको एक वर्कशीट से दूसरी वर्कशीट में पिवट टेबल कॉपी करनी है और फिर Excel फ़ाइल को PowerPoint प्रस्तुति में एक्सपोर्ट करना है, तो यह गाइड आपको दिखाएगा कैसे। Aspose.Cells का उपयोग करके आप कुछ ही C# कोड लाइनों में एक संपादन योग्य PPTX जेनरेट कर सकते हैं और वर्कबुक को PPTX के रूप में सहेज सकते हैं।

यह ट्यूटोरियल पिवट टेबल को स्थानांतरित करने, उसकी कार्यक्षमता बनाए रखने, और एक ऐसा PPTX फ़ाइल बनाने के सभी चरणों को कवर करता है जहाँ चार्ट और शेप्स संपादन योग्य रहते हैं। कोई बाहरी टूल आवश्यक नहीं—केवल Aspose.Cells लाइब्रेरी और एक .NET विकास वातावरण।

## आप क्या हासिल करेंगे

* **Copy pivot table** स्रोत शीट से गंतव्य शीट में सभी डेटा कनेक्शन को बनाए रखते हुए कॉपी करें।  
* **Export Excel to PPTX** ताकि परिणामी स्लाइड को PowerPoint में संपादित किया जा सके।  
* **Generate editable PPTX** जहाँ चार्ट, टेबल और शेप्स इमेज में नहीं बदलते।  
* **Save workbook as PPTX** वही Aspose.Cells API कॉल का उपयोग करके सहेजें।  

### पूर्वापेक्षाएँ

* .NET 6.0 या बाद का (कोड .NET Framework 4.6+ के साथ भी काम करता है)।  
* Aspose.Cells for .NET (NuGet पैकेज `Aspose.Cells`)।  
* C# कंसोल एप्लिकेशन की बुनियादी समझ।  

> **Pro tip:** नवीनतम संस्करण सुनिश्चित करने के लिए CLI के माध्यम से NuGet पैकेज इंस्टॉल करें:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## How to copy pivot table between worksheets

पहला ऑपरेशन पिवट टेबल को उसकी परिभाषा को बनाए रखते हुए स्थानांतरित करना है। Aspose.Cells `CopyRange` मेथड के साथ `CopyOptions` ऑब्जेक्ट प्रदान करता है जिसमें `CopyPivotTable` फ़्लैग शामिल है।

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Why this works:**  
`CopyRange` सेल डेटा, फ़ॉर्मेटिंग, और जब `CopyPivotTable` true हो तो पिवट टेबल का कैश और मेटाडेटा कॉपी करता है। गंतव्य रेंज सेल `A1` (पंक्ति 0, कॉलम 0) से शुरू होती है, लेकिन आप ऑफ़सेट बदलकर पिवट टेबल को कहीं और रख सकते हैं।

**Common edge case:** यदि गंतव्य शीट में पहले से ही समान नाम की पिवट टेबल मौजूद है, तो Aspose.Cells स्वचालित रूप से आने वाली टेबल का नाम बदल देगा, जिससे नाम टकराव नहीं होगा।

## Export Excel to PPTX and generate editable PPTX

पिवट टेबल स्थापित होने के बाद, आप पूरी वर्कबुक को PPTX फ़ाइल में एक्सपोर्ट कर सकते हैं। `ImageOrPrintOptions` क्लास आपको `ExportImageFormat = ImageFormat.Pptx` सेट करने की अनुमति देती है, जिससे Aspose.Cells आउटपुट को रास्टर इमेज के बजाय PowerPoint प्रस्तुति के रूप में ट्रीट करता है।

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Why this works:**  
जब `ExportImageFormat` को `Pptx` पर सेट किया जाता है, तो Aspose.Cells प्रत्येक वर्कशीट को एक स्लाइड में बदल देता है। शेप्स, चार्ट और पिवट टेबल को नेटिव PowerPoint ऑब्जेक्ट्स के रूप में लिखा जाता है, इसलिए आप PowerPoint में उन्हें डबल‑क्लिक करके अंतर्निहित डेटा को संपादित कर सकते हैं।

**Tip for large workbooks:** यदि आपको केवल कुछ शीट्स चाहिए, तो `Save` कॉल करने से पहले उन शीट्स को हटाने के लिए `workbook.Worksheets.RemoveAt(index)` सेट करें। इससे PPTX फ़ाइल का आकार घटता है।

## Full, runnable example

नीचे पूरा प्रोग्राम है जो पिछले चरणों को जोड़ता है। `YOUR_DIRECTORY` को अपने मशीन पर वास्तविक पाथ से बदलें।

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Expected output

प्रोग्राम चलाने पर यह प्रिंट करता है:

```
Pivot table copied and workbook exported to PPTX successfully.
```

जब आप `output.pptx` को Microsoft PowerPoint में खोलते हैं, तो आपको एक स्लाइड दिखेगी जिसमें कॉपी की गई पिवट टेबल एक संपादन योग्य चार्ट के रूप में होगी। चार्ट पर डबल‑क्लिक करने से PowerPoint चार्ट एडिटर खुलता है, जिससे आप सीरीज़, एक्सिस और डेटा लेबल्स को Excel में वापस जाए बिना संशोधित कर सकते हैं।

## Handling typical pitfalls

| समस्या | कारण | समाधान |
|-------|-------|-----|
| पिवट टेबल स्थिर छवि के रूप में दिखती है | `CopyPivotTable` फ़्लैग नहीं दिया गया या `ExportImageFormat` को `Png` पर सेट किया गया | सुनिश्चित करें कि `CopyPivotTable = true` और `ExportImageFormat = ImageFormat.Pptx` हो। |
| डेस्टिनेशन शीट में खाली सेल दिख रहे हैं | स्रोत रेंज पूरी पिवट टेबल क्षेत्र को कवर नहीं करती | रेंज को विस्तारित करें (जैसे, `"A1:H30"`) ताकि सभी पिवट फ़ील्ड शामिल हों। |
| एक्सपोर्ट किया गया PPTX बहुत बड़ा है | अनावश्यक वर्कशीट्स शामिल हैं | `Save` कॉल करने से पहले अनावश्यक शीट्स को हटा दें। |
| PowerPoint चार्ट को संपादित नहीं कर पा रहा है | Aspose.Cells का पुराना संस्करण उपयोग किया गया है जिसमें PPTX समर्थन नहीं है | नवीनतम Aspose.Cells संस्करण में अपग्रेड करें (रिलीज़ नोट्स देखें)। |

## Next steps and related topics

* **Export Excel sheet to PPTX with custom slide layouts** – स्लाइड की उपस्थिति पर अधिक नियंत्रण के लिए `WorksheetToPdfConverter` का अन्वेषण करें।  
* **Export Excel to PDF** – PDF जेनरेट करने के लिए `ImageFormat.Pptx` को `ImageFormat.Pdf` से बदलें।  
* **Programmatically modify PPTX after export** – एनीमेशन या स्पीकर नोट्स जोड़ने के लिए `Aspose.Slides` लाइब्रेरी का उपयोग करें।  

**copy pivot table**, **export excel to pptx**, और **generate editable pptx** में महारत हासिल करके आप एंड‑टू‑एंड रिपोर्टिंग पाइपलाइन बना सकते हैं जो स्प्रेडशीट्स से डेटा को सीधे प्रेजेंटेशन डेक्स में ले जाता है बिना संपादन क्षमता खोए।

---

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में निपुण होने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर करने में मदद करेंगे।

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Excel Workbook – Copy & Duplicate Pivot Table](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Create a Pivot Table in Excel Using Aspose.Cells for .NET](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}