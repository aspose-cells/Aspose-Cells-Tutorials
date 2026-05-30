---
category: general
date: 2026-05-30
description: C# वर्कशीट्स में वैकल्पिक पंक्तियों के रंग कैसे जोड़ें, सेल बैकग्राउंड
  को सॉलिड फ़िल पैटर्न से सेट करें, और वर्कशीट सेल स्टाइल को आसानी से कस्टमाइज़ करें।
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: hi
og_description: C# वर्कशीट्स में वैकल्पिक पंक्तियों के रंग आसानी से सेट करें। सेल
  बैकग्राउंड सेट करना सीखें, सॉलिड फ़िल पैटर्न का उपयोग करें, और वर्कशीट सेल स्टाइल
  में महारत हासिल करें।
og_title: C# वर्कशीट्स में वैकल्पिक पंक्तियों के रंग – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: C# वर्कशीट्स में वैकल्पिक पंक्तियों के रंग – पूर्ण मार्गदर्शिका
url: /hi/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# वर्कशीट्स में वैकल्पिक पंक्ति रंग – पूर्ण गाइड

क्या आपने कभी सोचा है कि **वैकल्पिक पंक्ति रंग** का उपयोग करके अपने Excel निर्यात को अधिक परिष्कृत कैसे बनाया जाए? आप अकेले नहीं हैं—डेवलपर्स लगातार पूछते रहते हैं कि पंक्तियों में *पृष्ठभूमि रंग* कैसे जोड़ा जाए बिना लाखों पंक्तियों के कोड लिखे।  

इस ट्यूटोरियल में हम एक सरल तरीका देखेंगे जिससे आप प्रत्येक पंक्ति पर **सेल बैकग्राउंड सेट** कर सकते हैं, **सॉलिड फ़िल पैटर्न** लागू कर सकते हैं, और **वर्कशीट सेल स्टाइल** को नियंत्रित कर सकते हैं ताकि परिणाम पढ़ने योग्य और दृश्य रूप से आकर्षक हो।

## आप क्या सीखेंगे

- डेटा को `DataTable` में प्राप्त करें (या किसी भी तालिका स्रोत में)।  
- दो रंगों के बीच वैकल्पिक होने वाले `Style` ऑब्जेक्ट्स की एक एरे बनाएं।  
- `DataTable` को वर्कशीट में आयात करें और साथ ही उन शैलियों को लागू करें।  
- आउटपुट की जाँच करें और आवश्यकता अनुसार रंग या पैटर्न को समायोजित करें।  

.NET वातावरण और एक स्प्रेडशीट लाइब्रेरी (उदाहरणों में हम **Aspose.Cells** का उपयोग करेंगे) के अलावा कोई बाहरी टूल आवश्यक नहीं है। अंत तक आपके पास एक पुन: उपयोग योग्य मेथड होगा जिसे आप किसी भी रिपोर्टिंग पाइपलाइन में डाल सकते हैं।

---

## चरण 1: स्रोत डेटा को `DataTable` के रूप में प्राप्त करें

सबसे पहले—डेटा के बिना स्टाइल करने को कुछ नहीं है। नीचे एक छोटा हेल्पर दिया गया है जो नमूना पंक्तियों के साथ एक `DataTable` बनाता है। वास्तविक प्रोजेक्ट में आप इसे डेटाबेस कॉल या CSV पार्सर से बदल देंगे।

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **यह क्यों महत्वपूर्ण है:** `DataTable` में डेटा होने से वर्कशीट इंजन इसे एक कॉल में *आयात* कर सकता है, जिससे कॉलम नाम और डेटा प्रकार स्वचालित रूप से संरक्षित रहते हैं।

## चरण 2: **वैकल्पिक पंक्ति रंग** शैलियों को बनाएं

अब हम `Style` ऑब्जेक्ट्स की एक एरे उत्पन्न करेंगे—प्रत्येक पंक्ति के लिए एक—ताकि सम पंक्तियों को हल्का पीला शेड मिले और विषम पंक्तियों को हल्का सियान। यह **वैकल्पिक पंक्ति रंग** तकनीक का मूल है।

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### **Solid Fill Pattern** क्यों उपयोग करें?

`Pattern` प्रॉपर्टी इंजन को बताती है कि रंग कैसे रेंडर किया जाए। एक `Solid` फ़िल यह गारंटी देता है कि पूरे सेल की पृष्ठभूमि रंगी हुई है, जिससे कोई भी हल्की ग्रिडलाइन नहीं दिखती जो अन्यथा दिखाई दे सकती थी। जब आप साफ़ लुक चाहते हैं तो यह **सेल बैकग्राउंड सेट** करने का सबसे सामान्य तरीका है।

## चरण 3: तैयार शैलियों के साथ `DataTable` आयात करें

