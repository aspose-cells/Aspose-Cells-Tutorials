---
category: general
date: 2026-09-15
description: SVG में फ़ॉन्ट एम्बेड करना और Excel चार्ट को PowerPoint में निर्यात करना
  सीखें, जिसमें XLSX को SVG में बदलना और XLSX को PPTX में बदलना, साथ ही पूर्ण कोड
  उदाहरण शामिल हैं।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in SVG
- export excel chart to powerpoint
- convert xlsx to svg
- convert xlsx to pptx
- save workbook as svg
language: hi
lastmod: 2026-09-15
og_description: SVG में फ़ॉन्ट एम्बेड करें और चरण‑दर‑चरण C# कोड के साथ Excel चार्ट
  को PowerPoint में निर्यात करें। XLSX को SVG और XLSX को PPTX में तेज़ी और भरोसेमंद
  तरीके से परिवर्तित करें।
og_image_alt: Screenshot showing an Excel chart exported to PowerPoint with embedded
  fonts in the resulting SVG file
og_title: SVG में फ़ॉन्ट एम्बेड करें और Excel चार्ट को PowerPoint में निर्यात करें
  – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  headline: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  type: TechArticle
- description: Learn how to embed fonts in SVG and export Excel chart to PowerPoint,
    covering convert XLSX to SVG and convert XLSX to PPTX with full code examples.
  name: How to embed fonts in SVG when converting Excel files to SVG and PowerPoint
  steps:
  - name: Open `EditableChart.pptx` in PowerPoint.
    text: Open `EditableChart.pptx` in PowerPoint.
  - name: Locate the slide containing the chart.
    text: Locate the slide containing the chart.
  - name: Choose **Chart Tools → Design → Edit Data**.
    text: Choose **Chart Tools → Design → Edit Data**.
  - name: Confirm that the Excel‑style data grid appears and that you can change values.
    text: Confirm that the Excel‑style data grid appears and that you can change values.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel फ़ाइलों को SVG और PowerPoint में बदलते समय SVG में फ़ॉन्ट एम्बेड कैसे
  करें
url: /hi/net/converting-excel-files-to-other-formats/how-to-embed-fonts-in-svg-when-converting-excel-files-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel फ़ाइलों को SVG और PowerPoint में बदलते समय SVG में फ़ॉन्ट एम्बेड कैसे करें  

यदि आपको Excel वर्कबुक को बदलते समय **SVG में फ़ॉन्ट एम्बेड** करने की आवश्यकता है, तो यह गाइड आपको ठीक‑ठीक बताता है कि कैसे करना है। आप यह भी सीखेंगे कि **Excel चार्ट को PowerPoint में एक्सपोर्ट** कैसे करें, और **XLSX को SVG** तथा **XLSX को PPTX** को संपादन योग्य चार्ट के साथ कैसे बदलें।  

प्रोग्रामेटिक रूप से Excel डेटा के साथ काम करने का मतलब अक्सर वही विज़ुअल कंटेंट विभिन्न फ़ाइल फ़ॉर्मेट्स के बीच ले जाना होता है। PowerPoint में मैन्युअली चार्ट को फिर से बनाना या SVG में फ़ॉन्ट को दोबारा लागू करना त्रुटिप्रवण और समय‑साध्य होता है। इस ट्यूटोरियल के अंत तक आपके पास एक सिंगल, पुन: उपयोग योग्य C# स्निपेट होगा जो:

* फ़ॉन्ट‑वैरिएशन सिलेक्टर्स के साथ एम्बेडेड फ़ॉन्ट्स के साथ वर्कबुक को SVG फ़ाइल के रूप में सेव करता है।  
* वही वर्कबुक को PPTX फ़ाइल में एक्सपोर्ट करता है जहाँ चार्ट संपादन योग्य रहता है।  

एकमात्र पूर्वशर्त **Aspose.Cells for .NET** (2024‑x या बाद का) का हालिया संस्करण और Visual Studio 2022 जैसे .NET विकास वातावरण है।

---

## आपको क्या चाहिए  

