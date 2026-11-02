---
category: general
date: 2026-07-03
description: C# का उपयोग करके डेटाटेबल को Excel में इम्पोर्ट करते समय वैकल्पिक पंक्तियों
  के रंग लागू करें। जानें कि C# डेटाटेबल को Excel में कैसे एक्सपोर्ट करें, स्टाइल्ड
  टेबल Excel को कैसे सहेजें, और वर्कबुक फ़ॉर्मेटिंग को कैसे बनाए रखें।
draft: false
keywords:
- apply alternating row colors
- import datatable to excel
- export c# datatable to excel
- save styled table excel
- save workbook with formatting
language: hi
og_description: C# का उपयोग करके Excel में वैकल्पिक पंक्तियों के रंग लागू करें। यह
  ट्यूटोरियल दिखाता है कि कैसे डेटाटेबल को Excel में इम्पोर्ट करें, C# डेटाटेबल को
  Excel में एक्सपोर्ट करें, और फ़ॉर्मेटिंग के साथ वर्कबुक को सहेजें।
og_title: C# के साथ Excel में वैकल्पिक पंक्तियों के रंग लागू करें – पूर्ण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  headline: Apply Alternating Row Colors in Excel with C# – Complete Guide
  type: TechArticle
- description: Apply alternating row colors while you import datatable to Excel using
    C#. Learn how to export C# datatable to Excel, save styled table excel, and keep
    workbook formatting.
  name: Apply Alternating Row Colors in Excel with C# – Complete Guide
  steps:
  - name: Expected Output
    text: '| ID | Name | Department | HireDate | |----|---------|------------|------------|
      | 1 | Alice | Finance | 15‑01‑2020 | | 2 | Bob | HR | 23‑06‑2019 | | 3 | Charlie
      | IT | 10‑03‑2021 | | 4 | Diana | Marketing | 05‑11‑2018 |'
  - name: What if my DataTable has thousands of rows?
    text: The `ImportDataTable` method streams data efficiently, but you might hit
      memory limits on very large tables. In such cases, consider splitting the export
      into multiple worksheets or using the `ImportDataTable` overload that lets you
      specify a start row and column.
  - name: Can I use custom colors instead of the built‑in ones?
    text: Absolutely. Just replace the `ForegroundColor` assignments in `styleWhite`
      and `styleGray` with any `System.Drawing.Color` you prefer—think pastel blues
      or corporate brand colors.
  - name: How do I ensure the alternating style works when the user adds rows later?
    text: If users edit the file manually, the original style array won’t automatically
      extend. A quick workaround is to convert the range into an Excel Table (`ListObject`)
      after import; Excel then repeats the pattern for new rows.
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataExport
title: C# के साथ Excel में वैकल्पिक पंक्तियों के रंग लागू करें – पूर्ण गाइड
url: /hi/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-excel-with-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# के साथ Excel में वैकल्पिक पंक्तियों के रंग लागू करें – पूर्ण गाइड

क्या आपको कभी C# `DataTable` को Excel में एक्सपोर्ट करते समय **वैकल्पिक पंक्तियों के रंग लागू** करने की ज़रूरत पड़ी है? आप अकेले नहीं हैं—डेवलपर्स लगातार पूछते रहते हैं कि इन स्प्रेडशीट्स को बिना मैन्युअली Excel में हाथ डालें कैसे परिष्कृत दिखाया जाए। अच्छी खबर? आप इसे प्रोग्रामेटिकली कुछ ही कोड लाइनों में कर सकते हैं।

इस ट्यूटोरियल में हम **import datatable to excel** को समझेंगे, आपको दिखाएंगे कि **export c# datatable to excel** को स्टाइल्ड टेबल के साथ कैसे किया जाए, और अंत में **save styled table excel** को फॉर्मेटिंग बनाए रखते हुए कैसे सेव करें। अंत तक आप **save workbook with formatting** कर पाएँगे जो क्लाइंट मीटिंग के लिए तैयार दिखे।

## Prerequisites

- .NET 6.0 या बाद का संस्करण (उदाहरण में .NET 6 उपयोग किया गया है, लेकिन कोई भी हालिया संस्करण काम करेगा)
- Aspose.Cells for .NET (फ्री ट्रायल या लाइसेंस्ड संस्करण) – यह लाइब्रेरी स्टाइलिंग को बहुत आसान बनाती है
- एक `DataTable` स्रोत (डेटाबेस, CSV, या इन‑मेमोरी कलेक्शन से हो सकता है)

> **Pro tip:** यदि आपके पास अभी तक Aspose.Cells नहीं है, तो आप इसे NuGet से `dotnet add package Aspose.Cells` कमांड से प्राप्त कर सकते हैं।

## Step 1: Set Up the Project and Load Your Data

पहले, एक कंसोल ऐप (या कोई भी C# प्रोजेक्ट) बनाइए और आवश्यक `using` स्टेटमेंट्स जोड़िए। फिर डेटा को `DataTable` में लोड कीजिए। उदाहरण के लिए हम तुरंत एक सरल टेबल जेनरेट करेंगे।

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Retrieve the source data as a DataTable
        DataTable sourceTable = GetSampleData();

        // The rest of the steps follow...
    }

    // Helper that creates a dummy DataTable
    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

