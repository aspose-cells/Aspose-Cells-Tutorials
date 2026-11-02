---
category: general
date: 2026-03-22
description: फ़ॉर्मेटिंग के साथ Excel निर्यात कैसे करें और संख्या फ़ॉर्मेट को संरक्षित
  रखें। Excel रेंज को बदलना, फ़ॉर्मूला परिणाम प्राप्त करना, और Aspose.Cells का उपयोग
  करके फ़ॉर्मेटिंग के साथ Excel निर्यात करना सीखें।
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: hi
og_description: फ़ॉर्मेटिंग के साथ Excel को निर्यात कैसे करें और संख्या फ़ॉर्मेट को
  संरक्षित रखें। Excel रेंज को बदलने, फ़ॉर्मूला परिणाम प्राप्त करने, और C# में फ़ॉर्मेटिंग
  के साथ Excel को निर्यात करने के लिए चरण‑दर‑चरण गाइड।
og_title: फ़ॉर्मेटिंग के साथ Excel निर्यात कैसे करें – संख्या फ़ॉर्मेट को संरक्षित
  रखें
tags:
- C#
- Aspose.Cells
- Excel automation
title: फ़ॉर्मेटिंग के साथ Excel निर्यात कैसे करें – संख्या फ़ॉर्मेट को संरक्षित रखें
url: /hi/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को फ़ॉर्मेटिंग के साथ निर्यात कैसे करें – नंबर फ़ॉर्मेट बनाए रखें

क्या आपने कभी सोचा है **how to export Excel** डेटा को इस तरह निर्यात करने के बारे में, जबकि प्रत्येक सेल का रूप बिल्कुल वैसा ही रहे जैसा आप वर्कबुक में देखते हैं? शायद आपको क्लाइंट को रिपोर्ट भेजनी है, ग्रिड कंट्रोल को डेटा देना है, या सिर्फ मानों को डेटाबेस में संग्रहीत करना है। आम समस्या नंबर फ़ॉर्मेटिंग के खो जाने या फ़ॉर्मूले के कच्चे स्ट्रिंग में बदल जाने की होती है।  

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने योग्य C# उदाहरण के माध्यम से चलेंगे जो **preserves number format**, **converts an Excel range** को `DataTable` में बदलता है, **gets the formula result**, और अंत में Aspose.Cells का उपयोग करके **exports Excel with formatting** करता है। अंत तक आपके पास एक एकल मेथड होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं और वर्कशीट रेफ़रेंस के साथ कॉल कर सकते हैं।

> **त्वरित पूर्वावलोकन:** कोड एक वर्कबुक बनाता है, एक मान और एक फ़ॉर्मूला लिखता है, Aspose.Cells को बताता है कि सेल्स को फ़ॉर्मेटेड स्ट्रिंग्स के रूप में निर्यात करे, और `123.456 | 246.912` प्रिंट करता है – बिल्कुल वही जो आप Excel में देखना अपेक्षित करेंगे।

---

## आप क्या चाहिए

- **Aspose.Cells for .NET** (फ़्री ट्रायल सीखने के लिए पर्याप्त है)
- .NET 6.0 या बाद का (API .NET Framework पर भी समान है)
- एक बेसिक C# डेवलपमेंट एनवायरनमेंट (Visual Studio, VS Code, Rider… आप चुनें)

Aspose.Cells के अलावा कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है। यदि आपने अभी तक इसे इंस्टॉल नहीं किया है, तो चलाएँ:

```bash
dotnet add package Aspose.Cells
```

---

## चरण 1 – एक वर्कबुक बनाएं और मान लिखें (फ़ॉर्मूला सहित)

सबसे पहले हम एक नया वर्कबुक बनाते हैं और **A1** में एक संख्यात्मक मान डालते हैं। फिर हम **B1** में एक सरल फ़ॉर्मूला जोड़ते हैं जो पहले सेल को दो से गुणा करता है। यह बाद में **get formula result** दर्शाने के लिए मंच तैयार करता है।

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**क्यों यह महत्वपूर्ण है:**  
- `PutValue` कच्ची संख्या संग्रहीत करता है, जबकि `PutFormula` गणना संग्रहीत करता है।  
- Aspose.Cells फ़ॉर्मूला को **alive** रखता है, इसलिए जब हम बाद में सेल का मान पूछते हैं तो हमें वास्तव में `246.912` मिलेगा, न कि स्ट्रिंग `"=A1*2"`।

---

## चरण 2 – Aspose.Cells को बताएं कि मानों को फ़ॉर्मेटेड स्ट्रिंग्स के रूप में निर्यात करे

यदि आप केवल `ExportDataTable` को डिफ़ॉल्ट सेटिंग्स के साथ कॉल करते हैं, तो संख्यात्मक सेल्स उनके मूल `double` मानों के रूप में लौटाए जाएंगे। इससे किसी भी हजार विभाजक, मुद्रा प्रतीक, या कस्टम दशमलव स्थान हट जाता है जो आपने सेट किए हों। `ExportTableOptions` क्लास हमें **preserve number format** और **export as string** करने की अनुमति देती है।

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**मुख्य बिंदु:** `ExportNumberFormat = true` वह फ़्लैग है जो **preserve number format** को कार्यशील बनाता है। इसके बिना आप `"123.456"` और `"246.912"` को कच्चे नंबरों के रूप में देखेंगे, जो कोड में ठीक लग सकते हैं लेकिन जब आप डेटा को ऐसे UI में पेस्ट करेंगे जो Excel जैसा फ़ॉर्मेट अपेक्षित करता है, तो सही नहीं रहेगा।

