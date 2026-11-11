---
category: general
date: 2026-10-26
description: C# के साथ Excel चार्ट को PowerPoint में निर्यात करना सीखें। आकार की संपादन
  योग्यता बनाए रखें और कुछ ही कोड लाइनों में PPTX के रूप में सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: hi
lastmod: 2026-10-26
og_description: C# के साथ Excel चार्ट को PowerPoint में निर्यात करें। यह गाइड दिखाता
  है कि कैसे आकृतियों को संपादन योग्य रखें और Aspose.Cells का उपयोग करके PPTX के रूप
  में सहेजें।
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: C# के साथ Excel चार्ट को PowerPoint में निर्यात करें – चरण-दर-चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: C# का उपयोग करके Excel चार्ट्स को PowerPoint में निर्यात कैसे करें
url: /hi/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# का उपयोग करके Excel चार्ट को PowerPoint में निर्यात कैसे करें

यदि आपको **Excel चार्ट को PowerPoint में निर्यात** करना है, तो यह गाइड आपको एक पूर्ण, तैयार‑चलाने योग्य समाधान के माध्यम से ले जाता है। चाहे आप रिपोर्टिंग डैशबोर्ड बना रहे हों या स्लाइड डेक्स को स्वचालित कर रहे हों, आप देखेंगे कि C# कोड की कुछ पंक्तियों से आपके चार्ट आकार रूपांतरण के बाद भी पूरी तरह संपादन योग्य रहते हैं।

इस ट्यूटोरियल में आप सीखेंगे कि कैसे:

* चार्ट वाले मौजूदा Excel वर्कबुक को लोड करें।  
* (वैकल्पिक) रूपांतरण से पहले वर्कबुक सेटिंग्स को समायोजित करें।  
* वर्कबुक को PowerPoint फ़ाइल के रूप में सहेजें जबकि आकार की संपादन क्षमता को बनाए रखें।  

इन सबको **Aspose.Cells for .NET** के साथ किया जाता है, एक लाइब्रेरी जो सर्वर पर Microsoft Office की आवश्यकता के बिना Excel‑to‑PowerPoint रूपांतरण को संभालती है।

## आपको क्या चाहिए

| आवश्यकता | कारण |
|-------------|--------|
| .NET 6.0 or later | आधुनिक रनटाइम जिसमें पूरी भाषा सुविधाएँ हैं |
| Visual Studio 2022 (or any IDE) | सुविधाजनक संपादक और डिबगर |
| **Aspose.Cells for .NET** NuGet package | `Workbook` क्लास और `SaveFormat.Pptx` समर्थन प्रदान करता है |
| An Excel file (`ChartAndShapes.xlsx`) that contains at least one chart | एक Excel फ़ाइल (`ChartAndShapes.xlsx`) जिसमें कम से कम एक चार्ट हो |

> **प्रो टिप:** कोड का परीक्षण करने के लिए मुफ्त **Aspose.Cells Evaluation** संस्करण का उपयोग करें; लाइसेंस कुंजी मूल्यांकन वॉटरमार्क को हटा देती है।

```bash
dotnet add package Aspose.Cells
```

## Excel चार्ट को PowerPoint में निर्यात – पूर्ण कार्यप्रवाह

नीचे वह अंत‑से‑अंत कोड है जो निर्यात को **आकार की संपादन क्षमता को बनाए रखते हुए** पूरा करता है। प्रत्येक चरण को विस्तार से समझाया गया है।

### चरण 1: Excel वर्कबुक लोड करें

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

`Workbook` क्लास पूरे Excel फ़ाइल का प्रतिनिधित्व करता है। फ़ाइल को लोड करने से सभी वर्कशीट, चार्ट और आकार मेमोरी में पढ़े जाते हैं, जो आगे की किसी भी हेरफेर के लिए आवश्यक है।

### चरण 2: (वैकल्पिक) वर्कबुक सेटिंग्स समायोजित करें

अधिकांश मामलों में डिफ़ॉल्ट सेटिंग्स साफ़ निर्यात के लिए पर्याप्त होती हैं। हालांकि, यदि आपको गणना मोड, पेज सेटअप बदलना है, या कुछ शीट्स को छिपाना है, तो आप यहाँ कर सकते हैं।

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **यह क्यों महत्वपूर्ण है:** रूपांतरण से पहले सेटिंग्स समायोजित करने से यह सुनिश्चित होता है कि उत्पन्न स्लाइड्स वही सटीक स्थिति दर्शाएँ जो आप चाहते हैं, विशेषकर जब फ़ॉर्मूले या छिपी शीट्स चार्ट डेटा को प्रभावित कर सकती हैं।

### चरण 3: वर्कबुक को PowerPoint फ़ाइल के रूप में सहेजें

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

