---
category: general
date: 2026-11-19
description: C# में सेल नंबर फ़ॉर्मेट सेट करें और जापानी युग की तिथियों के लिए Excel
  तिथि फ़ॉर्मेट कैसे लागू करें, यह सीखें, जिससे विश्वसनीय C# Excel तिथि रूपांतरण संभव
  हो सके।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: hi
lastmod: 2026-11-19
og_description: C# में सेल नंबर फ़ॉर्मेट सेट करें और जापानी युग की तिथियों पर Excel
  तिथि फ़ॉर्मेट लागू करें। सटीक C# Excel तिथि रूपांतरण के लिए इस संपूर्ण गाइड का पालन
  करें।
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: C# में सेल नंबर फ़ॉर्मेट सेट करें और जापानी तिथियों को बदलें – चरण‑दर‑चरण
  गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: C# में सेल नंबर फ़ॉर्मेट सेट करें और जापानी तिथियों को परिवर्तित करें
url: /hi/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# सेल नंबर फ़ॉर्मेट सेट करें और C# में जापानी तिथियों को परिवर्तित करें

यदि आपको C# Excel ऑटोमेशन प्रोजेक्ट में **सेल नंबर फ़ॉर्मेट सेट** करने की आवश्यकता है, तो यह गाइड आपको दिखाता है कि कैसे **Excel डेट फ़ॉर्मेट लागू** किया जाए और जापानी युग तिथियों के लिए **C# Excel डेट कन्वर्ज़न** किया जाए। आपको एक पूर्ण, चलाने योग्य उदाहरण मिलेगा जो Reiwa‑युग स्ट्रिंग (जैसे, `R3/04/01`) को ग्रेगोरियन तिथि `2021‑04‑01` में परिवर्तित करता है।

## आप क्या सीखेंगे

* वर्कबुक बनाना और उसकी पहली वर्कशीट तक पहुंचना।  
* कैसे **सेल नंबर फ़ॉर्मेट सेट** किया जाए ताकि Excel मान को तिथि के रूप में समझे।  
* कैसे **Excel डेट फ़ॉर्मेट लागू** किया जाए जो जापानी युग स्ट्रिंग्स को पहचानता है।  
* कैसे फ़ॉर्मूले पुनः गणना करके **C# Excel डेट कन्वर्ज़न** ट्रिगर किया जाए।  
* अपेक्षित आउटपुट और एज केसों के लिए ट्रबलशूटिंग टिप्स।

**पूर्वापेक्षाएँ**

* .NET 6 या बाद का (कोड .NET Framework 4.6+ के साथ भी काम करता है)।  
* Aspose.Cells for .NET 2024 या नया – NuGet के माध्यम से इंस्टॉल करें: `dotnet add package Aspose.Cells`।  
* C# और Excel डेट हैंडलिंग की बुनियादी परिचितता।

> **प्रो टिप:** Aspose.Cells Microsoft Office स्थापित किए बिना काम करता है, जिससे यह सर्वर‑साइड ऑटोमेशन के लिए आदर्श बनता है।

## Aspose.Cells के साथ C# में सेल नंबर फ़ॉर्मेट सेट करें

पहला कदम Excel को बताना है कि सेल में तिथि है। Excel तिथियों को सीरियल नंबरों के रूप में संग्रहीत करता है, इसलिए हमें लक्ष्य सेल पर एक बिल्ट‑इन डेट नंबर फ़ॉर्मेट (ID 14) लागू करना होगा।

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### यह क्यों काम करता है

* `Style.Number = 14` Excel के *शॉर्ट डेट* फ़ॉर्मेट (`mm/dd/yyyy` डिफ़ॉल्ट) से मेल खाता है।  
* जब सेल में `R3/04/01` जैसी जापानी युग स्ट्रिंग होती है, तो Aspose.Cells का आंतरिक पार्सर युग को पहचानता है और `CalculateFormula()` के दौरान इसे संबंधित ग्रेगोरियन सीरियल नंबर में बदल देता है।  
* गणना के बाद, `StringValue` फ़ॉर्मेटेड ग्रेगोरियन तिथि लौटाता है।

## जापानी युग तिथियों के लिए Excel डेट फ़ॉर्मेट लागू करें

