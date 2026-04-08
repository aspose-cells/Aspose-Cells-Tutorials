---
category: general
date: 2026-04-07
description: C# का उपयोग करके एक्सेल पंक्तियों में पृष्ठभूमि रंग जोड़ें। सीखें कि
  वैकल्पिक पंक्तियों के रंग कैसे लागू करें, ठोस पृष्ठभूमि शैलियों को सेट करें, और
  एक ही वर्कफ़्लो में डेटाटेबल को एक्सेल में इम्पोर्ट करें।
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: hi
og_description: C# के साथ एक्सेल पंक्तियों में पृष्ठभूमि रंग जोड़ें। यह गाइड दिखाता
  है कि वैकल्पिक पंक्तियों के रंग कैसे लागू करें, ठोस पृष्ठभूमि कैसे सेट करें, और
  डेटा टेबल को कुशलतापूर्वक एक्सेल में कैसे आयात करें।
og_title: Excel में पृष्ठभूमि रंग जोड़ें – C# में वैकल्पिक पंक्ति शैलियाँ
tags:
- C#
- Excel
- DataTable
- Styling
title: एक्सेल में पृष्ठभूमि रंग जोड़ें – C# में वैकल्पिक पंक्तियों की शैली
url: /hi/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में बैकग्राउंड रंग जोड़ें – C# में वैकल्पिक पंक्ति शैलियाँ

क्या आपको कभी **add background color excel** पंक्तियों को जोड़ने की ज़रूरत पड़ी है लेकिन हजारों पंक्तियों वाले जटिल कोड के बिना यह नहीं पता चला? आप अकेले नहीं हैं—अधिकांश डेवलपर्स इस समस्या का सामना करते हैं जब वे पहली बार अपने स्प्रेडशीट को सिर्फ कच्चे डेटा के ढेर से अधिक दिखाने की कोशिश करते हैं।  

अच्छी खबर? कुछ ही मिनटों में आप **apply alternating row colors** लागू कर सकते हैं, एक **solid background** सेट कर सकते हैं, और यहाँ तक कि **import datatable to excel** का उपयोग करके C# में एक साफ़, पुन: उपयोग योग्य पैटर्न के साथ कर सकते हैं।  

इस ट्यूटोरियल में हम पूरी प्रक्रिया को समझेंगे, `DataTable` में डेटा लाने से लेकर प्रत्येक पंक्ति को हल्के‑पीले‑सफ़ेद स्ट्राइप पैटर्न के साथ स्टाइल करने तक। **ClosedXML** या **GemBox.Spreadsheet** जैसे ठोस Excel‑हैंडलिंग पैकेज के अलावा कोई बाहरी लाइब्रेरी आवश्यक नहीं है, और आप देखेंगे कि यह तरीका क्यों प्रदर्शन‑उपयुक्त और रखरखाव में आसान है।

## आप क्या सीखेंगे

- डेटा को पुनः प्राप्त करने और उसे Excel वर्कशीट में फीड करने का तरीका।  
- वैकल्पिक बैकग्राउंड रंगों के साथ **style excel rows** करने का तरीका।  
- `Style` ऑब्जेक्ट का उपयोग करके **set solid background** के पीछे की यांत्रिकी।  
- पंक्ति शैलियों को संरक्षित रखते हुए **import datatable to excel** कैसे करें।  
- खाली टेबल या कस्टम कलर स्कीम जैसे एज केस को संभालने के टिप्स।  

> **Pro tip:** यदि आप पहले से ही ऐसी लाइब्रेरी से एक workbook ऑब्जेक्ट (`wb`) का उपयोग कर रहे हैं जो स्टाइल निर्माण का समर्थन करती है, तो आप कई वर्कशीट्स में वही `Style` इंस्टेंस पुनः उपयोग कर सकते हैं—जिससे मेमोरी बचती है और आपका कोड साफ़ रहता है।  

---

## चरण 1: डेटा प्राप्त करें – DataTable तैयार करना

कोई भी स्टाइलिंग होने से पहले हमें पंक्तियों का स्रोत चाहिए। अधिकांश वास्तविक‑दुनिया के परिदृश्यों में यह डेटाबेस, API, या CSV फ़ाइल से आता है। उदाहरण के लिए, हम केवल एक सरल `DataTable` इन‑मेमोरी बनाएँगे।  

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Why this matters:** `DataTable` का उपयोग करने से आपको एक टेबलर, स्कीमा‑जागरूक कंटेनर मिलता है जिसे Excel लाइब्रेरी सीधे इम्पोर्ट कर सकती है, जिससे सेल‑बाय‑सेल लूप लिखने की आवश्यकता समाप्त हो जाती है।  

---

## चरण 2: पंक्ति शैलियाँ बनाएं – **Apply alternating row colors**