**Why this matters:** एक तैयार `DataTable` होने से आप **import datatable to excel** को एक ही कॉल में कर सकते हैं, जिससे मैन्युअल सेल‑बाय‑सेल इन्सर्शन की ज़रूरत नहीं रहती।

## Step 2: Create a Workbook and Define the Alternating Row Styles

अब हम एक नया `Workbook` इंस्टैंशिएट करेंगे। **वैकल्पिक पंक्तियों के रंग लागू** करने का ट्रिक `ImportTableOptions.StyleArray` में है। हम पहले दो बिल्ट‑इन स्टाइल्स (आमतौर पर सफ़ेद और हल्का ग्रे) का उपयोग करेंगे, लेकिन बाद में इन्हें कस्टमाइज़ भी कर सकते हैं।

```csharp
// Step 2: Create a new workbook
Workbook workbook = new Workbook();

// Define two simple styles: white (default) and light gray
Style styleWhite = workbook.Styles[workbook.Styles.Add()];
styleWhite.ForegroundColor = System.Drawing.Color.White;
styleWhite.Pattern = BackgroundType.Solid;

Style styleGray = workbook.Styles[workbook.Styles.Add()];
styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242); // light gray
styleGray.Pattern = BackgroundType.Solid;

// Step 3: Set up ImportTableOptions with the alternating styles
ImportTableOptions importOptions = new ImportTableOptions
{
    // The array alternates between the two styles for each row
    StyleArray = new Style[] { styleWhite, styleGray }
};
```

**Explanation:** `ImportTableOptions` Aspose.Cells को बताता है कि इम्पोर्ट के दौरान प्रत्येक पंक्ति को कैसे ट्रीट किया जाए। दो एंट्रीज़ वाला `StyleArray` प्रदान करने से लाइब्रेरी स्वचालित रूप से हर विषम पंक्ति को पहले स्टाइल और हर सम पंक्ति को दूसरे स्टाइल से रंग देती है—बिल्कुल वही जो आपको **apply alternating row colors** के लिए चाहिए।

## Step 3: Pull the DataTable Into the Worksheet (Including Headers)

वर्कबुक और स्टाइल्स तैयार होने के बाद, हम अब **import datatable to excel** करेंगे। `ImportDataTable` मेथड भारी काम करता है: यह कॉलम हेडर लिखता है, स्टाइल एरे का सम्मान करता है, और डेटा को सेल A1 से शुरू करता है।

```csharp
// Step 4: Import the DataTable into the first worksheet (include column headers)
Worksheet sheet = workbook.Worksheets[0];
sheet.Cells.ImportDataTable(sourceTable, true, importOptions);
```

**Why we include `true` for the second argument:** यह मेथड को बताता है कि कॉलम नामों को पहली पंक्ति में लिखें, जो एक प्रोफ़ेशनल‑लुकिंग रिपोर्ट के लिए आवश्यक है।

## Step 4: Fine‑Tune the Table (Optional but Handy)

यदि आप टेबल को ऑटो‑फ़िट कॉलम्स या फ़िल्टर रो जोड़ना चाहते हैं, तो कुछ अतिरिक्त लाइनों से यह और बेहतर बन जाता है।

```csharp
// Auto‑fit all columns for readability
sheet.AutoFitColumns();

// Add a filter to the header row
sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";
```

ये ट्यूनिंग्स वैकल्पिक रंगों को प्रभावित नहीं करतीं, लेकिन **save styled table excel** फ़ाइल के समग्र उपयोगकर्ता अनुभव को सुधारती हैं।

## Step 5: Save the Workbook While Keeping All Formatting

अंत में, हम फ़ाइल को डिस्क पर लिखते हैं। `Save` मेथड हमने सेट किए गए हर स्टाइल को संरक्षित रखता है, जिससे वैकल्पिक पंक्तियाँ जैसा है वैसी ही रहती हैं।

