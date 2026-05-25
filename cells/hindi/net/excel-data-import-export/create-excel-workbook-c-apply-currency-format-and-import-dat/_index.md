---
category: general
date: 2026-03-30
description: C# में मुद्रा स्वरूपण के साथ Excel वर्कबुक बनाएं। सीखें कि DataTable
  को कैसे आयात करें, Excel में संख्या स्वरूप कैसे जोड़ें, और मिनटों में मुद्रा स्वरूप
  कॉलम लागू करें।
draft: false
keywords:
- create excel workbook c#
- format cells currency
- import datatable to excel
- add number format excel
- apply currency format column
language: hi
og_description: C# में Excel वर्कबुक बनाएं और तुरंत सेल्स को मुद्रा के रूप में फॉर्मेट
  करें। यह चरण‑दर‑चरण ट्यूटोरियल दिखाता है कि कैसे DataTable को Excel में इम्पोर्ट
  करें और किसी कॉलम के लिए नंबर फ़ॉर्मेट जोड़ें।
og_title: Excel वर्कबुक बनाएं C# – मुद्रा स्वरूपण गाइड
tags:
- Aspose.Cells
- C#
- Excel automation
title: C# में Excel वर्कबुक बनाएं – मुद्रा फ़ॉर्मेट लागू करें और DataTable आयात करें
url: /hi/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel वर्कबुक C# बनाएं – मुद्रा फ़ॉर्मेट लागू करें और DataTable आयात करें

क्या आपको कभी **create Excel workbook C#** बनाना पड़ा है जो पहले से ही एक परिष्कृत रिपोर्ट जैसा दिखे? शायद आप डेटाबेस से बिक्री आंकड़े निकाल रहे हैं और चाहते हैं कि कीमत वाला कॉलम डॉलर में दिखे बिना Excel को मैन्युअल रूप से एडजस्ट किए। यह परिचित लग रहा है? आप अकेले नहीं हैं—ज्यादातर डेवलपर्स को पहली बार Excel एक्सपोर्ट ऑटोमेट करते समय यही समस्या आती है।

> **आप क्या सीखेंगे**
> - .NET प्रोजेक्ट में Aspose.Cells को कैसे सेटअप करें  
> - **import datatable to excel** को एक स्टाइल एरे के साथ कैसे आयात करें  
> - किसी विशिष्ट कॉलम के लिए **add number format excel** कैसे जोड़ें  
> - अधिक कॉलम या विभिन्न लोकैल्स को संभालने के टिप्स  

> **पूर्वापेक्षाएँ**  
> - .NET 6+ (या .NET Framework 4.6+) स्थापित हो  
> - Aspose.Cells for .NET NuGet पैकेज (`Install-Package Aspose.Cells`)  
> - C# और DataTables की बुनियादी समझ  

---

## चरण 1: DataTable तैयार करें (import datatable to excel)

सबसे पहले, हमें कुछ नमूना डेटा चाहिए। वास्तविक एप्लिकेशन में आप इस टेबल को DB क्वेरी से भरेंगे, लेकिन एक हार्ड‑कोडेड उदाहरण चीज़ों को सरल रखता है।

```csharp
using System.Data;

// Create a DataTable with two columns: Product (string) and Price (double)
DataTable dataTable = new DataTable();
dataTable.Columns.Add("Product", typeof(string));
dataTable.Columns.Add("Price", typeof(double));

// Add a few rows – you can add as many as you like
dataTable.Rows.Add("Apple", 1.23);
dataTable.Rows.Add("Banana", 0.78);
dataTable.Rows.Add("Cherry", 2.50);
```

*यह क्यों महत्वपूर्ण है*: `DataTable` आपके बिज़नेस डेटा और Excel फ़ाइल के बीच का पुल है। Aspose.Cells इसे सीधे आयात कर सकता है, कॉलम नाम और डेटा टाइप को बरकरार रखते हुए।

---

## चरण 2: नया वर्कबुक बनाएं (create excel workbook c#)

अब हम वास्तविक Excel फ़ाइल ऑब्जेक्ट बनाते हैं। इसे एक खाली कैनवास समझें जिस पर आप पेंट करेंगे।

```csharp
using Aspose.Cells;

// Instantiate a fresh workbook – this is the core of create excel workbook c#
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0). You could also add more sheets later.
Worksheet worksheet = workbook.Worksheets[0];
```

> **प्रो टिप:** यदि आपको कई शीट्स चाहिए, तो `workbook.Worksheets.Add()` कॉल करें और प्रत्येक को एक सार्थक नाम दें।

---

## चरण 3: मुद्रा स्टाइल परिभाषित करें (format cells currency)