अब हम `Style` ऑब्जेक्ट्स की एक एरे बनाएँगे—प्रति पंक्ति एक—ताकि प्रत्येक पंक्ति अपना बैकग्राउंड प्राप्त कर सके। हम जो पैटर्न उपयोग करेंगे वह है सम पंक्तियों के लिए हल्का‑पीला और विषम पंक्तियों के लिए सफ़ेद।  

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Explanation:**  
- `wb.CreateStyle()` आपको एक साफ़ स्टाइल ऑब्जेक्ट देता है जिसे आप अन्य पर असर डाले बिना संशोधित कर सकते हैं।  
- टर्नरी ऑपरेटर `(i % 2 == 0)` तय करता है कि पंक्ति सम (हल्का पीला) है या विषम (सफ़ेद)।  
- `Pattern = BackgroundType.Solid` सेट करना वह महत्वपूर्ण कदम है जो **set solid background** करता है; इसके बिना रंग को नजरअंदाज किया जाएगा।  

---

## चरण 3: लक्ष्य वर्कशीट प्राप्त करें

अधिकांश लाइब्रेरीज़ एक वर्कशीट कलेक्शन प्रदान करती हैं। हम पहले वाले के साथ काम करेंगे, लेकिन आप अपनी पसंद के किसी भी इंडेक्स या नाम को टार्गेट कर सकते हैं।  

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

यदि workbook बिल्कुल नया है, तो लाइब्रेरी आमतौर पर आपके लिए एक डिफ़ॉल्ट शीट बनाती है। अन्यथा, आप स्पष्ट रूप से एक जोड़ सकते हैं:  

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

---

## चरण 4: DataTable को पंक्ति शैलियों के साथ इम्पोर्ट करें – **Import datatable to excel**

शैलियाँ तैयार होने के बाद, अंतिम कदम `DataTable` को शीट में धकेलना है जबकि प्रत्येक पंक्ति पर संबंधित स्टाइल लागू करना है।  

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**What’s happening under the hood?**  
- `true` मेथड को बताता है कि कॉलम हेडर को पहली पंक्ति के रूप में लिखें।  
- `0, 0` टॉप‑लेफ़्ट कॉर्नर (A1) को इन्सर्शन पॉइंट के रूप में चिह्नित करता है।  
- `rowStyles` प्रत्येक `Style` को मिलते‑जुलते डेटा पंक्ति के साथ संरेखित करता है, जिससे हमें पहले तैयार किए गए वैकल्पिक रंग मिलते हैं।  

---

## चरण 5: वर्कबुक को सहेजें

पज़ल का अंतिम टुकड़ा वर्कबुक को फ़ाइल में सहेजना है ताकि आप इसे Excel में खोल सकें और परिणाम देख सकें।  

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

फ़ाइल खोलें और आपको एक व्यवस्थित फ़ॉर्मेटेड शीट दिखेगी:

- हेडर पंक्ति बोल्ड में (डिफ़ॉल्ट लाइब्रेरी स्टाइलिंग)।  
- पंक्ति 1, 3, 5… साफ़ सफ़ेद बैकग्राउंड के साथ।  
- पंक्ति 2, 4, 6… एक हल्के‑पीले फ़िल के साथ, जिससे स्कैन करना आसान हो जाता है।  

### अपेक्षित आउटपुट स्नैपशॉट

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

पंक्तियाँ 2, 4, 6, … हल्के‑पीले बैकग्राउंड के साथ दिखाई देती हैं—बिल्कुल वही **apply alternating row colors** प्रभाव जिसे हम चाहते थे।  

![Add background color excel example](https://example.com/excel-background.png "Add background color excel example")

*(Alt text includes the primary keyword for SEO.)*  

---

## किनारे के मामलों और विविधताओं को संभालना

### खाली DataTable

यदि `dataTable.Rows.Count` शून्य है, तो `rowStyles` एरे खाली होगा और `ImportDataTable` फिर भी हेडर पंक्ति लिखेगा (यदि `includeHeaders` `true` है)। कोई अपवाद नहीं फेंका जाएगा, लेकिन आप लगभग‑खाली फ़ाइल बनाने से बचने के लिए सुरक्षा जोड़ना चाह सकते हैं:  

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### कस्टम कलर स्कीम्स

क्या आप पीले/सफ़ेद के बजाय नीले/ग्रे स्ट्राइप चाहते हैं? बस `Color` मानों को बदल दें:  

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

आप स्वतंत्र रूप से रंगों को एक कॉन्फ़िगरेशन फ़ाइल से ले सकते हैं ताकि गैर‑डेवलपर्स कोड को छुए बिना पैलेट को ट्यून कर सकें।  

### कई वर्कशीट्स में शैलियों का पुनः उपयोग

यदि आप कई टेबल्स को एक ही वर्कबुक में एक्सपोर्ट करते हैं, तो आप स्टाइल एरे को एक बार जेनरेट कर सकते हैं और पुनः उपयोग कर सकते हैं:  

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

सिर्फ यह ध्यान रखें कि दोनों टेबल्स की पंक्तियों की संख्या समान हो, या प्रत्येक शीट के लिए नई एरे जेनरेट करें।  

---

## पूर्ण कार्यशील उदाहरण

सब कुछ मिलाकर, यहाँ एक स्व-निहित प्रोग्राम है जिसे आप कॉपी‑पेस्ट करके एक कंसोल ऐप में उपयोग कर सकते हैं।  

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

प्रोग्राम चलाएँ, `Report.xlsx` खोलें, और आप वर्णित अनुसार वैकल्पिक बैकग्राउंड देखेंगे।  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}