शैलियों की एरे तैयार होने पर, आयात कॉल एक‑लाइनर बन जाता है। Aspose.Cells स्वचालित रूप से प्रत्येक पंक्ति पर संबंधित शैली लागू करेगा।

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **आंतरिक रूप से क्या होता है?**  
> लाइब्रेरी प्रत्येक पंक्ति पर इटरिट करती है, मानों को सेल्स में कॉपी करती है, और फिर `rowStyles` से मिलती‑जुलती `Style` लागू करती है। क्योंकि हमने पहले ही **सॉलिड फ़िल पैटर्न** परिभाषित किया है, एक पंक्ति के सभी सेल्स समान पृष्ठभूमि रंग विरासत में लेते हैं, जिससे आपको परिपूर्ण **वैकल्पिक पंक्ति रंग** मिलते हैं।

## चरण 4: वर्कबुक सहेजें और परिणाम सत्यापित करें

एक त्वरित सहेजने से आप फ़ाइल को Excel (या किसी भी संगत व्यूअर) में खोल सकते हैं और प्रभाव देख सकते हैं।

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

जब आप फ़ाइल खोलेंगे, पंक्तियाँ 1, 3, 5… हल्का पीला होगा, जबकि पंक्तियाँ 2, 4, 6… हल्का सियान होगा। कॉलम हेडर सफ़ेद रहेंगे, जिससे डेटा उभर कर दिखेगा।

![वैकल्पिक पंक्ति रंग दिखाने वाली वर्कशीट](/images/alternating-row-colors.png "वैकल्पिक पंक्ति रंग वाली वर्कशीट का स्क्रीनशॉट")

*छवि वैकल्पिक पाठ:* **वैकल्पिक पंक्ति रंग** स्क्रीनशॉट एक वर्कशीट का जहाँ प्रत्येक पंक्ति की पृष्ठभूमि हल्के पीले और हल्के सियान के बीच वैकल्पिक होती है।

## चरण 5: आगे अनुकूलन (वैकल्पिक)

### रंग बदलें

यदि आपके ब्रांड में अलग शेड्स उपयोग होते हैं, तो बस `Color.LightYellow` और `Color.LightCyan` को किसी भी `System.Drawing.Color` से बदल दें जो आपको पसंद हो। उदाहरण के लिए:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### अलग **Background Type** उपयोग करें

जबकि `BackgroundType.Solid` सबसे आम है, आप `BackgroundType.Gray125`, `BackgroundType.Horizontal` या लाइब्रेरी द्वारा समर्थित किसी भी पैटर्न के साथ प्रयोग कर सकते हैं। यह दृश्य बनावट को बदलता है जबकि अभी भी **पृष्ठभूमि रंग जोड़ना** संभव बनाता है।

### विशिष्ट कॉलमों पर **Worksheet Cell Style** लागू करें

कभी‑कभी आप केवल डेटा कॉलमों पर वैकल्पिक प्रभाव चाहते हैं, जबकि पहली कॉलम (जैसे IDs) को अपरिवर्तित छोड़ना चाहते हैं। उस कॉलम के लिए एक अलग शैली बनाएं और आयात के बाद उसे असाइन करें:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## निष्कर्ष

अब आपके पास C# वर्कशीट्स में **वैकल्पिक पंक्ति रंग** के लिए एक पूर्ण, पुन: उपयोग योग्य समाधान है। `Style` ऑब्जेक्ट्स की एरे बनाकर, **सॉलिड फ़िल पैटर्न** के साथ **सेल बैकग्राउंड सेट** करके, और एक कॉल में `DataTable` आयात करके, आप न्यूनतम कोड के साथ पेशेवर‑दिखावट वाले रिपोर्ट बना सकते हैं।  

अब आप कर सकते हैं:

- **हेडर पंक्तियों में पृष्ठभूमि रंग** जोड़ें अतिरिक्त जोर के लिए।  
- डायनामिक विज़ुअल संकेतों के लिए इस तकनीक को कंडीशनल फॉर्मेटिंग के साथ मिलाएँ।  
- फ़ॉन्ट, बॉर्डर, या नंबर फ़ॉर्मेट जैसे अन्य **worksheet cell style** गुणों का अन्वेषण करें।

अपने अगले एक्सपोर्ट रूटीन में इसे आज़माएँ—आपके उपयोगकर्ता साफ़, अधिक पढ़ने योग्य स्प्रेडशीट्स के लिए आपका धन्यवाद करेंगे। हैप्पी कोडिंग!

## अगला आप क्या सीखें?

- [Aspose.Cells for .NET के साथ वर्कशीट में पंक्ति ऊँचाई सेट करें](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Aspose.Cells for .NET का उपयोग करके Excel सेल नामों को पंक्ति और कॉलम सूचकांकों में बदलें](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Aspose.Cells .NET का उपयोग करके Excel में वर्कशीट टैब रंग सेट करें - एक व्यापक गाइड](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}