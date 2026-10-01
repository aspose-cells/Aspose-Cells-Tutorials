---
category: general
date: 2026-10-01
description: C# का उपयोग करके एक्सेल में वैकल्पिक कॉलम रंग – DataTable से Excel फ़ाइल
  बनाना सीखें, C# में सेल बैकग्राउंड रंग सेट करें, और स्टाइल किए हुए कॉलमों के साथ
  DataTable को Excel में इम्पोर्ट करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: hi
lastmod: 2026-10-01
og_description: एक्सेल में वैकल्पिक कॉलम रंग बनाना आसान। इस गाइड का पालन करें ताकि
  आप DataTable से एक Excel फ़ाइल बना सकें, C# में सेल बैकग्राउंड रंग सेट कर सकें,
  और स्टाइल्ड कॉलम के साथ DataTable को Excel में इम्पोर्ट कर सकें।
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: C# के साथ Excel में वैकल्पिक कॉलम रंग जोड़ें – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: C# का उपयोग करके Excel में वैकल्पिक कॉलम रंग कैसे जोड़ें
url: /hi/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# का उपयोग करके Excel में वैकल्पिक कॉलम रंग कैसे जोड़ें

यदि आपको अपने एप्लिकेशन से जेनरेट किए गए रिपोर्ट में **alternating column colors excel** चाहिए, तो यह गाइड एक पूर्ण समाधान दिखाती है। आप देखेंगे कि कैसे `DataTable` से Excel फ़ाइल बनाते हैं, सेल बैकग्राउंड कलर C# स्टाइल में सेट करते हैं, और प्रत्येक कॉलम पर अलग‑अलग स्टाइल लागू करते हुए datatable को Excel में इम्पोर्ट करते हैं।

यह ट्यूटोरियल वह सब कवर करता है जिसकी आपको आवश्यकता है: आवश्यक NuGet पैकेज, एक पूर्ण, रन‑एबल कोड सैंपल, और प्रत्येक चरण के महत्व की व्याख्याएँ। अंत में आपके पास एक स्टाइल्ड वर्कबुक होगी जिसे सीधे Microsoft Excel में खोला जा सकता है।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास ये हैं:

* .NET 6.0 (या बाद का) SDK स्थापित  
* Visual Studio 2022 (या कोई भी C#‑compatible IDE)  
* **Aspose.Cells for .NET** लाइब्रेरी – इसे स्थापित करें  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells उदाहरण में उपयोग किए गए `Workbook`, `Worksheet`, `Style`, और `BackgroundType` क्लासेस प्रदान करता है।

## Step 1: Retrieve the source data as a `DataTable`

पहला कार्य वह डेटा प्राप्त करना है जिसे आप एक्सपोर्ट करना चाहते हैं। वास्तविक प्रोजेक्ट्स में आप `DataTable` को डेटाबेस क्वेरी, API कॉल, या किसी भी इन‑मे़मोरी कलेक्शन से भर सकते हैं।

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Why this matters:**  
`DataTable` एक यूनिवर्सल कंटेनर है जो Excel वर्कशीट में साफ़‑साफ़ मैप हो जाता है। `DataTable` का उपयोग करके आप **create excel file from datatable c#** बिना प्रत्येक कॉलम के लिए कस्टम लूप लिखे बना सकते हैं।

## Step 2: Create a new workbook and get its first worksheet

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Explanation:**  
`Workbook` रूट ऑब्जेक्ट है; `Worksheets[0]` आपको डिफ़ॉल्ट शीट देता है जहाँ डेटा रखा जाएगा।

## Step 3: Prepare a distinct style for each column (alternating background colors)

**alternating column colors excel** प्राप्त करने के लिए, हम प्रत्येक कॉलम के लिए एक `Style` बनाते हैं और दो शेड्स के बीच बदलते हुए हल्के बैकग्राउंड कलर असाइन करते हैं।

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Why we use a loop:**  
लूप यह सुनिश्चित करता है कि **set cell background color c#** लगातार लागू हो, चाहे रन‑टाइम पर कॉलम की संख्या बदल भी जाए। इससे समाधान डायनामिक रिपोर्ट्स के लिए मजबूत बनता है।

## Step 4: Import the `DataTable` into the worksheet, applying the column styles

Aspose.Cells सीधे `DataTable` को इम्पोर्ट कर सकता है, और हम स्टाइल्स की एरे पास करके प्रत्येक कॉलम को रंग सकते हैं।

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**What happens under the hood:**  
`ImportDataTable` हेडर रो लिखता है, फिर प्रत्येक डेटा रो। क्योंकि हमने `columnStyles` प्रदान किए हैं, किसी भी कॉलम की हर सेल को संबंधित स्टाइल मिल जाता है, जिससे वांछित वैकल्पिक रंग प्राप्त होते हैं।

## Step 5: Save the styled workbook to a file

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

जब आप *StyledTable.xlsx* को Excel में खोलेंगे तो प्रत्येक कॉलम वैकल्पिक रूप से शेडेड दिखेगा, जिससे टेबल पढ़ने में आसान हो जाएगी।

## Full, runnable example

सभी हिस्सों को मिलाकर, यहाँ एक स्व-निहित प्रोग्राम है जिसे आप कॉपी, पेस्ट और रन कर सकते हैं।

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Expected output

* `C:\Temp\` पर स्थित **StyledTable.xlsx** नाम की फ़ाइल।  
* वर्कशीट में तीन कॉलम (`Id`, `Name`, `Score`) वैकल्पिक बैकग्राउंड कलर के साथ दिखेंगे: कॉलम 1 और 3 *LightYellow* में, कॉलम 2 *LightCyan* में।  
* `DataTable` की सभी रो हेडर रो के नीचे दिखाई देंगी।

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| *Can I use other colors?* | हाँ। `System.Drawing.Color.LightYellow` और `LightCyan` को किसी भी `System.Drawing.Color` वैल्यू से बदल दें। |
| *What if the DataTable has many columns?* | लूप स्वचालित रूप से प्रत्येक कॉलम के लिए एक स्टाइल बनाता है, इसलिए पैटर्न कोड में बदलाव के बिना स्केल करता है। |
| *Do I need to dispose of the workbook?* | Aspose.Cells `IDisposable` को इम्प्लीमेंट करता है। यदि आप `Workbook` को `using` ब्लॉक में रैप करते हैं, तो रिसोर्सेज तुरंत रिलीज़ हो जाते हैं। |
| *How to apply the same alternating colors to rows instead of columns?* | रो के लिए `Style[]` बनाएं और `worksheet.Cells.ImportDataTable(..., rowStyles)` कॉल करें – Aspose.Cells ओवरलोड दोनों को सपोर्ट करता है। |
| *Can I write the file directly to a stream (e.g., for a web API)?* | हाँ। `workbook.Save(stream, SaveFormat.Xlsx);` का उपयोग फ़ाइल पाथ की बजाय करें। |

## Tips from the field

* **Pro tip:** यदि आप एक ही रन में कई वर्कशीट्स जनरेट करते हैं तो स्टाइल ऑब्जेक्ट्स को कैश करें – स्टाइल बनाना अपेक्षाकृत सस्ता है, लेकिन उन्हें री‑यूज़ करने से मेमोरी चर्न कम होता है।  
* **Watch out for:** `System.Drawing.Color` को नॉन‑Windows प्लेटफ़ॉर्म पर उपयोग करने के लिए `System.Drawing.Common` NuGet पैकेज जोड़ें और सुनिश्चित करें कि रन‑टाइम GDI+ को सपोर्ट करता है।

## Conclusion

अब आप जानते हैं कि **alternating column colors excel** कैसे प्राप्त करें, `DataTable` से C# में Excel फ़ाइल बनाकर, Aspose.Cells के साथ सेल बैकग्राउंड कलर सेट करके, और **import datatable to excel** को स्टाइल्ड कॉलम एरे के साथ कैसे इम्पोर्ट करें। यह तरीका तेज़, मेंटेन करने योग्य, और किसी भी आकार के डेटा सेट के साथ काम करता है।

### Next steps

* **set cell background color c#** को कंडीशनल फ़ॉर्मेटिंग (जैसे, कम स्कोर को हाईलाइट करना) के लिए एक्सप्लोर करें।  
* इस तकनीक को **create excel file from datatable c#** के साथ मिलाकर मल्टी‑शीट रिपोर्ट बनाएं।  
* उसी वर्कबुक में विज़ुअल सारांश जोड़ने के लिए Aspose.Cells की चार्टिंग API देखें।

रंग, फ़ाइल फ़ॉर्मेट, या डेटा स्रोत को अपने प्रोजेक्ट की ज़रूरतों के अनुसार बदलें। Happy coding!

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Set Column Background in Excel with C# – Complete Guide](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Add background color excel – Alternating Row Styles in C#](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Create Workbook C# – Import DataTable to Excel with Styles](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}