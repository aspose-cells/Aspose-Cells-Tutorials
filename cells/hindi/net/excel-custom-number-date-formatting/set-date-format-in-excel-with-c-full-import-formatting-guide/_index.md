---
category: general
date: 2026-06-17
description: C# का उपयोग करके Excel में तिथि फ़ॉर्मेट सेट करें और साथ ही सेल की पृष्ठभूमि
  सेट करें, फ़ोरग्राउंड रंग लागू करें, तथा आयात के दौरान Excel कॉलम को रंगें। चरण‑दर‑चरण
  सीखें।
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: hi
og_description: C# के साथ Excel में तिथि फ़ॉर्मेट सेट करें, साथ ही सेल की पृष्ठभूमि
  सेट करें, अग्रभूमि रंग लागू करें, और आयात के दौरान Excel कॉलम को रंगें। पूर्ण ट्यूटोरियल।
og_title: C# के साथ Excel में तिथि स्वरूप सेट करें – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: C# के साथ Excel में तिथि फ़ॉर्मेट सेट करें – पूर्ण आयात फ़ॉर्मेटिंग गाइड
url: /hi/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# के साथ Excel में तिथि प्रारूप सेट करें – पूर्ण आयात फ़ॉर्मेटिंग गाइड

क्या आपको कभी C# कोड से उत्पन्न Excel शीट में **तिथि प्रारूप सेट** करने की जरूरत पड़ी है, लेकिन साथ ही कॉलम को कस्टम बैकग्राउंड या टेक्स्ट रंग देना भी चाहते थे? आप अकेले नहीं हैं। कई रिपोर्टिंग परिदृश्यों में आप डेटाबेस से एक `DataTable` निकालते हैं, उसे वर्कशीट में डालते हैं, और फिर तिथियों को सही दिखाने और कॉलम को सही रंगों से हाइलाइट करने के लिए जद्दोजहद करते हैं।  

इस ट्यूटोरियल में हम एक साफ़, एंड‑टू‑एंड समाधान के माध्यम से चलेंगे जो **तिथि प्रारूप सेट** करता है, **सेल बैकग्राउंड सेट** करता है, **फ़ोरग्राउंड रंग लागू** करता है, और यहाँ तक कि डेटा आयात करते समय **Excel कॉलम को रंगीन** भी बनाता है। अंत तक आपके पास एक पुन: उपयोग योग्य पैटर्न होगा जो **excel import formatting** को सामान्य ट्रायल‑एंड‑एरर के बिना संभालता है।

> **What you’ll need**  
> * .NET 6+ (or .NET Framework 4.7+)  
> * Aspose.Cells for .NET (free trial works for testing)  
> * A `DataTable` source – any ADO.NET query will do  
> * Visual Studio or your favorite IDE  

चलिए शुरू करते हैं।

---

## समाधान का अवलोकन

हम समस्या को तीन तार्किक भागों में विभाजित करेंगे:

1. **Retrieve the source data** – एक `DataTable` जिसमें आप निर्यात करना चाहते हैं।  
2. **Create column‑specific styles** – तिथि कॉलम के लिए एक स्टाइल, टेक्स्ट कॉलम के लिए दूसरा स्टाइल, और आप जो भी अतिरिक्त स्टाइलिंग चाहते हैं।  
3. **Import the table with styles** – `Worksheet.Cells.ImportDataTable` का उपयोग करें ताकि प्रत्येक कॉलम तैयार किए गए स्टाइल को विरासत में ले।

इस दृष्टिकोण का कारण? क्योंकि Aspose.Cells आपको `ImportDataTable` कॉल में सीधे `Style` एरे संलग्न करने देता है, जिससे आपको फ़ॉर्मेटिंग को फिर से लागू करने के लिए दूसरा पास नहीं करना पड़ता। यह तेज़, कम त्रुटिप्रवण, और आपका कोड साफ़ रखता है।

---

## चरण 1: निर्यात करने के लिए डेटा प्राप्त करें

सबसे पहले – आपको एक `DataTable` चाहिए। वास्तविक प्रोजेक्ट में आप संभवतः एक स्टोरड प्रोसीजर कॉल करेंगे या Entity Framework का उपयोग करके इसे भरेंगे, लेकिन उदाहरण के लिए हम एक सरल टेबल को मॉक करेंगे जिसमें एक तिथि और एक टेक्स्ट कॉलम होगा।

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Pro tip:** यदि आपका स्रोत nullable तिथियों का उपयोग करता है, तो सुनिश्चित करें कि कॉलम प्रकार `typeof(DateTime?)` हो – Aspose बाद में आप जो फ़ॉर्मेट असाइन करेंगे उसे अभी भी सम्मानित करेगा।

## चरण 2: स्टाइल्स की एक एरे तैयार करें – प्रत्येक कॉलम के लिए एक

अब हम एक `Style[]` बनाते हैं जिसकी लंबाई `DataTable` में कॉलमों की संख्या के बराबर होती है। प्रत्येक एंट्री अपने संबंधित कॉलम के फ़ॉर्मेट को रखेगी।

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 पहले कॉलम के लिए तिथि प्रारूप सेट करें

पहला कॉलम (`OrderDate`) “MM/dd/yyyy” के रूप में दिखना चाहिए। Aspose शॉर्ट डेट के लिए बिल्ट‑इन नंबर फ़ॉर्मेट इंडेक्स 14 का उपयोग करता है, लेकिन आप चाहें तो एक कस्टम फ़ॉर्मेट स्ट्रिंग भी प्रदान कर सकते हैं।

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Why this matters:** Excel तिथियों को सीरियल नंबरों के रूप में संग्रहीत करता है। एक नंबर फ़ॉर्मेट असाइन करके आप Excel को बताते हैं कि उन सीरियल को कच्चे नंबरों की बजाय मानव‑पठनीय तिथियों के रूप में रेंडर करे।

