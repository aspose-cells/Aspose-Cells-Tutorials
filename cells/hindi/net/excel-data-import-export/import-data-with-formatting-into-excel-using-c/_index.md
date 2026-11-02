---
category: general
date: 2026-03-01
description: C# का उपयोग करके फ़ॉर्मेटिंग के साथ डेटा को Excel में इम्पोर्ट करें।
  जानिए कैसे DataTable को Excel में इम्पोर्ट किया जाए और कुछ ही चरणों में सेल्स में
  बैकग्राउंड रंग जोड़ा जाए।
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: hi
og_description: C# का उपयोग करके फ़ॉर्मेटिंग के साथ डेटा को Excel में इम्पोर्ट करें।
  चरण‑दर‑चरण गाइड जो दिखाता है कि DataTable को कैसे इम्पोर्ट करें और सेल्स में बैकग्राउंड
  रंग कैसे जोड़ें।
og_title: फ़ॉर्मेटिंग के साथ डेटा को एक्सेल में आयात करें – C# गाइड
tags:
- C#
- Excel
- DataTable
- Formatting
title: C# का उपयोग करके फ़ॉर्मेटिंग के साथ डेटा को एक्सेल में आयात करें
url: /hi/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# का उपयोग करके फ़ॉर्मेटिंग के साथ डेटा को Excel में इम्पोर्ट करें

क्या आपको कभी **फ़ॉर्मेटिंग के साथ डेटा को इम्पोर्ट** करने की ज़रूरत पड़ी है Excel वर्कबुक में, लेकिन आपको हमेशा एक साधारण, बोरिंग शीट मिलती रही? आप अकेले नहीं हैं। अधिकांश डेवलपर्स इस समस्या का सामना करते हैं जब वे पाते हैं कि डिफ़ॉल्ट इम्पोर्ट सभी रंगों और शैलियों को हटा देता है जो उन्होंने अपने स्रोत डेटा में मेहनत से सेट किए होते हैं।

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य समाधान के माध्यम से चलेंगे जो **DataTable को Excel में इम्पोर्ट** करता है और **Excel सेल्स में बैकग्राउंड कलर जोड़ता** है। कोई अतिरिक्त पोस्ट‑प्रोसेसिंग नहीं चाहिए—आपका स्प्रेडशीट बिल्कुल वही दिखेगा जैसा आप चाहते हैं, बॉक्स से बाहर निकलते ही।

## आप क्या सीखेंगे

- `DataTable` में डेटा कैसे प्राप्त करें।
- बैकग्राउंड कलर ले जाने वाले `Style` ऑब्जेक्ट्स की एक एरे कैसे परिभाषित करें।
- उन स्टाइल्स के साथ `ImportDataTable` को कैसे कॉल करें ताकि इम्पोर्ट फ़ॉर्मेटिंग को बरकरार रखे।
- एक पूर्ण, रन करने योग्य उदाहरण जिसे आप एक कंसोल ऐप में डाल सकते हैं और तुरंत परिणाम देख सकते हैं।
- वास्तविक‑दुनिया के प्रोजेक्ट्स के लिए टिप्स, pitfalls, और वैरिएशन्स।

### आवश्यकताएँ

- .NET 6.0 या बाद का (कोड .NET Framework 4.6+ के साथ भी काम करता है)।
- **GemBox.Spreadsheet** लाइब्रेरी (डेमो के लिए फ्री वर्ज़न पर्याप्त है)।
- C# और Excel अवधारणाओं की बुनियादी जानकारी।

यदि आप सोच रहे हैं *GemBox क्यों?* क्योंकि यह एक सिंगल‑लाइन `ImportDataTable` मेथड प्रदान करता है जो स्टाइल एरे को स्वीकार करता है—बिल्कुल वही जो हमें **फ़ॉर्मेटिंग के साथ डेटा इम्पोर्ट** करने के लिए चाहिए, बिना लूप लिखे।

---

## चरण 1: प्रोजेक्ट सेट अप करें और GemBox.Spreadsheet जोड़ें

शुरू करने के लिए, एक नया कंसोल ऐप बनाएं:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Pro tip:** फ्री वर्ज़न में वर्कशीट्स की सीमा 150 k सेल्स तक है, जो डेमो के लिए पर्याप्त है। यदि आप सीमा तक पहुँचते हैं, तो अपग्रेड करें या EPPlus पर स्विच करें, लेकिन API थोड़ा अलग दिखेगा।

## चरण 2: स्रोत डेटा को `DataTable` के रूप में प्राप्त करें

पहले हमें एक `DataTable` चाहिए जो उस डेटा की नकल करे जिसे आप सामान्यतः डेटाबेस से निकालते हैं। यहाँ एक छोटा हेल्पर है जो मेमोरी में एक बनाता है:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**यह क्यों महत्वपूर्ण है:** डेटा रिट्रीवल को एक अलग मेथड में विभाजित करके, आप किसी भी स्रोत—SQL, CSV, वेब सर्विस—को बिना इम्पोर्ट लॉजिक को छुए बदल सकते हैं। यह कोड को साफ़ रखता है और ट्यूटोरियल **how to import datatable into excel** को पुन: उपयोग योग्य बनाता है।

## चरण 3: उन स्टाइल्स को परिभाषित करें जिन्हें आप लागू करना चाहते हैं

