---
category: general
date: 2026-05-04
description: C# का उपयोग करके कस्टम फ़ॉर्मेटिंग के साथ वर्कशीट रेंज निर्यात करें।
  कुछ आसान चरणों में एक्सेल रेंज को निर्यात करना और सेल निर्यात को कस्टमाइज़ करना
  सीखें।
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: hi
og_description: C# के साथ वर्कशीट रेंज निर्यात करें। यह गाइड दिखाता है कि कैसे एक्सेल
  रेंज को निर्यात करें और सेल निर्यात को तेज़ और विश्वसनीय तरीके से अनुकूलित करें।
og_title: C# में वर्कशीट रेंज निर्यात करें – पूर्ण प्रोग्रामिंग गाइड
tags:
- C#
- Excel
- Data Export
title: C# में वर्कशीट रेंज निर्यात करें – पूर्ण प्रोग्रामिंग गाइड
url: /hi/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में वर्कशीट रेंज निर्यात करें – पूर्ण प्रोग्रामिंग गाइड

क्या आपको कभी **वर्कशीट रेंज निर्यात** करने की ज़रूरत पड़ी, लेकिन डिफ़ॉल्ट आउटपुट वही नहीं था जो आप चाहते थे? आप अकेले नहीं हैं—कई डेवलपर्स इस समस्या का सामना करते हैं जब वे सेल्स के ब्लॉक को CSV या JSON फ़ाइल में निकालने की कोशिश करते हैं। अच्छी खबर? कुछ ही पंक्तियों के C# कोड से आप न केवल **excel range निर्यात** कर सकते हैं, बल्कि **सेल निर्यात को कस्टमाइज़** भी कर सकते हैं ताकि वह किसी भी डाउनस्ट्रीम फ़ॉर्मेट से मेल खाए।

इस ट्यूटोरियल में हम एक वास्तविक परिदृश्य को देखेंगे: Excel वर्कबुक से *A1:D10* रेंज के सेल्स को लेकर, प्रत्येक मान को ब्रैकेटेड स्ट्रिंग में बदलेंगे, और परिणाम को फ़ाइल में लिखेंगे। अंत तक आप बिल्कुल **वर्कशीट रेंज कैसे निर्यात करें** यह जान जाएंगे, साथ ही प्रत्येक सेल के प्रतिनिधित्व पर पूर्ण नियंत्रण के साथ, और कुछ उपयोगी टिप्स भी जो बाद में आपको मिल सकते हैं।

## आपको क्या चाहिए

- .NET 6 या बाद का संस्करण (कोड .NET Framework 4.7+ के साथ भी काम करता है)  
- **GemBox.Spreadsheet** NuGet पैकेज (या कोई भी लाइब्रेरी जो `ExportTableOptions` प्रदान करती हो; यहाँ दिखाया गया API GemBox से है)  
- C# सिंटैक्स की बुनियादी समझ – कुछ भी जटिल नहीं, बस सामान्य `using` स्टेटमेंट्स और ऑब्जेक्ट निर्माण  

यदि आपके पास ये सब है, तो आप शुरू करने के लिए तैयार हैं।

## चरण 1: एक्सपोर्ट विकल्प सेट करें – मुख्य नियंत्रण बिंदु  

सबसे पहले आपको एक `ExportTableOptions` इंस्टेंस बनाना है और इसे बताना है कि हर सेल को स्ट्रिंग के रूप में ट्रीट किया जाए। यह **excel range कैसे निर्यात करें** के लिए आधार है, जबकि डेटा टाइप को सुसंगत रखता है।

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*स्ट्रिंग निर्यात क्यों मजबूर करें?*  
जब आप बाद में प्रत्येक सेल को कस्टमाइज़ करेंगे, तो आप ब्रैकेट्स और संभवतः अन्य प्रतीक जोड़ेंगे। सब कुछ स्ट्रिंग के रूप में रखने से टाइप‑कन्वर्ज़न की आश्चर्यजनक स्थितियों से बचा जा सकता है (जैसे, डेट्स का सीरियल नंबर में बदलना)।

## चरण 2: CellExport इवेंट में हुक करें – प्रत्येक सेल को कस्टमाइज़ करना  

अब आता है मज़ेदार हिस्सा: **सेल निर्यात को कैसे कस्टमाइज़ करें**। GemBox हर उस सेल के लिए `CellExport` इवेंट उठाता है जो लिखे जाने वाला है। इसे हैंडल करके आप मान को ब्रैकेट्स में लपेट सकते हैं, प्रीफ़िक्स जोड़ सकते हैं, या पूरी तरह से सेल को स्किप भी कर सकते हैं।

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*प्रो टिप:* यदि आप केवल न्यूमेरिक सेल्स को बदलना चाहते हैं, तो ब्रैकेट्स लागू करने से पहले `e.Value.GetType()` चेक करें। यह छोटा गार्ड अनजाने में हेडर टेक्स्ट को बिगाड़ने से बचा सकता है।

