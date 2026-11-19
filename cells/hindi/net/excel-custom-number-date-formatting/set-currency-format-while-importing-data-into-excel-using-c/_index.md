---
category: general
date: 2026-11-19
description: C# के साथ Excel में मुद्रा स्वरूप सेट करें – सीखें कि Excel वर्कशीट आयात
  के दौरान संख्या स्वरूप और कॉलम की शैली कैसे सेट करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: hi
lastmod: 2026-11-19
og_description: C# के साथ Excel में मुद्रा प्रारूप सेट करें और जानें कि Excel वर्कशीट
  आयात के दौरान संख्या प्रारूप कैसे सेट करें, संख्या प्रारूप असाइन करें, और Excel
  कॉलम को स्टाइल करें।
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: C# के साथ Excel में मुद्रा स्वरूप सेट करें – पूर्ण चरण‑दर‑चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: C# का उपयोग करके डेटा को Excel में आयात करते समय मुद्रा स्वरूप सेट करें
url: /hi/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# का उपयोग करके Excel में डेटा आयात करते समय मुद्रा स्वरूप सेट करें

यदि आपको Excel वर्कशीट में **मुद्रा स्वरूप** सेट करना है, तो यह गाइड आपको **संख्या स्वरूप** सेट करने और **excel worksheet import** करते समय कॉलम्स को स्टाइल करने का तरीका दिखाता है। आप एक पूर्ण, चलाने योग्य उदाहरण देखेंगे जो `DataTable` के प्रत्येक कॉलम को सही संख्या स्वरूप असाइन करता है और वांछित स्टाइलिंग के साथ डेटा आयात करता है।

C# से Excel के साथ काम करना अक्सर केवल कच्चे मानों को डंप करने से अधिक की आवश्यकता रखता है—आपको यह भी नियंत्रित करना पड़ता है कि संख्याएँ कैसे दिखें। चाहे आप इनवॉइस, वित्तीय रिपोर्ट या डैशबोर्ड बना रहे हों, मुद्रा, प्रतिशत या तिथियों को सही ढंग से फॉर्मेट करना आउटपुट को तुरंत पढ़ने योग्य बनाता है।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

* .NET 6.0 (या बाद का) स्थापित हो।
* **Aspose.Cells for .NET** (या कोई भी लाइब्रेरी जो `Style` क्लास के साथ `Number` प्रॉपर्टी प्रदान करती हो) का रेफ़रेंस।  
  *NuGet*: `Install-Package Aspose.Cells`।
* `DataTable` और C# कलेक्शन्स की बुनियादी समझ।
* Visual Studio 2022 या VS Code जैसे IDE।

## Step 1: Retrieve the data to be written to the worksheet

सबसे पहले एक `DataTable` प्राप्त करें जिसमें वह कच्चा डेटा हो जिसे आप एक्सपोर्ट करना चाहते हैं। वास्तविक प्रोजेक्ट्स में यह डेटाबेस क्वेरी, API कॉल या CSV पार्सर से आ सकता है।

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Why this matters:** पूर्ण रूप से भरे हुए `DataTable` को आयात करने से डेटा‑रिट्रीवल लॉजिक को Excel‑जनरेशन लॉजिक से अलग रखा जा सकता है, जिससे टेस्टेबिलिटी और मेंटेनबिलिटी बेहतर होती है।

## Step 2: Create a style array – one entry per column in the DataTable

Aspose.Cells को एक `Style[]` चाहिए जिसकी लंबाई उन कॉलम्स की संख्या के बराबर हो जिन्हें आप आयात करने वाले हैं। प्रत्येक एलेमेंट में एक विशिष्ट संख्या स्वरूप रखा जा सकता है।

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Pro tip:** यदि आपको केवल कुछ कॉलम्स के लिए फॉर्मेटिंग चाहिए, तब भी आपको हर कॉलम के लिए एक `Style` इंस्टेंस बनाना होगा; अन्यथा आयात के दौरान `NullReferenceException` मिलेगा।

## Step 3: Assign number format to the desired columns

बिल्ट‑इन स्टाइल नंबर लाइब्रेरी के अनुसार अलग होते हैं। Aspose.Cells में:

* `0` → General (integer)  
* `2` → Currency (उदा., `$#,##0.00`)  
* `3` → Date, आदि।

यहाँ हम दो कॉलम्स को **संख्या स्वरूप** असाइन कर रहे हैं: पहला कॉलम (Id) को इंटेजर ही रहने दें, जबकि दूसरा कॉलम (Amount) को मुद्रा स्वरूप दें।

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **How to set number format**: `Number` प्रॉपर्टी का उपयोग सबसे तेज़ तरीका है बिल्ट‑इन फॉर्मेट चुनने का। लोकल‑स्पेसिफिक मुद्राओं के लिए, एक कस्टम फॉर्मेट स्ट्रिंग उपयोग करें जिसमें उपयुक्त मुद्रा प्रतीक शामिल हो।

## Step 4: Import the DataTable into the worksheet, applying the column styles

अब जब स्टाइल एरे तैयार है, डेटा आयात करें। `ImportDataTable` मेथड आपके द्वारा पास किए गए स्टाइल्स का सम्मान करता है।

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Expected result

जब आप **FinancialReport.xlsx** खोलेंगे, तो आपको यह दिखेगा:

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

***Amount** कॉलम वह मुद्रा स्वरूप दिखाता है जिसे आपने सेट किया है, जबकि **Id** इंटेजर ही रहता है।*

## How to set number format for additional scenarios

### Assign number format to date columns

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Use custom number formats for percentages

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Styling beyond number formats

आप उसी `Style` ऑब्जेक्ट पर फ़ॉन्ट, बैकग्राउंड रंग या अलाइनमेंट भी सेट कर सकते हैं:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Why this works:** `Style` ऑब्जेक्ट सेल की सभी विज़ुअल प्रॉपर्टीज़ को एकत्रित करता है। जब आप एरे को `ImportDataTable` को पास करते हैं, तो प्रत्येक सेल स्वचालित रूप से परिभाषित स्टाइल को विरासत में लेता है।

## Common pitfalls and how to avoid them

| Pitfall | Symptom | Fix |
|---------|---------|-----|
| प्रत्येक `Style` को इंस्टैंशिएट करना भूल जाना | `NullReferenceException` on import | एरे पर लूप चलाएँ और प्रॉपर्टीज़ सेट करने से पहले `CreateStyle()` कॉल करें। |
| गलत बिल्ट‑इन नंबर इंडेक्स का उपयोग | गलत फॉर्मेट (उदा., तिथियाँ इंटेजर के रूप में दिखें) | सही `Number` कॉन्स्टेंट्स के लिए लाइब्रेरी की डॉक्यूमेंटेशन देखें। |
| वर्कबुक को सेव न करना | कोई आउटपुट फ़ाइल नहीं या खाली फ़ाइल | आयात पूरा होने के बाद `workbook.Save(...)` कॉल करें। |
| मुद्रा प्रतीक के लिए लोकल मिसमैच | `$` गैर‑US लोकल में भी दिखता है | उपयुक्त प्रतीक के साथ कस्टम फॉर्मेट स्ट्रिंग उपयोग करें (उदा., `"€#,##0.00"`). |

## Full, runnable example



## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Create excel file c# – style cells and set currency format](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [How to Format Excel Columns in C# – Complete Guide](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}