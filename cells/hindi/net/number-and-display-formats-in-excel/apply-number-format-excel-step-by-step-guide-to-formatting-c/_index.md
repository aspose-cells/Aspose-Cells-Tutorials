---
category: general
date: 2026-02-26
description: एक्सेल में नंबर फ़ॉर्मेट जल्दी लागू करें और सीखें कि कॉलम को मुद्रा के
  रूप में फ़ॉर्मेट कैसे करें, कॉलम का नंबर फ़ॉर्मेट सेट करें, और केवल कुछ ही C# लाइनों
  में कॉलम का फ़ॉन्ट रंग कैसे सेट करें।
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: hi
og_description: C# में आसान चरणों के साथ एक्सेल में नंबर फ़ॉर्मेट लागू करें। कॉलम
  को मुद्रा के रूप में फ़ॉर्मेट करना, कॉलम नंबर फ़ॉर्मेट सेट करना, और पेशेवर स्प्रेडशीट्स
  के लिए कॉलम फ़ॉन्ट रंग सेट करना सीखें।
og_title: एक्सेल में संख्या स्वरूप लागू करें – कॉलम स्टाइलिंग के लिए संपूर्ण गाइड
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: एक्सेल में नंबर फ़ॉर्मेट लागू करें – कॉलम फ़ॉर्मेट करने के लिए चरण‑दर‑चरण गाइड
url: /hi/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