## चरण 3: इच्छित रेंज निर्यात करें – मुख्य कार्रवाई  

विकल्प तैयार होने के बाद, आप `ExportTable` को कॉल करते हैं। यह मेथड वह वर्कबुक लेता है जिसे आपने लोड किया है, रेंज का एड्रेस, और अभी कॉन्फ़िगर किए गए विकल्प।

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

हमने जो ओवरलोड इस्तेमाल किया है वह सीधे फ़ाइल में लिखता है (डिफ़ॉल्ट रूप से CSV)। यदि आप इन‑मेमोरी स्ट्रिंग चाहते हैं, तो अंतिम आर्ग्यूमेंट को `StringWriter` से बदलें और बाद में परिणाम पढ़ें।

### पूर्ण कार्यशील उदाहरण

नीचे एक स्व-निहित कंसोल एप्लिकेशन है जिसे आप नई प्रोजेक्ट में पेस्ट करके तुरंत चला सकते हैं (सिर्फ फ़ाइल पाथ बदलें)।

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**अपेक्षित आउटपुट (CSV स्निपेट):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

* A1* से *D10* तक का हर सेल अब स्क्वायर ब्रैकेट्स में लिपटा हुआ है, ठीक वैसे ही जैसा हमने `CellExport` हैंडलर में परिभाषित किया था।

## सामान्य किनारे के मामलों को संभालना  

### 1. खाली सेल्स  
यदि कोई सेल खाली है, तो `e.Value` `null` होगा। स्ट्रिंग इंटरपोलेशन के साथ इसे फ़ॉर्मेट करने की कोशिश करने से एक्सेप्शन फेंका जाएगा। इसे इस तरह गार्ड करें:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. बड़ी रेंजेस  
मिलियन‑सँख्या की पंक्तियों को निर्यात करने से मेमोरी लिमिट्स पर असर पड़ सकता है। ऐसे में पूरे वर्कबुक को मेमोरी में लोड करने के बजाय आउटपुट को स्ट्रीम करें:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. विभिन्न डिलिमिटर  
CSV ही एकमात्र फ़ॉर्मेट नहीं है जो आपको चाहिए हो सकता है। `ExportTableOptions.CCsvSeparator` को बदलकर डिलिमिटर बदलें:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## अक्सर पूछे जाने वाले प्रश्न  

**प्रश्न: क्या यह .xlsx फ़ाइलों के साथ काम करता है जो Excel 365 द्वारा बनाई गई हैं?**  
बिल्कुल। GemBox आधुनिक OpenXML फ़ॉर्मेट को बिना अतिरिक्त कॉन्फ़िगरेशन के पढ़ता है।

**प्रश्न: क्या मैं एक साथ कई गैर‑सतत रेंजेस निर्यात कर सकता हूँ?**  
एक ही `ExportTable` कॉल से सीधे नहीं। प्रत्येक रेंज स्ट्रिंग (`"A1:D10"`, `"F1:H5"` आदि) पर लूप करें और आउटपुट को स्वयं कॉन्कैटेनेट करें।

**प्रश्न: यदि मुझे प्रत्येक कॉलम के लिए अलग फ़ॉर्मेट लागू करना हो तो क्या करें?**  
`CellExport` हैंडलर में आपके पास `e.ColumnIndex` उपलब्ध है। कॉलम‑विशिष्ट लॉजिक लागू करने के लिए `switch` स्टेटमेंट का उपयोग करें।

## समापन  

हमने **वर्कशीट रेंज कैसे निर्यात करें** को पूर्ण नियंत्रण के साथ कवर किया, `ExportTableOptions` का उपयोग करके **excel range निर्यात** दिखाया, और `CellExport` इवेंट के माध्यम से **सेल निर्यात को कस्टमाइज़** करने का तरीका बताया। पूरा समाधान कुछ दर्जन लाइनों के C# में है, फिर भी यह प्रोडक्शन‑ग्रेड परिदृश्यों के लिए पर्याप्त लचीला है।

अगले कदम? ब्रैकेट रैपर को JSON‑फ्रेंडली फ़ॉर्मेट से बदलें, या ऐसी कंडीशनल लॉजिक आज़माएँ जो छिपी हुई पंक्तियों को स्किप करे। आप सीधे `MemoryStream` में निर्यात करने का भी प्रयोग कर सकते हैं ताकि वेब‑API रिस्पॉन्स के लिए कोई अस्थायी फ़ाइल न बनानी पड़े।

यदि आप इस गाइड को फॉलो कर चुके हैं, तो अब आपके पास किसी भी वर्कशीट रेंज को ठीक उसी तरह निर्यात करने का एक ठोस, पुन: उपयोग योग्य पैटर्न है जैसा आप चाहते हैं। खुश कोडिंग, और यदि कोई समस्या आती है तो टिप्पणी करके बताएं!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}