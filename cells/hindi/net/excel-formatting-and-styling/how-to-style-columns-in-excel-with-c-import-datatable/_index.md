---
category: general
date: 2026-02-21
description: C# का उपयोग करके DataTable को Excel में इम्पोर्ट करते समय कॉलम को कैसे
  स्टाइल करें, सीखें। इसमें Excel में दूसरी कॉलम को रंगने और DataTable को Excel में
  इम्पोर्ट करने के टिप्स शामिल हैं।
draft: false
keywords:
- how to style columns
- import datatable to excel
- how to import datatable
- color second column excel
- import datatable excel c#
language: hi
og_description: C# का उपयोग करके DataTable को Excel में आयात करते समय कॉलम को कैसे
  स्टाइल करें। चरण‑दर‑चरण कोड, Excel में दूसरे कॉलम को रंगें, और सर्वोत्तम प्रथाएँ।
og_title: C# के साथ Excel में कॉलम को स्टाइल करने का तरीका – पूर्ण गाइड
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: C# के साथ Excel में कॉलम को स्टाइल कैसे करें – DataTable आयात
url: /hi/net/excel-formatting-and-styling/how-to-style-columns-in-excel-with-c-import-datatable/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में C# के साथ कॉलम कैसे स्टाइल करें – Import DataTable

क्या आपने कभी सोचा है **कॉलम को कैसे स्टाइल करें** Excel वर्कशीट में जब डेटा सीधे एक `DataTable` से खींचा जाए? आप अकेले नहीं हैं। कई डेवलपर्स को यह समस्या आती है जब उन्हें जल्दी से रंग जोड़ने की जरूरत होती है—शायद पहली कॉलम के लिए लाल, दूसरी के लिए नीला—बिना आयात के बाद प्रत्येक सेल को मैन्युअली बदलें।  

अच्छी खबर? उत्तर कुछ ही पंक्तियों के C# कोड में है, और डेटा लैंड होते ही आपके पास एक पूरी तरह से स्टाइल्ड शीट होगी। इस ट्यूटोरियल में हम **import datatable to excel** को भी कवर करेंगे, आपको **color second column excel** दिखाएंगे, और समझाएंगे कि यह तरीका .NET Framework और .NET 6+ दोनों प्रोजेक्ट्स में क्यों काम करता है।

---

## आप क्या सीखेंगे

- भरे हुए `DataTable` को प्राप्त करें (या तुरंत बनाएं)।  
- प्रति‑कॉलम `Style` ऑब्जेक्ट्स को परिभाषित करें ताकि फ़ोरग्राउंड रंग सेट हो सके।  
- एक वर्कबुक बनाएं, पहली वर्कशीट प्राप्त करें, और स्टाइल लागू करके टेबल आयात करें।  
- खाली टेबल, कस्टम स्टार्ट रो, और डायनेमिक कॉलम काउंट जैसे एज केस को संभालें।  

अंत तक, आप किसी भी रिपोर्टिंग पाइपलाइन में एक स्टाइल्ड Excel फ़ाइल डाल सकेंगे—कोई पोस्ट‑प्रोसेसिंग आवश्यक नहीं।

> **Prerequisite:** C# की बुनियादी समझ और एक स्प्रेडशीट लाइब्रेरी का रेफ़रेंस जो `ImportDataTable` को सपोर्ट करती हो (जैसे, Aspose.Cells, GemBox.Spreadsheet, या EPPlus के साथ हेल्पर)। नीचे दिया गया कोड **Aspose.Cells** का उपयोग करता है क्योंकि इसका `ImportDataTable` ओवरलोड सीधे `Style[]` स्वीकार करता है।

## चरण 1: प्रोजेक्ट सेट अप करें और Excel लाइब्रेरी जोड़ें

किसी भी चीज़ को स्टाइल करने से पहले, हमें एक प्रोजेक्ट चाहिए जो Excel मैनिपुलेशन लाइब्रेरी को रेफ़रेंस करे।

```csharp
// Install-Package Aspose.Cells -Version 24.7
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;   // For Color
```

*Pro tip:* यदि आप .NET 6 पर हैं, तो पैकेज `dotnet add package Aspose.Cells` के माध्यम से जोड़ें। यह लाइब्रेरी Windows, Linux, और macOS पर काम करती है, इसलिए आप भविष्य के लिए तैयार हैं।

## चरण 2: स्रोत DataTable प्राप्त करें या बनाएं

ट्यूटोरियल का मुख्य फोकस स्टाइलिंग पर है, लेकिन आपको अभी भी एक `DataTable` चाहिए। नीचे एक त्वरित हेल्पर दिया गया है जो सैंपल डेटा बनाता है; प्रोडक्शन में इसे अपने `GetTable()` कॉल से बदलें।