which are not code fences but placeholders. Actually they are not fenced code blocks; they are placeholders. The requirement says preserve code blocks fenced with ```. There are none in the content except placeholders. So we keep placeholders as is.

We must translate step-by-step.

Let's produce Hindi translation.

Be careful with markdown formatting: headings (#, ##, ###). Keep them.

Translate bullet lists.

Translate blockquote >.

Translate table content: keep **Product** etc but translate maybe the description? The table header includes **Product** (blue font) etc. Should we translate "Product" to Hindi? It is a column name; maybe keep as is? The instruction: translate all text content naturally to Hindi, but keep technical terms in English. "Product" is a business term, could be translated as "उत्पाद". However it's column header; maybe keep as is? The original had **Product** (blue font). I'd translate "Product" to "उत्पाद". Similarly "Price" to "कीमत". The description in parentheses can be translated.

Let's translate.

Also list items under "What You’ll Learn" etc.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# apply number format excel – How to Style Excel Columns in C#

क्या आपने कभी सोचा है कि **apply number format excel** को कैसे लागू किया जाए जबकि आप पहले से ही एक `DataTable` पर लूप कर रहे हैं? आप अकेले नहीं हैं। अधिकांश डेवलपर्स को वही समस्या आती है जब उन्हें एक ही इम्पोर्ट ऑपरेशन में नीले‑फ़ॉन्ट हेडर *और* मुद्रा‑स्टाइल कॉलम चाहिए होता है। अच्छी खबर? कुछ ही C# लाइनों और सही स्टाइल ऑब्जेक्ट्स के साथ, आप इसे शीट के पोस्ट‑प्रोसेसिंग के बिना कर सकते हैं।

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे कि कैसे **format column as currency**, **set column number format** किसी भी अन्य कॉलम के लिए, और यहाँ तक कि **set column font color** हेडर के लिए सेट किया जाए। अंत तक आपके पास एक पुन: उपयोग योग्य पैटर्न होगा जिसे आप किसी भी Aspose.Cells (या समान) प्रोजेक्ट में डाल सकते हैं।

## What You’ll Learn

- कैसे एक `DataTable` प्राप्त करें और प्रत्येक कॉलम को एक विशिष्ट `Style` से मैप करें।
- `Worksheet.Cells.ImportDataTable` का उपयोग करके **apply number format excel** करने के सटीक चरण।
- क्यों स्टाइल्स को पहले से बनाना, एक‑एक सेल को फ़ॉर्मेट करने से अधिक कुशल होता है।
- जब स्रोत टेबल में आपके द्वारा स्टाइल किए गए कॉलम से अधिक कॉलम हों, तो किन किन मामलों को संभालना है।
- एक पूर्ण, कॉपी‑एंड‑पेस्ट‑रेडी कोड सैंपल जो आप आज ही चला सकते हैं।

> **Prerequisite:** यह गाइड मानता है कि आपके प्रोजेक्ट में Aspose.Cells for .NET (या कोई भी लाइब्रेरी जो `Workbook`, `Worksheet`, `Style` API प्रदान करती हो) रेफ़रेंस्ड है। यदि आप कोई अलग लाइब्रेरी उपयोग कर रहे हैं, तो अवधारणाएँ सीधे लागू होती हैं—सिर्फ टाइप नाम बदल दें।

---

## Step 1: Retrieve the Source Data as a DataTable

किसी भी स्टाइलिंग से पहले, आपको कच्चा डेटा चाहिए। अधिकांश वास्तविक‑दुनिया परिदृश्यों में डेटा डेटाबेस, CSV, या API में रहता है। स्पष्टता के लिए हम दो कॉलम वाला एक सरल `DataTable` मॉक करेंगे: *Product* (string) और *Price* (decimal)।

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Why this matters:** डेटा को `DataTable` में लाने से आपको एक टेबलर, इन‑मेमोरी प्रतिनिधित्व मिलता है जिसे `ImportDataTable` सीधे उपयोग कर सकता है, जिससे मैन्युअल सेल‑बाय‑सेल इन्सर्शन की आवश्यकता समाप्त हो जाती है।

## Step 2: Create an Array of Styles – One per Column

`ImportDataTable` ओवरलोड जो हम उपयोग करेंगे, `Style` ऑब्जेक्ट्स की एक एरे स्वीकार करता है। प्रत्येक एंट्री कॉलम इंडेक्स से मेल खाती है। यदि आप किसी एंट्री को `null` छोड़ते हैं, तो कॉलम डिफ़ॉल्ट वर्कबुक स्टाइल को इनहेरिट करता है।

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Pro tip:** एरे को *DataTable* मिलने के बाद डिक्लेयर करने से आकार ठीक‑ठाक रहता है, जिससे बाद में `IndexOutOfRangeException` से बचा जा सके।

## Step 3: Set Column Font Color (Blue) for the First Column

एक आम अनुरोध है हेडर या प्रमुख कॉलम को अलग फ़ॉन्ट रंग से हाइलाइट करना। यहाँ हम पहले कॉलम का टेक्स्ट नीला कर रहे हैं।

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Why use a style object?** स्टाइल्स पुन: उपयोग योग्य होते हैं और एक साथ लागू किए जा सकते हैं, जो इम्पोर्ट के बाद प्रत्येक सेल पर इटररेट करने की तुलना में बहुत तेज़ है। वर्कबुक स्टाइल को एक बार कैश करता है, फिर उस कॉलम के हर सेल के लिए पुन: उपयोग करता है।

## Step 4: Format the Second Column as Currency

Excel के बिल्ट‑इन नंबर फ़ॉर्मेट्स को एक इंडेक्स द्वारा पहचाना जाता है। `14` डिफ़ॉल्ट मुद्रा फ़ॉर्मेट को दर्शाता है (जैसे, `$1,234.00`)। यदि आपको कस्टम फ़ॉर्मेट चाहिए, तो आप फ़ॉर्मेट स्ट्रिंग असाइन कर सकते हैं।

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Edge case:** यदि आपका वर्कबुक ऐसे लोकेल में है जहाँ मुद्रा प्रतीक `$` नहीं है, तो वही इंडेक्स स्वचालित रूप से अनुकूल हो जाएगा (जैसे, जर्मन लोकेल में `€`)।

## Step 5: Import the DataTable with the Defined Styles

अब सब कुछ एक साथ लाते हैं। `ImportDataTable` मेथड डेटा को सेल `A1` (row 0, column 0) से शुरू करके पेस्ट करेगा और हमने जो स्टाइल्स तैयार किए हैं, उन्हें लागू करेगा।

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- दूसरा पैरामीटर `true` Aspose.Cells को बताता है कि `DataTable` की पहली पंक्ति को कॉलम हेडर माना जाए।
- `0, 0` कॉर्डिनेट्स इम्पोर्ट की शुरुआत वाले टॉप‑लेफ़्ट कोने को दर्शाते हैं।
- `columnStyles` प्रत्येक कॉलम को उसके संबंधित स्टाइल से मैप करता है।

## Step 6: Save the Workbook (Optional, but Handy for Verification)

यदि आप परिणाम को Excel में देखना चाहते हैं, तो वर्कबुक को डिस्क पर सेव करें। यह स्टेप स्टाइलिंग लॉजिक के लिए आवश्यक नहीं है, लेकिन डिबगिंग के लिए उपयोगी है।

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Expected Output

| **उत्पाद** (नीला फ़ॉन्ट) | **कीमत** (मुद्रा) |
|--------------------------|--------------------|
| Apple                    | $1.25              |
| Banana                   | $0.75              |
| Cherry                   | $2.10              |

- *उत्पाद* कॉलम नीले रंग में दिखेगा, जिससे वह अलग दिखेगा।
- *कीमत* कॉलम डिफ़ॉल्ट मुद्रा प्रतीक और दो दशमलव स्थानों के साथ मान प्रदर्शित करेगा।

---

## Frequently Asked Questions & Variations

### How do I **set column number format** for more than two columns?

बस `columnStyles` एरे को विस्तारित करें। उदाहरण के लिए, तीसरे कॉलम में प्रतिशत दिखाने के लिए:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### What if I need a *custom* currency format, like “USD 1,234.00”?

`Number` प्रॉपर्टी को फ़ॉर्मेट स्ट्रिंग से बदलें:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Can I apply a **set column font color** to a numeric column without affecting its number format?

बिल्कुल। स्टाइल्स कॉम्पोज़ेबल होते हैं। आप एक ही `Style` इंस्टेंस पर `Font.Color` और `Number` दोनों सेट कर सकते हैं:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### What happens if the `DataTable` has more columns than styles?

कोई भी कॉलम जिसके पास स्पष्ट स्टाइल (`null` एंट्री) नहीं है, वह वर्कबुक की डिफ़ॉल्ट स्टाइल को इनहेरिट करेगा। अनजाने में `null` एंट्री से बचने के लिए, आप पूरी एरे को पहले एक बेस स्टाइल से इनिशियलाइज़ कर सकते हैं:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

फिर केवल उन कॉलमों को ओवरराइड करें जिनकी आपको ज़रूरत है।

### Does this approach work with large data sets (10k+ rows)?

हां। क्योंकि स्टाइलिंग *प्रति कॉलम* एक बार लागू की जाती है इम्पोर्ट से पहले, ऑपरेशन की जटिलता पंक्तियों के संदर्भ में O(N) रहती है, और मेमोरी उपयोग कम रहता है। इम्पोर्ट के बाद प्रत्येक सेल पर लूप करने से बचें—वहीं पर प्रदर्शन गिरता है।

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

प्रोग्राम चलाएँ, `StyledReport.xlsx` खोलें, और आपको **apply number format excel** का परिणाम तुरंत दिखाई देगा।

---

## Conclusion

हमने अभी एक साफ़, कुशल तरीका दिखाया है जिससे आप एक इम्पोर्टेड `DataTable` पर **apply number format excel** कर सकते हैं। स्टाइल्स की `Style[]` एरे को पहले तैयार करके, आप **format column as currency**, **set column number format**, और **set column font color** को एक ही कॉल में कर सकते हैं—बिना किसी पोस्ट‑प्रोसेसिंग के।

इस पैटर्न को आगे बढ़ाएँ: कंडीशनल स्टाइलिंग जोड़ें, हेडर के लिए सेल मर्ज करें, या फ़ॉर्मूले इन्जेक्ट करें। वही सिद्धांत लागू होते हैं, जिससे आपका कोड साफ़ रहता है और आपके स्प्रेडशीट प्रोफ़ेशनल दिखते हैं।

---

### What’s Next?

- **conditional formatting** का उपयोग करके उन मानों को हाइलाइट करें जो एक थ्रेशहोल्ड से अधिक हैं।
- इस तकनीक को **pivot table generation** के साथ मिलाकर डायनामिक रिपोर्टिंग बनाएं।
- **set column number format** को डेट, प्रतिशत, या कस्टम साइंटिफिक नोटेशन के लिए आज़माएँ।

क्या आपने कोई ट्विस्ट आज़माया? कमेंट्स में शेयर करें—आइए इसे साथ मिलकर बेहतर बनाते रहें।

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}