---

## चरण 3 – निर्यातित डेटा को प्रिंट करें (सत्यापन)

अब जब हमारे पास फ़ॉर्मेटेड स्ट्रिंग्स से भरपूर `DataTable` है, तो चलिए सामग्री को कंसोल में डंप करते हैं। यह यह भी दर्शाता है कि हमने सफलतापूर्वक **get formula result** प्राप्त किया है बिना फ़ॉर्मूला को स्वयं मूल्यांकित किए।

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Running the program prints:

```
123.456 | 246.912
```

ध्यान दें कि दूसरी कॉलम **formula result** दिखा रही है, न कि फ़ॉर्मूला टेक्स्ट। यही वह चीज़ है जिसकी आपको **export Excel with formatting** करते समय डाउनस्ट्रीम प्रोसेसिंग के लिए आवश्यकता होती है।

---

## चरण 4 – बड़े Excel रेंज को बदलना (वैकल्पिक)

ऊपर दिया गया उदाहरण एक छोटे `A1:B1` स्लाइस को संभालता है, लेकिन वास्तविक दुनिया में अक्सर पूरे टेबल को निर्यात करने की आवश्यकता होती है। वही मेथड किसी भी आयताकार ब्लॉक के लिए काम करता है – बस `firstRow`, `firstColumn`, `totalRows`, और `totalColumns` आर्ग्यूमेंट्स को समायोजित करें।

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**प्रो टिप:** यदि आपकी शीट में पहले से ही हेडर रो है, तो `includeColumnNames` को `true` सेट करें। Aspose.Cells रेंज की पहली पंक्ति को कॉलम नामों के रूप में उपयोग करेगा, जो तब उपयोगी होता है जब आप बाद में `DataTable` को UI ग्रिड से बाइंड करते हैं।

---

## चरण 5 – सामान्य समस्याएँ और उन्हें कैसे टालें

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **संख्याओं से कॉमा या मुद्रा प्रतीक हट जाते हैं** | `ExportAsString` false है या `ExportNumberFormat` छोड़ा गया है | दोनों `ExportAsString = true` **और** `ExportNumberFormat = true` सेट करें। |
| **फ़ॉर्मूला सेल्स फ़ॉर्मूला टेक्स्ट लौटाते हैं** | आपने निर्यात से पहले `CalculateFormula` नहीं बुलाया (सिर्फ तब आवश्यक जब वर्कबुक ऑटो‑कैल्कुलेट पर सेट न हो) | या तो ऑटो‑कैल्कुलेट सक्षम करें (`workbook.CalculateFormula()`) या `ExportAsString` पर भरोसा करें जो मूल्यांकन को मजबूर करता है। |
| **हेडर डेटा रो के रूप में दिखते हैं** | `includeColumnNames` को `false` सेट किया गया है जबकि आपके रेंज में हेडर रो शामिल है | `includeColumnNames = true` सेट करें ताकि पहली पंक्ति को कॉलम नाम माना जाए। |
| **बड़े रेंज मेमोरी पर दबाव डालते हैं** | एक बार में पूरी शीट निर्यात करने से सब कुछ मेमोरी में लोड हो जाता है | डेटा को हिस्सों में निर्यात करें (जैसे, 500 पंक्तियों के समूह) और आवश्यक होने पर `DataTable`s को मर्ज करें। |

---

## चरण 6 – पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम है, `using` स्टेटमेंट्स से लेकर `Main` तक। इसे एक कंसोल ऐप में पेस्ट करें और **F5** दबाएँ – आपको फ़ॉर्मेटेड आउटपुट तुरंत दिखेगा।

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Expected output**

```
123.456 | 246.912

Press any key to exit...
```

यह पूरी **how to export excel** वर्कफ़्लो है, जिसमें फ़ॉर्मेटिंग बरकरार है, फ़ॉर्मूला परिणाम मूल्यांकित हुए हैं, और एक साफ़ `DataTable` तैयार है किसी भी .NET कंज्यूमर के लिए।

---

## निष्कर्ष

हमने सब कुछ कवर कर लिया है जो आपको **how to export Excel** डेटा को **preserving number format**, **converting an Excel range** को `DataTable` में बदलने, और **getting formula results** बिना अतिरिक्त पार्सिंग के चाहिए। मुख्य बात `ExportTableOptions` कॉन्फ़िगरेशन है – एक बार जब आप `ExportAsString` और `ExportNumberFormat` को `true` सेट कर देते हैं, तो Aspose.Cells आपके लिए भारी काम कर देता है।

- `DataTable` को WPF `DataGrid` या ASP.NET MVC व्यू में प्लग करें।  
- टेबल को CSV फ़ाइल में लिखें जबकि सटीक विज़ुअल प्रतिनिधित्व बरकरार रखें।  
- इस दृष्टिकोण को कई शीट्स या डायनामिक रेंजेज़ तक विस्तारित करें।

विभिन्न फ़ॉर्मेट्स (मुद्रा, प्रतिशत) और बड़े डेटा ब्लॉक्स के साथ प्रयोग करने में संकोच न करें। यदि आपको कोई अजीब व्यवहार मिलता है, तो **common pitfalls** तालिका को फिर से देखें – यह सबसे सामान्य समस्याओं को कवर करती है जब आप **export excel with formatting** करते हैं।

कोडिंग का आनंद लें, और आपकी निर्यातित स्प्रेडशीट्स हमेशा मूल जैसा ही पॉलिश्ड दिखें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}