```csharp
/// <summary>
/// Returns a DataTable with three columns and five rows of demo data.
/// </summary>
static DataTable GetTable()
{
    var dt = new DataTable("Demo");
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));

    dt.Rows.Add(1, "Alice", 92.5);
    dt.Rows.Add(2, "Bob", 85.3);
    dt.Rows.Add(3, "Charlie", 78.9);
    dt.Rows.Add(4, "Diana", 88.1);
    dt.Rows.Add(5, "Ethan", 91.4);

    return dt;
}
```

> **Why this matters:** `DataTable` का उपयोग करने से आपका डेटा स्रोत एग्नॉस्टिक रहता है—चाहे वह SQL, CSV, या इन‑मेमोरी कलेक्शन से आए, आयात लॉजिक वही रहता है। यह **how to import datatable** को प्रभावी रूप से करने की नींव है।

## चरण 3: कॉलम स्टाइल्स परिभाषित करें ( “How to Style Columns” का हृदय)

अब हम वर्कशीट को बताते हैं कि प्रत्येक कॉलम कैसे दिखेगा। `Style` क्लास आपको फ़ॉन्ट, रंग, बॉर्डर आदि सेट करने देती है। इस उदाहरण में हम केवल फ़ोरग्राउंड रंग बदलते हैं।

```csharp
// Step 3: Define column styles – red for first, blue for second, default for others
Style[] columnStyles = new Style[3]; // Assuming three columns; adjust as needed

// Style for column 0 (first column) – red text
columnStyles[0] = new Style();
columnStyles[0].ForegroundColor = Color.Red;

// Style for column 1 (second column) – blue text
columnStyles[1] = new Style();
columnStyles[1].ForegroundColor = Color.Blue;

// Column 2 (third column) – keep default styling
columnStyles[2] = new Style(); // No changes, but array entry required
```

*What if you have more columns?* बस एरे का आकार बढ़ाएँ और उन स्टाइल्स को भरें जिनकी आपको ज़रूरत है। बिना स्टाइल वाले कॉलम स्वचालित रूप से वर्कशीट की डिफ़ॉल्ट स्टाइल को इनहेरिट कर लेते हैं।

## चरण 4: वर्कबुक बनाएं और स्टाइल्स के साथ DataTable आयात करें

डेटा और स्टाइल्स तैयार होने के बाद, अब सब कुछ एक साथ लाने का समय है।

```csharp
static void Main()
{
    // Retrieve the data
    DataTable dataTable = GetTable();

    // Initialize a new workbook (in‑memory)
    Workbook workbook = new Workbook();

    // Grab the first worksheet (index 0)
    Worksheet worksheet = workbook.Worksheets[0];

    // Import the DataTable starting at cell A1 (row 0, column 0)
    // The 'true' flag tells Aspose.Cells to include column headers
    worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

    // Optional: Auto‑fit columns for a cleaner look
    worksheet.AutoFitColumns();

    // Save the result to disk
    string outputPath = "StyledDataTable.xlsx";
    workbook.Save(outputPath);

    Console.WriteLine($"Excel file saved to {outputPath}");
}
```

**क्या हुआ अभी?**  
- `ImportDataTable` पंक्तियों, कॉलमों, और *वैकल्पिक रूप से* हेडर रो को कॉपी करता है।  
- `columnStyles` पास करने से प्रत्येक कॉलम को पहले परिभाषित `Style` मिल जाता है।  
- यह कॉल एक ही पंक्ति में है, जिसका मतलब है कि **import datatable excel c#** उतना ही सरल है।

## चरण 5: परिणाम सत्यापित करें – अपेक्षित आउटपुट

`StyledDataTable.xlsx` को Excel (या LibreOffice) में खोलें। आपको यह दिखना चाहिए:

| **ID** (red) | **Name** (blue) | **Score** (default) |
|--------------|-----------------|----------------------|
| 1            | Alice           | 92.5                 |
| 2            | Bob             | 85.3                 |
| …            | …               | …                    |

- पहले कॉलम का टेक्स्ट **लाल** दिखता है, जो “how to style columns” की आवश्यकता को पूरा करता है।  
- दूसरे कॉलम का टेक्स्ट **नीला** है, जो **color second column excel** क्वेरी को भी कवर करता है।  

यदि फ़ाइल बिना त्रुटियों के खुलती है, तो आपने सफलतापूर्वक **how to import datatable** को कॉलम स्टाइलिंग के साथ महारत हासिल कर ली है।

## सामान्य प्रश्न और एज केस

### यदि DataTable खाली है तो क्या?

`ImportDataTable` अभी भी हेडर रो बनाएगा (यदि आपने `true` पास किया)। डेटा रो नहीं जोड़े जाएंगे, लेकिन स्टाइल्स हेडर सेल्स पर लागू रहेंगे।

### आयात को किसी अलग सेल से शुरू करने की आवश्यकता है?

`ImportDataTable` में `rowIndex` और `columnIndex` पैरामीटर बदलें। उदाहरण के लिए, `B2` से शुरू करने के लिए `0, 0` के बजाय `1, 1` उपयोग करें।