```csharp
// Step 5: Save the workbook with the styled table
string outputPath = @"C:\Temp\StyledEmployees.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

जब आप `StyledEmployees.xlsx` खोलेंगे, तो आपको एक साफ़ टेबल दिखेगा जहाँ पंक्तियाँ सफ़ेद और हल्के ग्रे के बीच वैकल्पिक रूप से बदलती हैं—बिल्कुल वही विज़ुअल क्यू जो कई उपयोगकर्ता पढ़ने में आसानी के लिए भरोसा करते हैं।

### Expected Output

| ID | Name    | Department | HireDate   |
|----|---------|------------|------------|
| 1  | Alice   | Finance    | 15‑01‑2020 |
| 2  | Bob     | HR         | 23‑06‑2019 |
| 3  | Charlie | IT         | 10‑03‑2021 |
| 4  | Diana   | Marketing  | 05‑11‑2018 |

- Row 1, 3 … → सफ़ेद बैकग्राउंड  
- Row 2, 4 … → हल्का‑ग्रे बैकग्राउंड  

यह पूरी **save workbook with formatting** प्रक्रिया है।

## Common Questions & Edge Cases

### What if my DataTable has thousands of rows?

`ImportDataTable` मेथड डेटा को कुशलता से स्ट्रीम करता है, लेकिन बहुत बड़ी टेबल्स पर मेमोरी लिमिट्स आ सकती हैं। ऐसे मामलों में एक्सपोर्ट को कई वर्कशीट्स में बाँटने या `ImportDataTable` के ओवरलोड का उपयोग करने पर विचार करें जो आपको स्टार्ट रो और कॉलम निर्दिष्ट करने देता है।

### Can I use custom colors instead of the built‑in ones?

बिल्कुल। बस `styleWhite` और `styleGray` में `ForegroundColor` असाइनमेंट को अपनी पसंद के किसी भी `System.Drawing.Color` से बदल दें—जैसे पेस्टल ब्लूज़ या कॉर्पोरेट ब्रांड कलर्स।

```csharp
styleWhite.ForegroundColor = System.Drawing.Color.LightBlue;
styleGray.ForegroundColor = System.Drawing.Color.LightCyan;
```

### How do I ensure the alternating style works when the user adds rows later?

यदि उपयोगकर्ता फ़ाइल को मैन्युअली एडिट करते हैं, तो मूल स्टाइल एरे स्वचालित रूप से विस्तारित नहीं होगा। एक तेज़ समाधान यह है कि इम्पोर्ट के बाद रेंज को एक Excel Table (`ListObject`) में बदल दें; Excel तब नए रो के लिए पैटर्न को दोहराता है।

```csharp
int lastRow = sheet.Cells.MaxDataRow;
int lastCol = sheet.Cells.MaxDataColumn;
string tableRange = $"A1:{CellsHelper.ColumnIndexToName(lastCol)}{lastRow + 1}";
ListObject table = sheet.ListObjects[sheet.ListObjects.Add(tableRange, true)];
```

अब कोई भी नई पंक्ति वैकल्पिक रंगों को विरासत में लेती है।

## Full Working Example (All Steps in One Place)

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve source data
        DataTable sourceTable = GetSampleData();

        // 2️⃣ Create workbook and define alternating styles
        Workbook workbook = new Workbook();

        Style styleWhite = workbook.Styles[workbook.Styles.Add()];
        styleWhite.ForegroundColor = System.Drawing.Color.White;
        styleWhite.Pattern = BackgroundType.Solid;

        Style styleGray = workbook.Styles[workbook.Styles.Add()];
        styleGray.ForegroundColor = System.Drawing.Color.FromArgb(242, 242, 242);
        styleGray.Pattern = BackgroundType.Solid;

        ImportTableOptions importOptions = new ImportTableOptions
        {
            StyleArray = new Style[] { styleWhite, styleGray }
        };

        // 3️⃣ Import DataTable (including headers)
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(sourceTable, true, importOptions);

        // 4️⃣ Optional polish
        sheet.AutoFitColumns();
        sheet.AutoFilter.Range = $"A1:{CellsHelper.ColumnIndexToName(sourceTable.Columns.Count - 1)}1";

        // 5️⃣ Save the styled workbook
        string outputPath = @"C:\Temp\StyledEmployees.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Employees");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Department", typeof(string));
        table.Columns.Add("HireDate", typeof(DateTime));

        table.Rows.Add(1, "Alice", "Finance", new DateTime(2020, 1, 15));
        table.Rows.Add(2, "Bob", "HR", new DateTime(2019, 6, 23));
        table.Rows.Add(3, "Charlie", "IT", new DateTime(2021, 3, 10));
        table.Rows.Add(4, "Diana", "Marketing", new DateTime(2018, 11, 5));

        return table;
    }
}
```

प्रोग्राम चलाएँ, जेनरेट की गई फ़ाइल खोलें, और आप तुरंत वैकल्पिक रंग लागू होते देखेंगे—कोई मैन्युअल फॉर्मेटिंग नहीं चाहिए।

## Conclusion

हमने अभी दिखाया कि कैसे **apply alternating row colors** किया जाता है जब आप C# का उपयोग करके **import datatable to excel** करते हैं। यह प्रक्रिया वह सब कवर करती है जो आपको **export c# datatable to excel**, **save styled table excel**, और **save workbook with formatting** करने के लिए चाहिए, जिससे आउटपुट प्रोफ़ेशनल दिखे।

अगले कदम? दो स्टाइल्स को बदलकर एक कस्टम थीम बनाएँ, या रेंज को Excel Table में बदलें ताकि उपयोगकर्ता सॉर्ट और फ़िल्टर कर सकें जबकि रंग पैटर्न बना रहे। आप `ConditionalFormattingCollection` के ज़रिए कंडीशनल फॉर्मेटिंग भी एक्सप्लोर कर सकते हैं अधिक डायनेमिक विज़ुअल क्यूज़ के लिए।

Got a twist

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [Apply Colors & Backgrounds in Excel using Aspose.Cells for .NET](/cells/english/net/formatting/colors-and-background/)
- [Automate Excel Theme Colors Using Aspose.Cells .NET for Efficient Formatting](/cells/english/net/formatting/automate-excel-theme-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}