---
category: general
date: 2026-08-14
description: Aspose.Cells का उपयोग करके Excel को PowerPoint में निर्यात करें और कोड
  में Excel फ़ॉर्मूले कैसे गणना करें सीखें। पूर्ण स्रोत के साथ चरण‑दर‑चरण C# उदाहरण।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- calculate excel formulas in code
- Aspose.Cells copy pivot table
- export editable objects pptx
- dynamic array EXPAND function
- C# workbook automation
language: hi
lastmod: 2026-08-14
og_description: Aspose.Cells के साथ Excel को PowerPoint में निर्यात करें और कोड में
  Excel फ़ॉर्मूले गणना करें। कार्यपुस्तिकाओं से संपादन योग्य PPTX फ़ाइलें बनाने के
  लिए इस पूर्ण गाइड का पालन करें।
og_image_alt: Screenshot showing an Excel sheet being exported to a PowerPoint slide
  with editable textboxes
og_title: Aspose.Cells के साथ Excel को PowerPoint में निर्यात करें – पूर्ण C# ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  headline: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  type: TechArticle
- description: Export Excel to PowerPoint using Aspose.Cells and learn how to calculate
    Excel formulas in code. Step‑by‑step C# example with full source.
  name: Export Excel to PowerPoint with Aspose.Cells – complete programming guide
  steps:
  - name: Why this works
    text: '* **`Workbook`** loads the entire Excel file into memory, giving you full
      API access. * **`CopyRange`** with `CopyPivotTable = true` ensures the pivot
      table’s data source, cache, and layout are duplicated exactly—something older
      versions of Aspose.Cells could not do. * Adding a new worksheet (`Copy`'
  - name: Explanation
    text: '* **`WorkbookDesigner`** is a high‑level helper that prepares the workbook
      for export, handling Smart Markers, named ranges, and layout adjustments. *
      Setting `ExportEditableObjects = true` tells Aspose.Cells to translate Excel
      drawings into PowerPoint shapes rather than flattening them into images.'
  - name: Why you might use this
    text: '* **Uniform data type:** Exporting as strings avoids type‑mismatch errors
      when the consumer expects text. * **Custom formatting:** Replace `value.ToString()`
      with any custom formatter (e.g., `value.ToString("yyyy-MM-dd")` for dates).'
  - name: How the calculation engine works
    text: '* The `Formula` property stores the expression exactly as you would type
      it in Excel. * `CalculateFormula()` triggers a full workbook recalculation,
      respecting dependencies between cells. * The `EXPAND` function (available in
      Excel 365) returns a spill range based on the source cell (`B1`) and the s'
  - name: What to verify
    text: '* Open `result.xlsx` in Excel to confirm the pivot table copy, the `EXPAND`
      formula result, and any custom‑exported strings. * Open `output.pptx` in PowerPoint;
      you should see a slide that mirrors the Excel layout, and all charts/textboxes
      should be editable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
- Office 365 functions
title: Aspose.Cells के साथ Excel को PowerPoint में निर्यात करें – पूर्ण प्रोग्रामिंग
  गाइड
url: /hi/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-aspose-cells-complete-progra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells के साथ Excel को PowerPoint में निर्यात करें – पूर्ण प्रोग्रामिंग गाइड

यदि आपको प्रोग्रामेटिक रूप से **Excel को PowerPoint में निर्यात** करना है, तो यह गाइड आपको Aspose.Cells for .NET के साथ इसे कैसे करें, बिल्कुल दिखाता है। आप यह भी सीखेंगे कि **कोड में Excel फ़ॉर्मूले कैसे गणना करें**, पिवट टेबल को परिभाषा खोए बिना कॉपी करें, और डायनामिक एरेज़ के लिए नया Office‑365 EXPAND फ़ंक्शन कैसे उपयोग करें।

इस गाइड में हम एक वास्तविक C# उदाहरण के माध्यम से प्रत्येक पंक्ति के महत्व को समझाएंगे और सामान्य समस्याओं को कवर करेंगे ताकि आप इस समाधान को अपने प्रोजेक्ट्स में अनुकूलित कर सकें।

## इस ट्यूटोरियल में क्या कवर किया गया है

* एक मौजूदा वर्कबुक (`input.xlsx`) लोड करना  
* पिवट टेबल वाले रेंज को उसकी परिभाषा को संरक्षित रखते हुए कॉपी करना  
* वर्कबुक को PowerPoint (`.pptx`) फ़ाइल में निर्यात करना, जिसमें संपादन योग्य टेक्स्टबॉक्स और शैप्स हों  
* कस्टम लॉजिक का उपयोग करके सेल रेंज को स्ट्रिंग्स के रूप में निर्यात करना  
* कोड में Excel फ़ॉर्मूले की गणना करना, जिसमें Office‑365 EXPAND फ़ंक्शन भी शामिल है  
* सभी बदलावों के लागू होने के बाद अंतिम वर्कबुक को सहेजना  

**पूर्वापेक्षाएँ**  
* .NET 6.0 या बाद का (कोड .NET Framework 4.7.2+ के साथ भी काम करता है)  
* Aspose.Cells for .NET v25.11 या नया ( `CopyPivotTable` विकल्प v25.11 में पेश किया गया था)  
* C# और Excel की बुनियादी समझ, जैसे रेंजेज, पिवट टेबल्स, और फ़ॉर्मूले  

> **प्रो टिप:** नवीनतम फीचर्स के साथ अपने प्रोजेक्ट को अद्यतन रखने के लिए NuGet (`Install-Package Aspose.Cells`) के माध्यम से Aspose.Cells इंस्टॉल करें।

## Aspose.Cells के साथ Excel को PowerPoint में निर्यात करें

पहला मुख्य कार्य वर्कबुक को PowerPoint प्रेज़ेंटेशन में बदलना है, जबकि सभी विज़ुअल एलिमेंट्स को संपादन योग्य रखा जाए। यह तब आवश्यक होता है जब आप वित्तीय रिपोर्ट या डैशबोर्ड से स्वचालित रूप से स्लाइड डेक बनाना चाहते हैं।

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;      // ExportTableOptions, ExportOptions, etc.
using Aspose.Cells.Pivot;      // Pivot‑table APIs
using Aspose.Cells.Drawing;    // Shapes, textboxes, etc.

// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Step 2: Copy a range that contains a pivot table (preserves the definition)
Worksheet sourceSheet = workbook.Worksheets["Source"];
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");   // includes a pivot table
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
destinationSheet.Cells.CopyRange(sourceRange, destinationSheet.Cells, new CopyOptions
{
    CopyPivotTable = true   // new option in v25.11
});
```

### यह क्यों काम करता है

* **`Workbook`** पूरे Excel फ़ाइल को मेमोरी में लोड करता है, जिससे आपको पूर्ण API एक्सेस मिलता है।  
* **`CopyRange`** के साथ `CopyPivotTable = true` पिवट टेबल के डेटा स्रोत, कैश, और लेआउट को बिल्कुल डुप्लिकेट करता है—जो पुराने Aspose.Cells संस्करण नहीं कर सकते थे।  
* नया वर्कशीट (`Copy`) जोड़ने से आप मूल शीट को अपरिवर्तित रख सकते हैं, जो ऑडिट ट्रेल्स के लिए उपयोगी है।

## संपादन योग्य ऑब्जेक्ट्स के साथ वर्कबुक को PowerPoint में निर्यात करें

अब हम वर्कबुक को PowerPoint फ़ाइल में बदलते हैं। `ExportEditableObjects` को सक्षम करके हर चार्ट, शैप, या टेक्स्टबॉक्स एक नेटिव PowerPoint ऑब्जेक्ट बन जाता है जिसे उपयोगकर्ता निर्यात के बाद सीधे संपादित कर सकते हैं।

```csharp
// Step 3: Export the workbook to PowerPoint with editable textboxes/shapes
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.Process();   // processes Smart Markers if present
designer.ExportToPptx("YOUR_DIRECTORY/output.pptx", new ExportOptions
{
    ExportEditableObjects = true   // makes objects editable in the PPTX
});
```

### व्याख्या

* **`WorkbookDesigner`** एक हाई‑लेवल हेल्पर है जो वर्कबुक को निर्यात के लिए तैयार करता है, स्मार्ट मार्कर्स, नामित रेंजेज, और लेआउट समायोजन को संभालता है।  
* `ExportEditableObjects = true` सेट करने से Aspose.Cells Excel ड्रॉइंग्स को PowerPoint शैप्स में बदलता है, न कि उन्हें इमेज में फ्लैट करता है। इससे **पूरी तरह से संपादन योग्य** स्लाइड डेक बनता है।  

> **एज केस:** यदि आपके वर्कबुक में बाहरी डेटा कनेक्शन्स से बने जटिल चार्ट हैं, तो `ExportToPptx` कॉल करने से पहले सुनिश्चित करें कि वे कनेक्शन हल हो चुके हैं, अन्यथा चार्ट खाली दिख सकता है।

## कस्टम लॉजिक का उपयोग करके रेंज को स्ट्रिंग्स के रूप में निर्यात करें

कभी-कभी आपको डाउनस्ट्रीम प्रोसेसिंग (जैसे CSV पार्सर को फीड करना) के लिए कच्चे स्ट्रिंग वैल्यूज़ चाहिए होते हैं। `ExportTableOptions` क्लास आपको यह नियंत्रित करने देती है कि प्रत्येक सेल कैसे परिवर्तित हो।

```csharp
// Step 4: Export a range as strings using custom logic
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true,
    CustomExport = (cell, value) => value.ToString()   // simple conversion for each cell
};
workbook.Worksheets[0].Cells.ExportTableAsString(tableOptions, "A1:D10");
```

### आप इसे क्यों उपयोग कर सकते हैं

* **समान डेटा प्रकार:** स्ट्रिंग्स के रूप में निर्यात करने से टाइप‑मिसमैच त्रुटियों से बचा जा सकता है जब उपभोक्ता टेक्स्ट की अपेक्षा करता है।  
* **कस्टम फ़ॉर्मेटिंग:** `value.ToString()` को किसी भी कस्टम फ़ॉर्मेटर से बदलें (उदाहरण के लिए, तिथियों के लिए `value.ToString("yyyy-MM-dd")`)।  

## कोड में Excel फ़ॉर्मूले की गणना करें

एक सामान्य आवश्यकता है **कोड में Excel फ़ॉर्मूले की गणना** करना बिना Excel खोले। Aspose.Cells एक बिल्ट‑इन कैल्कुलेशन इंजन प्रदान करता है जो ऑफ़लाइन काम करता है और नवीनतम Office‑365 फ़ंक्शन, जिसमें `EXPAND` भी शामिल है, को सपोर्ट करता है।

```csharp
// Step 5: Use the new Office‑365 EXPAND function to create a dynamic array
Worksheet firstSheet = workbook.Worksheets[0];
firstSheet.Cells["A1"].Formula = "EXPAND(B1,5,3)";   // expands array starting at B1
workbook.CalculateFormula();   // forces recalculation of the formula
```

### गणना इंजन कैसे काम करता है

* `Formula` प्रॉपर्टी एक्सप्रेशन को ठीक उसी तरह स्टोर करती है जैसा आप Excel में टाइप करेंगे।  
* `CalculateFormula()` पूर्ण वर्कबुक पुनर्गणना को ट्रिगर करता है, सेल्स के बीच निर्भरताओं का सम्मान करते हुए।  
* `EXPAND` फ़ंक्शन (Excel 365 में उपलब्ध) स्रोत सेल (`B1`) और निर्दिष्ट पंक्तियों (`5`) तथा कॉलम (`3`) के आधार पर एक स्पिल रेंज लौटाता है।  

> **टिप:** यदि आपको केवल वर्कबुक के एक हिस्से की गणना करनी है, तो स्कोप को सीमित करने और प्रदर्शन सुधारने के लिए `Worksheet.CalculateFormula()` का उपयोग करें।

## सभी बदलाव लागू करके वर्कबुक को सहेजें

अंत में, संशोधित वर्कबुक को डिस्क पर वापस लिखें। फ़ाइल एक्सटेंशन बदलकर आप किसी भी समर्थित फ़ॉर्मेट (`.xlsx`, `.xls`, `.csv`, आदि) में सहेज सकते हैं।

```csharp
// Step 6: Save the workbook with all changes applied
workbook.Save("YOUR_DIRECTORY/result.xlsx");
```

### क्या सत्यापित करें

* `result.xlsx` को Excel में खोलें और पिवट टेबल कॉपी, `EXPAND` फ़ॉर्मूला परिणाम, और किसी भी कस्टम‑निर्यात स्ट्रिंग्स की पुष्टि करें।  
* `output.pptx` को PowerPoint में खोलें; आपको एक स्लाइड दिखनी चाहिए जो Excel लेआउट को प्रतिबिंबित करती है, और सभी चार्ट/टेक्स्टबॉक्स संपादन योग्य होने चाहिए।

## सामान्य प्रश्न और समस्या निवारण

| प्रश्न | उत्तर |
|----------|--------|
| **क्या मुझे Aspose.Cells उपयोग करने के लिए लाइसेंस चाहिए?** | हाँ। ट्रायल मूल्यांकन के लिए काम करता है, लेकिन पूर्ण लाइसेंस मूल्यांकन वॉटरमार्क हटाता है और `CopyPivotTable` फीचर को अनलॉक करता है। |
| **यदि निर्यात किया गया PPTX खाली शैप्स दिखाता है तो क्या करें?** | सुनिश्चित करें कि वर्कबुक के ड्रॉइंग ऑब्जेक्ट्स छिपे नहीं हैं (`Visible = true`) और निर्यात से पहले सभी बाहरी इमेज लिंक एम्बेडेड हैं। |
| **क्या मैं कई वर्कशीट्स को अलग-अलग PPTX स्लाइड्स में निर्यात कर सकता हूँ?** | `WorkbookDesigner.ExportToPptx` को लूप में उपयोग करें, प्रत्येक वर्कशीट के लिए अलग `ExportOptions` निर्दिष्ट करें, या Aspose.Slides के माध्यम से मैन्युअल रूप से स्लाइड्स जोड़कर उन्हें एक ही प्रेजेंटेशन में संयोजित करें। |
| **क्या `CalculateFormula` थ्रेड‑सेफ है?** | नहीं। गणनाएँ एक ही थ्रेड पर करें या रेस कंडीशन से बचने के लिए प्रत्येक थ्रेड के लिए वर्कबुक को क्लोन करें। |

## निष्कर्ष

आपके पास अब Aspose.Cells का उपयोग करके **Excel को PowerPoint में निर्यात करने के लिए एक पूर्ण, एंड‑टू‑एंड समाधान** है, और आप **कोड में Excel फ़ॉर्मूले की गणना** कैसे करें—आधुनिक `EXPAND` फ़ंक्शन सहित—समझते हैं। इस ट्यूटोरियल में वर्कबुक लोड करना, पिवट टेबल कॉपी करना, संपादन योग्य PowerPoint निर्यात, कस्टम स्ट्रिंग निर्यात, फ़ॉर्मूला गणना, और अंतिम सहेजना शामिल था।

अब आप कर सकते हैं:

* एक्सपोर्ट को विस्तारित करके प्रत्येक वर्कशीट के लिए कई स्लाइड्स शामिल करें (द्वितीयक कीवर्ड: *calculate Excel formulas in code* का उपयोग चार्ट डेटा जनरेट करते समय पुनः किया जा सकता है)।  
* ऐनिमेशन या मास्टर स्लाइड लेआउट जोड़ने के लिए Aspose.Slides को इंटीग्रेट करें।  
* अंतर्राष्ट्रीय प्रोजेक्ट्स के लिए लोकल‑अवेयर फ़ॉर्मेटिंग के साथ साधारण `CustomExport` डेलीगेट को बदलें।  

विभिन्न रेंजेज़ के साथ प्रयोग करने, अन्य Office‑365 फ़ंक्शन (जैसे `FILTER`, `SORT`) का अन्वेषण करने, और इस वर्कफ़्लो को स्वचालित ईमेल डिलीवरी के साथ मिलाकर पूरी तरह से हैंड्स‑ऑफ़ रिपोर्टिंग पाइपलाइन बनाने में संकोच न करें।

---


## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच का अन्वेषण कर सकें।

- [Automate Excel Data Export Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/automation-batch-processing/automate-excel-data-export-aspose-cells-net/)
- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}