यदि आप सेल को ग्रेगोरियन तिथि के बजाय जापानी युग दिखाना चाहते हैं, तो आप एक कस्टम नंबर फ़ॉर्मेट उपयोग कर सकते हैं जिसमें युग कोड शामिल हो। यह **apply excel date format** क्षमता को दर्शाता है।

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` जापानी लोकैल को लागू करता है।  
* `ggg` युग का नाम दर्शाता है (जैसे, Reiwa के लिए `R`)।  
* लिटरल कैरेक्टर्स (`年`, `月`, `日`) जोड़ने से एक परिचित जापानी तिथि लेआउट बनता है।

### कस्टम फ़ॉर्मेट कब उपयोग करें

* जापानी दर्शकों के लिए तैयार रिपोर्ट्स।  
* जब आपको कानूनी दस्तावेज़ों के लिए मूल युग जानकारी संरक्षित रखनी हो।  
* डैशबोर्ड्स में जहाँ ग्रेगोरियन और युग दोनों तिथियां साथ‑साथ दिखती हैं।

## C# Excel डेट कन्वर्ज़न – जापानी युगों को संभालना

**c# excel date conversion** प्रक्रिया को तीन तार्किक भागों में विभाजित किया जा सकता है:

1. **एरा स्ट्रिंग को पार्स करें** – Aspose.Cells स्वचालित रूप से `R` (Reiwa), `H` (Heisei), `S` (Showa) आदि को पहचानता है।  
2. **सीरियल नंबर में बदलें** – Excel तिथियों को 1899‑12‑30 से दिनों के रूप में संग्रहीत करता है।  
3. **सीरियल नंबर को फ़ॉर्मेट करें** – या तो बिल्ट‑इन फ़ॉर्मेट (ID 14) से या कस्टम जापानी फ़ॉर्मेट से।

### पूर्ण अंत‑से‑अंत उदाहरण

नीचे एक स्व-निहित प्रोग्राम है जो एक ही रन में ग्रेगोरियन और युग दोनों आउटपुट दिखाता है।

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**अपेक्षित कंसोल आउटपुट**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### किनारे के केस और सामान्य समस्याएँ

| Situation                              | What to watch for                                   | Fix / Recommendation                                   |
|----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
| Empty or malformed era string         | `PutValue` लिटरल टेक्स्ट संग्रहीत करता है; रूपांतरण विफल हो जाता है | सेल में लिखने से पहले नियमित अभिव्यक्ति (regex) से इनपुट को मान्य करें। |
| Locale mismatch                        | कस्टम फ़ॉर्मेट पश्चिमी अंकों को दिखाता है, जापानी अक्षरों के बजाय | `Custom` फ़ॉर्मेट में `[$-ja-JP]` शामिल है या `Workbook.Settings.CultureInfo` को `ja-JP` सेट करें, यह सुनिश्चित करें। |
| Workbook contains formulas referencing the date cell | पुनः गणना फ़ॉर्मूला परिणामों को ओवरराइट कर सकती है | `CalculateFormula` को सभी फ़ॉर्मेटिंग चरणों के **बाद** कॉल करें, या यदि आपको त्रुटियों को छोड़ना है तो `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` उपयोग करें। |
| Using older Aspose.Cells versions      | जापानी युग समर्थन 2022 Q3 में जोड़ा गया था | नवीनतम NuGet पैकेज में अपग्रेड करें।                     |

## समाधान का परीक्षण

1. **प्रोग्राम चलाएँ** Visual Studio या `dotnet run` से।  
2. सुनिश्चित करें कि कंसोल ग्रेगोरियन तिथि `2021‑04‑01` और युग स्ट्रिंग `R3年04月01日` प्रिंट करता है।  
3. जनरेटेड वर्कबुक खोलें (यदि आप `wb.Save("Demo.xlsx");` जोड़ते हैं) Microsoft Excel में ताकि सेल्स पर वही फ़ॉर्मेटिंग देखी जा सके।

### ऑटोमेशन टिप

यदि आपको कई एरा तिथियों की बड़ी रेंज प्रोसेस करनी है (जैसे, कॉलम A में कई जापानी तिथियां हैं), तो रूपांतरण लॉजिक को लूप में लपेटें:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

यह तरीका **सेल नंबर फ़ॉर्मेट सेट** ऑपरेशन को तेज़ और मेमोरी‑कुशल रखता है।

## निष्कर्ष

अब आप जानते हैं कि Aspose.Cells का उपयोग करके C# में **सेल नंबर फ़ॉर्मेट सेट** कैसे किया जाता है, जापानी युग स्ट्रिंग्स के लिए **Excel डेट फ़ॉर्मेट लागू** कैसे किया जाता है, और युग से ग्रेगोरियन तिथियों में विश्वसनीय **C# Excel डेट कन्वर्ज़न** कैसे किया जाता है। पूर्ण, चलाने योग्य कोड दोनों आउटपुट दिखाता है और सामान्य किनारे के केसों को उजागर करता है।  

**अगले कदम**

* अन्य बिल्ट‑इन फ़ॉर्मेट IDs का अन्वेषण करें

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [C# में Excel डेट फ़ॉर्मेट सेट करें – पूर्ण चरण‑दर‑चरण गाइड](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Aspose.Cells के साथ Excel में नंबर फ़ॉर्मेट कैसे लागू करें](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [C# में Excel में कस्टम नंबर फ़ॉर्मेट कैसे लागू करें](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}