Aspose.Cells आपको एक `Style` ऑब्जेक्ट बनाने देता है जो बताता है कि सेल्स कैसे दिखेंगे। मुद्रा के लिए हम बिल्ट‑इन नंबर फ़ॉर्मेट ID 164 (`"$#,##0.00"`) का उपयोग करते हैं।

```csharp
// Create a new style object for the price column
Style priceStyle = workbook.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format "$#,##0.00"
```

*सिर्फ फ़ॉर्मेट स्ट्रिंग सेट न करके क्यों?* बिल्ट‑इन ID का उपयोग करने से Excel के विभिन्न संस्करणों में संगतता बनी रहती है और लोकैल‑विशिष्ट गड़बड़ियों से बचा जा सकता है।

---

## चरण 4: स्टाइल एरे बनाएं (apply currency format column)

जब आप एक `DataTable` आयात करते हैं, तो आप `Style` ऑब्जेक्ट्स की एक एरे पास कर सकते हैं—प्रति कॉलम एक। `null` का मतलब “डिफ़ॉल्ट स्टाइल उपयोग करें” है। यहाँ हम केवल दूसरे कॉलम पर `priceStyle` लागू करते हैं।

```csharp
// Column 0 (Product) gets the default style, Column 1 (Price) gets the currency style
Style[] columnStyles = { null, priceStyle };
```

यदि बाद में आप और कॉलम जोड़ते हैं, तो एरे को उसी अनुसार विस्तारित करें। `columnStyles` की लंबाई आपके आयात किए जा रहे कॉलमों की संख्या के बराबर होनी चाहिए, अन्यथा Aspose एक एक्सेप्शन फेंकेगा।

---

## चरण 5: स्टाइल के साथ DataTable आयात करें (import datatable to excel)

अब जादू होता है—हमारा `DataTable` वर्कशीट में उतरता है, और कीमत वाला कॉलम तुरंत मुद्रा के रूप में दिखता है।

```csharp
// Parameters:
//  - dataTable: source data
//  - true: include column headers
//  - startRow: 0 (top of sheet)
//  - startColumn: 0 (first column)
//  - columnStyles: style array defined above
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

*अगर आपके पास दो से अधिक कॉलम हैं तो क्या?* बस `columnStyles` को विस्तारित करें ताकि प्रत्येक कॉलम को उपयुक्त स्टाइल (या डिफ़ॉल्ट के लिए `null`) मिले। यह **add number format excel** को चयनात्मक रूप से जोड़ने का सबसे साफ़ तरीका है।

---

## चरण 6: वर्कबुक सहेजें (create excel workbook c#)

अंत में, फ़ाइल को डिस्क पर लिखें। कोई भी फ़ोल्डर चुनें जहाँ आपके पास लिखने की अनुमति हो।

```csharp
// Save the workbook as an XLSX file
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

`StyledTable.xlsx` को Excel में खोलें और आपको यह दिखना चाहिए:

| उत्पाद | मूल्य |
|---------|-------|
| Apple   | $1.23 |
| Banana  | $0.78 |
| Cherry  | $2.50 |

**Price** कॉलम पहले से ही मुद्रा के रूप में फ़ॉर्मेट किया गया है—कोई अतिरिक्त कदम नहीं चाहिए।

---

## किनारे के मामलों और विविधताएँ

### अधिक कॉलम, विभिन्न फ़ॉर्मेट

यदि आपको कई कॉलम (जैसे Cost, Tax, Total) के लिए **format cells currency** चाहिए, तो प्रत्येक के लिए अलग `Style` बनाएं और `columnStyles` को उसी अनुसार भरें:

```csharp
Style costStyle = workbook.CreateStyle();
costStyle.Number = 164; // currency

Style taxStyle = workbook.CreateStyle();
taxStyle.Number = 164;

// Assuming columns: Product, Cost, Tax, Total
Style[] styles = { null, costStyle, taxStyle, priceStyle };
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, styles);
```

### लोकैल‑विशिष्ट मुद्रा

Euro या British Pound के लिए अलग बिल्ट‑इन IDs (जैसे `€#,##0.00` के लिए 165) उपयोग करें। वैकल्पिक रूप से, एक कस्टम फ़ॉर्मेट स्ट्रिंग सेट करें:

```csharp
priceStyle.Custom = "€#,##0.00";
```

### बड़े डेटा सेट

Aspose.Cells लाखों पंक्तियों को संभाल सकता है, लेकिन स्टाइल ऑब्जेक्ट्स के साथ मेमोरी उपयोग बढ़ता है। सभी मुद्रा कॉलमों के लिए एक ही `Style` इंस्टेंस को पुन: उपयोग करें ताकि फ़ुटप्रिंट कम रहे।