### कॉलम के बजाय रो को स्टाइल करना चाहते हैं?

आयात के बाद आप `worksheet.Cells.Rows` पर लूप करके प्रत्येक रो को `Style` असाइन कर सकते हैं। हालांकि, कॉलम‑लेवल स्टाइलिंग अधिक प्रदर्शनकारी है क्योंकि लाइब्रेरी प्रत्येक कॉलम पर एक बार स्टाइल लागू करती है।

### EPPlus या ClosedXML का उपयोग कर रहे हैं?

इन लाइब्रेरियों में `ImportDataTable` का सीधे स्टाइल एरे वाला ओवरलोड नहीं है। समाधान यह है कि पहले टेबल आयात करें, फिर कॉलम रेंज पर इटररेट करके `Style.Font.Color.SetColor(...)` सेट करें। लॉजिक वही रहता है, बस कुछ अतिरिक्त पंक्तियों की जरूरत होगी।

## प्रोडक्शन‑रेडी कोड के लिए प्रो टिप्स

- **Reuse Styles:** प्रत्येक कॉलम के लिए नया `Style` बनाना बर्बादी हो सकता है। पुन: उपयोग योग्य स्टाइल्स को रंग या फ़ॉन्ट वेट के आधार पर डिक्शनरी में स्टोर करें।  
- **Avoid Hard‑Coded Column Counts:** `dataTable.Columns.Count` का पता लगाएँ और `columnStyles` एरे को डायनामिक रूप से बनाएं।  
- **Thread Safety:** यदि आप समानांतर में कई वर्कबुक बनाते हैं, तो प्रत्येक थ्रेड के लिए अलग `Workbook` इंस्टैंसिएट करें; Aspose.Cells ऑब्जेक्ट थ्रेड‑सेफ़ नहीं हैं।  
- **Performance:** 10 k से अधिक पंक्तियों वाली टेबल के लिए `AutoFitColumns` को डिसेबल करने पर विचार करें (यह हर सेल को स्कैन करता है) और कॉलम चौड़ाई मैन्युअली सेट करें।

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

```csharp
// ------------------------------------------------------------
// Full example: How to style columns while importing a DataTable
// ------------------------------------------------------------
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetTable();

        // 2️⃣ Define per‑column styles
        int colCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[colCount];

        // Red for first column
        columnStyles[0] = new Style { ForegroundColor = Color.Red };

        // Blue for second column (if it exists)
        if (colCount > 1)
            columnStyles[1] = new Style { ForegroundColor = Color.Blue };

        // Default style for remaining columns
        for (int i = 2; i < colCount; i++)
            columnStyles[i] = new Style(); // no special formatting

        // 3️⃣ Create workbook and import with styles
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
        sheet.AutoFitColumns();

        // 4️⃣ Save to file
        string path = "StyledDataTable.xlsx";
        workbook.Save(path);
        Console.WriteLine($"File saved: {path}");
    }

    // Helper: sample DataTable
    static DataTable GetTable()
    {
        var dt = new DataTable("Demo");
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        dt.Rows.Add(1, "Alice", 92.5);
        dt.Rows.Add(2, "Bob", 85.3);
        dt.Rows.Add(3, "Charlie", 78.9);
        dt.Rows.Add(4, "Diana", 88.1);
        dt.Rows.Add(5, "Ethan", 91.4);
        return dt;
    }
}
```

प्रोग्राम चलाएँ, जेनरेटेड `StyledDataTable.xlsx` खोलें, और आपको तुरंत रंगीन कॉलम दिखेंगे। यही पूरा **import datatable excel c#** वर्कफ़्लो है।

## निष्कर्ष

हमने अभी **how to style columns** को कवर किया है जब आप C# का उपयोग करके **import datatable to excel** करते हैं। `Style[]` एरे को परिभाषित करके और उसे `ImportDataTable` में पास करके, आप पहली कॉलम को लाल, दूसरी को नीला रंग दे सकते हैं, और बाकी को जैसा है वैसा छोड़ सकते हैं—सभी एक ही कोड लाइन में।

यह तरीका स्केलेबल है: अतिरिक्त कॉलम के लिए और `Style` ऑब्जेक्ट जोड़ें, स्टार्ट रो को समायोजित करें, या समान API वाली किसी अन्य लाइब्रेरी से Aspose.Cells को बदलें। अब आप बिना फ़ाइल को मैन्युअली छुए पॉलिश्ड Excel रिपोर्ट बना सकते हैं।

**Next steps** आप एक्सप्लोर कर सकते हैं:

- **conditional formatting** का उपयोग करके मानों को डायनामिक रूप से हाइलाइट करें (जो “color second column excel” से जुड़ा है)।  
- एक ही `DataTable` सेट से कई वर्कशीट्स एक्सपोर्ट करें (मासिक डैशबोर्ड के लिए बेहतरीन)।  
- इसे **CSV → DataTable** कन्वर्ज़न के साथ मिलाकर एक एंड‑टू‑

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}