### 2.2 दूसरे कॉलम के लिए सेल बैकग्राउंड सेट करें

आइए `CustomerName` कॉलम को हल्के नीले बैकग्राउंड दें। यही वह जगह है जहाँ **set cell background** काम आता है।

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Note:** `Pattern` को `Solid` सेट किए बिना, फ़ोरग्राउंड रंग नहीं दिखेगा क्योंकि डिफ़ॉल्ट पैटर्न “None” है।

### 2.3 फ़ोरग्राउंड (टेक्स्ट) रंग लागू करें – वैकल्पिक अतिरिक्त

यदि आप टेक्स्ट को भी एक कंट्रास्टिंग रंग देना चाहते हैं, तो आप वही स्टाइल थोड़ा बदल सकते हैं:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

यह **apply foreground color** की आवश्यकता को पूरा करता है जबकि कॉलम की बैकग्राउंड अपरिवर्तित रहती है।

## चरण 3: परिभाषित स्टाइल्स के साथ DataTable आयात करें

स्टाइल्स तैयार होने के बाद, अंतिम चरण एक ही लाइन है जो डेटा आयात करती है और स्टाइल्स को कॉलम‑बाय‑कॉलम लागू करती है।

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**How it works:** Aspose `columnStyles` एरे को पढ़ता है और प्रत्येक `Style` को संबंधित कॉलम इंडेक्स से मैप करता है। हेडर रो डिफ़ॉल्ट स्टाइल को विरासत में लेती है जब तक आप रो 0 के लिए अलग स्टाइल न प्रदान करें।

### 3.1 वर्कबुक सहेजें

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

प्रोग्राम चलाएँ, *FormattedReport.xlsx* खोलें, और आपको यह दिखना चाहिए:

- **OrderDate** कॉलम तिथियों के रूप में प्रदर्शित होगा (उदाहरण : `06/15/2026`)।  
- **CustomerName** कॉलम हल्के‑नीले फ़िल और गहरे‑नीले टेक्स्ट के साथ होगा।  

यह पूरी **excel import formatting** वर्कफ़्लो है, जो केवल 30 लाइनों के C# कोड में पूरी हो जाती है।

## चरण‑दर‑चरण सारांश (क्यों के साथ)

| चरण | आप क्या करते हैं | क्यों महत्वपूर्ण है |
|------|----------------|-------------------|
| **Retrieve data** | `GetData()` को कॉल करके `DataTable` भरें। | Aspose को सीधे इनजेस्ट करने के लिए एक संरचित स्रोत प्रदान करता है। |
| **Create style array** | कॉलम काउंट के बराबर `Style[]` आवंटित करें। | एक ही आयात कॉल में प्रति‑कॉलम स्टाइलिंग की अनुमति देता है। |
| **Set date format** | `columnStyles[0].Number = 14;` | Excel में तिथियों को सही ढंग से रेंडर करता है। |
| **Set background color** | `ForegroundColor = LightBlue; Pattern = Solid;` | कॉलम को हाइलाइट करता है, **set cell background** को संतुष्ट करता है। |
| **Apply foreground color** | `Font.Color = DarkBlue;` | पठनीयता बढ़ाता है और **apply foreground color** को पूरा करता है। |
| **Import with styles** | `ImportDataTable(..., columnStyles);` | सभी फ़ॉर्मेटिंग को सम्मानित करने वाला एक‑पास आयात। |
| **Save workbook** | `wb.Save(...);` | परिणाम को डाउनस्ट्रीम उपयोगकर्ताओं के लिए स्थायी बनाता है। |

## किनारे के मामलों और सामान्य प्रश्नों को संभालना

### यदि मेरे पास दो से अधिक कॉलम हों तो क्या करें?

बस `columnStyles` एरे को विस्तारित करें और प्रत्येक इच्छित इंडेक्स को एक `Style` असाइन करें। अनअसाइन किए गए इंडेक्स डिफ़ॉल्ट स्टाइल को फॉल्बैक करेंगे, जो पूरी तरह ठीक है।

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### कॉलम को मुद्रा के रूप में कैसे फ़ॉर्मेट करें?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### क्या मैं हेडर रो की शैली अलग से बदल सकता हूँ?

हाँ। आयात के बाद, आप पहली रो को पकड़कर एक अलग स्टाइल लागू कर सकते हैं:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### यदि DataTable में null तिथियाँ हों तो क्या करें?

Aspose उन सेल्स को खाली छोड़ देगा। यदि आप “N/A” जैसे प्लेसहोल्डर चाहते हैं, तो आप टेबल को प्री‑प्रोसेस कर सकते हैं:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

फिर स्टाइल को इस तरह समायोजित करें कि वह “N/A” को सेंटिनल वैल्यू के लिए दिखाए।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा, कॉपी‑पेस्ट‑तैयार प्रोग्राम है। इसे एक कंसोल ऐप के रूप में चलाएँ, और आपको एक सुंदर फ़ॉर्मेटेड Excel फ़ाइल मिलेगी।



## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [Set Font Color in Excel Cells using Aspose.Cells for .NET](/cells/english/net/formatting/setting-font-color/)
- [Set Font Color in .NET Excel with Aspose.Cells](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Set Excel Column Widths in Pixels Using Aspose.Cells for .NET | Step-by-Step Guide](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}