अब मज़ेदार हिस्सा: हम `Style` ऑब्जेक्ट्स की एक एरे बनाएँगे, प्रत्येक में एक अलग `ForegroundColor` होगा। GemBox आपको `BackgroundPatternColor` (सेल फ़िल) और `ForegroundColor` (टेक्स्ट कलर) सेट करने देता है। इस डेमो में हम पहले दो कॉलम को अलग‑अलग रंग देंगे।

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**व्याख्या:**  
- `Style` ऑब्जेक्ट्स हल्के कंटेनर होते हैं; आपको हर सेल के लिए नया बनाने की जरूरत नहीं।  
- एरे के क्रम को कॉलम क्रम के साथ मिलाकर रखने से GemBox इम्पोर्ट के दौरान स्वचालित रूप से मेल खाने वाला स्टाइल लागू करता है।  
- यही वह कुंजी है जो **फ़ॉर्मेटिंग के साथ डेटा इम्पोर्ट** को संभव बनाती है—फ़ॉर्मेटिंग डेटा के साथ यात्रा करती है, बाद में नहीं।

## चरण 4: `DataTable` को स्टाइल्स के साथ वर्कशीट में इम्पोर्ट करें

डेटा और स्टाइल्स तैयार होने पर, हम अब एक वर्कबुक बनाएँगे, पहली वर्कशीट चुनेंगे, और `ImportDataTable` को कॉल करेंगे। मेथड सिग्नेचर इस प्रकार दिखता है:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

इसे हम इस तरह उपयोग करते हैं:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**अंदर क्या हो रहा है?**  
- `true` GemBox को कॉलम नामों को पहली पंक्ति में लिखने के लिए कहता है।  
- `0, 0` इम्पोर्ट को सेल A1 पर पोज़िशन करता है।  
- `importStyles` प्रत्येक कॉलम को पहले परिभाषित रंगों से जोड़ता है।  

जब आप *Report.xlsx* खोलेंगे, तो आपको **ID** कॉलम हल्का नीला, **Name** कॉलम हल्का हरा, और **Score** कॉलम बिना बदलाव के दिखेगा। यही **फ़ॉर्मेटिंग के साथ डेटा इम्पोर्ट** एक ही कॉल में है।

## चरण 5: परिणाम सत्यापित करें (अपेक्षित आउटपुट)

जनरेटेड `Report.xlsx` खोलें। आपको कुछ इस तरह दिखना चाहिए:

| ID (light blue) | Name (light green) | Score |
|-----------------|--------------------|-------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- **ID** कॉलम की सेल्स का बैकग्राउंड हल्का‑नीला है।  
- **Name** कॉलम की सेल्स का बैकग्राउंड हल्का‑हरा है।  
- **Score** कॉलम डिफ़ॉल्ट सफ़ेद बैकग्राउंड रखता है।

यह विज़ुअल क्यू रिपोर्ट को तुरंत स्कैन करने योग्य बनाता है—एक छोटा टच जो यूज़र एक्सपीरियंस को काफी बेहतर बना सकता है।

![Excel sheet showing import data with formatting – ID column light blue, Name column light green](excel-screenshot.png "फ़ॉर्मेटिंग के साथ डेटा इम्पोर्ट का उदाहरण")

*Image alt text includes the primary keyword for SEO.*

---

## सामान्य प्रश्न और एज केस

### क्या मैं बैकग्राउंड कलर के अलावा और भी चीज़ें लागू कर सकता हूँ?

बिल्कुल। `Style` आपको फ़ॉन्ट, बॉर्डर, नंबर फ़ॉर्मेट, और यहाँ तक कि कंडीशनल फ़ॉर्मेटिंग भी सेट करने देता है। उदाहरण के लिए, 90 से ऊपर के स्कोर को बोल्ड और रेड बनाने के लिए:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### अगर मेरे `DataTable` में स्टाइल्स की तुलना में अधिक कॉलम हों तो क्या होगा?

GemBox केवल उन कॉलमों पर स्टाइल लागू करेगा जिनके लिए एरे में मिलते‑जुलते एंट्री मौजूद है। अतिरिक्त कॉलम डिफ़ॉल्ट स्टाइल पर रहेंगे—कोई एरर नहीं फेंका जाएगा।

### क्या यह बड़े डेटा सेट्स के साथ काम करता है?

हां, लेकिन फ्री वर्ज़न की सेल सीमा (150 k सेल्स) पर ध्यान रखें। बहुत बड़े रिपोर्ट्स के लिए पेड लाइसेंस पर विचार करें या `worksheet.Cells[row, col].Value = …` के साथ डेटा को रो‑बाय‑रो स्ट्रीम करें—हालांकि इस तरह आपको वन‑लाइनर सुविधा नहीं मिलेगी।

### मौजूदा Excel टेम्पलेट से फ़ॉर्मेटिंग के साथ डेटा कैसे इम्पोर्ट करूँ?

पहले एक टेम्पलेट वर्कबुक लोड कर सकते हैं:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

यह आपको हेडर लोगो, फुटर, और किसी भी प्री‑एक्ज़िस्टिंग स्टाइल को बरकरार रखने देता है, जबकि अभी भी डायनामिक हिस्से के लिए **फ़ॉर्मेटिंग के साथ डेटा इम्पोर्ट** कर सकते हैं।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

प्रोग्राम चलाएँ (`dotnet run`) और जनरेटेड *Report.xlsx* खोलें ताकि रंग तुरंत लागू होते देखें।

---

## निष्कर्ष

आपके पास अब एक ठोस, एंड‑टू‑एंड समाधान है जिससे आप **फ़ॉर्मेटिंग के साथ डेटा को Excel में इम्पोर्ट** कर सकते हैं, बिना अतिरिक्त पोस्ट‑प्रोसेसिंग के। यह तरीका न केवल कोड को साफ़ रखता है, बल्कि आपके रिपोर्ट्स को प्रोफ़ेशनल लुक भी देता है।

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}