* .NET 6.0 या बाद का (कोड .NET Framework 4.8 पर भी काम करता है)।  
* Aspose.Cells for .NET NuGet पैकेज (`Install-Package Aspose.Cells`)।  
* एक Excel फ़ाइल (`input.xlsx`) जिसमें कम से कम एक चार्ट हो।  
* आउटपुट डायरेक्टरी में लिखने की अनुमति।  

---

## XLSX को SVG में बदलते समय SVG में फ़ॉन्ट एम्बेड करें  

फ़ॉन्ट एम्बेड करने से यह सुनिश्चित होता है कि SVG किसी भी डिवाइस पर सही ढंग से रेंडर हो, भले ही लक्ष्य सिस्टम में मूल टाइपफ़ेस न हों। `SvgSaveOptions` क्लास दो फ़्लैग प्रदान करती है जो इसे संभव बनाते हैं: `EmbedFonts` और `FontVariationSelectors`।

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;

// Load the workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

// OPTIONAL: Use WRAPCOLS to reshape data before export (demonstrates a formula)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)"; // 2 columns per wrap
sheet.Calculate(); // Force calculation so the formula result appears

// Configure SVG options to embed fonts
SvgSaveOptions svgOptions = new SvgSaveOptions
{
    EmbedFonts = true,                // embed fonts in the SVG
    FontVariationSelectors = true    // include variation selectors for better Unicode handling
};

// Save the workbook as an SVG file
string svgPath = @"YOUR_DIRECTORY\WithFonts.svg";
workbook.Save(svgPath, svgOptions);
```

**यह क्यों काम करता है:**  
* `EmbedFonts = true` फ़ॉन्ट फ़ाइलों को SVG के `<defs>` सेक्शन में कॉपी कर देता है, जिससे बाहरी निर्भरताएँ समाप्त हो जाती हैं।  
* `FontVariationSelectors = true` उन फ़ॉन्ट्स के लिए आवश्यक सिलेक्टर्स जोड़ता है जो OpenType फीचर्स को सपोर्ट करते हैं, जैसे लिगेचर जैसी ग्लिफ़ वैरिएशन को संरक्षित करता है।  

**अपेक्षित परिणाम:** `WithFonts.svg` को किसी भी आधुनिक ब्राउज़र में खोलें; चार्ट या सेल्स के भीतर का टेक्स्ट Excel में उपयोग किए गए बिल्कुल वही टाइपफ़ेस दिखाएगा, भले ही मशीन पर वह फ़ॉन्ट इंस्टॉल न हो।

---

## Excel चार्ट को PowerPoint में एक्सपोर्ट करें, साथ ही संपादन योग्य चार्ट रखें  

जब आपको एक चार्ट को PowerPoint स्लाइड में एम्बेड करना हो लेकिन प्राप्तकर्ता को चार्ट डेटा संपादित करने की अनुमति भी देनी हो, तो Aspose.Cells का `PptxSaveOptions` `ExportEditableChart` फ़्लैग प्रदान करता है।

```csharp
// Configure PPTX options to keep charts editable after export
PptxSaveOptions pptxOptions = new PptxSaveOptions
{
    ExportEditableChart = true   // allow chart editing in PowerPoint
};