### स्टाइल्स की कमी

यदि `columnStyles` कॉलमों की संख्या से छोटी है, तो Aspose शेष कॉलमों पर डिफ़ॉल्ट स्टाइल लागू करेगा। यह तब उपयोगी है जब आपको केवल कुछ कॉलमों की परवाह है।

---

## पूर्ण कार्यशील उदाहरण (सभी चरण एक साथ)

नीचे वह पूरा प्रोग्राम है जिसे आप कॉन्सोल ऐप में कॉपी‑पेस्ट कर सकते हैं। इसमें हमने चर्चा किए सभी हिस्से शामिल हैं, साथ ही कुछ उपयोगी टिप्पणी भी।

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Build sample DataTable (import datatable to excel)
        // -------------------------------------------------
        DataTable dataTable = new DataTable();
        dataTable.Columns.Add("Product", typeof(string));
        dataTable.Columns.Add("Price", typeof(double));
        dataTable.Rows.Add("Apple", 1.23);
        dataTable.Rows.Add("Banana", 0.78);
        dataTable.Rows.Add("Cherry", 2.50);
        // You can add as many rows as you like here.

        // -------------------------------------------------
        // Step 2: Create a new workbook (create excel workbook c#)
        // -------------------------------------------------
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // -------------------------------------------------
        // Step 3: Define a currency style (format cells currency)
        // -------------------------------------------------
        Style priceStyle = workbook.CreateStyle();
        priceStyle.Number = 164; // "$#,##0.00" – built‑in currency format

        // -------------------------------------------------
        // Step 4: Build the style array (apply currency format column)
        // -------------------------------------------------
        // First column gets default style (null), second column uses priceStyle.
        Style[] columnStyles = { null, priceStyle };

        // -------------------------------------------------
        // Step 5: Import the DataTable with the style array
        // -------------------------------------------------
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // -------------------------------------------------
        // Step 6: Save the workbook to disk
        // -------------------------------------------------
        string outputPath = @"YOUR_DIRECTORY\StyledTable.xlsx";
        workbook.Save(outputPath);

        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**अपेक्षित परिणाम:** `StyledTable.xlsx` खोलने पर `Price` कॉलम में डॉलर साइन और दो दशमलव स्थान दिखेंगे, बिल्कुल वही जैसा कि `format cells currency` निर्देश ने माँगा था।

---

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या यह .NET Core के साथ काम करता है?**  
उत्तर: बिल्कुल। Aspose.Cells .NET‑standard संगत है, इसलिए आप .NET 5, .NET 6 या बाद के संस्करणों को बिना बदलाव के टार्गेट कर सकते हैं।

**प्रश्न: यदि मेरे DataTable में 10 कॉलम हैं लेकिन मैं केवल कॉलम 5 को फ़ॉर्मेट करना चाहता हूँ तो?**  
उत्तर: लंबाई 10 की `Style[]` बनाएं, इंडेक्स 0‑4 और 6‑9 को `null` रखें, और कस्टम स्टाइल को इंडेक्स 4 (ज़ीरो‑बेस्ड) पर रखें। Aspose प्रत्येक एंट्री का सम्मान करेगा।

**प्रश्न: क्या मैं हेडर रो को छिपा सकता हूँ?**  
उत्तर: आयात के बाद `worksheet.Cells.Rows[0].Hidden = true;` सेट करें या `ImportDataTable` में `includeColumnNames` पैरामीटर को `false` पास करें।

---

## निष्कर्ष

हमने अभी **create Excel workbook C#**, एक `DataTable` आयात किया, और Aspose.Cells का उपयोग करके **currency format column** लागू किया। मुख्य चरण—डेटा तैयार करना, स्टाइल परिभाषित करना, स्टाइल एरे बनाना, `ImportDataTable` के साथ आयात करना, और सहेजना—ज्यादातर Excel‑ऑटोमेशन कार्यों की रीढ़ बनाते हैं।

अब आप आगे खोज सकते हैं:

- तिथियों या प्रतिशतों के लिए **add number format excel**  
- एक ही फ़ाइल में कई शीट्स एक्सपोर्ट करना  
- लोकैल‑विशिष्ट प्रतीकों के साथ **format cells currency**  
- समान डेटा पर आधारित चार्ट निर्माण को ऑटोमेट करना  

इनका प्रयोग करें, और आप अपनी टीम में Excel रिपोर्टिंग के लिए go‑to व्यक्ति बन जाएंगे। कोई ट्विस्ट शेयर करना चाहते हैं? नीचे कमेंट करें—हैप्पी कोडिंग!  

![create excel workbook c# screenshot](image.png "create excel workbook c#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}