`SaveFormat.Pptx` कॉन्स्टेंट Aspose.Cells को PowerPoint प्रस्तुति लिखने के लिए बताता है। आंतरिक रूप से, लाइब्रेरी प्रत्येक Excel चार्ट को PowerPoint आकार में परिवर्तित करती है जो Microsoft PowerPoint में पूरी तरह संपादन योग्य रहता है।

### चरण 4: परिणाम सत्यापित करें

`Shapes.pptx` को PowerPoint में खोलें और:

1. किसी भी स्लाइड पर एक चार्ट चुनें।  
2. राइट‑क्लिक → **Edit Data**।  
3. पुष्टि करें कि चार्ट डेटा टेबल दिखाई देती है और आप मान बदल सकते हैं।

यदि चार्ट **Edit Data** पैनल खोलता है, तो रूपांतरण सफल रहा और **आकार की संपादन क्षमता** बनी रहती है।

![Export Excel charts to PowerPoint example](export-excel-charts-to-powerpoint.png){.img-fluid alt="PowerPoint में Excel चार्ट निर्यात का उदाहरण"}

## सामान्य समस्याएँ और उन्हें कैसे टालें

| समस्या | कारण | समाधान |
|-------|-------|-----|
| चार्ट स्थिर छवियों के रूप में दिखते हैं | ऐसी पुरानी Aspose.Cells संस्करण का उपयोग करना जिसमें PPTX निर्यात समर्थन नहीं है | नवीनतम Aspose.Cells 23.x या बाद के संस्करण में अपग्रेड करें |
| PowerPoint चार्ट में डेटा गायब है | निर्यात से पहले वर्कबुक पूरी तरह गणना नहीं हुई | सेव करने से पहले `workbook.CalculateFormula()` कॉल करें |
| आकार संपादन योग्य नहीं हैं | `SaveFormat.Xlsx` के साथ सहेजना, `SaveFormat.Pptx` के बजाय | सुनिश्चित करें कि आप `Workbook.Save` में `SaveFormat.Pptx` पास कर रहे हैं |
| रनटाइम पर लाइसेंस अपवाद | पंजीकृत लाइसेंस के बिना मूल्यांकन संस्करण | अपना लाइसेंस इस प्रकार पंजीकृत करें: `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### किनारा मामला: अलग-अलग चार्ट वाले कई वर्कशीट निर्यात करना

यदि आपकी Excel फ़ाइल में कई वर्कशीट हैं, प्रत्येक में अपना चार्ट है, तो Aspose.Cells स्वचालित रूप से प्रत्येक चार्ट के लिए एक अलग स्लाइड बनाता है। आप सहेजने से पहले वर्कशीट को पुनर्व्यवस्थित करके स्लाइड क्रम नियंत्रित कर सकते हैं।

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### प्रदर्शन टिप: डिस्क पर लिखने के बजाय आउटपुट को स्ट्रीम करें

वेब API में PowerPoint फ़ाइलें बनाते समय, `MemoryStream` में लिखकर अस्थायी फ़ाइलों से बचें।

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## पूर्ण, चलाने योग्य उदाहरण

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**अपेक्षित आउटपुट:** कंसोल पुष्टि संदेश प्रिंट करता है, और `Shapes.pptx` PowerPoint में खुलता है जहाँ प्रत्येक Excel चार्ट अपनी स्लाइड पर दिखता है। एक चार्ट चुनने से आप उसका डेटा संपादित कर सकते हैं, जिससे पुष्टि होती है कि **आकार की संपादन क्षमता** बनी रहती है।

## सारांश और अगले कदम

अब आप जानते हैं कि C# के साथ **Excel चार्ट को PowerPoint में निर्यात** कैसे करें जबकि चार्ट पूरी तरह संपादन योग्य रहें। समाधान का मूल `Workbook.Save` मेथड है जिसमें `SaveFormat.Pptx` उपयोग किया जाता है, जो **Aspose.Cells export** की एक सुविधा है जो जटिल Open XML हैंडलिंग को सरल बनाती है।

From here you might explore:

* **Aspose.Slides** API का उपयोग करके कस्टम स्लाइड शीर्षक या नोट्स जोड़ना।  
* चार्ट के साथ अन्य Excel ऑब्जेक्ट्स (टेबल, इमेज) को भी परिवर्तित करना।  
* बैकग्राउंड सर्विस में कई वर्कबुक की बैच प्रोसेसिंग को स्वचालित करना।

ऊपर दिखाए गए वैकल्पिक सेटिंग्स के साथ प्रयोग करने में संकोच न करें, और इस पैटर्न को अपनी रिपोर्टिंग पाइपलाइन में एकीकृत करें ताकि तेज़ और भरोसेमंद PowerPoint जनरेशन हो सके।

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [C# के साथ Excel चार्ट को PowerPoint में निर्यात – पूर्ण Aspose.Cells गाइड](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [C# के साथ Excel को PowerPoint में निर्यात कैसे करें – पूर्ण गाइड](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [Excel से PowerPoint में आकार निर्यात कैसे करें – पूर्ण गाइड](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}