// Save the same workbook as a PPTX file
string pptxPath = @"YOUR_DIRECTORY\EditableChart.pptx";
workbook.Save(pptxPath, pptxOptions);
```

**यह क्यों महत्वपूर्ण है:**  
`ExportEditableChart` को `true` सेट करने से चार्ट को एक स्थैतिक इमेज़ की बजाय Office Open XML चार्ट ऑब्जेक्ट के रूप में स्टोर किया जाता है। जब आप PowerPoint में `EditableChart.pptx` खोलते हैं, तो आप चार्ट पर राइट‑क्लिक → **Edit Data** करके डेटा सीरीज़ को मूल PowerPoint चार्ट की तरह संशोधित कर सकते हैं।

**वेरिफ़िकेशन स्टेप्स:**  

1. PowerPoint में `EditableChart.pptx` खोलें।  
2. चार्ट वाले स्लाइड को locate करें।  
3. **Chart Tools → Design → Edit Data** चुनें।  
4. पुष्टि करें कि Excel‑स्टाइल डेटा ग्रिड दिखाई देता है और आप मान बदल सकते हैं।

---

## XLSX को SVG में बदलें – संपूर्ण वर्कफ़्लो सारांश  

नीचे एक कॉम्पैक्ट संस्करण है जो लोडिंग, वैकल्पिक डेटा मैनिपुलेशन, और SVG के रूप में सेविंग को मिलाता है। जब आपको केवल SVG आउटपुट चाहिए, तब इसका उपयोग करें।

```csharp
public void ConvertXlsxToSvg(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Example: apply a formula to demonstrate cell calculations
    Worksheet ws = wb.Worksheets[0];
    ws.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
    ws.Calculate();

    SvgSaveOptions opts = new SvgSaveOptions
    {
        EmbedFonts = true,
        FontVariationSelectors = true
    };

    wb.Save(outputPath, opts);
}
```

मेथड को इस प्रकार कॉल करें:

```csharp
ConvertXlsxToSvg(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.svg");
```

**एज केस टिप:** यदि आपके वर्कबुक में कस्टम फ़ॉन्ट्स हैं जो सर्वर पर इंस्टॉल नहीं हैं, तो `Save` कॉल करने से पहले उन्हें मैन्युअली एम्बेड करें। `FontInfoCollection` का उपयोग करके फ़ॉन्ट फ़ाइलों को `SvgSaveOptions` के `CustomFonts` प्रॉपर्टी (नए Aspose.Cells रिलीज़ में उपलब्ध) में जोड़ें।

---

## XLSX को PPTX में बदलें – चार्ट की संपादन योग्यता बनाए रखें  

निम्नलिखित हेल्पर मेथड **XLSX को PPTX** बदलने का मार्ग दर्शाता है जबकि यह सुनिश्चित करता है कि चार्ट संपादन योग्य रहे।

```csharp
public void ConvertXlsxToPptx(string inputPath, string outputPath)
{
    Workbook wb = new Workbook(inputPath);

    // Ensure any chart you want to keep editable is on the first worksheet
    // (Aspose.Cells exports only the first worksheet by default for PPTX)
    PptxSaveOptions opts = new PptxSaveOptions
    {
        ExportEditableChart = true
    };

    wb.Save(outputPath, opts);
}
```

उपयोग:

```csharp
ConvertXlsxToPptx(@"YOUR_DIRECTORY\input.xlsx", @"YOUR_DIRECTORY\Result.pptx");
```

**सामान्य प्रश्न:** *यदि मेरे वर्कबुक में कई वर्कशीट्स हैं जिनमें चार्ट्स हैं तो क्या होगा?*  
**उत्तर:** Aspose.Cells डिफ़ॉल्ट रूप से पहले वर्कशीट को एक्सपोर्ट करता है। अतिरिक्त शीट्स को शामिल करने के लिए `workbook.Worksheets` पर इटरेट करें, प्रत्येक चार्ट को नई स्लाइड पर कॉपी करें, और Aspose.Slides के `Presentation` ऑब्जेक्ट्स का उपयोग करके प्रत्येक स्लाइड को अलग‑अलग सेव करें। यह उन्नत परिदृश्य बुनियादी “वर्कबुक को SVG के रूप में सेव” और “Excel चार्ट को PowerPoint में एक्सपोर्ट” फ्लो से परे है, लेकिन कोर फ़्लैग वही रहते हैं।

---

## व्यावहारिक टिप्स और संभावित समस्याएँ  

* **परफ़ॉर्मेंस:** फ़ॉन्ट एम्बेड करने से SVG फ़ाइल का आकार बढ़ जाता है। यदि आकार की चिंता है, तो `EmbedFonts = false` सेट करें और वेब‑सेफ़ फ़ॉन्ट्स पर निर्भर रहें।  
* **फ़ॉन्ट लाइसेंसिंग:** सुनिश्चित करें कि आप जिन फ़ॉन्ट्स को एम्बेड कर रहे हैं, उनके पास एम्बेड करने का अधिकार है; कुछ कमर्शियल फ़ॉन्ट्स एम्बेडिंग को प्रतिबंधित करते हैं।  
* **चार्ट संगतता:** संपादन योग्य चार्ट्स PPTX के अंदर `chart.xml` पार्ट्स के रूप में सेव होते हैं। बहुत जटिल चार्ट्स (जैसे 3‑D या कॉम्बो चार्ट्स) PowerPoint में एडिट करते समय कुछ स्टाइलिंग खो सकते हैं। सबसे सामान्य चार्ट टाइप्स का परीक्षण करें।  
* **वर्ज़न मिसमैच:** `ExportEditableChart` फ़्लैग को Aspose.Cells 20.10 या बाद के संस्करण की आवश्यकता होती है। पुराने संस्करण में यह स्वचालित रूप से रास्टर इमेज़ में फॉल्बैक हो जाता है।  
* **थ्रेड सेफ़्टी:** Workbook ऑब्जेक्ट थ्रेड‑सेफ़ नहीं होते। वेब सर्विस परिदृश्य में प्रत्येक रिक्वेस्ट के लिए नया `Workbook` इंस्टेंस बनाएं।  

---

## पूर्ण एंड‑टू‑एंड उदाहरण  

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

class ExcelExportDemo
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputFile = @"YOUR_DIRECTORY\input.xlsx";
        string svgFile   = @"YOUR_DIRECTORY\WithFonts.svg";
        string pptxFile  = @"YOUR_DIRECTORY\EditableChart.pptx";

        // 1. Load workbook
        Workbook workbook = new Workbook(inputFile);

        // 2. Optional: reshape data using WRAPCOLS
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].Formula = "=WRAPCOLS({1,2,3,4,5},2)";
        sheet.Calculate();

        // 3. Save as SVG with embedded fonts
        SvgSaveOptions svgOpts = new SvgSaveOptions
        {
            EmbedFonts = true,
            FontVariationSelectors = true
        };
        workbook.Save(svgFile, svgOpts);
        Console.WriteLine($"SVG saved with embedded fonts to: {svgFile}");

        // 4. Save as PPTX with editable chart
        PptxSaveOptions pptxOpts = new PptxSaveOptions
        {
            ExportEditableChart = true
        };
        workbook.Save(pptxFile, pptxOpts);
        Console.WriteLine($"PPTX saved with editable chart to: {pptxFile}");
    }
}
```

इस प्रोग्राम को चलाने पर दो फ़ाइलें बनेंगी:

* **WithFonts.svg** – एक SVG जो Excel व्यू की तरह ही रेंडर होता है, फ़ॉन्ट्स सहित।  
* **EditableChart.pptx** – एक PowerPoint प्रेज़ेंटेशन जहाँ चार्ट को सीधे एडिट किया जा सकता है।

---

## निष्कर्ष  

अब आप जानते हैं कि **XLSX को SVG में बदलते समय SVG में फ़ॉन्ट एम्बेड** कैसे करें, और **Excel चार्ट को PowerPoint में एक्सपोर्ट** करते समय चार्ट को संपादन योग्य कैसे रखें। वही कोड यह भी दर्शाता है कि कैसे **वर्कबुक को SVG के रूप में सेव** करें और **XLSX को PPTX में बदलें** न्यूनतम प्रयास के साथ।  

अब आप आगे के विषयों का अन्वेषण कर सकते हैं, जैसे:

* प्रोग्रामेटिक रूप से कस्टम फ़ॉन्ट्स जोड़ना (`svgOptions.CustomFonts`)।  
* बैकग्राउंड सर्विस में कई वर्कबुक्स को बैच‑प्रोसेस करना।  
* Aspose.Slides का उपयोग करके कई Excel चार्ट्स को मिलाकर मल्टी‑स्लाइड PPTX फ़ाइल बनाना।  

विकल्पों के साथ प्रयोग करें, स्निपेट्स को अपने प्रोजेक्ट में अनुकूलित करें, और मैनुअल पोस्ट‑प्रोसेसिंग के बिना भरोसेमंद Excel‑to‑SVG/PPTX कन्वर्ज़न का आनंद लें। Happy coding!

## आगे क्या सीखें?  

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/german/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [Convert Excel Chart To Svg Aspose Cells Net](/cells/french/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}